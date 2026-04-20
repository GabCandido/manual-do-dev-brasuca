## Arrays em R

Diferente das **matrizes**, que são restritas a duas dimensões (linhas e colunas), os **arrays** em R permitem a manipulação de dados com mais de duas dimensões. Pense em um array como uma estrutura capaz de armazenar dados em um formato cúbico ou multidimensional, sendo fundamental para modelagem estatística complexa e análise de dados que exigem estratificação profunda (como séries temporais com múltiplas variáveis ou dados sensoriais).

Para criar um array, utilizamos a função `array()`. O argumento `dim` é o pilar que define a estrutura do objeto.

```r
# Criamos um vetor com valores de 1 a 24
thisarray <- c(1:24)

# Transformamos o vetor em um array multidimensional
# dim = c(linhas, colunas, camadas)
multiarray <- array(thisarray, dim = c(4, 3, 2))

multiarray
```
[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_array)

**Explicação do código:**
No exemplo acima, definimos `dim = c(4, 3, 2)`. Isso instrui o R a organizar os 24 elementos em uma estrutura composta por:
*   **4 linhas**
*   **3 colunas**
*   **2 camadas** (níveis de matriz)

**Nota:** Arrays são estruturas homogêneas; isso significa que eles **podem conter apenas um tipo de dado** (todos numéricos, todos caracteres, etc.).

---

## Acessando Itens em um Array

A extração de dados em um array multidimensional segue a lógica de coordenadas posicional. Utilizamos os colchetes `[]` para navegar pelas dimensões.

```r
thisarray <- c(1:24)
multiarray <- array(thisarray, dim = c(4, 3, 2))

# Acessa o elemento na linha 2, coluna 3, da segunda matriz (camada 2)
multiarray[2, 3, 2]
```
[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_array_access)

**Sintaxe:** `array[linha, coluna, nível]`

Você também pode extrair fatias inteiras de dados usando a função `c()` dentro da indexação:

```r
# Acessando a primeira linha de todas as matrizes
multiarray[c(1), , 1]

# Acessando a primeira coluna da primeira matriz
multiarray[, c(1), 1]
```
[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_array_access_rc)

**Observação:** Ao deixar um espaço vazio entre as vírgulas, você instrui o R a retornar *todos* os elementos daquela dimensão.
*   Uma vírgula antes do `c()` refere-se à **coluna**.
*   Uma vírgula após o `c()` refere-se à **linha**.

---

## Verificação e Estrutura

### Verificar se um item existe
Para validar a presença de um valor dentro do seu conjunto de dados, utilizamos o operador binário `%in%`. Este é um recurso poderoso para limpeza de dados e filtragem condicional.

```r
# Retorna TRUE se o valor 2 existir no array, caso contrário, FALSE
2 %in% multiarray
```
[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_array_check)

### Dimensões e Comprimento
*   **`dim()`**: Retorna um vetor contendo a contagem exata de linhas, colunas e camadas. Essencial para verificar se os dados foram importados ou processados com a forma esperada.
*   **`length()`**: Retorna o número total de elementos contidos em todo o array.

```r
# Verificando a estrutura (4, 3, 2)
dim(multiarray)

# Verificando o total de elementos (24)
length(multiarray)
```
[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_array_dim)
[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_array_length)

---

## Iterando sobre um Array

Para processar cada item individualmente, o laço `for` é a ferramenta de controle de fluxo mais adequada. Ao passar um array por um loop, o R percorrerá cada elemento seguindo a ordem de preenchimento original.

```r
for(x in multiarray){
  print(x)
}
```
[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_array_loop)

**Por que usar loops?** Embora operações vetorizadas sejam preferíveis em R, o `for` loop é indispensável quando a lógica de processamento exige uma verificação complexa ou uma transformação que depende do valor anterior do elemento dentro da estrutura.

<br>

---

<p align="center">
  <a href="31_Matrices.md">⬅️ Anterior</a> | <a href="33_Data_Frames.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---