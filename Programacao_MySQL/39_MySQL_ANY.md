## O Operador ANY no MySQL

O operador **ANY** é uma ferramenta poderosa de lógica relacional usada para comparar um valor único com uma lista de valores retornada por uma **subquery** (subconsulta).

Em cenários de desenvolvimento de sistemas, muitas vezes precisamos verificar se um registro específico possui alguma relação com um conjunto de dados em outra tabela. O `ANY` simplifica essa verificação ao retornar `TRUE` caso a condição especificada seja atendida por **pelo menos um** dos elementos resultantes da subconsulta.

### Sintaxe

A estrutura básica utiliza um operador de comparação padrão para validar a relação entre a coluna principal e o conjunto retornado:

```sql
SELECT column_name(s)
FROM table_name
WHERE column_name operator ANY (subquery);
```

**Nota:** O `operator` deve ser um operador de comparação padrão, como `=`, `<>`, `!=`, `>`, `>=`, `<`, ou `<=`.

---

## Banco de Dados de Demonstração

Para ilustrar o uso, considere as seguintes tabelas extraídas do banco de dados de exemplo *Northwind*:

**Tabela: Products**

| ProductID | ProductName | Price |
| :--- | :--- | :--- |
| 1 | Chais | 18.00 |
| 2 | Chang | 19.00 |
| 3 | Aniseed Syrup | 10.00 |
| 4 | Chef Anton's Cajun Seasoning | 22.00 |

**Tabela: OrderDetails**

| OrderDetailID | ProductID | Quantity |
| :--- | :--- | :--- |
| 1 | 11 | 12 |
| 2 | 42 | 10 |
| 3 | 72 | 5 |
| 4 | 14 | 9 |

---

## Exemplos Práticos de Uso

O `ANY` atua como um filtro que "escuta" o resultado da subconsulta. Se qualquer uma das linhas da subconsulta satisfizer o critério, a linha da tabela externa é incluída no resultado final.

### 1. Verificando a existência de uma quantidade específica
Neste exemplo, buscamos nomes de produtos onde o `ProductID` exista em uma lista de pedidos que tiveram exatamente a quantidade 10.

```sql
SELECT ProductName 
FROM Products
WHERE ProductID = ANY (
  SELECT ProductID 
  FROM OrderDetails 
  WHERE Quantity = 10
);
```
**Resultado esperado:** A query retornará os nomes dos produtos cuja ID esteja presente na subconsulta. Se houver qualquer `OrderDetail` com `Quantity = 10`, o `ANY` retorna verdadeiro para esse `ProductID`.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_any)

### 2. Comparação de maior valor (Threshold)
Podemos usar o `ANY` para identificar itens que superam certos limites definidos em outras tabelas. Aqui, buscamos produtos que foram vendidos em quantidades superiores a 99.

```sql
SELECT ProductName 
FROM Products
WHERE ProductID = ANY (
  SELECT ProductID 
  FROM OrderDetails 
  WHERE Quantity > 99
);
```
**Resultado esperado:** O SQL varrerá a tabela `OrderDetails`. Se encontrar qualquer registro com `Quantity > 99`, o `ANY` validará a condição para os produtos relacionados, retornando seus nomes.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_any2)

### 3. Cenário com resultado falso
O `ANY` avalia para `FALSE` se nenhuma linha da subconsulta atender à condição.

```sql
SELECT ProductName 
FROM Products
WHERE ProductID = ANY (
  SELECT ProductID 
  FROM OrderDetails 
  WHERE Quantity > 1000
);
```
**Resultado esperado:** Como não existem registros na tabela `OrderDetails` onde a `Quantity` seja superior a 1000, a subconsulta retorna um conjunto vazio, resultando em um retorno de consulta nulo para a query principal.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_any3)

<br>

---

<p align="center">
  <a href="38_MySQL_EXISTS.md">⬅️ Anterior</a> | <a href="40_MySQL_ALL.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---