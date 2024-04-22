# NORMALIZACION Y CONSULTAS EN SQL

1. ## Comandos DDL.

   ```sql
   CREATE TABLE ciudad (
       id INT NOT NULL AUTO_INCREMENT,
       nombre_ciudad VARCHAR(255) NOT NULL,
       region_id SMALLINT NOT NULL,
       PRIMARY KEY (id)
   );
   
   CREATE TABLE cliente (
       id INT NOT NULL AUTO_INCREMENT,
       nombre_cliente VARCHAR(50) NOT NULL,
       apellido_1_cliente VARCHAR(50) NOT NULL,
       apellido_2_cliente VARCHAR(50) NOT NULL,
       rep_ventas_id SMALLINT,
       limite_credito DOUBLE,
       PRIMARY KEY (id)
   );
   
   CREATE TABLE contacto (
       id INT NOT NULL AUTO_INCREMENT,
       nombre_contacto VARCHAR(50) NOT NULL,
       apellido_contacto VARCHAR(30) NOT NULL,
       emai_contacto VARCHAR(30),
       cliente_id SMALLINT,
       PRIMARY KEY (id),
       FOREIGN KEY (cliente_id) REFERENCES cliente(id)
   );
   
   CREATE TABLE detalle_pedido (
       id INT NOT NULL AUTO_INCREMENT,
       pedido_id SMALLINT NOT NULL,
       detalle_producto_id SMALLINT NOT NULL,
       cantidad SMALLINT NOT NULL,
       precio_unidad DOUBLE NOT NULL,
       numero_linea SMALLINT NOT NULL,
       transaccion_id SMALLINT NOT NULL,
       PRIMARY KEY (id),
       FOREIGN KEY (pedido_id) REFERENCES pedido(id),
       FOREIGN KEY (detalle_producto_id) REFERENCES detalle_producto(id),
       FOREIGN KEY (transaccion_id) REFERENCES transaccion(id)
   );
   
   CREATE TABLE detalle_producto (
       id INT NOT NULL AUTO_INCREMENT,
       id_producto SMALLINT NOT NULL,
       id_gama SMALLINT NOT NULL,
       id_dimension SMALLINT NOT NULL,
       id_proveedor SMALLINT,
       descripcion VARCHAR(50),
       stock SMALLINT,
       precio_venta DOUBLE NOT NULL,
       precio_proveedor DOUBLE NOT NULL,
       PRIMARY KEY (id),
       FOREIGN KEY (id_producto) REFERENCES producto(id),
       FOREIGN KEY (id_gama) REFERENCES gama(id),
       FOREIGN KEY (id_dimension) REFERENCES dimension(id),
       FOREIGN KEY (id_proveedor) REFERENCES proveedor(id)
   );
   
   CREATE TABLE dimension (
       id INT NOT NULL AUTO_INCREMENT,
       dimension VARCHAR(25),
       PRIMARY KEY (id)
   );
   
   CREATE TABLE direccion_cliente (
       id INT NOT NULL AUTO_INCREMENT,
       linea_1 VARCHAR(50) NOT NULL,
       linea_2 VARCHAR(50),
       codigo_postal SMALLINT,
       ciudad_id SMALLINT NOT NULL,
       cliente_id SMALLINT NOT NULL,
       PRIMARY KEY (id),
       FOREIGN KEY (ciudad_id) REFERENCES ciudad(id),
       FOREIGN KEY (cliente_id) REFERENCES cliente(id)
   );
   
   CREATE TABLE direccion_oficina (
       id INT NOT NULL AUTO_INCREMENT,
       linea_1 VARCHAR(50) NOT NULL,
       linea_2 VARCHAR(50) NOT NULL,
       codigo_postal SMALLINT,
       ciudad_id SMALLINT NOT NULL,
       oficina_id SMALLINT NOT NULL,
       PRIMARY KEY (id),
       FOREIGN KEY (ciudad_id) REFERENCES ciudad(id),
       FOREIGN KEY (oficina_id) REFERENCES oficina(id)
   );
   
   CREATE TABLE empleado (
       id INT NOT NULL AUTO_INCREMENT,
       nombre_empledo VARCHAR(50) NOT NULL,
       apellido_1 VARCHAR(50) NOT NULL,
       apellido_2 VARCHAR(50),
       oficina_id SMALLINT NOT NULL,
       codigo_jefe INT NOT NULL,
       id_puesto SMALLINT NOT NULL,
       PRIMARY KEY (id),
       FOREIGN KEY (oficina_id) REFERENCES oficina(id),
       FOREIGN KEY (codigo_jefe) REFERENCES empleado(id),
       FOREIGN KEY (id_puesto) REFERENCES puesto(id)
   );
   
   CREATE TABLE estado (
       id INT NOT NULL AUTO_INCREMENT,
       estado VARCHAR(15) NOT NULL,
       PRIMARY KEY (id)
   );
   
   CREATE TABLE forma_pago (
       id INT NOT NULL AUTO_INCREMENT,
       tipo VARCHAR(255) NOT NULL,
       PRIMARY KEY (id)
   );
   
   CREATE TABLE forma_pago_cliente (
       id INT NOT NULL AUTO_INCREMENT,
       id_forma_pago SMALLINT NOT NULL,
       id_cliente SMALLINT NOT NULL,
       PRIMARY KEY (id),
       FOREIGN KEY (id_forma_pago) REFERENCES forma_pago(id),
       FOREIGN KEY (id_cliente) REFERENCES cliente(id)
   );
   
   CREATE TABLE gama (
       id INT NOT NULL AUTO_INCREMENT,
       descripcion_texto TEXT,
       descripcion_html TEXT,
       imagen VARCHAR(256),
       PRIMARY KEY (id)
   );
   
   CREATE TABLE oficina (
       id BIGINT NOT NULL AUTO_INCREMENT,
       nombre_oficina VARCHAR(255) NOT NULL,
       PRIMARY KEY (id)
   );
   
   CREATE TABLE pais (
       id INT NOT NULL AUTO_INCREMENT,
       nombre_pais VARCHAR(255) NOT NULL,
       PRIMARY KEY (id)
   );
   
   CREATE TABLE pedido (
       id INT NOT NULL AUTO_INCREMENT,
       fecha_pedido DATE NOT NULL,
       fecha_esperada DATE NOT NULL,
       fecha_entrega DATE,
       comentarios VARCHAR(255),
       id_cliente SMALLINT NOT NULL,
       estado_id SMALLINT NOT NULL,
       PRIMARY KEY (id),
       FOREIGN KEY (id_cliente) REFERENCES cliente(id),
       FOREIGN KEY (estado_id) REFERENCES estado(id)
   );
   
   CREATE TABLE producto (
       id INT NOT NULL AUTO_INCREMENT,
       nombre_producto VARCHAR(70),
       PRIMARY KEY (id)
   );
   
   CREATE TABLE proveedor (
       id INT NOT NULL AUTO_INCREMENT,
       nombre_proveedor VARCHAR(50) NOT NULL,
       PRIMARY KEY (id)
   );
   
   CREATE TABLE puesto (
       id INT NOT NULL AUTO_INCREMENT,
       nombre_puesto VARCHAR(255) NOT NULL,
       PRIMARY KEY (id)
   );
   
   CREATE TABLE region (
       id BIGINT NOT NULL AUTO_INCREMENT,
       nombre_region VARCHAR(255) NOT NULL,
       pais_id SMALLINT NOT NULL,
       PRIMARY KEY (id),
       FOREIGN KEY (pais_id) REFERENCES pais(id)
   );
   
   CREATE TABLE telefono_cliente (
       cliente_id SMALLINT NOT NULL,
       tipo_telefono_id SMALLINT NOT NULL,
       numero SMALLINT NOT NULL,
       id VARCHAR(255) NOT NULL,
       fax SMALLINT NOT NULL,
       PRIMARY KEY (id),
       FOREIGN KEY (cliente_id) REFERENCES cliente(id),
       FOREIGN KEY (tipo_telefono_id) REFERENCES tipo_telefono(id)
   );
   
   CREATE TABLE telefono_contacto (
       id VARCHAR(255) NOT NULL,
       numero SMALLINT NOT NULL,
       tipo_telefono SMALLINT NOT NULL,
       contacto_id SMALLINT NOT NULL,
       PRIMARY KEY (id),
       FOREIGN KEY (tipo_telefono) REFERENCES tipo_telefono(id),
       FOREIGN KEY (contacto_id) REFERENCES contacto(id)
   );
   
   CREATE TABLE telefono_empleado (
       id INT NOT NULL AUTO_INCREMENT,
       tipo_telefono SMALLINT NOT NULL,
       empleado_id SMALLINT NOT NULL,
       numero SMALLINT NOT NULL,
       extension SMALLINT NOT NULL,
       PRIMARY KEY (id),
       FOREIGN KEY (tipo_telefono) REFERENCES tipo_telefono(id),
       FOREIGN KEY (empleado_id) REFERENCES empleado(id)
   );
   
   CREATE TABLE telefono_oficina (
       id INT NOT NULL AUTO_INCREMENT,
       tipo_telefono SMALLINT NOT NULL,
       oficina_id SMALLINT NOT NULL,
       numero SMALLINT NOT NULL,
       PRIMARY KEY (id),
       FOREIGN KEY (tipo_telefono) REFERENCES tipo_telefono(id),
       FOREIGN KEY (oficina_id) REFERENCES oficina(id)
   );
   
   CREATE TABLE tipo_telefono (
       id INT NOT NULL AUTO_INCREMENT,
       tipo_telefono VARCHAR(20) NOT NULL,
       PRIMARY KEY (id)
   );
   
   CREATE TABLE transaccion (
       id INTEGER NOT NULL,
       id_forma_pago_cliente SMALLINT NOT NULL,
       fecha_pago DATE,
       total DOUBLE PRECISION NOT NULL,
       PRIMARY KEY (id),
       FOREIGN KEY (id_forma_pago_cliente) REFERENCES forma_pago_cliente(id)
   );
   
   ```

   

2. ## Comandos DML.

   ```sql
   INSERT INTO ciudad (nombre_ciudad, region_id)
   VALUES ('Madrid', 1),
          ('Barcelona', 2),
          ('Sevilla', 3);
   
   
   INSERT INTO cliente (nombre_cliente, apellido_1_cliente, apellido_2_cliente, rep_ventas_id, limite_credito)
   VALUES ('Juan', 'Gómez', 'Martínez', 1, 500),
          ('María', 'López', 'Sánchez', 2, 700),
          ('Pedro', 'Rodríguez', 'García', 3, 1000);
   
   
   INSERT INTO contacto (nombre_contacto, apellido_contacto, emai_contacto, cliente_id)
   VALUES ('Luis', 'Pérez', 'luis@example.com', 1),
          ('Ana', 'García', 'ana@example.com', 2),
          ('Carlos', 'Ruiz', 'carlos@example.com', 3);
   
   INSERT INTO detalle_pedido (pedido_id, detalle_producto_id, cantidad, precio_unidad, numero_linea, transaccion_id)
   VALUES (1, 1, 2, 10.5, 1, 1),
          (2, 2, 3, 15.75, 1, 2),
          (3, 3, 1, 20, 1, 3);
   
   
   INSERT INTO detalle_producto (id_producto, id_gama, id_dimension, id_proveedor, descripcion, stock, precio_venta, precio_proveedor)
   VALUES (1, 1, 1, 1, 'Producto 1', 50, 20, 15),
          (2, 2, 2, 2, 'Producto 2', 30, 25, 18),
          (3, 3, 3, 3, 'Producto 3', 20, 30, 22);
   
   
   INSERT INTO dimension (dimension)
   VALUES ('Dimensión 1'),
          ('Dimensión 2'),
          ('Dimensión 3');
   
   
   INSERT INTO direccion_cliente (linea_1, linea_2, codigo_postal, ciudad_id, cliente_id)
   VALUES ('Calle Principal 123', 'Piso 2', '28001', 1, 1),
          ('Avenida Central 456', NULL, '28940', 2, 2),
          ('Plaza Mayor 789', NULL, '28942', 3, 3);
   
   
   INSERT INTO direccion_oficina (linea_1, linea_2, codigo_postal, ciudad_id, oficina_id)
   VALUES ('Calle Principal 123', 'Piso 2', '28001', 1, 1),
          ('Avenida Central 456', NULL, '28940', 2, 2),
          ('Plaza Mayor 789', NULL, '28942', 3, 3);
   
   
   INSERT INTO empleado (nombre_empledo, apellido_1, apellido_2, oficina_id, codigo_jefe, id_puesto)
   VALUES ('Ana', 'Martínez', 'Gómez', 1, NULL, 1),
          ('Carlos', 'González', 'López', 2, 1, 2),
          ('Luis', 'Ruiz', 'Pérez', 3, 2, 3);
   
   
   INSERT INTO estado (estado)
   VALUES ('Activo'),
          ('Inactivo');
   
   
   INSERT INTO forma_pago (tipo)
   VALUES ('Efectivo'),
          ('Tarjeta de crédito'),
          ('Transferencia bancaria');
   
   
   INSERT INTO forma_pago_cliente (id_forma_pago, id_cliente)
   VALUES (1, 1),
          (2, 2),
          (3, 3);
   
   
   INSERT INTO gama (descripcion_texto, descripcion_html, imagen)
   VALUES ('Gama 1', '<b>Gama 1</b>', 'imagen1.jpg'),
          ('Gama 2', '<b>Gama 2</b>', 'imagen2.jpg'),
          ('Gama 3', '<b>Gama 3</b>', 'imagen3.jpg');
   
   
   INSERT INTO oficina (nombre_oficina)
   VALUES ('Oficina Central'),
          ('Sucursal Norte'),
          ('Sucursal Sur');
   
   
   INSERT INTO pais (nombre_pais)
   VALUES ('España'),
          ('Francia'),
          ('Alemania');
   
   INSERT INTO pedido (fecha_pedido, fecha_esperada, fecha_entrega, comentarios, id_cliente, estado_id)
   VALUES ('2023-01-15', '2023-01-20', '2023-01-18', 'Pedido urgente', 1, 1),
          ('2023-02-10', '2023-02-15', NULL, 'Pedido estándar', 2, 2),
          ('2023-03-05', '2023-03-10', NULL, 'Pedido retrasado', 3, 2);
   
   
   INSERT INTO producto (nombre_producto)
   VALUES ('Producto 1'),
          ('Producto 2'),
          ('Producto 3');
   
   
   INSERT INTO proveedor (nombre_proveedor)
   VALUES ('Proveedor 1'),
          ('Proveedor 2'),
          ('Proveedor 3');
   
   
   INSERT INTO puesto (nombre_puesto)
   VALUES ('Vendedor'),
          ('Gerente de ventas'),
          ('Cajero');
   
   
   INSERT INTO region (nombre_region, pais_id)
   VALUES ('Comunidad de Madrid', 1),
          ('Provenza-Alpes-Costa Azul', 2),
          ('Renania del Norte-Westfalia', 3);
   
   
   INSERT INTO telefono_cliente (cliente_id, tipo_telefono_id, numero, fax)
   VALUES (1, 1, '123456789', NULL),
          (2, 2, '987654321', NULL),
          (3, 3, '456789123', '789456123');
   
   
   INSERT INTO telefono_empleado (empleado_id, tipo_telefono_id, numero)
   VALUES (1, 1, '987654321'),
          (2, 2, '123456789'),
          (3, 3, '456789123');
   
   
   INSERT INTO telefono_oficina (oficina_id, tipo_telefono_id, numero)
   VALUES (1, 1, '123456789'),
          (2, 2, '987654321'),
          (3, 3, '456789123');
   
   
   INSERT INTO transaccion (id_forma_pago_cliente, fecha_pago, total)
   VALUES (1, '2023-01-18', 100),
          (2, '2023-02-14', 200),
          (3, '2023-03-08', 300);
   
   INSERT INTO tipo_telefono (tipo)
   VALUES ('Móvil'),
          ('Fijo'),
          ('Fax');
   
   ```

   

3. ## Explicación de la normalización.

4. ![normalizacion](normalizacion.png)

5. 

   #### Tablas en 1FN:

   ![forma1](forma1.png)

   Se caracterizan por que no hay múltiples valores en una misma celda, hay una sola llave primaria y cada atributo es atómico.

   Tablas en 2FN

   Para la normalizacion de estas tablas, se normalizó teniendo en cuenta desde la 1FN, definiendo la llave primaria, atributos atómicos y se eliminaron dependecias parciales

   

6. ## Resultados de las consultas.

   ### Consultas sobre una tabla

   1. Devuelve un listado con el código de oficina y la ciudad donde hay oficinas.

      ```sql
      SELECT o.id, c.nombre_ciudad
      FROM oficina as o
      inner join ciudad as c ON c.id = o.id
       id | nombre_ciudad
      ----+---------------
        1 | Madrid
        2 | Barcelona
        3 | ParÝs
      ```

      

   2. Devuelve un listado con la ciudad y el teléfono de las oficinas de España.

      ```sql
      SELECT ci.nombre_ciudad as ciudad, t_o.numero as numero
      FROM direccion_oficina as d_o
      INNER JOIN telefono_oficina as t_O ON d_o.oficina_id = d_o.oficina_id
      INNER JOIN ciudad as ci ON d_o.ciudad_id = ci.id
      INNER JOIN region as reg ON ci.region_id = reg.id
      INNER JOIN pais as pa ON reg.pais_id = pa.id
      WHERE pa.nombre_pais = 'España';
      ---------------------------------
      "numero"	"ciudad"
      11110000	"Madrid"
      22220000	"Barcelona"
      
      ```

   3. Devuelve un listado con el nombre, apellidos y email de los empleados cuyo
      jefe tiene un código de jefe igual a 7.

     ```sql
   select e.nombre_empledo, e.apellido_1, e.apellido_2, e.emai
   from empleado as e
   INNER JOIN telefono_empleado AS t_e ON e.id = t_e.empleado_id
   WHERE e.codigo_jefe = 7;
    nombre_empledo | apellido_1 | apellido_2
   ----------------+------------+------------
   (0 filas)
   
     ```


   4. Devuelve el nombre del puesto, nombre, apellidos y email del jefe de la
      empresa.

     ```sql
   SELECT e.nombre_empledo, apellido_1, apellido_2, p_u.nombre_puesto
   FROM empleado as e
   INNER JOIN puesto as p_u ON e.id_puesto = p_u.id
   WHERE codigo_jefe IS NULL;
   
    nombre_empledo | apellido_1 | apellido_2 |   nombre_puesto
   ----------------+------------+------------+-------------------
    Laura          | Hernßndez  | GarcÝa     | Gerente de Ventas
     ```


   5. Devuelve un listado con el nombre, apellidos y puesto de aquellos
      empleados que no sean representantes de ventas.

     ```sql
   SELECT e.nombre_empledo, apellido_1, apellido_2, p_u.nombre_puesto
   FROM empleado as e
   INNER JOIN puesto as p_u ON e.id_puesto = p_u.id
   WHERE p_u.id != 2;
    nombre_empledo | apellido_1 | apellido_2 |      nombre_puesto
   ----------------+------------+------------+--------------------------
    Carlos         | RodrÝguez  | PÚrez      | Asistente Administrativo
    Pedro          | DÝaz       | Ruiz       | Vendedor
    Juan           | Gonzßlez   | L¾pez      | Vendedor
     ```


   6. Devuelve un listado con el nombre de los todos los clientes españoles.

      ```sql
      SELECT DISTINCT c.nombre_cliente, c.apellido_1_cliente, c.apellido_2_cliente
      FROM direccion_cliente AS d_c
      INNER JOIN cliente as c ON d_c.cliente_id = c.id
      INNER JOIN ciudad as ci ON d_c.ciudad_id = ci.id
      INNER JOIN region as reg ON ci.region_id = reg.id
      INNER JOIN pais as pa ON reg.pais_id = pa.id
      WHERE pa.nombre_pais = 'España';
      nombre_cliente | apellido_1_cliente | apellido_2_cliente
      ----------------+--------------------+--------------------
       Ana            | L¾pez              | Sßnchez
       Carlos         | Gonzßlez           | MartÝnez
      ```

   7. Devuelve un listado con los distintos estados por los que puede pasar un
      pedido.

     ```sql
    SELECT id, estado FROM estado;
    id |   estado
   ----+------------
     1 | Activo
     2 | Inactivo
     3 | En Proceso
     ```


   8. Devuelve un listado con el código de cliente de aquellos clientes que
      realizaron algún pago en 2008. Tenga en cuenta que deberá eliminar
      aquellos códigos de cliente que aparezcan repetidos. Resuelva la consulta:
      • Utilizando la función YEAR de MySQL.
      • Utilizando la función DATE_FORMAT de MySQL.
      • Sin utilizar ninguna de las funciones anteriores.

     ```sql
    
   
   SELECT c.id, c.nombre_cliente
   FROM transaccion AS trans
   INNER JOIN forma_pago_cliente AS fpc ON trans.id_forma_pago_cliente = fpc.id
   INNER JOIN cliente AS c ON fpc.id_cliente = c.id
   WHERE YEAR(trans.fecha_pago) = 2008;
   
   id | nombre_cliente | fecha_pago
   ----+----------------+------------
   (0 filas)
   ---------------------------------------
   SELECT c.id, c.nombre_cliente
   FROM transaccion AS trans
   INNER JOIN forma_pago_cliente AS fpc ON trans.id_forma_pago_cliente = fpc.id
   INNER JOIN cliente AS c ON fpc.id_cliente = c.id
   WHERE YEAR(trans.fecha_pago) = 2024;
    id | nombre_cliente | fecha_pago
   ----+----------------+------------
     1 | Carlos         | 2024-04-20
     2 | Ana            | 2024-04-21
     3 | Pedro          | 2024-04-22
     1 | Carlos         | 2024-04-20
     2 | Ana            | 2024-04-21
     3 | Pedro          | 2024-04-22
   
     ```


   9. Devuelve un listado con el código de pedido, código de cliente, fecha
      esperada y fecha de entrega de los pedidos que no han sido entregados a
      tiempo.

     ```sql
   SELECT pe.id, pe.id_cliente, pe.fecha_esperada, pe.fecha_entrega
   FROM pedido as pe
   WHERE pe.estado_id = 1;
   
    id | id_cliente | fecha_esperada | fecha_entrega
   ----+------------+----------------+---------------
     1 |          1 | 2024-04-25     |
     2 |          2 | 2024-04-28     |
     3 |          3 | 2024-04-27     |
     ```


   10. Devuelve un listado con el código de pedido, código de cliente, fecha
       esperada y fecha de entrega de los pedidos cuya fecha de entrega ha sido al
       menos dos días antes de la fecha esperada.
       • Utilizando la función ADDDATE de MySQL.
       • Utilizando la función DATEDIFF de MySQL.
       • ¿Sería posible resolver esta consulta utilizando el operador de suma + o
       resta -?

   11. Devuelve un listado de todos los pedidos que fueron rechazados en 2009.

       ```sql
       SELECT  pe.id , pe.fecha_pedido , pe.fecha_esperada , pe.fecha_entrega ,   pe.comentarios   , pe.id_cliente , pe.estado_id
       FROM pedido AS pe
       INNER JOIN estado as st ON pe.estado_id = st.id
       WHERE pe.estado_id = 2 and YEAR(pe.fecha_pedido) = 2009;
       
        id | fecha_pedido | fecha_esperada | fecha_entrega | comentarios | id_cliente | estado_id
       ----+--------------+----------------+---------------+-------------+------------+-----------
       (0 filas)
       ```

   12. Devuelve un listado de todos los pedidos que han sido entregados en el
       mes de enero de cualquier año.

       ```sql
       SELECT pe.id, pe.fecha_pedido, pe.fecha_esperada, pe.fecha_entrega, pe.comentarios, pe.id_cliente, pe.estado_id
       FROM pedido AS pe
       WHERE MONTH(pe.fecha_entrega) = 1;
        id | fecha_pedido | fecha_esperada | fecha_entrega | comentarios | id_cliente | estado_id
       ----+--------------+----------------+---------------+-------------+------------+-----------
       
       ```

       

   13. Devuelve un listado con todos los pagos que se realizaron en el
       año 2008 mediante Paypal. Ordene el resultado de mayor a menor.

       ```sql
       SELECT trans.id, trans.id_forma_pago_cliente, trans.fecha_pago, trans.total
       FROM transaccion AS trans
       INNER JOIN forma_pago_cliente AS fpc ON trans.id_forma_pago_cliente = fpc.id
       INNER JOIN forma_pago AS fp ON fpc.id_forma_pago = fp.id
       WHERE fp.tipo = 'Paypal' AND YEAR(trans.fecha_pago) = 2008;
        id | id_forma_pago_cliente | fecha_pago | total
       ----+-----------------------+------------+-------
       (0 filas)
       ```

   14. Devuelve un listado con todas las formas de pago que aparecen en la
       tabla pago. Tenga en cuenta que no deben aparecer formas de pago
       repetidas.

       ```sql
       SELECT DISTINCT tipo FROM forma_pago
                 tipo
       ------------------------
        Apple Pay
        Transferencia bancaria
        Cryptomonedas
        Cheque
        Pago en efectivo
        Google Pay
        Tarjeta de crÚdito
        PayPal
       ```

   15. Devuelve un listado con todos los productos que pertenecen a la
       gama Ornamentales y que tienen más de 100 unidades en stock. El listado
       deberá estar ordenado por su precio de venta, mostrando en primer lugar
       los de mayor precio.

       ```sql
       SELECT p.id, p.nombre_producto, dp.precio_venta, dp.stock
       FROM producto AS p
       INNER JOIN detalle_producto AS dp ON p.id = dp.id_producto
       INNER JOIN gama AS g ON dp.id_gama = g.id
       WHERE g.descripcion_texto = 'Ornamentales' AND dp.stock > 100
       ORDER BY dp.precio_venta DESC;
        id | nombre_producto | precio_venta | stock
       ----+-----------------+--------------+-------
       (0 filas)
       
       ```

   16. Devuelve un listado con todos los clientes que sean de la ciudad de Madrid y
       cuyo representante de ventas tenga el código de empleado 11 o 30.

       ```sql
       SELECT  c.id , c.nombre_cliente, c.apellido_1_cliente,  c.apellido_2_cliente, c.rep_ventas_id,  c.limite_credito
       FROM cliente AS c
       INNER JOIN direccion_cliente AS dc ON c.id = dc.cliente_id
       INNER JOIN ciudad AS ci ON dc.ciudad_id = ci.id
       WHERE ci.nombre_ciudad = 'Madrid' AND c.rep_ventas_id = 11 OR c.rep_ventas_id = 30;
        id | nombre_cliente | apellido_1_cliente | apellido_2_cliente | rep_ventas_id | limite_credito
       ----+----------------+--------------------+--------------------+---------------+--------------
       ```

       

   ### Consultas multitabla (Composición interna)

   Resuelva todas las consultas utilizando la sintaxis de SQL1 y SQL2. Las consultas con
   sintaxis de SQL2 se deben resolver con INNER JOIN y NATURAL JOIN.

   1. Obtén un listado con el nombre de cada cliente y el nombre y apellido de su
      representante de ventas.

     ```sql
   SELECT c.nombre_cliente, e.nombre_empledo, e.apellido_1
   FROM cliente as c
   INNER JOIN empleado as e ON c.id = e.id;
    nombre_cliente | nombre_empledo | apellido_1
   ----------------+----------------+------------
    Carlos         | Juan           | Gonzßlez
    Ana            | MarÝa          | MartÝnez
    Pedro          | Carlos         | RodrÝguez
     ```


   2. Muestra el nombre de los clientes que hayan realizado pagos junto con el
      nombre de sus representantes de ventas.

     ```sql
   SELECT c.nombre_cliente, co.nombre_contacto AS representante_ventas
   FROM cliente AS c
   INNER JOIN contacto AS co ON c.rep_ventas_id = co.id
   INNER JOIN forma_pago_cliente AS fpc ON c.id = fpc.id_cliente
   INNER JOIN transaccion AS t ON fpc.id = t.id_forma_pago_cliente;
    nombre_cliente | representante_ventas
   ----------------+----------------------
    Carlos         | MarÝa
    Ana            | Juan
    Pedro          | MarÝa
    Carlos         | MarÝa
    Ana            | Juan
    Pedro          | MarÝa
     ```


   3. Muestra el nombre de los clientes que no hayan realizado pagos junto con
      el nombre de sus representantes de ventas.

     ```sql
   SELECT c.nombre_cliente, co.nombre_contacto AS representante_ventas
   FROM cliente AS c
   LEFT JOIN contacto AS co ON c.rep_ventas_id = co.id
   LEFT JOIN forma_pago_cliente AS fpc ON c.id = fpc.id_cliente
   LEFT JOIN transaccion AS t ON fpc.id = t.id_forma_pago_cliente
   WHERE t.id IS NULL;
    nombre_cliente | representante_ventas
   ----------------+----------------------
   (0 filas)
     ```


   4. Devuelve el nombre de los clientes que han hecho pagos y el nombre de sus
      representantes junto con la ciudad de la oficina a la que pertenece el
      representante.

     ```sql
   SELECT c.nombre_cliente, co.nombre_contacto AS representante_ventas, p.nombre_puesto
   FROM cliente AS c
   INNER JOIN  contacto AS co ON c.rep_ventas_id = co.id
   INNER JOIN empleado AS e ON c.rep_ventas_id = e.id
   INNER JOIN puesto AS p ON e.id_puesto = p.id
   INNER JOIN forma_pago_cliente AS fpc ON c.id = fpc.id_cliente
   INNER JOIN transaccion AS t ON fpc.id = t.id_forma_pago_cliente;
    nombre_cliente | representante_ventas |   nombre_puesto
   ----------------+----------------------+-------------------
    Carlos         | MarÝa                | Vendedor
    Ana            | Juan                 | Gerente de Ventas
    Pedro          | MarÝa                | Vendedor
    Carlos         | MarÝa                | Vendedor
    Ana            | Juan                 | Gerente de Ventas
    Pedro          | MarÝa                | Vendedor
     ```


   5. Devuelve el nombre de los clientes que no hayan hecho pagos y el nombre
      de sus representantes junto con la ciudad de la oficina a la que pertenece el
      representante.

     ```sql
   SELECT  c.nombre_cliente, co.nombre_contacto AS representante_ventas, ci.nombre_ciudad AS ciudad_representante
   FROM  cliente AS c
   INNER JOIN contacto AS co ON c.rep_ventas_id = co.id
   INNER JOIN empleado AS e ON c.rep_ventas_id = e.id
   INNER JOIN direccion_oficina AS o ON e.oficina_id = o.id
   INNER JOIN ciudad AS ci ON o.ciudad_id = ci.id
   LEFT JOIN forma_pago_cliente AS fpc ON c.id = fpc.id_cliente
   LEFT JOIN transaccion AS t ON fpc.id = t.id_forma_pago_cliente
   WHERE t.id IS NULL;
    nombre_cliente | representante_ventas | ciudad_representante
   ----------------+----------------------+----------------------
   (0 filas)
     ```


   6. Lista la dirección de las oficinas que tengan clientes en Fuenlabrada.

   7. Devuelve el nombre de los clientes y el nombre de sus representantes junto
      con la ciudad de la oficina a la que pertenece el representante.

   8. Devuelve un listado con el nombre de los empleados junto con el nombre
      de sus jefes.

   9. Devuelve un listado que muestre el nombre de cada empleados, el nombre
      de su jefe y el nombre del jefe de sus jefe.

   10. Devuelve el nombre de los clientes a los que no se les ha entregado a
       tiempo un pedido.

   11. Devuelve un listado de las diferentes gamas de producto que ha comprado
       cada cliente.

       ### Consultas multitabla (Composición externa)

       Resuelva todas las consultas utilizando las cláusulas LEFT JOIN, RIGHT JOIN, NATURAL
       LEFT JOIN y NATURAL RIGHT JOIN.

   12. Devuelve un listado que muestre solamente los clientes que no han
       realizado ningún pago.

   13. Devuelve un listado que muestre solamente los clientes que no han
       realizado ningún pedido.

   14. Devuelve un listado que muestre los clientes que no han realizado ningún
       pago y los que no han realizado ningún pedido.

   15. Devuelve un listado que muestre solamente los empleados que no tienen
       una oficina asociada.

   16. Devuelve un listado que muestre solamente los empleados que no tienen un
       cliente asociado.

   17. Devuelve un listado que muestre solamente los empleados que no tienen un
       cliente asociado junto con los datos de la oficina donde trabajan.

   18. Devuelve un listado que muestre los empleados que no tienen una oficina
       asociada y los que no tienen un cliente asociado.

   19. Devuelve un listado de los productos que nunca han aparecido en un
       pedido.

   20. Devuelve un listado de los productos que nunca han aparecido en un
       pedido. El resultado debe mostrar el nombre, la descripción y la imagen del
       producto.

   21. Devuelve las oficinas donde no trabajan ninguno de los empleados que
       hayan sido los representantes de ventas de algún cliente que haya realizado
       la compra de algún producto de la gama Frutales.

   22. Devuelve un listado con los clientes que han realizado algún pedido pero no
       han realizado ningún pago.

   23. Devuelve un listado con los datos de los empleados que no tienen clientes
       asociados y el nombre de su jefe asociado.
       Consultas resumen

   24. ¿Cuántos empleados hay en la compañía?

   25. ¿Cuántos clientes tiene cada país?

   26. ¿Cuál fue el pago medio en 2009?

   27. ¿Cuántos pedidos hay en cada estado? Ordena el resultado de forma
       descendente por el número de pedidos.

   28. Calcula el precio de venta del producto más caro y más barato en una
       misma consulta.

   29. Calcula el número de clientes que tiene la empresa.

   30. ¿Cuántos clientes existen con domicilio en la ciudad de Madrid?

   31. ¿Calcula cuántos clientes tiene cada una de las ciudades que empiezan
       por M?

   32. Devuelve el nombre de los representantes de ventas y el número de clientes
       al que atiende cada uno.

   33. Calcula el número de clientes que no tiene asignado representante de
       ventas.

   34. Calcula la fecha del primer y último pago realizado por cada uno de los
       clientes. El listado deberá mostrar el nombre y los apellidos de cada cliente.

   35. Calcula el número de productos diferentes que hay en cada uno de los
       pedidos.

   36. Calcula la suma de la cantidad total de todos los productos que aparecen en
       cada uno de los pedidos.

   37. Devuelve un listado de los 20 productos más vendidos y el número total de
       unidades que se han vendido de cada uno. El listado deberá estar ordenado
       por el número total de unidades vendidas.

   38. La facturación que ha tenido la empresa en toda la historia, indicando la
       base imponible, el IVA y el total facturado. La base imponible se calcula
       sumando el coste del producto por el número de unidades vendidas de la
       tabla detalle_pedido. El IVA es el 21 % de la base imponible, y el total la
       suma de los dos campos anteriores.

   39. La misma información que en la pregunta anterior, pero agrupada por
       código de producto.

   40. La misma información que en la pregunta anterior, pero agrupada por
       código de producto filtrada por los códigos que empiecen por OR.

   41. Lista las ventas totales de los productos que hayan facturado más de 3000
       euros. Se mostrará el nombre, unidades vendidas, total facturado y total
       facturado con impuestos (21% IVA).

   42. Muestre la suma total de todos los pagos que se realizaron para cada uno
       de los años que aparecen en la tabla pagos.

   ### Consultas variadas

   1. Devuelve el listado de clientes indicando el nombre del cliente y cuántos
      pedidos ha realizado. Tenga en cuenta que pueden existir clientes que no
      han realizado ningún pedido.

   2. Devuelve un listado con los nombres de los clientes y el total pagado por
      cada uno de ellos. Tenga en cuenta que pueden existir clientes que no han
      realizado ningún pago.

   3. Devuelve el nombre de los clientes que hayan hecho pedidos en 2008
      ordenados alfabéticamente de menor a mayor.

   4. Devuelve el nombre del cliente, el nombre y primer apellido de su
      representante de ventas y el número de teléfono de la oficina del 

     representante de ventas, de aquellos clientes que no hayan realizado ningún
     pago.

   5. Devuelve el listado de clientes donde aparezca el nombre del cliente, el
      nombre y primer apellido de su representante de ventas y la ciudad donde
      está su oficina.
   6. Devuelve el nombre, apellidos, puesto y teléfono de la oficina de aquellos
      empleados que no sean representante de ventas de ningún cliente.
   7. Devuelve un listado indicando todas las ciudades donde hay oficinas y el
      número de empleados que tiene.





