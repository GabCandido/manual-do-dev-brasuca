## Recursividade em R

A **recursividade** é um conceito fundamental na ciência da computação e na matemática. Em R, dizemos que uma função é recursiva quando ela possui a capacidade de **chamar a si mesma** durante sua execução.

### Por que utilizar a recursividade?

O propósito central da recursividade é simplificar problemas complexos, dividindo-os em subproblemas menores e mais fáceis de resolver. Em vez de utilizar estruturas de repetição tradicionais (como `for` ou `while`), a recursividade permite "navegar" por dados ou realizar cálculos iterativos de uma forma matematicamente elegante.

**Nota:** Embora poderosa, a recursividade exige cautela. Se a condição de parada (o caso base) não for bem definida, o programa entrará em um loop infinito, resultando em erro de execução ou esgotamento dos recursos de memória do seu sistema.

### Exemplo Prático: `tri_recursion()`

Abaixo, apresentamos uma função que calcula a soma de uma sequência numérica de forma recursiva. A cada chamada, a variável `k` é decrementada até atingir o limite definido.

```r
tri_recursion <- function(k) {
  if (k > 0) {
    result <- k + tri_recursion(k - 1)
    print(result)
  } else {
    result <- 0
    return(result)
  }
}

tri_recursion(6)
```

**Análise do código:**
1. **Condição Base:** O bloco `else` (onde `k <= 0`) é o que interrompe o ciclo recursivo. Sem ele, a função chamaria a si mesma infinitamente.
2. **O Passo Recursivo:** A linha `result <- k + tri_recursion(k - 1)` é o "coração" do processo. Aqui, a função pausa sua execução atual para resolver a instância menor (`k - 1`) antes de prosseguir com o cálculo da soma.
3. **Resultado:** O comando `print(result)` exibirá os valores acumulados à medida que a pilha de chamadas é resolvida (o processo de "desenrolar" a recursão).

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_function_recursion)

### Insights de Desenvolvimento

* **Eficiência:** A recursividade é excelente para algoritmos de busca em estruturas de dados complexas (como árvores ou grafos) e problemas de divisão e conquista.
* **Custo Computacional:** Lembre-se que cada chamada recursiva adiciona uma nova camada à **pilha de chamadas (call stack)**. Se estiver trabalhando com volumes massivos de dados, considere se uma abordagem iterativa (loops tradicionais) não seria mais performática para economizar memória RAM.
* **Legibilidade:** Em cenários de manipulação de lógica matemática pura, o código recursivo tende a ser muito mais curto e compreensível do que a sua versão iterativa equivalente.

<br>

---

<p align="center">
  <a href="25_Nested_Functions.md">⬅️ Anterior</a> | <a href="27_Global_Variables.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---