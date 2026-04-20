## Média, Mediana e Moda

Na análise estatística de dados, frequentemente buscamos sintetizar conjuntos de informações complexas em valores representativos que nos ajudem a entender a tendência central de uma amostra. Os três conceitos fundamentais que dominam essa análise são:

*   **Mean (Média):** O valor médio aritmético de um conjunto de dados.
*   **Median (Mediana):** O valor que divide o conjunto de dados exatamente ao meio.
*   **Mode (Moda):** O valor que aparece com maior frequência no conjunto.

---

## Mean (Média)

A **Média** é a medida de tendência central mais utilizada. Matematicamente, para calculá-la, somamos todos os valores de uma variável e dividimos o resultado pelo número total de observações. Em termos de desenvolvimento de software e ciência de dados, essa operação é essencial para obter uma "visão geral" de um comportamento, como o peso médio de veículos ou a média de vendas diárias.

Para ilustrar, utilizaremos o conjunto de dados `mtcars`, um dataset clássico em R que contém informações sobre diversos modelos de carros. Abaixo, observamos os pesos (`wt`) ordenados:

| 1.513 | 1.615 | 1.835 | 1.935 | 2.140 | 2.200 | 2.320 | 2.465 |
|---|---|---|---|---|---|---|---|
| 2.620 | 2.770 | 2.780 | 2.875 | 3.150 | 3.170 | 3.190 | 3.215 |
| 3.435 | 3.440 | 3.440 | 3.440 | 3.460 | 3.520 | 3.570 | 3.570 |
| 3.730 | 3.780 | 3.840 | 3.845 | 4.070 | 5.250 | 5.345 | 5.424 |

Em R, não precisamos realizar o cálculo manual (soma e divisão). A linguagem oferece a função nativa `mean()`, que abstrai toda essa lógica matemática para uma única chamada de função, garantindo eficiência e legibilidade no seu código.

### Exemplo: Calculando a Média

Para encontrar o peso médio (`wt`) dos carros contidos no dataset, utilizamos a seguinte estrutura:

```r
# Atribuímos o dataset mtcars a uma variável chamada Data_Cars
Data_Cars <- mtcars

# Calculamos a média da coluna wt (weight) usando o operador $ para acessar a coluna
mean(Data_Cars$wt)
```

**Resultado esperado:**
```text
[1] 3.21725
```

**Nota:** O operador `$` no R é utilizado para acessar colunas específicas dentro de um *data frame*. Ao passar `Data_Cars$wt` para a função `mean()`, estamos instruindo o R a extrair apenas o vetor de pesos para realizar o cálculo estatístico.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_stat_mean)

<br>

---

<p align="center">
  <a href="42_Max_and_Min.md">⬅️ Anterior</a> | <a href="44_Median.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---