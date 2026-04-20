## R: Nested Loops (Loops Aninhados)

Em programação, frequentemente precisamos realizar tarefas repetitivas que dependem de outras repetições. Quando colocamos um loop dentro de outro, chamamos essa estrutura de **Nested Loop** (ou loop aninhado).

O propósito central dessa técnica é permitir a iteração sobre estruturas de dados multidimensionais ou a realização de combinações exaustivas de conjuntos de elementos. Em cenários de mercado e análise de dados, isso é fundamental para percorrer matrizes, cruzar informações de múltiplas listas ou realizar simulações que exigem múltiplas variáveis de controle.

### Como funciona na prática

Imagine que o loop externo é o "ritmo" principal e o loop interno é a "ação" executada para cada passo do ritmo. O loop interno será executado completamente a cada única iteração do loop externo.

```r
# Definindo as listas de trabalho
adj <- list("red", "big", "tasty")
fruits <- list("apple", "banana", "cherry")

# Loop externo: itera sobre cada adjetivo
for (x in adj) {
  # Loop interno: itera sobre cada fruta para o adjetivo atual
  for (y in fruits) {
    print(paste(x, y))
  }
}
```

**Explicação do código:**
1. O primeiro loop (`for (x in adj)`) seleciona "red".
2. O segundo loop (`for (y in fruits)`) assume o comando e imprime "red apple", "red banana" e "red cherry".
3. Uma vez que o loop de frutas termina, o controle volta ao loop de adjetivos, que agora seleciona "big".
4. O processo se repete até que todos os adjetivos sejam combinados com todas as frutas.

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_for_loop_nested)

**Nota:** O uso excessivo de loops aninhados (especialmente com grandes conjuntos de dados) pode impactar a performance do seu código. Em R, sempre que possível, considere utilizar funções da família `apply` ou operações vetorizadas, que são otimizadas para processar dados de forma mais eficiente do que loops explícitos.

**Observação:** Lembre-se que cada nível de aninhamento adiciona uma camada de complexidade à sua lógica. Certifique-se de manter o código legível e, se o nível de profundidade for muito alto, considere modularizar a lógica do loop interno em uma função separada.

<br>

---

<p align="center">
  <a href="22_For_Loop.md">⬅️ Anterior</a> | <a href="24_Functions.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---