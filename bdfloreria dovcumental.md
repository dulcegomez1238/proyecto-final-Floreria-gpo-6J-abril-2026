Aquí tienes un ejemplo claro y práctico de cómo estructurar una base de datos para una florería usando un modelo tipo **NoSQL (por ejemplo, MongoDB)**, con **colecciones, documentos, atributos y tipos de datos**.

---

# 🌸 Base de Datos: `floreria_db`

## 📁 Colección: `productos`

Contiene la información de flores, arreglos y artículos.

```json
{
  "_id": ObjectId,
  "nombre": "Ramo de rosas rojas",
  "descripcion": "Ramo con 12 rosas rojas frescas",
  "precio": 350.50,
  "stock": 25,
  "categoria": "Ramos",
  "fecha_ingreso": ISODate("2026-04-20"),
  "activo": true
}
```

**Tipos de datos:**

* `_id`: ObjectId
* `nombre`: String
* `descripcion`: String
* `precio`: Decimal / Double
* `stock`: Integer
* `categoria`: String
* `fecha_ingreso`: Date
* `activo`: Boolean

---

## 📁 Colección: `clientes`

Información de los clientes.

```json
{
  "_id": ObjectId,
  "nombre": "María López",
  "telefono": "6561234567",
  "email": "maria@email.com",
  "direccion": {
    "calle": "Av. Juárez",
    "numero": "123",
    "ciudad": "Ciudad Juárez",
    "codigo_postal": "32000"
  },
  "fecha_registro": ISODate("2026-04-15")
}
```

**Tipos de datos:**

* `nombre`: String
* `telefono`: String
* `email`: String
* `direccion`: Object
* `fecha_registro`: Date

---

## 📁 Colección: `pedidos`

Registro de compras realizadas.

```json
{
  "_id": ObjectId,
  "cliente_id": ObjectId,
  "productos": [
    {
      "producto_id": ObjectId,
      "cantidad": 2,
      "precio_unitario": 350.50
    }
  ],
  "total": 701.00,
  "fecha_pedido": ISODate("2026-04-25"),
  "estado": "Entregado",
  "direccion_entrega": "Av. Tecnológico 456"
}
```

**Tipos de datos:**

* `cliente_id`: ObjectId (referencia a clientes)
* `productos`: Array de objetos
* `total`: Decimal
* `fecha_pedido`: Date
* `estado`: String
* `direccion_entrega`: String

---

## 📁 Colección: `proveedores`

Información de proveedores de flores.

```json
{
  "_id": ObjectId,
  "nombre": "Flores del Norte",
  "telefono": "6569876543",
  "email": "contacto@floresnorte.com",
  "direccion": "Chihuahua, México",
  "productos_suministrados": ["rosas", "tulipanes", "girasoles"]
}
```

**Tipos de datos:**

* `nombre`: String
* `telefono`: String
* `email`: String
* `direccion`: String
* `productos_suministrados`: Array de String

---

## 📁 Colección: `empleados`

Datos del personal.

```json
{
  "_id": ObjectId,
  "nombre": "Carlos Pérez",
  "puesto": "Florista",
  "telefono": "6562223344",
  "fecha_contratacion": ISODate("2025-10-01"),
  "salario": 8500.00,
  "activo": true
}
```

**Tipos de datos:**

* `nombre`: String
* `puesto`: String
* `telefono`: String
* `fecha_contratacion`: Date
* `salario`: Decimal
* `activo`: Boolean

---

# 🧠 Relación entre colecciones

* `pedidos.cliente_id` → referencia a `clientes`
* `pedidos.productos.producto_id` → referencia a `productos`

---

# ✅ Notas importantes

* MongoDB usa documentos flexibles (puedes agregar más campos sin problema).
* Las relaciones se manejan mediante referencias (`ObjectId`).
* Ideal para apps web o móviles de ventas.

---

Si quieres, puedo darte este mismo ejemplo pero en **SQL (MySQL o PostgreSQL)** con tablas, llaves primarias y foráneas 👌
