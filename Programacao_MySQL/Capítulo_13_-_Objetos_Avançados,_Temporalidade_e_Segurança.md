# Capítulo 13 - Objetos Avançados, Temporalidade e Segurança

Neste capítulo, exploraremos os mecanismos que elevam o desenvolvimento de banco de dados do nível de simples consultas para uma arquitetura robusta e profissional. Discutiremos como encapsular lógica com **Stored Procedures** e **Views**, gerenciar com precisão dados temporais e, fundamentalmente, como proteger suas aplicações contra as vulnerabilidades mais críticas do mundo SQL.

---

## Stored Procedures no MySQL

Uma **Stored Procedure** (procedimento armazenado) é um bloco de código SQL pré-compilado que reside no servidor de banco de dados. Pense nela como uma "função" ou "método" dentro do seu banco de dados: em vez de enviar consultas complexas repetidamente a partir da sua aplicação, você encapsula essa lógica no banco e a invoca pelo nome.

### Por que utilizar Stored Procedures?

O uso estratégico de procedimentos traz benefícios fundamentais para arquiteturas de software escaláveis:

*   **Reutilização de Código:** Centralize a lógica de negócios. Diferentes aplicações (Web, Mobile, Desktop) podem chamar o mesmo procedimento, garantindo consistência.
*   **Desempenho Otimizado:** Como o SQL é pré-compilado, o motor do banco de dados não precisa analisar e otimizar o caminho de execução a cada chamada, reduzindo a latência.
*   **Segurança Reforçada:** Você pode conceder permissões de execução a um usuário específico sem permitir que ele acesse diretamente as tabelas subjacentes. Isso protege a integridade dos dados.
*   **Manutenção Simplificada:** Alterar a lógica de um processo de negócio requer a atualização apenas da Procedure, e não de dezenas de arquivos de código fonte na sua aplicação.

### Sintaxe de Criação

Para definir um procedimento, utilizamos a palavra-chave `DELIMITER`. O MySQL precisa de um delimitador customizado (como `//`) para não confundir o ponto-e-vírgula (`;`) interno do procedimento com o comando de finalização da criação.

```sql
DELIMITER //

CREATE PROCEDURE procedure_name(
    @param1 datatype,
    @param2 datatype
)
BEGIN
    -- Lógica SQL aqui
    SELECT column1, column2
    FROM table_name
    WHERE columnN = @paramN;
END //

DELIMITER ;
```

**Nota:** O `DELIMITER //` altera temporariamente o terminador de comandos, permitindo que o bloco `BEGIN...END` seja lido como uma única unidade lógica pelo servidor.

### Executando e Gerenciando Procedures

Após criar o procedimento, a execução é direta através do comando `CALL`.

**Execução:**
Para disparar a lógica armazenada, basta invocar o nome da procedure passando os valores dos parâmetros:

```sql
CALL procedure_name('valor1', 'valor2');
```

**Remoção:**
Se a procedure tornar-se obsoleta ou precisar de uma reescrita total, utilize o `DROP PROCEDURE`.

**Dica de Arquiteto:** Para evitar erros de "procedimento não encontrado" em scripts de migração ou automação, utilize sempre a cláusula de segurança:

```sql
DROP PROCEDURE IF EXISTS procedure_name;
```

### Exemplo Prático: Filtragem de Clientes

Vamos criar um procedimento para extrair clientes de uma cidade específica. Isso evita que o código da aplicação contenha a estrutura da query `SELECT`, mantendo a camada de dados isolada.

```sql
DELIMITER //

CREATE PROCEDURE GetCustomersByCity(
    @City VARCHAR(50)
)
BEGIN
    SELECT * FROM Customers
    WHERE City = @City;
END //

DELIMITER ;
```

[🚀 Pratique este código](https://www.w3schools.com/mysql/mysql_stored_procedures.asp)

Agora, basta executar o comando abaixo para obter os resultados de 'London':

```sql
CALL GetCustomersByCity('London');
```

Você também pode expandir a funcionalidade adicionando múltiplos parâmetros, separados por vírgula. Ao utilizar múltiplos parâmetros, a ordem no comando `CALL` deve corresponder exatamente à ordem definida na assinatura da procedure.

---

## Trabalhando com Datas no MySQL

O gerenciamento de dados temporais é um dos pilares fundamentais em sistemas de banco de dados relacionais. A precisão em consultas que envolvem tempo é o que separa um relatório financeiro exato de um erro de conformidade. No MySQL, o desafio central reside na **consistência de formatos**.

### Tipos de Dados de Data

A escolha correta entre os tipos de dados define a performance da sua indexação:

*   **`DATE`**: Armazena apenas a data (`YYYY-MM-DD`).
*   **`DATETIME`**: Armazena data e hora (`YYYY-MM-DD HH:MI:SS`).
*   **`TIMESTAMP`**: Similar ao `DATETIME`, mas sensível ao fuso horário (Timezone).
*   **`TIME`**: Armazena apenas o tempo (`HH:MI:SS`).
*   **`YEAR`**: Armazena apenas o ano.

**Observação:** Alterar o tipo de dado de uma coluna em tabelas com milhões de registros pode ser uma operação extremamente onerosa.

### O Desafio da Precisão

Em sistemas reais, colunas do tipo `DATETIME` costumam incluir horas, minutos e segundos. O MySQL busca uma equivalência exata. Se você tentar filtrar `2025-11-11` em uma coluna que contém `2025-11-11 13:23:44`, a consulta retornará um conjunto vazio, pois o banco interpreta a data simples como `00:00:00`.

**Dica de Arquiteto:** Para manter suas queries simples, evite incluir o componente de tempo em colunas onde apenas a data é necessária. O excesso de precisão não utilizado gera ruído na lógica de negócio e dificulta a indexação.

---

## MySQL Views

Uma **View** (ou exibição) é uma tabela virtual definida por uma consulta SQL. Diferente de uma tabela comum, ela não armazena os dados fisicamente; ela armazena a estrutura da consulta (`SELECT`). Sempre que acessada, o banco executa a consulta em tempo real.

### Por que usar Views?
*   **Simplificação:** Oculta `JOINs` complexos por trás de um nome simples.
*   **Segurança:** Exponha apenas colunas específicas para determinados usuários.
*   **Consistência:** Garante que toda a equipe utilize a mesma lógica de cálculo (ex: preços com desconto).

Para criar uma visualização, utilizamos o comando `CREATE VIEW`:

```sql
CREATE VIEW brazil_customers_view AS
SELECT CustomerName, ContactName
FROM Customers
WHERE Country = 'Brazil';
```

**Nota:** Como a view é uma "janela" para os dados, ela reflete sempre o estado atual das tabelas base. Se precisar alterar a estrutura, utilize `CREATE OR REPLACE VIEW`. Para remover uma view sem afetar os dados originais, utilize `DROP VIEW`.

---

## Segurança: SQL Injection e Prepared Statements

A **SQL Injection** é uma técnica de exploração onde um atacante insere comandos SQL maliciosos em campos de entrada. Isso ocorre quando dados de usuário são concatenados diretamente em uma *string* de consulta sem tratamento.

### O Perigo da Lógica "Sempre Verdadeira"
Se um atacante inserir `' OR 1=1` em um campo de busca, a consulta resultante pode ignorar filtros e retornar toda a tabela de usuários, expondo dados confidenciais. Em cenários mais críticos, o atacante pode usar comandos em lote (`SELECT * FROM Users; DROP TABLE Suppliers;`) para destruir estruturas de dados.

### A Solução: Prepared Statements

As **Prepared Statements** funcionam como um modelo de consulta pré-compilado, separando a estrutura da query dos dados.

1. **Prepare:** O banco analisa e otimiza a query com *placeholders* (`?`).
2. **Execute:** A aplicação envia apenas os valores, que são tratados estritamente como dados, nunca como código executável.

**Exemplo em PHP:**

```php
// Modelo da consulta SQL com placeholders (?)
$sql = "INSERT INTO MyGuests (firstname, lastname, email) VALUES (?, ?, ?)";

// Preparação e vinculação
if($stmt = $conn->prepare($sql)) {
  $stmt->bind_param("sss", $firstname, $lastname, $email);

  $firstname = "John";
  $lastname = "Doe";
  $email = "john@example.com";
  $stmt->execute();
}
```

[🚀 Pratique este código](https://www.w3schools.com/php/php_mysql_prepared_statements.asp)

**Nota:** Embora as *Prepared Statements* sejam uma barreira de segurança poderosa, a **sanitização** e a **validação** dos dados na origem continuam sendo boas práticas indispensáveis no desenvolvimento web profissional.

<br>

---

<p align="center">
  <a href="Capítulo_12_-_Lógica_de_Conjuntos_e_Expressões_Condicionais.md">⬅️ Anterior</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---