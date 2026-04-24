## Restrição PRIMARY KEY no MySQL

A restrição **PRIMARY KEY** (Chave Primária) é o alicerce da integridade de dados em um banco de dados relacional. Sua função fundamental é identificar de forma única cada registro (linha) dentro de uma tabela.

Pense nela como o "RG" de um registro: assim como um CPF não pode se repetir e não faz sentido que um cidadão não tenha um identificador, uma `PRIMARY KEY` garante que nunca teremos dois registros idênticos que sejam impossíveis de distinguir. Tecnicamente, ela é a combinação de duas outras restrições: **UNIQUE** (garante que não haja valores duplicados) e **NOT NULL** (garante que o campo nunca esteja vazio).

**Observação:** Uma tabela pode ter apenas UMA `PRIMARY KEY`. Ela pode ser composta por uma única coluna ou pela combinação de várias colunas. Além disso, ela serve como o alvo principal para **FOREIGN KEY** (Chaves Estrangeiras) em outras tabelas, criando o relacionamento que dá nome aos Bancos de Dados Relacionais.

---

## Definindo PRIMARY KEY na criação (CREATE TABLE)

Ao projetar o esquema do seu banco de dados, você deve definir a chave primária logo na estrutura da tabela.

### Chave Primária em uma única coluna
Este é o cenário mais comum, onde um ID numérico identifica cada usuário ou produto.

```sql
CREATE TABLE Persons (
    ID int PRIMARY KEY,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int
);
```
**Resultado esperado:** A tabela `Persons` é criada com a coluna `ID` definida como o identificador único e obrigatório.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_create_table_pk)

### Chave Primária composta (Múltiplas colunas)
Às vezes, um único campo não é suficiente para garantir a unicidade. Nesses casos, usamos uma chave composta.

```sql
CREATE TABLE Persons (
    ID int,
    LastName varchar(255),
    FirstName varchar(255),
    Age int,
    PRIMARY KEY (ID, LastName)
);
```
**Resultado esperado:** A combinação dos valores em `ID` e `LastName` deve ser única. Por exemplo, o usuário pode ter o ID 1, mas se houver outro com ID 1, o sobrenome deverá ser diferente para que o registro seja aceito.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_create_table_pk2)

### Chave Primária Nomeada
Em sistemas de nível empresarial, é uma boa prática dar nomes às suas restrições. Isso facilita a manutenção futura, como identificar erros ou remover chaves específicas.

```sql
CREATE TABLE Persons (
    ID int,
    LastName varchar(255),
    FirstName varchar(255),
    Age int,
    CONSTRAINT PK_Person PRIMARY KEY (ID, LastName)
);
```
**Nota:** Ao nomear a restrição como `PK_Person`, você ganha controle semântico sobre o esquema, tornando a documentação e os logs de erro muito mais claros.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_create_table_pk3)

---

## Modificando tabelas existentes (ALTER TABLE)

Se você já possui uma tabela e precisa adicionar uma chave primária, utilize o comando `ALTER TABLE`.

### Adicionando chave primária simples
```sql
ALTER TABLE Persons
ADD PRIMARY KEY (ID);
```

### Adicionando chave primária nomeada em múltiplas colunas
```sql
ALTER TABLE Persons
ADD CONSTRAINT PK_Person PRIMARY KEY (ID, LastName);
```

**Importante:** Ao utilizar `ALTER TABLE` para definir uma chave primária, as colunas envolvidas **devem** ter sido criadas anteriormente com a restrição `NOT NULL`. O MySQL não permitirá que um campo que aceite valores nulos torne-se uma `PRIMARY KEY`.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_alter_table_pk)

---

## Removendo uma PRIMARY KEY

Se a estrutura de dados mudar ou se a chave primária atual não atender mais aos requisitos de negócio, você pode removê-la facilmente:

```sql
ALTER TABLE Persons
DROP PRIMARY KEY;
```

**Nota:** A remoção de uma `PRIMARY KEY` pode ter impactos profundos em sua aplicação, especialmente se houver outras tabelas referenciando esta chave via `FOREIGN KEY`. Sempre verifique as dependências antes de executar este comando em um ambiente de produção.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_drop_pk)

<br>

---

<p align="center">
  <a href="54_MySQL_Unique.md">⬅️ Anterior</a> | <a href="56_MySQL_Foreign_Key.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---