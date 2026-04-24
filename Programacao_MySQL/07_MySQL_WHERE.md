## A Cláusula WHERE no MySQL

Em bancos de dados relacionais, o gerenciamento de grandes volumes de informações exige a capacidade de extrair apenas o que é relevante. A cláusula **WHERE** é a ferramenta fundamental para essa tarefa: ela atua como um filtro lógico que determina quais registros serão processados em uma operação.

Sempre que você precisar restringir um conjunto de dados para análise ou manipulação, o `WHERE` será seu aliado. Ele não se limita apenas a consultas (`SELECT`), sendo essencial também para garantir a segurança em operações de `UPDATE` e `DELETE`, evitando alterações em toda a tabela quando o objetivo é atingir apenas uma linha específica.

---

### Sintaxe Básica

A estrutura de uma consulta com filtro segue uma ordem lógica que o motor do banco de dados interpreta para localizar os dados:

```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

**Nota:** O `WHERE` é um componente versátil. Ele é utilizado sempre que a intenção é aplicar um critério seletivo sobre os dados existentes na tabela.

---

### Filtragem Prática: O "Porquê" das Aspas

Uma das maiores fontes de erro para desenvolvedores iniciantes é a formatação de valores no filtro. O MySQL exige que valores do tipo **texto** (como strings ou datas) estejam entre aspas simples (`' '`), enquanto valores **numéricos** devem ser escritos diretamente.

Isso ocorre porque o banco precisa distinguir entre nomes de colunas/palavras-chave e o conteúdo literal que você está buscando.

#### Exemplo com Texto
Para selecionar todos os clientes localizados no México:

```sql
SELECT * FROM Customers
WHERE Country = 'Mexico';
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_where)

#### Exemplo com Números
Ao filtrar por um campo numérico (como um ID), as aspas não são necessárias:

```sql
SELECT * FROM Customers
WHERE CustomerID = 1;
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_where_number)

---

### Operadores de Comparação

O uso do sinal de igual (`=`) é apenas o início. O poder do `WHERE` reside na sua capacidade de lidar com condições complexas usando operadores lógicos e de comparação.

Para buscar, por exemplo, todos os clientes com um ID superior a 80:

```sql
SELECT * FROM Customers
WHERE CustomerID > 80;
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_where_gt)

#### Tabela de Referência de Operadores

| Operador | Descrição | Exemplo |
| :--- | :--- | :--- |
| `=` | Igual a | [Pratique](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_op_equal_to) |
| `>` | Maior que | [Pratique](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_op_greater_than) |
| `<` | Menor que | [Pratique](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_op_less_than) |
| `>=` | Maior ou igual a | [Pratique](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_op_greater_than2) |
| `<=` | Menor ou igual a | [Pratique](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_op_less_than2) |
| `<>` ou `!=` | Diferente de | [Pratique](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_op_not_equal_to) |
| `BETWEEN` | Em um intervalo específico | [Pratique](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_op_between) |
| `LIKE` | Busca por padrões de texto | [Pratique](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_op_like) |
| `IN` | Especifica múltiplos valores possíveis | [Pratique](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_op_in) |

**Observação:** O operador `<>` é o padrão SQL para "diferente de", embora muitos sistemas de gerenciamento de banco de dados (SGBDs) modernos também aceitem `!=`. Utilize `<>` para garantir maior compatibilidade entre diferentes sistemas.

<br>

---

<p align="center">
  <a href="06_MySQL_SELECT_DISTINCT.md">⬅️ Anterior</a> | <a href="08_MySQL_ORDER_BY.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---