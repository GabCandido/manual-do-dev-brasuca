# Capítulo 08 - Funções de Agregação e Resumo de Dados

No universo dos bancos de dados relacionais, frequentemente não estamos interessados apenas em extrair linhas individuais, mas em obter **insights** sobre o conjunto de dados como um todo. É aqui que entram as **Funções de Agregação** (*Aggregate Functions*). Uma função de agregação é um método que processa um conjunto de valores e retorna um **único valor** resultante. Pense nelas como ferramentas estatísticas que resumem grandes volumes de dados em informações valiosas para a tomada de decisão.

Embora possam ser usadas isoladamente, essas funções atingem seu potencial máximo quando combinadas com a cláusula **`GROUP BY`**. Enquanto o `SELECT` convencional traz colunas, o `GROUP BY` segmenta o conjunto de resultados em subgrupos, permitindo que a função de agregação calcule um resumo específico para cada um desses grupos — por exemplo, calcular a média salarial por departamento ou o total de vendas por categoria.

As funções mais essenciais do MySQL são:
*   **`MIN()`**: Retorna o menor valor de uma coluna especificada.
*   **`MAX()`**: Retorna o maior valor de uma coluna especificada.
*   **`COUNT()`**: Retorna a contagem total de linhas em um conjunto.
*   **`SUM()`**: Retorna a soma total de valores em uma coluna numérica.
*   **`AVG()`**: Retorna a média aritmética de uma coluna numérica.

> **Nota:** Por definição, as funções de agregação **ignoram valores `NULL`** durante o processamento. Isso é fundamental para manter a precisão estatística. A única exceção notável é a função `COUNT(*)`, que contabiliza todas as linhas, independentemente de valores nulos.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_func_count)

---

## A Função MySQL MIN()

A função **`MIN()`** é uma ferramenta indispensável para encontrar o **menor valor** presente em uma coluna. Sua versatilidade permite aplicá-la em colunas numéricas, de texto (para encontrar a primeira palavra em ordem alfabética) ou de datas (para localizar a data mais antiga em uma série cronológica).

### Sintaxe
```sql
SELECT MIN(column_name)
FROM table_name
WHERE condition;
```

### Exemplo Prático: Identificando o Valor Mínimo
Para identificar o produto mais barato em um catálogo:

```sql
SELECT MIN(Price) AS SmallestPrice
FROM Products;
```

O uso da palavra-chave **`AS`** (como em `AS SmallestPrice`) é uma boa prática de interface, tornando o resultado da consulta mais legível para relatórios ou aplicações front-end. Em sistemas de RH, podemos usar a mesma lógica para datas:

```sql
SELECT MIN(BirthDate) AS EarliestBirthdate
FROM Employees;
```

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_min) | [🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_min2)

---

## A Função MySQL MAX()

Complementar ao `MIN()`, a função **`MAX()`** retorna o maior valor contido em um conjunto de dados. Ela é essencial para identificar o valor mais elevado, a data mais recente ou o registro de maior destaque em uma tabela.

### Sintaxe
```sql
SELECT MAX(column_name)
FROM table_name
WHERE condition;
```

### Exemplo Prático: Identificando o Maior Valor
Considerando nossa tabela de produtos, podemos descobrir o item de maior preço facilmente:

```sql
SELECT MAX(Price) AS LargestPrice
FROM Products;
```

Da mesma forma, ao lidar com colunas de datas, o `MAX()` permite identificar rapidamente a última atividade ou a data mais recente, sendo crucial para registros de logs ou sistemas de usuários:

```sql
SELECT MAX(BirthDate) AS LatestBirthdate
FROM Employees;
```

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_max) | [🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_max2)

---

## A Função MySQL COUNT()

A função **`COUNT()`** realiza a agregação de dados permitindo obter métricas quantitativas sobre o volume de registros. Seu comportamento varia conforme o argumento passado:

*   **`COUNT(*)`**: Conta o número total de linhas, incluindo registros com valores `NULL`.
*   **`COUNT(column_name)`**: Conta apenas as linhas onde a coluna especificada **não é NULL**.
*   **`COUNT(DISTINCT column_name)`**: Filtra valores duplicados e conta apenas valores **únicos e não-nulos**.

### Exemplos Práticos
Para contar o volume total de itens no inventário:
```sql
SELECT COUNT(*) FROM Products;
```

Para verificar quantos produtos possuem um identificador definido ou contar variedades de preços ignorando repetições:
```sql
SELECT COUNT(DISTINCT Price) FROM Products;
```

Ao combinar com a cláusula `WHERE`, podemos restringir a contagem a critérios específicos, como identificar quantos produtos custam mais de 20:
```sql
SELECT COUNT(ProductID) FROM Products WHERE Price > 20;
```

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_count2) | [🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_count) | [🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_count_distinct) | [🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_count3)

---

## A Função MySQL SUM()

A função **`SUM()`** calcula o total de uma coluna numérica. Ela é a forma mais eficiente de realizar consolidações, como o total de vendas ou estoque, diretamente no servidor de banco de dados.

### Exemplo Prático: Calculando Totais
Para somar a quantidade total de itens vendidos:

```sql
SELECT SUM(Quantity) FROM OrderDetails;
```

Se precisarmos de totalizações segmentadas, a combinação com o `WHERE` é essencial para performance:

```sql
SELECT SUM(Quantity) FROM OrderDetails WHERE ProductId = 11;
```

> **Nota:** A função `SUM()` ignora valores `NULL`, evitando distorções estatísticas. Lembre-se que utilizar `WHERE` antes da agregação é uma prática recomendada para otimizar o uso de memória e processamento.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_sum) | [🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_sum_where)

---

## A Função MySQL AVG()

Por fim, a função **`AVG()`** calcula a média aritmética de uma coluna numérica. Assim como as demais funções de agregação, ela ignora automaticamente valores `NULL`, garantindo que o resultado reflita apenas registros válidos.

### Exemplo Prático: Média de Preços
```sql
SELECT AVG(Price) FROM Products;
```

Podemos refinar a análise filtrando por categorias:
```sql
SELECT AVG(Price) FROM Products WHERE CategoryID = 1;
```

### Análise Avançada: Subconsultas
Para cenários de BI onde precisamos identificar itens com desempenho acima da média, utilizamos uma **subquery**:

```sql
SELECT * FROM Products 
WHERE Price > (SELECT AVG(Price) FROM Products);
```

Esta abordagem demonstra a capacidade do SQL de realizar operações em múltiplos níveis de processamento em uma única consulta, transformando dados brutos em inteligência de negócio.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_avg) | [🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_avg_where) | [🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_avg2)

---

<p align="center">
  <a href="16_MySQL_LIMIT.md">🏠 Voltar ao Início</a>
</p>

<br>

---

<p align="center">
  <a href="Capítulo_07_-_Manipulação_de_Dados__Inserção,_Atualização_e_Exclusão.md">⬅️ Anterior</a> | <a href="Capítulo_09_-_Refinamento_de_Busca_e_Legibilidade.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---