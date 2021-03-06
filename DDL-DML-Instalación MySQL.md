# Apuntes de los sublenguajes DDL y DML

## Índice

* [DDL (Definición y ejemplos)](#DDL)
   * [Sentecias DDL](#Sentencias-DDL) 
* [DML (Definición y ejemplo)](#DML)
   * [Sentencias DML](#Sentencias-DML)
* [Tipos de Datos](#Tipos-de-Datos)
* [Constraints](#Constraints)
* [MySQL](#MySQL)

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
      
* **Texto**
    * De largo fijo
      * CHAR(N), los caracteres no usados a la derecha se rellenan con espacios en blanco
    * De largo variable
      * VARCHAR(N), se mantienen el largo en un entero
    * Los caracteres deben ser parte del juego de caracteres de la base (UNICODE es un juego de caracteres que sopota internacionalización)

* **Booleanos**
    * No todos los RDBMS lo soportan 
    
* **Fecha y hora**
    * DATE: año, mes y día
    * TIME: hora, minuto y segundo
    * TIMESTAMP: DATE + TIME
    
    * El formato dependerá de la configuración del "National Language"
    
* **Objetos grandes**
    * CLOB: Character Long Object
      * Permite almacenar textos muy grandes, que superen los límites de VARCHAR
      * Los caracteres deben ser parte del juego de caracteres de la base
    
    * BLOP: Binary Long Object
      * Permite almacenar archivos binarios, como imágenes o documentos 

* Todos los tipos de datos aceptan el valor NULL
* Los límites dependen de la implementación, por lo que varían de un RDBMS a otro
* El tipo de datos de una columna debe permitir almacenar todos los valores previstos, pero usar un tipo demasiado grande puede desperdiciar espacio y limitar el desempeño (no usar TIMESTAMP si alcanza con DATE, no usar CLOB si alcanza con VARCHAR, etc)

### Constraints (restricciones)

* **Clave Primaria (Primary Key, PK)**
    * • Sólo una de las columnas puede ser definida como PK de esta forma (sólo sirve para claves por una única columna)
    * Cuando estamos creando o añadiendo una columa: `columna tipo ... [CONSTRAINT nombre] PRIMARY KEY`
    * Al final de la lista de columnas `[CONSTRAINT nombre] PRIMARY KEY (listaColumnas)`
    * Ejemplo
    ```sql
          CREATE TABLE movimientos( cod_persona NUMBER(10),
                                    fecha TIMESTAMP,
                                    importe NUMBER(11,4),
          CONSTRAINT movimientos_pk PRIMARY KEY(cod_persona,fecha));
    ```
    
* **Unicidad (Unique)**    
    * Se definen de la misma forma que una Primary Key, simplemente cambiando PRIMARY KEY por UNIQUE

    * Cuando estamos creando o añadiendo una columna:`columna tipo ... [CONSTRAINT nombre] UNIQUE`
    * Al final de la lista de columnas [CONSTRAINT nombre] UNIQUE(listaColumnas)

* **Clave Fornánea (Foreign Key )**
    * Se definen de forma parecida a una PK o UK mediante ALTER TABLE
      `CREATE TABLE tabla1 (columna_1 tipo_dato_1 [NOT NULL],columna_2 tipo_dato_2 [NOT NULL],... columna_n tipo_dato_n [NOT NULL] );`
      
      ```sql 
            ALTER TABLE tabla1
            ADD CONSTRAINT FK_tabla1_tabla2
            FOREIGN KEY (columna_1) references tabla2(columna_1);
      ```

* **Obligatoriedad**
    * Solo cuando estamos creando tablas o añadiendo una columa: `columna tipo ... [CONSTRAINT nombre] NOT NULL`

* **Integridad referencial**
    * Cuando estamos creando tablas o añadiendo una columna:` columna tipo … [CONSTRAINT nombre] REFERENCES tablaPrincipal[(columnas)] [ON DELETE CASCADE|SET NULL]`
  * Al final de la lista de columnas `[CONSTRAINT nombre] FOREIGN KEY(columnas) REFERENCES tablaPrincipal(columnas) [ON DELETE CASCADE|SET NULL]`
  
* **Validación(CHECK)**
    * Cuando estamos creando o añadiendo una columna: `columna tipo … [CONSTRAINT nombre] CHECK(condición)`
    * Al final de la lista de columnas `[CONSTRAINT nombre] CHECK(condición)`
    * Se pueden definir inline o a través de ALTER TABLE
        `CREATE TABLE tabla1 (columna_1 tipo_dato_1 [NOT NULL],columna_2 tipo_dato_2 [NOT NULL],... columna_n tipo_dato_n [NOT NULL]);`
                                
         ```sql 
            ALTER TABLE tabla1
            ADD CONSTRAINT check_columna_1_tabla1
            CHECK (columna_1 in ('V1', 'V2', ..., 'Vn'));
         ```

### MySQL

Descargamos desde su web a una máquina virtual y seguimos los pasos como se demuestran a continuación. Mayormente en todas las ventanas se clica en ejecutar o finalizar.

![1](https://github.com/ElyOrodas/Apuntes-MySQL/blob/master/Install%20MySQL/1.PNG)

![2](https://github.com/ElyOrodas/Apuntes-MySQL/blob/master/Install%20MySQL/2.PNG)

![3](https://github.com/ElyOrodas/Apuntes-MySQL/blob/master/Install%20MySQL/3.PNG)

![4](https://github.com/ElyOrodas/Apuntes-MySQL/blob/master/Install%20MySQL/4.PNG)

![5](https://github.com/ElyOrodas/Apuntes-MySQL/blob/master/Install%20MySQL/5.PNG)

![6](https://github.com/ElyOrodas/Apuntes-MySQL/blob/master/Install%20MySQL/6.PNG)

![7](https://github.com/ElyOrodas/Apuntes-MySQL/blob/master/Install%20MySQL/7.PNG)

![8](https://github.com/ElyOrodas/Apuntes-MySQL/blob/master/Install%20MySQL/8.PNG)

![9](https://github.com/ElyOrodas/Apuntes-MySQL/blob/master/Install%20MySQL/9.PNG)

![10](https://github.com/ElyOrodas/Apuntes-MySQL/blob/master/Install%20MySQL/10.PNG)

![11](https://github.com/ElyOrodas/Apuntes-MySQL/blob/master/Install%20MySQL/11.PNG)

![12](https://github.com/ElyOrodas/Apuntes-MySQL/blob/master/Install%20MySQL/12.PNG)

![13](https://github.com/ElyOrodas/Apuntes-MySQL/blob/master/Install%20MySQL/13.PNG)

![14](https://github.com/ElyOrodas/Apuntes-MySQL/blob/master/Install%20MySQL/14.PNG)
