# M6_Ventas_export_legacy

El siguiente documentos, muestra la normalización del dataset enviado por el equipo de IT. En el cual se realizaron las siguientes transformaciones:

Qué transformaciones se realizo y en qué orden? 
1- Se definió una tabla de hecho con PK (id_ventas) y FK (id_cliente, id_producto), y a su vez dos tablas dimensionales para id_clientes y id_productos;
2- Se eliminó filas duplicadas y vacías;
3- Se renombró las columnas según el formato snake_case;
4- Se modificó los formatos de valores según correspondiera a cada columna (fecha, moneda, decimales, enteros, etc).

Por qué elegiste cada tipo de dato?
Para mantener la integridad del dashboard. Tomando como ejemplo la fecha, se modificó a valor tipo fecha (dd/mm/yyyy) y no como texto.

Cómo resolviste los valores nulos y duplicados encontrados?
Marcando todas las columnas y en la solapa de inicio -> reducir filas -> quitar filas -> quitar duplicados;
Marcando todas las columnas y en la solapa de inicio -> reducir filas -> quitar filas -> quitar vacías.

Qué criterio usaste para separar los datos del cliente de los de la transacción?
Tomando todas las columnas de la tabla orinal, referentes al id_cliente:
- nombre;
- mail;
- teléfono;
- ciudad;
- provincia;
- segmento;
- fecha de alta;
- actividad.

- 
