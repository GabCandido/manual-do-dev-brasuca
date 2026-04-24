# Capítulo 05 - Recuperação de Dados e Ordenação

## O Comando MySQL SELECT

O comando **SELECT** é a espinha dorsal de qualquer interação com bancos de dados relacionais. Em termos práticos, ele é a ferramenta que utilizamos para extrair informações específicas armazenadas em tabelas. Sempre que você consulta um perfil de usuário, busca um produto em um e-commerce ou gera um relatório de vendas, você está, essencialmente, executando um `SELECT`.

Quando o banco de dados processa esse comando, ele retorna os dados organizados em uma estrutura tabular temporária, chamada de **result-set** (conjunto de resultados).

### Sintaxe Básica

Para realizar uma consulta, você deve indicar quais campos (colunas) deseja visualizar e a origem (tabela) onde esses dados residem.

```sql
SELECT coluna1, coluna2, ...
FROM nome_da_tabela;
```

*   `coluna1`, `coluna2`: representam os nomes das colunas que você deseja recuperar.
*   `nome_da_tabela`: o local onde os dados estão armazenados.

**Nota:** O SQL (Structured Query Language) não diferencia maiúsculas de minúsculas nos comandos, mas é uma convenção de mercado utilizar letras maiúsculas para as palavras-chave (como `SELECT` e `FROM`) para melhorar a legibilidade do código.

### Exemplo Prático

Imagine que no banco de dados "Northwind" temos a tabela `Customers`. Se quisermos extrair apenas o nome do cliente, a cidade e o país, o comando seria:

```sql
SELECT CustomerName, City, Country 
FROM Customers;
```

Após a execução, o MySQL retornará uma tabela contendo apenas as três colunas solicitadas para todos os registros encontrados na tabela `Customers`.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_columns)

### Selecionando Todas as Colunas

Frequentemente, durante o desenvolvimento ou depuração, precisamos visualizar a estrutura completa de uma tabela. Em vez de listar manualmente cada nome de coluna, utilizamos o operador curinga `*` (asterisco).

```sql
SELECT * FROM Customers;
```

**Observação:** Embora o `SELECT *` seja extremamente útil para exploração de dados, evite utilizá-lo em aplicações de produção (sistemas finais). Ao especificar apenas as colunas necessárias, você reduz o tráfego de rede e o consumo de memória, tornando sua aplicação mais performática e segura.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_all)

---

## A cláusula SELECT DISTINCT no MySQL

Após aprender a extrair colunas específicas, nos deparamos com o desafio da redundância. Em cenários reais, é comum que tabelas contenham dados repetidos, como diversos clientes vindos do mesmo país. Quando precisamos listar apenas os valores únicos, utilizamos o **SELECT DISTINCT**.

O propósito fundamental desta cláusula é realizar a **deduplicação** de resultados, filtrando o conjunto de dados para exibir apenas valores únicos e otimizar a visualização.

### Sintaxe e Uso

A estrutura de comando deve ser aplicada logo após a palavra-chave `SELECT`:

```sql
SELECT DISTINCT coluna1, coluna2, ...
FROM nome_da_tabela;
```

**Nota:** Ao utilizar múltiplas colunas, o MySQL tratará a combinação desses valores como o critério de unicidade.

#### Exemplo Prático
Para obter uma lista de todos os países presentes na sua base de dados, evitando duplicatas:

```sql
SELECT DISTINCT Country FROM Customers;
```

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_distinct)

Para compreender a importância deste comando, compare-o com uma consulta simples (`SELECT Country FROM Customers`), que retornará todos os registros, linha por linha. Em grandes volumes, isso gera tráfego desnecessário e dificulta a análise.

### Contagem de Valores Únicos
O `DISTINCT` pode ser combinado com funções de agregação, como o `COUNT()`:

```sql
SELECT COUNT(DISTINCT Country) FROM Customers;
```

**Análise técnica:** O MySQL primeiro isola os valores únicos e, em seguida, realiza a contagem. Isso é essencial para gerar métricas de **cardinalidade**.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_distinct2)

---

## A Cláusula WHERE no MySQL

Para ir além da extração de todos os dados, utilizamos a cláusula **WHERE**, que atua como um filtro lógico, determinando exatamente quais registros devem ser processados. Ela é essencial não apenas para consultas, mas também para garantir a segurança em operações de `UPDATE` e `DELETE`.

### Sintaxe Básica

```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

**Nota:** Lembre-se que valores do tipo **texto** (strings ou datas) devem ser envolvidos por aspas simples (`' '`), enquanto **valores numéricos** são escritos diretamente.

#### Operadores de Comparação
O poder do `WHERE` reside nos seus operadores lógicos. Veja a tabela de referência:

| Operador | Descrição |
| :--- | :--- |
| `=` | Igual a |
| `>` | Maior que |
| `<` | Menor que |
| `<>` ou `!=` | Diferente de |
| `BETWEEN` | Em um intervalo específico |
| `LIKE` | Busca por padrões de texto |
| `IN` | Especifica múltiplos valores |

**Exemplo:** Para filtrar clientes do México:
```sql
SELECT * FROM Customers WHERE Country = 'Mexico';
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_where)

---

## A Palavra-Chave MySQL ORDER BY

Uma vez filtrados os dados, a organização é o próximo passo. A cláusula **ORDER BY** permite definir a exibição dos resultados, seja em ordem crescente (**ASC**) ou decrescente (**DESC**).

### Ordenação Simples e Múltipla
O padrão é a ordem ascendente. Para inverter, utilize o `DESC`:

```sql
SELECT * FROM Products
ORDER BY Price DESC;
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_orderby_price_desc)

Você também pode ordenar por múltiplas colunas. O banco de dados utilizará a primeira coluna como critério principal e, em caso de empate, utilizará a segunda coluna como desempate:

```sql
SELECT * FROM Customers
ORDER BY Country ASC, CustomerName DESC;
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_orderby3)

---

## A Cláusula MySQL LIMIT

Por fim, ao lidar com milhões de registros, é vital controlar o volume de dados retornados. A cláusula **LIMIT** permite restringir o número de registros, sendo a base para a técnica de **paginação** de dados.

### Sintaxe e Paginação

```sql
SELECT column_name(s)
FROM table_name
LIMIT number;
```

**Nota:** O `LIMIT` deve ser sempre a última instrução da consulta. Para implementar paginação, utilizamos o **OFFSET**, que define um ponto de partida:

```sql
-- Pula os 3 primeiros registros e traz os próximos 3
SELECT * FROM Customers
LIMIT 3 OFFSET 3;
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_limit_offset)

**Observação:** Quando você utiliza `ORDER BY` em conjunto com `LIMIT`, o banco de dados primeiro ordena o conjunto completo para depois aplicar o recorte. Em tabelas muito grandes, certifique-se de que a coluna de ordenação possua um **Índice** para garantir a performance da query.

---

<p align="center">
  <a href="Capítulo_04_-_Relacionamentos_Referenciais_e_Otimização.md">⬅️ Anterior</a> | <a href="Capítulo_06_-_Operadores_Lógicos_e_Expressões.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---