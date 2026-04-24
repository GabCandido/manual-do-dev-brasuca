## O Operador OR no MySQL

Na manipulação de bancos de dados, a cláusula **WHERE** é a sua principal ferramenta para filtrar dados. No entanto, quando precisamos extrair registros que atendam a pelo menos uma condição entre várias, o operador **OR** torna-se indispensável.

O **OR** atua como um operador de união lógica: ele instrui o motor do banco de dados a retornar qualquer linha que satisfaça, pelo menos, uma das condições especificadas.

**Nota:** O operador **OR** exibirá um registro se **qualquer** uma das condições for verdadeira (**TRUE**).

### Filtrando com OR

Imagine que você precisa extrair do seu banco de dados todos os clientes localizados em cidades específicas. Em vez de realizar múltiplas consultas, você utiliza o **OR** para agrupar essas possibilidades.

```sql
SELECT * FROM Customers
WHERE City = 'Berlin'
OR City = 'Stuttgart';
```

Neste exemplo, o MySQL percorre a tabela `Customers`. Se o valor na coluna `City` for 'Berlin', o registro é selecionado. Se não for, ele verifica se é 'Stuttgart'. Se qualquer um desses testes resultar em verdadeiro, a linha é incluída no seu resultado final.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_where_or)

Da mesma forma, podemos aplicar o operador em colunas diferentes ou com outros critérios:

```sql
SELECT * FROM Customers
WHERE Country = 'Germany'
OR Country = 'Spain';
```

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_where_or2)

---

### Sintaxe

A estrutura básica segue uma lógica linear de verificação. Você pode encadear quantos operadores **OR** forem necessários para atender à regra de negócio da sua aplicação.

```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition1 OR condition2 OR condition3 ...;
```

---

### AND vs. OR: A Diferença Crucial

É comum confundir a lógica de filtros. Para garantir a precisão dos seus dados, lembre-se:

*   **AND**: Exibe o registro apenas se **todas** as condições forem verdadeiras. É restritivo.
*   **OR**: Exibe o registro se **qualquer** condição for verdadeira. É inclusivo.

---

### Combinando AND e OR

Em cenários reais, as regras de negócio raramente são simples. Frequentemente, você precisará combinar filtros restritivos (**AND**) com filtros inclusivos (**OR**). 

Para evitar ambiguidades na interpretação do banco de dados, utilizamos **parênteses**. Eles garantem a precedência da operação, funcionando como na matemática: o que está entre parênteses é avaliado primeiro.

```sql
SELECT * FROM Customers
WHERE Country = 'Germany'
AND (City = 'Berlin' OR City = 'Stuttgart');
```

**Por que usar parênteses?** Sem eles, o MySQL poderia interpretar a consulta de forma inesperada (devido à precedência de operadores), potencialmente retornando clientes de outros países caso a condição `City = 'Stuttgart'` fosse atendida. Os parênteses isolam a lógica do **OR**, garantindo que o sistema busque primeiro clientes de Berlin ou Stuttgart e, em seguida, filtre esse subconjunto para garantir que pertençam à Alemanha.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_where_and_or)

<br>

---

<p align="center">
  <a href="09_MySQL_AND.md">⬅️ Anterior</a> | <a href="11_MySQL_NOT.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---