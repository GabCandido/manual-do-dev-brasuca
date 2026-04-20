## Data Frames

Os **Data Frames** são a estrutura de dados mais fundamental para a análise de dados no R. Eles representam informações organizadas em um formato de tabela (linhas e colunas), funcionando de maneira muito similar a uma planilha do Excel ou uma tabela de banco de dados SQL.

A grande flexibilidade dos Data Frames reside na sua capacidade de armazenar tipos de dados heterogêneos. Embora cada coluna deva conter um único tipo de dado (como `character`, `numeric` ou `logical`), o Data Frame como um todo pode combinar essas diferentes colunas.

Para criar um Data Frame, utilizamos a função `data.frame()`.

```r
# Criando um Data Frame
Data_Frame <- data.frame (
  Training = c("Strength", "Stamina", "Other"),
  Pulse = c(100, 150, 120),
  Duration = c(60, 30, 45)
)

# Exibindo o Data Frame
Data_Frame
```

Ao executar o código acima, o R imprimirá no console uma representação visual organizada, onde as colunas são alinhadas verticalmente, facilitando a visualização de observações relacionadas.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_data_frames)

---

## Resumo Estatístico

Para obter uma visão rápida sobre a distribuição dos dados, utilizamos a função `summary()`. Esta ferramenta é essencial em Ciência de Dados, pois fornece automaticamente métricas como mínimo, máximo, média e quartis para colunas numéricas, além de contagens de frequência para colunas categóricas.

```r
Data_Frame <- data.frame (
  Training = c("Strength", "Stamina", "Other"),
  Pulse = c(100, 150, 120),
  Duration = c(60, 30, 45)
)

summary(Data_Frame)
```

**Nota:** Você aprenderá mais sobre as aplicações avançadas da função `summary()` e estatística descritiva nos próximos módulos deste curso.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_data_frames_summary)

---

## Acessando Itens

Como o Data Frame é bidimensional, existem três formas principais de extrair dados. O uso de `$` é a convenção mais utilizada em fluxos de trabalho modernos, pois permite acessar colunas pelo nome diretamente.

```r
# Usando colchetes simples para filtrar por índice de coluna
Data_Frame[1]

# Usando colchetes duplos (retorna o conteúdo da coluna)
Data_Frame[["Training"]]

# Usando o cifrão (forma mais comum e legível)
Data_Frame$Training
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_data_frames_access)

---

## Adicionando Linhas e Colunas

Data Frames são estruturas dinâmicas. Você pode expandir seu conjunto de dados facilmente usando as funções de ligação (`bind`):

*   **`rbind()`** (Row Bind): Adiciona novas linhas ao final da tabela.
*   **`cbind()`** (Column Bind): Adiciona novas colunas à direita da tabela.

```r
# Adicionando uma nova linha
New_row_DF <- rbind(Data_Frame, c("Strength", 110, 110))

# Adicionando uma nova coluna
New_col_DF <- cbind(Data_Frame, Steps = c(1000, 6000, 2000))
```

[🚀 Pratique o uso de rbind](https://www.w3schools.com/r/tryr.asp?filename=demo_data_frames_add_rows)
[🚀 Pratique o uso de cbind](https://www.w3schools.com/r/tryr.asp?filename=demo_data_frames_add_cols)

---

## Removendo Dados

Para remover linhas ou colunas, utilizamos a indexação negativa com a função `c()`. O sinal de menos `-` diz ao R: "exclua esta posição específica".

```r
# Remove a primeira linha e a primeira coluna
Data_Frame_New <- Data_Frame[-c(1), -c(1)]
```

**Observação:** Lembre-se que o R utiliza indexação começando em 1, não em 0.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_data_frames_remove)

---

## Dimensões e Tamanho

Para entender a estrutura do seu conjunto de dados, o R oferece comandos para verificar a "forma" do Data Frame:

*   **`dim()`**: Retorna um vetor com o número de linhas e colunas.
*   **`nrow()`** e **`ncol()`**: Retornam, respectivamente, o número de linhas e o número de colunas.
*   **`length()`**: Em um Data Frame, retorna o número de colunas.

```r
dim(Data_Frame)    # Retorna: Linhas Colunas
ncol(Data_Frame)   # Número de colunas
nrow(Data_Frame)   # Número de linhas
length(Data_Frame) # Equivalente a ncol()
```

[🚀 Pratique dim()](https://www.w3schools.com/r/tryr.asp?filename=demo_data_frames_dim)
[🚀 Pratique ncol() e nrow()](https://www.w3schools.com/r/tryr.asp?filename=demo_data_frames_ncol_nrow)
[🚀 Pratique length()](https://www.w3schools.com/r/tryr.asp?filename=demo_data_frames_length)

---

## Combinando Data Frames

Em cenários reais, frequentemente precisamos unir bases de dados. 

*   **Verticalmente (`rbind`)**: Usado quando você tem novos dados que seguem o mesmo esquema (mesmas colunas) da tabela original.
*   **Horizontalmente (`cbind`)**: Usado para adicionar novas variáveis ou atributos às observações existentes.

```r
# Empilhando Data Frames verticalmente
New_Data_Frame <- rbind(Data_Frame1, Data_Frame2)

# Unindo lateralmente (adicionando novas variáveis)
New_Data_Frame1 <- cbind(Data_Frame3, Data_Frame4)
```

[🚀 Pratique a união vertical](https://www.w3schools.com/r/tryr.asp?filename=demo_data_frames_combine)
[🚀 Pratique a união horizontal](https://www.w3schools.com/r/tryr.asp?filename=demo_data_frames_combine2)

<br>

---

<p align="center">
  <a href="32_Arrays.md">⬅️ Anterior</a> | <a href="34_Factors.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---