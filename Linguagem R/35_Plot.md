## Plotting no R

A função `plot()` é a espinha dorsal da visualização de dados base no R. O seu propósito central é a **representação gráfica bidimensional**, permitindo transformar vetores de dados em coordenadas visuais. Seja para uma análise exploratória rápida ou para a criação de diagramas complexos, entender como o R mapeia números em posições espaciais é fundamental para qualquer cientista de dados.

### Conceitos Básicos de Coordenadas

A forma mais simples de utilizar a função `plot()` é passando dois parâmetros: o primeiro define o ponto no **x-axis** (eixo horizontal) e o segundo define o ponto no **y-axis** (eixo vertical).

```r
plot(1, 3)
```

**Resultado:** O R desenha um gráfico contendo um único ponto localizado na intersecção da coordenada `x=1` e `y=3`.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_graph_plot_simple)

---

### Trabalhando com Vetores

Para desenhar múltiplos pontos, não precisamos de loops. O R utiliza a natureza vetorial da linguagem através da função `c()` (combine). Ao passar dois vetores de mesmo comprimento, o R mapeia cada par de elementos como um ponto individual.

```r
plot(c(1, 8), c(3, 10))
```

**Explicação:** Aqui, instruímos o interpretador a desenhar dois pontos: o primeiro em `(1, 3)` e o segundo em `(8, 10)`.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_graph_plot)

---

## Múltiplos Pontos e Variáveis

Em cenários reais, raramente digitamos os valores diretamente na função. Normalmente, armazenamos nossos conjuntos de dados em variáveis para facilitar a manipulação e a reutilização.

```r
x <- c(1, 2, 3, 4, 5)
y <- c(3, 7, 8, 9, 12)

plot(x, y)
```

**Observação:** O R é altamente eficiente ao lidar com vetores. Certifique-se sempre de que ambos os vetores possuam o mesmo comprimento; caso contrário, o R emitirá um aviso e o gráfico não será renderizado corretamente.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_graph_plot3)

---

### Sequências de Pontos

Se você precisar gerar uma progressão aritmética simples, pode utilizar o operador `:` (operador de sequência). Ele cria um vetor contendo todos os inteiros entre os dois números fornecidos.

```r
plot(1:10)
```

**Nota:** Quando apenas um argumento é passado para `plot()`, o R assume que os valores fornecidos são para o eixo Y, e utiliza o índice da sequência (1, 2, 3...) como o eixo X.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_graph_plot_seq)

---

## Conectando Pontos com Linhas

Muitas vezes, em séries temporais ou funções matemáticas, queremos observar a tendência entre os pontos. Para isso, utilizamos o parâmetro `type`. Ao definir `type="l"` (de *line*), o R desenha um traço conectando os pontos sequencialmente.

```r
plot(1:10, type="l")
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_graph_plot_line)

---

## Rotulagem e Títulos

Um gráfico sem contexto é apenas uma imagem abstrata. Para torná-lo profissional, utilizamos argumentos de rotulagem:
*   `main`: Define o título principal.
*   `xlab`: Define o rótulo do eixo X.
*   `ylab`: Define o rótulo do eixo Y.

```r
plot(1:10, main="Meu Gráfico", xlab="Eixo X", ylab="Eixo Y")
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_graph_plot_labels)

---

## Personalização Visual

O R permite um controle granular sobre a estética dos elementos gráficos através de parâmetros adicionais:

### Cores e Tamanho
*   `col`: Define a cor dos pontos ou linhas.
*   `cex`: Controla a escala de tamanho (*Character Expansion*). O valor `1` é o padrão, `0.5` reduz pela metade e `2` dobra o tamanho original.

```r
plot(1:10, col="red", cex=2)
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_graph_plot_cex)

### Formato dos Pontos (pch)
O parâmetro `pch` (*Plot Character*) permite alterar o símbolo usado para representar os dados. O R oferece uma gama de 0 a 25 para formatos pré-definidos.

```r
plot(1:10, pch=25, cex=2)
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_graph_plot_pch)

<br>

---

<p align="center">
  <a href="34_Factors.md">⬅️ Anterior</a> | <a href="36_Line.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---