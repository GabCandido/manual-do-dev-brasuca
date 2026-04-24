## MySQL Self Join

Um **Self Join** (ou autojunção) é um tipo especial de operação em bancos de dados relacionais onde uma tabela é conectada a ela mesma. Embora a sintaxe utilize os comandos padrões de `JOIN`, o objetivo central é comparar linhas dentro da mesma entidade, tratando a tabela como se fossem duas fontes de dados distintas.

Isso é fundamental em cenários onde os dados possuem relações hierárquicas ou de comparação lateral — como funcionários que reportam a gerentes em uma única tabela de funcionários, ou clientes que residem na mesma cidade.

### Sintaxe do Self Join

Para realizar um Self Join, você deve obrigatoriamente utilizar **Aliases** (apelidos). Como estamos consultando a mesma tabela duas vezes, o SQL precisa de uma forma de distinguir qual "instância" da tabela estamos referenciando.

```sql
SELECT column_name(s)
FROM table1 T1, table1 T2
WHERE condition;
```

**Nota:** `T1` e `T2` são apelidos diferentes para a mesma tabela. Sem eles, o motor do banco de dados não saberia como diferenciar as colunas durante a comparação.

---

### Exemplo Prático: Comparando Dados da Mesma Tabela

Imagine que você precise identificar quais clientes moram na mesma cidade. Utilizando a tabela de `Customers`, cruzaremos os registros para encontrar pares que compartilhem o mesmo valor na coluna `City`, excluindo, obviamente, o mesmo registro comparado com ele mesmo.

```sql
SELECT A.CustomerName AS CustomerName1, 
       B.CustomerName AS CustomerName2, 
       A.City
FROM Customers A, Customers B
WHERE A.CustomerID <> B.CustomerID
AND A.City = B.City 
ORDER BY A.City;
```

**Explicação técnica:**
1. **`Customers A, Customers B`**: Aqui criamos duas instâncias virtuais da nossa tabela `Customers`.
2. **`A.CustomerID <> B.CustomerID`**: Esta é a condição de segurança. Ela garante que não compararemos o registro com ele mesmo (o que sempre seria verdadeiro).
3. **`A.City = B.City`**: Esta é a lógica de negócio principal, que filtra apenas os pares que habitam a mesma localidade.

O resultado esperado é uma lista de pares de clientes organizados pela cidade, permitindo análises de proximidade geográfica ou identificação de grupos dentro da mesma base de dados.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_join_self)

**Observação:** O uso de Self Joins é uma técnica de modelagem de dados extremamente eficiente para transformar tabelas "planas" em estruturas que revelam relacionamentos complexos sem a necessidade de criar tabelas auxiliares desnecessárias.

<br>

---

<p align="center">
  <a href="32_MySQL_CROSS_JOIN.md">⬅️ Anterior</a> | <a href="34_MySQL_UNION.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---