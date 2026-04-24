## Otimizando Consultas com MySQL CREATE INDEX

No mundo dos bancos de dados relacionais, conforme a massa de dados cresce, o desempenho das suas consultas pode degradar significativamente. O comando `CREATE INDEX` é a ferramenta fundamental para contornar essa lentidão, agindo como um "índice remissivo" de livro, que permite ao banco encontrar registros específicos sem precisar ler a tabela inteira (processo conhecido como *Full Table Scan*).

O propósito central de um índice é **acelerar a recuperação de dados**. Quando você cria um índice, o MySQL constrói uma estrutura de dados separada (geralmente uma árvore B-Tree) que mapeia o valor da coluna ao local físico onde a linha reside na memória.

**Nota:** Embora índices acelerem a leitura, eles possuem um custo de escrita. Toda vez que você realiza um `INSERT`, `UPDATE` ou `DELETE` em uma tabela indexada, o MySQL precisa atualizar o índice também. Portanto, aplique índices apenas em colunas frequentemente utilizadas em cláusulas `WHERE`, `JOIN` ou `ORDER BY`.

---

## Tipos de Índices

Existem duas abordagens principais para definir como o banco deve gerenciar a unicidade dos dados:

*   **Non-unique Index (`CREATE INDEX`):** Permite que existam múltiplos registros com o mesmo valor na coluna indexada. É ideal para campos como `Sobrenome` ou `Cidade`, onde repetições são esperadas.
*   **Unique Index (`CREATE UNIQUE INDEX`):** Garante que não existam dois registros com o mesmo valor na coluna, disparando um erro caso uma tentativa de duplicidade ocorra. É essencial para campos como `E-mail` ou `CPF`.

### Sintaxe: Índice Comum
```sql
CREATE INDEX index_name
ON table_name (column1, column2, ...);
```

### Sintaxe: Índice Único
```sql
CREATE UNIQUE INDEX index_name
ON table_name (column1, column2, ...);
```

---

## Exemplos Práticos

Abaixo, vemos como aplicar um índice simples em uma tabela de pessoas.

```sql
CREATE INDEX idx_lastname
ON Persons (LastName);
```
**Explicação:** O índice `idx_lastname` agora armazena uma versão organizada da coluna `LastName`. Sempre que você buscar alguém pelo sobrenome, o banco consultará este índice primeiro, saltando diretamente para as linhas correspondentes.

**Dica de Arquiteto:** Você também pode criar índices em múltiplas colunas (índices compostos).

```sql
CREATE INDEX idx_lname_fname
ON Persons (LastName, FirstName);
```
**Resultado:** Isso otimiza consultas que filtram tanto por sobrenome quanto por nome, ou apenas pelo sobrenome (o índice composto atende a prefixos da ordem definida).

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_create_index)

---

## Removendo Índices

Se um índice não está mais sendo utilizado ou está causando lentidão excessiva em operações de escrita (escrita pesada), ele deve ser removido com o comando `DROP INDEX`.

```sql
ALTER TABLE table_name
DROP INDEX index_name;
```

**Observação:** Diferente de outras operações SQL, a remoção de um índice através de `ALTER TABLE` é uma operação estrutural (DDL). Certifique-se de que nenhum script de aplicação ou relatório dependa da performance desse índice antes de removê-lo.

<br>

---

<p align="center">
  <a href="58_MySQL_Default.md">⬅️ Anterior</a> | <a href="60_MySQL_Auto_Increment.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---