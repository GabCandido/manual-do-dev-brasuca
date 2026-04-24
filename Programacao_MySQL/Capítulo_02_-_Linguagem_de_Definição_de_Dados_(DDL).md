# Definição de Estrutura (DDL)

A **Linguagem de Definição de Dados (DDL)** é o conjunto de comandos SQL responsáveis por estruturar o esqueleto do seu banco de dados. É através dela que definimos onde os dados serão armazenados, como estarão organizados e como evoluirão ao longo do tempo.

## A declaração CREATE DATABASE no MySQL

A instrução `CREATE DATABASE` é a fundação de qualquer aplicação baseada em dados no ecossistema MySQL. Sua função principal é alocar um espaço de armazenamento lógico no servidor, permitindo que você organize tabelas, índices e outros objetos de banco de dados de forma isolada e estruturada.

**Nota:** Para executar este comando, é fundamental possuir **privilégios administrativos** no servidor. Sem as permissões adequadas (geralmente concedidas pelo usuário `root` ou um administrador do sistema), o MySQL negará a criação do novo esquema.

### Sintaxe
A estrutura básica é direta, focada na definição do nome que identificará o seu conjunto de dados.

```sql
CREATE DATABASE database_name;
```

### Exemplo Prático: Criando um Banco de Dados
Imagine que você está iniciando um novo projeto de catálogo de produtos. Para isolar os dados deste projeto, você criará um banco chamado `testDB`.

```sql
CREATE DATABASE testDB;
```

**O que acontece aqui?** Ao enviar esse comando para o servidor, o MySQL reserva um novo diretório no sistema de arquivos do servidor, preparando a estrutura necessária para que você comece a criar suas tabelas.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_create_db)

## Listando Bancos de Dados
Após criar um ou vários bancos, é comum precisar verificar o estado do servidor. O comando `SHOW DATABASES` exibe uma lista de todos os bancos que estão atualmente hospedados na instância MySQL que você está acessando.

### Sintaxe
```sql
SHOW DATABASES;
```

**Observação:** No contexto de desenvolvimento profissional, utilizar este comando é uma excelente forma de validar se o banco foi criado corretamente antes de tentar conectar sua aplicação ao esquema recém-criado.

---

## O Comando DROP DATABASE no MySQL
O comando **`DROP DATABASE`** é a instrução utilizada para a exclusão permanente de um banco de dados. Diferente de comandos que apenas limpam registros, este remove a estrutura completa, incluindo todas as tabelas, índices, *views* e procedimentos armazenados.

**Nota:** Utilize este comando com extrema cautela. Uma vez executado, não há um comando "desfazer" (*undo*). Todos os dados associados serão eliminados definitivamente.

### Sintaxe
```sql
DROP DATABASE nome_do_banco;
```

**Observação:** Para executar esta operação, é imperativo que o usuário possua **privilégios administrativos**.

### Exemplo Prático
Para remover um banco de dados de testes chamado `testDB`:

```sql
DROP DATABASE testDB;
```

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_drop_db)

**Insights de Arquiteto:** Em ambientes de produção, o uso do `DROP DATABASE` é raro. Frequentemente, opta-se por mecanismos de **backup** (como `mysqldump`) antes de qualquer operação destrutiva. Em pipelines de CI/CD, este comando é usado em ambientes efêmeros de teste para garantir um estado limpo (*clean slate*).

---

## A Declaração MySQL CREATE TABLE
Uma vez que o banco de dados existe, precisamos definir as tabelas. A instrução `CREATE TABLE` estabelece as "regras de negócio" para a organização, o tipo de dado esperado em cada coluna e as restrições de integridade que garantem a qualidade da informação.

### Sintaxe Básica
```sql
CREATE TABLE table_name (
    column1 datatype constraint,
    column2 datatype constraint,
    ....
);
```

**Anatomia da estrutura:**
*   **`table_name`**: Identificador único da tabela.
*   **`datatype`**: Especifica o tipo de dado (como `int`, `varchar`, `date`).
*   **`constraint`**: Regras adicionais (como `PRIMARY KEY` ou `NOT NULL`).

### Exemplo Prático: Criando uma Tabela de Pessoas
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

### Criação a partir de Tabelas Existentes
O MySQL permite criar uma nova tabela baseada no resultado de uma consulta (`SELECT`), o que é ideal para migrações ou relatórios.

```sql
CREATE TABLE new_table AS
SELECT column1, column2 FROM existing_table WHERE condition;
```

---

## Comando DROP TABLE e a diferença com TRUNCATE
O **`DROP TABLE`** remove a estrutura da tabela inteira, enquanto o **`TRUNCATE TABLE`** mantém a estrutura, removendo apenas os registros de forma rápida.

### Sintaxe do DROP TABLE
```sql
DROP TABLE IF EXISTS table_name;
```

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_drop_table)

**Observação:** O `TRUNCATE` é considerado um comando DDL mais eficiente que o `DELETE`, pois ele reseta a tabela sem registrar cada linha excluída no log, sendo ideal para limpezas em massa.

---

## O Comando ALTER TABLE
O comando `ALTER TABLE` é essencial para a **evolução de esquemas**, permitindo modificar uma tabela existente sem a necessidade de recriá-la do zero.

### Operações comuns:
*   **Adicionar Coluna**: `ALTER TABLE nome_tabela ADD coluna tipo;`
*   **Remover Coluna**: `ALTER TABLE nome_tabela DROP COLUMN coluna;`
*   **Modificar Coluna**: `ALTER TABLE nome_tabela MODIFY coluna novo_tipo;`
*   **Renomear Tabela**: `ALTER TABLE nome_tabela RENAME TO novo_nome;`

**Exemplo de Evolução de Tabela:**
```sql
-- Adicionando uma coluna
ALTER TABLE Persons ADD DateOfBirth date;

-- Alterando o tipo
ALTER TABLE Persons MODIFY COLUMN DateOfBirth year;

-- Removendo a coluna
ALTER TABLE Persons DROP COLUMN DateOfBirth;
```

[🚀 Pratique estes comandos](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_alter_add)

**Observação:** Em bancos de dados grandes, comandos de `ALTER TABLE` podem causar *locking* (bloqueio) na tabela. Planeje essas alterações para momentos de baixa carga no servidor.

<br>

---

<p align="center">
  <a href="Capítulo_01_-_Introdução_e_Arquitetura_RDBMS.md">⬅️ Anterior</a> | <a href="Capítulo_03_-_Integridade_de_Dados_e_Chaves_Primárias.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---