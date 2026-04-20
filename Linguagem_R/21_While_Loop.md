## Loops

Na programação, **loops** (laços de repetição) são estruturas fundamentais que permitem executar um bloco de código repetidamente, desde que uma condição específica seja atendida. O uso de loops é uma das melhores práticas para economizar tempo, reduzir a redundância de código e minimizar erros manuais, tornando seus scripts muito mais legíveis e fáceis de manter.

Em R, existem dois comandos principais para controlar o fluxo de repetição:
* `while` loops
* `for` loops

---

## R While Loops

O **while loop** (laço "enquanto") é utilizado para repetir uma série de instruções enquanto uma condição lógica for avaliada como `TRUE`. 

O segredo aqui é o estado da variável de controle. O loop continuará rodando infinitamente até que a condição seja `FALSE`.

### Exemplo Prático
Vamos imprimir o valor de `i` enquanto ele for menor que 6:

```r
i <- 1
while (i < 6) {
  print(i)
  i <- i + 1
}
```

**Explicação:**
Neste código, definimos uma variável de indexação `i` inicializada como 1. A cada iteração, o R verifica se `i < 6`. Se for verdadeiro, ele imprime o número e incrementa `i` em 1. Quando `i` atinge 6, a condição `6 < 6` torna-se `FALSE`, e o loop encerra automaticamente.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_while_loop)

**Nota:** É vital garantir que o loop tenha uma condição de saída. Sempre lembre-se de incrementar ou modificar a variável que controla a condição dentro do bloco de código; caso contrário, você criará um **loop infinito**, que travará a execução do seu programa.

---

## Break

Às vezes, queremos interromper um loop prematuramente, mesmo que a condição principal ainda seja `TRUE`. Para isso, utilizamos o comando `break`.

### Exemplo Prático
Vamos forçar o encerramento do loop assim que `i` atingir 4:

```r
i <- 1
while (i < 6) {
  print(i)
  i <- i + 1
  if (i == 4) {
    break
  }
}
```

**Resultado esperado:** O loop imprimirá os números 1, 2 e 3. Quando o incremento atinge 4, o comando `break` interrompe a execução, ignorando o restante das iterações restantes.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_while_loop_break)

---

## Next

O comando `next` permite um controle mais refinado: ele pula a iteração atual e salta diretamente para a próxima rodada do loop, sem encerrá-lo completamente.

### Exemplo Prático
Vamos pular a impressão do número 3:

```r
i <- 0
while (i < 6) {
  i <- i + 1
  if (i == 3) {
    next
  }
  print(i)
}
```

**Resultado esperado:** O programa imprimirá 1, 2, 4, 5 e 6. O valor 3 é simplesmente ignorado devido ao comando `next`.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_while_loop_next)

---

## Estudo de Caso: Yahtzee!

Para visualizar o poder do `while` combinado com estruturas condicionais (`if...else`), imagine a lógica de um jogo de dados como o Yahtzee.

### Exemplo Prático
Vamos percorrer os números de 1 a 6 e identificar quando atingimos o resultado máximo:

```r
dice <- 1
while (dice <= 6) {
  if (dice < 6) {
    print("No Yahtzee")
  } else {
    print("Yahtzee!")
  }
  dice <- dice + 1
}
```

**Explicação:** Este padrão é muito comum em automações de processos em R, onde verificamos o status de uma variável de estado (`dice`) e alteramos a saída do programa com base em um critério de sucesso (neste caso, o valor 6).

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_while_loop_yahtzee)

<br>

---

<p align="center">
  <a href="20_And_Or.md">⬅️ Anterior</a> | <a href="22_For_Loop.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---