## A Cláusula MySQL LIMIT

Em sistemas de banco de dados que gerenciam milhões de registros, processar a totalidade de uma tabela em uma única consulta é uma prática ineficiente, tanto para a memória do servidor quanto para a latência da aplicação. A cláusula **LIMIT** é o recurso fundamental do SQL para resolver esse gargalo, permitindo que você especifique exatamente quantos registros deseja recuperar.

Ao definir um limite, você reduz a carga de trabalho do motor de banco de dados (Query Optimizer) e otimiza a experiência do usuário final, técnica conhecida em arquitetura de software como **Pagination** (Paginação).

### Sintaxe Básica

A estrutura de comando segue o padrão abaixo, onde você determina o número máximo de linhas retornadas:

```sql
SELECT column_name(s)
FROM table_name
WHERE condition
LIMIT number;
```

**Nota:** A cláusula `LIMIT` deve ser sempre a última instrução em uma consulta, aparecendo após os filtros (`WHERE`) e ordenações (`ORDER BY`).

---

## Exemplos Práticos

Para ilustrar, utilizaremos uma tabela hipotética de `Customers` (Clientes). Imagine um cenário onde você precisa exibir apenas uma amostra rápida dos seus dados.

### 1. Limitando o retorno de dados
Se você deseja obter apenas os três primeiros registros de uma tabela, utilize o `LIMIT` seguido pelo valor inteiro:

```sql
SELECT * FROM Customers
LIMIT 3;
```

**Explicação:** O motor do MySQL lerá a tabela e interromperá a varredura assim que encontrar o terceiro registro, descartando o processamento dos demais.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_limit)

---

### 2. Paginação com OFFSET
Muitas vezes, precisamos exibir dados "fatiados" (ex: página 2 de uma lista). Para isso, utilizamos o **OFFSET**, que define o ponto de partida para a contagem.

```sql
SELECT * FROM Customers
LIMIT 3 OFFSET 3;
```

**Resultado esperado:** O MySQL pulará os 3 primeiros registros (índice 0 a 2) e retornará os próximos 3 registros (4, 5 e 6). Este comando é o alicerce para implementar "Carregar mais" em interfaces de usuário.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_limit_offset)

---

### 3. Combinando com Filtros (WHERE)
Você pode restringir o conjunto de dados antes de aplicar o limite. Aqui, filtramos apenas clientes da Alemanha e exibimos os primeiros três encontrados:

```sql
SELECT * FROM Customers
WHERE Country='Germany'
LIMIT 3;
```

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_limit_where)

---

### 4. Combinando com Ordenação (ORDER BY)
O uso combinado com `ORDER BY` é comum para obter, por exemplo, os "Top 3" de uma categoria.

```sql
SELECT * FROM Customers
ORDER BY Country
LIMIT 3;
```

**Observação:** Quando você usa `ORDER BY` com `LIMIT`, o MySQL primeiro realiza a ordenação de todo o conjunto de dados para depois aplicar o recorte. Em tabelas massivas, certifique-se de que a coluna utilizada no `ORDER BY` possua um **Índice (Index)** para evitar lentidão na execução da consulta.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_limit_orderby)

<br>

---

<p align="center">
  <a href="15_MySQL_DELETE.md">⬅️ Anterior</a> | <a href="17_MySQL_Aggregate_Functions.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---