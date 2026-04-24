## SQL Injection: Entendendo a Vulnerabilidade

A **SQL Injection** (Injeção de SQL) é uma técnica de exploração de falhas de segurança onde um atacante insere comandos SQL maliciosos em campos de entrada de dados de uma aplicação. O objetivo é manipular a consulta original para que o banco de dados execute operações não autorizadas, como ler, modificar ou excluir informações confidenciais.

No desenvolvimento de software, este é um dos vetores de ataque mais críticos. Ele ocorre quando dados fornecidos pelo usuário são concatenados diretamente em uma *string* de consulta SQL sem o devido tratamento, permitindo que a sintaxe do comando seja alterada pelo atacante.

---

## SQL Injection: O perigo da lógica "Sempre Verdadeira"

Muitas vezes, uma consulta SQL é construída dinamicamente. Se não houver validação, um usuário mal-intencionado pode alterar a lógica booleana da consulta.

Considere este exemplo de busca de usuário:

```sql
txtUserId = getRequestString("UserId");
txtSQL = "SELECT * FROM Users WHERE UserId = " + txtUserId;
```

Se o usuário inserir `105`, o SQL executado será `SELECT * FROM Users WHERE UserId = 105`. No entanto, um atacante pode inserir `105 OR 1=1`.

```sql
SELECT * FROM Users WHERE UserId = 105 OR 1=1;
```

**Por que isso acontece?**
Como a condição `OR 1=1` é **sempre verdadeira**, o banco de dados ignorará a restrição de `UserId` e retornará **todos os registros** da tabela `Users`. Se essa tabela contiver senhas ou dados sensíveis, o atacante terá acesso total a eles.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_injection)

---

## SQL Injection em formulários de Login

O mesmo princípio se aplica a formulários de autenticação. Imagine a consulta de verificação de login:

```sql
sql = 'SELECT * FROM Users WHERE Name ="' + uName + '" AND Pass ="' + uPass + '"'
```

Se o atacante inserir `" OR ""="` nos campos de `Name` ou `Pass`, a consulta resultante será:

```sql
SELECT * FROM Users WHERE Name ="" or ""="" AND Pass ="" or ""=""
```

**Nota:** Como a cláusula `OR ""=""` também é sempre verdadeira, o banco de dados interpretará a condição como sucesso, permitindo o login sem a necessidade de uma senha válida. Este é um exemplo clássico de como a falta de sanitização de *inputs* pode comprometer a segurança de todo o sistema.

---

## SQL Injection através de comandos em lote (Batched SQL)

Alguns bancos de dados permitem o uso de **Batched SQL statements** (instruções SQL em lote), onde múltiplos comandos são separados por ponto e vírgula (`;`). Isso abre margem para ataques destrutivos.

Se um campo de entrada permitir que o atacante encerre o comando original e inicie outro, as consequências podem ser fatais para a base de dados:

```sql
SELECT * FROM Users WHERE UserId = 105; DROP TABLE Suppliers;
```

**O que acontece aqui?**
1. O sistema executa a consulta original (`SELECT`).
2. O banco de dados prossegue e executa o segundo comando injetado, que neste exemplo deleta a tabela `Suppliers` inteira.

**Observação:** A prevenção definitiva contra SQL Injection não envolve apenas validar o que o usuário digita, mas sim utilizar **Prepared Statements** (consultas parametrizadas), que garantem que o dado seja tratado estritamente como valor, e nunca como parte do código SQL.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_injection_drop)

<br>

---

<p align="center">
  <a href="62_MySQL_Views.md">⬅️ Anterior</a> | <a href="64_MySQL_Prepared_Statements.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---