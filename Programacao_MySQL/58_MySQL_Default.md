## MySQL DEFAULT Constraint

A *constraint* **DEFAULT** é utilizada para definir um valor padrão para uma coluna. Quando um novo registro é inserido em uma tabela e nenhum valor é especificado para essa coluna específica, o MySQL automaticamente preenche o campo com o valor definido.

O uso desse recurso é uma excelente prática de **integridade de dados**, garantindo que campos importantes não fiquem vazios (nulos) por erro ou omissão, mantendo a consistência do banco de dados em cenários onde certos valores são repetitivos ou previsíveis.

---

## DEFAULT Constraint em CREATE TABLE

Ao definir a estrutura de uma tabela, você pode aplicar a regra de valor padrão diretamente na definição da coluna.

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

**Explicação:** Ao criar a tabela `Persons`, definimos que, caso o usuário não informe a cidade ao inserir uma nova pessoa, o sistema atribuirá automaticamente o valor `'Sandnes'`. Isso economiza tempo e evita inconsistências em registros incompletos.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_default_create)

### Uso de Funções de Sistema
O `DEFAULT` não se limita a valores estáticos (como strings ou números). Você também pode utilizar **funções do sistema** para gerar valores dinâmicos, como a data atual:

```sql
CREATE TABLE Orders
(
    ID int PRIMARY KEY,
    OrderNumber int NOT NULL,
    OrderDate date DEFAULT CURRENT_DATE()
);
```

**Nota:** A função `CURRENT_DATE()` captura a data do servidor no exato momento da inserção. Em aplicações reais, isso é fundamental para registros de auditoria e controle de pedidos, garantindo precisão temporal sem necessidade de intervenção da camada de aplicação (backend).

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_default_date)

---

## DEFAULT Constraint em ALTER TABLE

Se você já possui uma tabela criada e percebe a necessidade de adicionar uma regra de valor padrão a uma coluna existente, você pode alterar a estrutura da tabela utilizando o comando `ALTER TABLE`.

```sql
ALTER TABLE Persons
ALTER City SET DEFAULT 'Sandnes';
```

**Observação:** Diferente de outros bancos de dados que utilizam apenas `ADD CONSTRAINT`, no MySQL, o comando `ALTER ... SET DEFAULT` é a sintaxe padrão para modificar essa regra em colunas que já existem.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_default_alter)

---

## Remover (DROP) uma DEFAULT Constraint

Caso a regra de valor padrão não seja mais necessária, você pode removê-la facilmente para que a coluna volte a aceitar apenas valores explícitos ou `NULL`.

```sql
ALTER TABLE Persons
ALTER City DROP DEFAULT;
```

**Insight de Arquiteto:** A remoção de um `DEFAULT` é uma operação comum durante processos de **refatoração de banco de dados** ou migração de esquemas, quando a lógica de negócio exige que um campo deixe de ter um comportamento automático.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_default_drop)

<br>

---

<p align="center">
  <a href="57_MySQL_Check.md">⬅️ Anterior</a> | <a href="59_MySQL_Create_Index.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---