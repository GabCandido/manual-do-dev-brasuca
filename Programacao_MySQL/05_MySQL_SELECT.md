## O Comando MySQL SELECT

O comando **SELECT** é a espinha dorsal de qualquer interação com bancos de dados relacionais. Em termos práticos, ele é a ferramenta que utilizamos para extrair informações específicas armazenadas em tabelas. Sempre que você consulta um perfil de usuário, busca um produto em um e-commerce ou gera um relatório de vendas, você está, essencialmente, executando um `SELECT`.

Quando o banco de dados processa esse comando, ele retorna os dados organizados em uma estrutura tabular temporária, chamada de **result-set** (conjunto de resultados).

### Sintaxe Básica

Para realizar uma consulta, você deve indicar quais campos (colunas) deseja visualizar e a origem (tabela) onde esses dados residem.

```sql
SELECT coluna1, coluna2, ...
FROM nome_da_tabela;
```

*   `coluna1`, `coluna2`: representam os nomes das colunas que você deseja recuperar.
*   `nome_da_tabela`: o local onde os dados estão armazenados.

**Nota:** O SQL (Structured Query Language) não diferencia maiúsculas de minúsculas nos comandos, mas é uma convenção de mercado utilizar letras maiúsculas para as palavras-chave (como `SELECT` e `FROM`) para melhorar a legibilidade do código.

### Exemplo Prático

Imagine que no banco de dados "Northwind" temos a tabela `Customers`. Se quisermos extrair apenas o nome do cliente, a cidade e o país, o comando seria:

```sql
SELECT CustomerName, City, Country 
FROM Customers;
```

Após a execução, o MySQL retornará uma tabela contendo apenas as três colunas solicitadas para todos os registros encontrados na tabela `Customers`.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_columns)

---

### Selecionando Todas as Colunas

Frequentemente, durante o desenvolvimento ou depuração, precisamos visualizar a estrutura completa de uma tabela. Em vez de listar manualmente cada nome de coluna, utilizamos o operador curinga `*` (asterisco).

```sql
SELECT * FROM Customers;
```

**Observação:** Embora o `SELECT *` seja extremamente útil para exploração de dados, evite utilizá-lo em aplicações de produção (sistemas finais). Ao especificar apenas as colunas necessárias, você reduz o tráfego de rede e o consumo de memória, tornando sua aplicação mais performática e segura.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_all)

---

### Exemplo de Base de Dados (Northwind)

Para ilustrar o comportamento do `SELECT`, utilizaremos a tabela `Customers`. Abaixo, veja uma amostra de como os dados são organizados internamente:

| CustomerID | CustomerName | ContactName | City | Country |
| :--- | :--- | :--- | :--- | :--- |
| 1 | Alfreds Futterkiste | Maria Anders | Berlin | Germany |
| 2 | Ana Trujillo Emparedados | Ana Trujillo | México D.F. | Mexico |
| 3 | Antonio Moreno Taquería | Antonio Moreno | México D.F. | Mexico |
| 4 | Around the Horn | Thomas Hardy | London | UK |
| 5 | Berglunds snabbköp | Christina Berglund | Luleå | Sweden |

Ao executar um `SELECT *` nesta tabela, o banco de dados retornará todas as linhas apresentadas acima com suas respectivas colunas. Se você restringir as colunas (ex: `SELECT CustomerName, City`), o banco filtrará apenas as informações essenciais para a sua necessidade atual.

<br>

---

<p align="center">
  <a href="04_MySQL_SQL.md">⬅️ Anterior</a> | <a href="06_MySQL_SELECT_DISTINCT.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---