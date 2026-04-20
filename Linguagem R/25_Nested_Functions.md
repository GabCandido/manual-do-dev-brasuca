## Nested Functions (Funções Aninhadas)

Em R, a modularização é um dos pilares da programação eficiente. **Nested Functions** (funções aninhadas) referem-se à capacidade de organizar o fluxo lógico permitindo que uma função resida ou interaja dentro do contexto de outra. Isso é particularmente útil para encapsular comportamentos complexos que não precisam ser expostos globalmente no seu ambiente de trabalho.

Existem duas formas principais de implementar este conceito:

1.  **Chamada de função dentro de outra função:** Utilizar o retorno de uma função como argumento para outra.
2.  **Definição de função dentro de outra função:** Criar o escopo de uma função dentro do bloco de código de uma função "pai" (ou *outer function*).

---

## 1. Chamada de função dentro de outra função

Neste cenário, estamos apenas compondo chamadas. O resultado de uma função é processado imediatamente e repassado como input para outra função.

```r
# Definimos uma função simples de soma
Nested_function <- function(x, y) {
  a <- x + y
  return(a)
}

# Chamando a função dentro da própria chamada
Nested_function(Nested_function(2, 2), Nested_function(3, 3))
```

### Explicação do código
Aqui, a lógica é executada de dentro para fora. Primeiro, o interpretador do R resolve `Nested_function(2, 2)` (que resulta em 4) e `Nested_function(3, 3)` (que resulta em 6). Em seguida, a função "externa" recebe esses dois resultados e realiza a soma final: `4 + 6 = 10`.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_function_nested)

---

## 2. Escrevendo uma função dentro de outra

Esta é uma técnica avançada de **escopo lexical**. Ao definir uma função dentro de outra, a função "interna" (*Inner function*) tem acesso aos argumentos da função "externa" (*Outer function*), mas a função interna não está disponível no ambiente global do seu código.

```r
Outer_func <- function(x) {
  Inner_func <- function(y) {
    a <- x + y
    return(a)
  }
  return(Inner_func)
}

# Atribuímos a função "pai" a uma variável
output <- Outer_func(3) 

# Agora executamos a função que foi retornada
output(5)
```

### Explicação do código
Note que não podemos chamar `Inner_func` diretamente fora da `Outer_func`, pois ela é privada ao escopo da função principal. 

1. Ao chamar `Outer_func(3)`, o R cria um "ambiente" onde `x` vale 3 e retorna a definição de `Inner_func`.
2. Armazenamos esse retorno na variável `output`.
3. Quando chamamos `output(5)`, o R executa a lógica `3 + 5`, resultando em **8**.

**Nota:** Este padrão é frequentemente usado para criar "geradores de funções" ou *closures*, onde você pré-configura parte do comportamento de uma função e a finaliza em um momento posterior da execução.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_function_nested2)

<br>

---

<p align="center">
  <a href="24_Functions.md">⬅️ Anterior</a> | <a href="26_Recursion.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---