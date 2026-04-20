## Matemática em R

No ecossistema R, o processamento numérico é uma das suas competências fundamentais. Diferente de linguagens de propósito geral, o R foi desenhado desde o seu núcleo para estatística e análise de dados, o que torna a manipulação matemática uma tarefa nativa e altamente performática.

### Operações Matemáticas Simples

A forma mais básica de interagir com dados numéricos é através dos **operadores** aritméticos. Eles são os pilares que permitem realizar cálculos rápidos e transformações em conjuntos de dados.

```r
# Adição
10 + 5

# Subtração
10 - 5
```

Ao executar estes comandos, o R avalia a expressão e retorna o resultado imediatamente no console. Em cenários reais de análise, você raramente usará números "hardcoded" (fixos), aplicando esses operadores sobre **vetores** ou colunas de data frames para realizar cálculos em massa de forma eficiente.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_math_oper1)
[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_math_oper2)

**Observação:** Para um domínio completo de como manipular dados, recomendo explorar a seção de [Operadores em R](https://www.w3schools.com/r/r_operators.asp).

---

## Funções Matemáticas Embutidas

Além dos operadores, o R oferece uma vasta biblioteca de **funções built-in** (nativas). Estas funções encapsulam lógicas complexas, permitindo que você execute tarefas estatísticas sofisticadas com uma sintaxe simples e legível.

Por exemplo, para identificar os limites de um conjunto de valores, utilizamos as funções `min()` e `max()`:

```r
# Encontra o maior valor
max(5, 10, 15)

# Encontra o menor valor
min(5, 10, 15)
```

**Nota:** Essas funções são a base para o pré-processamento de dados, permitindo a limpeza de outliers ou a normalização de variáveis antes de alimentar modelos de aprendizado de máquina.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_math_max_min)

---

## Cálculo de Raiz Quadrada: `sqrt()`

A função `sqrt()` é utilizada para calcular a raiz quadrada de um valor numérico. É uma ferramenta essencial em cálculos de variância e desvio padrão.

```r
sqrt(16)
```

O resultado esperado desta operação é `4`. Se você tentar aplicar esta função a um número negativo, o R retornará `NaN` (*Not a Number*), pois a raiz quadrada de números negativos não é real.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_math_sqrt)

---

## Valor Absoluto: `abs()`

Muitas vezes, em análise de dados, o que importa é a magnitude da diferença, e não a direção (positiva ou negativa). A função `abs()` retorna o **valor absoluto** de um número, garantindo que o resultado seja sempre não-negativo.

```r
abs(-4.7)
```

O R transformará `-4.7` em `4.7`. Este é um procedimento comum para calcular o erro absoluto em modelos preditivos.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_math_abs)

---

## Arredondamento: `ceiling()` e `floor()`

Em manipulação de dados, a precisão numérica nem sempre é desejável. Frequentemente precisamos "limitar" o valor a um número inteiro. As funções `ceiling()` e `floor()` servem para este controle direcional:

*   **`ceiling()`**: Arredonda para cima (para o próximo inteiro maior ou igual).
*   **`floor()`**: Arredonda para baixo (para o próximo inteiro menor ou igual).

```r
# Arredonda para o maior inteiro (2)
ceiling(1.4)

# Arredonda para o menor inteiro (1)
floor(1.4)
```

Estas funções são vitais em engenharia de atributos, por exemplo, quando você precisa categorizar idades ou transformar variáveis contínuas em intervalos discretos.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_math_ceiling_floor)

<br>

---

<p align="center">
  <a href="12_Numbers.md">⬅️ Anterior</a> | <a href="14_Strings.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---