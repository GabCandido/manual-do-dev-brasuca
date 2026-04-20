## Listas em R

Uma **lista** em R é um objeto que pode conter diversos tipos de dados (strings, números, vetores e até outras listas) dentro de uma única estrutura. Ao contrário dos vetores, que são homogêneos (todos os elementos devem ser do mesmo tipo), as listas oferecem a flexibilidade necessária para agrupar dados heterogêneos. Elas são estruturas ordenadas e mutáveis, sendo fundamentais para organizar resultados complexos de análises estatísticas ou importar dados estruturados em formato JSON.

Para criar uma lista, utilizamos a função `list()`:

```r
# Lista contendo strings
thislist <- list("apple", "banana", "cherry")

# Exibindo a lista
thislist
```

**Nota:** Ao imprimir a lista, o R exibirá o índice de cada elemento precedido por colchetes duplos (ex: `[[1]]`), indicando que aquele valor é um item da lista.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_lists)

---

## Acessando Elementos

Você pode acessar os itens de uma lista referenciando seu **índice** dentro de colchetes. Em R, a indexação começa em **1** (diferente de linguagens como Python ou C, que começam em 0).

```r
thislist <- list("apple", "banana", "cherry")

# Acessando o primeiro item
thislist[1]
```

O resultado será a extração do valor armazenado na primeira posição da estrutura.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_lists_access)

---

## Alterando Valores

Como as listas são mutáveis, você pode sobrescrever o conteúdo de uma posição específica utilizando o operador de atribuição `<-` sobre o índice desejado.

```r
thislist <- list("apple", "banana", "cherry")
thislist[1] <- "blackcurrant"

# Exibindo a lista atualizada
thislist
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_lists_change)

---

## Comprimento da Lista

Para verificar a quantidade de itens presentes em uma lista, utilizamos a função `length()`. Isso é essencial ao criar loops ou validar a estrutura de dados antes de processá-los.

```r
thislist <- list("apple", "banana", "cherry")

length(thislist)
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_lists_length)

---

## Verificando a Existência de Itens

Para checar se um elemento específico pertence à lista, usamos o operador `%in%`. Este comando retorna um valor booleano (`TRUE` ou `FALSE`).

```r
thislist <- list("apple", "banana", "cherry")

# Verifica se "apple" está presente
"apple" %in% thislist
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_lists_check)

---

## Adicionando Itens

Existem duas formas principais de expandir sua lista:

### 1. Adicionando ao final
Use a função `append()` para inserir um novo elemento após o último item da lista.

```r
thislist <- list("apple", "banana", "cherry")

append(thislist, "orange")
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_lists_append)

### 2. Adicionando em uma posição específica
Utilize o argumento `after` na função `append()` para definir a posição exata da nova inserção.

```r
thislist <- list("apple", "banana", "cherry")

# Adiciona "orange" após o segundo item
append(thislist, "orange", after = 2)
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_lists_append2)

---

## Removendo Itens

Para remover um item, basta criar uma nova lista excluindo o índice desejado através do sinal de menos (`-`).

```r
thislist <- list("apple", "banana", "cherry")

# Remove o primeiro item
newlist <- thislist[-1]

newlist
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_lists_remove)

---

## Intervalo de Índices (Range)

Você pode extrair uma sub-lista definindo um intervalo com o operador `:`. 

```r
thislist <- list("apple", "banana", "cherry", "orange", "kiwi", "melon", "mango")

# Retorna do segundo ao quinto item
thislist[2:5]
```

**Observação:** O intervalo em R é inclusivo. Ou seja, os elementos nas posições 2 e 5 são incluídos no resultado final.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_lists_range)

---

## Iterando sobre uma Lista

Para percorrer todos os itens de uma lista e realizar alguma ação (como imprimir ou processar dados), utilize o loop `for`.

```r
thislist <- list("apple", "banana", "cherry")

for (x in thislist) {
  print(x)
}
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_lists_loop)

---

## Concatenando Listas

Para unir duas ou mais listas em uma estrutura única, utilizamos a função `c()` (de *concatenate*). Isso combina todos os elementos das listas originais em uma nova lista.

```r
list1 <- list("a", "b", "c")
list2 <- list(1, 2, 3)

# Unindo list1 e list2
list3 <- c(list1, list2)

list3
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_lists_join)

<br>

---

<p align="center">
  <a href="29_Vectors.md">⬅️ Anterior</a> | <a href="31_Matrices.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---