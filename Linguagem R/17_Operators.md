## Operadores em R

Os **operadores** são os blocos construtores fundamentais de qualquer linguagem de programação. Eles permitem manipular variáveis e valores, servindo como "verbos" que definem a ação a ser executada sobre os dados. Sem eles, seria impossível realizar desde cálculos simples até a lógica complexa de algoritmos de Data Science.

No exemplo abaixo, utilizamos o operador `+` para realizar uma soma aritmética:

```r
10 + 5
```

Este código instrui o interpretador do R a realizar a adição entre dois valores numéricos, resultando no valor `15`.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_oper)

---

## Classificação dos Operadores

O R organiza seus operadores em categorias funcionais, cada uma voltada a um propósito específico no fluxo de desenvolvimento:

*   **Operadores Aritméticos:** Cálculos matemáticos básicos.
*   **Operadores de Atribuição:** Definição e armazenamento de valores em variáveis.
*   **Operadores de Comparação:** Avaliação de relações entre valores (retornam booleanos).
*   **Operadores Lógicos:** Combinação de múltiplas condições.
*   **Operadores Diversos:** Manipulações específicas de dados e vetores.

---

## Operadores Aritméticos

Estes operadores são a base para o processamento de dados numéricos.

| Operador | Nome | Exemplo | Prática |
| :--- | :--- | :--- | :--- |
| `+` | Adição | `x + y` | [🚀 Pratique](https://www.w3schools.com/r/tryr.asp?filename=demo_oper_add) |
| `-` | Subtração | `x - y` | [🚀 Pratique](https://www.w3schools.com/r/tryr.asp?filename=demo_oper_sub) |
| `*` | Multiplicação | `x * y` | [🚀 Pratique](https://www.w3schools.com/r/tryr.asp?filename=demo_oper_mult) |
| `/` | Divisão | `x / y` | [🚀 Pratique](https://www.w3schools.com/r/tryr.asp?filename=demo_oper_div) |
| `^` | Exponenciação | `x ^ y` | [🚀 Pratique](https://www.w3schools.com/r/tryr.asp?filename=demo_oper_exp) |
| `%%` | Modulus | `x %% y` | [🚀 Pratique](https://www.w3schools.com/r/tryr.asp?filename=demo_oper_mod) |
| `%/%` | Divisão Inteira | `x %/% y` | [🚀 Pratique](https://www.w3schools.com/r/tryr.asp?filename=demo_oper_int_div) |

**Observação:** O **Modulus** (`%%`) retorna o resto da divisão, uma ferramenta essencial para verificar paridade ou realizar operações cíclicas. Já a **Divisão Inteira** (`%/%`) descarta a parte decimal do resultado.

---

## Operadores de Atribuição

Em R, a atribuição é o ato de associar um valor a um nome de variável. É assim que persistimos estados na memória durante a execução de um script.

```r
my_var <- 3      # Atribuição padrão
my_var <<- 3     # Atribuição de escopo global
3 -> my_var      # Atribuição à direita
3 ->> my_var     # Atribuição global à direita
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_oper_assignment)

**Nota:** O operador `<<-` é um **atribuidor global**. Ele altera o valor de uma variável fora do escopo local atual (como dentro de funções). Use-o com cautela para evitar efeitos colaterais inesperados em seu código.

---

## Operadores de Comparação

Fundamentais para o fluxo de controle (como `if` e `while`), estes operadores testam relações de igualdade ou magnitude.

| Operador | Nome | Exemplo | Prática |
| :--- | :--- | :--- | :--- |
| `==` | Igual | `x == y` | [🚀 Pratique](https://www.w3schools.com/r/tryr.asp?filename=demo_oper_compare1) |
| `!=` | Diferente | `x != y` | [🚀 Pratique](https://www.w3schools.com/r/tryr.asp?filename=demo_oper_compare2) |
| `>` | Maior que | `x > y` | [🚀 Pratique](https://www.w3schools.com/r/tryr.asp?filename=demo_oper_compare4) |
| `<` | Menor que | `x < y` | [🚀 Pratique](https://www.w3schools.com/r/tryr.asp?filename=demo_oper_compare5) |
| `>=` | Maior ou igual | `x >= y` | [🚀 Pratique](https://www.w3schools.com/r/tryr.asp?filename=demo_oper_compare6) |
| `<=` | Menor ou igual | `x <= y` | [🚀 Pratique](https://www.w3schools.com/r/tryr.asp?filename=demo_oper_compare7) |

---

## Operadores Lógicos

Permitem construir expressões booleanas complexas, avaliando múltiplas condições simultaneamente.

*   `&` (Element-wise AND): Avalia cada elemento de um vetor, retornando `TRUE` apenas se ambos forem verdadeiros.
*   `&&` (Logical AND): Avalia apenas o primeiro elemento de cada vetor; útil em condições de controle de fluxo.
*   `|` (Element-wise OR): Retorna `TRUE` se pelo menos um dos elementos for verdadeiro.
*   `||` (Logical OR): Avalia apenas o primeiro elemento para verificar se um ou outro é verdadeiro.
*   `!` (Logical NOT): Inverte o valor booleano (`TRUE` vira `FALSE` e vice-versa).

---

## Operadores Diversos

Estes operadores são específicos do ecossistema R e facilitam a manipulação de estruturas de dados:

| Operador | Descrição | Exemplo |
| :--- | :--- | :--- |
| `:` | Cria uma sequência de números | `x <- 1:10` |
| `%in%` | Verifica se um elemento pertence a um vetor | `x %in% y` |
| `%*%` | Multiplicação de matrizes | `x <- Matrix1 %*% Matrix2` |

**Nota:** A multiplicação de matrizes é um pilar em estatística computacional e aprendizado de máquina. Estudaremos sua aplicação detalhada em capítulos futuros.

<br>

---

<p align="center">
  <a href="16_Booleans.md">⬅️ Anterior</a> | <a href="18_If...Else.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---