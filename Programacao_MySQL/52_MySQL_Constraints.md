## Restrições no MySQL (Constraints)

As **Constraints** (restrições) são as regras fundamentais que aplicamos às colunas de uma tabela em um banco de dados relacional. Elas atuam como sentinelas da integridade dos dados, garantindo que qualquer informação inserida, atualizada ou excluída esteja de acordo com a lógica de negócio estabelecida.

### Por que utilizar Constraints?
O propósito central das constraints é impedir a entrada de **dados inválidos**. Elas garantem a precisão e a confiabilidade do seu banco de dados. Caso uma operação viole uma regra definida, o MySQL aborta a ação imediatamente, protegendo a integridade da sua base de dados contra corrupção ou inconsistência.

As restrições podem ser aplicadas de duas formas:
* **No momento da criação:** Definidas diretamente no comando `CREATE TABLE`.
* **Após a criação:** Adicionadas posteriormente utilizando o comando `ALTER TABLE`.

---

## Principais Constraints do MySQL

No desenvolvimento de sistemas, as seguintes restrições são as mais utilizadas para modelar o comportamento de tabelas:

*   `NOT NULL`: Garante que uma coluna não possa conter valores nulos (é obrigatória).
*   `UNIQUE`: Assegura que todos os valores contidos em uma coluna sejam distintos entre si, evitando duplicidade.
*   `PRIMARY KEY`: A "identidade" da linha. É uma combinação de `NOT NULL` e `UNIQUE`. Identifica cada registro de forma única.
*   `FOREIGN KEY`: Estabelece um vínculo relacional entre tabelas, prevenindo ações que possam destruir a integridade desse relacionamento (como excluir um registro que possui dependências em outra tabela).
*   `CHECK`: Valida se os valores inseridos em uma coluna atendem a uma condição lógica específica.
*   `DEFAULT`: Define um valor padrão para a coluna caso nenhum valor seja especificado durante a inserção.
*   `CREATE INDEX`: Embora tecnicamente não seja uma restrição de integridade, é utilizado para otimizar a velocidade de recuperação de dados, criando índices em colunas específicas.

---

### Exemplo Prático de Aplicação

Ao projetar um sistema, imagine uma tabela de usuários. Você deseja que o `ID` seja único e obrigatório, e que o `E-mail` não seja repetido.

```sql
CREATE TABLE Usuarios (
    ID int NOT NULL PRIMARY KEY,
    Nome varchar(255) NOT NULL,
    Email varchar(255) UNIQUE,
    Status varchar(50) DEFAULT 'Ativo'
);
```

**Análise do código:**
1. O `ID` utiliza `PRIMARY KEY`, garantindo identificação exclusiva.
2. `Nome` utiliza `NOT NULL`, impedindo cadastros sem identificação do usuário.
3. `Email` utiliza `UNIQUE`, evitando que dois usuários se registrem com o mesmo endereço.
4. `Status` utiliza `DEFAULT`, economizando processamento ao preencher automaticamente o valor caso o desenvolvedor não o defina na query.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_create_table)

**Nota:** A utilização estratégica de constraints é o que diferencia uma aplicação robusta de uma aplicação vulnerável a erros de lógica. Sempre defina as regras no nível do banco de dados, nunca dependa apenas da validação no código da aplicação (Backend).

<br>

---

<p align="center">
  <a href="51_MySQL_Alter_Table.md">⬅️ Anterior</a> | <a href="53_MySQL_Not_Null.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---