## A Declaração MySQL GROUP BY

A cláusula **GROUP BY** é uma ferramenta fundamental em SQL, utilizada para organizar dados em conjuntos baseados em colunas específicas. Sua função principal é agrupar linhas que possuem valores idênticos, permitindo que você condense informações detalhadas em "linhas de resumo".

Em cenários reais de análise de dados, o `GROUP BY` é indispensável para responder a perguntas de negócio, como: "Quantos pedidos cada cliente realizou?" ou "Qual o faturamento total por categoria de produto?".

**Nota:** A declaração `GROUP BY` é quase sempre utilizada em conjunto com **funções de agregação** (como `COUNT()`, `MAX()`, `MIN()`, `SUM()` e `AVG()`), que realizam cálculos matemáticos ou estatísticos sobre cada grupo formado.

---

### Sintaxe do GROUP BY

Para utilizar o agrupamento, você deve selecionar as colunas que deseja agrupar ou agregar e definir a lógica de filtragem, se necessário.

```sql
SELECT column1, aggregate_function(column2), column3, ...
FROM table_name
WHERE condition
GROUP BY column1, column3
ORDER BY column_name;
```

**Explicação técnica:**
- **`SELECT`**: Define as colunas que serão retornadas. Lembre-se: qualquer coluna listada no `SELECT` que não seja um argumento de uma função de agregação deve obrigatoriamente estar presente no `GROUP BY`.
- **`GROUP BY`**: Define o critério de agrupamento. O motor do banco de dados irá varrer a tabela e criar "baldes" (grupos) para cada valor único encontrado nas colunas especificadas.
- **`ORDER BY`**: Opcional, mas útil para apresentar os resultados agrupados de forma organizada (ex: do maior para o menor).

---

### Exemplos práticos

#### 1. Contando registros por categoria
Se quisermos saber quantos clientes existem em cada país, o SQL agrupará todos os registros que compartilham o mesmo valor na coluna `Country` e aplicará a função `COUNT()` sobre eles.

```sql
SELECT Country, COUNT(CustomerID) AS "Number of Customers"
FROM Customers
GROUP BY Country;
```

*Resultado esperado:* Uma lista de países acompanhada do total de registros associados a cada um.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_groupby)

#### 2. Ordenando resultados agregados
Podemos combinar o agrupamento com a ordenação para destacar os dados mais relevantes, como ver os países com a maior base de clientes no topo:

```sql
SELECT Country, COUNT(CustomerID) AS "Number of Customers"
FROM Customers
GROUP BY Country
ORDER BY COUNT(CustomerID) DESC;
```

*Resultado esperado:* O mesmo conjunto de dados do exemplo anterior, porém reordenado em ordem decrescente (`DESC`) com base no valor da contagem.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_groupby_orderby)

---

### GROUP BY com JOIN

O verdadeiro poder do `GROUP BY` brilha quando precisamos consolidar dados de múltiplas tabelas. Ao realizar um `JOIN`, podemos agrupar informações relacionadas em tabelas distintas para gerar relatórios complexos.

**Exemplo:** Listar a quantidade de pedidos processados por cada transportadora:

```sql
SELECT Shippers.ShipperName, COUNT(Orders.OrderID) AS "Number of Orders"
FROM Orders
LEFT JOIN Shippers ON Orders.ShipperID = Shippers.ShipperID
GROUP BY ShipperName;
```

**Por que isso funciona?**
O `LEFT JOIN` combina as tabelas de pedidos e transportadoras. O `GROUP BY ShipperName` garante que, para cada transportadora, o SQL conte apenas os pedidos vinculados ao seu ID, tratando a transportadora como o "pilar" central da agregação.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_groupby1)

<br>

---

<p align="center">
  <a href="35_MySQL_UNION_ALL.md">⬅️ Anterior</a> | <a href="37_MySQL_HAVING.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---