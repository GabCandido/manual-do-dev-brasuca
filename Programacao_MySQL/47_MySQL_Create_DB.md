## A declaração CREATE DATABASE no MySQL

A instrução `CREATE DATABASE` é a fundação de qualquer aplicação baseada em dados no ecossistema MySQL. Sua função principal é alocar um espaço de armazenamento lógico no servidor, permitindo que você organize tabelas, índices e outros objetos de banco de dados de forma isolada e estruturada.

**Nota:** Para executar este comando, é fundamental possuir **privilégios administrativos** no servidor. Sem as permissões adequadas (geralmente concedidas pelo usuário `root` ou um administrador do sistema), o MySQL negará a criação do novo esquema.

### Sintaxe

A estrutura básica é direta, focada na definição do nome que identificará o seu conjunto de dados.

```sql
CREATE DATABASE database_name;
```

---

## Exemplo Prático: Criando um Banco de Dados

Imagine que você está iniciando um novo projeto de catálogo de produtos. Para isolar os dados deste projeto, você criará um banco chamado `testDB`.

```sql
CREATE DATABASE testDB;
```

**O que acontece aqui?** Ao enviar esse comando para o servidor, o MySQL reserva um novo diretório no sistema de arquivos do servidor, preparando a estrutura necessária para que você comece a criar suas tabelas (tabelas onde os registros residirão).

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_create_db)

---

## Listando Bancos de Dados

Após criar um ou vários bancos, é comum precisar verificar o estado do servidor. O comando `SHOW DATABASES` exibe uma lista de todos os bancos que estão atualmente hospedados na instância MySQL que você está acessando.

### Sintaxe

```sql
SHOW DATABASES;
```

**Observação:** No contexto de desenvolvimento profissional, utilizar este comando é uma excelente forma de validar se o banco foi criado corretamente antes de tentar conectar sua aplicação (como um backend em Python ou Node.js) ao esquema recém-criado.

<br>

---

<p align="center">
  <a href="46_MySQL_Operators.md">⬅️ Anterior</a> | <a href="48_MySQL_Drop_DB.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---