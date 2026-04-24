## MySQL - Prepared Statements

As **Prepared Statements** (ou declarações preparadas) são um recurso fundamental para garantir a integridade e a segurança de uma aplicação. Elas funcionam como um modelo de consulta SQL pré-compilado, permitindo que a estrutura da query seja definida separadamente dos dados que serão processados.

O propósito central desta técnica é mitigar vulnerabilidades críticas, como o **SQL Injection**, onde usuários mal-intencionados tentam manipular comandos SQL através de entradas de dados não validadas.

### O Funcionamento em Duas Etapas

O processo de execução de uma *Prepared Statement* divide-se em dois momentos distintos:

1. **Prepare (Preparação):** Você envia um modelo de consulta SQL para o servidor utilizando *placeholders* (geralmente o caractere `?`). O banco de dados analisa, compila e otimiza este modelo sem executar a lógica. Como os dados ainda não foram enviados, não há risco de execução de código malicioso.
2. **Execute (Execução):** A aplicação vincula os valores reais aos parâmetros definidos e solicita a execução. O banco de dados insere esses valores nos locais reservados, tratando-os puramente como dados e nunca como comandos.

### Vantagens Estratégicas

*   **Redução do tempo de parsing:** Como a estrutura da query é compilada apenas uma vez, o servidor economiza recursos em execuções repetitivas.
*   **Otimização de largura de banda:** Você envia apenas os parâmetros nas execuções subsequentes, não a consulta completa.
*   **Segurança Robusta:** Elimina a necessidade de escapar manualmente cada caractere especial nas entradas do usuário, pois o protocolo de transporte de dados é isolado da estrutura da query.
*   **Código Limpo:** Promove a separação clara entre a lógica de persistência (SQL) e o conteúdo dos dados (variáveis).

---

## Implementação em PHP com MySQL

Abaixo, vemos como aplicar este conceito utilizando a extensão `mysqli` do PHP.

```php
<?php
$servername = "localhost";
$username = "username";
$password = "password";
$dbname = "myDB";

// Criação da conexão
$conn = new mysqli($servername, $username, $password, $dbname);

// Verificação de erro na conexão
if ($conn->connect_error) {
  die("Falha na conexão: " . $conn->connect_error);
}

// Modelo da consulta SQL com placeholders (?)
$sql = "INSERT INTO MyGuests (firstname, lastname, email) VALUES (?, ?, ?)";

// Preparação do modelo
if($stmt = $conn->prepare($sql)) {
  // Vinculação dos parâmetros: "sss" indica três strings
  $stmt->bind_param("sss", $firstname, $lastname, $email);

  // Definição dos valores e execução
  $firstname = "John";
  $lastname = "Doe";
  $email = "john@example.com";
  $stmt->execute();

  $firstname = "Mary";
  $lastname = "Moe";
  $email = "mary@example.com";
  $stmt->execute();

  echo "Novos registros criados com sucesso";
} else {
  echo "Erro: " . $sql . "<br>" . $conn->error;
}

$stmt->close();
$conn->close();
?>
```

[🚀 Pratique este código](https://www.w3schools.com/php/php_mysql_prepared_statements.asp)

**Explicação do código:**
Os pontos de interrogação `(?)` atuam como *placeholders* que serão preenchidos posteriormente. O método `bind_param()` é o coração desta operação: ele associa as variáveis do PHP aos parâmetros da consulta. O primeiro argumento `"sss"` define o tipo de dado de cada parâmetro, onde `s` significa *string*.

### Tipos de Dados Suportados
Ao definir os tipos no `bind_param`, você deve mapear corretamente cada parâmetro:

*   **i** - `integer` (número inteiro)
*   **d** - `double` (número de ponto flutuante)
*   **s** - `string` (texto)
*   **b** - `binary` (binários, como imagens ou PDFs)

**Nota:** Embora as *Prepared Statements* sejam uma barreira de segurança poderosa, a **sanitização** e a **validação** dos dados na origem continuam sendo boas práticas indispensáveis no desenvolvimento web profissional.

<br>

---

<p align="center">
  <a href="63_MySQL_Injection.md">⬅️ Anterior</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---