## Funções em R

Uma **função** é um bloco de código estruturado que executa uma tarefa específica apenas quando é invocado (chamado). No desenvolvimento de software, funções são os pilares da reutilização: em vez de repetir o mesmo bloco de código várias vezes ao longo de um script, você o encapsula em uma função, tornando seu programa mais legível, fácil de manter e livre de redundâncias.

Além de executar blocos de lógica, as funções podem receber dados de entrada — conhecidos como **parâmetros** — e retornar resultados processados, permitindo uma comunicação dinâmica entre diferentes partes do seu sistema.

---

## Criando uma Função

Para definir uma função em R, utilizamos a palavra-chave reservada `function()`. A sintaxe exige que você atribua a definição da função a um nome de variável, que será usado para invocá-la posteriormente.

```r
my_function <- function() { 
  # O código dentro das chaves {} é o corpo da função
  print("Hello World!")
}
```

**Nota:** O código acima cria a função, mas não a executa imediatamente. Ele apenas armazena a instrução na memória do R.

---

## Chamando uma Função

Para executar (ou "chamar") uma função, basta digitar o seu nome seguido por parênteses `()`. Se a função exigir dados, estes serão inseridos dentro desses parênteses.

```r
my_function <- function() {
  print("Hello World!")
}

# Invocação da função
my_function() 
```

**Resultado esperado:** Ao rodar este comando, o console exibirá a mensagem `"Hello World!"`.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_function)

---

## Argumentos

As funções tornam-se poderosas quando processam dados externos. Chamamos essas informações de **argumentos**. Eles são especificados entre os parênteses da definição da função. Você pode incluir quantos argumentos desejar, desde que os separe por vírgulas.

```r
my_function <- function(fname) {
  paste(fname, "Griffin")
}

my_function("Peter")
my_function("Lois")
my_function("Stewie")
```

**Observação:** Note a distinção técnica importante:
*   **Parâmetro:** É a variável listada na definição da função (ex: `fname`).
*   **Argumento:** É o valor real que você passa para a função ao chamá-la (ex: `"Peter"`).

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_function_args)

---

## Número de Argumentos

Em R, por padrão, a função espera receber exatamente o número de argumentos definido. Se a sua função foi criada para receber dois argumentos, ela falhará caso você passe apenas um ou exceda o limite.

```r
my_function <- function(fname, lname) {
  paste(fname, lname)
}

my_function("Peter", "Griffin")
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_function_args2)

**Atenção:** Tentar rodar `my_function("Peter")` resultará em um erro, pois o interpretador R não encontrará o segundo argumento esperado (`lname`).

[🚀 Pratique este código (Erro de argumento)](https://www.w3schools.com/r/tryr.asp?filename=demo_function_args3)

---

## Valores Padrão (Default Parameter Value)

Você pode definir um valor padrão para um parâmetro caso o usuário não forneça um argumento. Isso é extremamente útil para criar comportamentos "fallback" em bibliotecas e APIs.

```r
my_function <- function(country = "Norway") {
  paste("I am from", country)
}

my_function("Sweden")
my_function("India")
my_function() # Usará o valor padrão: "Norway"
my_function("USA")
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_function_default)

---

## Valores de Retorno

Para que uma função devolva um resultado para o escopo global ou para outra função, utilizamos a função `return()`. Sem ela, a função apenas executará a lógica interna, mas não disponibilizará o resultado do cálculo para uso posterior.

```r
my_function <- function(x) {
  return (5 * x)
}

print(my_function(3))
print(my_function(5))
print(my_function(9))
```

**Resultado esperado:**
```text
[1] 15
[1] 25
[1] 45
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_function_return)

<br>

---

<p align="center">
  <a href="23_Nested_Loop.md">⬅️ Anterior</a> | <a href="25_Nested_Functions.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---