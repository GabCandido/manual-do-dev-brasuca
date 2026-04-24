## Wildcards no MySQL

Um **wildcard** (caractere curinga) é um símbolo especial utilizado para substituir um ou mais caracteres em uma string. No ecossistema SQL, eles são ferramentas indispensáveis para realizar buscas flexíveis, permitindo que você encontre dados sem precisar conhecer a cadeia de caracteres exata.

Os wildcards são utilizados em conjunto com o operador **LIKE**, que é aplicado na cláusula **WHERE** para filtrar resultados com base em um padrão específico.

### Tabela de Referência: Símbolos Wildcard

| Símbolo | Descrição | Exemplo |
| :--- | :--- | :--- |
| `%` | Representa zero, um ou múltiplos caracteres | `bl%` encontra "bl", "black", "blue", "blob" |
| `_` | Representa exatamente um único caractere | `h_t` encontra "hot", "hat", "hit" |

---

### O Poder da Flexibilidade: Combinando Operadores

Você não está limitado a usar um wildcard isoladamente. É possível combinar esses símbolos para criar padrões de busca complexos e precisos.

| Operador LIKE | Descrição |
| :--- | :--- |
| `LIKE 'a%'` | Inicia com "a" |
| `LIKE '%a'` | Finaliza com "a" |
| `LIKE '%or%'` | Contém "or" em qualquer posição |
| `LIKE '_r%'` | Possui "r" na segunda posição |
| `LIKE 'a_%_%'` | Inicia com "a" e possui pelo menos 3 caracteres |
| `LIKE 'a%o'` | Inicia com "a" e finaliza com "o" |

---

### Utilizando o Wildcard `%` (Múltiplos caracteres)

O caractere `%` é o mais utilizado quando queremos buscar partes de nomes, endereços ou descrições onde o conteúdo restante é irrelevante para a nossa filtragem. Ele representa qualquer sequência de caracteres, incluindo a ausência total deles (zero caracteres).

**Exemplo 1: Buscando cidades que iniciam com "ber"**

```sql
SELECT * FROM Customers
WHERE City LIKE 'ber%';
```

**Resultado esperado:** O banco retornará todas as linhas onde a coluna `City` comece com "ber" (ex: "Berlin", "Bern", "Bergen").

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_wildcard_percent)

**Exemplo 2: Buscando cidades que contêm "es"**

```sql
SELECT * FROM Customers
WHERE City LIKE '%es%';
```

**Resultado esperado:** O banco filtrará registros onde o termo "es" aparece em qualquer parte da string, seja no início, meio ou fim.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_wildcard_percent_pattern)

---

### Utilizando o Wildcard `_` (Caractere único)

Diferente do `%`, o `_` é restritivo. Ele exige a presença de um caractere e apenas um. É ideal para situações onde você conhece a estrutura do dado, mas não sabe o valor exato de uma posição específica.

**Exemplo 3: Padrão com posição fixa**

```sql
SELECT * FROM Customers
WHERE City LIKE '_ondon';
```

**Resultado esperado:** Retornará registros como "London". O primeiro caractere pode ser qualquer letra (como o 'L'), seguido obrigatoriamente pela sequência "ondon".

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_wildcard_underscore)

**Exemplo 4: Estrutura complexa**

```sql
SELECT * FROM Customers
WHERE City LIKE 'L_n_on';
```

**Nota:** Aqui, cada `_` atua como um "espaço reservado" obrigatório. A consulta acima busca por cidades que começam com 'L', seguidas de um caractere qualquer, o caractere 'n', outro caractere qualquer e finalizando com 'on'.

[🚀 Pratique este código](https://www.w3schools.com/mysql/trymysql.asp?filename=trysql_select_wildcard_underscore2)

<br>

---

<p align="center">
  <a href="23_MySQL_LIKE.md">⬅️ Anterior</a> | <a href="25_MySQL_IN.md">Próxima ➡️</a>
</p>

<p align="center">
  <a href="00_Sumario.md">🏠 Sumário</a>
</p>

---