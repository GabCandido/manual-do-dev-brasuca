# Capítulo 03 - Integridade de Dados e Chaves Primárias

As **Constraints** (restrições) são as regras fundamentais que aplicamos às colunas de uma tabela em um banco de dados relacional. Elas atuam como sentinelas da integridade dos dados, garantindo que qualquer informação inserida, atualizada ou excluída esteja de acordo com a lógica de negócio estabelecida.

### Por que utilizar Constraints?
O propósito central das constraints é impedir a entrada de **dados inválidos**. Elas garantem a precisão e a confiabilidade do seu banco de dados. Caso uma operação viole uma regra definida, o MySQL aborta a ação imediatamente, protegendo a integridade da sua base de dados contra corrupção ou inconsistência.

As restrições podem ser aplicadas de duas formas:
* **No momento da criação:** Definidas diretamente no comando `CREATE TABLE`.
* **Após a criação:** Adicionadas posteriormente utilizando o comando `ALTER TABLE`.

## Principais Constraints do MySQL

No desenvolvimento de sistemas, as seguintes restrições são as mais utilizadas para modelar o comportamento de tabelas:

*   `NOT NULL`: Garante que uma coluna não possa conter valores nulos (é obrigatória).
*   `UNIQUE`: Assegura que todos os valores contidos em uma coluna sejam distintos entre si, evitando duplicidade.
*   `PRIMARY KEY`: A "identidade" da linha. É uma combinação de `NOT NULL` e `UNIQUE`. Identifica cada registro de forma única.
*   `FOREIGN KEY`: Estabelece um vínculo relacional entre tabelas, prevenindo ações que possam destruir a integridade desse relacionamento.
*   `CHECK`: Valida se os valores inseridos em uma coluna atendem a uma condição lógica específica.
*   `DEFAULT`: Define um valor padrão para a coluna caso nenhum valor seja especificado durante a inserção.
*   `CREATE INDEX`: Utilizado para otimizar a velocidade de recuperação de dados, criando índices em colunas específicas.

**Nota:** A utilização estratégica de constraints é o que diferencia uma aplicação robusta de uma aplicação vulnerável a erros de lógica. Sempre defina as regras no nível do banco de dados, nunca dependa apenas da validação no código da aplicação (Backend).

## A Restrição NOT NULL

A restrição **NOT NULL** é fundamental para garantir a consistência das suas informações. Por padrão, colunas em bancos de dados SQL aceitam valores `NULL`. No entanto, em cenários reais de negócio — como o preenchimento de um cadastro de usuários ou um registro de transação financeira — existem campos que **não podem ser ignorados**.

### Aplicando NOT NULL durante a criação
Para garantir que uma coluna seja obrigatória desde o nascimento da tabela, adicionamos a palavra-chave logo após a definição do tipo de dado:

```sql
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255) NOT NULL,
    Age int
);
```

[🚀 Pratique este código](https://www.w3schools.com/mysql/trysql.asp?filename=trysql_create_table_notnull)

### Modificação Retroativa
Caso precise tornar um campo obrigatório em uma tabela existente, utilize `ALTER TABLE` com `MODIFY`:

```sql
ALTER TABLE Persons
MODIFY Age int NOT NULL;
```

**Nota:** Antes de aplicar esta restrição, certifique-se de que não existam registros com valor `NULL` na coluna, caso contrário, o comando falhará. Para reverter, basta substituir `NOT NULL` por `NULL` no mesmo comando.

## A Restrição UNIQUE

Enquanto o `NOT NULL` foca no preenchimento, a restrição **UNIQUE** foca na exclusividade, garantindo que nenhum valor duplicado seja inserido em uma coluna específica. Diferente da *PRIMARY KEY*, você pode ter múltiplas colunas com *UNIQUE* em uma mesma tabela.

### Implementação de Unicidade
Ao definir a estrutura, podemos aplicar a regra na declaração da coluna ou criar uma restrição nomeada:

```sql
CREATE TABLE Persons
(
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    CONSTRAINT UC_Person UNIQUE (ID, LastName)
);
```

**Observação:** Ao usar `UNIQUE (ID, LastName)`, o MySQL validará se a **combinação** dos campos é única. Você pode ter o mesmo `ID` repetido se o `LastName` for diferente, e vice-versa.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trysql.asp?filename=trysql_unique)

**Insight de Arquiteto:** Sempre que você define uma restrição *UNIQUE*, o MySQL cria automaticamente um **índice** por baixo dos panos. Isso acelera drasticamente as consultas, pois o motor do banco não precisará realizar um "table scan" (leitura completa da tabela).

## Restrição PRIMARY KEY (Chave Primária)

A **PRIMARY KEY** é o alicerce da integridade. Ela funciona como o "RG" de um registro: é a combinação de `NOT NULL` e `UNIQUE`. Uma tabela pode conter apenas **uma** chave primária.

### Definindo a chave primária
Seja em uma única coluna ou composta, a definição é vital para o relacionamento entre tabelas (via *FOREIGN KEY*):

```sql
CREATE TABLE Persons (
    ID int,
    LastName varchar(255),
    PRIMARY KEY (ID, LastName)
);
```

[🚀 Pratique este código](https://www.w3schools.com/mysql/trysql.asp?filename=trysql_create_table_pk2)

**Importante:** Ao utilizar `ALTER TABLE` para definir uma chave primária em uma tabela existente, as colunas envolvidas **devem** ter sido criadas anteriormente com a restrição `NOT NULL`.

## Automatização com AUTO_INCREMENT

Para simplificar o gerenciamento de chaves primárias, o MySQL oferece o atributo **AUTO_INCREMENT**. Ele gera automaticamente um número exclusivo a cada novo registro, eliminando o risco de colisões manuais.

```sql
CREATE TABLE Persons
(
  Personid int AUTO_INCREMENT PRIMARY KEY,
  LastName varchar(255) NOT NULL
);
```

[🚀 Pratique este código](https://www.w3schools.com/mysql/trysql.asp?filename=trysql_create_table_auto_increment)

Ao inserir dados, você ignora a coluna de ID, permitindo que o banco de dados assuma a tarefa:

```sql
INSERT INTO Persons (LastName) VALUES ('Monsen');
```

Caso precise ajustar o ponto de partida da numeração para uma migração ou regra específica, utilize:
`ALTER TABLE Persons AUTO_INCREMENT = 100;`

<br>

---

<p align="center">
  <a href="Capítulo_02_-_Linguagem_de_Definição_de_Dados_(DDL).md">⬅️ Anterior</a> | <a href="Capítulo_04_-_Relacionamentos_Referenciais_e_Otimização.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---