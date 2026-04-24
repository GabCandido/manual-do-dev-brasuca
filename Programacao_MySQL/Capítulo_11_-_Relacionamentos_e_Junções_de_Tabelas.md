# Capítulo 11 - Relacionamentos e Junções de Tabelas

Em bancos de dados relacionais, os dados raramente residem em uma única tabela. Para manter a integridade e evitar a redundância, seguimos os princípios da **Normalização**, dividindo as informações em entidades distintas. A cláusula `JOIN` é a ferramenta fundamental para reconstruir essas relações, permitindo combinar linhas de duas ou mais tabelas com base em uma coluna relacionada entre elas.

Imagine que você possui uma tabela `Orders` (Pedidos) contendo apenas IDs de clientes, e uma tabela `Customers` (Clientes) com os detalhes cadastrais. O `JOIN` atua como o "elo" que permite extrair um relatório unificado onde cada pedido é exibido ao lado do nome real do cliente correspondente.

## Tipos de JOIN

Dependendo da sua necessidade de negócio — seja para obter apenas registros com correspondência total ou incluir dados incompletos — utilizamos diferentes tipos de junção:

*   **`INNER JOIN`**: Retorna apenas as linhas que possuem **valores correspondentes** em ambas as tabelas. É o tipo mais comum, ideal para quando você precisa de dados "completos".
*   **`LEFT JOIN`**: Retorna **todas as linhas da tabela da esquerda** e as linhas correspondentes da tabela da direita. Se não houver correspondência, o resultado exibirá `NULL` nos campos da direita.
*   **`RIGHT JOIN`**: O inverso do anterior; retorna **todas as linhas da tabela da direita** e as correspondentes da tabela da esquerda.
*   **`CROSS JOIN`**: Produz o **produto cartesiano**, combinando cada linha da primeira tabela com cada linha da segunda. Use com cautela, pois pode gerar volumes massivos de dados.

## O Comando INNER JOIN

O **INNER JOIN** é um dos pilares fundamentais da linguagem SQL. Ele retorna apenas as linhas que possuem valores correspondentes em ambas as tabelas; se uma linha não encontrar um par na outra, ela será excluída do conjunto de resultados.

### Sintaxe e Aplicação
Para realizar esta operação, utilizamos a cláusula `JOIN` acompanhada da palavra-chave `ON`, que define a regra de "casamento" entre os dados, geralmente comparando uma **Chave Primária** com uma **Chave Estrangeira**.

```sql
SELECT table1.column1, table1.column2, table2.column1
FROM table1
INNER JOIN table2 ON table1.condition_column = table2.condition_column;
```

**Exemplo Prático: Relacionando Produtos e Categorias**
Em um e-commerce, para exibir o nome do produto ao lado de sua categoria, cruzamos as tabelas `Products` e `Categories` via `CategoryID`:

```sql
SELECT Products.ProductID, Products.ProductName, Categories.CategoryName
FROM Products
INNER JOIN Categories ON Products.CategoryID = Categories.CategoryID;
```

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_join_inner)

**Nota:** O `INNER JOIN` é restritivo. Se um produto não possuir categoria (`NULL`), ele não aparecerá no resultado.

### Combinando Múltiplas Tabelas
É possível encadear cláusulas `INNER JOIN` para conectar diversas entidades. Ao fazer isso, transformamos uma estrutura normalizada em um relatório legível e consolidado:

```sql
SELECT Orders.OrderID, Customers.CustomerName, Shippers.ShipperName
FROM Orders
INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID
INNER JOIN Shippers ON Orders.ShipperID = Shippers.ShipperID;
```

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_join_inner2)

## O Comando LEFT JOIN

O `LEFT JOIN` preserva a integridade da tabela da esquerda. Ele garante que todos os seus registros sejam retornados, independentemente de possuírem correspondência na tabela da direita. Caso não haja correspondência, o MySQL preenche os campos da direita com **NULL**.

### Exemplo Prático: Identificando Lacunas
Esta junção é ideal para relatórios onde precisamos visualizar toda a base, como listar clientes que ainda não realizaram pedidos:

```sql
SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
LEFT JOIN Orders
ON Customers.CustomerID = Orders.CustomerID
ORDER BY Customers.CustomerName;
```

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_join_left)

**Nota:** Utilizando `WHERE Orders.CustomerID IS NULL`, podemos identificar "órfãos" (clientes inativos ou sem compras), uma técnica essencial em Business Intelligence.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_join_left2)

## O Comando RIGHT JOIN

O **RIGHT JOIN** é o espelho do `LEFT JOIN`. Ele prioriza a tabela listada após o comando `JOIN` (a da direita), retornando todos os seus registros e apenas as correspondências da tabela da esquerda.

### Exemplo Prático: Auditoria de Funcionários
No cenário de uma base de dados, para listar todos os funcionários e verificar quais deles não processaram pedidos, utilizamos:

```sql
SELECT Orders.OrderID, Employees.LastName, Employees.FirstName
FROM Orders
RIGHT JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID
ORDER BY Orders.OrderID;
```

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_join_right)

**Nota:** O uso de `RIGHT JOIN` é comum em auditorias para garantir que nenhuma entidade da tabela de referência seja omitida, mesmo sem transações vinculadas.

## O Comando CROSS JOIN

O `CROSS JOIN` retorna o **Produto Cartesiano**, combinando cada linha da primeira tabela com cada linha da segunda. 

**Nota:** Este comando pode gerar volumes massivos de dados rapidamente. Use-o para gerar matrizes de teste ou combinações complexas, como todas as variações de um produto (tamanho x cor).

```sql
SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
CROSS JOIN Orders;
```

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_join_cross)

## Self Join: A Autojunção

O **Self Join** ocorre quando uma tabela é conectada a ela mesma. Isso é fundamental para relações hierárquicas, como funcionários que reportam a gerentes ou clientes que residem na mesma cidade. Para realizá-lo, é obrigatório o uso de **Aliases** para distinguir as duas instâncias da mesma tabela.

### Exemplo Prático: Clientes na mesma cidade
Cruzamos a tabela `Customers` com ela mesma para encontrar pares de clientes que residem no mesmo local:

```sql
SELECT A.CustomerName AS CustomerName1, 
       B.CustomerName AS CustomerName2, 
       A.City
FROM Customers A, Customers B
WHERE A.CustomerID <> B.CustomerID
AND A.City = B.City 
ORDER BY A.City;
```

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_join_self)

**Nota:** Ao trabalhar com grandes volumes de dados, certifique-se de que as colunas utilizadas na cláusula `ON` possuam **índices** definidos. Isso reduz drasticamente o tempo de processamento, pois o motor do banco de dados não precisará percorrer toda a tabela para encontrar os pares correspondentes.

<br>

---

<p align="center">
  <a href="Capítulo_10_-_Relatórios_e_Agrupamentos_de_Dados.md">⬅️ Anterior</a> | <a href="Capítulo_12_-_Lógica_de_Conjuntos_e_Expressões_Condicionais.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---