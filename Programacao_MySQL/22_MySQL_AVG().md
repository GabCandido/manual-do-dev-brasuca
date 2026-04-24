## A Função MySQL AVG()

A função **AVG()** é uma ferramenta de agregação fundamental no SQL, projetada para calcular o valor médio de uma coluna numérica específica. Em cenários de análise de dados, ela é essencial para extrair métricas de desempenho, tendências de mercado ou médias estatísticas diretamente do banco de dados, evitando a necessidade de exportar grandes volumes de dados para processamento externo.

**Observação importante:** A função `AVG()` ignora automaticamente valores **NULL**. Isso significa que, ao calcular a média, o banco de dados não inclui linhas onde a coluna não possui um dado atribuído, garantindo que o cálculo reflita apenas os registros com valores válidos.

---

## Sintaxe da Função

Para utilizar o `AVG()`, aplicamos a função sobre o nome da coluna dentro de um comando `SELECT`:

```sql
SELECT AVG(nome_da_coluna)
FROM nome_da_tabela
WHERE condicao;
```

O uso da cláusula `WHERE` é opcional, mas frequentemente utilizado para filtrar apenas o subconjunto de dados que você deseja analisar.

---

## Exemplo Prático: Média de Preços

Considere uma tabela de `Produtos` (Products). Para obter o preço médio de todo o nosso inventário, utilizamos o seguinte comando:

```sql
SELECT AVG(Price) 
FROM Products;
```

**O que este código faz:** O motor do banco de dados percorre todas as linhas da coluna `Price`, soma os valores contidos nelas e divide pelo número total de registros (excluindo os `NULL`). O resultado é um valor escalar único representando a média geral.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_avg)

---

## Filtrando com WHERE

Frequentemente, não queremos a média de todos os registros, mas sim de uma categoria ou grupo específico. Ao adicionar uma cláusula `WHERE`, restringimos o escopo do cálculo.

```sql
SELECT AVG(Price) 
FROM Products 
WHERE CategoryID = 1;
```

**Resultado esperado:** Este comando retorna apenas a média dos preços dos produtos que pertencem à categoria de ID 1. É uma técnica poderosa para comparações rápidas entre departamentos ou grupos de produtos.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_avg_where)

---

## Analisando Dados acima da Média

Uma aplicação avançada e comum em sistemas de e-commerce ou BI é identificar itens que possuem um desempenho (ou valor) acima da média. Para isso, utilizamos uma **Subquery** (subconsulta).

```sql
SELECT * FROM Products 
WHERE Price > (SELECT AVG(Price) FROM Products);
```

**Análise técnica:**
1. A subconsulta `(SELECT AVG(Price) FROM Products)` é executada primeiro pelo banco de dados.
2. O resultado retornado pela subconsulta é um único valor (o preço médio global).
3. O comando externo filtra a tabela exibindo todos os produtos cujo preço é estritamente maior que o valor médio calculado.

Esta abordagem demonstra a capacidade do SQL de realizar operações em múltiplos níveis de processamento em uma única consulta.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_avg2)

<br>

---

<p align="center">
  <a href="21_MySQL_SUM().md">⬅️ Anterior</a> | <a href="23_MySQL_LIKE.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---