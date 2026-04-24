## Comentários no MySQL

Os **comentários** são elementos fundamentais em qualquer linguagem de programação ou consulta. Eles permitem que desenvolvedores insiram anotações explicativas no código sem que o **mecanismo de banco de dados** (database engine) tente executá-las.

O propósito central dos comentários é duplo:
1. **Documentação:** Explicar a lógica de consultas complexas para facilitar a manutenção futura ou o trabalho em equipe.
2. **Depuração (Debugging):** Isolar partes específicas de um script ou desativar temporariamente comandos sem precisar deletá-los permanentemente.

O MySQL oferece suporte a duas formas de comentar código: comentários de linha única e comentários de múltiplas linhas.

---

## Comentários de Linha Única

Os comentários de uma única linha iniciam com os caracteres `--`. Tudo o que for digitado após esses caracteres, até o final da linha, será ignorado pelo servidor MySQL.

**Nota:** O MySQL exige estritamente um **espaço** após o segundo traço (`-- `). Sem este espaço, o interpretador pode gerar um erro se o código logo em seguida for mal interpretado.

### Exemplos de uso

Podemos usar comentários para documentar o que uma cláusula específica faz:

```sql
-- Seleciona todos os clientes da Alemanha
SELECT * FROM Customers
WHERE Country = 'Germany';
```

Também é possível utilizá-los no final de uma linha de código:

```sql
SELECT * FROM Customers -- WHERE City='Berlin';
```

Ou para "comentar" uma instrução inteira durante testes:

```sql
-- SELECT * FROM Customers;
SELECT * FROM Products;
```

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_comment_single_1)
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_comment_single_2)
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_comment_single_3)

---

## Comentários de Múltiplas Linhas

Quando você precisa inserir blocos maiores de texto ou comentar grandes trechos de código, utilizamos a sintaxe de bloco: `/* ... */`. Qualquer conteúdo inserido entre o abre e fecha do bloco é ignorado.

Este formato é muito utilizado para desativar blocos lógicos inteiros ou adicionar cabeçalhos descritivos em *Stored Procedures* e *Scripts* complexos.

### Exemplos de uso

Documentação detalhada ou explicação de regras de negócio complexas:

```sql
/* Seleciona todos os clientes alemães
   que residem especificamente em Berlim */
SELECT * FROM Customers
WHERE Country = 'Germany' AND City = 'Berlin';
```

Ignorando múltiplos comandos de uma vez:

```sql
/*SELECT * FROM Customers;
SELECT * FROM Products;
SELECT * FROM Orders;
SELECT * FROM Categories;*/
SELECT * FROM Suppliers;
```

Remoção pontual de uma coluna ou condição dentro de um comando:

```sql
SELECT CustomerName, /*City,*/ Country FROM Customers;
```

Ou isolando partes de uma cláusula `WHERE` para testes de filtro:

```sql
SELECT * FROM Customers 
WHERE (CustomerName LIKE 'L%'
OR CustomerName LIKE 'R%' /*OR CustomerName LIKE 'S%'
OR CustomerName LIKE 'T%'*/ OR CustomerName LIKE 'W%')
AND Country='USA'
ORDER BY CustomerName;
```

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_comment_multi_1)
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_comment_multi_2)
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_comment_part_1)
[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_comment_part_2)

<br>

---

<p align="center">
  <a href="44_MySQL_Stored_Procedures.md">⬅️ Anterior</a> | <a href="46_MySQL_Operators.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---