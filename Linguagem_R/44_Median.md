## Mediana (Median)

A **mediana** é uma medida de tendência central fundamental em estatística e análise de dados. Diferente da média aritmética, que pode ser fortemente influenciada por valores extremos (outliers), a mediana representa o "ponto de equilíbrio" posicional de um conjunto de dados.

Em termos práticos, a mediana é o valor que divide uma amostra exatamente ao meio: 50% dos dados são menores ou iguais a ela e 50% são maiores ou iguais. Para encontrá-la manualmente, é necessário primeiro **ordenar** todos os valores em ordem crescente.

### Por que a Mediana importa?
No desenvolvimento de aplicações de análise de dados com R, utilizamos a mediana para entender a distribuição real de uma variável sem que valores muito altos ou muito baixos distorçam a percepção da amostra. Por exemplo, ao analisar salários em uma empresa, a mediana é muito mais representativa do que a média, pois não é "puxada" pelos salários milionários dos executivos.

Se tivermos um número par de observações, a regra é simples: somamos os dois valores centrais e dividimos por dois. 

**Observação:** Quando o conjunto de dados é grande (milhares de observações), realizar essa ordenação e busca manualmente seria proibitivo. O R automatiza esse processo computacionalmente através da função `median()`.

### Calculando a Mediana no R

A função `median()` é o método padrão para extrair essa informação de um vetor ou de uma coluna em um *data frame*. 

Observe o exemplo abaixo utilizando o conjunto de dados clássico `mtcars`, que contém especificações de diversos modelos de carros:

```r
# Importando o conjunto de dados para uma variável
Data_Cars <- mtcars

# Calculando a mediana da coluna wt (peso do carro)
median(Data_Cars$wt)
```

**Resultado esperado:**
```text
[1] 3.325
```

O valor retornado, `3.325`, indica que a metade dos carros presentes na base de dados `mtcars` possui um peso (em milhares de libras) inferior a este valor, enquanto a outra metade possui um peso superior.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_stat_median)

**Nota:** A função `median()` ignora automaticamente valores ausentes (`NA`) se você adicionar o argumento `na.rm = TRUE` (ex: `median(Data_Cars$wt, na.rm = TRUE)`). Isso é uma prática recomendada em cenários de produção onde seus dados podem conter lacunas.

<br>

---

<p align="center">
  <a href="43_Mean_Median_Mode.md">⬅️ Anterior</a> | <a href="45_Mode.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---