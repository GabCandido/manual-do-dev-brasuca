## Tipos de Dados em R

Em programação, o conceito de **tipo de dado** é um dos pilares fundamentais para o desenvolvimento de software. Ele define a natureza do valor armazenado em uma variável e, crucialmente, determina quais operações podem ser realizadas com esse dado.

Diferente de linguagens como C ou Java, o R é uma linguagem de **tipagem dinâmica**. Isso significa que você não precisa declarar o tipo de uma variável ao criá-la; o R é inteligente o suficiente para inferir o tipo com base no valor atribuído. Além disso, uma variável pode mudar de tipo durante a execução do script caso você reatribua um valor de natureza diferente a ela.

### Exemplo de Dinamismo
Observe como a mesma variável pode transitar entre tipos distintos:

```r
my_var <- 30    # my_var é do tipo numeric
my_var <- "Sally" # my_var agora é do tipo character (string)
```

**Explicação:** No primeiro momento, o interpretador identifica o valor `30` como um número. Ao reatribuir `"Sally"`, o R descarta o tipo anterior e transforma a variável em uma string. Essa flexibilidade é extremamente útil para análise de dados exploratória, embora exija cuidado para evitar inconsistências em sistemas complexos.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_variables2)

---

## Tipos de Dados Básicos

O R organiza seus dados em classes específicas. Conhecê-las é essencial para realizar cálculos matemáticos, manipulação de texto ou controle de fluxo lógico. Os tipos básicos são:

*   **numeric**: Números reais (ex: `10.5`, `55`, `787`). É o tipo padrão para operações aritméticas.
*   **integer**: Números inteiros. Em R, para especificar um inteiro, utilizamos o sufixo `L` (ex: `1L`, `55L`, `100L`).
*   **complex**: Números complexos contendo uma parte imaginária (ex: `9 + 3i`).
*   **character**: Também conhecido como **string** ou texto. São delimitados por aspas (ex: `"k"`, `"R is exciting"`).
*   **logical**: O tipo booleano, que assume apenas dois estados: `TRUE` ou `FALSE`.

Para verificar o tipo de dado de qualquer objeto, utilizamos a função `class()`.

### Verificação de Tipos
Veja como identificar a classe de diferentes valores utilizando o console do R:

```r
# numeric
x <- 10.5
class(x)

# integer
x <- 1000L
class(x)

# complex
x <- 9i + 3
class(x)

# character/string
x <- "R is exciting"
class(x)

# logical/boolean
x <- TRUE
class(x)
```

**Resultado esperado:** Ao executar cada bloco `class(x)`, o R retornará o nome da classe correspondente (ex: `"numeric"`, `"integer"`, `"complex"`, `"character"`, `"logical"`). 

**Nota:** O uso de `L` após um número (ex: `1000L`) não é apenas uma convenção estética; ele força o R a armazenar o valor como um número inteiro de 32 bits, o que pode ser mais eficiente em termos de memória para grandes conjuntos de dados.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_data_types)

**Observação:** Você aprenderá a manipular esses tipos de forma avançada e como eles se comportam dentro de estruturas de dados mais complexas (como vetores e listas) nos próximos capítulos.

<br>

---

<p align="center">
  <a href="10_Variable_Names.md">⬅️ Anterior</a> | <a href="12_Numbers.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---