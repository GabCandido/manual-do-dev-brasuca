## MySQL LEFT JOIN

O comando `LEFT JOIN` é uma ferramenta fundamental na manipulação de bancos de dados relacionais. Ele permite realizar consultas que preservam a integridade de uma tabela "principal" (esquerda), garantindo que todos os seus registros sejam retornados, independentemente de possuírem ou não uma correspondência em uma tabela secundária (direita).

Se não houver correspondência na tabela da direita, o MySQL preencherá essas colunas com **NULL**.

### Sintaxe do LEFT JOIN

A estrutura básica segue a lógica de selecionar colunas específicas e definir o ponto de união entre as tabelas.

```sql
SELECT table1.column1, table1.column2, table2.column1
FROM table1
LEFT JOIN table2
ON table1.condition_column = table2.condition_column;
```

**Nota:** A palavra-chave **ON** é o motor dessa operação; ela define a regra de negócio que conecta as tabelas, geralmente baseada em chaves primárias e chaves estrangeiras.

---

### Exemplo Prático: Clientes e Pedidos

Imagine um cenário de e-commerce onde temos a tabela `Customers` (Clientes) e a tabela `Orders` (Pedidos). Para identificar todos os clientes e seus respectivos pedidos (caso existam), utilizamos o `LEFT JOIN`.

```sql
SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
LEFT JOIN Orders
ON Customers.CustomerID = Orders.CustomerID
ORDER BY Customers.CustomerName;
```

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_join_left)

**Explicação:** Ao executar este código, você obterá uma lista de todos os clientes registrados. Se um cliente não realizou nenhum pedido, o campo `OrderID` aparecerá como **NULL**. Isso é vital em relatórios de análise de vendas, onde precisamos visualizar toda a base de clientes, inclusive aqueles que ainda não converteram uma compra.

---

### Insight de Negócio: Filtrando Registros sem Correspondência

Uma das aplicações mais úteis do `LEFT JOIN` é identificar itens "órfãos" ou registros sem relacionamento. Por exemplo, se quisermos listar apenas os clientes que **não realizaram nenhum pedido**, podemos filtrar o resultado buscando por valores `NULL`.

```sql
SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
LEFT JOIN Orders
ON Customers.CustomerID = Orders.CustomerID
WHERE Orders.CustomerID IS NULL;
```

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_join_left2)

**Observação:** Ao utilizar a cláusula `WHERE` com a condição `IS NULL` após um `LEFT JOIN`, estamos aplicando uma técnica comum em Business Intelligence para encontrar lacunas em processos de negócio, como clientes inativos ou produtos sem estoque cadastrado.

<br>

---

<p align="center">
  <a href="29_MySQL_INNER_JOIN.md">⬅️ Anterior</a> | <a href="31_MySQL_RIGHT_JOIN.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---