## O que é SQL?

O **SQL** (*Structured Query Language* - Linguagem de Consulta Estruturada) é o padrão da indústria para a comunicação com **Bancos de Dados Relacionais**. Imagine o banco de dados como um arquivo digital complexo e organizado; o SQL é o "idioma" que você utiliza para interagir com esse arquivo, permitindo inserir, buscar, atualizar e remover registros com precisão cirúrgica.

No ecossistema de desenvolvimento, o SQL é a espinha dorsal de quase todas as aplicações web. Seja em um sistema de e-commerce gerenciando o estoque ou em uma rede social processando perfis, a lógica de persistência de dados é quase sempre mediada por comandos SQL.

## Como utilizar o SQL

Para realizar operações no banco de dados, utilizamos comandos chamados **instruções** (*statements*). A instrução mais comum é a `SELECT`, que atua como uma ferramenta de busca para extrair informações de uma tabela específica.

```sql
SELECT * FROM Customers;
```

Neste exemplo, o asterisco (`*`) atua como um caractere curinga, solicitando "tudo" o que existe na tabela. Ao executar este comando, o banco de dados retorna todos os registros presentes na tabela `Customers`.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_all)

## Pontos importantes sobre a sintaxe

Ao escrever comandos SQL, há convenções que facilitam a leitura e a manutenção do código por equipes de desenvolvimento:

*   **Case Insensitivity:** As palavras-chave do SQL não diferenciam maiúsculas de minúsculas. Portanto, `select` e `SELECT` são interpretados da mesma forma pelo motor do banco de dados. 
    *   **Nota:** Por uma questão de legibilidade e boas práticas profissionais, adotaremos neste material o padrão de escrever todas as palavras-chave em **MAIÚSCULO**.

## O uso do ponto e vírgula (;)

O uso do **ponto e vírgula** (`;`) ao final de cada instrução é uma prática fundamental. Em muitos sistemas gerenciadores de banco de dados, o ponto e vírgula atua como um delimitador. Ele é essencial quando você precisa executar múltiplas instruções em uma única chamada ao servidor, permitindo que o sistema identifique onde termina um comando e começa o próximo.

## Comandos SQL essenciais

Para dominar a manipulação de dados, você deve se familiarizar com os comandos mais frequentes no mercado de trabalho. Eles são divididos, em termos gerais, entre manipulação de dados e definição de estrutura:

*   `SELECT`: Extrai dados de uma base.
*   `UPDATE`: Modifica dados existentes.
*   `DELETE`: Remove registros específicos.
*   `INSERT INTO`: Insere novas informações no banco.
*   `CREATE DATABASE`: Cria um novo contêiner para seus dados.
*   `ALTER DATABASE`: Modifica a estrutura ou configurações de um banco existente.
*   `CREATE TABLE`: Define uma nova tabela (a estrutura onde os dados residem).
*   `ALTER TABLE`: Altera a estrutura de uma tabela (adicionando colunas, por exemplo).
*   `DROP TABLE`: Exclui permanentemente uma tabela.
*   `CREATE INDEX`: Cria uma chave de busca, otimizando drasticamente a velocidade de consulta.
*   `DROP INDEX`: Remove um índice existente.

**Observação:** O comando `CREATE INDEX` é um dos diferenciais de um desenvolvedor de alto nível. Ele é aplicado quando uma tabela cresce a ponto de tornar as buscas (`SELECT`) lentas, permitindo que o banco localize registros quase instantaneamente.

<br>

---

<p align="center">
  <a href="03_MySQL_RDBMS.md">⬅️ Anterior</a> | <a href="05_MySQL_SELECT.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---