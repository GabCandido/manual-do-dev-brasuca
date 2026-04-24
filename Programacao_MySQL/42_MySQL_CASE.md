## Declaração CASE no MySQL

A instrução **CASE** é uma ferramenta poderosa de lógica condicional dentro do SQL. Ela permite que você defina resultados dinâmicos com base em condições específicas avaliadas durante a execução da consulta.

Pense no `CASE` como a estrutura de controle de fluxo `if-then-else` que você encontraria em linguagens de programação, como Python ou JavaScript. No contexto de bancos de dados, ele é essencial para transformar dados "crus" em informações organizadas sem a necessidade de processar esses dados em uma aplicação externa.

### Como o CASE funciona

O motor do MySQL percorre a lista de condições que você definiu. Assim que ele encontra uma **condição verdadeira**, ele interrompe a verificação e retorna o resultado associado a ela. Se nenhuma condição for atendida, ele verifica se existe uma cláusula **ELSE**. Caso não haja uma cláusula `ELSE` definida e nenhuma condição seja satisfeita, o retorno padrão será `NULL`.

### Sintaxe

A estrutura básica segue o padrão abaixo:

```sql
CASE
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    WHEN conditionN THEN resultN
    ELSE result
END;
```

*   **WHEN**: Define a condição que será avaliada.
*   **THEN**: Define o valor ou ação a ser retornada caso a condição anterior seja verdadeira.
*   **ELSE**: (Opcional) Define um valor padrão caso nenhuma das condições `WHEN` anteriores tenha sido satisfeita.
*   **END**: Encerra o bloco da declaração.

### Exemplo Prático: Categorização de Dados

Um cenário comum no desenvolvimento de software é a necessidade de categorizar dados de negócio para facilitar a visualização em dashboards. No exemplo abaixo, transformamos valores numéricos (Preço) em categorias textuais (Baixo, Médio, Alto custo) diretamente no resultado da consulta.

```sql
SELECT ProductName, Price,
CASE
  WHEN Price < 20 THEN 'Low Cost'
  WHEN Price BETWEEN 20 AND 50 THEN 'Medium Cost'
  ELSE 'High Cost'
END AS PriceCategory
FROM Products;
```

**Resultado esperado:**
O MySQL retornará uma tabela com as colunas `ProductName`, `Price` e uma nova coluna calculada chamada `PriceCategory`. Para cada linha, o motor avaliará o preço: se for menor que 20, rotulará como 'Low Cost'; se estiver entre 20 e 50, 'Medium Cost'; caso contrário, será classificado como 'High Cost'.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_case)

**Nota:** O uso de `AS` após o bloco `END` é uma **boa prática**. Isso define um **alias** (apelido) para a nova coluna, tornando o resultado da sua consulta muito mais legível e profissional para quem consome esses dados.

<br>

---

<p align="center">
  <a href="41_MySQL_INSERT_SELECT.md">⬅️ Anterior</a> | <a href="43_MySQL_Null_Functions.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---