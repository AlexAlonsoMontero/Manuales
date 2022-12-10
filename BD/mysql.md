# MY SQL

- Conetar al servidor

```bash
mysql -h nombre_servidor -u nombre_usuario -p
```

- Crear base de datos:

```sql
create database miprueba;
```

- Listar bases de datos

```sql

show databases;
```

- Seleccionar base de datos para trabajar con ella

```sql
use miprueba;
```

- Mostrar tablas

```sql
show tables;
```

<hr>

## USUARIOS

- Crear usuario:

  - Con permiso para acceder en local, sin permisos al crearse.

```sql
CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'password';
```

- Crear usuario que se pueda conectar desde otra ip:
  - Despues del arroba ponemos la ip desde la que se puede conectar o % para que sea cualquier ip

```sql
CREATE USER 'newuser'@'ip o %' IDENTIFIED BY 'password';
```

- Modificar un usuario para que se pueda conectar en remoto:

```sql
RENAME USER 'pym'@'localhost' TO 'pym'@'ip_servidor_remoto';
```

- Proporcionar permisos al usuario, los \* se refieren a la base de datos y tabla, Este comando específico permite al usuario leer, editar, ejecutar y realizar todas las tareas en todas las bases de datos y tablas

```sql
GRANT ALL PRIVILEGES ON * . * TO 'newuser'@'localhost';
```

- Una vez que haya finalizado los permisos que desea configurar para sus nuevos usuarios, asegúrese siempre de volver a cargar todos los privilegios

```sql
FLUSH PRIVILEGES;
```

### Permisos de usuarios:

- ALL PRIVILEGES: Como vimos antes, esto le otorgaría a un usuario de MySQL acceso completo a una base de datos designada (o si no se selecciona ninguna base de datos, acceso global a todo el sistema).
- CREATE: Permite crear nuevas tablas o bases de datos.
- DROP: Permite eliminar tablas o bases de datos.
- DELETE: Permite eliminar filas de las tablas.
- INSERT: Permite insertar filas en las tablas.
- SELECT: Les permite usar el comando SELECT para leer las bases de datos.
- UPDATE: Permite actualizar las filas de las tablas.
  GRANT OPTION: Permite otorgar o eliminar privilegios de otros usuarios

- Ejemplo dar permisos a un usuario concreto:

```sql
GRANT type_of_permission ON database_name.table_name TO 'username'@'localhost';
```

- Revoca un permiso.

```sql
REVOKE type_of_permission ON database_name.table_name FROM 'username'@'localhost';
```

- Revisar los permisos de un ususario:

```sql
SHOW GRANTS FOR 'username'@'localhost';
```

- Borrar un usuario:

```sql
GRANT type_of_permission ON database_name.table_name TO 'username'@'localhost';
```

<hr>

## TABLAS

### CREACIÓN DE TABLAS

- Ejemplo de dos tablas relacionadas entre si, con distintos tipos de datos y distintas características como permitir un campo null, no permitirlo...

```sql
CREATE TABLE usuarios(
	id_usuario INT UNSIGNED NOT NULL AUTO_INCREMENT,
	username VARCHAR(64) NOT NULL,
	password VARCHAR(64) NOT NULL,
	email VARCHAR(256) NOT NULL,
	tipo ENUM ('INQUILINO','CASERO','INQUILINO/CASERO','ADMINISTRADOR'),
	activated_at TIMESTAMP DEFAULT NULL,
	activated_code VARCHAR(64) DEFAULT NULL,
	avatar VARCHAR(256) NOT NULL,
	nombre VARCHAR(256) NOT NULL,
	apellidos VARCHAR(512) NOT NULL,
	telefono VARCHAR(12) NOT NULL,
    deleted BOOLEAN DEFAULT FALSE,
    deleted_date TIMESTAMP DEFAULT NULL,

	CONSTRAINT UNIQUE KEY UK_usuarios_username (username),
    CONSTRAINT UNIQUE KEY UK_usuarios_email (email),
    CONSTRAINT PK_usuarios PRIMARY KEY(id_usuario)

);

CREATE TABLE inmuebles (
	id_inmueble INT UNSIGNED NOT NULL AUTO_INCREMENT,
    fk_usuario  INT UNSIGNED NOT NULL,
    precio FLOAT(8,2) NOT NULL,
    dipnibilidad ENUM ('MENSUAL', 'ANUAL', 'MENSUAL/ANUAL') DEFAULT 'MENSUAL',
	tipo_via ENUM ('CALLE','AVENIDA','CAMINO','CARRETERA','OTROS') DEFAULT 'OTROS',
	fecha_alta TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
	tipo_inmueble ENUM ('PISO','ESTUDIO','CASA','ADOSADO','OTROS'),
	lng DECIMAL(9,6) DEFAULT 0,
    lat DECIMAL(9,6) DEFAULT 0,
    metros_2 SMALLINT DEFAULT 0,
    calle VARCHAR(256) NOT NULL,
    numero VARCHAR (16),
    piso VARCHAR (16),
    ciudad VARCHAR(128) NOT NULL,
    provincia VARCHAR(128) NOT NULL,
    comunidad VARCHAR(128) NOT NULL,
    pais VARCHAR (128) NOT NULL,
    cp VARCHAR (5) NOT NULL,
    banos SMALLINT NOT NULL DEFAULT 0,
    habitaciones SMALLINT NOT NULL DEFAULT 0,
    amueblado BOOLEAN DEFAULT FALSE,
    calefaccion BOOLEAN DEFAULT FALSE,
    aire_acondicionado BOOLEAN DEFAULT FALSE,
    jardin BOOLEAN DEFAULT FALSE,
    terraza BOOLEAN DEFAULT FALSE,
    ascensor BOOLEAN DEFAULT FALSE,
    piscina BOOLEAN DEFAULT FALSE,
	wifi BOOLEAN DEFAULT FALSE,
	deleted BOOLEAN DEFAULT FALSE,
    delete_date TIMESTAMP DEFAULT NULL,


    CONSTRAINT FK_inmuebles_usuarios FOREIGN KEY (fk_usuario)
    REFERENCES usuarios(id_usuario),
    CONSTRAINT PK_inmueble PRIMARY KEY(id_inmueble),
    UNIQUE (calle,numero,piso,ciudad,provincia)
);
```

### MODIFICAR TABLAS:

- Renombrar una tabla:
  ```sql
  ALTER TABLE clientes RENAME AS socios;
  ```
- Renombrar un campo:
  ```sql
  ALTER TABLE nombre-tabla CHANGE COLUMN nombre_campo nuevo_nombre_ campo VARCHAR(150);
  ```
- Cambiar tipos de datos y restricciones.
  - Indicamos que la columna last_name pasa a ser un varchar de 10.
  ```sql
  ALTER TABLE employees MODIFY COLUMN last_name VARCHAR(100);
  ```
  - Modificamos en la tabla employees la columna first_name, siendo un varchar de 10 y situandose depues del campo DNI
  ```sql
  ALTER TABLE employees MODIFY COLUMN first_name VARCHAR(100) AFTER dni;
  ```
- Eliminar un campo, en este caso el campo Email
  ```sql
  ALTER TABLE employees DROP COLUMN email;
  ```

## REGISTROS:

- Inertar registros

  ```
  INSERT INTO tblCustomers (CustomerID, [Last Name], [First Name])
  VALUES (1, 'Kelly', 'Jill')
  ```

  - Puede omitir la lista de campos, pero solo si proporciona todos los valores que puede contener el registro.

  ```
  INSERT INTO tblCustomers
  VALUES (1, Kelly, 'Jill', '555-1040', 'someone@microsoft.com')
  ```
  - Insertar registros que vienen de una consulta.La siguiente instrucción INSERT INTO inserta todos los valores de los campos CustomerID, Last Name y First Name de la tabla tblOldCustomers en los campos correspondientes de la tabla tblCustomers.
  ```
  INSERT INTO tblCustomers (CustomerID, [Last Name], [First Name]) 
    SELECT CustomerID, [Last Name], [First Name] 
    FROM tblOldCustomers
  ```
- Actualización de registros:

    - Actualziar los registros de una tabla:
    ```
    UPDATE table name SET field name  = some value
    ```
    - Actualizar los registros que coincidan con una condición:
    ```
    UPDATE tblCustomers
    SET Email = 'None'
    WHERE [Last Name] = 'Smith'
    ```
- Eliminar registros:
    - Eliminar todos los rgistros de una tabla (ESTO ES PELIGROSO):
    ```
    DELETE FROM table list
    ```
    - Eliminar todos los registros que cumplan una determinada condición:
    ```
    DELETE FROM tblInvoices 
    WHERE InvoiceID = 3
    ```
    - Si lo que queremos es quitar datos de deterinados campos, usamos la clausula UPDATE, y ponemos esos valores en NULL
    ```
    UPDATE tblCustomers
    SET Email = Null
    ```
### CONSULTAS:
- Estructura de una consulta básica:
    ```
    SELECT campos
    FROM tabla
    WHERE condicion
    ```
-  Operadores condiciones:

    |Operador|Significado|
    |----|----|
    |= |	Igual que|
    |> |	Mayor que|
    |< |	Menor que|
    |>= |	Mayor o igual que|
    |<= |	Menor o igual que|
    |!= |	Diferente de|
    |Between |	Rango.. Entre un valor y otro|
    |In |	Valores que Coinciden en una Lista|

- Ejemplos de consultas:
```
SELECT * FROM table;
SELECT * FROM table1, table2;
SELECT field1, field2 FROM table1, table2;
SELECT ... FROM ... WHERE condition
SELECT ... FROM ... WHERE condition GROUP BY field;
SELECT ... FROM ... WHERE condition GROUP BY field HAVING condition2;
SELECT ... FROM ... WHERE condition ORDER BY field1, field2;
SELECT ... FROM ... WHERE condition ORDER BY field1, field2 DESC;
SELECT ... FROM ... WHERE condition LIMIT 10;
SELECT DISTINCT field1 FROM ...
SELECT DISTINCT field1, field2 FROM .
```

- INNERJOINS
<img src="./mysqlInnerJoins.jpg" alt="cuadro innerjjoins mysql">