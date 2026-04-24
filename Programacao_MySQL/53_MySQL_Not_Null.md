## A Restrição MySQL NOT NULL

A integridade dos dados é um dos pilares de qualquer aplicação robusta. No MySQL, uma **Constraint** (restrição) é uma regra aplicada a uma coluna para limitar o tipo de dado que pode ser inserido. A restrição **NOT NULL** é fundamental para garantir a consistência das suas informações: ela força uma coluna a rejeitar valores nulos (`NULL`).

**Por que isso é importante?** 
Por padrão, colunas em bancos de dados SQL aceitam valores `NULL`. No entanto, em cenários reais de negócio — como o preenchimento de um cadastro de usuários ou um registro de transação financeira — existem campos que **não podem ser ignorados**, como o e-mail de um usuário ou o valor de uma compra. O `NOT NULL` impede que o banco aceite registros incompletos que poderiam quebrar a lógica da sua aplicação no futuro.

---

## Aplicando NOT NULL durante a criação da tabela

Para garantir que uma coluna seja obrigatória desde o momento em que a tabela nasce, adicionamos a palavra-chave `NOT NULL` logo após a definição do tipo de dado.

```sql
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255) NOT NULL,
    Age int
);
```

**Análise do código:**
Neste exemplo, estamos definindo que qualquer registro inserido na tabela `Persons` deve, obrigatoriamente, fornecer um `ID`, um `LastName` (sobrenome) e um `FirstName` (nome). Caso você tente inserir uma linha omitindo um desses valores, o MySQL retornará um erro e a operação será abortada. Observe que a coluna `Age` (idade) não possui esta restrição, portanto, ela é opcional e pode conter valores nulos.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trysql.asp?filename=trysql_create_table_notnull)

---

## Adicionando NOT NULL em tabelas existentes

E se a tabela já existir e você descobrir que um campo precisa ser obrigatório? Não há necessidade de excluir a tabela; utilizamos o comando `ALTER TABLE` em conjunto com `MODIFY` para aplicar essa regra retroativamente.

```sql
ALTER TABLE Persons
MODIFY Age int NOT NULL;
```

**Análise do código:**
O comando `MODIFY` altera a estrutura da coluna `Age` para que ela passe a exigir o preenchimento. 

**Nota:** Antes de aplicar esta restrição em uma tabela que já possui dados, certifique-se de que não existam registros com valor `NULL` na coluna, caso contrário, o comando falhará. Você deve limpar ou preencher esses dados antes de tornar a coluna obrigatória.

---

## Removendo a restrição NOT NULL

Se a regra de negócio mudar e você precisar permitir que uma coluna volte a aceitar valores nulos, a sintaxe é praticamente idêntica, substituindo o `NOT NULL` por `NULL`.

```sql
ALTER TABLE Persons
MODIFY Age int NULL;
```

**Observação:** Ao permitir valores `NULL`, você está liberando a flexibilidade do campo, mas lembre-se: quanto mais colunas permitem `NULL`, mais cauteloso deve ser o seu código na aplicação (Back-end), pois você precisará tratar a ausência de valores para evitar erros como `NullPointerException` ou comportamentos inesperados em cálculos matemáticos.

<br>

---

<p align="center">
  <a href="52_MySQL_Constraints.md">⬅️ Anterior</a> | <a href="54_MySQL_Unique.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---