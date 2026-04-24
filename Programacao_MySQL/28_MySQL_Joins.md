## A Cláusula JOIN no MySQL

Em bancos de dados relacionais, os dados raramente residem em uma única tabela. Para manter a integridade e evitar a redundância (conforme os princípios de **Normalização**), dividimos as informações em entidades distintas. A cláusula `JOIN` é a ferramenta fundamental para reconstruir essas relações, permitindo combinar linhas de duas ou mais tabelas com base em uma coluna relacionada entre elas.

Imagine que você tem uma tabela `Orders` (Pedidos) contendo apenas IDs de clientes, e uma tabela `Customers` (Clientes) com os detalhes cadastrais. O `JOIN` é o "elo" que permite extrair um relatório unificado onde cada pedido seja exibido ao lado do nome real do cliente correspondente.

### Tipos de JOIN

Dependendo da sua necessidade de negócio — ou seja, se você quer apenas registros completos ou todos os registros de uma tabela, mesmo que não tenham correspondência na outra — utilizamos diferentes tipos de junção:

*   **`INNER JOIN`**: Retorna apenas as linhas que possuem **valores correspondentes** em ambas as tabelas. É o tipo mais comum, ideal para quando você precisa de dados "completos".
*   **`LEFT JOIN`**: Retorna **todas as linhas da tabela da esquerda** e as linhas correspondentes da tabela da direita. Se não houver correspondência, o resultado exibirá `NULL` nos campos da direita.
*   **`RIGHT JOIN`**: O inverso do anterior; retorna **todas as linhas da tabela da direita** e as correspondentes da tabela da esquerda.
*   **`CROSS JOIN`**: Produz o **produto cartesiano**, combinando cada linha da primeira tabela com cada linha da segunda. Use com cautela, pois pode gerar volumes massivos de dados.

---

### Exemplo Prático: Relacionando Pedidos e Clientes

Observe a relação entre as tabelas `Orders` e `Customers`. Ambas compartilham a coluna `CustomerID`. Esta coluna é a **Chave Estrangeira** (*Foreign Key*) que permite conectar o pedido ao seu autor.

Para listar todos os pedidos com o nome do cliente, utilizamos o `INNER JOIN`:

```sql
SELECT Orders.OrderID, Customers.CustomerName, Orders.OrderDate
FROM Orders
INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID;
```

**Análise do código:**
1.  **`SELECT`**: Definimos as colunas específicas que queremos visualizar. Note que usamos o prefixo `Tabela.Coluna` para evitar ambiguidade.
2.  **`FROM`**: Indicamos a tabela base (geralmente a tabela de fatos, neste caso, os pedidos).
3.  **`INNER JOIN`**: Realizamos a junção com a tabela de dimensões (`Customers`).
4.  **`ON`**: Definimos a regra de junção. É aqui que o banco de dados compara a `CustomerID` de um lado com a do outro para "colar" os registros que possuem a mesma identidade.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_join)

**Resultado esperado:**
O banco de dados retornará um conjunto de resultados consolidado. Onde existia apenas o número `2` na tabela de pedidos, agora teremos o nome "Ana Trujillo Emparedados y helados" extraído da tabela de clientes, facilitando a legibilidade e a análise de dados.

**Nota:** Ao trabalhar com grandes volumes de dados, certifique-se de que as colunas utilizadas na cláusula `ON` possuam **índices** definidos. Isso reduz drasticamente o tempo de processamento da consulta, pois o motor do banco de dados não precisará percorrer toda a tabela para encontrar os pares correspondentes.

<br>

---

<p align="center">
  <a href="27_MySQL_Aliases.md">⬅️ Anterior</a> | <a href="29_MySQL_INNER_JOIN.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---