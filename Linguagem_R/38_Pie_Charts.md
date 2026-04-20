## Gráficos de Setores (Pie Charts) no R

Um **gráfico de setores** (comumente chamado de gráfico de pizza) é uma representação circular que divide dados em fatias, onde cada fatia representa uma proporção do todo. No R, utilizamos este tipo de visualização para exibir rapidamente a composição relativa de um conjunto de dados.

### A função `pie()`

O coração da visualização de setores no R é a função `pie()`. O propósito desta função é transformar um vetor numérico em uma representação gráfica circular, onde a área de cada setor é proporcional ao seu valor em relação à soma total dos dados.

```r
# Criando um vetor de valores
x <- c(10, 20, 30, 40)

# Gerando o gráfico de setores
pie(x)
```

**Explicação do código:**
Ao passar o vetor `x` para `pie()`, o R calcula automaticamente a proporção de cada elemento usando a fórmula: `valor / soma(x)`. O gráfico começa a ser desenhado a partir do eixo x, percorrendo o círculo no sentido **anti-horário**.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_graph_pie)

**Nota:** O tamanho de cada fatia é determinado estritamente pela relação matemática entre o valor individual e o total do vetor.

---

## Ajustando o Ângulo Inicial

Às vezes, por razões de legibilidade ou design, você desejará alterar o ponto de partida do primeiro setor. Para isso, utilizamos o parâmetro `init.angle`.

```r
# Definindo o início do primeiro setor em 90 graus
pie(x, init.angle = 90)
```

**Explicação do código:**
O parâmetro `init.angle` aceita um valor numérico em graus. O padrão do R é 0 (eixo horizontal à direita). Ao definir como 90, o primeiro elemento do vetor começará no topo do círculo.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_graph_pie_start_angle)

---

## Rótulos e Títulos

Um gráfico sem contexto é apenas uma forma geométrica. Para tornar a visualização compreensível, adicionamos legendas e um título principal.

```r
# Definindo rótulos para as categorias
mylabel <- c("Apples", "Bananas", "Cherries", "Dates")

# Adicionando rótulos e título ao gráfico
pie(x, label = mylabel, main = "Frutas")
```

**Explicação do código:**
- `label`: Recebe um vetor de caracteres que será exibido ao lado de cada fatia.
- `main`: Define o título que aparece acima do gráfico, essencial para identificar o que os dados representam em um relatório ou dashboard.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_graph_pie_labels)

---

## Personalização de Cores

A estética influencia diretamente a interpretação dos dados. Você pode utilizar o parâmetro `col` para atribuir uma paleta de cores personalizada ao seu gráfico.

```r
# Definindo um vetor de cores
colors <- c("blue", "yellow", "green", "black")

# Aplicando cores ao gráfico
pie(x, label = mylabel, main = "Frutas", col = colors)
```

**Explicação do código:**
O parâmetro `col` mapeia cada elemento do vetor de cores para as fatias correspondentes no gráfico, na mesma ordem em que aparecem no vetor de dados original.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_graph_pie_col)

---

## Adicionando uma Legenda

Para gráficos com categorias complexas, é uma boa prática remover os rótulos internos e utilizar uma **legenda** (legend), o que evita sobreposição de texto e melhora a clareza.

```r
# Criando a legenda explicativa
pie(x, label = mylabel, main = "Pie Chart", col = colors)

# Posicionando a caixa de legenda
legend("bottomright", mylabel, fill = colors)
```

**Explicação do código:**
A função `legend()` é chamada separadamente da função `pie()`. O primeiro argumento define a posição (como `"bottomright"`, `"topleft"`, `"center"`, etc.), o segundo são os textos dos rótulos, e `fill` vincula as cores aplicadas anteriormente à caixa de legenda.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_graph_pie_legend)

**Observação:** O R permite posicionar a legenda em diversas áreas do gráfico usando argumentos como `bottom`, `left`, `right`, `top`, além das variações diagonais como `topright` ou `bottomleft`, garantindo flexibilidade total para o seu layout.

<br>

---

<p align="center">
  <a href="37_Scatterplot.md">⬅️ Anterior</a> | <a href="39_Bars.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---