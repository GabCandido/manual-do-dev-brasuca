## A Função COUNT() no MySQL

A função **COUNT()** é uma das ferramentas mais fundamentais na manipulação de bancos de dados. Seu propósito central é realizar a **agregação de dados**, permitindo que você obtenha métricas quantitativas sobre o volume de registros em uma tabela ou subconjunto de dados.

No desenvolvimento de sistemas, o `COUNT()` é indispensável para gerar relatórios, implementar paginação (saber quantos itens existem para exibir por página) e validar a integridade de conjuntos de dados.

### Sintaxe do COUNT()

A versatilidade do `COUNT()` advém de como você estrutura seu argumento. A sintaxe básica segue este padrão:

```sql
SELECT COUNT([DISTINCT] column_name | *)
FROM table_name
WHERE condition;
```

**Nota:** O comportamento da função varia conforme o que é passado entre parênteses. Entender essa distinção é crucial para evitar erros em contagens de registros com valores `NULL`.

---

### Os Três Modos de Contagem

Para aplicar a função corretamente, considere como o MySQL interpreta diferentes entradas:

*   **`COUNT(*)`**: Conta o número total de linhas na tabela, **incluindo** registros com valores `NULL`. É a forma mais comum quando queremos saber o "tamanho" total da base.
*   **`COUNT(column_name)`**: Conta apenas as linhas onde o valor da coluna especificada **não é NULL**.
*   **`COUNT(DISTINCT column_name)`**: Filtra valores duplicados e conta apenas os valores **únicos e não-nulos** na coluna.

---

### Exemplos Práticos

Para ilustrar, utilizaremos uma tabela hipotética chamada `Products`:

| ProductID | ProductName | SupplierID | CategoryID | Unit | Price |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Chais | 1 | 1 | 10 boxes x 20 bags | 18.00 |
| 2 | Chang | 1 | 1 | 24 - 12 oz bottles | 19.00 |
| 3 | Aniseed Syrup | 1 | 2 | 12 - 550 ml bottles | 10.00 |
| 4 | Chef Anton's Cajun Seasoning | 2 | 2 | 48 - 6 oz jars | 22.00 |
| 5 | Chef Anton's Gumbo Mix | 2 | 2 | 36 boxes | 21.35 |

#### 1. Contando o total de registros
Para verificar o volume total de itens no inventário, usamos o asterisco (*).

```sql
SELECT COUNT(*) 
FROM Products;
```
**Resultado esperado:** Este comando retorna o número total de linhas presentes na tabela `Products`, sem filtrar por qualquer critério de coluna.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_count2)

#### 2. Contando valores em uma coluna específica
Se você deseja saber quantos produtos possuem um identificador definido:

```sql
SELECT COUNT(ProductID) 
FROM Products;
```
**Resultado esperado:** A query retorna a quantidade de linhas onde `ProductID` possui um valor atribuído (não nulo).

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_count)

#### 3. Contando valores únicos (DISTINCT)
Em cenários de negócio, frequentemente queremos saber a variedade de preços disponíveis, ignorando repetições.

```sql
SELECT COUNT(DISTINCT Price) 
FROM Products;
```
**Observação:** O uso de `DISTINCT` aqui é vital. Ele garante que, se dois produtos possuem o mesmo preço, eles sejam contabilizados como apenas uma unidade de valor.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_count_distinct)

---

### Filtrando com WHERE

O poder do `COUNT()` é ampliado quando combinado com cláusulas de filtro. Você não precisa contar a tabela inteira; pode restringir o cálculo a condições específicas.

```sql
SELECT COUNT(ProductID) 
FROM Products
WHERE Price > 20;
```
**Explicação:** Aqui, o MySQL primeiro aplica o filtro `WHERE Price > 20` e, sobre este subconjunto resultante, executa a contagem. É a maneira correta de responder a perguntas de negócio como: "Quantos produtos do meu catálogo custam mais de 20 reais?".

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_count3)

<br>

---

<p align="center">
  <a href="19_MySQL_MAX().md">⬅️ Anterior</a> | <a href="21_MySQL_SUM().md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---