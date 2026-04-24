## MySQL Aliases

Um **alias** (apelido) é um identificador temporário atribuído a uma coluna ou tabela durante a execução de uma instrução `SELECT`. Criado com a palavra-chave `AS`, ele é fundamental para melhorar a legibilidade de resultados complexos ou para simplificar referências em consultas que envolvem múltiplas fontes de dados.

**Nota:** Um alias existe apenas enquanto a consulta está sendo processada. Ele não altera o nome real da coluna ou tabela no banco de dados.

### Sintaxe de Alias para Colunas

Utilizamos aliases em colunas para transformar nomes técnicos ou abreviados em labels claros para relatórios ou interfaces de usuário.

```sql
SELECT column_name AS alias_name
FROM table_name;
```

### Sintaxe de Alias para Tabelas

Em consultas complexas com vários joins ou autojunções, aliases de tabelas reduzem a verbosidade do código, tornando-o mais fácil de ler e manter.

```sql
SELECT column_name(s)
FROM table_name AS alias_name;
```

---

## Alias para Colunas

O uso de aliases é a maneira mais elegante de apresentar dados. Em vez de exibir o nome bruto da coluna definido no esquema (que pode ser `cust_name_01`), você pode exibir `Cliente`.

```sql
SELECT CustomerID AS ID, CustomerName AS Customer
FROM Customers;
```

**Resultado esperado:** A saída apresentará as colunas com os cabeçalhos renomeados para "ID" e "Customer".

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_alias_column0)

---

## Alias com Espaços

Se o seu alias precisar conter espaços, caracteres especiais ou seguir uma convenção de nomenclatura específica, você deve envolver o nome entre aspas simples (`' '`) ou duplas (`" "`).

```sql
SELECT CustomerName AS Customer, ContactName AS "Contact Person"
FROM Customers;
```

**Observação:** Embora o SQL permita espaços, é uma boa prática de desenvolvimento evitar espaços em nomes de campos para facilitar a manipulação posterior em linguagens de programação (como Python ou PHP).

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_alias_column)

---

## Concatenando Colunas

Aliases são extremamente poderosos quando combinados com funções de string. Ao concatenar múltiplas colunas para formar um endereço completo, por exemplo, o alias fornece o nome da nova coluna virtual criada.

```sql
SELECT CustomerName, CONCAT_WS(', ', Address, PostalCode, City, Country) 
AS Address
FROM Customers;
```

**Por que usar:** O comando `CONCAT_WS` (Concatenate With Separator) une as colunas com uma vírgula. Sem o alias, o motor do banco de dados retornaria um nome de coluna pouco legível como `CONCAT_WS(', ', Address, ...)`. O alias garante que o resultado seja rotulado como `Address`.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_alias_column2)

---

## Alias para Tabelas

Em cenários reais, tabelas frequentemente possuem nomes longos. O uso de aliases (geralmente letras únicas como `c` para `Customers` e `o` para `Orders`) é o padrão da indústria para evitar que a query se torne ilegível.

```sql
SELECT o.OrderID, o.OrderDate, c.CustomerName
FROM Customers AS c, Orders AS o
WHERE c.CustomerName='Around the Horn' AND c.CustomerID=o.CustomerID;
```

**Dica de Arquiteto:** Compare com a versão sem alias:

```sql
SELECT Orders.OrderID, Orders.OrderDate, Customers.CustomerName
FROM Customers, Orders
WHERE Customers.CustomerName='Around the Horn' AND Customers.CustomerID=Orders.CustomerID;
```

A primeira opção é não apenas mais curta, mas reduz drasticamente a carga cognitiva de quem lê o código, permitindo focar na lógica do relacionamento entre as tabelas.

[🚀 Pratique este código (Com Alias)](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_alias_table)

[🚀 Pratique este código (Sem Alias)](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_alias_no)

---

### Quando utilizar Aliases?

A adoção de aliases é recomendada nos seguintes casos:
* Quando há mais de uma tabela envolvida na query.
* Quando funções (como `CONCAT`, `SUM`, `AVG`, `COUNT`) são aplicadas às colunas.
* Quando os nomes das colunas originais são excessivamente longos ou pouco intuitivos.
* Quando é necessário combinar duas ou mais colunas em um único campo de saída.

<br>

---

<p align="center">
  <a href="26_MySQL_BETWEEN.md">⬅️ Anterior</a> | <a href="28_MySQL_Joins.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---