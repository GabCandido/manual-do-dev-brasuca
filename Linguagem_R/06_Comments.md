## Comentários em R

Os **comentários** são elementos fundamentais em qualquer linguagem de programação. No R, eles servem como notas de rodapé integradas ao seu código-fonte, permitindo que você explique a lógica por trás de funções complexas, documente variáveis ou deixe instruções para outros desenvolvedores.

O interpretador do R ignora qualquer texto que venha após o caractere `#`. Isso significa que os comentários não impactam a performance ou a execução do seu script; eles existem puramente para o benefício do programador e da manutenibilidade do projeto a longo prazo.

### Utilizando Comentários

Você pode inserir comentários de duas formas principais: iniciando uma linha inteira ou adicionando-os ao final de uma linha de código.

#### Comentário em linha isolada
Esta prática é recomendada para descrever blocos de lógica ou seções do seu script.

```r
# Este é um comentário que explica a próxima linha
"Hello World!"
```

#### Comentário ao final da linha
Ideal para explicar comandos curtos que podem ser ambíguos.

```r
"Hello World!" # Este é um comentário após o código
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_comments)

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_comments2)

---

### Por que usar comentários?

Além da documentação, os comentários são uma ferramenta poderosa para o **debug** (depuração). Ao colocar um `#` antes de uma linha de código, você "desativa" essa instrução sem precisar deletá-la. Isso é extremamente útil ao testar diferentes abordagens para resolver o mesmo problema.

**Exemplo de depuração:**
Neste caso, o R executará apenas a última linha, ignorando a mensagem de bom dia.

```r
# "Good morning!"
"Good night!"
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_comments3)

---

### Comentários de Múltiplas Linhas

Diferente de linguagens como Java ou C++, o R não possui um delimitador específico para blocos de comentários (como `/* ... */`). Para criar comentários que ocupam várias linhas, a sintaxe padrão exige que você insira o caractere `#` no início de cada linha.

```r
# Este é um comentário
# escrito em
# mais de uma linha
"Hello World!"
```

[🚀 Pratique este código](https://www.w3schools.com/r/tryr.asp?filename=demo_comments4)

**Nota:** Embora pareça trabalhoso, essa estrutura é consistente com a filosofia do R de manter o código limpo e legível. Em editores de código modernos (como o RStudio), você pode comentar blocos inteiros rapidamente utilizando o atalho `Ctrl + Shift + C` (ou `Cmd + Shift + C` no macOS).

<br>

---

<p align="center">
  <a href="05_Print.md">⬅️ Anterior</a> | <a href="07_Variables.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---