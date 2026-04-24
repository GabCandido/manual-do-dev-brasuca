## Funções de Manipulação de NULL no MySQL

Em ambientes de banco de dados, a integridade da informação é vital. Operações que envolvem dados desconhecidos ou ausentes frequentemente levam a comportamentos inesperados. Para lidar com essa lacuna, o MySQL oferece mecanismos nativos para tratar valores `NULL`.

**Nota:** Um valor `NULL` não é o mesmo que zero (0) ou uma string vazia (""). Ele representa a **ausência de dados** ou uma informação desconhecida. Quando você realiza uma operação matemática envolvendo `NULL`, o resultado resultante será, invariavelmente, `NULL`.

### O Problema do `NULL` em Cálculos

Considere a seguinte tabela `Products`:

| PId | ProductName | Price | InStock | InOrder |
| :--- | :--- | :--- | :--- | :--- |
| 1 | Jarlsberg | 10.45 | 16 | 15 |
| 2 | Mascarpone | 32.56 | 23 | *null* |
| 3 | Gorgonzola | 15.67 | 9 | 20 |

Se tentarmos calcular o estoque total multiplicando o preço pela soma dos itens em estoque (`InStock`) e os itens sob encomenda (`InOrder`), teremos problemas:

```sql
SELECT ProductName, Price * (InStock + InOrder)
FROM Products;
```

**Resultado:** Para o produto "Mascarpone", o cálculo `32.56 * (23 + NULL)` resultará em `NULL`. Em cenários reais de negócio, isso pode quebrar relatórios financeiros e dashboards de estoque.

---

## Função COALESCE()

A função `COALESCE()` é o padrão recomendado pela linguagem SQL para lidar com valores ausentes. Ela avalia uma lista de argumentos e retorna o primeiro valor que **não seja NULL**.

### Sintaxe
```sql
COALESCE(val1, val2, ...., val_n)
```

Sua grande vantagem é a versatilidade: você pode fornecer múltiplas opções de substituição. Se `val1` for nulo, ele tentará `val2`, e assim por diante.

**Exemplo de Aplicação:**
```sql
SELECT ProductName, Price * (InStock + COALESCE(InOrder, 0))
FROM Products;
```

**Explicação:** Aqui, instruímos o banco de dados a considerar `0` caso o campo `InOrder` seja `NULL`. Isso garante que a operação aritmética prossiga com um número válido.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_func_mysql_coalesce)

---

## Função IFNULL()

A função `IFNULL()` é uma alternativa específica do MySQL para testar uma expressão e retornar um valor substituto caso o resultado seja `NULL`.

### Sintaxe
```sql
IFNULL(expr, alt)
```

Diferente do `COALESCE`, esta função aceita apenas dois argumentos: a expressão a ser testada (`expr`) e o valor que deve ser retornado caso ela seja nula (`alt`).

**Exemplo de Aplicação:**
```sql
SELECT ProductName, Price * (InStock + IFNULL(InOrder, 0))
FROM Products;
```

**Explicação:** O `IFNULL` verifica se `InOrder` contém dados. Se for nulo, o segundo argumento (0) é utilizado no cálculo, evitando que toda a linha retorne um valor nulo.

**Observação:** Embora o `IFNULL` seja simples e eficiente para substituições diretas, o uso de `COALESCE` é considerado uma **boa prática de arquitetura**, pois torna seu código SQL compatível com outros sistemas de banco de dados (como PostgreSQL ou SQL Server).

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_func_mysql_ifnull)

<br>

---

<p align="center">
  <a href="42_MySQL_CASE.md">⬅️ Anterior</a> | <a href="44_MySQL_Stored_Procedures.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---