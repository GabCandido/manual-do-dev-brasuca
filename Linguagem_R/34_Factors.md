## Fatores (Factors) no R

Em R, os **Fatores** são estruturas de dados especializadas utilizadas para categorizar dados e armazená-los como níveis (levels). Eles são fundamentais na análise estatística e no aprendizado de máquina, pois permitem que o interpretador do R trate variáveis categóricas de forma distinta de textos simples (*strings*).

O uso de fatores é essencial quando você possui dados que representam grupos finitos, como:
*   **Demografia:** Masculino/Feminino.
*   **Preferências Musicais:** Rock, Pop, Classic, Jazz.
*   **Intensidade de Treino:** Força, Resistência.

### Criando um Fator

Para criar um fator, utilizamos a função `factor()`, passando um vetor como argumento. O R identificará automaticamente os elementos únicos e os organizará como níveis.

```r
# Criando um fator
music_genre <- factor(c("Jazz", "Rock", "Classic", "Classic", "Pop", "Jazz", "Rock", "Jazz"))

# Exibindo o fator
music_genre
```

**Resultado esperado:**
O R exibirá os dados e listará os `Levels` encontrados em ordem alfabética por padrão.
```text
[1] Jazz    Rock    Classic Classic Pop     Jazz    Rock    Jazz
Levels: Classic Jazz Pop Rock
```
[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_factor)

### Explorando Níveis (Levels)

Muitas vezes, em um fluxo de trabalho de limpeza de dados, precisamos verificar quais são as categorias (níveis) disponíveis. A função `levels()` retorna um vetor com esses valores únicos.

```r
music_genre <- factor(c("Jazz", "Rock", "Classic", "Classic", "Pop", "Jazz", "Rock", "Jazz"))

# Extraindo os níveis do fator
levels(music_genre)
```

**Resultado esperado:**
```text
[1] "Classic" "Jazz"    "Pop"     "Rock"
```
[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_factor_levels)

**Nota:** Você pode definir manualmente a ordem ou a existência de níveis ao criar o fator através do argumento `levels`. Isso é útil para forçar uma ordenação lógica (como "Baixo", "Médio", "Alto") que não seguiria a ordem alfabética.

```r
music_genre <- factor(c("Jazz", "Rock", "Classic", "Classic", "Pop", "Jazz", "Rock", "Jazz"), 
                      levels = c("Classic", "Jazz", "Pop", "Rock", "Other"))

levels(music_genre)
```
[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_factor_levels2)

### Comprimento de um Fator

Para saber quantos elementos compõem o seu vetor de fatores, utilizamos a função `length()`.

```r
music_genre <- factor(c("Jazz", "Rock", "Classic", "Classic", "Pop", "Jazz", "Rock", "Jazz"))

length(music_genre)
```

**Resultado esperado:**
```text
[1] 8
```
[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_factor_length)

### Acessando e Modificando Fatores

Você pode acessar ou alterar itens individuais de um fator utilizando a indexação por colchetes `[]`, assim como em vetores convencionais.

#### Acessando um item
```r
music_genre[3]
```
[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_factor_access)

#### Alterando um valor
```r
music_genre[3] <- "Pop"
```
[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_factor_change)

**Atenção:** Os fatores no R são rígidos. Você não pode atribuir um valor que não faça parte dos níveis pré-definidos. Caso tente, o R gerará um aviso (*Warning*) e inserirá um valor ausente (`NA`).

```r
# Isto produzirá um erro/aviso, pois "Opera" não é um nível existente
music_genre[3] <- "Opera"
```
[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_factor_change2)

**Solução:** Se o novo valor for necessário, ele deve ser incluído na definição dos `levels` do fator desde o início:

```r
music_genre <- factor(c("Jazz", "Rock", "Classic", "Classic", "Pop", "Jazz", "Rock", "Jazz"), 
                      levels = c("Classic", "Jazz", "Pop", "Rock", "Opera"))

music_genre[3] <- "Opera"
```
[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_factor_change3)

<br>

---

<p align="center">
  <a href="33_Data_Frames.md">⬅️ Anterior</a> | <a href="35_Plot.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---