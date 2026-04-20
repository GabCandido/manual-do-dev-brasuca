## Nomes de Variáveis (Identificadores) em R

Em R, uma **variável** atua como um contêiner nomeado para armazenar dados. A escolha de nomes (também chamados de **identificadores**) é uma parte crucial da legibilidade do código. Embora você possa usar nomes curtos como `x` ou `y`, a adoção de nomes descritivos (como `taxa_de_juros` ou `volume_total`) torna o seu script significativamente mais fácil de manter e auditar por outros desenvolvedores.

### Regras de Sintaxe
Para que o interpretador do R aceite um nome de variável, ele deve seguir um conjunto de diretrizes estritas. O não cumprimento dessas regras resultará em erros de sintaxe (`syntax error`).

1. **Estrutura:** Um nome deve começar com uma letra (A-Z ou a-z). Após o primeiro caractere, ele pode conter letras, dígitos (0-9), pontos (`.`) ou sublinhados (`_`).
2. **Início com ponto:** Se o nome começar com um ponto (`.`), o caractere seguinte **não pode** ser um número.
3. **Restrições de início:** Nomes não podem começar com números ou sublinhados (`_`).
4. **Case-sensitivity:** R diferencia maiúsculas de minúsculas. Portanto, `Idade`, `idade` e `IDADE` são tratados como três variáveis distintas.
5. **Palavras Reservadas:** Você não pode utilizar palavras que fazem parte da sintaxe da linguagem (como `TRUE`, `FALSE`, `NULL`, `if`, `else`, etc.).

### Exemplos Práticos

Abaixo, demonstramos como definir variáveis seguindo as convenções da linguagem e quais formatos resultam em falhas.

```r
# Nomes permitidos (Legal):
myvar <- "John"
my_var <- "John"
myVar <- "John"
MYVAR <- "John"
myvar2 <- "John"
.myvar <- "John"

# Nomes inválidos (Illegal):
2myvar <- "John"    # Começa com número
my-var <- "John"    # Usa hífen (interpretado como subtração)
my var <- "John"    # Contém espaço
_my_var <- "John"   # Começa com underscore
my_v@ar <- "John"   # Contém caractere especial inválido
TRUE <- "John"      # Palavra reservada
```

**Resultado esperado:** Ao executar os exemplos "Legal", o R armazena a string "John" nos identificadores especificados. Ao tentar executar os exemplos "Illegal", o console retornará um erro, impedindo a atribuição do valor.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_variables_name)

---

**Nota:** Lembre-se sempre que a sensibilidade a maiúsculas (**case-sensitivity**) é uma das fontes mais comuns de bugs em R. Sempre que encontrar um erro do tipo *object not found*, verifique se não houve uma inconsistência na capitalização do nome da variável.

**Observação:** O uso do ponto (`.`) em nomes de variáveis é comum em R (estilo `meu.objeto`), diferentemente de muitas outras linguagens de programação onde o ponto é reservado exclusivamente para acessar métodos ou propriedades de objetos (como em Python ou JS). Embora permitido, o uso do `snake_case` (sublinhado) é frequentemente preferido por legibilidade.

<br>

---

<p align="center">
  <a href="09_Multiple_Variables.md">⬅️ Anterior</a> | <a href="11_Data_Types.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---