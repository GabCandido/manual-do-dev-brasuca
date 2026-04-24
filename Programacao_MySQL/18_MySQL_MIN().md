## A Função MySQL MIN()

A função **MIN()** é uma ferramenta essencial no conjunto de funções de agregação do MySQL. Seu propósito fundamental é realizar uma varredura em um conjunto de dados para retornar o **menor valor** presente em uma coluna específica.

Ela é extremamente versátil, pois não se limita a valores numéricos; você pode aplicá-la em colunas do tipo **string** (para encontrar a primeira palavra em ordem alfabética) ou **data** (para localizar a data mais antiga em uma série cronológica).

### Sintaxe

A estrutura da função segue o padrão das funções agregadoras SQL:

```sql
SELECT MIN(column_name)
FROM table_name
WHERE condition;
```

*   `column_name`: A coluna que você deseja analisar.
*   `table_name`: A tabela onde os dados estão armazenados.
*   `WHERE`: (Opcional) Filtra as linhas antes que o cálculo do valor mínimo seja executado.

---

### Exemplo Prático: Identificando o Valor Mínimo

Imagine que você gerencia um e-commerce e precisa identificar qual é o produto mais barato do seu catálogo para uma campanha de marketing. Utilizando a tabela `Products`, podemos extrair essa informação facilmente:

```sql
SELECT MIN(Price) AS SmallestPrice
FROM Products;
```

**Explicação:**
*   A função `MIN(Price)` percorre toda a coluna de preços e isola o menor valor.
*   O uso da palavra-chave **AS** é uma boa prática de interface. Como o MySQL, por padrão, nomearia a coluna resultante como `MIN(Price)`, usar `AS SmallestPrice` torna o resultado da consulta muito mais legível para aplicações front-end ou relatórios.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_min)

---

### Aplicando em Datas

A utilidade de `MIN()` vai além do financeiro. Em sistemas de RH ou registros históricos, frequentemente precisamos encontrar a "primeira ocorrência" de um evento. O MySQL trata datas internamente de forma que nos permite identificar a data mais antiga com precisão.

```sql
SELECT MIN(BirthDate) AS EarliestBirthdate
FROM Employees;
```

**Resultado Esperado:** Esta consulta retornará a data de nascimento mais antiga registrada na tabela `Employees`, essencial, por exemplo, para determinar quem é o colaborador com maior senioridade de idade na empresa.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_min2)

---

**Nota:** Ao trabalhar com funções de agregação, lembre-se que, se a coluna especificada contiver valores `NULL`, a função `MIN()` os ignorará automaticamente (a menos que todos os valores da coluna sejam nulos, caso em que o resultado será `NULL`).

**Observação:** Diferente de uma consulta `SELECT` comum, que pode retornar múltiplas linhas, o uso de `MIN()` (sem uma cláusula `GROUP BY`) sempre retornará apenas um único valor escalar, condensando o resultado de toda a busca.

<br>

---

<p align="center">
  <a href="17_MySQL_Aggregate_Functions.md">⬅️ Anterior</a> | <a href="19_MySQL_MAX().md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---