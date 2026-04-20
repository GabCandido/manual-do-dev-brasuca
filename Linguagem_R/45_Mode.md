## Moda (Mode)

Em estatística, a **Moda** é definida como o valor que ocorre com a maior frequência em um conjunto de dados. Diferente da média ou da mediana, que buscam o "centro" matemático ou posicional, a moda identifica o "padrão de recorrência" ou o comportamento mais típico dentro de uma distribuição.

No **R**, é importante notar que não existe uma função nativa única (como `mode()`) dedicada ao cálculo estatístico da moda. O R possui uma função chamada `mode()`, mas ela serve para identificar o *tipo de armazenamento* de um objeto, não para cálculos estatísticos. Por isso, precisamos combinar funções de contagem para atingir nosso objetivo.

### Por que calcular a moda?

Em análise de dados e ciência de mercado, a moda é crucial para identificar **tendências predominantes**. Imagine que você está analisando o peso de veículos (`wt` no dataset `mtcars`). Saber qual o peso mais comum não diz apenas o valor central, mas sim o valor que define a maior parte da sua amostra.

### Implementando a Moda no R

Para encontrar a moda, utilizamos uma combinação estratégica de três funções fundamentais:
1. `table()`: Cria uma tabela de frequências (conta quantas vezes cada valor aparece).
2. `sort()`: Ordena essas frequências.
3. `names()`: Extrai o rótulo do valor que obteve a maior contagem.

Observe o exemplo abaixo aplicando isso ao dataset `mtcars`:

```R
# Criamos uma tabela de frequências de 'wt' e a ordenamos de forma decrescente
# O sinal de negativo (-) inverte a ordem para que o valor mais frequente fique no topo
Data_Cars <- mtcars
resultado <- names(sort(-table(Data_Cars$wt)))[1]

# Exibindo o resultado
print(resultado)
```

**Explicação técnica:**
*   A função `table(Data_Cars$wt)` agrupa os dados e conta as repetições.
*   O prefixo `-` aplicado a `table` é um "truque" de conveniência: ao ordenar, o R coloca os valores numéricos em ordem crescente. Como queremos o valor mais frequente, invertemos a lógica para que o maior número (a contagem mais alta) apareça primeiro na ordenação.
*   `[1]` seleciona o primeiro elemento do vetor resultante, que é justamente a nossa moda.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_stat_mode)

**Nota:** No conjunto de dados `mtcars`, o valor **3.44** (ou 3.440 lbs) aparece com maior frequência, confirmando que este é o peso predominante entre a amostra de veículos analisada.

---

### Observação sobre Tipagem
Tenha cuidado ao utilizar a técnica acima. Como o resultado de `names()` retorna um *string* (caractere), se você precisar realizar cálculos matemáticos com esse valor posteriormente, lembre-se de convertê-lo novamente para numérico usando a função `as.numeric()`.

<br>

---

<p align="center">
  <a href="44_Median.md">⬅️ Anterior</a> | <a href="46_Percentiles.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---