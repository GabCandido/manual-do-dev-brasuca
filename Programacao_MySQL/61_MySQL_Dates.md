## Trabalhando com Datas no MySQL

O gerenciamento de dados temporais é um dos pilares fundamentais em sistemas de banco de dados relacionais. A precisão em consultas que envolvem tempo é o que separa um relatório financeiro exato de um erro de conformidade. No MySQL, o desafio central não reside apenas na sintaxe, mas na **consistência de formatos**: o valor que você insere ou consulta deve respeitar rigorosamente a estrutura definida na coluna do seu banco de dados.

---

## Tipos de Dados de Data

O MySQL oferece tipos específicos para armazenamento de informações temporais. A escolha correta entre eles define a performance da sua indexação e a facilidade com que você poderá realizar cálculos de datas posteriormente.

*   **`DATE`**: Armazena apenas a data, no formato `YYYY-MM-DD`. Ideal para aniversários ou datas de eventos onde a hora é irrelevante.
*   **`DATETIME`**: Armazena data e hora, no formato `YYYY-MM-DD HH:MI:SS`. É o padrão para registros de eventos que exigem precisão absoluta.
*   **`TIMESTAMP`**: Similar ao `DATETIME` em formato, mas armazena valores como o número de segundos desde a "Epoch" (1970-01-01). É sensível ao fuso horário (Timezone).
*   **`TIME`**: Armazena apenas o tempo, no formato `HH:MI:SS`.
*   **`YEAR`**: Armazena apenas o ano, aceitando formatos `YYYY` ou `YY`.

**Observação:** O tipo de dado de uma coluna é definido no momento da criação da tabela. Alterar o tipo posteriormente pode ser uma operação onerosa em tabelas com milhões de registros.

---

## Manipulando Datas em Consultas

Para compreender como o banco de dados enxerga essas informações, observe a tabela `Orders` abaixo:

| OrderId | ProductName | OrderDate |
| :--- | :--- | :--- |
| 1 | Geitost | 2025-11-11 |
| 2 | Camembert Pierrot | 2025-11-09 |
| 3 | Mozzarella di Giovanni | 2025-11-11 |
| 4 | Mascarpone Fabioli | 2025-10-29 |

Se o seu objetivo é recuperar todos os pedidos realizados em "2025-11-11", você utilizará a cláusula `WHERE` para filtrar o conteúdo da coluna `OrderDate`:

```sql
SELECT * FROM Orders WHERE OrderDate='2025-11-11';
```

**Resultado:** O MySQL retornará os registros de ID 1 e 3. Como a coluna não possui componente de tempo, a comparação é direta e exata.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trysql.asp?filename=trysql_select_where_date)

---

## O Desafio da Precisão: O Componente de Tempo

Em sistemas reais, colunas do tipo `DATETIME` costumam incluir horas, minutos e segundos. Considere a mesma tabela, mas agora com registros mais detalhados:

| OrderId | ProductName | OrderDate |
| :--- | :--- | :--- |
| 1 | Geitost | 2025-11-11 13:23:44 |
| 2 | Camembert Pierrot | 2025-11-09 15:45:21 |
| 3 | Mozzarella di Giovanni | 2025-11-11 11:12:01 |
| 4 | Mascarpone Fabioli | 2025-10-29 14:56:59 |

Se você tentar executar a mesma consulta anterior:

```sql
SELECT * FROM Orders WHERE OrderDate='2025-11-11';
```

**Resultado:** O resultado será um conjunto vazio. Isso ocorre porque o MySQL busca uma equivalência exata. O valor `2025-11-11` é interpretado pelo banco como `2025-11-11 00:00:00`. Como não há registros exatamente à meia-noite, a consulta falha.

**Nota:** Para comparar datas que possuem componentes de tempo, você deve utilizar funções de extração (como `DATE()`) ou operadores de intervalo (como `BETWEEN`), garantindo que a comparação seja feita no nível de precisão desejado.

**Dica de Arquiteto:** Para manter suas queries simples e fáceis de manter, evite incluir o componente de tempo em colunas onde apenas a data é necessária. O excesso de precisão não utilizado gera ruído na lógica de negócio e dificulta a indexação eficiente.

<br>

---

<p align="center">
  <a href="60_MySQL_Auto_Increment.md">⬅️ Anterior</a> | <a href="62_MySQL_Views.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---