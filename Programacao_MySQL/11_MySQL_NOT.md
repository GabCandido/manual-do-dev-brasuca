## O Operador NOT no MySQL

O operador **NOT** é uma peça fundamental na lógica de filtragem de dados em SQL. Ele é utilizado dentro da cláusula **WHERE** para inverter o resultado de uma condição lógica: registros que atenderiam ao critério original são excluídos, enquanto aqueles que não atendem são retornados.

Pense no `NOT` como uma negação lógica. Se o seu objetivo é "trazer tudo, menos o que se encaixa no padrão X", o `NOT` é o seu operador de escolha.

### Exemplo de Aplicação
Para selecionar todos os clientes que **não** residem na Alemanha:

```sql
SELECT * FROM Customers
WHERE NOT Country = 'Germany';
```

**Explicação:** O motor do banco de dados avalia a condição `Country = 'Germany'`. Normalmente, isso retornaria apenas os registros alemães. Ao prefixar com `NOT`, você instrui o SQL a retornar exatamente o conjunto complementar — todos os registros onde a coluna `Country` contenha qualquer valor diferente de 'Germany'.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_where_not)

---

## Sintaxe Básica

A estrutura de negação segue a lógica de pré-condicionamento do filtro:

```sql
SELECT column1, column2, ...
FROM table_name
WHERE NOT condition;
```

---

## Combinando Operadores: AND, OR e NOT

A verdadeira flexibilidade do `NOT` brilha quando o combinamos com operadores lógicos para criar filtros complexos.

**Nota:** Ao misturar operadores, utilize sempre **parênteses** para garantir que a precedência lógica seja respeitada, evitando resultados inesperados.

### Exemplo: Filtros Complexos
Se quisermos selecionar clientes que **não** são da Alemanha e **não** são dos EUA:

```sql
SELECT * FROM Customers
WHERE NOT Country = 'Germany'
AND NOT Country = 'USA';
```

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_where_not_and)

---

## O Poder do NOT com Operadores Especiais

O `NOT` é frequentemente usado como um modificador para outros operadores, permitindo uma limpeza de dados mais expressiva:

*   **NOT LIKE**: Exclui registros baseados em padrões de texto.
*   **NOT BETWEEN**: Exclui registros dentro de um intervalo numérico ou de data.
*   **NOT IN**: Exclui registros que correspondem a qualquer valor presente em uma lista.
*   **IS NOT NULL**: Retorna registros que possuem dados (não vazios).

### Exemplos Práticos

#### 1. NOT LIKE
Útil para excluir nomes que seguem um padrão específico. Por exemplo, excluir nomes que começam com 'A':

```sql
SELECT * FROM Customers
WHERE CustomerName NOT LIKE 'A%';
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_not_like)

#### 2. NOT BETWEEN
Exclui uma faixa de valores. Abaixo, selecionamos IDs que estão fora do intervalo de 10 a 60:

```sql
SELECT * FROM Customers
WHERE CustomerID NOT BETWEEN 10 AND 60;
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_not_between2)

#### 3. NOT IN
Exclui registros presentes em um conjunto de valores. Aqui, removemos registros de cidades específicas:

```sql
SELECT * FROM Customers
WHERE City NOT IN ('Paris', 'London');
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_not_in)

---

## Consideração sobre "Maior que" e "Menor que"

Embora seja tecnicamente possível escrever `WHERE NOT CustomerID > 50`, o uso de operadores de comparação padrão é considerado uma boa prática de **Clean Code** e legibilidade.

*   `NOT > 50` é logicamente equivalente a `<= 50`.
*   `NOT < 50` é logicamente equivalente a `>= 50`.

**Observação:** Utilizar os operadores de comparação direta (`>=`, `<=`) é preferível, pois torna a intenção da sua consulta óbvia para outros desenvolvedores, além de permitir que o otimizador de consultas do banco de dados trabalhe com maior eficiência.

<br>

---

<p align="center">
  <a href="10_MySQL_OR.md">⬅️ Anterior</a> | <a href="12_MySQL_INSERT_INTO.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---