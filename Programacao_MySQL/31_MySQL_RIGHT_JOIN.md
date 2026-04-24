## MySQL RIGHT JOIN

O comando **RIGHT JOIN** é uma ferramenta fundamental em bancos de dados relacionais para o resgate de informações que possuem dependência hierárquica ou de referência. Sua função principal é retornar **todos os registros da tabela à direita** (`table2`) e apenas as linhas correspondentes da tabela à esquerda (`table1`).

Quando não há uma correspondência na tabela à esquerda para um determinado registro da tabela à direita, o MySQL preencherá as colunas resultantes da tabela à esquerda com o valor `NULL`.

### Sintaxe do RIGHT JOIN

A estrutura básica utiliza a cláusula `ON` para definir o critério de junção entre as colunas relacionadas.

```sql
SELECT table1.column1, table1.column2, table2.column1
FROM table1
RIGHT JOIN table2
ON table1.condition_column = table2.condition_column;
```

**Nota:** O uso do `ON` é obrigatório para especificar a condição de correspondência (geralmente uma chave estrangeira ligada a uma chave primária). O `RIGHT JOIN` prioriza a integridade da tabela listada após o comando `JOIN`.

---

## Cenário de Estudo: Base de Dados Northwind

Para entender o comportamento deste comando no mundo real, utilizaremos a base de dados *Northwind*. Vamos imaginar uma relação entre **Orders** (Pedidos) e **Employees** (Funcionários).

**Tabela: Orders (Seleção)**

| OrderID | CustomerID | EmployeeID | OrderDate | ShipperID |
| :--- | :--- | :--- | :--- | :--- |
| 10308 | 2 | 7 | 1996-09-18 | 3 |
| 10309 | 37 | 3 | 1996-09-19 | 1 |
| 10310 | 77 | 8 | 1996-09-20 | 2 |

**Tabela: Employees (Seleção)**

| EmployeeID | LastName | FirstName | BirthDate | Photo |
| :--- | :--- | :--- | :--- | :--- |
| 1 | Davolio | Nancy | 1968-12-08 | EmpID1.pic |
| 2 | Fuller | Andrew | 1952-02-19 | EmpID2.pic |
| 3 | Leverling | Janet | 1963-08-30 | EmpID3.pic |

Aqui, a coluna de relação entre as duas tabelas é `EmployeeID`.

---

## Exemplo Prático: Listando Funcionários e seus Pedidos

O código abaixo busca todos os registros da tabela `Employees` (a "tabela da direita") e, caso existam, vincula os registros correspondentes da tabela `Orders`.

```sql
SELECT Orders.OrderID, Employees.LastName, Employees.FirstName
FROM Orders
RIGHT JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID
ORDER BY Orders.OrderID;
```

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_join_right)

**O que esperar deste resultado?**
Diferente de um `INNER JOIN` (que excluiria funcionários que ainda não realizaram pedidos), o `RIGHT JOIN` garante que **todos os funcionários** da tabela `Employees` aparecerão na lista. Se um funcionário ainda não tiver nenhum `OrderID` associado, o valor na coluna `OrderID` será exibido como `NULL`, permitindo que você identifique rapidamente quais colaboradores ainda não processaram vendas ou pedidos.

**Observação técnica:** No desenvolvimento de sistemas de gestão, utilizamos o `RIGHT JOIN` principalmente para auditoria e relatórios de completude, onde é vital não omitir entidades (como funcionários ou produtos) mesmo quando não há transações associadas a eles no momento da consulta.

<br>

---

<p align="center">
  <a href="30_MySQL_LEFT_JOIN.md">⬅️ Anterior</a> | <a href="32_MySQL_CROSS_JOIN.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---