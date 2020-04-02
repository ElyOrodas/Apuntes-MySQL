# Apuntes de los sublenguajes DDL y DML

## Índice

* [DDL (Definición y ejemplo)](#DDL)
   * [Sentecias DDL](#Sentencias-DDL) 
* [DML (Definición y ejemplo)]
* [Tabla definición de tipo de dato y CONSTRAINTS]
    * [Tipo de dato]
    * [CONSTRAINTS]
* [DBMS]

### DDL

*Definición* : sus siglas (Data Definition Language, DDL) significan Lenguaje de Definición de Datos,
               este lenguaje se encarga de la modificación de la estructura de los objetos de la base
               de datos. Incluye órdenes para modificar, borrar o definir las tablas en las que se 
               almacenan los datos de la base de datos. 

#### Sentencias DDL

* **CREATE | CREAR**
- Permite crear objetos de datos, como nuevas bases de datos, tablas, vistas y procedimientos almacenados.
- Este comando admite por lo menos cinco predicados:
      - DATABASE: creación de una base de datos, sin ella no se podrán                     crear tablas, ni dominios, ni usuarios...
      - SCHEMA: creación de un esquema, se parece a una tabla pero más                    extenso, describendo su estructura y organización de                       datos.
 
      * Ejemplo (crear una tabla):
      ```sql 
            CREATE TABLE 'CUSTOMERS ';
      ```      
