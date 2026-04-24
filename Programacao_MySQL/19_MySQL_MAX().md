## A Função MAX() no MySQL

A função **`MAX()`** é uma ferramenta de agregação fundamental no SQL, projetada para retornar o maior valor contido em um conjunto de dados selecionado. Ela é essencial para análises rápidas, como identificar o produto mais caro, a data mais recente em um histórico ou o maior valor de uma pontuação em um sistema.

A versatilidade da `MAX()` permite que ela opere sobre diversos tipos de dados, incluindo **numéricos**, **strings** (ordem alfabética) e **datas** (cronologia), tornando-a indispensável para a extração de inteligência de negócios.

### Sintaxe

A estrutura básica da função requer que você especifique a coluna que deseja analisar e a tabela de origem.

```sql
SELECT MAX(column_name)
FROM table_name
WHERE condition;
```

**Por que usar a cláusula `WHERE`?**
Embora opcional, a cláusula `WHERE` permite filtrar os dados *antes* que a função `MAX()` seja aplicada. Isso garante que você encontre o valor máximo dentro de um subconjunto específico, otimizando o processamento e a precisão do resultado.

---

## Tabela de Exemplo: Products

Para ilustrar o uso, considere a seguinte amostra da tabela `Products`:

| ProductID | ProductName | Price |
| :--- | :--- | :--- |
| 1 | Chais | 18.00 |
| 2 | Chang | 19.00 |
| 3 | Aniseed Syrup | 10.00 |
| 4 | Chef Anton's Cajun Seasoning | 22.00 |
| 5 | Chef Anton's Gumbo Mix | 21.35 |

---

## Exemplo Prático: Identificando o Maior Valor

Se precisarmos descobrir qual é o preço mais elevado entre todos os nossos produtos cadastrados, utilizamos a `MAX()` aplicada à coluna `Price`.

```sql
SELECT MAX(Price) AS LargestPrice
FROM Products;
```

**Nota:** O uso de `AS LargestPrice` é um **alias** (apelido). Como o SQL retornará o valor sem um nome de coluna amigável por padrão, renomear o resultado torna o relatório muito mais legível para aplicações front-end ou dashboards.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_max)

---

## Uso com Datas

A `MAX()` brilha ao lidar com colunas de data. Em sistemas de usuários ou registros de logs, ela permite identificar rapidamente a última atividade ou a data mais recente de um evento.

```sql
SELECT MAX(BirthDate) AS LatestBirthdate
FROM Employees;
```

**Observação:** Quando aplicada a datas, o valor "máximo" é interpretado pelo banco de dados como a data mais "recente" (ou seja, a data mais distante no futuro ou a mais próxima do momento atual).

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_max2)

<br>

---

<p align="center">
  <a href="18_MySQL_MIN().md">⬅️ Anterior</a> | <a href="20_MySQL_COUNT().md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---