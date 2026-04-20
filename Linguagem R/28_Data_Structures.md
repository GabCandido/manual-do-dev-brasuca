## Estruturas de Dados em R

As **estruturas de dados** são os alicerces de qualquer linguagem de programação. Elas definem como os valores são armazenados, organizados e acessados na memória do computador. Em R, a escolha da estrutura correta é fundamental, pois cada uma possui propriedades específicas para manipular tipos diferentes de informações, garantindo eficiência na análise estatística e processamento de dados.

R oferece cinco estruturas nativas principais: **Vectors**, **Lists**, **Matrices**, **Arrays** e **Data Frames**.

---

## Vectors (Vetores)

O **vetor** é a estrutura mais básica e fundamental em R. Ele é uma sequência de elementos que devem ser obrigatoriamente do **mesmo tipo** (todos numéricos, todos strings, etc.). Pense nele como uma "lista simples" onde a homogeneidade é garantida.

```r
# Criando um vetor de strings
fruits <- c("banana", "apple", "orange")

# Exibindo o vetor
fruits
```

**Nota:** O comando `c()` significa *concatenate* (concatenar). Ele é a função padrão para agrupar elementos em um único vetor.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_data_structures_vectors)

---

## Lists (Listas)

Diferente dos vetores, uma **lista** é uma estrutura heterogênea. Ela permite que você combine tipos de dados variados — como números, strings, vetores e até outras listas — em um único objeto. É a estrutura ideal quando você precisa agrupar informações que não seguem um padrão único.

```r
# Lista com tipos de dados misturados
thislist <- list("apple", "banana", 50, 100)

# Exibindo a lista
thislist
```

**Observação:** Listas são extremamente versáteis em R e são frequentemente usadas para armazenar resultados complexos de modelos estatísticos.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_data_structures_lists)

---

## Matrices (Matrizes)

Uma **matriz** é uma estrutura de dados bidimensional (2D) que organiza elementos do mesmo tipo em linhas e colunas. É a representação matemática clássica de uma tabela onde a estrutura é rígida.

```r
# Criando uma matriz 3x2 (3 linhas, 2 colunas)
thismatrix <- matrix(c(1,2,3,4,5,6), nrow = 3, ncol = 2)

# Exibindo a matriz
thismatrix
```

Utilize os argumentos `nrow` (número de linhas) e `ncol` (número de colunas) para definir as dimensões da sua matriz.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_data_structures_matrices)

---

## Arrays (Matrizes Multidimensionais)

Um **array** estende o conceito da matriz. Enquanto uma matriz está limitada a duas dimensões (linhas e colunas), um array pode armazenar elementos em múltiplas dimensões (3D ou mais). Todos os elementos, assim como na matriz, devem ser do mesmo tipo.

```r
# Criando um vetor base
thisarray <- c(1:24)

# Convertendo para um array com dimensões 4x3x2
multiarray <- array(thisarray, dim = c(4, 3, 2))
multiarray
```

Arrays são essenciais em computação científica, permitindo modelar dados complexos como séries temporais com múltiplas variáveis ou imagens (que possuem altura, largura e canais de cor).

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_data_structures_arrays)

---

## Data Frames

O **Data Frame** é a estrutura mais utilizada em Ciência de Dados com R. Ele se comporta como uma tabela de planilha ou um banco de dados SQL: cada coluna pode conter um tipo de dado diferente (uma coluna numérica, outra de texto, etc.), mas todos os elementos de uma coluna específica devem ter o mesmo tipo.

```r
# Criando um Data Frame
Data_Frame <- data.frame (
  Training = c("Strength", "Stamina", "Other"),
  Pulse = c(100, 150, 120),
  Duration = c(60, 30, 45)
)

# Exibindo o Data Frame
Data_Frame
```

**Por que usar Data Frames?** Eles são a espinha dorsal de bibliotecas poderosas como `tidyverse` e `ggplot2`, sendo a forma padrão de ler arquivos CSV e manipular datasets reais.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_data_structures_df)

---

## Resumo Comparativo

| Estrutura | Contém | Mesmos Tipos? | Caso de Uso |
| :--- | :--- | :--- | :--- |
| **Vector** | Linha única de valores | Sim | Sequências simples e cálculos matemáticos |
| **List** | Múltiplos tipos | Não | Agrupar dados heterogêneos |
| **Matrix** | Valores 2D | Sim | Tabelas com dados numéricos |
| **Array** | Valores multidimensionais | Sim | Dados 3D ou de alta dimensionalidade |
| **Data Frame** | Colunas de tipos mistos | Não | Manipulação de tabelas e análise de dados |

<br>

---

<p align="center">
  <a href="27_Global_Variables.md">⬅️ Anterior</a> | <a href="29_Vectors.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---