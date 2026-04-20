## Caracteres de Escape em R

Em programação, quando definimos uma **string** (sequência de caracteres delimitada por aspas), o interpretador espera que o conteúdo termine exatamente onde a próxima aspa aparece. No entanto, existem cenários onde precisamos incluir caracteres especiais dentro desse texto — como aspas dentro de uma frase ou quebras de linha.

Para lidar com esses "caracteres ilegais", utilizamos **caracteres de escape**. Um caractere de escape é composto por uma **barra invertida** (`\`) seguida pelo caractere que você deseja inserir literalmente no texto.

### O Problema: Conflito de Sintaxe

Se você tentar inserir aspas duplas dentro de uma string que já está delimitada por aspas duplas, o R interpretará a aspa interna como o fim da sua string, gerando um erro de sintaxe.

```r
str <- "We are the so-called "Vikings", from the north."
str
```

**Resultado esperado:**
O R retornará um erro, pois ele entende que a string termina em `"Vikings"`, deixando o restante do código (`from the north."`) sem contexto sintático.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_strings_esc)

---

### A Solução: Escapando o Caractere

Para informar ao R que as aspas internas são parte do conteúdo do texto e não o delimitador da string, usamos a sequência `\"`.

```r
str <- "We are the so-called \"Vikings\", from the north."

str
cat(str)
```

**Nota:** Ao imprimir a variável `str` diretamente, você verá as barras invertidas no console. Isso ocorre porque o R exibe a representação interna do objeto. Para visualizar o texto formatado como ele apareceria em uma interface de usuário ou arquivo de texto, utilizamos a função `cat()`.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_strings_esc2)

---

### Tabela de Referência: Caracteres de Escape

Além das aspas, outros caracteres especiais são fundamentais para formatar saídas de dados ou manipular caminhos de arquivos:

| Código | Descrição |
| :--- | :--- |
| `\\` | Insere uma barra invertida literal |
| `\n` | Nova linha (Line Break) |
| `\r` | Retorno de carro (Carriage Return) |
| `\t` | Tabulação (Tab) |
| `\b` | Retrocesso (Backspace) |

**Observação:** O uso de caracteres de escape é uma técnica universal em quase todas as linguagens de programação (C, Python, Java, etc.). Dominar esses símbolos é essencial para a limpeza e preparação de dados (data munging), especialmente ao lidar com arquivos `.csv` ou logs que contenham caracteres especiais em campos de texto.

<br>

---

<p align="center">
  <a href="14_Strings.md">⬅️ Anterior</a> | <a href="16_Booleans.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---