## Gráficos de Dispersão (Scatter Plots)

Você já aprendeu, através do capítulo anterior sobre a função `plot()`, que o R possui recursos nativos poderosos para a visualização de dados. O **Scatter Plot** (gráfico de dispersão) é uma das ferramentas fundamentais da estatística descritiva, sendo utilizado para exibir o relacionamento entre duas variáveis numéricas.

Cada ponto no gráfico representa uma observação individual no seu conjunto de dados. Para construí-lo, você precisa de dois **vetores** de mesmo comprimento: um para o eixo-x (horizontal) e outro para o eixo-y (vertical).

### Criando seu primeiro Scatter Plot

O objetivo do gráfico de dispersão é identificar padrões, tendências ou correlações entre duas métricas. Veja como representar dados simples:

```r
# Definindo os vetores de dados
x <- c(5, 7, 8, 7, 2, 2, 9, 4, 11, 12, 9, 6)
y <- c(99, 86, 87, 88, 111, 103, 87, 94, 78, 77, 85, 86)

# Gerando o gráfico
plot(x, y)
```

O código acima gera um gráfico básico onde o R mapeia automaticamente os valores de `x` e `y` como coordenadas cartesianas. Cada par de valores resulta em um ponto no plano.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_graph_scatterplot)

---

### Adicionando Contexto: Rótulos e Títulos

Um gráfico sem contexto é apenas uma coleção de pontos. Para tornar a visualização profissional e compreensível, utilizamos parâmetros adicionais para descrever o que os dados representam:

```r
plot(x, y, 
     main="Observação de Carros", 
     xlab="Idade do carro", 
     ylab="Velocidade do carro")
```

**Análise do código:**
*   `main`: Define o título principal do gráfico.
*   `xlab` / `ylab`: Definem os rótulos dos eixos horizontal e vertical, respectivamente.

Ao aplicar essas legendas, transformamos dados brutos em uma história. Neste exemplo, podemos observar a relação entre a idade de 12 carros e a velocidade que atingiram. Visualmente, parece haver uma tendência (quanto mais novo o carro, mais rápido), embora 12 amostras sejam poucas para uma conclusão estatística definitiva.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_graph_scatterplot_cars)

---

### Comparando Conjuntos de Dados

Frequentemente, precisamos comparar diferentes séries de dados no mesmo plano para verificar se o comportamento observado se mantém. A função `points()` é essencial para essa tarefa, pois permite "adicionar" camadas a um gráfico existente sem criar uma nova figura.

```r
# Dados do primeiro dia
x1 <- c(5, 7, 8, 7, 2, 2, 9, 4, 11, 12, 9, 6)
y1 <- c(99, 86, 87, 88, 111, 103, 87, 94, 78, 77, 85, 86)

# Dados do segundo dia
x2 <- c(2, 2, 8, 1, 15, 8, 12, 9, 7, 3, 11, 4, 7, 14, 12)
y2 <- c(100, 105, 84, 105, 90, 99, 90, 95, 94, 100, 79, 112, 91, 80, 85)

# Plotando a primeira série com customização de cor (col) e tamanho (cex)
plot(x1, y1, main="Observação de Carros", xlab="Idade", ylab="Velocidade", col="red", cex=2)

# Adicionando a segunda série
points(x2, y2, col="blue", cex=2)
```

**Observação:** O parâmetro `cex` (character expansion) é utilizado aqui para ajustar o tamanho dos pontos, tornando a leitura mais clara. A escolha de cores distintas (`col`) é uma prática de design de dados indispensável para garantir que o leitor diferencie as séries de dados instantaneamente.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_graph_scatterplot_cars2)

**Nota:** A utilização de camadas (`plot` + `points`) é uma técnica poderosa em R para análise exploratória, permitindo sobrepor modelos, médias ou conjuntos de dados históricos sobre observações atuais.

<br>

---

<p align="center">
  <a href="36_Line.md">⬅️ Anterior</a> | <a href="38_Pie_Charts.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---