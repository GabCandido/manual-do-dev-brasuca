## A Palavra-Chave MySQL ORDER BY

A cláusula **ORDER BY** é um componente fundamental na linguagem SQL, utilizada para organizar a apresentação dos dados retornados por uma consulta. Em ambientes de produção, onde tabelas frequentemente contêm milhares ou milhões de registros, a capacidade de ordenar essas informações é essencial para gerar relatórios, dashboards e interfaces de usuário legíveis.

Por padrão, o banco de dados retorna os registros na ordem em que foram armazenados fisicamente ou conforme o plano de execução da query. O `ORDER BY` permite que você defina uma lógica de exibição baseada no valor de colunas específicas.

### Como funciona a ordenação

O `ORDER BY` classifica os resultados de forma **ascendente** (**ASC**) por padrão — do menor para o maior (ou de A a Z). Caso você precise inverter essa lógica, basta utilizar o modificador **DESC** (descendente).

#### Exemplo: Ordenação Simples
Para listar produtos ordenados pelo preço, do menor para o maior:

```sql
SELECT * FROM Products
ORDER BY Price;
```

**Resultado:** Esta consulta organiza todo o seu conjunto de dados de acordo com a coluna `Price`, facilitando a identificação de itens mais baratos no estoque.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_orderby_price)

---

## Sintaxe do ORDER BY

A estrutura básica segue a ordem lógica de uma consulta SQL, onde a ordenação ocorre após a filtragem dos dados:

```sql
SELECT column1, column2, ...
FROM table_name
ORDER BY column1, column2, ... ASC|DESC;
```

**Nota:** Você pode ordenar por múltiplas colunas separando-as por vírgula. O banco de dados aplicará a ordenação na ordem hierárquica em que as colunas foram listadas.

---

## Ordenação Descendente (DESC)

Quando o requisito de negócio exige visualizar os itens "mais caros primeiro" ou "as transações mais recentes", utilizamos a palavra-chave **DESC**.

```sql
SELECT * FROM Products
ORDER BY Price DESC;
```

**Resultado:** O resultado exibirá os registros começando pelos valores mais altos da coluna `Price`.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_orderby_price_desc)

---

## Ordenação por Múltiplas Colunas

Em cenários reais, a ordenação de um único critério muitas vezes não é suficiente. Por exemplo, ao listar clientes, você pode querer agrupar todos por `Country` (País) e, dentro de cada país, ordenar os nomes alfabeticamente.

```sql
SELECT * FROM Customers
ORDER BY Country, CustomerName;
```

**Por que isso é importante?**
Neste caso, o MySQL primeiro organiza todos os registros por `Country`. Quando ele encontra registros que possuem o mesmo país, ele utiliza a segunda coluna (`CustomerName`) como critério de desempate para organizar esses subgrupos.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_orderby2)

---

## Combinando ASC e DESC

Você não está limitado a usar uma única direção de ordenação para todas as colunas. É possível misturar as regras para obter exatamente o relatório desejado.

```sql
SELECT * FROM Customers
ORDER BY Country ASC, CustomerName DESC;
```

**Explicação:** Aqui, os países serão listados em ordem alfabética (A-Z). Contudo, dentro de cada país, os nomes dos clientes serão exibidos em ordem decrescente (Z-A). Esta flexibilidade é o que torna o SQL uma ferramenta poderosa para a manipulação e apresentação de dados.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_orderby3)

<br>

---

<p align="center">
  <a href="07_MySQL_WHERE.md">⬅️ Anterior</a> | <a href="09_MySQL_AND.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---