# Capítulo 06 - Operadores Lógicos e Expressões

No ecossistema de bancos de dados relacionais, a capacidade de filtrar dados com precisão cirúrgica é fundamental para a construção de sistemas eficientes. Para isso, utilizamos **operadores**, que são palavras-chave reservadas ou símbolos especiais capazes de realizar operações sobre valores de dados, permitindo a construção de consultas complexas dentro das cláusulas `SELECT` e `WHERE`.

Os operadores no MySQL são categorizados em grupos funcionais: aritméticos, de comparação, compostos, bitwise e, principalmente, lógicos.

---

## Operadores Aritméticos e de Comparação

Antes de aprofundar na lógica de filtragem, é necessário compreender como o banco de dados manipula valores numéricos e compara relações entre dados.

### Operadores Aritméticos
Utilizados para realizar cálculos matemáticos com valores numéricos armazenados em suas tabelas.

| Operador | Descrição | Exemplo |
| :--- | :--- | :--- |
| `+` | Adição | [🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_op_add) |
| `-` | Subtração | [🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_op_subtract) |
| `*` | Multiplicação | [🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_op_multiply) |
| `/` | Divisão | [🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_op_divide) |
| `%` | Módulo (Resto da divisão) | [🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_op_modulo) |

### Operadores de Comparação
Estes operadores retornam um valor booleano (`TRUE` ou `FALSE`), definindo quais linhas serão incluídas em uma consulta.

| Operador | Descrição | Exemplo |
| :--- | :--- | :--- |
| `=` | Igual a | [🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_op_equal_to) |
| `>` | Maior que | [🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_op_greater_than) |
| `<` | Menor que | [🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_op_less_than) |
| `>=` | Maior ou igual a | [🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_op_greater_than2) |
| `<=` | Menor ou igual a | [🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_op_less_than2) |
| `<>` | Diferente de | [🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_op_not_equal_to) |

**Nota:** No padrão SQL, o operador `<>` é o mais amplamente aceito para "diferente de", embora muitos bancos suportem `!=`.

---

## Operadores Lógicos: AND, OR e NOT

Os operadores lógicos são a base da filtragem de dados. Eles permitem que você combine múltiplos critérios na cláusula `WHERE` para restringir ou ampliar o conjunto de resultados.

### O Operador AND
O operador **AND** é um componente essencial para combinar múltiplas condições de busca. Seu propósito é garantir que apenas os registros que satisfaçam **todas** as condições especificadas sejam retornados.

**Nota:** Se qualquer uma das condições for avaliada como `FALSE` ou `UNKNOWN`, o registro será excluído da seleção final.

```sql
SELECT * FROM Customers
WHERE Country = 'UK'
AND City = 'London';
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_where_and)

### O Operador OR
Ao contrário do `AND`, o operador **OR** atua como uma união lógica: ele instrui o banco de dados a retornar qualquer linha que satisfaça, pelo menos, uma das condições especificadas.

```sql
SELECT * FROM Customers
WHERE City = 'Berlin'
OR City = 'Stuttgart';
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_where_or)

### O Operador NOT
O **NOT** é utilizado para inverter o resultado de uma condição lógica. Ele é ideal para situações em que você deseja extrair "tudo, menos o que se encaixa em um padrão específico".

```sql
SELECT * FROM Customers
WHERE NOT Country = 'Germany';
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_where_not)

---

## Técnicas Avançadas de Filtragem

### Combinando AND e OR
Em cenários reais, regras de negócio exigem a mistura de filtros restritivos e inclusivos. Para evitar ambiguidades, **sempre utilize parênteses**. Eles garantem a precedência da operação, assegurando que o motor do banco de dados execute a lógica na ordem que você planejou.

```sql
SELECT * FROM Customers
WHERE Country = 'Germany'
AND (City = 'Berlin' OR City = 'Stuttgart');
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_where_and_or)

### O uso do NOT com outros operadores
O `NOT` potencializa outros operadores, permitindo uma limpeza de dados expressiva:
*   **NOT LIKE**: Exclui registros baseados em padrões de texto.
*   **NOT BETWEEN**: Exclui registros dentro de um intervalo.
*   **NOT IN**: Exclui registros presentes em uma lista específica.
*   **IS NOT NULL**: Filtra registros que possuem dados (não vazios).

---

## Documentação: Comentários no MySQL

Para manter a legibilidade de consultas complexas que utilizam múltiplos operadores, o MySQL permite o uso de comentários. Eles são ignorados pelo motor de banco de dados e servem para documentação ou testes.

*   **Linha única**: Iniciam com `-- ` (o espaço após o segundo traço é obrigatório).
*   **Múltiplas linhas**: Utilizam o formato `/* ... */`, ideal para blocos longos de texto ou para desativar temporariamente grandes trechos de código.

```sql
/* Seleciona clientes alemães de Berlim, 
   excluindo testes antigos */
SELECT * FROM Customers 
WHERE Country = 'Germany' 
AND City = 'Berlin'; -- Filtro por localidade
```

---

## Resumo de Operadores Lógicos

| Operador | Descrição |
| :--- | :--- |
| `ALL` | TRUE se todos os valores da subconsulta atenderem à condição |
| `AND` | TRUE se todas as condições combinadas forem verdadeiras |
| `ANY` | TRUE se qualquer valor da subconsulta atender à condição |
| `BETWEEN` | TRUE se o valor estiver dentro de um intervalo inclusivo |
| `EXISTS` | TRUE se a subconsulta retornar um ou mais registros |
| `IN` | TRUE se o operando for igual a qualquer valor em uma lista |
| `LIKE` | TRUE se o operando corresponder a um padrão |
| `NOT` | Inverte o valor lógico da condição |
| `OR` | TRUE se pelo menos uma das condições combinadas for verdadeira |

**Observação:** O uso correto desses operadores é o que define o desempenho e a precisão das suas aplicações. Ao realizar filtros, sempre prefira operadores de comparação direta (`>=`, `<=`) em vez de construções negadas complexas para manter a clareza e permitir a otimização de consultas pelo servidor.

<br>

---

<p align="center">
  <a href="Capítulo_05_-_Recuperação_de_Dados_e_Ordenação.md">⬅️ Anterior</a> | <a href="Capítulo_07_-_Manipulação_de_Dados__Inserção,_Atualização_e_Exclusão.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---