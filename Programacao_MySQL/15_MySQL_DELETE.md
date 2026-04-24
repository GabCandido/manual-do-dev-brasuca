## A instrução DELETE no MySQL

A instrução **DELETE** é a ferramenta fundamental utilizada para remover registros existentes de uma tabela em um banco de dados relacional. Em sistemas de gestão de dados, saber como remover informações de forma precisa é tão importante quanto saber como inseri-las ou consultá-las.

### Sintaxe do DELETE

Para realizar a exclusão, utilizamos a estrutura básica abaixo:

```sql
DELETE FROM nome_da_tabela 
WHERE condicao;
```

O comando funciona seguindo uma lógica de filtragem: o MySQL localiza a tabela especificada e, através da cláusula **WHERE**, avalia cada linha. Se a linha atender aos critérios definidos, ela será permanentemente removida do banco de dados.

**Nota:** Tenha extrema cautela ao utilizar o `DELETE`. A cláusula `WHERE` é o que garante a segurança da operação. Se você omitir essa cláusula, o MySQL entenderá que você deseja remover **todos** os registros da tabela, o que geralmente resulta em perda de dados irreversível em ambientes de produção.

---

### Exemplo Prático

Imagine que precisamos remover o cliente "Alfreds Futterkiste" da nossa tabela de `Customers`. O comando seria estruturado da seguinte forma:

```sql
DELETE FROM Customers
WHERE CustomerName = 'Alfreds Futterkiste';
```

**Explicação:**
Após a execução deste comando, o motor do banco de dados varre a coluna `CustomerName` em busca do valor exato especificado. Ao encontrar a correspondência, o registro é deletado. A estrutura da tabela permanece intacta, mas a linha contendo os dados daquele cliente deixa de existir.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_delete)

---

### Removendo todos os registros

Existe um cenário onde o objetivo é limpar uma tabela, removendo todas as suas linhas, mas mantendo a sua estrutura (colunas, tipos de dados e índices). Para isso, utilizamos o `DELETE` sem a cláusula `WHERE`:

```sql
DELETE FROM nome_da_tabela;
```

**Observação:** Diferente do comando `DROP TABLE`, o `DELETE` apenas esvazia o conteúdo. A definição da tabela, que permite armazenar novos dados futuramente, continua presente no esquema do banco de dados.

---

### Diferença entre DELETE e DROP

É comum confundir a limpeza de dados com a remoção de toda a estrutura. Para deletar uma tabela **completamente** (incluindo sua definição e estrutura), utilizamos o comando `DROP TABLE`:

```sql
DROP TABLE nome_da_tabela;
```

*   **`DELETE`**: Remove registros linha a linha. É possível reverter (se transacionado corretamente) e a estrutura permanece.
*   **`DROP`**: Apaga a tabela do dicionário de dados do servidor. Não sobram vestígios da tabela.

**Dica de Arquitetura:** Em sistemas críticos, prefira utilizar "Soft Deletes" (uma coluna `is_deleted` ou `status`) em vez de deletar registros fisicamente. Isso permite auditoria e recuperação de dados excluídos acidentalmente por usuários.

<br>

---

<p align="center">
  <a href="14_MySQL_UPDATE.md">⬅️ Anterior</a> | <a href="16_MySQL_LIMIT.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---