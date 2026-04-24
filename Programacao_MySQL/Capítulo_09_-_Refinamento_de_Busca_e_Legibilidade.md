# Capítulo 09 - Refinamento de Busca e Legibilidade

Dominar a linguagem SQL exige mais do que apenas extrair dados; exige a capacidade de filtrar, organizar e apresentar essas informações de maneira precisa. Neste capítulo, exploraremos técnicas essenciais para refinar consultas, desde a busca por padrões de texto até a melhoria da legibilidade dos resultados finais através de apelidos.

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

### Exemplos Práticos de Filtragem
Considerando a tabela `Customers`, podemos aplicar diversas variações:

**1. Início e fim de string:**
```sql
SELECT * FROM Customers WHERE CustomerName LIKE 'a%';
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_like)

**2. Conteúdo em qualquer posição:**
```sql
SELECT * FROM Customers WHERE CustomerName LIKE '%or%';
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_like_pattern)

**3. Negando o padrão:**
Para excluir registros que seguem determinado padrão, utilizamos `NOT LIKE`:
```sql
SELECT * FROM Customers WHERE CustomerName NOT LIKE 'a%';
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_like_not)

**Observação:** O uso de curingas no início de uma busca (ex: `%termo`) pode impactar a performance em tabelas massivas, pois impede que o banco de dados utilize índices, forçando um *Full Table Scan*.

## Wildcards no MySQL

Os **wildcards** (caracteres curinga) são símbolos especiais que permitem substituir um ou mais caracteres em uma string, proporcionando uma flexibilidade inigualável em buscas onde a cadeia exata é desconhecida.

### Tabela de Referência
| Símbolo | Descrição | Exemplo |
| :--- | :--- | :--- |
| `%` | Representa zero, um ou múltiplos caracteres | `bl%` encontra "black", "blue" |
| `_` | Representa exatamente um único caractere | `h_t` encontra "hot", "hat" |

O uso do `_` (sublinhado) é particularmente útil para estruturas fixas. Por exemplo, a consulta `SELECT * FROM Customers WHERE City LIKE '_ondon';` retornará "London", pois o curinga reserva exatamente um espaço para o primeiro caractere, seguido pela sequência "ondon".

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_wildcard_underscore)

---

Após refinar a busca por padrões de texto, muitas vezes nos deparamos com a necessidade de filtrar por conjuntos de valores ou intervalos. É aqui que entram os operadores `IN` e `BETWEEN`.

## O Operador IN no MySQL

O operador **IN** permite verificar se o valor de uma coluna corresponde a qualquer item dentro de uma lista predefinida. Ele atua como um substituto elegante para múltiplas condições `OR`.

### Exemplo de Uso
Se você deseja listar clientes de países específicos:
```sql
SELECT * FROM Customers WHERE Country IN ('Germany', 'France', 'UK');
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_in)

O verdadeiro poder do `IN` surge com **subconsultas (subqueries)**. Você pode filtrar clientes com base em dados de outra tabela:
```sql
SELECT * FROM Customers 
WHERE CustomerID IN (SELECT CustomerID FROM Orders);
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_in2)

## Operador MySQL BETWEEN

O operador **BETWEEN** é utilizado para selecionar valores dentro de um intervalo inclusivo. Ele simplifica expressões de comparação como `>=` e `<=`.

**Nota:** O intervalo definido pelo `BETWEEN` é inclusivo, contemplando tanto o limite inicial quanto o final.

### Filtragem de Dados
Seja para valores numéricos, alfabéticos ou temporais, a lógica se mantém:
```sql
SELECT * FROM Products WHERE Price BETWEEN 10 AND 20;
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_between)

Para datas, certifique-se de usar o formato `YYYY-MM-DD`:
```sql
SELECT * FROM Orders WHERE OrderDate BETWEEN '1996-07-01' AND '1996-07-31';
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_between_date2)

---

Finalmente, para que os resultados das nossas consultas sejam apresentados de forma profissional e compreensível, utilizamos os **Aliases**.

## MySQL Aliases

Um **alias** (apelido) é um identificador temporário para colunas ou tabelas, criado com a palavra-chave `AS`. Ele não altera o esquema do banco, servindo apenas para tornar o output das queries mais claro.

### Alias para Colunas
Ideal para transformar nomes técnicos em labels amigáveis:
```sql
SELECT CustomerName AS Customer, ContactName AS "Contact Person"
FROM Customers;
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_alias_column)

### Alias para Tabelas
Em consultas que envolvem múltiplas tabelas, os aliases reduzem a verbosidade e melhoram a legibilidade:
```sql
SELECT o.OrderID, o.OrderDate, c.CustomerName
FROM Customers AS c, Orders AS o
WHERE c.CustomerID = o.CustomerID;
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_alias_table)

**Dica de Arquiteto:** A adoção de aliases é recomendada sempre que houver mais de uma tabela envolvida na query ou quando forem aplicadas funções de agregação, garantindo que o relatório final seja elegante e de fácil interpretação.


---

<p align="center">
  <a href="Capítulo_08_-_Funções_de_Agregação_e_Resumo_de_Dados.md">⬅️ Anterior</a> | <a href="Capítulo_10_-_Relatórios_e_Agrupamentos_de_Dados.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---