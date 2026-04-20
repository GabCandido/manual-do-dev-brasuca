## Variáveis em R

As **variáveis** são os blocos de construção fundamentais de qualquer linguagem de programação. Elas funcionam como contêineres lógicos na memória do computador, permitindo que você armazene, nomeie e manipule dados ao longo da execução do seu script ou análise de dados.

Diferente de linguagens como C ou Java, o R não exige que você "declare" um tipo de variável (como `int` ou `string`) antes de usá-la. O R é uma linguagem de tipagem dinâmica: a variável é criada no exato momento em que você atribui um valor a ela.

### Criando Variáveis

Para atribuir um valor a uma variável em R, utilizamos o operador de atribuição `<-`. Este símbolo visual representa uma "seta" apontando da direita para a esquerda, indicando que o valor está sendo inserido dentro do contêiner.

```r
name <- "John"
age  <- 40

name   # Exibe o valor de name
age    # Exibe o valor de age
```

No exemplo acima, `name` e `age` são as **variáveis** (os nomes que escolhemos), enquanto `"John"` e `40` são os **valores** armazenados. 

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_variables)

**Nota:** Embora muitas linguagens utilizem o sinal de `=` para atribuição, no R o operador `<-` é o padrão preferencial da comunidade e dos desenvolvedores. Embora o `=` funcione na maioria dos casos, ele pode ser proibido ou gerar comportamentos inesperados em contextos específicos de escopo. Use `<-` para garantir consistência e segurança.

---

### Exibindo Variáveis (Output)

Em R, a forma mais rápida de visualizar o conteúdo de uma variável é simplesmente digitar o nome dela no console.

```r
name <- "John Doe"

name # O R faz o "auto-print" do valor
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_variables_print)

Embora o *auto-print* seja conveniente para uma exploração rápida, o R oferece a função `print()` para situações onde você precisa de um controle mais explícito. Esta função é familiar para quem migra de linguagens como Python e é indispensável em fluxos de controle.

```r
name <- "John Doe"

print(name) # Exibição explícita através da função
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_variables_print2)

**Observação:** Quando você está trabalhando dentro de estruturas de controle, como loops (`for`, `while`) ou blocos de código definidos entre chaves `{}`, o comportamento de *auto-print* é frequentemente suprimido. Nesses casos, o uso da função `print()` torna-se obrigatório se você deseja que o R exiba o resultado no console.

```r
for (x in 1:10) {
  print(x) # O uso de print é necessário dentro do bloco de código
}
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_syntax_print_for)

**Resumo:** O uso do `print()` é opcional em scripts simples, mas torna-se um padrão profissional necessário quando seu código está encapsulado em expressões complexas. Utilize-o para garantir que seus resultados sejam visíveis independentemente de onde o código esteja posicionado.

<br>

---

<p align="center">
  <a href="06_Comments.md">⬅️ Anterior</a> | <a href="08_Concatenate_Elements.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---