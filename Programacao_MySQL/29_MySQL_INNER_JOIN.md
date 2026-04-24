## MySQL INNER JOIN

O comando **INNER JOIN** é um dos pilares fundamentais da linguagem SQL. Sua função principal é combinar linhas de duas ou mais tabelas baseando-se em uma coluna relacionada entre elas.

Diferente de outros tipos de junção, o `INNER JOIN` retorna **apenas as linhas que possuem valores correspondentes em ambas as tabelas**. Se uma linha em uma tabela não encontrar um par na outra através da condição especificada, ela será excluída do conjunto de resultados final.

### Sintaxe do INNER JOIN

Para realizar esta operação, utilizamos a cláusula `JOIN` acompanhada da palavra-chave `ON`, que define a lógica de "casamento" entre os dados.

```sql
SELECT table1.column1, table1.column2, table2.column1
FROM table1
INNER JOIN table2 ON table1.condition_column = table2.condition_column;
```

**Análise técnica:**
*   `SELECT`: Especificamos quais colunas desejamos recuperar (é boa prática prefixar com o nome da tabela para evitar ambiguidade).
*   `INNER JOIN`: Indica ao banco de dados que queremos fundir o conjunto A com o conjunto B.
*   `ON`: É o filtro relacional. Aqui, comparamos chaves (geralmente uma **Chave Primária** de uma tabela com uma **Chave Estrangeira** de outra) para garantir que apenas os dados vinculados sejam exibidos.

---

## Exemplo Prático: Relacionando Produtos e Categorias

Imagine um cenário de e-commerce onde temos uma tabela `Products` e uma tabela `Categories`. O ponto de intersecção entre elas é a coluna `CategoryID`.

**Tabela Products:**
| ProductID | ProductName | CategoryID | Price |
| :--- | :--- | :--- | :--- |
| 3 | Aniseed Syrup | 2 | 10.00 |

**Tabela Categories:**
| CategoryID | CategoryName | Description |
| :--- | :--- | :--- |
| 2 | Condiments | Sweet and savory sauces... |

Para exibir o nome do produto ao lado do nome de sua respectiva categoria, utilizamos o seguinte código:

```sql
SELECT Products.ProductID, Products.ProductName, Categories.CategoryName
FROM Products
INNER JOIN Categories ON Products.CategoryID = Categories.CategoryID;
```

**Resultado Esperado:** O SQL cruzará o `CategoryID` 2 das duas tabelas e retornará uma única linha contendo o ID, o nome do produto ("Aniseed Syrup") e o nome da categoria ("Condiments").

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_join_inner)

**Nota:** O `INNER JOIN` é restritivo por design. Se você tiver um produto que não possui uma categoria atribuída (valor `NULL`), ou uma categoria que não possui produtos vinculados, esses registros **não aparecerão** no resultado final.

---

## Combinando Múltiplas Tabelas

Em arquiteturas de banco de dados relacionais complexas, é comum precisarmos conectar mais de duas tabelas simultaneamente. Você pode encadear quantas cláusulas `INNER JOIN` forem necessárias para construir uma consulta robusta.

Exemplo de uma consulta que cruza Pedidos, Clientes e Transportadoras:

```sql
SELECT Orders.OrderID, Customers.CustomerName, Shippers.ShipperName
FROM Orders
INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID
INNER JOIN Shippers ON Orders.ShipperID = Shippers.ShipperID;
```

**Por que utilizar assim?** Ao encadear os joins, você transforma uma estrutura de dados normalizada (dividida em várias tabelas para evitar redundância) em um relatório unificado e legível. O banco de dados processa essas junções sequencialmente, garantindo a integridade referencial em cada etapa da consulta.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_join_inner2)

<br>

---

<p align="center">
  <a href="28_MySQL_Joins.md">⬅️ Anterior</a> | <a href="30_MySQL_LEFT_JOIN.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---