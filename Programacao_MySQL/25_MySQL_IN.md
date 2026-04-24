## O Operador IN no MySQL

O operador **IN** é uma ferramenta fundamental na linguagem SQL, utilizada dentro da cláusula `WHERE` para determinar se o valor de uma coluna específica corresponde a qualquer item presente em uma lista de valores predefinida.

Em termos de arquitetura de consulta, o `IN` atua como um atalho elegante para múltiplas condições `OR`. Ao evitar uma cadeia longa de operadores lógicos, você torna seu código não apenas mais curto, mas significativamente mais legível e fácil de manter.

### Sintaxe do Operador IN

A estrutura básica permite que você especifique uma coluna e uma lista de valores entre parênteses.

```sql
SELECT column_name(s)
FROM table_name
WHERE column_name IN (value1, value2, ...);
```

**Por que usar?** Imagine que você precise filtrar registros baseando-se em dez países diferentes. Utilizar `OR` repetidamente resultaria em uma linha de comando densa e propensa a erros de digitação. O `IN` abstrai essa complexidade, permitindo que o motor do banco de dados avalie a pertinência do dado dentro de um conjunto.

---

## Exemplo Prático: Filtragem de Dados

Considere uma tabela de clientes (*Customers*). Se o seu objetivo é extrair apenas os registros de clientes localizados na Alemanha, França ou Reino Unido, o operador `IN` simplifica drasticamente essa tarefa.

```sql
SELECT * FROM Customers
WHERE Country IN ('Germany', 'France', 'UK');
```

**Resultado esperado:** A consulta retornará todos os registros da tabela onde a coluna `Country` contenha exatamente um dos três valores especificados.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_in)

---

## O Operador NOT IN

Assim como podemos filtrar o que queremos incluir, frequentemente precisamos excluir dados específicos. O operador **NOT IN** realiza o trabalho inverso: ele retorna todos os registros cujos valores na coluna selecionada **não** estejam presentes na lista fornecida.

```sql
SELECT * FROM Customers
WHERE Country NOT IN ('Germany', 'France', 'UK');
```

**Nota:** Ao utilizar `NOT IN`, esteja atento a valores `NULL`. Em SQL, comparar `NULL` com uma lista pode resultar em comportamentos inesperados, pois `NULL` representa a ausência de valor e não "nada".

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_in_not)

---

## Utilizando IN com Subconsultas (Subqueries)

O verdadeiro poder do operador `IN` é revelado quando o combinamos com **subconsultas**. Em cenários reais, muitas vezes não sabemos os valores exatos de antemão, mas sabemos que eles devem existir em outra tabela relacionada.

O exemplo abaixo filtra clientes que possuem registros de pedidos na tabela `Orders`:

```sql
SELECT * FROM Customers
WHERE CustomerID IN (SELECT CustomerID FROM Orders);
```

**Observação:** Aqui, o SQL executa primeiro a *subquery* entre parênteses, cria um conjunto de resultados temporário e, em seguida, utiliza esse conjunto como filtro para a consulta principal. É uma forma eficiente de realizar cruzamento de dados (join implícito) sem a necessidade de um `JOIN` explícito.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_in2)

---

## NOT IN com Subconsultas

Da mesma forma, podemos usar `NOT IN` com subconsultas para identificar lacunas nos dados. Por exemplo, podemos localizar clientes que, por algum motivo, ainda não realizaram nenhum pedido.

```sql
SELECT * FROM Customers
WHERE CustomerID NOT IN (SELECT CustomerID FROM Orders);
```

Este tipo de consulta é essencial para tarefas de auditoria de dados e limpeza de base, permitindo identificar registros "órfãos" ou clientes inativos que não possuem movimentação vinculada no sistema.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_in3)

<br>

---

<p align="center">
  <a href="24_MySQL_Wildcards.md">⬅️ Anterior</a> | <a href="26_MySQL_BETWEEN.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---