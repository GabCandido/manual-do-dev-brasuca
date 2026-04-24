## Stored Procedures no MySQL

Uma **Stored Procedure** (procedimento armazenado) é um bloco de código SQL pré-compilado que reside no servidor de banco de dados. Pense nela como uma "função" ou "método" dentro do seu banco de dados: em vez de enviar consultas complexas repetidamente a partir da sua aplicação, você encapsula essa lógica no banco e a invoca pelo nome.

### Por que utilizar Stored Procedures?

O uso estratégico de procedimentos traz benefícios fundamentais para arquiteturas de software escaláveis:

*   **Reutilização de Código:** Centralize a lógica de negócios. Diferentes aplicações (Web, Mobile, Desktop) podem chamar o mesmo procedimento, garantindo consistência.
*   **Desempenho Otimizado:** Como o SQL é pré-compilado, o motor do banco de dados não precisa analisar e otimizar o caminho de execução a cada chamada, reduzindo a latência.
*   **Segurança Reforçada:** Você pode conceder permissões de execução a um usuário específico sem permitir que ele acesse diretamente as tabelas subjacentes. Isso protege a integridade dos dados.
*   **Manutenção Simplificada:** Alterar a lógica de um processo de negócio requer a atualização apenas da Procedure, e não de dezenas de arquivos de código fonte na sua aplicação.

---

## Sintaxe de Criação

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

---

## Executando e Gerenciando Procedures

Após criar o procedimento, a execução é direta através do comando `CALL`.

### Execução
Para disparar a lógica armazenada, basta invocar o nome da procedure passando os valores dos parâmetros:

```sql
CALL procedure_name('valor1', 'valor2');
```

### Remoção
Se a procedure tornar-se obsoleta ou precisar de uma reescrita total, utilize o `DROP PROCEDURE`:

```sql
DROP PROCEDURE procedure_name;
```

**Dica de Arquiteto:** Para evitar erros de "procedimento não encontrado" em scripts de migração ou automação, utilize sempre a cláusula de segurança:

```sql
DROP PROCEDURE IF EXISTS procedure_name;
```

---

## Exemplo Prático: Filtragem de Clientes

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

---

## Procedures com múltiplos parâmetros

Você pode expandir a funcionalidade adicionando quantos parâmetros forem necessários, separando-os por vírgula na definição.

```sql
DELIMITER //

CREATE PROCEDURE GetCustomersByCity(
    @City VARCHAR(50),
    @PostalCode VARCHAR(10)
)
BEGIN
    SELECT * FROM Customers
    WHERE City = @City AND PostalCode = @PostalCode;
END //

DELIMITER ;
```

**Observação:** Ao utilizar múltiplos parâmetros, a ordem no comando `CALL` deve corresponder exatamente à ordem definida na assinatura da procedure.

Para executar esta versão com filtros duplos:

```sql
CALL GetCustomersByCity('London', 'WA1 1DP');
```

[🚀 Pratique este código](https://www.w3schools.com/mysql/mysql_stored_procedures.asp)

<br>

---

<p align="center">
  <a href="43_MySQL_Null_Functions.md">⬅️ Anterior</a> | <a href="45_MySQL_Comments.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---