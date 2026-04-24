## Operador MySQL BETWEEN

O operador **BETWEEN** é uma ferramenta fundamental na cláusula `WHERE` do SQL. Sua função principal é selecionar valores dentro de um intervalo definido, simplificando consultas que, de outra forma, exigiriam múltiplos operadores lógicos (como `>=` e `<=`).

**Nota:** O intervalo definido pelo `BETWEEN` é **inclusivo**. Isso significa que tanto o valor inicial quanto o valor final são considerados parte do conjunto de resultados.

### Sintaxe do Operador

```sql
SELECT column_name(s)
FROM table_name
WHERE column_name BETWEEN value1 AND value2;
```

A versatilidade do `BETWEEN` permite que você trabalhe com números, textos ou datas, tornando-o extremamente útil para relatórios de vendas, filtros de produtos por preço ou busca de registros em janelas temporais.

---

### Exemplo Prático: Filtragem Numérica

Para filtrar produtos que possuem um preço dentro de uma faixa específica, utilizamos o `BETWEEN` seguido pelos limites inferior e superior.

```sql
SELECT * FROM Products
WHERE Price BETWEEN 10 AND 20;
```
**Resultado esperado:** A consulta retornará todas as linhas da tabela `Products` onde o valor da coluna `Price` seja maior ou igual a 10 **e** menor ou igual a 20.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_between)

---

### Invertendo a Lógica: NOT BETWEEN

Se você precisa excluir um intervalo específico e obter tudo o que está fora dele, basta utilizar o operador **NOT BETWEEN**.

```sql
SELECT * FROM Products
WHERE Price NOT BETWEEN 10 AND 20;
```
**Resultado esperado:** Esta consulta filtra todos os produtos cujos preços sejam estritamente menores que 10 ou estritamente maiores que 20.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_not_between)

---

### Filtragem Combinada

O poder do SQL reside na combinação de operadores. Você pode restringir um intervalo de valores e, simultaneamente, aplicar um filtro de categoria.

```sql
SELECT * FROM Products
WHERE Price BETWEEN 10 AND 20
AND CategoryID IN (1, 2, 3);
```
**Resultado esperado:** O banco de dados retornará apenas os produtos que atendem aos dois critérios: preço entre 10 e 20 **e** que pertençam exclusivamente às categorias 1, 2 ou 3.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_between_in)

---

### Operando com Textos

O `BETWEEN` também pode ser aplicado a colunas do tipo texto. Nesse caso, o banco de dados utiliza a ordem alfabética para determinar o intervalo.

```sql
SELECT * FROM Products
WHERE ProductName BETWEEN 'Carnarvon Tigers' AND 'Mozzarella di Giovanni'
ORDER BY ProductName;
```
**Resultado esperado:** A query retorna todos os nomes de produtos que começam alfabeticamente entre "Carnarvon Tigers" e "Mozzarella di Giovanni", ordenados de A a Z.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_between_text)

**Nota:** O comportamento de `NOT BETWEEN` aplicado a textos segue a mesma lógica de exclusão: ele ignorará todos os registros que estariam dentro do intervalo alfabético delimitado.

[🚀 Pratique este código (NOT BETWEEN com texto)](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_not_between_text)

---

### Filtragem de Datas

No desenvolvimento de sistemas, é comum a necessidade de buscar registros em um período de tempo específico. O `BETWEEN` é ideal para isso, desde que o formato da data seja respeitado (geralmente `YYYY-MM-DD`).

```sql
SELECT * FROM Orders
WHERE OrderDate BETWEEN '1996-07-01' AND '1996-07-31';
```
**Resultado esperado:** A consulta retornará todos os pedidos realizados durante todo o mês de julho de 1996.

**Observação:** Ao trabalhar com datas, certifique-se de que a coluna de dados no seu banco esteja definida como `DATE` ou `DATETIME` para garantir que a comparação ocorra corretamente.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_between_date2)

<br>

---

<p align="center">
  <a href="25_MySQL_IN.md">⬅️ Anterior</a> | <a href="27_MySQL_Aliases.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---