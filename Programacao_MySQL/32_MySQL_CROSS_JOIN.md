## MySQL CROSS JOIN

O comando `CROSS JOIN` é uma operação fundamental na álgebra relacional dentro do ecossistema SQL. Ele retorna o **Produto Cartesiano** de duas ou mais tabelas. Em termos práticos, ele combina cada linha da primeira tabela com cada linha da segunda tabela.

**Por que isso importa?**
Diferente dos `JOINs` convencionais que buscam uma correspondência entre chaves (como o `ID`), o `CROSS JOIN` cria todas as combinações possíveis. No desenvolvimento de software, isso é útil para gerar matrizes de dados, testar limites de carga, criar relatórios de "combinações de itens" (como todas as cores de um produto com todos os tamanhos disponíveis) ou gerar dados sintéticos para testes de performance.

**Nota:** O `CROSS JOIN` pode gerar conjuntos de resultados massivos rapidamente. Se a Tabela A possui 100 linhas e a Tabela B possui 500, o resultado será de 50.000 linhas ($100 \times 500$). Sempre utilize com cautela em tabelas de produção extensas.

### Sintaxe

A estrutura básica segue a lógica declarativa do SQL, focando em "o que" queremos extrair:

```sql
SELECT column_name(s)
FROM table1
CROSS JOIN table2;
```

---

## Exemplo Prático: Produto Cartesiano

Imagine um cenário onde você precisa mapear cada cliente a cada pedido existente, independentemente de haver uma relação de venda direta no momento.

```sql
SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
CROSS JOIN Orders;
```

Após a execução, o banco de dados retornará uma tabela longa contendo todas as permutações possíveis entre nomes de clientes e números de pedidos.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_join_cross)

---

## O uso de CROSS JOIN com WHERE

É importante notar que, se você adicionar uma cláusula `WHERE` para restringir a combinação com base em uma relação lógica (por exemplo, `CustomerID`), o resultado final do `CROSS JOIN` será idêntico ao de um `INNER JOIN`.

```sql
SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
CROSS JOIN Orders
WHERE Customers.CustomerID = Orders.CustomerID;
```

**Observação:** Embora o resultado seja o mesmo que um `INNER JOIN`, o uso deste último é semanticamente preferível e mais comum na indústria, pois deixa claro para outros desenvolvedores que você está filtrando dados por uma chave relacional específica.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_join_cross_where)

<br>

---

<p align="center">
  <a href="31_MySQL_RIGHT_JOIN.md">⬅️ Anterior</a> | <a href="33_MySQL_Self_Join.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---