## O Comando ALTER TABLE no MySQL

O comando **ALTER TABLE** é uma das ferramentas mais poderosas no arsenal de um desenvolvedor SQL. Ele é utilizado para modificar a estrutura de uma tabela que já existe, sem a necessidade de excluí-la e recriá-la do zero. Isso é fundamental para a **evolução de esquemas** em sistemas reais, onde você precisa adicionar novos campos ou ajustar restrições sem perder os dados já armazenados.

Com o `ALTER TABLE`, você pode:
* Adicionar, deletar ou renomear colunas.
* Alterar o tipo de dado (data type) ou o tamanho de uma coluna existente.
* Adicionar ou remover **constraints** (regras de integridade, como `NOT NULL`, `CHECK`, etc.).
* Renomear a própria tabela.

---

## Adicionando Colunas (ADD)

Quando os requisitos de negócio mudam e você precisa capturar novas informações, usamos o comando `ADD`.

### Sintaxe
```sql
ALTER TABLE table_name
ADD column_name datatype;
```

**Exemplo:** Adicionando uma coluna de e-mail na tabela de clientes.
```sql
ALTER TABLE Customers
ADD Email varchar(255);
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_alter_add)

**Nota:** Ao adicionar uma coluna em uma tabela que já possui dados, o MySQL preencherá automaticamente as linhas existentes com valores `NULL`, a menos que uma restrição padrão seja definida.

---

## Removendo Colunas (DROP)

Se um dado se tornou obsoleto ou desnecessário, o `DROP COLUMN` permite remover a estrutura da coluna permanentemente. **Cuidado:** esta ação é irreversível e excluirá todos os dados contidos nessa coluna.

### Sintaxe
```sql
ALTER TABLE table_name
DROP COLUMN column_name;
```

**Exemplo:** Removendo a coluna "Email".
```sql
ALTER TABLE Customers
DROP COLUMN Email;
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_alter_drop)

---

## Renomeando Colunas (RENAME)

Às vezes, a semântica de uma coluna muda. O `RENAME COLUMN` permite atualizar o nome para algo mais descritivo sem alterar o tipo de dado ou os valores.

### Sintaxe
```sql
ALTER TABLE table_name
RENAME COLUMN old_name TO new_name;
```

---

## Modificando Definições (MODIFY)

O comando `MODIFY` é usado para alterar a natureza de uma coluna. Isso é comum ao ajustar limites de caracteres (ex: aumentar um `varchar`) ou aplicar restrições de integridade.

**Exemplo:** Alterando o tamanho do e-mail e garantindo que ele não aceite valores nulos (`NOT NULL`).
```sql
ALTER TABLE Customers
MODIFY Email varchar(100) NOT NULL;
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_alter_modify)

---

## Adicionando Restrições (ADD CONSTRAINT)

As **constraints** garantem que os dados sigam regras específicas de negócio (como garantir que uma idade seja sempre maior que 18).

**Exemplo:** Criando uma regra de checagem (`CHECK`) na tabela de membros.
```sql
ALTER TABLE Members
ADD CONSTRAINT CHK_Age CHECK (Age >= 18);
```
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_alter_add_constraint)

---

## Renomeando Tabelas (RENAME TO)

Caso a entidade que a tabela representa precise de um novo nome para refletir melhor a arquitetura do banco.

**Exemplo:**
```sql
ALTER TABLE Customers
RENAME TO Clients;
```

---

## Exemplo Prático: Evolução de Tabela

Imagine que temos a tabela `Persons` com os campos `ID`, `LastName`, `FirstName`, `Address` e `City`.

### 1. Adicionando uma coluna de data
Para registrar a data de nascimento, usamos:
```sql
ALTER TABLE Persons
ADD DateOfBirth date;
```

### 2. Alterando o tipo de dado
Se decidirmos que queremos apenas o ano, podemos alterar o tipo da coluna:
```sql
ALTER TABLE Persons
MODIFY COLUMN DateOfBirth year;
```

### 3. Removendo a coluna
Se decidirmos que essa informação não é mais necessária:
```sql
ALTER TABLE Persons
DROP COLUMN DateOfBirth;
```

**Observação:** O gerenciamento cuidadoso de `ALTER TABLE` é vital em produção. Em bancos de dados muito grandes, comandos de alteração podem travar a tabela por um curto período (o chamado *locking*), por isso, em ambientes de missão crítica, essas alterações devem ser planejadas com cautela.

<br>

---

<p align="center">
  <a href="50_MySQL_Drop_Table.md">⬅️ Anterior</a> | <a href="52_MySQL_Constraints.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---