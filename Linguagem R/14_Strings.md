## Strings em R

As **Strings** (cadeias de caracteres) são o tipo de dado fundamental para o armazenamento e manipulação de texto. Em análise de dados e ciência de dados, elas são essenciais para processar nomes, endereços, categorias e logs que compõem datasets reais.

### Literais de String

Uma string é definida cercando o texto com aspas simples (`'`) ou aspas duplas (`"`). Em R, não há diferença funcional entre elas; você pode escolher o estilo que preferir ou que melhor se adapte ao conteúdo da sua string (por exemplo, usar aspas simples para conter uma frase com aspas duplas dentro).

```r
"hello"
'hello'
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_strings)

---

### Atribuindo Strings a Variáveis

Para armazenar uma string e reutilizá-la posteriormente, utilizamos o operador de atribuição `<-`. Este é o padrão idiomático da linguagem R para vincular um valor a um nome de objeto.

```r
str <- "Hello"
str # imprime o valor de str
```

**Nota:** O símbolo `#` é utilizado em R para comentários. Tudo o que vier após ele na mesma linha será ignorado pelo interpretador.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_strings2)

---

### Strings Multilinhas

Às vezes, precisamos manipular textos longos que ocupam várias linhas. O R permite que você insira quebras de linha diretamente dentro das aspas.

```r
str <- "Lorem ipsum dolor sit amet,
consectetur adipiscing elit,
sed do eiusmod tempor incididunt
ut labore et dolore magna aliqua."

str # imprime o valor de str
```

**Observação:** Ao imprimir este conteúdo, você notará a presença do caractere `\n`. Este é um **caractere de escape** que representa uma "nova linha" (*new line*). O R o insere automaticamente para que o interpretador saiba exatamente onde o texto deve ser quebrado.

Se o seu objetivo é que a saída no console respeite exatamente a formatação de quebra de linha que você definiu, utilize a função `cat()`:

```r
cat(str)
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_strings_multi2)

---

### Comprimento da String

Para saber quantos caracteres compõem um texto (incluindo espaços e pontuações), utilizamos a função `nchar()`. Isso é extremamente útil em cenários de limpeza de dados (*data cleaning*), onde é necessário validar se um campo de texto atende a um limite específico de tamanho.

```r
str <- "Hello World!"
nchar(str)
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_strings_nchar)

---

### Verificando a presença de texto

A função `grepl()` (de *grep logical*) é utilizada para verificar se um padrão de texto existe dentro de uma string. Ela retorna um valor lógico: `TRUE` se o padrão for encontrado, e `FALSE` caso contrário.

```r
str <- "Hello World!"

grepl("H", str)      # Verifica se 'H' está presente
grepl("Hello", str)  # Verifica se a palavra 'Hello' está presente
grepl("X", str)      # Verifica se 'X' está presente
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_strings_grepl)

---

### Concatenando Strings

Para combinar ou unir strings, utilizamos a função `paste()`. Ela permite concatenar múltiplos elementos, separando-os por espaços por padrão.

```r
str1 <- "Hello"
str2 <- "World"

paste(str1, str2)
```

**Por que usar `paste()`?** Em análise de dados, usamos essa função constantemente para criar nomes de arquivos dinâmicos (por exemplo, unindo "relatorio_" com a "data_de_hoje") ou para formatar mensagens de saída em relatórios automatizados.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_strings_paste)

<br>

---

<p align="center">
  <a href="13_Math.md">⬅️ Anterior</a> | <a href="15_Escape_Characters.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---