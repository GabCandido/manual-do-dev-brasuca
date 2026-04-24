## A Declaração MySQL CREATE TABLE

A instrução `CREATE TABLE` é o alicerce fundamental para a persistência de dados em um sistema relacional. Ela é utilizada para definir a estrutura de uma nova tabela dentro de um banco de dados, estabelecendo as "regras de negócio" para a organização, o tipo de dado esperado em cada coluna e as restrições de integridade que garantem a qualidade da informação.

### Sintaxe Básica

Para criar uma tabela, você deve nomeá-la e definir cada coluna seguindo uma estrutura estrita de nome, tipo e, opcionalmente, uma regra de restrição.

```sql
CREATE TABLE table_name (
    column1 datatype constraint,
    column2 datatype constraint,
    column3 datatype constraint,
    ....
);
```

**Anatomia da estrutura:**
*   **`table_name`**: Define o identificador único da tabela.
*   **`column1`...**: Define o nome do campo.
*   **`datatype`**: Especifica o tipo de dado (como `int`, `varchar`, `date`). Isso é crucial para o motor do banco de dados otimizar o armazenamento e realizar validações automáticas.
*   **`constraint`**: Regras adicionais (como `PRIMARY KEY` ou `NOT NULL`) que impõem limites à integridade dos dados, evitando informações corrompidas ou duplicadas.

---

## Exemplo Prático: Criando uma Tabela de Pessoas

Vamos aplicar esse conceito criando uma tabela chamada `Persons`. Observe como definimos cada característica dos dados:

```sql
CREATE TABLE Persons
(
  PersonID int PRIMARY KEY,
  LastName varchar(255) NOT NULL,
  FirstName varchar(255),
  Address varchar(255),
  City varchar(255)
);
```

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_create_table)

### Decomposição do Exemplo:
*   **`PersonID int PRIMARY KEY`**: Utilizamos o tipo `int` para o identificador. A restrição `PRIMARY KEY` é vital: ela garante que cada linha seja única e serve como um índice para buscas extremamente rápidas.
*   **`LastName varchar(255) NOT NULL`**: O tipo `varchar(255)` reserva espaço para até 255 caracteres de tamanho variável. A instrução `NOT NULL` obriga que este campo seja preenchido; sem um sobrenome, o banco de dados rejeitará a inclusão do registro, mantendo a consistência dos dados.
*   **Colunas Adicionais**: `FirstName`, `Address` e `City` possuem flexibilidade. Como não definimos `NOT NULL`, o banco de dados aceitará valores nulos (vazios) por padrão caso o dado não esteja disponível no momento da inserção.

---

## Criação de Tabelas a partir de Tabelas Existentes

Em cenários reais de análise de dados ou migração, frequentemente precisamos extrair um subconjunto de dados para uma nova tabela. O MySQL permite fazer isso de forma direta utilizando uma combinação de `CREATE TABLE` e `SELECT`.

### Sintaxe de Duplicação Seletiva

Ao utilizar `AS SELECT`, você não apenas cria a estrutura da nova tabela, mas também popula essa tabela com os dados resultantes da consulta.

```sql
CREATE TABLE new_table AS
SELECT column1, column2,...
FROM existing_table
WHERE ....;
```

**Exemplo:**
Se você deseja segmentar apenas os clientes da Alemanha em uma nova tabela chamada `GermanCustomers` para um relatório de marketing, você faria:

```sql
CREATE TABLE GermanCustomers AS
SELECT * FROM Customers
WHERE Country = 'Germany';
```

**Nota:** Ao utilizar este método, o banco de dados copia a estrutura e os dados filtrados. No entanto, lembre-se que restrições complexas (como chaves primárias ou índices) podem não ser replicadas automaticamente dependendo da configuração; sempre verifique a estrutura da nova tabela após a criação.

**Observação:** Lembre-se que, após criar a tabela, ela estará inicialmente vazia (exceto no caso da criação via `SELECT`). Para preencher tabelas criadas manualmente, você utilizará futuramente a instrução `INSERT INTO`.

<br>

---

<p align="center">
  <a href="48_MySQL_Drop_DB.md">⬅️ Anterior</a> | <a href="50_MySQL_Drop_Table.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---