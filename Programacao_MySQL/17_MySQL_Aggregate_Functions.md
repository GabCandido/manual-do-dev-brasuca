## Funções de Agregação no MySQL

No mundo dos bancos de dados relacionais, frequentemente não estamos interessados apenas em extrair linhas individuais, mas em obter **insights** sobre o conjunto de dados como um todo. É aqui que entram as **Funções de Agregação** (*Aggregate Functions*).

Uma função de agregação é um método que processa um conjunto de valores e retorna um **único valor** resultante. Pense nelas como ferramentas estatísticas que resumem grandes volumes de dados em informações úteis para a tomada de decisão.

### O Poder da Agregação com GROUP BY

Embora possam ser usadas isoladamente, essas funções atingem seu potencial máximo quando combinadas com a cláusula **`GROUP BY`**. Enquanto o `SELECT` convencional traz colunas, o `GROUP BY` segmenta o conjunto de resultados em subgrupos, permitindo que a função de agregação calcule um resumo específico para cada um desses grupos (por exemplo: calcular a média salarial *por departamento* ou o total de vendas *por categoria*).

As funções mais essenciais do MySQL são:

*   **`MIN()`**: Retorna o menor valor de uma coluna especificada.
*   **`MAX()`**: Retorna o maior valor de uma coluna especificada.
*   **`COUNT()`**: Retorna a contagem total de linhas em um conjunto.
*   **`SUM()`**: Retorna a soma total de valores em uma coluna numérica.
*   **`AVG()`**: Retorna a média aritmética de uma coluna numérica.

---

### Observações Técnicas Importantes

**Nota:** Por definição, as funções de agregação **ignoram valores `NULL`** durante o processamento. Isso é fundamental para manter a precisão estatística (por exemplo, uma média não é distorcida por campos vazios). A única exceção notável é a função `COUNT(*)`, que contabiliza todas as linhas, independentemente de valores nulos, sendo usada tipicamente para contar o volume total de registros em uma tabela.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_func_count)

---

### Aplicação em Cenários Reais

No mercado, o uso de funções de agregação é onipresente. Sistemas de **Business Intelligence (BI)** e dashboards financeiros dependem dessas funções para gerar métricas de desempenho em tempo real. Por exemplo:
*   Um e-commerce utiliza `SUM()` para calcular o faturamento diário.
*   Um sistema acadêmico utiliza `AVG()` para determinar a média geral de uma turma.
*   Uma plataforma de rede social utiliza `COUNT()` para exibir o número de seguidores ou curtidas em uma publicação.

Dominar estas funções é o primeiro passo para transformar dados brutos em inteligência de negócio.

<br>

---

<p align="center">
  <a href="16_MySQL_LIMIT.md">⬅️ Anterior</a> | <a href="18_MySQL_MIN().md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---