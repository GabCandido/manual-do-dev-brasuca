## A Função SUM() no MySQL

A função **SUM()** é uma das ferramentas fundamentais no arsenal de qualquer desenvolvedor ou analista de dados que utiliza SQL. Seu propósito central é realizar operações de **agregação**, permitindo que você calcule o total de uma coluna numérica em um conjunto de registros.

Em cenários reais de desenvolvimento — como sistemas de e-commerce, ERPs ou dashboards financeiros — você raramente precisará apenas listar dados; a necessidade de consolidar informações (como o total de vendas de um vendedor ou o estoque acumulado de um produto) é constante. A função `SUM()` é a forma mais direta de obter esse resultado diretamente no servidor de banco de dados, evitando a necessidade de transferir milhares de linhas para processamento posterior na sua aplicação (o que seria ineficiente).

### Sintaxe

A estrutura básica para utilizar a função segue a lógica de selecionar a agregação e indicar a origem dos dados:

```sql
SELECT SUM(column_name)
FROM table_name
WHERE condition;
```

**Explicação técnica:**
*   `column_name`: A coluna que contém os valores numéricos que você deseja somar.
*   `table_name`: A tabela onde os dados residem.
*   `WHERE condition` (Opcional): Permite filtrar os registros antes da soma, garantindo que o cálculo seja preciso apenas para o subconjunto desejado.

---

## Exemplo Prático: Calculando Totais

Imagine uma tabela chamada `OrderDetails` que armazena os itens de cada pedido. Para saber a quantidade total de itens vendidos em toda a loja, utilizamos o `SUM()` sem restrições.

### Código de Exemplo

```sql
SELECT SUM(Quantity) 
FROM OrderDetails;
```

**O que acontece aqui?**
O mecanismo de banco de dados varre a coluna `Quantity`, ignora qualquer valor que não seja numérico e retorna um único registro contendo a soma aritmética de todas as linhas.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_sum)

**Nota:** Um detalhe crucial para a integridade dos seus dados: a função `SUM()` **ignora valores NULL**. Se uma linha possuir um valor nulo em vez de um número, ela não será tratada como zero; ela será simplesmente excluída do cálculo, o que é um comportamento padrão e seguro para evitar distorções estatísticas.

---

## Filtrando com a cláusula WHERE

Na prática, quase sempre precisaremos de totalizações segmentadas. Se quisermos saber quanto foi vendido especificamente de um produto, combinamos o `SUM()` com a cláusula `WHERE`.

### Código de Exemplo

```sql
SELECT SUM(Quantity) 
FROM OrderDetails 
WHERE ProductId = 11;
```

**Resultado esperado:**
O motor do MySQL filtrará a tabela `OrderDetails` para encontrar apenas os registros onde o `ProductId` é 11. Após esse filtro (o subconjunto), a função `SUM()` entra em ação e soma apenas as quantidades correspondentes a esse produto específico.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_sum_where)

**Observação:** A utilização da cláusula `WHERE` antes da agregação é uma prática de performance essencial. Ao restringir os dados antes do cálculo, o MySQL utiliza menos recursos de memória e processamento, resultando em consultas muito mais rápidas em tabelas de larga escala.

<br>

---

<p align="center">
  <a href="20_MySQL_COUNT().md">⬅️ Anterior</a> | <a href="22_MySQL_AVG().md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---