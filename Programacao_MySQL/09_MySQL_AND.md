## Operador AND no MySQL

No ecossistema de bancos de dados relacionais, a capacidade de filtrar dados com precisão cirúrgica é fundamental. O operador **AND** é um componente essencial da cláusula `WHERE`, permitindo que você combine múltiplas condições de busca. 

O propósito central do `AND` é restringir o conjunto de resultados, garantindo que apenas os registros que satisfaçam **todas** as condições especificadas sejam retornados pela consulta.

### Como funciona o operador AND

Quando você utiliza o `AND`, o motor do banco de dados (o **Query Optimizer**) avalia cada condição ligada por esse operador. O registro só é incluído no resultado final se — e somente se — cada uma dessas avaliações resultar em um valor booleano `TRUE` (verdadeiro).

**Nota:** Se qualquer uma das condições for avaliada como `FALSE` ou `UNKNOWN`, o registro será excluído da seleção final.

Imagine que precisamos localizar clientes específicos em uma base de dados global:

```sql
SELECT * FROM Customers
WHERE Country = 'UK'
AND City = 'London';
```

Neste exemplo, o MySQL processa a tabela `Customers` e filtra os registros onde o campo `Country` é igual a "UK". Dentro desse subconjunto, ele aplica um segundo filtro, restringindo os resultados apenas para aqueles onde a coluna `City` também é "London".

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_where_and)

### Sintaxe

A estrutura básica segue a lógica de empilhamento de critérios:

```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition1 AND condition2 AND condition3 ...;
```

---

### AND vs. OR: A Diferença Lógica

Embora ambos sejam operadores lógicos, eles atendem a propósitos distintos no desenvolvimento de sistemas:

*   **AND**: Exige que **todas** as condições sejam verdadeiras (Foco em interseção/restrição).
*   **OR**: Exige que **pelo menos uma** das condições seja verdadeira (Foco em união/amplitude).

**Observação:** O uso correto desses operadores é o que define a performance e a precisão de um relatório ou de uma busca em uma aplicação web.

### Combinando AND e OR

Em cenários reais, as regras de negócio raramente são simples. Frequentemente, precisamos combinar lógica de interseção (`AND`) com lógica de união (`OR`). 

Para evitar ambiguidades na interpretação do MySQL, utilizamos **parênteses**. Os parênteses alteram a precedência dos operadores, garantindo que o banco de dados execute a lógica na ordem que você planejou.

```sql
SELECT * FROM Customers
WHERE Country = 'Germany'
AND (City = 'Berlin' OR City = 'Stuttgart');
```

Neste caso, a consulta busca clientes da Alemanha que residam **ou** em Berlin, **ou** em Stuttgart. Sem os parênteses, o MySQL poderia interpretar a consulta de forma inesperada devido à precedência padrão dos operadores (onde o `AND` geralmente é avaliado antes do `OR`).

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_where_and_or)

<br>

---

<p align="center">
  <a href="08_MySQL_ORDER_BY.md">⬅️ Anterior</a> | <a href="10_MySQL_OR.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---