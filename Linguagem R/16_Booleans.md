## Booleans (Valores Lógicos)

Na programação, a capacidade de tomar decisões é o que transforma um script estático em um sistema inteligente. Para que o computador saiba quando executar uma ação específica, ele precisa avaliar se uma condição é **verdadeira** ou **falsa**.

Em R, utilizamos os chamados **Booleans** (ou valores lógicos) para representar esses dois estados. Ao avaliar qualquer expressão no R, o resultado será invariavelmente `TRUE` (verdadeiro) ou `FALSE` (falso).

### Avaliando Expressões

Quando você compara dois valores utilizando operadores de comparação, o R processa a lógica matemática por trás e retorna o status lógico correspondente. 

```r
10 > 9    # TRUE, pois 10 é maior que 9
10 == 9   # FALSE, pois 10 não é igual a 9
10 < 9    # FALSE, pois 10 é maior que 9
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_booleans)

**Nota:** Observe o uso de `==`. Em R (e na maioria das linguagens), um único sinal de igual `=` é frequentemente usado para atribuição, enquanto o sinal duplo `==` é o operador relacional de **comparação de igualdade**.

### Comparação de Variáveis

A lógica booleana brilha quando aplicada a variáveis. Isso permite que você crie programas que respondam de forma dinâmica aos dados armazenados em memória.

```r
a <- 10
b <- 9

a > b     # O resultado será TRUE
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_booleans_var)

**Por que isso importa?**
No desenvolvimento de software e ciência de dados, essa funcionalidade é o alicerce para estruturas de controle de fluxo. Sem a capacidade de avaliar se `a > b`, não conseguiríamos filtrar dados, validar entradas de usuários ou criar loops de repetição.

### Controle de Fluxo: Estruturas Condicionais

Os valores booleanos são os "pilares de decisão" dentro de uma estrutura `if`. Quando o R encontra um `if`, ele verifica o valor booleano resultante da condição entre parênteses: se for `TRUE`, o código dentro do bloco é executado; se for `FALSE`, o programa salta para o `else` (se existir).

```r
a <- 200
b <- 33

if (b > a) {
  print("b é maior que a")
} else {
  print("b não é maior que a")
}
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_booleans_if)

**Observação:** O R é sensível a letras maiúsculas e minúsculas. Os valores lógicos reservados pela linguagem devem ser escritos sempre em maiúsculas: `TRUE` e `FALSE`. O uso de `True` ou `true` resultará em erro, pois o R os interpretará como nomes de variáveis e não como tipos de dados booleanos.

<br>

---

<p align="center">
  <a href="15_Escape_Characters.md">⬅️ Anterior</a> | <a href="17_Operators.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---