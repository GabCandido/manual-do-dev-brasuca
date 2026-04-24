# Capítulo 12 - Lógica de Conjuntos e Expressões Condicionais

Neste capítulo, exploraremos como manipular conjuntos de dados de forma avançada e como implementar lógica condicional diretamente em nossas consultas SQL. Combinar resultados de múltiplas fontes e aplicar regras de negócio em tempo de execução são habilidades fundamentais para qualquer desenvolvedor que busca transformar dados brutos em inteligência estratégica.

## O Operador UNION no MySQL

O operador **`UNION`** é uma ferramenta poderosa para manipulação de conjuntos de dados. Ele é utilizado para combinar o conjunto de resultados de duas ou mais instruções `SELECT` em um único resultado final.

Em cenários de desenvolvimento real, o `UNION` é fundamental quando você precisa agregar dados de tabelas diferentes que compartilham uma estrutura lógica semelhante, como consolidar listas de contatos de fontes distintas (ex: "Clientes" e "Fornecedores").

### Regras de Ouro para o uso de UNION
Para que a união de dados ocorra sem erros, é obrigatório respeitar três requisitos técnicos:

1. **Equivalência de Colunas:** Cada instrução `SELECT` deve possuir exatamente o mesmo número de colunas.
2. **Compatibilidade de Tipos:** As colunas nas mesmas posições devem possuir tipos de dados similares.
3. **Ordem Preservada:** A ordem das colunas definida na primeira instrução `SELECT` deve ser mantida nas demais.

**Observação:** Por padrão, o operador `UNION` filtra automaticamente duplicatas, garantindo que o conjunto final contenha apenas valores distintos.

### Sintaxe Básica

A estrutura reflete a junção vertical de resultados:

```sql
SELECT column_name(s) FROM table1
UNION
SELECT column_name(s) FROM table2;
```

**Nota:** Os nomes das colunas no resultado final serão herdados, por padrão, da primeira instrução `SELECT` declarada.

### Exemplo Prático: Consolidando Cidades
Imagine que precisamos listar todas as cidades presentes em nossa base, considerando tanto a tabela `Customers` quanto a `Suppliers`.

```sql
SELECT City FROM Customers
UNION
SELECT City FROM Suppliers
ORDER BY City;
```

Neste exemplo, o MySQL executará ambas as consultas, mesclará os resultados e removerá qualquer cidade que apareça em ambas as tabelas, apresentando uma lista única e organizada.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_union)

### Filtragem com WHERE
Você pode aplicar cláusulas `WHERE` individualmente em cada `SELECT` antes de uni-los. Isso permite isolar subconjuntos específicos de dados antes da consolidação final.

```sql
SELECT City, Country FROM Customers
WHERE Country='Germany'
UNION
SELECT City, Country FROM Suppliers
WHERE Country='Germany'
ORDER BY City;
```

Este código retorna apenas as cidades alemãs que aparecem nas duas tabelas, filtrando o conjunto de resultados conforme a regra de negócio aplicada.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_union2)

### Trabalhando com Identificadores (Aliasing)
Frequentemente, ao unir tabelas distintas, perdemos a referência da origem do dado. Para resolver isso, utilizamos **Aliases** (apelidos) para criar colunas temporárias que contextualizam a informação.

```sql
SELECT 'Customer' AS Type, ContactName, City, Country
FROM Customers
UNION
SELECT 'Supplier', ContactName, City, Country
FROM Suppliers;
```

**Por que usar Aliases?**
Neste exemplo, criamos uma coluna estática chamada `Type`. Ao analisar o relatório final, o desenvolvedor conseguirá distinguir, linha a linha, se aquele contato pertence à categoria de "Customer" ou "Supplier".

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_union3)

---

## O Operador MySQL UNION ALL

Enquanto o `UNION` limpa duplicatas, o operador **`UNION ALL`** é utilizado quando precisamos combinar o *result-set* de duas ou mais declarações `SELECT` preservando **todas as linhas**, incluindo quaisquer duplicatas encontradas nas tabelas de origem.

### Requisitos para o uso de UNION ALL
As regras de arquitetura são idênticas às do `UNION`:
1. **Consistência de Colunas:** Mesmo número de colunas.
2. **Tipagem Compatível:** Tipos de dados idênticos nas posições correspondentes.
3. **Ordenação:** Ordem das colunas idêntica.

**Nota:** O nome das colunas no conjunto de resultados final será herdado da primeira instrução `SELECT`.

### Sintaxe
```sql
SELECT column_name(s) FROM table1
UNION ALL
SELECT column_name(s) FROM table2;
```

### Exemplo Prático: Unindo Dados
Ao extrair a lista completa de cidades de `Customers` e `Suppliers`, o `UNION ALL` garante que, caso "Berlin" apareça em ambas, ela seja listada duas vezes.

```sql
SELECT City FROM Customers
UNION ALL
SELECT City FROM Suppliers
ORDER BY City;
```

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_union_all)

**Observação:** O `UNION ALL` é geralmente mais performático que o `UNION` padrão, pois o banco de dados não precisa realizar o processamento extra para comparar e remover linhas duplicadas. Utilize-o sempre que souber que as duplicatas não interferem no resultado final.

---

## Operadores de Subconsulta: EXISTS, ANY e ALL

Para além da união de conjuntos, o SQL oferece operadores especializados para validar relações entre uma tabela principal e subconsultas.

### O Operador EXISTS
O operador **`EXISTS`** é uma ferramenta fundamental para testar a existência de registros. Ele retorna `TRUE` se a subconsulta encontrar pelo menos uma linha, sendo altamente eficiente para validar relacionamentos sem retornar os dados da subconsulta em si.

```sql
SELECT SupplierName 
FROM Suppliers
WHERE EXISTS (
  SELECT ProductName 
  FROM Products 
  WHERE Products.SupplierID = Suppliers.supplierID 
  AND Price < 20
);
```

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_exists)

### O Operador ANY
O operador **`ANY`** compara um valor único com uma lista retornada por uma subconsulta. Ele retorna `TRUE` se a condição for atendida por **pelo menos um** dos elementos resultantes.

```sql
SELECT ProductName 
FROM Products
WHERE ProductID = ANY (
  SELECT ProductID 
  FROM OrderDetails 
  WHERE Quantity = 10
);
```

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_any)

### O Operador ALL
Diferente dos anteriores, o **`ALL`** é restritivo: ele só retorna `TRUE` se a condição for satisfeita para **todos** os elementos do conjunto resultante da subconsulta. É ideal para validar conformidade total de um grupo.

```sql
SELECT ProductName 
FROM Products
WHERE ProductID = ALL (
  SELECT ProductID
  FROM OrderDetails
  WHERE Quantity = 10
);
```

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_all3)

---

## Declaração CASE: Lógica Condicional no SQL

Para finalizar nosso estudo sobre manipulação de dados, a instrução **`CASE`** introduz a capacidade de definir resultados dinâmicos com base em condições lógicas, assemelhando-se à estrutura `if-then-else` de linguagens de programação.

### Sintaxe
```sql
CASE
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    ELSE result
END;
```

### Exemplo Prático: Categorização de Dados
Transformar dados "crus" em informações organizadas é uma das maiores utilidades do `CASE`. Abaixo, rotulamos produtos com base em seu preço:

```sql
SELECT ProductName, Price,
CASE
  WHEN Price < 20 THEN 'Low Cost'
  WHEN Price BETWEEN 20 AND 50 THEN 'Medium Cost'
  ELSE 'High Cost'
END AS PriceCategory
FROM Products;
```

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_case)

**Nota:** O uso de `AS` após o bloco `END` é uma **boa prática**. Isso define um alias para a nova coluna calculada, conferindo clareza e profissionalismo aos seus relatórios.

<br>

---

<p align="center">
  <a href="Capítulo_11_-_Relacionamentos_e_Junções_de_Tabelas.md">⬅️ Anterior</a> | <a href="Capítulo_13_-_Objetos_Avançados,_Temporalidade_e_Segurança.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---