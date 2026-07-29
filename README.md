# CampusCar

Este repositorio contiene el diseño de la base de datos relacional para la gestión de inventario, proceso de ventas y control de mantenimientos en un concesionario de vehículos.

---

## 📐 Diagrama Entidad-Relación

El modelo relacional está compuesto por **6 tablas principales** conectadas mediante Claves Primarias (`PK`) y Claves Foráneas (`FK`), siguiendo la notación *Crow's Foot* (pata de gallo) para la definición de cardinalidades.

---

## 📁 Diccionario de Datos

### 1. `Vehiculos`
Almacena la información técnica e inventario de los automóviles.

| Campo | Tipo de Dato | Restricción | Descripción |
| :--- | :--- | :--- | :--- |
| `vehiculoID` | `INTEGER` | `PRIMARY KEY` | Identificador único del vehículo |
| `marca` | `VARCHAR(30)` | `NOT NULL` | Marca del vehículo |
| `modelo` | `VARCHAR(30)` | `NOT NULL` | Modelo del vehículo |
| `año` | `INTEGER` | `NOT NULL` | Año de fabricación |
| `VIN` | `VARCHAR` | `UNIQUE` | Número de serie/identificación vehicular |
| `precio` | `INTEGER` | `NOT NULL` | Precio comercial |
| `color` | `VARCHAR(30)` | | Color exterior |
| `combustible` | `VARCHAR(30)` | | Tipo de combustible |
| `transmision` | `VARCHAR(30)` | | Tipo de caja de cambios |
| `estado` | `VARCHAR(30)` | | Condición (ej. Nuevo, Usado) |
| `disponibilidad`| `VARCHAR(30)` | | Estado de venta (ej. Disponible, Vendido) |

---

### 2. `Clientes`
Almacena la información de contacto e identificación de los compradores/usuarios.

| Campo | Tipo de Dato | Restricción | Descripción |
| :--- | :--- | :--- | :--- |
| `clienteID` | `INTEGER` | `PRIMARY KEY` | Identificador único del cliente |
| `nombre` | `VARCHAR(30)` | `NOT NULL` | Nombre completo |
| `telefono` | `VARCHAR(30)` | | Teléfono de contacto |
| `correo_electronico` | `VARCHAR(30)` | | Correo electrónico |
| `direccion` | `VARCHAR(50)` | | Dirección de residencia |

---

### 3. `Vendedores`
Registra al personal comercial encargado de gestionar las ventas.

| Campo | Tipo de Dato | Restricción | Descripción |
| :--- | :--- | :--- | :--- |
| `vendedorID` | `INTEGER` | `PRIMARY KEY` | Identificador único del vendedor |
| `nombre` | `VARCHAR(30)` | `NOT NULL` | Nombre completo del empleado |
| `numero_empleado` | `VARCHAR` | `UNIQUE` | Código corporativo de empleado |
| `fecha_de_contratacion` | `DATE` | | Fecha de ingreso a la empresa |

---

### 4. `Ventas`
Encabezado de la transacción comercial efectuada.

| Campo | Tipo de Dato | Restricción | Descripción |
| :--- | :--- | :--- | :--- |
| `ventaID` | `INTEGER` | `PRIMARY KEY` | Identificador único de la transacción |
| `fecha` | `TIMESTAMP` | `NOT NULL` | Fecha y hora exacta de compra |
| `total` | `INTEGER` | `NOT NULL` | Monto total transaccionado |
| `metodo_de_pago` | `VARCHAR(30)` | | Forma de pago utilizada |
| `clienteID` | `INTEGER` | `FOREIGN KEY` | Referencia al cliente comprador |
| `vendedorID` | `INTEGER` | `FOREIGN KEY` | Referencia al vendedor a cargo |

---

### 5. `detalle_ventas`
Tabla de desglose de los vehículos asociados a una venta concreta.

| Campo | Tipo de Dato | Restricción | Descripción |
| :--- | :--- | :--- | :--- |
| `detalleID` | `INTEGER` | `PRIMARY KEY` | Identificador del registro de detalle |
| `ventaID` | `INTEGER` | `FOREIGN KEY` | Transacción a la que pertenece |
| `vehiculoID` | `INTEGER` | `FOREIGN KEY, UNIQUE` | Vehículo vendido |
| `precio_venta` | `INTEGER` | `NOT NULL` | Precio final asignado en la venta |

---

### 6. `Mantenimiento`
Historial de revisiones y reparaciones mecánicas de los vehículos.

| Campo | Tipo de Dato | Restricción | Descripción |
| :--- | :--- | :--- | :--- |
| `mantenimientoID`| `INTEGER` | `PRIMARY KEY` | Identificador único del servicio |
| `tipo_de_servicio` | `VARCHAR(30)` | `NOT NULL` | Tipo de trabajo realizado |
| `costo` | `INTEGER` | `NOT NULL` | Valor del servicio |
| `fecha` | `TIMESTAMP` | `NOT NULL` | Fecha de realización |
| `vehiculoID` | `INTEGER` | `FOREIGN KEY` | Vehículo atendido |
| `clienteID` | `INTEGER` | `FOREIGN KEY, NULLABLE` | Cliente solicitante (Opcional) |

