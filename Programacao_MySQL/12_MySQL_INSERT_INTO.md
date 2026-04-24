## A instrução INSERT INTO no MySQL

A instrução **INSERT INTO** é o pilar fundamental para a persistência de dados em bancos relacionais. Sua função primordial é a criação de novos registros (linhas) dentro de uma tabela pré-existente. Sem ela, o banco de dados seria estático; é através do `INSERT` que alimentamos nossas aplicações com informações dinâmicas, como usuários, pedidos ou registros de logs.

Existem duas formas principais de estruturar esse comando, dependendo do seu objetivo e da sua familiaridade com o esquema da tabela.

### Sintaxe 1: Especificação de Colunas
Esta é a forma recomendada e mais segura para ambientes de produção. Ao listar as colunas explicitamente, você garante que o valor seja inserido no local correto, mesmo que a ordem das colunas no banco de dados seja alterada futuramente.

```sql
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);
```

### Sintaxe 2: Inserção Direta
Se você pretende preencher **todos** os campos da tabela em uma única operação, pode omitir os nomes das colunas. 

**Atenção:** Aqui a ordem é mandatória. Os valores devem respeitar rigorosamente a ordem em que as colunas foram definidas na criação da tabela (`CREATE TABLE`).

```sql
INSERT INTO table_name
VALUES (value1, value2, value3, ...);
```

---

## Exemplo Prático: Inserindo novos registros

Considere a tabela `Customers`. Para inserir um novo cliente sem especificar as colunas, garantindo que os valores correspondam à estrutura da tabela, utilizamos:

```sql
INSERT INTO Customers 
VALUES ('Cardinal', 'Tom B. Erichsen', 'Skagen 21', 'Stavanger', '4006', 'Norway');
```

**O que aconteceu aqui?**
O MySQL mapeou cada valor para a respectiva coluna na ordem correta. Como resultado, o registro foi adicionado com sucesso.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_insert_all)

**Nota:** Observe que não inserimos um valor para `CustomerID`. Em bancos de dados modernos, utilizamos colunas **auto-increment** (auto-incremento), que geram identificadores únicos de forma automática a cada nova inserção, prevenindo erros de duplicidade.

---

## Inserindo dados em colunas específicas

Muitas vezes, você não possui informações para preencher todos os campos (ou alguns campos possuem valores padrão). Nesse caso, listamos apenas as colunas desejadas:

```sql
INSERT INTO Customers (CustomerName, City, Country)
VALUES ('Cardinal', 'Stavanger', 'Norway');
```

**Resultado esperado:**
O banco de dados inserirá os valores especificados e deixará as colunas omitidas como `NULL` (nulo) ou utilizará o valor *default* configurado na coluna.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_insert_columns)

---

## Inserção de múltiplas linhas (Bulk Insert)

Para otimizar o desempenho em cenários onde precisamos adicionar diversos registros simultaneamente, o MySQL permite o envio de múltiplos conjuntos de valores em um único comando. Isso reduz o "overhead" de rede e processamento.

```sql
INSERT INTO Customers (CustomerName, ContactName, Address, City, PostalCode, Country)
VALUES
('Cardinal', 'Tom B. Erichsen', 'Skagen 21', 'Stavanger', '4006', 'Norway'),
('Greasy Burger', 'Per Olsen', 'Gateveien 15', 'Sandnes', '4306', 'Norway'),
('Tasty Tee', 'Finn Egan', 'Streetroad 19B', 'Liverpool', 'L1 0AA', 'UK');
```

**Observação:** Note que cada conjunto de valores é agrupado por parênteses e separado por uma vírgula. Esta técnica é altamente recomendada para processos de importação de dados ou inicialização de sistemas.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_insert_multiple)

<br>

---

<p align="center">
  <a href="11_MySQL_NOT.md">⬅️ Anterior</a> | <a href="13_MySQL_NULL_Values.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---