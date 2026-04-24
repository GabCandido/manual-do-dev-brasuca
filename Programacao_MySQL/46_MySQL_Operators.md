## Operadores no MySQL

Os **operadores** no MySQL são palavras-chave reservadas ou símbolos especiais utilizados para realizar operações sobre valores de dados. Eles são o motor lógico que permite manipular colunas, filtrar resultados e realizar cálculos diretamente dentro do banco de dados.

Você utilizará esses operadores em comandos como `SELECT` (para definir o que buscar), `WHERE` (para filtrar registros) e `LIKE` (para buscas por padrões), sendo essenciais para a construção de queries eficientes.

Os operadores no MySQL são categorizados da seguinte forma:

*   **Aritméticos:** Cálculos matemáticos básicos.
*   **Comparação:** Testam a relação entre dois valores.
*   **Compostos:** Realizam uma operação e atribuem o resultado a uma variável.
*   **Bitwise:** Operam em nível de bits (binário).
*   **Lógicos:** Combinam múltiplos critérios de busca.

---

## Operadores Aritméticos

Utilizados para realizar cálculos matemáticos com valores numéricos armazenados em suas tabelas.

| Operador | Descrição | Exemplo |
| :--- | :--- | :--- |
| `+` | Adição | [🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_op_add) |
| `-` | Subtração | [🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_op_subtract) |
| `*` | Multiplicação | [🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_op_multiply) |
| `/` | Divisão | [🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_op_divide) |
| `%` | Módulo (Resto da divisão) | [🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_op_modulo) |

---

## Operadores de Comparação

Estes são, talvez, os operadores mais utilizados no dia a dia. Eles retornam um valor booleano (TRUE ou FALSE), definindo quais linhas serão incluídas ou excluídas em uma consulta.

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

## Operadores Compostos

Os **operadores compostos** permitem realizar uma operação aritmética ou lógica em um valor e, simultaneamente, atribuir o resultado de volta a essa variável. São amplamente utilizados em **Stored Procedures** e gatilhos (**Triggers**) para manipular contadores e acumuladores.

| Operador | Descrição |
| :--- | :--- |
| `+=` | Adiciona e atribui |
| `-=` | Subtrai e atribui |
| `*=` | Multiplica e atribui |
| `/=` | Divide e atribui |
| `%=` | Módulo e atribui |
| `&=` | Bitwise AND e atribui |
| `^-=` | Bitwise Exclusive OR e atribui |
| `\|*=` | Bitwise OR e atribui |

---

## Operadores Bitwise

Estes operadores manipulam dados no nível de bits, sendo cruciais para sistemas de permissões complexas ou processamento de sinal de baixo nível.

| Operador | Descrição |
| :--- | :--- |
| `&` | Bitwise AND |
| `\|` | Bitwise OR |
| `^` | Bitwise Exclusive OR (XOR) |

---

## Operadores Lógicos

Os **operadores lógicos** permitem construir critérios complexos de filtragem. Eles determinam a veracidade de uma condição baseada em múltiplos inputs.

| Operador | Descrição | Exemplo |
| :--- | :--- | :--- |
| `ALL` | TRUE se todos os valores da subconsulta atenderem à condição | [🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_op_all) |
| `AND` | TRUE se todas as condições combinadas forem verdadeiras | [🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_op_and) |
| `ANY` | TRUE se qualquer valor da subconsulta atender à condição | [🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_op_any) |
| `BETWEEN` | TRUE se o valor estiver dentro de um intervalo inclusivo | [🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_op_between) |
| `EXISTS` | TRUE se a subconsulta retornar um ou mais registros | [🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_op_exists) |
| `IN` | TRUE se o operando for igual a qualquer valor em uma lista | [🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_op_in) |
| `LIKE` | TRUE se o operando corresponder a um padrão (regex simplificado) | [🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_op_like) |
| `NOT` | Inverte o valor lógico da condição | [🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_op_not) |
| `OR` | TRUE se pelo menos uma das condições combinadas for verdadeira | [🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_op_or) |
| `SOME` | Sinônimo de ANY | [🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_op_some) |

**Observação:** O uso de `LIKE` é fundamental para aplicações que possuem funcionalidade de busca, permitindo localizar registros mesmo quando o usuário não conhece a string exata, utilizando curingas como `%` e `_`.

<br>

---

<p align="center">
  <a href="45_MySQL_Comments.md">⬅️ Anterior</a> | <a href="47_MySQL_Create_DB.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---