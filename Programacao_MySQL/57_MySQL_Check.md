## MySQL CHECK Constraint

A restrição **CHECK** é um mecanismo fundamental de integridade de dados no SQL. Sua função principal é garantir que os valores inseridos em uma coluna específica satisfaçam a uma condição lógica predefinida (uma expressão booleana).

Em cenários de desenvolvimento de sistemas, utilizamos o `CHECK` para aplicar regras de negócio diretamente no banco de dados. Isso atua como uma "segunda linha de defesa", garantindo que, independentemente da origem da entrada (API, formulário web ou script de migração), os dados sempre respeitem as regras de validade do seu domínio.

O funcionamento é binário:
* **TRUE**: A operação de inserção ou atualização prossegue.
* **FALSE**: A operação é abortada imediatamente e o MySQL dispara um erro, impedindo a persistência de dados inválidos.

---

## CHECK Constraint no CREATE TABLE

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

**Explicação:** O motor do MySQL avalia a expressão `Age >= 18` para cada nova linha. Se um valor abaixo de 18 for enviado, o banco rejeitará o registro, garantindo que sua tabela de "Adultos" não contenha dados inconsistentes.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_check)

### Nomeando uma CHECK Constraint

Para facilitar a manutenção ou remoção posterior da restrição, é uma **boa prática** nomeá-la utilizando a palavra-chave `CONSTRAINT`. Além disso, podemos criar validações que envolvem múltiplas colunas simultaneamente.

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

**Observação:** O uso de `AND` dentro do `CHECK` permite criar regras de negócio complexas. Aqui, a constraint exige que o usuário tenha no mínimo 18 anos **e** resida obrigatoriamente na cidade de 'Sandnes'.

---

## CHECK Constraint no ALTER TABLE

Se a tabela já existir e você precisar aplicar uma nova regra de negócio, utilizamos o comando `ALTER TABLE`. 

```sql
ALTER TABLE Persons
ADD CHECK (Age >= 18);
```

Para aplicar uma restrição nomeada em uma tabela pré-existente, utilizamos a sintaxe combinada:

```sql
ALTER TABLE Persons
ADD CONSTRAINT chk_PersonAge CHECK (Age >= 18 AND City = 'Sandnes');
```

**Nota:** Ao adicionar uma restrição a uma tabela que já contém dados, o MySQL tentará validar as linhas existentes contra a nova regra. Se houver dados que violem a condição, o comando falhará.

---

## Removendo uma CHECK Constraint

Caso a regra de negócio mude (por exemplo, a idade mínima deixe de ser um requisito fixo), você pode remover a restrição utilizando o comando `DROP`.

```sql
ALTER TABLE Persons
DROP CHECK chk_PersonAge;
```

**Importante:** Ao deletar uma constraint, você está removendo a validação automática do banco de dados. Certifique-se de que a lógica de negócio foi migrada para a sua camada de aplicação (código fonte), caso contrário, o banco passará a aceitar qualquer valor nessas colunas.

<br>

---

<p align="center">
  <a href="56_MySQL_Foreign_Key.md">⬅️ Anterior</a> | <a href="58_MySQL_Default.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---