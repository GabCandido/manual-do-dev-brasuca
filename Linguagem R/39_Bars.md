## Gráficos de Barras (Bar Charts)

Um **Gráfico de Barras** é uma ferramenta de visualização de dados fundamental para comparar quantidades discretas entre diferentes categorias. Ele utiliza barras retangulares, onde a altura ou o comprimento de cada barra é proporcional ao valor que ela representa.

No ecossistema R, a função `barplot()` é a interface primária para renderizar esses gráficos. A escolha por este tipo de visualização é estratégica: ela permite ao espectador identificar rapidamente variações, tendências e discrepâncias entre grupos de dados.

### Criando um Gráfico de Barras Vertical

Para gerar o gráfico, definimos dois vetores: um para as categorias (eixo X) e outro para os valores numéricos correspondentes (eixo Y).

```r
# Definindo as categorias no eixo X
x <- c("A", "B", "C", "D")

# Definindo os valores correspondentes no eixo Y
y <- c(2, 4, 6, 8)

# Gerando o gráfico de barras
barplot(y, names.arg = x)
```

**Explicação técnica:**
*   `x`: Vetor que armazena os rótulos das categorias.
*   `y`: Vetor que contém a magnitude dos dados.
*   `names.arg`: Argumento essencial que mapeia os rótulos definidos em `x` para cada barra correspondente. Sem ele, o gráfico exibiria apenas os números das colunas.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_graph_bar)

---

### Customização de Cores

A percepção visual é crucial na análise de dados. Podemos utilizar o parâmetro `col` para atribuir cores às barras, facilitando a diferenciação ou destacando informações específicas em um dashboard.

```r
barplot(y, names.arg = x, col = "red")
```

**Observação:** O R aceita nomes de cores em formato string (como "red", "blue", "green") ou códigos hexadecimais, o que permite uma integração precisa com guias de estilo (branding) de empresas.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_graph_bar_col)

---

### Textura e Densidade

Em relatórios impressos em preto e branco ou quando é necessário distinguir barras sem depender apenas da matiz (cor), utilizamos a **textura**. O parâmetro `density` controla o sombreamento interno das barras.

```r
barplot(y, names.arg = x, density = 10)
```

**Nota:** O valor atribuído a `density` define a quantidade de linhas por polegada quadrada. Valores mais altos resultam em barras visualmente mais "densas" ou preenchidas.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_graph_bar_density)

---

### Ajuste de Largura das Barras

Às vezes, queremos enfatizar a importância de uma categoria específica ou acomodar rótulos mais longos no eixo horizontal. O parâmetro `width` permite o ajuste fino do tamanho das barras.

```r
barplot(y, names.arg = x, width = c(1, 2, 3, 4))
```

**Insight:** Ao passar um vetor para `width`, você pode definir larguras variáveis para cada barra, o que é útil para representar pesos ou importâncias relativas além do valor do eixo Y.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_graph_bar_width)

---

### Gráficos de Barras Horizontais

Quando temos categorias com nomes longos, o gráfico de barras verticais pode sofrer com problemas de legibilidade no eixo X. Nestes casos, a rotação para o layout horizontal é a solução mais profissional.

```r
barplot(y, names.arg = x, horiz = TRUE)
```

**Por que utilizar?** O layout horizontal é preferível em interfaces de usuário (UIs) onde o espaço lateral é limitado, permitindo uma lista de categorias mais legível e organizada verticalmente.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_graph_bar_hor)

<br>

---

<p align="center">
  <a href="38_Pie_Charts.md">⬅️ Anterior</a> | <a href="40_Statistics_Intro.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---