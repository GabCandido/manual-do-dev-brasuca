## O Operador MySQL UNION ALL

O operador `UNION ALL` é utilizado para combinar o **conjunto de resultados** (*result-set*) de duas ou mais declarações `SELECT` em uma única resposta unificada.

Diferente do operador `UNION` padrão, que filtra automaticamente linhas duplicadas para garantir valores únicos, o `UNION ALL` mantém **todas as linhas**, incluindo quaisquer duplicatas encontradas nas tabelas de origem.

### Requisitos para o uso de UNION ALL
Para que a união seja processada com sucesso pelo motor do banco de dados, as consultas devem respeitar três regras fundamentais de arquitetura:
1. **Consistência de Colunas:** Cada `SELECT` deve conter exatamente o mesmo número de colunas.
2. **Tipagem Compatível:** As colunas correspondentes nas diferentes instruções devem possuir tipos de dados compatíveis (ex: não é possível unir uma coluna do tipo `INTEGER` com uma `DATE` na mesma posição).
3. **Ordenação:** A ordem das colunas em cada instrução `SELECT` deve ser idêntica.

**Nota:** O nome das colunas no conjunto de resultados final será, por padrão, herdado da primeira instrução `SELECT`.

### Sintaxe
```sql
SELECT column_name(s) FROM table1
UNION ALL
SELECT column_name(s) FROM table2;
```

---

## Exemplo Prático: Unindo Dados

Imagine que você precisa extrair uma lista completa de cidades presentes tanto na tabela `Customers` quanto na tabela `Suppliers`. O `UNION ALL` é a ferramenta ideal para consolidar essa informação rapidamente.

```sql
SELECT City FROM Customers
UNION ALL
SELECT City FROM Suppliers
ORDER BY City;
```

**Resultado esperado:** Esta consulta retornará uma lista vertical contendo todas as cidades de ambas as tabelas. Caso uma cidade como "Berlin" apareça em ambas, ela será exibida duas vezes na lista final. O `ORDER BY` organiza o resultado resultante de forma alfabética.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_union_all)

---

## Filtrando Dados Combinados

Você pode utilizar a cláusula `WHERE` em cada um dos `SELECT` antes da operação de união. Isso permite que você combine apenas subconjuntos específicos de dados de diferentes tabelas.

```sql
SELECT City, Country FROM Customers
WHERE Country='Germany'
UNION ALL
SELECT City, Country FROM Suppliers
WHERE Country='Germany'
ORDER BY City;
```

**Por que usar este método?** 
Em cenários reais de análise de dados, essa técnica é amplamente utilizada para criar relatórios consolidados de entidades diferentes (como clientes e fornecedores) que compartilham atributos geográficos ou categorias, permitindo uma visão panorâmica sem a necessidade de criar joins complexos quando a estrutura dos dados é similar.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_union_all2)

**Observação:** Lembre-se que o `UNION ALL` é geralmente mais performático que o `UNION` padrão, pois o banco de dados não precisa realizar a tarefa adicional de processamento para comparar e remover linhas duplicadas. Utilize-o sempre que souber que as duplicatas não interferem no resultado final desejado.

<br>

---

<p align="center">
  <a href="34_MySQL_UNION.md">⬅️ Anterior</a> | <a href="36_MySQL_GROUP_BY.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---