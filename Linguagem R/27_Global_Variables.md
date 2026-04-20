## Variáveis Globais em R

Em R, o **escopo** de uma variável define onde ela pode ser acessada dentro do seu código. Variáveis criadas fora de qualquer função são chamadas de **variáveis globais**.

O conceito de escopo é fundamental para a organização de projetos de ciência de dados. Variáveis globais são visíveis em todo o seu script, o que permite que funções acessem dados carregados globalmente (como um *dataset* principal) sem a necessidade de passar esses dados como argumentos repetidamente.

### Utilizando Variáveis Globais

Como as variáveis globais estão no nível mais alto do seu ambiente, elas podem ser lidas de qualquer lugar, incluindo o interior de funções.

```r
txt <- "awesome"

my_function <- function() {
  paste("R is", txt)
}

my_function()
```

**Explicação:** Aqui, a variável `txt` foi definida no escopo global. Quando `my_function()` é chamada, o R busca o valor de `txt` no seu ambiente local; ao não encontrar, ele "sobe" na hierarquia e o encontra no escopo global.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_variables_global)

---

### Escopo Local vs. Global

Se você criar uma variável com o mesmo nome dentro de uma função, o R criará uma **variável local**. Esta variável "esconde" a variável global apenas durante a execução daquela função específica. A variável global original permanece intacta fora da função.

```r
txt <- "global variable"

my_function <- function() {
  txt <- "fantastic"
  paste("R is", txt)
}

my_function()
txt # O valor permanece "global variable"
```

**Nota:** A variável `txt` definida dentro da função existe apenas enquanto a função está sendo processada. Após o término da execução, o R descarta o valor local, preservando o valor original da variável global.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_variables_global2)

---

## O Operador de Atribuição Global

Embora o comportamento padrão proteja as variáveis globais de alterações acidentais, existem momentos em que você *precisa* modificar o valor de uma variável global a partir de uma função. Para isso, utilizamos o **operador de atribuição global** `<<-`.

### Criando ou Alterando Variáveis no Escopo Global

O operador `<<-` força o R a procurar a variável no escopo global. Se ela existir, ele altera o valor original. Se não existir, ele a cria no escopo global.

```r
my_function <- function() {
  txt <<- "fantastic"
  paste("R is", txt)
}

my_function()
print(txt)
```

**Observação:** O uso frequente de atribuições globais (`<<-`) deve ser feito com cautela. Em grandes sistemas ou fluxos de análise complexos, isso pode gerar efeitos colaterais difíceis de rastrear, tornando o código mais propenso a erros.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_variables_global3)

### Atualizando uma Variável Existente

Você também pode usar o operador para atualizar uma variável global que já possuía um valor diferente:

```r
txt <- "awesome"

my_function <- function() {
  txt <<- "fantastic"
  paste("R is", txt)
}

my_function()
paste("R is", txt)
```

**Explicação:** O `<<-` garante que a alteração dentro da função reflita no ambiente global, sobrescrevendo o valor "awesome" pelo valor "fantastic".

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_variables_global4)

<br>

---

<p align="center">
  <a href="26_Recursion.md">⬅️ Anterior</a> | <a href="28_Data_Structures.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---