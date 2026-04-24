## Campo AUTO_INCREMENT no MySQL

Um campo **AUTO_INCREMENT** é uma coluna numérica que gera automaticamente um número exclusivo sempre que um novo registro é inserido em uma tabela.

Este recurso é frequentemente utilizado em conjunto com a **PRIMARY KEY** (chave primária). O objetivo é garantir que cada linha da sua tabela possua um identificador único, sem a necessidade de gerenciamento manual ou risco de duplicidade de chaves. Em cenários reais, isso simplifica drasticamente a lógica de inserção de dados em bancos de dados relacionais.

---

## A palavra-chave AUTO_INCREMENT

O MySQL utiliza a palavra-chave `AUTO_INCREMENT` para ativar essa funcionalidade.

No exemplo abaixo, definimos a coluna "Personid" como uma chave primária auto-incrementável na tabela "Persons":

```sql
CREATE TABLE Persons
(
  Personid int AUTO_INCREMENT PRIMARY KEY,
  LastName varchar(255) NOT NULL,
  FirstName varchar(255),
  Age int
);
```

**Explicação:**
Ao declarar `AUTO_INCREMENT` junto ao tipo de dado `int`, instruímos o MySQL a gerenciar o valor daquela coluna. Por padrão, o valor inicial é **1** e ele incrementa em **1** a cada novo registro inserido.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trysql.asp?filename=trysql_create_table_auto_increment)

---

## Gerenciando o valor inicial

O valor padrão do incremento é sempre 1. Se, por questões de negócio ou migração de sistemas, você precisar que a contagem inicie em um número diferente (por exemplo, 100), utilize o comando `ALTER TABLE`:

```sql
ALTER TABLE Persons AUTO_INCREMENT = 100;
```

**Nota:** Alterar o valor inicial não afeta registros já existentes, apenas define o ponto de partida para os próximos registros a serem inseridos.

---

## Inserindo registros com AUTO_INCREMENT

Um dos grandes benefícios de utilizar o `AUTO_INCREMENT` é que, no momento da inserção, você **não precisa especificar** um valor para a coluna definida como auto-incrementável. O banco de dados assume essa responsabilidade automaticamente.

```sql
INSERT INTO Persons (FirstName, LastName)
VALUES ('Lars', 'Monsen');
```

**O que esperar:**
Ao executar este comando, o MySQL processará o registro e atribuirá automaticamente o próximo número disponível à coluna "Personid". Isso elimina a necessidade de consultas prévias para verificar qual o maior ID existente, prevenindo erros de concorrência em aplicações web de alto tráfego.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trysql.asp?filename=trysql_insert_auto_increment)

<br>

---

<p align="center">
  <a href="59_MySQL_Create_Index.md">⬅️ Anterior</a> | <a href="61_MySQL_Dates.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---