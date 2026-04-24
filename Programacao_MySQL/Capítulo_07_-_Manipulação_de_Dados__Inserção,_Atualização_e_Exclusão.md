# Capítulo 07 - Manipulação de Dados: Inserção, Atualização e Exclusão

A gestão eficaz de um banco de dados relacional vai muito além da simples recuperação de informações. Para que um sistema seja funcional e dinâmico, é necessário dominar a manipulação de registros — ou seja, a capacidade de criar, modificar e remover dados de forma precisa e segura. Neste capítulo, exploraremos as instruções fundamentais do SQL que compõem o ciclo de vida do dado: `INSERT`, `UPDATE` e `DELETE`, além de técnicas avançadas de migração e o tratamento de valores nulos.

## A instrução INSERT INTO no MySQL

A instrução **INSERT INTO** é o pilar fundamental para a persistência de dados. Sua função primordial é a criação de novos registros (linhas) dentro de uma tabela pré-existente. Sem ela, o banco de dados seria estático; é através do `INSERT` que alimentamos nossas aplicações com informações dinâmicas, como usuários, pedidos ou registros de logs.

Existem duas formas principais de estruturar esse comando, dependendo do seu objetivo e da sua familiaridade com o esquema da tabela.

### Sintaxe 1: Especificação de Colunas
Esta é a forma recomendada e mais segura para ambientes de produção. Ao listar as colunas explicitamente, você garante que o valor seja inserido no local correto, mesmo que a ordem das colunas no banco de dados seja alterada futuramente.

```sql
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);
```

### Sintaxe 2: Inserção Direta
Se você pretende preencher **todos** os campos da tabela em uma única operação, pode omitir os nomes das colunas. 

**Atenção:** Aqui a ordem é mandatória. Os valores devem respeitar rigorosamente a ordem em que as colunas foram definidas na criação da tabela (`CREATE TABLE`).

```sql
INSERT INTO table_name
VALUES (value1, value2, value3, ...);
```

### Exemplo Prático: Inserindo novos registros
Considere a tabela `Customers`. Para inserir um novo cliente sem especificar as colunas, garantindo que os valores correspondam à estrutura da tabela, utilizamos:

```sql
INSERT INTO Customers 
VALUES ('Cardinal', 'Tom B. Erichsen', 'Skagen 21', 'Stavanger', '4006', 'Norway');
```

**O que aconteceu aqui?** O MySQL mapeou cada valor para a respectiva coluna na ordem correta. Como resultado, o registro foi adicionado com sucesso.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_insert_all)

**Nota:** Observe que não inserimos um valor para `CustomerID`. Em bancos de dados modernos, utilizamos colunas **auto-increment** (auto-incremento), que geram identificadores únicos de forma automática a cada nova inserção, prevenindo erros de duplicidade.

### Inserindo dados em colunas específicas
Muitas vezes, você não possui informações para preencher todos os campos (ou alguns campos possuem valores padrão). Nesse caso, listamos apenas as colunas desejadas:

```sql
INSERT INTO Customers (CustomerName, City, Country)
VALUES ('Cardinal', 'Stavanger', 'Norway');
```

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_insert_columns)

### Inserção de múltiplas linhas (Bulk Insert)
Para otimizar o desempenho em cenários onde precisamos adicionar diversos registros simultaneamente, o MySQL permite o envio de múltiplos conjuntos de valores em um único comando, reduzindo o "overhead" de rede.

```sql
INSERT INTO Customers (CustomerName, ContactName, Address, City, PostalCode, Country)
VALUES
('Cardinal', 'Tom B. Erichsen', 'Skagen 21', 'Stavanger', '4006', 'Norway'),
('Greasy Burger', 'Per Olsen', 'Gateveien 15', 'Sandnes', '4306', 'Norway'),
('Tasty Tee', 'Finn Egan', 'Streetroad 19B', 'Liverpool', 'L1 0AA', 'UK');
```

**Observação:** Note que cada conjunto de valores é agrupado por parênteses e separado por uma vírgula.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_insert_multiple)

---

## O uso de INSERT INTO SELECT

Para casos onde precisamos mover dados entre tabelas de forma automatizada, a instrução **INSERT INTO SELECT** é uma ferramenta poderosa. Em vez de inserir registros manualmente, você utiliza o próprio motor do banco para copiar dados de uma tabela de origem (**source table**) e inseri-los em uma tabela de destino (**target table**), sendo essencial em rotinas de ETL e backups rápidos.

### Exemplos Práticos
Se a estrutura das tabelas for compatível, podemos mover grandes conjuntos de dados de uma vez:

```sql
INSERT INTO Customers (CustomerName, City, Country)
SELECT SupplierName, City, Country FROM Suppliers;
```

**Por que utilizar este método?** Ao processar a inserção no nível do servidor SQL, você reduz drasticamente o tráfego de rede e a carga na memória da sua aplicação, tornando a operação significativamente mais rápida.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_insert_into_select)

---

## Valores NULL no MySQL

No mundo dos bancos de dados relacionais, nem sempre temos todas as informações disponíveis. É aqui que entra o conceito de **NULL**. Um valor `NULL` representa dados desconhecidos, ausentes ou inaplicáveis.

**Nota:** `NULL` não é o mesmo que zero (0) ou uma string vazia (''). O `NULL` preserva a integridade semântica da sua base de dados, informando que a informação simplesmente não existe para aquele registro.

### Como testar Valores NULL?
Como o `NULL` representa uma ausência, ele não possui um valor comparável. Portanto, você **não pode** utilizar operadores de comparação comuns (`=`, `<>`, etc.). O SQL disponibiliza operadores específicos: `IS NULL` e `IS NOT NULL`.

#### Exemplo: IS NULL
Utilizamos para identificar lacunas nos dados.
```sql
SELECT CustomerName, ContactName, Address
FROM Customers
WHERE Address IS NULL;
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_is_null)

#### Exemplo: IS NOT NULL
Essencial quando você precisa garantir que está trabalhando apenas com registros que possuem dados concretos.
```sql
SELECT CustomerName, ContactName, Address
FROM Customers
WHERE Address IS NOT NULL;
```

---

## Atualizando Registros com o comando UPDATE

Quando precisamos modificar dados existentes, utilizamos o comando **UPDATE**. Ele permite que o estado do banco de dados reflita mudanças necessárias, como a alteração de um endereço ou status de um pedido.

### Sintaxe e Segurança
A estrutura básica define a tabela, os novos valores e o filtro de segurança:

```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

**Nota:** Tenha extrema cautela ao utilizar o `UPDATE`. A cláusula `WHERE` especifica exatamente quais registros devem ser atualizados. **Se você omitir a cláusula WHERE, todos os registros da tabela serão alterados.**

### Exemplo de Atualização
Para atualizar dados de um cliente específico via `PRIMARY KEY`:

```sql
UPDATE Customers
SET ContactName = 'Alfred Schmidt', City = 'Frankfurt'
WHERE CustomerID = 1;
```

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_update)

---

## Exclusão de dados com o comando DELETE

A instrução **DELETE** é a ferramenta utilizada para remover registros de uma tabela. Assim como no `UPDATE`, a precisão aqui é vital para a integridade dos dados.

### Sintaxe do DELETE
```sql
DELETE FROM nome_da_tabela 
WHERE condicao;
```

O MySQL avalia cada linha conforme a cláusula `WHERE`. Se a linha atender ao critério, ela será permanentemente removida.

### Exemplo Prático
```sql
DELETE FROM Customers
WHERE CustomerName = 'Alfreds Futterkiste';
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_delete)

### Diferença entre DELETE e DROP
*   **`DELETE`**: Remove registros linha a linha, mantendo a estrutura da tabela intacta.
*   **`DROP TABLE`**: Apaga a tabela completamente do dicionário de dados. Não sobram vestígios.

**Dica de Arquitetura:** Em sistemas críticos, prefira utilizar "Soft Deletes" (uma coluna `is_deleted` ou `status`) em vez de deletar registros fisicamente. Isso permite auditoria e recuperação de dados excluídos acidentalmente por usuários.

<br>

---

<p align="center">
  <a href="Capítulo_06_-_Operadores_Lógicos_e_Expressões.md">⬅️ Anterior</a> | <a href="Capítulo_08_-_Funções_de_Agregação_e_Resumo_de_Dados.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---