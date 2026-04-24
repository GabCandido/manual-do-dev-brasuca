## A cláusula SELECT DISTINCT no MySQL

Em cenários reais de banco de dados, é extremamente comum nos depararmos com tabelas que contêm dados redundantes. Por exemplo, em uma tabela de clientes, a coluna "País" pode listar "Brasil" centenas de vezes. Quando precisamos extrair apenas a lista de países atendidos, sem repetições, o uso de filtros simples é insuficiente.

É aqui que entra o **SELECT DISTINCT**.

O propósito fundamental desta cláusula é realizar a **deduplicação** de resultados em uma consulta. Em vez de retornar cada ocorrência encontrada na tabela, o MySQL filtra o conjunto de dados para exibir apenas valores únicos, otimizando a visualização e o processamento posterior das informações.

### Sintaxe Básica

A estrutura de comando é intuitiva e deve ser aplicada logo após a palavra-chave `SELECT`.

```sql
SELECT DISTINCT coluna1, coluna2, ...
FROM nome_da_tabela;
```

**Nota:** Ao utilizar múltiplas colunas, o MySQL tratará a combinação desses valores como o critério de unicidade. Ou seja, a linha só será suprimida se a combinação completa de todas as colunas especificadas for idêntica a uma linha anterior.

### Exemplo Prático

Imagine que você precisa obter uma lista de todos os países presentes na sua base de dados de clientes, evitando que o mesmo país apareça múltiplas vezes no relatório.

```sql
SELECT DISTINCT Country FROM Customers;
```

**O que este comando faz:**
1. O motor de busca percorre a coluna `Country` na tabela `Customers`.
2. Ele armazena os valores encontrados e compara cada novo registro com o conjunto de valores únicos já identificados.
3. Se o valor for novo, ele é incluído no resultado; caso contrário, é ignorado.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_distinct)

---

### Comparação: Com vs. Sem DISTINCT

Para compreender a importância deste comando, observe o que acontece quando o omitimos.

```sql
SELECT Country FROM Customers;
```

**Resultado esperado:**
Sem a instrução `DISTINCT`, o MySQL retornará todos os registros da coluna `Country`, linha por linha, incluindo todas as duplicatas. Em grandes volumes de dados (como tabelas com milhões de registros), isso gera um tráfego desnecessário de dados e dificulta a análise humana.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_no_distinct)

---

### Contagem de Valores Únicos

Uma das aplicações mais poderosas do `DISTINCT` em BI (Business Intelligence) e análise de dados é combiná-lo com funções de agregação, como a função `COUNT()`.

```sql
SELECT COUNT(DISTINCT Country) FROM Customers;
```

**Análise técnica:**
Aqui, não estamos apenas filtrando os dados; estamos solicitando que o banco de dados compute a **cardinalidade** daquela coluna. O MySQL primeiro isola os valores únicos de `Country` e, em seguida, realiza a contagem desses itens. Isso é essencial para gerar métricas rápidas, como "quantos países distintos temos em nossa base de clientes?" sem a necessidade de processar essa lógica na aplicação (lado do cliente).

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_distinct2)

**Observação:** A função `COUNT()` será detalhada em módulos futuros, mas é importante notar como o `DISTINCT` atua como um modificador de escopo para ela, alterando drasticamente o resultado da contagem.

<br>

---

<p align="center">
  <a href="05_MySQL_SELECT.md">⬅️ Anterior</a> | <a href="07_MySQL_WHERE.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---