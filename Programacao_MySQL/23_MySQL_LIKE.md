## O Operador LIKE no MySQL

O operador **LIKE** é uma ferramenta fundamental na linguagem SQL, utilizada dentro da cláusula `WHERE` para realizar buscas baseadas em padrões de texto. Diferente do operador de igualdade (`=`), que busca por correspondências exatas, o `LIKE` permite localizar registros que contenham partes específicas de uma string, tornando-o essencial para sistemas de busca, filtros de usuários e análise de dados parciais.

Para criar esses padrões de busca, utilizamos dois **wildcards** (caracteres curinga):

*   **% (Sinal de porcentagem):** Representa zero, um ou múltiplos caracteres.
*   **_ (Sublinhado):** Representa exatamente um único caractere.

### Sintaxe

A estrutura básica para filtrar dados utilizando padrões é:

```sql
SELECT column1, column2, ...
FROM table_name
WHERE columnN LIKE pattern;
```

**Nota:** Você pode combinar múltiplos critérios de busca utilizando os operadores lógicos `AND` ou `OR` para refinar ainda mais seus resultados.

### Padrões de Busca e Wildcards

A eficácia do `LIKE` reside na capacidade de manipular os curingas para atender a diferentes necessidades de negócio. Confira abaixo os padrões mais comuns:

| Operador LIKE | Descrição |
| :--- | :--- |
| `WHERE CustomerName LIKE 'a%'` | Busca valores que iniciam com "a" |
| `WHERE CustomerName LIKE '%a'` | Busca valores que terminam com "a" |
| `WHERE CustomerName LIKE '%or%'` | Busca valores que contenham "or" em qualquer posição |
| `WHERE CustomerName LIKE '_r%'` | Busca valores com "r" na segunda posição |
| `WHERE CustomerName LIKE 'a_%'` | Busca valores que iniciam com "a" e têm pelo menos 2 caracteres |
| `WHERE CustomerName LIKE 'a__%'` | Busca valores que iniciam com "a" e têm pelo menos 3 caracteres |
| `WHERE ContactName LIKE 'a%o'` | Busca valores que iniciam com "a" e terminam com "o" |

---

## Exemplos Práticos

Para ilustrar o uso, considere a tabela `Customers`:

| CustomerID | CustomerName | ContactName | City | Country |
| :--- | :--- | :--- | :--- | :--- |
| 1 | Alfreds Futterkiste | Maria Anders | Berlin | Germany |
| 2 | Ana Trujillo... | Ana Trujillo | México D.F. | Mexico |
| 3 | Antonio Moreno... | Antonio Moreno | México D.F. | Mexico |
| 4 | Around the Horn | Thomas Hardy | London | UK |
| 5 | Berglunds snabbköp | Christina Berglund | Luleå | Sweden |

### 1. Início de string
Seleciona todos os clientes cujo nome começa com "a":

```sql
SELECT * FROM Customers
WHERE CustomerName LIKE 'a%';
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_like)

### 2. Final de string
Seleciona todos os clientes cujo nome termina com "a":

```sql
SELECT * FROM Customers
WHERE CustomerName LIKE '%a';
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_like_ending)

### 3. Conteúdo em qualquer posição
Seleciona clientes que possuem a sequência "or" em qualquer parte do nome:

```sql
SELECT * FROM Customers
WHERE CustomerName LIKE '%or%';
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_like_pattern)

### 4. Posição específica (Wildcard de um caractere)
Seleciona clientes que possuem a letra "r" na segunda posição do nome:

```sql
SELECT * FROM Customers
WHERE CustomerName LIKE '_r%';
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_like_underscore)

### 5. Comprimento mínimo
Seleciona clientes que começam com "a" e possuem pelo menos 3 caracteres:

```sql
SELECT * FROM Customers
WHERE CustomerName LIKE 'a__%';
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_like_start_least)

### 6. Combinação de início e fim
Seleciona contatos que começam com "a" e terminam com "o":

```sql
SELECT * FROM Customers
WHERE ContactName LIKE 'a%o';
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_like_start_end)

### 7. Negando o padrão
Para excluir registros que seguem determinado padrão, utilizamos `NOT LIKE`:

```sql
SELECT * FROM Customers
WHERE CustomerName NOT LIKE 'a%';
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_like_not)

**Observação:** O uso de curingas no início de uma busca (ex: `%termo`) pode impactar a performance em tabelas massivas, pois impede que o banco de dados utilize índices da coluna, forçando um *Full Table Scan*. Sempre que possível, tente restringir sua busca utilizando filtros adicionais.

<br>

---

<p align="center">
  <a href="22_MySQL_AVG().md">⬅️ Anterior</a> | <a href="24_MySQL_Wildcards.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---