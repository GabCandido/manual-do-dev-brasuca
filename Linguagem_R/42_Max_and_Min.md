## Max e Min em R

No estudo de análise de dados, identificar os limites de um conjunto é um dos primeiros passos para compreender a distribuição das informações. Em R, as funções `max()` e `min()` são ferramentas fundamentais para extrair os valores extremos de um vetor ou coluna de um *data frame*.

Continuaremos utilizando o conjunto de dados **mtcars**, um *dataset* clássico em R que contém especificações de diversos modelos de automóveis da década de 70.

### Encontrando valores extremos

Para obter o valor mais alto e o mais baixo de uma variável específica (como a potência, representada pela coluna `hp`), utilizamos as funções integradas da linguagem:

```R
# Carregando o conjunto de dados para a variável local
Data_Cars <- mtcars

# Identificando o maior valor de hp
max(Data_Cars$hp)

# Identificando o menor valor de hp
min(Data_Cars$hp)
```

**Resultado esperado:**
O terminal retornará os valores `335` e `52`, respectivamente.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_stat_max_min)

---

### Localizando registros com funções de índice

Embora saibamos que 335 é o valor máximo e 52 o mínimo, frequentemente precisamos saber a *quem* esses valores pertencem. Em vez de percorrer uma tabela visualmente, usamos funções de busca por índice: `which.max()` e `which.min()`.

Estas funções não retornam o valor em si, mas a **posição numérica** (o índice) da linha onde o valor extremo foi encontrado.

```R
# Retorna o número da linha (índice) do maior e menor hp
which.max(Data_Cars$hp)
which.min(Data_Cars$hp)
```

**Resultado esperado:**
O R retornará `31` e `19`. Isso indica que, no *data frame* original, o valor máximo reside na linha 31 e o mínimo na linha 19.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_stat_max_min2)

---

### Mapeando nomes aos valores

Para tornar o dado legível, podemos combinar o índice retornado com a função `rownames()`. Isso permite que o R extraia o nome do veículo correspondente àquela posição específica dentro do conjunto de dados.

```R
# Extraindo o nome da linha baseada no índice do valor máximo/mínimo
rownames(Data_Cars)[which.max(Data_Cars$hp)]
rownames(Data_Cars)[which.min(Data_Cars$hp)]
```

**Resultado esperado:**
```text
[1] "Maserati Bora"
[1] "Honda Civic"
```

**Nota:** Ao aninhar as funções `rownames(Data_Cars)[...]`, estamos utilizando o índice retornado por `which.max()` como um seletor de vetor. Em R, isso é uma prática comum para filtrar metadados baseados em critérios estatísticos.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_stat_max_min3)

---

### Identificação de Outliers

Além de descrever o conjunto, as funções `max()` e `min()` são vitais para a detecção de **outliers**. Um outlier (ou valor atípico) é uma observação que se desvia drasticamente do padrão esperado dos demais dados.

A verificação dos valores extremos é a primeira linha de defesa na **limpeza de dados** (*data cleaning*). Exemplos de potenciais erros ou anomalias que poderiam ser detectados via `max` e `min`:

*   **Valores impossíveis:** Se o número máximo de marchas de um carro fosse 11 (tecnicamente improvável para o conjunto).
*   **Dados ausentes ou nulos:** Se a potência mínima encontrada fosse 0 (sugerindo um registro corrompido ou entrada faltando).
*   **Erros de escala:** Se o peso máximo de um carro fosse registrado como 50.000 lbs (provável erro de unidade de medida).

**Observação:** A detecção de outliers não significa que o dado deva ser deletado imediatamente, mas que ele merece investigação, pois pode representar um erro de medição ou uma descoberta extraordinária que exige atenção especial.

<br>

---

<p align="center">
  <a href="41_Data_Set.md">⬅️ Anterior</a> | <a href="43_Mean_Median_Mode.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---