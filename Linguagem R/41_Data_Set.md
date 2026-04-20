## Conjuntos de Dados (Data Sets) em R

Um **conjunto de dados** (*data set*) é, na sua essência, uma coleção organizada de informações, geralmente estruturada em formato tabular. No ecossistema de ciência de dados com R, a manipulação eficiente desses dados é o pilar fundamental para qualquer análise estatística ou projeto de aprendizado de máquina.

Para iniciarmos nossos estudos, utilizaremos o conjunto de dados nativo **`mtcars`** (*Motor Trend Car Road Tests*). Este conjunto contém dados extraídos da revista americana *Motor Trend* de 1974 e é amplamente utilizado em ambientes acadêmicos e de treinamento devido à sua clareza e estrutura balanceada.

### O Comando mtcars
Para visualizar o conteúdo completo de um *data set* carregado na memória, basta digitar o nome da variável que o representa no console:

```r
# Exibir o conjunto de dados mtcars
mtcars
```

Ao executar este comando, o R retornará uma matriz de dados contendo 32 observações (linhas) e 11 variáveis (colunas), cobrindo aspectos como consumo de combustível (mpg), cilindradas (cyl), potência (hp), entre outros.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_stat_ds_print)

---

### Explorando Metadados com o Operador de Ajuda
Nem sempre saberemos o significado das colunas de um conjunto de dados complexo. No R, utilizamos o caractere especial **`?`** antes do nome do objeto para acessar a documentação técnica oficial:

```r
# Acessar a documentação do conjunto de dados
?mtcars
```

**Nota:** A documentação exibida fornece o contexto histórico, a origem dos dados e uma descrição detalhada de cada variável, o que é crucial para evitar interpretações estatísticas equivocadas.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_stat_ds_view)

---

### Investigando a Estrutura (Dimensões e Nomes)
Antes de realizar operações complexas, é uma boa prática de arquitetura de software verificar a forma dos dados com os comandos `dim()` e `names()`:

```r
# Atribuindo a uma variável para melhor organização
Data_Cars <- mtcars 

# dim() retorna o número de linhas e colunas
dim(Data_Cars)

# names() lista os rótulos de cada variável (coluna)
names(Data_Cars)
```

**Observação:** O comando `dim()` retorna um vetor onde o primeiro elemento é o número de observações (linhas) e o segundo é o número de variáveis (colunas).

Se precisar identificar as observações específicas (neste caso, os modelos de carro), utilize a função `rownames()`:

```r
# Listando os nomes das linhas (os modelos de carros)
rownames(Data_Cars)
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_stat_ds_dim_names)
[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_stat_ds_rownames)

---

### Manipulação e Acesso a Variáveis
Para acessar uma coluna específica dentro de um *data frame*, utilizamos o operador **`$`** (sifrão), que vincula o nome do conjunto de dados ao nome da variável desejada.

```r
# Acessando apenas a coluna 'cyl' (cilindros)
Data_Cars$cyl

# Ordenando os valores da variável de forma crescente
sort(Data_Cars$cyl)
```

O comando `sort()` é essencial quando queremos identificar a distribuição de frequências ou outliers em uma série de dados numérica.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_stat_ds_varval)
[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_stat_ds_sort)

---

### Análise Estatística Preliminar
Para obter uma visão panorâmica e rápida dos dados, utilizamos a função `summary()`. Ela é, provavelmente, o comando mais útil para uma exploração inicial (*Exploratory Data Analysis* - EDA).

```r
# Gerando um resumo estatístico completo
summary(Data_Cars)
```

A função `summary()` retorna seis métricas estatísticas vitais para cada variável numérica:
1. **Min**: O valor mínimo observado.
2. **1st Quartile**: O ponto que divide os 25% iniciais dos dados.
3. **Median**: O valor central da distribuição (50º percentil).
4. **Mean**: A média aritmética.
5. **3rd Quartile**: O ponto que divide os 75% iniciais dos dados.
6. **Max**: O valor máximo observado.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_stat_ds_summary)

<br>

---

<p align="center">
  <a href="40_Statistics_Intro.md">⬅️ Anterior</a> | <a href="42_Max_and_Min.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---