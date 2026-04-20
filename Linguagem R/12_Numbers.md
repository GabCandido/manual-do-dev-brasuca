## Números em R

Em R, a forma como manipulamos dados numéricos é fundamental para qualquer análise estatística ou processo de ciência de dados. Diferente de linguagens de propósito geral onde a tipagem pode ser flexível, o R categoriza números de maneira específica para otimizar o processamento matemático e o uso de memória.

Existem três tipos principais de números em R:

*   **`numeric`**: O tipo padrão para números reais.
*   **`integer`**: Números inteiros (sem casas decimais).
*   **`complex`**: Números com uma parte imaginária.

Variáveis do tipo numérico são instanciadas automaticamente no momento em que você realiza uma atribuição (`<-`):

```r
x <- 10.5   # numeric
y <- 10L    # integer
z <- 1i     # complex
```

## Numeric

O tipo **`numeric`** é o cavalo de batalha do R. Ele é utilizado sempre que você precisa representar números decimais ou inteiros sem restrições de formato. Em R, qualquer número que contenha um ponto decimal ou seja declarado sem um sufixo especial é tratado como `numeric` por padrão.

```r
x <- 10.5
y <- 55

# Exibindo os valores
x
y

# Verificando o tipo da variável com a função class()
class(x)
class(y)
```

**Resultado esperado:** Ao executar `class(x)` e `class(y)`, o console retornará `"numeric"`, confirmando que, para o R, números inteiros sem declaração específica são tratados como decimais de ponto flutuante.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_numbers_numeric)

## Integer

**`integer`** são números inteiros estritos, ou seja, sem casas decimais. No desenvolvimento de software e análise de dados, utilizamos `integer` quando temos a certeza de que a variável nunca precisará de precisão decimal, o que pode otimizar a performance em grandes conjuntos de dados. Para forçar um número a ser um `integer`, utilizamos o sufixo **`L`** após o valor.

```r
x <- 1000L
y <- 55L

# Exibindo valores
x
y

# Verificando a classe
class(x)
class(y)
```

**Nota:** Sem o sufixo `L`, o R trataria o número 1000 como `numeric` (1000.0). O sufixo é uma instrução ao interpretador para alocar o tipo de dado específico.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_numbers_integer)

## Complex

Números **`complex`** são essenciais em áreas como engenharia, física e computação gráfica. Eles são representados pela combinação de uma parte real e uma parte imaginária, marcada pela letra **`i`**.

```r
x <- 3+5i
y <- 5i

# Exibindo valores
x
y

# Verificando a classe
class(x)
class(y)
```

**Observação:** O R gerencia automaticamente a aritmética complexa, permitindo que cálculos envolvendo esses números sejam realizados de forma transparente, assim como faríamos com números decimais comuns.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_numbers_complex)

## Conversão de Tipo (Type Casting)

Frequentemente, ao importar dados de fontes externas (como CSVs ou bancos de dados), os números podem não vir no formato que seu algoritmo exige. O R fornece funções de coerção para transformar esses tipos:

*   `as.numeric()`: Converte para decimal.
*   `as.integer()`: Converte para inteiro (truncando casas decimais).
*   `as.complex()`: Converte para formato complexo.

```r
x <- 1L # integer
y <- 2  # numeric

# Convertendo de integer para numeric
a <- as.numeric(x)

# Convertendo de numeric para integer
b <- as.integer(y)

# Verificando as novas classes
class(a)
class(b)
```

**Por que converter?** Em produção, garantir que um dado seja do tipo correto é uma etapa vital da **limpeza de dados** (data cleaning). Tentar realizar operações matemáticas em tipos incompatíveis ou realizar cálculos de alta precisão com inteiros pode gerar erros ou perda de informação.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_numbers_convert)

<br>

---

<p align="center">
  <a href="11_Data_Types.md">⬅️ Anterior</a> | <a href="13_Math.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---