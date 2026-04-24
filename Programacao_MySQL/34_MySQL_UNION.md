## O Operador UNION no MySQL

O operador **`UNION`** é uma ferramenta poderosa para manipulação de conjuntos de dados. Ele é utilizado para combinar o conjunto de resultados de duas ou mais instruções `SELECT` em um único resultado final.

Em cenários de desenvolvimento real, o `UNION` é fundamental quando você precisa agregar dados de tabelas diferentes que compartilham uma estrutura lógica semelhante (por exemplo, consolidar listas de contatos de fontes distintas como "Clientes" e "Fornecedores").

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

---

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

---

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

---

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
Neste exemplo, criamos uma coluna estática chamada `Type`. Ao analisar o relatório final, o desenvolvedor ou o sistema consumidor conseguirá distinguir, linha a linha, se aquele contato pertence à categoria de "Customer" ou "Supplier".

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_union3)

<br>

---

<p align="center">
  <a href="33_MySQL_Self_Join.md">⬅️ Anterior</a> | <a href="35_MySQL_UNION_ALL.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---