## A instrução MySQL INSERT INTO SELECT

A instrução **INSERT INTO SELECT** é uma ferramenta poderosa e eficiente para migração e manipulação de dados dentro do seu banco de dados. Em vez de inserir registros manualmente ou via aplicação externa, você utiliza o próprio motor do banco para copiar dados de uma tabela de origem (**source table**) e inseri-los em uma tabela de destino (**target table**).

Este comando é essencial em cenários de ETL (*Extract, Transform, Load*), arquivamento de logs, consolidação de tabelas temporárias ou backups rápidos de registros específicos.

**Observação:** A instrução `INSERT INTO SELECT` não altera os dados já existentes na tabela de destino; ela simplesmente adiciona as novas linhas ao conjunto existente.

### A Sintaxe Fundamental

Para que a operação ocorra sem erros, é imperativo que os tipos de dados das colunas na tabela de origem sejam compatíveis com os tipos das colunas na tabela de destino.

#### Copiando todas as colunas
Se você deseja espelhar os dados, a sintaxe é direta:

```sql
INSERT INTO target_table
SELECT * FROM source_table
WHERE condition;
```

**Nota:** Ao omitir a definição explícita das colunas, o banco de dados assume que a ordem e a quantidade de campos em ambas as tabelas são idênticas. Se houver qualquer divergência, a operação falhará.

#### Copiando colunas específicas
Para maior controle e segurança, é recomendável mapear quais campos serão transferidos:

```sql
INSERT INTO target_table (column1, column2, column3, ...)
SELECT column1, column2, column3, ...
FROM source_table
WHERE condition;
```

Este formato é a melhor prática em ambientes de produção, pois protege seu código contra alterações na estrutura (como a adição de novas colunas) na tabela de origem.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_insert_into_select)

---

### Exemplos Práticos

Para ilustrar, imagine que desejamos consolidar informações de nossos fornecedores (`Suppliers`) dentro da nossa tabela principal de clientes (`Customers`).

#### 1. Inserção parcial
Aqui, copiamos apenas os dados essenciais. As colunas da tabela `Customers` que não foram incluídas no comando receberão o valor `NULL` (ou o valor padrão, caso configurado).

```sql
INSERT INTO Customers (CustomerName, City, Country)
SELECT SupplierName, City, Country FROM Suppliers;
```

#### 2. Cópia completa
Se a estrutura das tabelas for perfeitamente alinhada, podemos mover todo o conjunto de dados de uma vez:

```sql
INSERT INTO Customers
SELECT * FROM Suppliers;
```

#### 3. Inserção filtrada
A cláusula `WHERE` é fundamental para garantir a integridade dos dados. Podemos, por exemplo, mover apenas fornecedores de um país específico:

```sql
INSERT INTO Customers (CustomerName, City, Country)
SELECT SupplierName, City, Country FROM Suppliers
WHERE Country='Germany';
```

**Por que utilizar este método?** 
Ao processar a inserção no nível do servidor SQL, você reduz drasticamente o tráfego de rede e a carga na memória da sua aplicação. O banco de dados lida com a transação internamente, tornando a operação significativamente mais rápida e segura do que o método tradicional de "buscar, iterar e inserir via código".

<br>

---

<p align="center">
  <a href="40_MySQL_ALL.md">⬅️ Anterior</a> | <a href="42_MySQL_CASE.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---