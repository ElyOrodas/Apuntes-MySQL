# Apuntes de los sublenguajes DDL y DML

## Índice

* [DDL (Definición y ejemplos)](#DDL)
   * [Sentecias DDL](#Sentencias-DDL) 
* [DML (Definición y ejemplo)](#DML)
   * [Sentencias DML](#Sentencias-DML)
* [Tipos de Datos](Tipos-de-Datos)
* [CONSTRAINTS]
* [DBMS]

### DDL

*Definición* : sus siglas (Data Definition Language, DDL) significan Lenguaje de Definición de Datos,
               este lenguaje se encarga de la modificación de la estructura de los objetos de la base
               de datos. Incluye órdenes para modificar, borrar o definir las tablas en las que se 
               almacenan los datos de la base de datos. 

#### Sentencias DDL

* **CREATE | CREAR**
  * Permite crear objetos de datos, como nuevas bases de datos, tablas, vistas y procedimientos almacenados.
  * Este comando admite por lo menos cinco predicados:
      - DATABASE: creación de una base de datos, sin ella no se podrán                     crear tablas, ni dominios, ni usuarios...
      - SCHEMA: creación de un esquema, se parece a una tabla pero más                    extenso, describendo su estructura y organización de                       datos.
      - TABLE: creación de una entidad (una tabla con filas y columnas)
      - USER: creación de usuario para que realice consultas a la base de               datos
      - DOMAIN: creación de un dominio, que es un tipo de datos                           CONSTRAINST (con restricciones opcionales)
      
   * Ejemplo (crear una tabla):
      ```sql 
            CREATE DATABASE "Nombre_BD";
      ```      
      ```sql
            CREATE TABLE "nombre_tabla" ("primera_columna" tipoDato Restricciones,
                                         "segunda_columna" tipoDato Restricciones, 
                                        etc);
      ```
* **ALTER | MODIFICAR**
  * Permite modificar la estructura de una tabla u objeto. Se pueden agregar/quitar campos a una tabla, modificar el tipo de campo, agregar/quitar índices a una tabla, modificar un trigger o disparador, etc.
  * Ejemplo (agregar columna a una tabla)
    ```sql
          ALTER TABLE "nombre_tabla" ADD "nombre_columna";
    ```
    
* **DROP | ELIMINAR**
  * Permite eliminar un objeto de la base de datos. Puede ser una tabla, vista, índice, trigger, función, procedimiento o cualquier objeto que el motor de la base de datos soporte. Se puede commbinar con la sentencia ALTER.
  * Ejemplo (eliminar columna)
  ```sql
        ALTER TABLE "nombre_tabla"
        DROP COLUMN "nombre_columna";
  ```
  
* **TRUNCATE | BORRAR TABLA**  
    * Permite truncar todo el contenido de una tabla, borra la tabla y la vuelve a crear y no ejecuta ninguna transacción.
    * La *ventaja* sobre el comando DROP, es que si se quiere borrar todo el contenido de la tabla, es mucho más rápido, especialmente si la tabla es muy grande.
    * La *desventaja* es que TRUNCATE sólo sirve cuando se quiere eliminar absolutamente todos los registros, ya que no se permite la cláusula WHERE.  
    * Ejemplo 
      ```sql
            DROP TABLE "nombre_tabla"
      ```

### DML

*Definición*: sus siglas (Data Manipulation Language, DML) significa lenguaje de manipulación de datos, es un lenguaje proporcionado por el sistema de gestión de base de datos que permite a los usuarios llevar a cabo las tareas de consulta o manipulación de datos (almacenarlos, modificarlos, instertarlos o actualizarlos), organizados por el modelo de datos adecuado. Al conjunto de instrucciones DML que se ejecutan consecutivamente, se le llama *transacción*. 

### Sentencias DML

* **SELECT | SELECCIONAR**
    * Utilizado para consultar registros de la  base de datos que satisfagan un criterio determinado. Esta sentencia se utiliza principalmente para la recuperación de datos específicos de una tabla. 
    * Ejemplos:
      1. Seleccionar alguna columna específica:
      ```sql
            SELECT nombre_columna FROM tabla;
      ```
      2. Seleccionar todas las columnas:
      ```sql
            SELECT * FROM tabla;
      ```
      
* **INSERT | INSERTAR**
    * Utilizado para carga de datos en una base de datos en una única operación. Esta sentencia agrega uno o más registros a uno (y sólo una) tabla en una base de datos relacioanl. 
    * Se puede insertar nuevas filas en una tabla con la instrucción INSERT INTO.
    * Para guardar los datos insertados hay que ejecutar *COMMIT* y para cancelar la insercción hay que ejecutar *ROLLBACK*.
    * El orden en que se asignen los valores en la cláusula *VALUES* tiene que coincidir con el orden en que se definieron las columnas en la creaciónn del objeto tabla, dado que los valores se asignan por posicionamiento relativo.
    * Es necesario que por lo menos se asginen valores a todas aquellas columnas que no admiten valores nulos en la tabla (NOT NULL)
    * Formato posible:
    ```sql
          INSERT INTO nombre_tabla
          VALUES (serie de valores);
    ```
    * Ejemplos:
    ```sql
          INSERT INTO tabla_pedidos
          VALUES (125,2,'Pedro');
    ```
    ```sql
          INSERT INTO nombre_tabla (columna1, columna2,.....)
          VALUES (valor1, valor2,.....);
    ```
    
* **UPDATE | ACTUALIZAR**
    * Utilizado para modificar los valores de los campos y registros especificados en una tabla.
    * Se pueden modificar valores de un registro con la instrucción `UPDATE tabla SET`.
    * Ejemplo (modificar el nombre del prducto que tenga como código un 2)
    ```sql
          UPDATE producto SET nombre= ' Pelota'
          WHERE id_producto = 2;      
    ```
    
* **DELETE | ELIMINAR** 
    * Utilizado para eliminar registros de una tabla de una base de datos.
    * Puede eliminar uno o más registros existentes en una tabla, dependiendo de la condición WHERE
    * Para guardar los cambios hay que ejecutar *COMMIT* y para cancelar el borrado  hay que ejecutar *ROLLBACK*.
    * Si no se pone la condición de selección, borra todas las filas de la tabla, así que hay que tener mucho cuidado.
    * La sintaxis es la siguiente:
        ```sql
            DELETE FROM nombre_tabla
            [WHERE condición];
        ```
    * Ejemplos:
      1. Borrar toda la tabla:
          ```sql 
               DELETE FROM tabla_pedidos;
          ```
      2. Borrar sólo un registro:
           ```sql
                DELETE FROM tabla_ pedidos
                WHERE id_pedido=15;  
           ```
    
### Tipos de Datos

**Nota**: RDBMS, significa sistema de gestión de bases de datos relacionales 

* **Numéricos**
    * Exactos:
         * Enteros, según el RDBMS: SMALLINT, INTEGER.
         * Con precisión y escala, según el RDBMS: NUMERIC(X,Y) O NUMBER(X,Y).
    * Aproximados
      * De punto flotante, según el RDBMS: REAL/DOUBLE.
