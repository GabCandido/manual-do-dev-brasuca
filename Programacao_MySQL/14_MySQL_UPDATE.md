## O Comando MySQL UPDATE

O comando **UPDATE** é a ferramenta fundamental na linguagem SQL para realizar a manutenção e a persistência de dados. Ele é utilizado para modificar os valores de um ou mais registros existentes em uma tabela, permitindo que o estado do banco de dados reflita as mudanças necessárias em um sistema (como alteração de endereço, atualização de preços ou status de um pedido).

### Sintaxe do UPDATE

A estrutura básica para atualizar registros segue a lógica de identificar a tabela, definir as novas atribuições e, crucialmente, filtrar quais registros serão afetados.

```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

*   **UPDATE:** Indica a tabela que sofrerá a alteração.
*   **SET:** Define as colunas que serão alteradas e seus novos valores.
*   **WHERE:** O filtro de segurança. Ele determina quais linhas devem receber as modificações.

---

**Nota:** Tenha extrema cautela ao utilizar o comando `UPDATE`. A cláusula `WHERE` especifica exatamente quais registros devem ser atualizados. **Se você omitir a cláusula WHERE, todos os registros da tabela serão alterados.**

---

### Exemplo Prático: Atualização de Registros

Imagine que precisamos atualizar as informações de contato e a cidade de um cliente específico no banco de dados. Utilizamos a `PRIMARY KEY` (neste caso, o `CustomerID`) para garantir que alteraremos apenas o registro desejado.

```sql
UPDATE Customers
SET ContactName = 'Alfred Schmidt', City = 'Frankfurt'
WHERE CustomerID = 1;
```

**Resultado esperado:** O sistema localizará a linha onde o `CustomerID` é igual a 1 e substituirá o valor de `ContactName` para "Alfred Schmidt" e `City` para "Frankfurt", mantendo os demais dados daquela linha intactos.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_update)

---

### Atualizando Múltiplos Registros

O poder do SQL reside na capacidade de manipular conjuntos de dados em massa. Ao definir uma condição (`WHERE`) que abrange várias linhas, o `UPDATE` aplicará as alterações em todos os registros que satisfizerem o critério.

```sql
UPDATE Customers
SET PostalCode = 00000
WHERE Country = 'Mexico';
```

**Por que isso é útil?** Em cenários de mercado, esta funcionalidade é indispensável para processos de normalização de dados, como corrigir um erro de cadastro em massa ou aplicar um ajuste de preço em todo o catálogo de produtos de uma categoria específica.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_update_multiple)

---

### Aviso: O perigo da ausência de WHERE

Como desenvolvedor, é vital entender a consequência de esquecer o filtro. Se você executar o comando abaixo sem o `WHERE`, o banco de dados interpretará que a intenção é aplicar o novo valor a **toda a tabela**.

```sql
UPDATE Customers
SET PostalCode = 00000;
```

**Observação:** Em um ambiente de produção real, isso causaria a perda irreparável de todos os códigos postais originais dos seus clientes. Sempre valide sua cláusula `WHERE` antes de executar um `UPDATE`, especialmente se estiver trabalhando diretamente na linha de comando ou em um terminal de gerenciamento.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_update_all)

<br>

---

<p align="center">
  <a href="13_MySQL_NULL_Values.md">⬅️ Anterior</a> | <a href="15_MySQL_DELETE.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---