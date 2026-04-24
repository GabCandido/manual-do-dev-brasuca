# Capítulo 10 - Relatórios e Agrupamentos de Dados

Para transformar dados brutos em decisões estratégicas, o SQL oferece ferramentas poderosas de sumarização. Neste capítulo, exploraremos como organizar informações, filtrar grupos de dados e garantir a integridade dos seus relatórios ao lidar com valores ausentes.

## A Declaração MySQL GROUP BY

A cláusula **GROUP BY** é uma ferramenta fundamental em SQL, utilizada para organizar dados em conjuntos baseados em colunas específicas. Sua função principal é agrupar linhas que possuem valores idênticos, permitindo que você condense informações detalhadas em "linhas de resumo".

Em cenários reais de análise de dados, o `GROUP BY` é indispensável para responder a perguntas de negócio, como: "Quantos pedidos cada cliente realizou?" ou "Qual o faturamento total por categoria de produto?".

**Nota:** A declaração `GROUP BY` é quase sempre utilizada em conjunto com **funções de agregação** (como `COUNT()`, `MAX()`, `MIN()`, `SUM()` e `AVG()`), que realizam cálculos matemáticos ou estatísticos sobre cada grupo formado.

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
*   **`SELECT`**: Define as colunas que serão retornadas. Lembre-se: qualquer coluna listada no `SELECT` que não seja um argumento de uma função de agregação deve obrigatoriamente estar presente no `GROUP BY`.
*   **`GROUP BY`**: Define o critério de agrupamento. O motor do banco de dados irá varrer a tabela e criar "baldes" (grupos) para cada valor único encontrado nas colunas especificadas.
*   **`ORDER BY`**: Opcional, mas útil para apresentar os resultados agrupados de forma organizada (ex: do maior para o menor).

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

---

## A Cláusula HAVING no MySQL

Após agruparmos os dados, frequentemente precisamos filtrar esses grupos. É aqui que entra a cláusula **HAVING**. Ela foi introduzida no SQL porque a cláusula **WHERE** não pode ser utilizada diretamente com **funções de agregação** (como `COUNT()`, `SUM()`, `AVG()`, etc.).

Enquanto o `WHERE` atua na filtragem de linhas individuais *antes* de qualquer agrupamento ocorrer, o `HAVING` atua na filtragem de grupos *após* a agregação ter sido processada. 

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

### Combinando Filtros: WHERE, GROUP BY e HAVING

Você pode combinar a precisão do `WHERE` com o poder do `HAVING` na mesma consulta. Veja o cenário abaixo, onde contamos pedidos de vendedores específicos ("Davolio" ou "Fuller"), mas apenas se tiverem registrado mais de 25 pedidos:

```sql
SELECT Employees.LastName, COUNT(Orders.OrderID) AS NumberOfOrders
FROM Orders
INNER JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID
WHERE LastName = 'Davolio' OR LastName = 'Fuller'
GROUP BY LastName
HAVING COUNT(Orders.OrderID) > 25;
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_having_where)

**Observação:** O uso correto destas cláusulas é fundamental para evitar o processamento desnecessário de dados que não serão exibidos, otimizando o tempo de resposta da sua aplicação.

---

## Lidando com Valores NULL em Relatórios

A precisão de um relatório depende diretamente da qualidade dos dados. Em ambientes de banco de dados, é comum encontrar lacunas. O valor `NULL` representa a **ausência de dados** ou uma informação desconhecida. 

**Nota:** Um valor `NULL` não é o mesmo que zero (0) ou uma string vazia (""). Quando você realiza uma operação matemática envolvendo `NULL`, o resultado resultante será, invariavelmente, `NULL`. Isso pode quebrar cálculos financeiros e dashboards se não for tratado adequadamente.

### A Função COALESCE()

A função `COALESCE()` é o padrão recomendado pela linguagem SQL para lidar com valores ausentes. Ela avalia uma lista de argumentos e retorna o primeiro valor que **não seja NULL**.

```sql
SELECT ProductName, Price * (InStock + COALESCE(InOrder, 0))
FROM Products;
```

**Explicação:** Aqui, instruímos o banco de dados a considerar `0` caso o campo `InOrder` seja `NULL`, garantindo que a operação aritmética prossiga com um número válido.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_func_mysql_coalesce)

### A Função IFNULL()

A função `IFNULL()` é uma alternativa específica do MySQL que aceita dois argumentos: a expressão a ser testada e o valor substituto.

```sql
SELECT ProductName, Price * (InStock + IFNULL(InOrder, 0))
FROM Products;
```

**Observação:** Embora o `IFNULL` seja simples para o MySQL, o uso de `COALESCE` é considerado uma **boa prática de arquitetura**, pois torna seu código SQL compatível com outros sistemas de banco de dados, como PostgreSQL ou SQL Server.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_func_mysql_ifnull)

<br>

---

<p align="center">
  <a href="Capítulo_09_-_Refinamento_de_Busca_e_Legibilidade.md">⬅️ Anterior</a> | <a href="Capítulo_11_-_Relacionamentos_e_Junções_de_Tabelas.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---