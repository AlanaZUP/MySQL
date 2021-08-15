# Introdução ao MySQL

### Definições

- O `Banco de Dados` é um repositório que armazena dados que podem ser recuperados. Ele ocupa espaço em disco, sendo possível dentro do ambiente ir para um diretório específico e ver um ou mais arquivos que representam o banco de dados.

- As `Entidades` são estruturas que organizam o armazenamento do dado dentro do banco de dados. A entidade principal, entre outras, é a tabela. 

- As `Tabelas` são um conjunto de colunas e linhas. No momento em que ela é criada, é necessário as definições sobre o que ela terá.

- Os `Campos` são as coluna de uma tabela. Existem campos do tipo texto, número, campos com números com casas decimais ou números inteiros; campos do tipo lógico, ou seja, verdadeiro ou falso; campos do tipo binário, em que tenho bytes armazenados que representam, por exemplo, uma imagem, um outro arquivo com formato diferente do formato texto. Os valores do campo não podem ser de tipos diferentes

- As linhas da tabela são `Registros`. Uma tabela pode ter infinitos registros de acordo com o espaço disponível para o meu banco de dados crescer

- Na tabela temos a `Chave Primária`. Ela indica que aquele campo não pode se repetir em uma linha. A `Chave Primária Composta`, o que não pode se repetir é a combinação das duas colunas. 

- Um banco de dados pode possuir inúmeras tabelas e essas tabelas podem se relacionar. A `Chave Estrangeira` permite esse relacionamento através da chave primária.

- O `Índice` facilita achar elementos na minha tabela. Quando temos uma chave estrangeira, automaticamente o banco de dados cria índices nesses campos que se inter-relacionam.

- Dentro do banco de dados temos várias tabelas, compostas por linhas e colunas, ou campos e registros. Essas tabelas têm chaves estrangeiras, chaves primárias e podem ter índices também. Podemos associar um grupo de tabelas ao que chamamos de `Esquema`.

- `View` é um grupamento de tabelas, a view tem um comportamento igual ao de uma tabela, só que por detrás dela já tem uma consulta construída fazendo algum tipo de regra de negócio para agrupar informações, juntar coisas.

- Para buscar informações em duas ou mais tabelas, tenho que fazer uma coisa chamada `Join`, que junta as tabelas através de um critério.

- `Procedures`  é como uma linguagem nativa do banco de dados utilizando comandos de SQL que pode nos permitir fazer algum tipo de lógica estruturada, através de ifs, whiles e vários comandos de repetição. 

- Dentro das procedures, posso também ter `Funções`, cálculos que faço com os campos. O próprio banco de dados, já tem um catálogo de funções já prontas, mas é possível construir funções próprias e usá-la.

- ``Trigger`` é um aviso, um alerta que programo caso alguma coisa aconteça no banco de dados ou na tabela. Ele pode realizar um fazer um processo, que pode ser uma função, uma procedure ou um único comando SQL, que seja executado quando a condição da trigger for satisfeita.


### Comandos iniciais

Para criarmos uma Database, ou um esquema, nós usamos o sequinte comando:

```sql
CREATE {DATABASE | SCHEMA} [IF NOT EXISTS] db_name
    [create_option] ...

create_option: [DEFAULT] {
    CHARACTER SET [=] charset_name
  | COLLATE [=] collation_name
  | ENCRYPTION [=] {'Y' | 'N'}
}
```

```sql
CREATE SCHEMA orangetalents DEFAULT CHARACTER SET utf8;
```


Para deletarmos uma Database, ou um esquema, nós usamos o sequinte comando:

```sql
DROP {DATABASE | SCHEMA} [IF EXISTS] db_name
```

```sql
DROP orangetalents;
```


### Tipos de dados

- Inteiros

| Tipo | Valor em Bytes | Menor Valor - Signed| Menor Valor - Unsigned | Maior Valor - Signed| Maior Valor - Unsigned |
| ---- | :-----: | :----: | :----:  | :----: | :----:  |
| TINYINT | 1 | -128  | 0 | 127 | 255  |
| SMALLINT | 2 | -32768  | 0 | 32767 | 65535  |
| MEDIUMINT | 3 | -8388608  | 0 | 8388607 | 16777215  |
| INT | 4 | -2147483648  | 0 | 2147483647 | 4294967295  |
| BIGINT | 8 | -2xE63  | 0 | 2xE63-1 | -2xE64-1  |


- Reais:
    - FLOAT (4 bytes)
    - DOUBLE (8 bytes)

- Fixos:
    - DECIMAL ou NUMERIC (65 dígitos)


- Único:
    - BIT (64 bits)

- Atributos campos númericos:
    - SIGNED ou UNSIGNED - possuir sinal ou não no ´numero
    - ZEROFILL - Preenche com Zeros os espaços
    - AUTO_INCREMENT - sequencia auto incrementada
    * **Erro OUT OF RANGE** - quando os valores estourarem os limites  


- Data e hora:
    - DATE - 1000-01-01 até 9999-12-31
    - DATETIME - 1000-01-01 00:00:00 até 9999-12-31 23:59:59
    - TIMESTAMP - 1970-01-01 00:00:01 UTC até 2038-01-19
    - TIME - -838:59:59 e 839:59:59
    - YEAR - 1901 - 2155 (Pode ser expresso no formato 2 ou 4 dígitos)

- STRINGS:
    - CHAR - valor fixo (0 a 255), preenche com espaços
    - VARCHAR - valor variado (0 a 255)
    - BINARY - valor fixo (0 a 255) expresso em binário
    - VARBINARY - valor VARIADO (0 a 255) expresso em binário
    - BLOB - binário longo:
        - TINYBLOB
        - BLOB
        - MEDIUMBLOB
        - LONGBLOB
    - TEXT - texto longo:
        - TINYTEXT
        - TEXT
        - MEDIUMTEXT
        - LONGTEXT
    - ENUM - armazena lista pré-definida de valores

- Atributos campos Strings:
    - SET e COLLATE - conjunto de caracteres que são suportados

- SPACIAL:
    - GEOMETRY
    - POINT
    - LINESTRING
    - POLYGON


### Criando tabelas

```sql
CREATE TABLE name_table(
    CPF VARCHAR(11),
    NOME VARCHAR(100),
    ENDERECO1 VARCHAR(150),
    ENDERECO2 VARCHAR(150),
    BAIRRO VARCHAR(50),
    CIDADE VARCHAR(50),
    ESTADO VARCHAR(50),
    CEP VARCHAR(8),
    IDADE SMALLINT UNSIGNED,
    SEXO VARCHAR(1),
    LIMITE_CREDITO FLOAT,
    VOLUME_COMPRA FLOAT,
    PRIMEIRA_COMPRA BIT(1)
    )
```

```sql
CREATE TABLE TABELA_DE_VENDEDORAS(
    MATRICULA VARCHAR(5),
    NOME VARCHAR(100),
    PERCENTUAL_COMISSAO FLOAT
    )
```

### Apagando tabelas

```sql
DROP TABLE database.name_table
```

### Inserindo registros

```sql
USE database;

INSERT INTO name_table(nome_campo1, nome_campo2, nome_campo3) VALUES (valor_campo1, valor_campo2, valor_campo3)

```

### Alterando registros

```sql
USE database;

UPDATE name_table SET nome_campo1 = 'valor_correto' WHERE nome_campoID = 'identificação
```

### Excluindo registros

```sql
USE database;

DELETE FROM name_table WHERE nome_campoID = 'identificação
```


### Incluindo chave primária

```sql
USE database;

ALTER TABLE name_table ADD PRIMARY KEY (nome_campo);
```


### Incluindo colunas

```sql
USE database;

ALTER TABLE name_table ADD COLUMN (nome_campo TIPO_CAMPO);
```



### Seleção de dados

```sql
USE database;

SELECT * FROM name_table;

SELECT campo1, campo3, campo2 FROM name_table;

SELECT campo3 AS CAMPO3, campo2 AS ALEATORIO FROM name_table LIMIT 10;

SELECT * FROM name_table WHERE campo1 = condicao;

SELECT * FROM name_table WHERE campo1 <= condicao;

SELECT * FROM name_table WHERE campo1 >= condicao;

SELECT * FROM name_table WHERE campo1 <> condicao;

SELECT * FROM name_table WHERE campo1 BETWEEN condicao1 AND condicao2;

SELECT * FROM name_table WHERE YEAR(campo_date) = year;

SELECT * FROM name_table WHERE MONTH(campo_date) = month;

SELECT * FROM name_table WHERE campo1 OR campo2 ;
```








