# Modelo Entidad-Relación para Tajinaste S.A.

Este repositorio contiene el modelo entidad-relación (ER) para el escenario de gestión de stock, empleados y programa de fidelización de la empresa Tajinaste S.A. dedicado a la venta de plantas y productos de jardinería. 

## Entidades

1. **Vivero**
   - **Código** (PK): Identificador único de cada vivero.
   - **Georreferenciación**: Consta de los atributos `Latitud` y `Longitud` para ubicar el vivero.

2. **Zona**
   - **Código** (PK): Identificador único de cada zona dentro de un vivero.
   - **Nombre**: Descripción de la zona (e.g., "zona exterior", "almacén").
   - **Georreferenciación**: Consta de `Latitud` y `Longitud` para la ubicación de la zona dentro del vivero.

3. **Producto**
   - **Código** (PK): Identificador único del producto.
   - **Nombre**: Nombre del producto.
   - **Stock**: Cantidad disponible del producto en la zona asignada.

4. **Empleado**
   - **DNI** (PK): Identificador único de cada empleado.
   - **Nombre**: Nombre del empleado.
   - **Apellidos**: Incluye `Apellido1` y `Apellido2`.
   - **Teléfono**: Número de contacto del empleado.
   - **Historial**:
      - **Código Vivero**: Referencia al vivero donde trabajó el empleado.
      - **Código Zona**: Referencia a la zona donde trabajó el empleado.
      - **Fecha Inicio** y **Fecha Fin**: Período de tiempo en el que el empleado trabajó en una determinada zona.
      - **Productividad**: Medida de la productividad del empleado durante su estancia en la zona.

6. **Cliente Fidelizado**
   - **DNI** (PK): Identificador único del cliente.
   - **Nombre** y **Apellidos**: Datos del cliente.
   - **Teléfono**: Número de contacto del cliente.
   - **Fecha de ingreso al programa**: Fecha en la que el cliente se unió al programa Tajinaste Plus.
   - **Bonificación**: Beneficio que recibe el cliente en función del volumen de compras mensual.
   - **Pedidos Totales**: Número de pedidos totales hecho por el cliente.

7. **Pedido**
   - **Código** (PK): Identificador único de cada pedido.
   - **Fecha**: Fecha de realización del pedido.

## Relaciones

1. **Trabaja**
   - **Vivero** (1,1) - **Empleado** (0,n): Cada empleado puede trabajar en un único vivero en cada época del año, pero un vivero puede tener múltiples empleados.
   - **Zona** (1,1) - **Empleado** (1,1): Un empleado desempeña su trabajo en una zona específica de un vivero.

2. **Asigna**
   - **Zona** (1,n) - **Producto** (1,n): Cada producto se asigna a una o varias zonas y una zona puede contener varios productos.

3. **Realiza**
   - **Cliente Fidelizado** (1,n) - **Pedido** (1,1): Un cliente puede realizar varios pedidos, pero cada pedido pertenece a un único cliente.

4. **Gestiona**
   - **Empleado** (1,1) - **Pedido** (1,n): Cada pedido es gestionado por un único empleado, pero un empleado puede gestionar múltiples pedidos.

5. **Tiene**
   - **Vivero** (1,1) - **Zona** (1,n): Un vivero tiene una o varias zonas.
   - **Producto** (1,1) - **Stock** (0,n): Cada producto tiene un stock determinado en cada zona en la que se encuentra.

## Atributos y Ejemplos

1. **Latitud** y **Longitud**: Atributos de tipo `float` para ubicar geográficamente.
   - Ejemplo: Latitud: `28.12345`, Longitud: `-16.34567`.

2. **Nombre (Producto, Zona, Empleado)**: Atributos de tipo `string`.
   - Ejemplo: Producto: "Planta de interior", Zona: "Almacén", Empleado: "Ana".

3. **Productividad**: Atributo de tipo `int` que mide el rendimiento del empleado.
   - Ejemplo: `85` (rendimiento de un 85%).

4. **Fecha**: Atributo de tipo `date` para las fechas de pedidos e historial.
   - Ejemplo: `2024-10-14`.

## Restricciones Semánticas

1. **Un empleado no puede estar asignado a más de un vivero al mismo tiempo**, garantizando que la relación entre **Empleado** y **Vivero** es `1:1` en cada período.
2. **Un pedido solo puede ser gestionado por un empleado**, pero un empleado puede gestionar varios pedidos.
3. **Un cliente debe pertenecer al programa Tajinaste Plus para que se le realicen bonificaciones**.
4. **Un producto debe tener stock positivo en cada zona en la que esté asignado**.

## Archivos Incluidos

- `Modelo_entidad_relación_Viveros.drawio`: Archivo editable del diagrama entidad-relación.
- `Modelo_entidad_relación_Viveros.png`: Imagen del modelo entidad-relación.
- `Readme.md`: Descripción detallada del modelo.
