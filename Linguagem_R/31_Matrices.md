## Matrizes em R

Uma **matriz** é uma estrutura de dados bidimensional composta por linhas e colunas. Em ciência de dados e análise estatística, as matrizes são fundamentais para organizar conjuntos de dados que possuem um formato tabular homogêneo (onde todos os elementos devem ser do mesmo tipo de dado).

Uma **coluna** representa a dimensão vertical dos dados, enquanto uma **linha** representa a dimensão horizontal.

Para criar uma matriz, utilizamos a função `matrix()`. Os argumentos `nrow` (número de linhas) e `ncol` (número de colunas) definem as dimensões da nossa estrutura.

```r
# Criando uma matriz de 3 linhas e 2 colunas
thismatrix <- matrix(c(1, 2, 3, 4, 5, 6), nrow = 3, ncol = 2)

# Exibindo a matriz no console
thismatrix
```

**Explicação:** O código acima organiza os números de 1 a 6 em um formato de grade. O R preenche a matriz coluna por coluna por padrão.

**Nota:** A função `c()` é essencial no R; ela é usada para **concatenar** (juntar) itens em um único vetor, que é a base para o conteúdo da sua matriz.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_matrices)

Você também pode criar matrizes contendo texto (strings):

```r
thismatrix <- matrix(c("apple", "banana", "cherry", "orange"), nrow = 2, ncol = 2)
thismatrix
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_matrices2)

## Acessando Itens da Matriz

Para acessar elementos específicos, utilizamos os colchetes `[ ]`. O primeiro valor indica a posição da **linha**, enquanto o segundo indica a posição da **coluna**.

```r
# Acessando o item na linha 1, coluna 2
thismatrix[1, 2]
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_matrices_access)

### Acessando linhas ou colunas inteiras
Se você omitir um dos números e deixar apenas a vírgula, o R retornará a linha ou coluna completa:

```r
# Acessando toda a segunda linha
thismatrix[2, ]

# Acessando toda a segunda coluna
thismatrix[, 2]
```

[🚀 Pratique este código (Linhas)](https://www.w3schools.com/r/tryr.asp?filename=demo_matrices_access_row)  
[🚀 Pratique este código (Colunas)](https://www.w3schools.com/r/tryr.asp?filename=demo_matrices_access_col)

Para acessar múltiplas linhas ou colunas, utilizamos a função `c()` dentro do índice:

```r
# Acessando as linhas 1 e 2
thismatrix[c(1, 2), ]

# Acessando as colunas 1 e 2
thismatrix[, c(1, 2)]
```

[🚀 Pratique este código (Múltiplas Linhas)](https://www.w3schools.com/r/tryr.asp?filename=demo_matrices_access_row2)  
[🚀 Pratique este código (Múltiplas Colunas)](https://www.w3schools.com/r/tryr.asp?filename=demo_matrices_access_col2)

## Manipulação de Estrutura: Adicionar e Remover

Podemos expandir ou reduzir matrizes usando funções de vinculação:

*   **`cbind()`**: Adiciona novas **colunas**.
*   **`rbind()`**: Adiciona novas **linhas**.

```r
# Adicionando uma coluna
newmatrix <- cbind(thismatrix, c("strawberry", "blueberry", "raspberry"))

# Adicionando uma linha
newmatrix <- rbind(thismatrix, c("strawberry", "blueberry", "raspberry"))
```

**Nota:** Ao usar `cbind` ou `rbind`, os dados adicionados devem ter o mesmo comprimento (ou ser compatíveis com o número de elementos) da dimensão correspondente da matriz existente.

[🚀 Pratique este código (Colunas)](https://www.w3schools.com/r/tryr.asp?filename=demo_matrices_add_cols)  
[🚀 Pratique este código (Linhas)](https://www.w3schools.com/r/tryr.asp?filename=demo_matrices_add_rows)

Para remover linhas ou colunas, usamos o sinal de menos `-` com a função `c()`:

```r
# Remove a primeira linha e a primeira coluna
thismatrix <- thismatrix[-c(1), -c(1)]
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_matrices_remove_rows_cols)

## Consultas e Dimensões

Para verificar se um elemento existe dentro da estrutura, usamos o operador `%in%`:

```r
"apple" %in% thismatrix
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_matrices_check)

Para obter o tamanho da matriz:

*   `dim()`: Retorna o número de linhas e colunas.
*   `length()`: Retorna o número total de células (`linhas * colunas`).

[🚀 Pratique este código (dim)](https://www.w3schools.com/r/tryr.asp?filename=demo_matrices_dim)  
[🚀 Pratique este código (length)](https://www.w3schools.com/r/tryr.asp?filename=demo_matrices_length)

## Iteração (Loops)

Podemos percorrer cada elemento de uma matriz utilizando **loops aninhados** (um dentro do outro), iterando sobre os índices de linhas e colunas:

```r
for (rows in 1:nrow(thismatrix)) {
  for (columns in 1:ncol(thismatrix)) {
    print(thismatrix[rows, columns])
  }
}
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_matrices_loop)

## Combinando Matrizes

Você pode fundir duas matrizes diferentes utilizando `rbind()` ou `cbind()`, desde que as dimensões sejam compatíveis com a operação desejada.

```r
# Combinando como linhas
Matrix_Combined <- rbind(Matrix1, Matrix2)

# Combinando como colunas
Matrix_Combined <- cbind(Matrix1, Matrix2)
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_matrices_combine)

<br>

---

<p align="center">
  <a href="30_Lists.md">⬅️ Anterior</a> | <a href="32_Arrays.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---