## Restrição FOREIGN KEY no MySQL

A restrição **FOREIGN KEY** (chave estrangeira) é o mecanismo fundamental para garantir a **integridade referencial** em bancos de dados relacionais. Seu propósito central é estabelecer um vínculo lógico entre duas tabelas, assegurando que a relação entre os dados permaneça consistente e que operações não autorizadas, como a exclusão de um registro pai cujos dados ainda são referenciados, sejam bloqueadas pelo sistema.

Uma **FOREIGN KEY** é uma coluna (ou conjunto de colunas) em uma tabela que aponta diretamente para a **PRIMARY KEY** de outra tabela.

*   **Tabela Filha (Child Table):** É a tabela que contém a coluna com a chave estrangeira.
*   **Tabela Pai (Parent/Referenced Table):** É a tabela que contém a chave primária que está sendo referenciada.

### Por que utilizar FOREIGN KEY?

1.  **Consistência de Dados:** Impede a inserção de valores inválidos na tabela filha. Se o valor não existir na coluna de referência da tabela pai, o MySQL rejeitará a transação.
2.  **Proteção contra Exclusão Indevida:** O banco de dados impede que você delete um registro na tabela pai caso existam registros dependentes na tabela filha, evitando a criação de "dados órfãos".

---

### Exemplo Prático de Relacionamento

Imagine um sistema de e-commerce com as seguintes tabelas:

**Tabela Persons**
| PersonID | LastName | FirstName | Age |
| :--- | :--- | :--- | :--- |
| 1 | Hansen | Ola | 30 |
| 2 | Svendson | Tove | 23 |

**Tabela Orders**
| OrderID | OrderNumber | PersonID |
| :--- | :--- | :--- |
| 3 | 22456 | 2 |
| 4 | 24562 | 1 |

Neste cenário, a coluna `PersonID` na tabela `Orders` atua como a **FOREIGN KEY**, vinculando cada pedido ao indivíduo correspondente na tabela `Persons`.

---

### Definindo FOREIGN KEY no CREATE TABLE

Você pode definir a restrição no momento da criação da tabela. A instrução `CONSTRAINT` é usada para nomear a regra, facilitando manutenções futuras.

```sql
CREATE TABLE Orders
(
    OrderID int PRIMARY KEY,
    OrderNumber int NOT NULL,
    PersonID int,
    CONSTRAINT fk_Person
    FOREIGN KEY (PersonID)
    REFERENCES Persons(PersonID)
);
```

**Explicação:** O código acima cria a tabela `Orders` e define que o campo `PersonID` deve obrigatoriamente existir na tabela `Persons`. O nome `fk_Person` é um identificador para essa regra de negócio dentro do banco de dados.

---

### Definindo FOREIGN KEY no ALTER TABLE

Caso a tabela já exista, você pode aplicar a restrição de chave estrangeira posteriormente utilizando o comando `ALTER TABLE`.

```sql
ALTER TABLE Orders
ADD CONSTRAINT fk_Person
FOREIGN KEY (PersonID) 
REFERENCES Persons(PersonID);
```

**Explicação:** Este comando altera a estrutura da tabela `Orders` existente, impondo a restrição de integridade referencial sobre a coluna `PersonID` em relação à tabela `Persons`.

---

### Removendo uma Restrição FOREIGN KEY

Se precisar remover a regra de integridade, utilize o comando `DROP FOREIGN KEY`:

```sql
ALTER TABLE Orders
DROP FOREIGN KEY fk_Person;
```

**Observação:** Ao remover uma `FOREIGN KEY`, o banco de dados deixa de validar a relação entre as tabelas, permitindo operações que antes eram bloqueadas. Use com cautela para não comprometer a integridade dos seus dados.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_create_table_fk)

<br>

---

<p align="center">
  <a href="55_MySQL_Primary_Key.md">⬅️ Anterior</a> | <a href="57_MySQL_Check.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---