## R - Operadores Lógicos AND e OR

No desenvolvimento de algoritmos, frequentemente precisamos que o computador tome decisões baseadas em múltiplas condições simultâneas. Para isso, utilizamos os **operadores lógicos**. Eles permitem conectar expressões condicionais para criar filtros complexos e fluxos de controle precisos.

### AND (&)
O símbolo **&** é um operador lógico de "E" (AND). Ele é utilizado para combinar duas ou mais condições onde **todas** devem ser verdadeiras para que o resultado final da expressão seja `TRUE`. Se qualquer uma das partes for falsa, o bloco de código não será executado.

Imagine um sistema de validação de crédito onde você precisa verificar se um cliente tem idade suficiente **e** um score de crédito acima de um determinado valor.

```r
a <- 200
b <- 33
c <- 500

if (a > b & c > a) {
  print("Ambas as condições são verdadeiras")
}
```

**Explicação:** O interpretador avalia `a > b` (200 > 33 é `TRUE`) e `c > a` (500 > 200 é `TRUE`). Como ambos os lados retornam `TRUE`, o bloco `if` é disparado.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_if_and)

---

### OR (|)
O símbolo **|** é o operador lógico de "OU" (OR). Diferente do AND, este operador verifica se **pelo menos uma** das condições declaradas é verdadeira. Se qualquer um dos lados da expressão for `TRUE`, o bloco de código será executado.

Este operador é fundamental em cenários onde você aceita diferentes caminhos para um mesmo resultado, como permitir o acesso a um sistema se o usuário for um "Administrador" **ou** tiver a "Permissão Especial".

```r
a <- 200
b <- 33
c <- 500

if (a > b | a > c) {
  print("Pelo menos uma das condições é verdadeira")
}
```

**Explicação:** O R testa se `a > b` (200 > 33) é `TRUE` ou se `a > c` (200 > 500) é `FALSE`. Como o primeiro teste resultou em `TRUE`, a condição do `if` é satisfeita, ignorando o resultado do segundo teste.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_if_or)

**Nota:** Em R, é importante não confundir o operador lógico simples (`&` ou `|`) com os operadores de vetorização dupla (`&&` ou `||`). Os operadores de símbolo único que aprendemos aqui são utilizados para comparar vetores, enquanto os duplos são geralmente reservados para controle de fluxo único dentro de instruções `if`.

<br>

---

<p align="center">
  <a href="19_Nested_If.md">⬅️ Anterior</a> | <a href="21_While_Loop.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---