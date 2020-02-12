# Apuntes-MySQL

## Índice

- [Reglas de sintaxis](#reglas-de-sintaxis)
- [Explicación de las Sentencias y sus ejemplos](#explicación-de-las-sentencias-y-sus-ejemplos)
- [SELECT y ejemplo para estructura básica](#SELECT-y-ejemplo-como-estructura-básica)
- [IN y ejemplo](#IN-y-ejemplo)
- [AS y ejemplo](#AS-y-ejemplo)
- [BETWEEN y ejemplo](#BETWEEN-y-ejemplo)
- [ORDER BY y ejemplo](#ORDER-BY-y-ejemplo)
- [LIKE y ejemplos](#LIKE-y-ejemplos)
- [REPLACE y ejemplo](#REPLACE-y-ejemplo)
- [ROUND y ejemplo](#ROUND-y-ejemplo)
- [LENGTH y ejemplo](#LENGTH-y-ejemplo)
- [(LEFT y RIGHT) y ejemplo](#(-LEFT-y-RIGHT-)-y-ejemplo)
- [CONCAT y ejemplo](#CONCAT-y-ejemplo)
- [(SUM y COUNT) y ejemplos](#(-SUM-y-COUNT-)-y-ejemplos)
- [(MAX Y MIN) y ejemplo](#(-MAX-y-MIN-)-y-ejemplo)
- [AVG y ejemplo](#AVG-y-ejemplo)
- [GROUP BY y ejemplo](#GROUP BY-y-ejemplo)
- [HAVING y ejemplo](#HAVING-y-ejemplo)
- [JOIN y ejemplo](#JOIN-y-ejemplo)
- [INNER JOIN y ejemplo](#INNER-JOIN-y-ejemplo)
- [LEFT JOIN y ejemplo](#LEFT-JOIN-y-ejemplo)
- [RIGHT JOIN y ejemplo](#RIGHT-JOIN-y-ejemplo)

## Reglas de sintaxis

1. Es una práctica común escribir todos los comandos/sentencias SQL en **mayúsculas** (es decir: SELECT, JOIN, AVG, etc)
2. Al finalizar cada declaración SQL, se debe colocar un **punto y coma** para indicar que la declaración está completay lista para ser interpretada
3. En SQL, el asterisco (*****), significa todos(as)
4. Los strings deben ir entre comillas **('____')**, pero deben ser las simples
5. Los comentarios de una línea, se deben hacer: **-comentario-**
6. Al realizar comentarios multilínea, debemos utilizar barras y asteriscos de esta forma: **/*comentario*/**

## Explicación de las Sentencias y sus ejemplos

### SELECT y ejemplo como estructura básica
Es utilizada para seleccionar datos de una base de datos. El resultado es almacenado en una tabla resultante (también llamada: conjunto resultante)
**Ejemplo**
```sql
      SELECT NombreObjeto
      FROM NombreTabla
      WHERE condición;
```
***Nota***

***WHERE***: es utilizada pra extraer sólo los registros que cumplen con un criterio específico 
En esta se usan algunos operadores lógicos que pueden ser utilizados para combinar dos valores para obtener el resultado deseado, estos son:
- ***=***: igual
- ***!=***: no igual
- ***>***: mayor que
- ***<***: menor que
- ***>=***: mayor igual que
- ***<=***: menor igual que

***AND***: si se desea seleccionar filas que satisfagan las condiciones dada, debemos usar este operador lógico
Ejemplo:
Necesitamos encontrar nombres (name) de una tabla "customers" entre 30 y 40 años de edad (columna: age)
```sql
      SELECT name
      FROM customers
      WHERE age >= 30 AND age <= 40
```

***OR***: si se desea seleccionar filas que satisfagan al menos una de las condiciones, podemos usar este operador lógico
Ejemplo:
Necesitamos encontrar todos los registros de la tabla "customers" cuya ciudad esta registrada en la columna "City" es igual a "New York" o "Chicago"
```sql
      SELECT *
      FROM customers
      WHERE City='New York' OR City='Chicago';
```

### IN y ejemplo
Este operador es utilizado cuando se quiere comparar una columna con más de un valor 
***Ejemplo***
Necesitamos seleccionar todos los registros de la tabla "customers" con "New York", "Los Angeles", "Chicago" de la columna "City"
```sql 
      SELECT *
      FROM customers
      WHERE City IN ('New York','Los Angeles','Chicago');
```
***Nota***: también podría usarse OR pero de esta forma resumimos

***NOT IN***: Permite excluir una lista de valores específicos del conjunto resultado. Es decir, en el ejemplo anterior si utilizamos este operador, la tabla no tendría los valores que se piden

### AS y ejemplo
Se utiliza para que la tabla resultado tenga un nombre determinado por el usuario
***Ejemplo***
Necesitamos los nombres de los empleados (name) de la tabla "customers" que se demuestren en una tabla resultado llamada "NombreEmpleados"
```sql
      SELECT name AS NombreEmpleados
      FROM customers ;
```

### BETWEEN y ejemplo   
Selecciona valores dentro de un rango. El primer valor debe ser el límite menos y el segundo valor es el límite superior
***Ejemplo***
Necesitamos todos los registros con la identificación (ID) de la tabla "customers" que están entre 3 y 7:
```sql
      SELECT *
      FROM customers
      WHERE ID BETWEEN 3 AND 7;
```

### ORDER BY y ejemplo
Es utilizado con SELECT para ordenar los datos recuperador, por defecto ordena los resultados en orden ascendente (ASC), si queremos descendente debemos poner DESC 
***Ejemplo***
Necesitamos ordenar la tabla "customers" por la columna "name" en orden descendente
```sql
      SELECT * 
      FROM customers
      ORDER BY name DESC;
```

### LIKE y ejemplos
Es útil cuando especificas una condición de búsqueda dentro de WHERE. El emparejado de patrones SQL te permite utilizar "_" para coinicir con cualquier carácter único y "%" para coinicidir con un número arbitrario de caracteres.
***Ejemplos***
Necesitamos seleccionar empleados de la tabla "employees" cuyos registros en la columna "name", comience con la letra "A" 
```sql
      SELECT *
      FROM employees
      WHERE name LIKE 'A%';
```
Necesitamos seleccionar empleados de la tabla "employees" cuyos registros en la columna "name", terminen con la letra "s"
```sql
      SELECT *
      FROM employees
      WHERE name LIKE '%s';
```
***Nota:*** El comodín ***%*** puede ser utilizado varias veces dentro del mismo patrón

### REPLACE y ejemplo
Sirve  para reemplaza caracteres determinados por un atributo
***Ejemplo***
Necesitamos seleccionar la capital que tiene de nombre de la capital (capital) "DF" de la tabla "countries", para sustituirlo por "Distrito Federal"
```sql
      SELECT capital
        REPLACE (capital. 'DF','Distrito Federal')
      FROM countries
      WHERE name LIKE '%_DF';
```

### ROUND y ejemplo 
Se utiliza para seleccionar un atributo y redondearlo a cierto número con una cantidad "x" de decimales
***Ejemplo***
Necesitamos el nombre de los países de África y que posean una población en millones con 6 decimales de redondeo 
```sql
      SELECT name, ROUND(population/1000000,3) 
      FROM world
      WHERE continent = 'Africa';
```      

### LENGTH y ejemplo
Se utiliza para devolver el número de letras que tiene la palabra del atributo "x"
***Ejemplo***
Necesitamos seleccionar todos los países (countries) y que se reduzca los nombres a las tres primeras letras del nombre del país
```sql 
      SELECT countries, LENGHT(countries,3)
      FROM world;
``` 

### (LEFT y RIGHT) y ejemplo
- LEFT(x, n): Se usa para recoger los primeros "n" carácteres del atributo "x".  
- RIGHT(x, n): Tiene la misma función que LEFT pero comenzando por la derecha.  
***Ejemplo***
Necesitamos todos los países con una población superior a 200000000 *(200 millones)* y asígnarles una abreviatura que sean las tres primeras letras del nombre del país.  
```sql
      SELECT name, LEFT(name, 3)
      FROM world
      WHERE population >= 200000000;
```
### CONCAT y ejemplo
Esta es una función que se utiliza para concatenar (unir) dos o más valores de texto y retorna la cadena de texto concatenada, puede tomar dos o más parámetros
***Ejemplo***
Necesitamos concatenar la columna "name" y "City", separadas por coma de la tabla "customers"
```sql
      SELECT CONCAT(name,',',City)
      FROM customers ;     
```

### (SUM y COUNT) y ejemplos
- SUM: es utilizada esta función para calcular la suma de los valores de una columna
***Ejemplo***
Necesitamos obtener la suma de los salarios de la tabla empleados
```sql 
       SELECT SUM(salario)
       FROM empleados
```       
- COUNT: es utilizada para contar el número de tuplas que existen
***Ejemplo***
Necesitamos contar todos los países (countries) de Europa de la tabla world 
```sql 
      SELECT COUNT(countries)
      FROM world
      WHERE continent = 'Europa';
```     
### (MAX y MIN) y ejemplo)   
- MIN: es una función que se utiliza para retornar el valor mínimo de una expresión en una declaración SELECT
- MAX: es una función que se utiliza para retornar el valor máximo de una expresión en una declaración SELECT
***Ejemplo***
Necesitamos saber el salario mínimo entre empleados 
```sql
      SELECT MIN(salario)
      FROM empleados
```      



