## O Operador EXISTS no MySQL

O operador **EXISTS** é uma ferramenta fundamental em SQL utilizada dentro de uma cláusula `WHERE`. Sua função principal é verificar a existência de registros em uma subconsulta (**subquery**).

Diferente de operadores que comparam valores diretamente, o `EXISTS` atua como um teste lógico: ele retorna **TRUE** se a subconsulta retornar pelo menos uma linha, e **FALSE** caso contrário. 

### Por que utilizar o EXISTS?
Em arquitetura de dados e desenvolvimento de sistemas, muitas vezes precisamos filtrar dados de uma tabela principal com base na existência de uma relação em outra tabela (por exemplo: "Liste todos os clientes que fizeram *pelo menos um* pedido"). O `EXISTS` é altamente eficiente para este cenário, pois o banco de dados pode parar de processar a subconsulta assim que encontrar a primeira correspondência, otimizando o desempenho em grandes volumes de dados.

### Sintaxe
```sql
SELECT column_name(s)
FROM table_name
WHERE EXISTS (subquery);
```

**Nota:** O `EXISTS` não retorna os dados da subconsulta em si, mas apenas um booleano que determina se a linha da tabela principal deve ser incluída no resultado final da consulta externa.

---

## Exemplos Práticos

Para ilustrar o uso, considere as tabelas `Suppliers` (Fornecedores) e `Products` (Produtos).

### Verificando a existência de produtos com preço específico
O código abaixo recupera o nome dos fornecedores que possuem pelo menos um produto com preço inferior a 20. Note como a subconsulta correlaciona o `SupplierID` de ambas as tabelas para validar a condição.

```sql
SELECT SupplierName 
FROM Suppliers
WHERE EXISTS (
  SELECT ProductName 
  FROM Products 
  WHERE Products.SupplierID = Suppliers.supplierID 
  AND Price < 20
);
```

**Explicação:** O motor do banco de dados percorre a tabela `Suppliers`. Para cada fornecedor, ele executa a subconsulta. Se encontrar um produto relacionado cujo preço seja menor que 20, o `EXISTS` retorna `TRUE` e o fornecedor é listado.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_exists)

---

O exemplo a seguir é uma variação, buscando fornecedores que oferecem produtos com o valor exato de 22.

```sql
SELECT SupplierName 
FROM Suppliers
WHERE EXISTS (
  SELECT ProductName 
  FROM Products 
  WHERE Products.SupplierID = Suppliers.supplierID 
  AND Price = 22
);
```

**Observação:** O uso do `EXISTS` é frequentemente comparado ao `IN`. Enquanto o `IN` geralmente avalia uma lista completa de valores, o `EXISTS` é mais performático em subconsultas complexas que dependem de colunas da tabela externa (subconsultas correlacionadas).

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_exists2)

<br>

---

<p align="center">
  <a href="37_MySQL_HAVING.md">⬅️ Anterior</a> | <a href="39_MySQL_ANY.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---