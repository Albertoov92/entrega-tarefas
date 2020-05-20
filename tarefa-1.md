# Data Definition Language
## Índice
  - [Detalles importantes](#detalles-importantes)
  - [O sublinguaxe DDL](#o-sublinguaxe-ddl)
    - [```CREATE```](#create)
      - [```CREATE (DATABASE|SCHEMA)```](#create-(databse|schema))

### Detalles importantes
  > Cando algo esta entre ```[]``` é opcional.    
  > Cando hai unha ```|``` significa OU.    
  > Recomendase evitar o uso de acentos e espazos nas expresións.

### O sublinguaxe DDL
O sublinguaxe SQL é usado para crear bases de datos, táboas, usuarios ou dominios. Tamén nos permite engadir atributos cun tipos de datos definidos, establecer restricións e establecer criterios nas táboas interrelacionadas. Chámase DDL porque significa linguaxe de definición de datos.

### ```CREATE```
- #### ```CREATE (DATABASE|SCHEMA)```
  Ambos dous teñen a mesma función, declarar a Base de Datos na que engadiremos as táboas, datos e restricións.
  Anque dependendo do xestor utilizado pode variar a función de cada un. En MySQL podemos usar os dous indistintamente. Sen embargo en PostgreSQL. ```ESCHEMA``` é usado como unha capa intermedia entre ```DATABASE``` e as táboas que a compoñen.  

    **FÓRMULA**
  ```SQL
  Create (DATABASE|SCHEMA)
         [IF NOT EXISTS] <nomeBD>
         [CHARACTER SET <nomeDoCharset>]
  ;
  ```
    > Con ```IF NOT EXISTS``` evitamos crear dúas bases de datos co mesmo nome.   
    >Con ```CHARACTER SET``` indicamos o CharSet que queremos usar, como UTF-8.

- #### ```CREATE DOMAIN```
Crearemos un dominio cando teñamos que repetir varias veces nunha BD o mesmo tipo de datos en distintos atributos. Ademais en caso de que tivésemos que modificalo, resulta moito mais sinxelo que ir atributo por atributo.

  **FÓRMULA**
  ```SQL
  CREATE DOMAIN <nomeDoDominio> <tipoDeDato>
                [NOT NULL]
                [CHECK (restrición)]
  ;
  ```
  **Parámetros opcionais**

    > Engadimos ```NOT NULL```  a fórmula se queremos evitar os valores nulos.     
    > Usaremos  ```CHECK``` cando precisemos engadir restricións.

- #### ```CREATE TABLE```
Para crear táboas usaremos a seguinte formula.
```SQL
CREATE TABLE [IF NOT EXISTS] <nomeDaTaboa> (
	     <nomeDoAtributo1> <tipoDeDato> [PRIMARY KEY],
	     <nomeDoAtributoN> <dominioN>   [DEFAULT <'expresion'>] [NOT NULL] [UNIQUE],

);
```
# Apuntes del sublenguaje DML
## Índice
  - [Sentencias DML](#Sentencias-DML)
    - [INSERT](#INSERT)
    - [UPDATE](#UPDATE)
    - [DELETE](#DELETE)

  ## Sentencias DML
  Na linguaxe SQL hai 3 instrucións que compoñen o DML (* Data Manipulation Language*). Son aquelas frases que nos permiten manipular a información que almacenamos nas bases de datos.

  Existen 3 instrucións que nos permitirán inserir datos nunha táboa **(INSERT)** , modificar eses datos **(UPDATE)** e borralos **(DELETE)**.

  ### INSERT
A instrución **INSERT** permite engadir datos a unha táboa.

**FORMULA**
```sql
INSERT INTO <nombreDeLaTabla>
  (<atributo1>[, <atributo2>, <atributo3>...])
  VALUES (
  (<valor1>[, <valor2>, <valor3>...])
  ) || (
  SELECT <atributoX> FROM <tablaX> ...);
```

**EXEMPLO**
```sql
  INSERT INTO world
  [(name, continent, area)]
  VALUES
  ('SPAIN', 'EUROPE', 100),
  ('PORTUGAL','EUROPE', 10);
```
Como podemos observar na sentencia anterior engadimos dúas tuplas con os valores especificados en **VALUES**, como podemos observar podemos engadir máis de una tupla a vez sempre que sepáresmos as tuplas por coma.

   **Nota** : Os  valores numéricos non van entre comillas.

### UPDATE
A instrución **UPDATE** permite modificar datos.

**FORMULA**
```sql
UPDATE <nombreDeLaTabla>
SET <atributo1> = <valor1>,
    <atrubuto2> = <valor2>,
    ...3

    <atributoN> = <valorN>
[WHERE <predicado>];
```
**Nota** El WHERE es opcional

**EXEMPLO**
```sql
UPDATE world
SET continent = 'ASIA'
WHERE name = 'SPAIN'
OR name = 'PORTUGAL'
```
No  exemplo anterior engadimos  a tupla Spain e Portugal o novo valor de continente que seria Asia. Se non establecemos o WHERE modificaríanse todos os continentes de todas as tuplas.
### DELETE
A instrución **DELETE** serve para eliminar valores de algunhas tuplas ou hasta bases de datos.

**FORMULA**
```SQL
DELETE FROM <nombreDeLaTabla>
  WHERE <predicado>;
```
**Nota**: Se non utilizamos o WHERE eliminiaremos toda a taboa.

**EXEMPLO**
```SQL
DELETE FROM world
  WHERE continent = 'EUROPE';
```
No exemplo, eliminamos todas as tuplas que conteñan o valor de continente igual  a EUROPE.


