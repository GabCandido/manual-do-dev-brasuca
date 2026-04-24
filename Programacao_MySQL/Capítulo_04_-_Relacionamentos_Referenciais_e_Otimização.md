# Capítulo 04 - Relacionamentos Referenciais e Otimização

Para garantir que um sistema de banco de dados seja robusto e eficiente, não basta apenas armazenar dados; é preciso definir regras que governem o comportamento das informações e otimizar a forma como o sistema as recupera. Este capítulo aborda as ferramentas essenciais para manter a integridade referencial e o desempenho em consultas.

## Restrição FOREIGN KEY no MySQL

A restrição **FOREIGN KEY** (chave estrangeira) é o mecanismo fundamental para garantir a **integridade referencial** em bancos de dados relacionais. Seu propósito central é estabelecer um vínculo lógico entre duas tabelas, assegurando que a relação entre os dados permaneça consistente e que operações não autorizadas, como a exclusão de um registro pai cujos dados ainda são referenciados, sejam bloqueadas pelo sistema.

Uma **FOREIGN KEY** é uma coluna (ou conjunto de colunas) em uma tabela que aponta diretamente para a **PRIMARY KEY** de outra tabela.

*   **Tabela Filha (Child Table):** É a tabela que contém a coluna com a chave estrangeira.
*   **Tabela Pai (Parent/Referenced Table):** É a tabela que contém a chave primária que está sendo referenciada.

### Por que utilizar FOREIGN KEY?

1.  **Consistência de Dados:** Impede a inserção de valores inválidos na tabela filha. Se o valor não existir na coluna de referência da tabela pai, o MySQL rejeitará a transação.
2.  **Proteção contra Exclusão Indevida:** O banco de dados impede que você delete um registro na tabela pai caso existam registros dependentes na tabela filha, evitando a criação de "dados órfãos".

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

### Definindo FOREIGN KEY no ALTER TABLE

Caso a tabela já exista, você pode aplicar a restrição de chave estrangeira posteriormente utilizando o comando `ALTER TABLE`.

```sql
ALTER TABLE Orders
ADD CONSTRAINT fk_Person
FOREIGN KEY (PersonID) 
REFERENCES Persons(PersonID);
```

**Explicação:** Este comando altera a estrutura da tabela `Orders` existente, impondo a restrição de integridade referencial sobre a coluna `PersonID` em relação à tabela `Persons`.

### Removendo uma Restrição FOREIGN KEY

Se precisar remover a regra de integridade, utilize o comando `DROP FOREIGN KEY`:

```sql
ALTER TABLE Orders
DROP FOREIGN KEY fk_Person;
```

> **Observação:** Ao remover uma `FOREIGN KEY`, o banco de dados deixa de validar a relação entre as tabelas, permitindo operações que antes eram bloqueadas. Use com cautela para não comprometer a integridade dos seus dados.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_create_table_fk)

---

## MySQL CHECK Constraint

Além de relacionar tabelas, precisamos garantir a qualidade dos dados individuais. A restrição **CHECK** é um mecanismo fundamental de integridade, utilizada para assegurar que os valores inseridos em uma coluna satisfaçam uma condição lógica predefinida. Isso atua como uma "segunda linha de defesa", garantindo que, independentemente da origem da entrada, os dados sempre respeitem as regras de validade do seu domínio.

O funcionamento é binário:
* **TRUE**: A operação de inserção ou atualização prossegue.
* **FALSE**: A operação é abortada imediatamente e o MySQL dispara um erro.

### CHECK Constraint no CREATE TABLE

Ao definir uma tabela, podemos aplicar a restrição diretamente na coluna. No exemplo abaixo, garantimos que a idade de uma pessoa nunca seja inferior a 18 anos.

```sql
CREATE TABLE Persons
(
    ID int PRIMARY KEY,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int CHECK (Age >= 18)
);
```

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_check)

### Nomeando e combinando condições

Para facilitar a manutenção, é uma **boa prática** nomear a restrição. Além disso, podemos criar validações que envolvem múltiplas colunas:

```sql
CREATE TABLE Persons
(
    ID int PRIMARY KEY,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    City varchar(255),
    CONSTRAINT chk_PersonAge CHECK (Age >= 18 AND City = 'Sandnes')
);
```

> **Observação:** O uso de `AND` dentro do `CHECK` permite criar regras de negócio complexas. Aqui, a constraint exige que o usuário tenha no mínimo 18 anos **e** resida obrigatoriamente na cidade de 'Sandnes'.

### CHECK Constraint no ALTER TABLE

Se a tabela já existir, utilizamos o comando `ALTER TABLE` para adicionar a regra.

```sql
ALTER TABLE Persons
ADD CONSTRAINT chk_PersonAge CHECK (Age >= 18 AND City = 'Sandnes');
```

> **Nota:** Ao adicionar uma restrição a uma tabela que já contém dados, o MySQL tentará validar as linhas existentes. Se houver dados que violem a condição, o comando falhará.

Para remover, utiliza-se `DROP CHECK`:

```sql
ALTER TABLE Persons
DROP CHECK chk_PersonAge;
```

> **Importante:** Ao deletar uma constraint, você está removendo a validação automática do banco de dados. Certifique-se de que a lógica de negócio foi migrada para a sua camada de aplicação, caso contrário, o banco passará a aceitar valores inválidos.

---

## MySQL DEFAULT Constraint

Para campos onde valores recorrentes são esperados, a *constraint* **DEFAULT** é a solução ideal. Ela define um valor padrão para uma coluna, preenchendo-a automaticamente caso nenhum valor seja fornecido durante a inserção, promovendo a integridade ao evitar campos indesejadamente nulos.

### DEFAULT Constraint em CREATE TABLE

```sql
CREATE TABLE Persons
(
    ID int PRIMARY KEY,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    City varchar(255) DEFAULT 'Sandnes'
);
```

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_default_create)

### Uso de Funções de Sistema
O `DEFAULT` também aceita funções dinâmicas, o que é essencial para registros de auditoria:

```sql
CREATE TABLE Orders
(
    ID int PRIMARY KEY,
    OrderNumber int NOT NULL,
    OrderDate date DEFAULT CURRENT_DATE()
);
```

> **Nota:** A função `CURRENT_DATE()` captura a data do servidor no exato momento da inserção, garantindo precisão temporal sem necessidade de intervenção da camada de aplicação.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_default_date)

### Modificando e Removendo Defaults

Para adicionar ou alterar o valor padrão em uma coluna existente, utilizamos:

```sql
ALTER TABLE Persons
ALTER City SET DEFAULT 'Sandnes';
```

E, para remover:

```sql
ALTER TABLE Persons
ALTER City DROP DEFAULT;
```

> **Insight de Arquiteto:** A remoção de um `DEFAULT` é comum durante processos de **refatoração de banco de dados** ou migração de esquemas.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_default_alter)

---

## Otimizando Consultas com MySQL CREATE INDEX

Finalmente, quando a massa de dados cresce, a integridade não é suficiente; precisamos de velocidade. O comando `CREATE INDEX` atua como um "índice remissivo" de livro, permitindo ao banco encontrar registros específicos sem precisar realizar um *Full Table Scan* (ler a tabela inteira).

> **Nota:** Embora índices acelerem a leitura, eles possuem um custo de escrita, pois o MySQL precisa atualizar o índice a cada `INSERT`, `UPDATE` ou `DELETE`. Aplique índices apenas em colunas frequentemente utilizadas em cláusulas `WHERE`, `JOIN` ou `ORDER BY`.

### Tipos de Índices

*   **Non-unique Index (`CREATE INDEX`):** Permite repetições. Ideal para sobrenomes ou cidades.
*   **Unique Index (`CREATE UNIQUE INDEX`):** Garante a unicidade dos valores. Essencial para campos como e-mail ou CPF.

### Exemplos Práticos

```sql
-- Índice Simples
CREATE INDEX idx_lastname
ON Persons (LastName);

-- Índice Composto (Otimiza buscas por LastName E FirstName)
CREATE INDEX idx_lname_fname
ON Persons (LastName, FirstName);
```

A remoção de índices desnecessários também é vital para manter a performance:

```sql
ALTER TABLE Persons
DROP INDEX idx_lastname;
```

> **Observação:** A remoção de um índice é uma operação estrutural (DDL). Certifique-se de que nenhum script de relatório ou aplicação dependa da performance desse índice antes de removê-lo.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_create_index)

<br>

---

<p align="center">
  <a href="Capítulo_03_-_Integridade_de_Dados_e_Chaves_Primárias.md">⬅️ Anterior</a> | <a href="Capítulo_05_-_Recuperação_de_Dados_e_Ordenação.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---