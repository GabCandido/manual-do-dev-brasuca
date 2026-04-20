## Vetores (Vectors)

Um **vetor** é a estrutura de dados mais básica e fundamental no R. Em termos simples, é uma sequência de elementos que compartilham o mesmo tipo de dado. Se você vem de outras linguagens de programação, pode pensar neles como arrays unidimensionais.

O R é otimizado para operações estatísticas e matemáticas; por isso, o vetor é a peça fundamental. Quase tudo o que você manipula no R (mesmo valores únicos) é armazenado internamente como um vetor.

Para combinar elementos em um vetor, utilizamos a função `c()` (de *concatenate* ou combinar). Os itens devem ser separados por vírgulas.

### Vetores de Strings
Para criar um conjunto de caracteres, passamos as strings como argumentos para a função `c()`:

```r
# Criando um vetor de strings
fruits <- c("banana", "apple", "orange")

# Imprimindo o vetor
fruits
```
**Explicação:** A variável `fruits` agora armazena os três valores. Ao chamar `fruits`, o R exibirá o conteúdo da estrutura.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_vector_strings)

---

### Vetores Numéricos
Da mesma forma, podemos agrupar números para realizar cálculos estatísticos ou processamento em lote:

```r
# Criando um vetor de valores numéricos
numbers <- c(1, 2, 3)

numbers
```
[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_vector_num)

---

### Sequências Numéricas
Quando precisamos de uma série de números (muito comum em loops ou na geração de índices), utilizamos o operador `:` para definir um intervalo:

```r
# Criando uma sequência de 1 a 10
numbers <- 1:10

numbers
```
**Nota:** O operador `:` cria uma sequência crescente ou decrescente com incremento de 1.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_vector_colon)

Se você utilizar decimais, o R seguirá o incremento de 1. Caso o último elemento definido não se encaixe na sequência natural, o R simplesmente o ignora:

```r
# Exemplo com decimais
numbers1 <- 1.5:6.5 # Resultado: 1.5 2.5 3.5 4.5 5.5 6.5
numbers2 <- 1.5:6.3 # Resultado: 1.5 2.5 3.5 4.5 5.5
```
[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_vector_colon2)

---

### Vetores Lógicos
Vetores também podem armazenar valores booleanos (`TRUE` ou `FALSE`), fundamentais para filtros de dados e testes condicionais:

```r
# Vetor de valores lógicos
log_values <- c(TRUE, FALSE, TRUE, FALSE)
```
[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_vector_logical)

---

## Tamanho do Vetor
Para verificar quantos elementos existem em um vetor, utilizamos a função `length()`:

```r
fruits <- c("banana", "apple", "orange")
length(fruits)
```
**Insight:** Saber o comprimento de um vetor é essencial antes de iterar sobre ele ou realizar operações de combinação (como unir dois vetores).

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_vector_length)

---

## Ordenando Vetores
A função `sort()` reorganiza os elementos. Para strings, a ordenação é alfabética; para números, é numérica:

```r
fruits <- c("banana", "apple", "orange", "mango", "lemon")
numbers <- c(13, 3, 5, 7, 20, 2)

sort(fruits)   # Ordena alfabeticamente
sort(numbers)  # Ordena numericamente
```
[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_vector_sort)

---

## Acessando Elementos
No R, o acesso é feito por **índices**. Diferente de linguagens como C ou Python (que começam em 0), **o R começa a indexação no 1**. Utilizamos colchetes `[]` para acessar posições específicas:

```r
fruits <- c("banana", "apple", "orange")
fruits[1] # Acessa o primeiro item: "banana"
```

Para selecionar vários itens, passe um vetor de índices dentro dos colchetes:
```r
fruits[c(1, 3)] # Seleciona o primeiro e o terceiro item
```

**Dica Pro:** Usar índices negativos exclui os itens daquela posição, retornando todo o restante do vetor:
```r
fruits[c(-1)] # Retorna tudo, menos o primeiro item
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_vector_access)

---

## Modificando Itens
Para atualizar um valor, basta referenciar o índice e atribuir um novo valor:

```r
fruits <- c("banana", "apple", "orange")
fruits[1] <- "pear" # Substitui "banana" por "pear"
```
[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_vector_modify)

---

## Repetindo Vetores
A função `rep()` é poderosa para criar conjuntos de dados repetitivos ou mock data para testes:

*   **each:** Repete cada elemento individualmente `n` vezes.
*   **times:** Repete o vetor completo `n` vezes.

```r
# Repete cada valor 3 vezes
rep(c(1,2,3), each = 3) 

# Repete a sequência inteira 3 vezes
rep(c(1,2,3), times = 3)
```
[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_vector_repeat)

---

## Geração de Sequências Customizadas
Enquanto `:` gera sequências com passo 1, a função `seq()` permite definir intervalos personalizados com o parâmetro `by`:

```r
# Sequência de 0 a 100, pulando de 20 em 20
numbers <- seq(from = 0, to = 100, by = 20)
```
**Observação:** `seq()` é extremamente útil quando você precisa criar eixos para gráficos ou janelas de tempo em séries temporais.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_vector_seq)

<br>

---

<p align="center">
  <a href="28_Data_Structures.md">⬅️ Anterior</a> | <a href="30_Lists.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---