## Laços de Repetição: For Loops no R

Em programação, um **laço de repetição** (*loop*) é uma estrutura fundamental que nos permite executar um bloco de código várias vezes, automatizando tarefas repetitivas e processamento de grandes conjuntos de dados. No R, o `for` loop é especificamente projetado para iterar sobre uma sequência (como um vetor, lista ou série numérica).

Diferente de outras linguagens que utilizam um índice numérico para controlar a iteração, o `for` no R atua como um **iterador**, percorrendo cada elemento de um objeto de forma direta.

### O Básico: Iterando sobre sequências

A estrutura `for` percorre cada item contido em uma sequência definida.

```r
for (x in 1:10) {
  print(x)
}
```

**Explicação:** O código acima cria uma sequência de 1 a 10. A variável `x` assume, a cada volta do laço, o valor correspondente na sequência, e o comando `print(x)` exibe esse valor no console. Ao final do décimo ciclo, o laço é encerrado automaticamente.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_syntax_print_for)

---

### Aplicando a Listas e Vetores

A verdadeira utilidade dos `for` loops no R surge quando precisamos processar coleções de dados, como **listas** e **vetores**.

```r
fruits <- list("apple", "banana", "cherry")

for (x in fruits) {
  print(x)
}
```

**Resultado:** O R percorre a lista `fruits` e imprime individualmente cada fruta. Note que não precisamos definir o tamanho da lista previamente; o iterador se adapta automaticamente ao conteúdo do objeto.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_for_loop)

**Observação:** O R não exige que você defina uma variável de controle de índice (como ocorre em `while` ou em linguagens como C++), tornando o código mais limpo e menos propenso a erros de limite de vetor.

---

### Controle de Fluxo: Break e Next

Às vezes, precisamos interromper ou pular partes da iteração baseados em condições lógicas.

#### Interrompendo com `break`
O comando `break` finaliza o laço imediatamente, saindo da estrutura de repetição antes de completar todos os itens da sequência.

```r
fruits <- list("apple", "banana", "cherry")

for (x in fruits) {
  if (x == "cherry") {
    break
  }
  print(x)
}
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_for_loop_break)

#### Pulando uma iteração com `next`
O comando `next` força o laço a pular a iteração atual e prosseguir imediatamente para a próxima, sem interromper o fluxo total.

```r
fruits <- list("apple", "banana", "cherry")

for (x in fruits) {
  if (x == "banana") {
    next
  }
  print(x)
}
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_for_loop_next)

---

### Exemplo Prático: Lógica Condicional e Loops

Combinar estruturas de controle (`if/else`) dentro de um `for` loop é uma prática comum para análise de dados ou simulações. Abaixo, simulamos a rolagem de dados em um jogo:

```r
dice <- 1:6

for(x in dice) {
  if (x == 6) {
    print(paste("The dice number is", x, "Yahtzee!"))
  } else {
    print(paste("The dice number is", x, "Not Yahtzee"))
  }
}
```

**Explicação:** Aqui utilizamos a função `paste()` para concatenar strings com valores dinâmicos. O laço avalia cada face do dado: se o valor for 6, ele dispara uma mensagem específica; caso contrário, informa que não é o resultado esperado. Este padrão de codificação é a base para criar relatórios automatizados ou validar entradas em pipelines de Ciência de Dados.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_for_loop_yahtzee)

<br>

---

<p align="center">
  <a href="21_While_Loop.md">⬅️ Anterior</a> | <a href="23_Nested_Loop.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---