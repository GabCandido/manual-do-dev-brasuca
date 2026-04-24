## MySQL Views

Uma **View** (ou exibição) no MySQL é, essencialmente, uma tabela virtual definida por uma consulta SQL. Diferente de uma tabela comum, ela não armazena os dados fisicamente no disco; em vez disso, ela armazena a estrutura da consulta (**SELECT**).

Sempre que você acessa uma view, o banco de dados executa a consulta armazenada em tempo real, garantindo que os dados retornados sejam os mais recentes possíveis.

### Por que usar Views?
- **Simplificação:** Permite ocultar consultas complexas envolvendo múltiplas tabelas (JOINs) por trás de um nome simples.
- **Segurança:** Você pode expor apenas colunas específicas para determinados usuários, restringindo o acesso a campos sensíveis na tabela original.
- **Consistência:** Garante que toda a equipe utilize a mesma lógica de negócio (ex: o cálculo de um "preço com desconto") ao consultar dados.

---

## O Comando CREATE VIEW

Para criar uma visualização, utilizamos o comando `CREATE VIEW`. A sintaxe básica segue a estrutura de uma consulta padrão, encapsulada pelo comando de criação.

```sql
CREATE VIEW view_name AS
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

**Nota:** Como a view é uma "janela" para os dados, ela reflete sempre o estado atual das tabelas base. Se você alterar um registro na tabela original, o resultado retornado pela view será atualizado automaticamente na próxima execução.

---

## Exemplos Práticos

### 1. Criando uma View simples
Imagine que você precisa acessar frequentemente todos os clientes brasileiros. Em vez de repetir o filtro `WHERE Country = 'Brazil'` em várias partes do seu código, você cria uma view.

```sql
CREATE VIEW brazil_customers_view AS
SELECT CustomerName, ContactName
FROM Customers
WHERE Country = 'Brazil';
```

Para consultar esta view, tratamos o objeto como se fosse uma tabela comum:

```sql
SELECT * FROM brazil_customers_view;
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_view_create)

### 2. View com lógica de agregação
Views são extremamente úteis para encapsular cálculos complexos. O exemplo abaixo cria uma lista de produtos cujo preço está acima da média geral da tabela.

```sql
CREATE VIEW products_above_average_price AS
SELECT ProductName, Price
FROM Products
WHERE Price > (SELECT AVG(Price) FROM Products);
```

Após a execução, a consulta aos dados fica limpa e legível:

```sql
SELECT * FROM products_above_average_price;
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_view_create_avg)

---

## Atualizando uma View: CREATE OR REPLACE

Se precisar alterar a estrutura de uma view existente (por exemplo, adicionar uma nova coluna), utilize o comando `CREATE OR REPLACE VIEW`. Isso evita a necessidade de deletar e criar a view novamente.

```sql
CREATE OR REPLACE VIEW brazil_customers_view AS
SELECT CustomerName, ContactName, City
FROM Customers
WHERE Country = 'Brazil';
```

**Observação:** O comando acima sobrescreve a definição anterior, garantindo que a view esteja sempre alinhada com as mudanças no esquema do seu banco de dados.

---

## Removendo uma View: DROP VIEW

Quando uma view não for mais necessária, utilize o comando `DROP VIEW` para removê-la do catálogo do banco de dados. Este comando apaga a definição da view, mas **não afeta os dados das tabelas originais**.

```sql
DROP VIEW brazil_customers_view;
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_view_drop)

<br>

---

<p align="center">
  <a href="61_MySQL_Dates.md">⬅️ Anterior</a> | <a href="63_MySQL_Injection.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---