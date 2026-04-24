## O Operador ALL no MySQL

O operador **ALL** é uma ferramenta poderosa de lógica relacional usada para comparar um valor único com **cada um dos valores** retornados por uma subconsulta.

Diferente de consultas que buscam apenas um "match" (como o operador `IN` ou `ANY`), o `ALL` é restritivo: ele só retorna `TRUE` se a condição for satisfeita para **todos** os elementos do conjunto resultante da subconsulta. Em cenários de análise de dados, ele é frequentemente utilizado em cláusulas `WHERE` ou `HAVING` para validar regras de negócio que exigem conformidade total de um grupo.

### Sintaxe

A estrutura básica segue o padrão de comparação de subconsultas:

```sql
SELECT column_name(s)
FROM table_name
WHERE column_name operator ALL (subquery);
```

**Observação:** O *operator* deve ser um operador de comparação padrão, como `=`, `<>`, `!=`, `>`, `>=`, `<`, ou `<=`.

---

## Exemplo Prático

Para ilustrar, imagine que precisamos validar uma regra de negócio sobre o estoque. O exemplo abaixo tenta retornar o nome de um produto caso a sua `ProductID` seja igual a **todos** os registros da tabela `OrderDetails` onde a `Quantity` é igual a 10.

```sql
SELECT ProductName 
FROM Products
WHERE ProductID = ALL (
  SELECT ProductID
  FROM OrderDetails
  WHERE Quantity = 10
);
```

**O que esperar deste código?**
Logicamente, esta consulta retornará `FALSE` (ou nenhum resultado) na maioria dos casos reais. Como a coluna `Quantity` na tabela `OrderDetails` contém diversos valores diferentes, a subconsulta retornará uma lista variada de `ProductID`. O operador `ALL` só passaria no teste se o `ProductID` externo fosse igual a *cada um* desses itens retornados, o que é estatisticamente improvável em tabelas de vendas reais, onde um produto raramente domina todas as entradas de uma transação.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_all3)

**Nota:** O uso do `ALL` exige cautela. Se a subconsulta retornar um conjunto vazio, o operador `ALL` é considerado `TRUE` por padrão. Sempre valide o comportamento da sua subconsulta isoladamente antes de integrá-la com `ALL`.

<br>

---

<p align="center">
  <a href="39_MySQL_ANY.md">⬅️ Anterior</a> | <a href="41_MySQL_INSERT_SELECT.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---