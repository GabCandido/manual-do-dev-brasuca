## Sintaxe no R

A sintaxe de uma linguagem de programação é o conjunto de regras que define a estrutura de comandos e expressões que o computador consegue interpretar. No **R**, uma linguagem focada primordialmente em computação estatística e análise de dados, a clareza sintática é fundamental para a manipulação eficiente de vetores, matrizes e data frames.

Entender como o R interpreta diferentes tipos de dados é o seu primeiro passo para automatizar análises complexas.

---

### Saída de Texto (Strings)

Para exibir texto no R, utilizamos aspas. Elas sinalizam ao interpretador que o conteúdo ali contido deve ser tratado como um **caractere** (ou *string*), e não como uma variável ou comando do sistema. Você pode usar aspas simples (`'`) ou duplas (`"`).

```r
"Hello World!"
```

**Explicação:** O código acima envia uma string literal para o console. O R reconhece as aspas como delimitadores de texto, garantindo que o conteúdo seja impresso exatamente como escrito.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_syntax_str)

---

### Saída de Números

Ao contrário dos textos, os números não exigem aspas. Quando você insere um valor numérico bruto, o R o identifica como um tipo de dado **numérico** (*numeric*), permitindo que ele seja utilizado imediatamente em operações matemáticas.

```r
5
10
25
```

**Explicação:** O R processa cada linha individualmente, exibindo os valores numéricos no console. Em cenários reais, isso é comum ao carregar constantes ou resultados de medições que serão utilizados em cálculos subsequentes.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_syntax_num)

---

### Cálculos Matemáticos

O R foi desenhado para ser uma "calculadora avançada". A sintaxe para operações aritméticas segue a lógica algébrica convencional. A capacidade de realizar cálculos diretamente no console permite que desenvolvedores e cientistas de dados validem hipóteses rapidamente.

```r
5 + 5
```

**Explicação:** O interpretador avalia a expressão matemática e retorna o resultado da soma. Este é o alicerce para o processamento de grandes conjuntos de dados, onde operações aritméticas são aplicadas a colunas inteiras de uma só vez (vetorização).

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_syntax_add)

---

**Nota:** O R é *case-sensitive*, o que significa que letras maiúsculas e minúsculas são interpretadas como diferentes. Sempre verifique a grafia dos seus comandos.

**Observação:** Você acabou de executar seus primeiros comandos. A partir daqui, a lógica de programação no R evolui para o armazenamento desses valores em variáveis, permitindo que os dados sejam manipulados, transformados e visualizados com muito mais poder.

<br>

---

<p align="center">
  <a href="03_Get_Started.md">⬅️ Anterior</a> | <a href="05_Print.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---