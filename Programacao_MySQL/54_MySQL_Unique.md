## Restrição UNIQUE no MySQL

A restrição (constraint) **UNIQUE** é um mecanismo fundamental na integridade de dados em bancos de dados relacionais. Seu propósito central é garantir que nenhum valor duplicado seja inserido em uma coluna específica, assegurando a **unicidade** das informações.

Diferente da *PRIMARY KEY*, que identifica univocamente um registro inteiro, o *UNIQUE* é frequentemente utilizado para campos que possuem valor único por natureza, mas que não são necessariamente a chave primária da tabela (como e-mails, nomes de usuário ou números de documentos).

**Nota:** Você pode aplicar múltiplos *UNIQUE* em uma mesma tabela, enquanto a *PRIMARY KEY* é limitada a apenas uma.

---

## UNIQUE ao criar uma tabela

Ao definir a estrutura inicial de uma tabela, podemos aplicar a regra diretamente na declaração das colunas.

```sql
CREATE TABLE Persons
(
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    UNIQUE (ID)
);
```

**Explicação:** Aqui, o banco de dados impedirá que qualquer novo registro seja inserido caso o valor de `ID` já exista na tabela `Persons`. Se tentar inserir um ID repetido, o MySQL retornará um erro e abortará a transação.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_unique)

### Nomeando restrições

Para facilitar a manutenção futura (como a remoção de uma regra específica), é uma boa prática nomear sua restrição. Podemos também definir a unicidade composta, onde a combinação de valores em múltiplas colunas deve ser única.

```sql
CREATE TABLE Persons
(
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    CONSTRAINT UC_Person UNIQUE (ID,LastName)
);
```

**Observação:** Ao usar `CONSTRAINT UC_Person UNIQUE (ID, LastName)`, o MySQL validará se a **combinação** dos dois campos é única. Você pode ter dois registros com o mesmo `ID` desde que o `LastName` seja diferente, e vice-versa.

---

## UNIQUE com ALTER TABLE

Se a tabela já existe em produção e você precisa aplicar essa regra, utilize o comando `ALTER TABLE`.

```sql
ALTER TABLE Persons
ADD UNIQUE (ID);
```

Para nomear a restrição nesta fase:

```sql
ALTER TABLE Persons
ADD CONSTRAINT UC_Person UNIQUE (ID,LastName);
```

---

## Removendo uma restrição UNIQUE

Se a regra de negócio mudar e você precisar permitir valores duplicados, é possível remover a restrição utilizando o índice associado a ela.

```sql
ALTER TABLE Persons
DROP INDEX UC_Person;
```

**Insight de Arquiteto:** Sempre que você define uma restrição *UNIQUE*, o MySQL cria automaticamente um **índice** por baixo dos panos. Isso não apenas garante a integridade dos dados, mas também acelera drasticamente as consultas que utilizam essa coluna em cláusulas `WHERE`, pois o motor de busca do banco não precisará realizar um "table scan" (leitura completa da tabela) para encontrar o registro.

<br>

---

<p align="center">
  <a href="53_MySQL_Not_Null.md">⬅️ Anterior</a> | <a href="55_MySQL_Primary_Key.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---