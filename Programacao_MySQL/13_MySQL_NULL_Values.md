## Valores NULL no MySQL

No mundo dos bancos de dados relacionais, nem sempre temos todas as informações disponíveis no momento em que um registro é criado. É aqui que entra o conceito de **NULL**.

Um valor `NULL` representa dados desconhecidos, ausentes ou inaplicáveis em um campo de uma tabela. É fundamental compreender que **NULL não é o mesmo que zero (0) ou uma string vazia ('')**. Enquanto o zero é um número e a string vazia é um caractere, `NULL` é um marcador de posição que indica a total ausência de um valor.

**Por que isso importa?**
Em cenários reais, como em um cadastro de clientes, talvez o `PostalCode` de um país onde esse dado não é utilizado deva ficar vazio. Se tentássemos inserir um "0", estaríamos inserindo um dado incorreto. O `NULL` preserva a integridade semântica da sua base de dados, informando que a informação simplesmente não existe para aquele registro.

---

## Como testar Valores NULL?

Como o `NULL` representa uma ausência, ele não possui um valor comparável. Por isso, você **não pode** utilizar operadores de comparação comuns, como `=` (igual), `<` (menor que) ou `<>` (diferente de), para verificar se um campo é `NULL`.

Para realizar essa tarefa, o SQL disponibiliza operadores específicos de teste: `IS NULL` e `IS NOT NULL`.

### Sintaxe: IS NULL
Utilizamos este operador para filtrar registros onde um campo específico não foi preenchido.

```sql
SELECT column_names
FROM table_name
WHERE column_name IS NULL;
```

### Sintaxe: IS NOT NULL
Utilizamos este operador para localizar registros que possuem algum dado inserido no campo, ignorando todos os que estiverem vazios.

```sql
SELECT column_names
FROM table_name
WHERE column_name IS NOT NULL;
```

---

## O Operador IS NULL

O operador `IS NULL` é a ferramenta correta para identificar lacunas nos seus dados.

**Exemplo:** Imagine que precisamos extrair uma lista de clientes que, por algum motivo, não possuem um endereço registrado na tabela `Customers`.

```sql
SELECT CustomerName, ContactName, Address
FROM Customers
WHERE Address IS NULL;
```

**Nota:** Ao executar este comando, o MySQL filtrará apenas as linhas onde o campo `Address` não recebeu nenhuma informação durante a inserção ou atualização.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_is_null)

---

## O Operador IS NOT NULL

Inversamente, o operador `IS NOT NULL` é essencial quando você precisa garantir que está trabalhando apenas com registros que possuem dados concretos em uma coluna específica.

**Exemplo:** Se você deseja listar todos os clientes que possuem um endereço cadastrado para fins de envio de correspondência, a consulta seria:

```sql
SELECT CustomerName, ContactName, Address
FROM Customers
WHERE Address IS NOT NULL;
```

**Dica:** Desenvolvedores experientes sempre utilizam `IS NULL` ou `IS NOT NULL` para tratar a existência de dados. Tentar usar `WHERE column = NULL` resultará em um erro de lógica, pois o banco de dados não consegue comparar um valor real com uma "ausência de valor".

<br>

---

<p align="center">
  <a href="12_MySQL_INSERT_INTO.md">⬅️ Anterior</a> | <a href="14_MySQL_UPDATE.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---