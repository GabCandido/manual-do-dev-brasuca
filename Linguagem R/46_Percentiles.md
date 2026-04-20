## Percentis no R

Os **percentis** são medidas estatísticas fundamentais utilizadas para compreender a distribuição de um conjunto de dados. Eles indicam o valor abaixo do qual uma determinada porcentagem de observações de um grupo cai. 

Em ciência de dados e análise estatística, percentis são cruciais para identificar *outliers*, entender a dispersão de variáveis e segmentar populações. Por exemplo, se você sabe que o percentil 75 do peso de uma frota de veículos é 3.610 libras, você tem a garantia estatística de que 75% dos veículos possuem esse peso ou menos.

### Analisando Percentis com a função `quantile()`

No R, a forma mais eficiente de calcular percentis é através da função `quantile()`. Vamos utilizar o dataset integrado `mtcars`, que contém dados de desempenho de diversos modelos de automóveis, focando na variável `wt` (peso).

Para calcular um percentil específico, passamos um vetor de probabilidades como segundo argumento da função.

```r
# Carregando o dataset para o ambiente de trabalho
Data_Cars <- mtcars

# Calculando o percentil 75 (0.75) do peso (wt)
quantile(Data_Cars$wt, c(0.75))
```

**Explicação:** O parâmetro `c(0.75)` instrui o R a localizar o valor exato que separa os 75% inferiores dos 25% superiores dos dados. O resultado retornado (3.61) representa 3.610 lbs, confirmando que a maioria dos veículos no dataset está abaixo desse patamar de peso.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_stat_percentile)

---

### Visão Geral da Distribuição

Se você omitir o parâmetro de probabilidades, a função `quantile()` fornecerá, por padrão, as estatísticas de resumo de cinco números (0%, 25%, 50%, 75% e 100%).

```r
# Resumo completo dos percentis
quantile(Data_Cars$wt)
```

**Explicação:** Este comando é uma ferramenta rápida de diagnóstico. Ele exibe o valor mínimo (0%), o primeiro quartil (25%), a mediana (50%), o terceiro quartil (75%) e o valor máximo (100%). É a maneira mais rápida de entender a "amplitude" e o "centro" da sua distribuição de dados.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_stat_percentile2)

---

## Quartis

Os **quartis** são um caso especial de percentis onde os dados são divididos em quatro partes iguais, após ordenados de forma crescente:

1.  **Primeiro Quartil (Q1):** O valor que separa os primeiros 25% dos dados.
2.  **Segundo Quartil (Q2):** O valor que separa os primeiros 50% dos dados (a **Mediana**).
3.  **Terceiro Quartil (Q3):** O valor que separa os primeiros 75% dos dados.
4.  **Quarto Quartil:** O valor que representa 100% dos dados (o **Máximo**).

**Observação:** Em análises de negócio, o intervalo entre o primeiro e o terceiro quartil é chamado de *Intervalo Interquartil* (IQR), uma medida de dispersão muito utilizada por ser robusta contra valores extremos (*outliers*).

**Nota:** Lembre-se que a função `quantile()` é o seu principal recurso no R para segmentar dados dessa forma, sendo a base para a criação de *boxplots* e análises de variabilidade.

<br>

---

<p align="center">
  <a href="45_Mode.md">⬅️ Anterior</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---