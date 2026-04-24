## A Cláusula HAVING no MySQL

A cláusula **HAVING** foi introduzida no SQL porque a cláusula **WHERE** não pode ser utilizada com **funções de agregação** (como `COUNT()`, `SUM()`, `AVG()`, etc.).

Quando trabalhamos com bancos de dados, frequentemente precisamos realizar cálculos sobre grupos de dados. Enquanto o `WHERE` atua na filtragem de linhas individuais *antes* de qualquer agrupamento ocorrer, o `HAVING` atua na filtragem de grupos *após* a agregação ter sido processada. 

Em termos de performance e lógica, pense no `WHERE` como um filtro de "pré-processamento" e no `HAVING` como um refinamento "pós-processamento".

### Sintaxe da cláusula HAVING

A estrutura segue uma ordem rígida no SQL, garantindo que o motor do banco de dados saiba exatamente quando aplicar a lógica de conjunto.

```sql
SELECT column1, aggregate_function(column2), column3, ...
FROM table_name
WHERE condition
GROUP BY column1, column3
HAVING condition -- A condição aplicada sobre os dados agrupados
ORDER BY column_name;
```

**Nota:** A cláusula `HAVING` deve sempre aparecer após o `GROUP BY` e antes do `ORDER BY`.

---

### Exemplo Prático: Filtrando Grupos

Imagine que você precisa extrair um relatório de quantos clientes existem em cada país, mas o seu objetivo de negócio é focar apenas em mercados consolidados, ou seja, países com mais de 5 clientes.

```sql
SELECT Country, COUNT(CustomerID) AS "Number of Customers"
FROM Customers
GROUP BY Country
HAVING COUNT(CustomerID) > 5;
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_having)

**Explicação:** O `GROUP BY Country` cria subconjuntos de clientes baseados em sua localização. O `HAVING` então avalia o resultado da função `COUNT` para cada um desses subconjuntos, descartando qualquer grupo que não atenda ao critério numérico.

---

### Combinando Filtros: WHERE, GROUP BY e HAVING

Você pode combinar a precisão do `WHERE` com o poder do `HAVING` na mesma consulta. 

Veja o cenário abaixo: queremos contar quantos pedidos foram realizados por dois vendedores específicos ("Davolio" ou "Fuller"), mas apenas se esses funcionários tiverem registrado mais de 25 pedidos no total.

```sql
SELECT Employees.LastName, COUNT(Orders.OrderID) AS NumberOfOrders
FROM Orders
INNER JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID
WHERE LastName = 'Davolio' OR LastName = 'Fuller'
GROUP BY LastName
HAVING COUNT(Orders.OrderID) > 25;
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_having_where)

**Por que esta ordem funciona?**
1. **WHERE:** O motor filtra as linhas da tabela `Employees` para manter apenas "Davolio" e "Fuller".
2. **JOIN:** Os dados são combinados com a tabela de pedidos (`Orders`).
3. **GROUP BY:** Os dados filtrados são agrupados pelos nomes dos funcionários.
4. **HAVING:** Após a contagem dos pedidos de cada um, o sistema descarta os grupos que não superam a marca de 25 registros.

**Observação:** O uso correto destas cláusulas é fundamental para evitar o processamento desnecessário de dados que não serão exibidos no resultado final, otimizando o tempo de resposta da sua aplicação.

<br>

---

<p align="center">
  <a href="36_MySQL_GROUP_BY.md">⬅️ Anterior</a> | <a href="38_MySQL_EXISTS.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---