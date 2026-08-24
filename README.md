# M6_Ventas_export_legacy

1. Transformaciones realizadas y orden aplicado
El proceso de normalización se ejecutó siguiendo una secuencia lógica de ETL (Extract–Transform–Load) dentro de Power Query, asegurando consistencia y trazabilidad mediante los Pasos Aplicados. El orden fue el siguiente:

Definición del modelo relacional (esquema estrella)
- Se identificó la tabla de hechos fact_ventas, con su clave primaria id_venta;
- Se definieron las claves foráneas id_cliente y id_producto;
- Se generaron las tablas dimensionales dim_cliente y dim_producto, tomando únicamente atributos propios de cada entidad.
Esta separación permite reducir redundancia, mejorar el rendimiento del modelo y facilitar el análisis.

Eliminación de filas duplicadas y vacías
- Se seleccionaron todas las columnas → Inicio → Reducir filas → Quitar filas → Quitar duplicados.
- Luego, nuevamente todas las columnas → Quitar filas → Quitar vacías.
Esto garantiza que la tabla de hechos no contenga registros repetidos ni transacciones incompletas.

Estandarización de nombres de columnas (snake_case)
- Se renombraron todas las columnas siguiendo la convención snake_case, por ejemplo:
- Precio Unitario → precio_unitario
- Fecha Venta → fecha_venta
Esto mejora la legibilidad, evita errores en DAX y facilita la integración con otros sistemas.

Corrección de tipos de datos según el contenido de cada columna
- Se asignaron tipos adecuados:
    - Fechas → date
    - Valores monetarios → decimal number
    - Cantidades → whole number
    - Códigos → text

Esta etapa es crítica para evitar errores en agregaciones, filtros y relaciones.

2. Justificación de los tipos de datos elegidos
La elección de cada tipo de dato responde a criterios de integridad, precisión y compatibilidad con el motor de Power BI:

- Fecha:
  Convertida a tipo date para permitir ordenamiento cronológico, segmentación por períodos y uso de funciones de inteligencia temporal.
  Ejemplo: dd/mm/yyyy en lugar de texto.

- Valores monetarios (precio_unitario, total_venta):
  Tipo decimal number para evitar errores de redondeo y asegurar cálculos financieros precisos.

- Cantidades (cantidad):
  Tipo whole number, ya que no admite decimales.

- Identificadores (id_cliente, id_producto):
  Tipo text para evitar interpretaciones numéricas incorrectas (por ejemplo, eliminación de ceros a la izquierda).

3. Resolución de valores nulos y duplicados
- Duplicados
  - Se seleccionaron todas las columnas → Quitar duplicados.
Esto asegura que cada transacción sea única y evita distorsiones en métricas como ventas totales.

- Filas vacías
  - Se seleccionaron todas las columnas → Quitar filas vacías.
Esto elimina registros incompletos que podrían generar errores en el modelo.

- Valores nulos en columnas específicas
  - Se filtraron los nulos en columnas críticas (por ejemplo, precio_unitario, id_cliente).
En caso de ser necesario, se derivaron tablas auxiliares para analizar estos casos por separado.

4. Criterio para separar datos del cliente y datos de la transacción
La separación se realizó siguiendo el principio de dependencia funcional:

Los atributos que dependen exclusivamente del cliente se trasladaron a dim_cliente:
- nombre;
- mail;
- teléfono;
- ciudad;
- provincia;
- segmento;
- fecha_alta;
- actividad.

Los atributos que dependen de la transacción permanecieron en fact_ventas:
- fecha_venta;
- cantidad;
- precio_unitario;
- total_venta;
- id_producto;
- id_cliente.

Este criterio evita redundancia, mejora la calidad del modelo y permite análisis más eficientes.
