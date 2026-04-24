## O que é RDBMS?

**RDBMS** é a sigla para *Relational Database Management System* (Sistema de Gerenciamento de Banco de Dados Relacional). Na prática, um RDBMS é o software fundamental que utilizamos para criar, atualizar e administrar bancos de dados relacionais.

Sistemas como MySQL, Microsoft SQL Server, Oracle e Microsoft Access são construídos sob este paradigma. A importância de compreender o RDBMS reside no fato de que ele é o padrão industrial para garantir a **integridade dos dados**, a consistência e a capacidade de realizar consultas complexas entre diferentes conjuntos de informações.

No modelo relacional, os dados são organizados em objetos chamados **tabelas**. Uma tabela é, essencialmente, uma coleção estruturada de entradas relacionadas, composta por um conjunto definido de colunas e linhas.

---

## O que é uma Tabela de Banco de Dados?

Uma tabela é a unidade básica de armazenamento em um banco de dados. Para entender sua estrutura, imagine uma planilha:

*   **Coluna (ou Field):** É a entidade vertical. Define o tipo de dado que será armazenado (ex: nome, data, ID). Cada coluna possui um tipo específico, garantindo que os dados sigam um formato consistente.
*   **Linha (ou Record):** É a entidade horizontal. Representa cada entrada individual de dados, contendo um valor para cada coluna definida na tabela.

Veja um exemplo extraído da tabela "Customers" (Clientes):

| CustomerID | CustomerName | ContactName | Address | City | PostalCode | Country |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Alfreds Futterkiste | Maria Anders | Obere Str. 57 | Berlin | 12209 | Germany |
| 2 | Ana Trujillo | Ana Trujillo | Avda. Constitucion | México D.F. | 05021 | Mexico |
| 3 | Antonio Moreno | Antonio Moreno | Mataderos 2312 | México D.F. | 05023 | Mexico |
| 4 | Around the Horn | Thomas Hardy | 120 Hanover Sq. | London | WA1 1DP | UK |
| 5 | Berglunds | Christina Berglund | Berguvsvägen 8 | Luleå | S-958 22 | Sweden |

Neste exemplo, temos 7 colunas (campos) e 5 registros (linhas).

---

## O que é um Banco de Dados Relacional?

O termo "relacional" deriva da capacidade do sistema de definir **relacionamentos** entre diferentes tabelas. Em vez de armazenar todos os dados em um único lugar (o que geraria redundância e erros), o RDBMS permite que tabelas sejam vinculadas através de dados comuns, conhecidos como **chaves**.

Considere três tabelas do banco de dados *Northwind*:

### 1. Tabela Customers
Armazena informações cadastrais dos clientes.

### 2. Tabela Orders
Armazena o registro de cada venda realizada. 

**Nota:** O relacionamento entre a tabela *Customers* e *Orders* é estabelecido pela coluna `CustomerID`. Isso permite que o sistema saiba exatamente qual cliente fez qual pedido, sem precisar repetir o nome ou endereço do cliente em cada registro de pedido.

### 3. Tabela Shippers
Armazena dados sobre as transportadoras.

**Observação:** O relacionamento entre *Orders* e *Shippers* é feito através da coluna `ShipperID`. Esse modelo de normalização é o que torna os bancos de dados relacionais eficientes, permitindo que você atualize o endereço de uma transportadora apenas uma vez na tabela *Shippers*, e essa mudança seja refletida automaticamente em todos os pedidos associados.

[🚀 Pratique este código](https://www.w3schools.com/mysql/mysql_rdbms.asp)

<br>

---

<p align="center">
  <a href="02_MySQL_Intro.md">⬅️ Anterior</a> | <a href="04_MySQL_SQL.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---