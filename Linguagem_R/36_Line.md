## Gráficos de Linha em R

Um gráfico de linha é uma das ferramentas mais fundamentais na visualização de dados. Ele utiliza uma linha contínua para conectar pontos de dados, permitindo identificar tendências, flutuações e padrões ao longo de um eixo, geralmente o tempo ou uma sequência numérica.

No ecossistema R, a função `plot()` é o motor gráfico versátil que permite criar essas representações de forma direta.

### Criando sua primeira linha

Para converter o comportamento padrão de dispersão da função `plot()` em um gráfico de linhas, utilizamos o parâmetro `type` com o argumento `"l"` (abreviação para *line*).

```r
plot(1:10, type="l")
```

**Explicação:** O argumento `1:10` gera uma sequência de números de 1 a 10. Ao definir `type="l"`, instruímos o R a conectar esses pontos ordenadamente, em vez de apenas plotá-los como pontos isolados no plano cartesiano.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_graph_plot_line)

---

### Personalizando a cor

A legibilidade é a chave para uma boa visualização. O R permite que você altere a cor da linha utilizando o parâmetro `col` (*color*).

```r
plot(1:10, type="l", col="blue")
```

**Insight:** Utilizar cores distintas é essencial quando você precisa destacar um gráfico específico em um relatório ou quando deseja associar visualmente uma variável a uma categoria (ex: azul para "vendas" e vermelho para "custos").

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_graph_line_color)

---

### Ajustando a espessura da linha

Para enfatizar uma tendência ou melhorar o contraste visual em apresentações, ajustamos a espessura da linha através do parâmetro `lwd` (*line width*).

```r
plot(1:10, type="l", lwd=2)
```

**Nota:** O valor padrão é `1`. Usar valores abaixo de 1 (ex: `0.5`) torna a linha mais fina, ideal para gráficos com densidade de dados muito alta, enquanto valores acima de 1 (ex: `2`) tornam a linha mais espessa, ideal para destacar a tendência principal.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_graph_line_width)

---

### Estilizando a linha (Line Styles)

Nem todas as linhas devem ser sólidas. Em contextos técnicos ou acadêmicos, é comum usar linhas tracejadas ou pontilhadas para diferenciar projeções (estimativas futuras) de dados consolidados (histórico). Controlamos isso com o parâmetro `lty` (*line type*).

```r
plot(1:10, type="l", lwd=5, lty=3)
```

**Observação:** O parâmetro `lty` aceita valores de 0 a 6, cada um representando um padrão geométrico:
* `0`: Invisível (útil para camadas ocultas).
* `1`: Sólida (padrão).
* `2`: Tracejada.
* `3`: Pontilhada.
* `4`: Traço-ponto.
* `5`: Traço longo.
* `6`: Dois traços.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_graph_line_dotted)

---

### Múltiplas Linhas em um mesmo Gráfico

Muitas vezes, o valor real da análise de dados surge da comparação. Para adicionar mais de uma série de dados ao mesmo gráfico, usamos a função `plot()` para inicializar a área e a função `lines()` para sobrepor as séries subsequentes.

```r
line1 <- c(1,2,3,4,5,10)
line2 <- c(2,5,7,8,9,10)

plot(line1, type = "l", col = "blue")
lines(line2, type="l", col = "red")
```

**Importante:** A função `plot()` cria a "tela" (limites dos eixos). A função `lines()` desenha sobre essa tela existente. Certifique-se de que os dados adicionais estejam dentro da mesma escala, caso contrário, parte do gráfico pode ser cortada.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_graph_line_multi)

<br>

---

<p align="center">
  <a href="35_Plot.md">⬅️ Anterior</a> | <a href="37_Scatterplot.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---