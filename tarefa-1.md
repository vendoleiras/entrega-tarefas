# Apuntes DDL e DML

## Índice <a name="indice"></a>
 - [Introducción a SQL](#introduccion1)
 - [Sublenguajes SQL](#sublenguajes)
 - [DDL](#ddl)
	 - [Introducción](#introduccion2)
	 - [CREATE](#create)
	 - [ALTER](#alter)
	 - [DROP](#drop)
	 - [Tipos de datos](#tipoDatos)
	 - [Constraints o restricciones](#constraintsRestric)
- [DML](#dml)
	- [Introducción](#introduccion3)
	- [INSERT](#insert)
	- [UPDATE](#update)
	- [DELETE](#delete)
	- [SELECT](#select)
## Introducción a SQL <a name="introduccion1"></a>
El lenguaje SQL es un lenguaje de dominio específico utilizado en programación, diseñado para administrar y recuperar información de sistemas de gestión de bases de datos relacionales y pudiéndose integrar a lenguajes de programación como PHP o ASP.
Sus siglas (SQL) significan _**Structured Query Language**_.
Se suele describir como un *lenguaje declarativo* ya que a la hora de programar declaras *que* quieres hacer y no *como* lo quieres hacer.
***
## Sublenguajes SQL <a name="sublenguajes"></a>

 - **DDL Data Definition Language.**
 
 - **TCL Transaction Control Language.**
  
 - **DCL Data Control Language.**
  
 - **DML Data Manipulation Language.**
  
 - **DRL/DQL Data Retrieval Language/Data Query Language.**
   
 - **SCL Session Control Language**

## DDL

### Introducción a DDL <a name="introduccion2"></a>

**DDL** son las iniciales de "Data Definition Language", o lo que es lo mismo, *lenguaje de definición de datos*. Sirve para crear, modificar e inclusor borrar la estructura de las tablas de la propia base de datos. Sus comandos principales son `ALTER`, `DROP` y `CREATE`.

---

### CREATE
El comando **`CREATE`** nos permite crear nuevas bases de datos, tablas, objetos, etc.
>**EJEMPLO:**

- Para crear una base de datos podemos utilizar `CREATE DATABASE nombre_basedatos` o `CREATE SCHEMA nombre_basedatos`.
```SQL
CREATE DATABASE prueba;
```
- Para crear una tabla `CREATE TABLE nombre_tabla`, con la siguiente estructura
```SQL
CREATE TABLE nombre_tabla
	Columna1 TipoDato_Columna1
	Columna2 TipoDato_Columna2
```
```SQL
CREATE TABLE clase (
	nombre_Al VARCHAR(50),
	dni_Al CHAR(9)
);
```

---
### ALTER
El comando **`ALTER`** nos permite modificar los datos y la estructura de las tablas ya creadas.
```SQL
ALTER TABLE nombre_tabla
	ADD COLUMN nombre_columna tipo_columna
	DROP COLUMN nombre_columna
	etc
```
>**EJEMPLO:**
- Si queremos añadir una columna nueva usamos `ADD COLUMN`
```SQL
ALTER TABLE clase
	ADD COLUMN notas INTEGER;
```
>En caso de querer añadir o eliminar más de una columna es importante no olvidarse de las comas despues de especificar cada una de ellas.
- Si queremos eliminar una columna usamos `DROP COLUMN`
```SQL
ALTER TABLE clase
	DROP COLUMN notas;
```
- Podremos también renombrar las columnas
```SQL
ALTER TABLE clase	
	RENAME clase TO clase_nova;
```
- También podemos añadir y eliminar restricciones (`CONSTRAINTS`), pero eso lo veremos más adelante.
---
### DROP
El comando **`DROP`** nos sirve para borrar objetos dentro de la base de datos.
Podremos borrar una tabla de una base de datos o incluso una base de datos.
```SQL
DROP DATABASE nombre_base
```
```SQL
DROP TABLE nombre_tabla
```
> Si usamos `CASCADE CONSTRAINT` también eliminaremos las restricciones de integredad referencial de las tablas descendientes.
> ```SQL
>DROP TABLE nombre_tabla CASCADE CONSTRAINT;
>```
>

---
### Tipos de datos <a name="tipoDatos"></a>
Los tipos de datos más usados para la información de la columna son:
- **`INTEGER`**
- **`DECIMAL`** (preciso)
- **`REAL`** (no muy preciso)
- **`CHAR`** (con longitud fija, por ejemplo un DNI)
- **`VARCHAR`** (longitud variable)
- **`TEXT`** (no puedes poner límite de tamaño y ocupa mucho espacio)
- **`DATE`** (día, mes, año)
- **`TIME`** (hora, minutos, segundos)
- **`TIMESTAMP`** (Date + Time)
- **`BOOLEAN`** ( true (1) | false (0) )
- **`MONEY`** (dinero)
- **`JSON`**
- **`CIDR`**
- **`UUID`**
- **`INET`**
---
### Constraint o restricciones <a name="constraintsRestric"></a>
Nos sirven para especificar reglas para los datos de la tabla. Se pueden usar justo después de definir el tipo de datos, pero esto solo se podría hacer en caso de que sean casos simples y no compuestos. La mejor opción es añadirlas al final, después de haber definido todos los datos. Los más usados son:
- **`NOT NULL`** - De forma predeterminada una columna puede ser `NULL`, usamos `NOT NULL` si queremos evitar que esta columna lo sea.
- **`PRIMARY KEY`** - Las claves primarias se usan para identificar cada fila como única. Puede consistir en una o varias columnas. Siempre tiene que ser `NOT NULL`. Pueden especificarse cuando se usa `CREATE TABLE` o cuando se use `ALTER TABLE`.
 ```SQL
CREATE TABLE clase (
	nombre_Al VARCHAR(50) NOT NULL PRIMARY KEY,
	dni_Al CHAR(9)
);
```
- **`UNIQUE`** - Es muy parecida a `PRIMARY KEY`, solo que la tabla puede tener más de un `UNIQUE`. Se asegura de que todos los valores de una columna sean distintos, la usamos para limitar los parámetros los cuáles no queremos que tengan valores duplicados.
 ```SQL
CREATE TABLE clase (
	nombre_Al VARCHAR(50) NOT NULL UNIQUE,
	dni_Al CHAR(9)
);
```
- **`CHECK`** - Nos asegura que todos los valores que hay en una columna cumplan unas determinadas condiciones. Se puede aplicar más de un `CHECK` a una columna.
 ```SQL
CREATE TABLE clase (
	nombre_Al VARCHAR(50) NOT NULL,
	dni_Al CHAR(9),
	CONSTRAINT CH_comprobar
		CHECK (nombre_Al >= 0)
);
```
- **`FOREIGN KEY`** - Las claves foráneas se usan para 'linkear' dos tablas. Está formada por una columna o combinación de columnas de una tabla que sirven de enlace hacia otra tabla. Este enlace estaría formado por `PRIMARY KEY`.
 ```SQL
CREATE TABLE clase (
	nombre_Al VARCHAR(50) PRIMARY KEY,
	dni_Al CHAR(9),
	CONSTRAINT FK_dni_profesor
		FOREIGN KEY (dni_Al)
		REFERENCES departamento (dni_Al)
		ON UPDATE CASCADE
		ON DELETE CASCADE
);
```
- **`ON DELETE CASCADE`** -  Significa que si se elimina la clave primaria también se eliminan las claves secundarias. Es lo contrario a `NO ACTION`.
- **`ON UPDATE CASCADE`** - Significa que si se cambia la clave primaria también se cambian las claves secundarias. Lo contrario a `NO ACTION`.
- **`ON DELETE/ON UPDATE NO ACTION`** - Equivalente a `RESTRICT`. Si modificas/borras algo en la tabla padre no afecta a las tablas hijas que tengan información que deriva de la tabla padre.
- **`ON DELETE/ON UPDATE RESTRICT`** - Es el comportamiento predeterminado. Cualquier intento de modificar/borrar la tabla padre dará un error.
- **`ON DELETE/ON UPDATE SET NULL`** - Esto establece como `NULL` el valor de la clave secundaria que tiene relación con algo de la clave primaria.

---
[Volver al principio](#indice)

---
## DML
### Introducción a DML <a name="introduccion3"></a>

**DML** son las iniciales de "Data Manipulation Language", o lo que es lo mismo, *lenguaje de manipulación de datos*. Sirve para llevar a cabo las tareas de consulta o modificación de los datos contenidos en la propia base de datos. Sus comandos principales son `SELECT`, `INSERT`, `UPDATE` y `DELETE`.

---
### INSERT
El comando **`INSERT`** nos permite insertar valores en una base de datos, es decir, añadimos filas a una tabla. Los valores se deben insertar en el mismo orden en el que se realizó la llamada de los campos. Deben ir separados por comas. En caso de que queramos añadir un *string* este debe ir entre comillas.
>**EJEMPLO:**

 ```SQL
INSERT INTO nombre_tabla
[(<atributo_1>,<atributo_2>,...)]
(VALUES(<valor_1>,<valor_2>,...)]
;
```
 ```SQL
INSERT INTO clase (nombre_Al, dni_Al)
VALUES ('pepe','21343487T'),
	   ('luis','86785485R'),
	   ('moncho','78454545Y')
;
```
---
### UPDATE
El comando **`UPDATE`** nos sirve para modificar los valores previamente insertados. Se usa conjuntamente con `SET`. También podemos incluirlo junto con `WHERE` para modificar solo las tuplas que cumplan ciertas condiciones.
>**EJEMPLO:**

 ```SQL
UPDATE nombre_tabla
SET <atributo_1>=<valor_1>,
    <atributo_2>=<valor_2>
;
```
 ```SQL
UPDATE nombre_tabla
SET <atributo_1>=<valor_1>,
    <atributo_2>=<valor_2>
WHERE <predicado>
;
```
> La sentencia `WHERE` puede ser negada con `NOT` -> **`WHERE NOT`**
 ```SQL
UPDATE world
SET name='Francia', 
continent='Africa'
WHERE name='France'
;
```
### DELETE
El comando **`DELETE`** se utiliza para eliminar las tuplas o filas de una tabla. Si no se usa `WHERE` se borrarán todos los datos de la tabla.
>**EJEMPLO:**
 ```SQL
DELETE FROM <nombre_tabla>
;
```
> Eliminará todos los datos de <nombre_tabla>.
 ```SQL
DELETE FROM <nombre_tabla>
WHERE <predicado>
;
```
> Eliminará todos los datos de <nombre_tabla> que cumplan las condiciones del `WHERE`.
 ```SQL
DELETE FROM world
WHERE population > 1000000000
;
```
### SELECT
El comando **`SELECT`** nos sirve para realizar consultas sobre los datos. Se suele decir que forma parte del lenguaje DQL por lo que no nos centraremos mucho en él. `WHERE, GROUP BY, FROM, HAVING, ORDER BY` son unos de los muchos comandos que se suelen usar junto con `SELECT`.
 ```SQL
 SELECT nombre_Al, dni_Al 
 FROM clase
 ORDER BY fecha_Al;
```
---
[Volver al principio](#indice)

---

