## Estruturas Condicionais Aninhadas (Nested If)

No desenvolvimento de software, frequentemente nos deparamos com cenários onde uma decisão lógica depende de outra. Quando colocamos uma estrutura condicional `if` dentro de outro bloco `if` ou `else`, chamamos isso de **Nested If** (ou *if* aninhado).

O propósito dessa técnica é permitir um controle de fluxo mais granular. Enquanto um `if` simples avalia uma condição booleana básica, o *nested if* permite que você "funile" a lógica, verificando condições secundárias apenas se a condição primária for atendida.

### Sintaxe e Exemplo Prático

A lógica de aninhamento exige atenção à indentação. Embora o interpretador do **R** não exija espaços para que o código funcione, manter uma hierarquia visual clara é essencial para a manutenibilidade do seu projeto e para evitar erros de leitura humana.

```r
x <- 41

if (x > 10) {
  print("Above ten")
  
  if (x > 20) {
    print("and also above 20!")
  } else {
    print("but not above 20.")
  }
  
} else {
  print("below 10.")
}
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_if_nested)

**Análise do Código:**

1.  Primeiro, avaliamos se `x` é maior que 10.
2.  Se a condição for verdadeira, entramos no primeiro bloco. Dentro dele, realizamos um novo teste: `x > 20`.
3.  Se `x` for 41, o console exibirá ambos os resultados: "Above ten" e "and also above 20!".
4.  Caso `x` fosse 15, o código imprimiria "Above ten" e "but not above 20.".
5.  Se `x` fosse 5, o primeiro `if` falharia e o programa saltaria diretamente para o `else` final, exibindo "below 10.".

**Observação:** O uso excessivo de *nested ifs* pode tornar o código difícil de seguir, uma técnica conhecida no mercado como "código espaguete". Sempre que possível, avalie se operadores lógicos (como `&&` ou `||`) podem simplificar a sua estrutura antes de recorrer ao aninhamento.

<br>

---

<p align="center">
  <a href="18_If...Else.md">⬅️ Anterior</a> | <a href="20_And_Or.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---