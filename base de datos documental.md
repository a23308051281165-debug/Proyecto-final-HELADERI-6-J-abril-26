Te doy un ejemplo claro y práctico de cómo estructurar una base de datos en **Firestore (Firebase)** para una heladería 🍦. Esto incluye **colecciones, documentos, atributos y tipos de datos**.

---

## 🧊 1. Colección: `productos`

Aquí guardas los helados y otros productos.

### 📄 Documento: `producto_001`

```json
{
  "nombre": "Helado de vainilla",
  "precio": 35.5,
  "stock": 50,
  "categoria": "Helado",
  "sabores": ["vainilla"],
  "tamano": "mediano",
  "disponible": true,
  "fecha_creacion": "2026-04-27T10:00:00Z"
}
```

### 🔹 Tipos de datos:

* `nombre`: string
* `precio`: number (double)
* `stock`: number (int)
* `categoria`: string
* `sabores`: array
* `tamano`: string
* `disponible`: boolean
* `fecha_creacion`: timestamp

---

## 👤 2. Colección: `clientes`

### 📄 Documento: `cliente_001`

```json
{
  "nombre": "Juan Pérez",
  "telefono": "6561234567",
  "correo": "juan@email.com",
  "direccion": "Calle 123, Juárez",
  "fecha_registro": "2026-04-20T15:30:00Z"
}
```

### 🔹 Tipos de datos:

* `nombre`: string
* `telefono`: string
* `correo`: string
* `direccion`: string
* `fecha_registro`: timestamp

---

## 🧾 3. Colección: `ventas`

### 📄 Documento: `venta_001`

```json
{
  "cliente_id": "cliente_001",
  "fecha": "2026-04-27T12:00:00Z",
  "total": 105.5,
  "metodo_pago": "efectivo",
  "productos": [
    {
      "producto_id": "producto_001",
      "cantidad": 2,
      "precio_unitario": 35.5
    },
    {
      "producto_id": "producto_002",
      "cantidad": 1,
      "precio_unitario": 34.5
    }
  ]
}
```

### 🔹 Tipos de datos:

* `cliente_id`: string (referencia)
* `fecha`: timestamp
* `total`: number
* `metodo_pago`: string
* `productos`: array de objetos

---

## 🏪 4. Colección: `empleados`

### 📄 Documento: `empleado_001`

```json
{
  "nombre": "Ana López",
  "puesto": "Cajera",
  "telefono": "6569876543",
  "activo": true,
  "fecha_ingreso": "2025-10-01T09:00:00Z"
}
```

### 🔹 Tipos de datos:

* `nombre`: string
* `puesto`: string
* `telefono`: string
* `activo`: boolean
* `fecha_ingreso`: timestamp

---

## 🧠 Tips importantes

* En Firestore **no hay tablas**, sino **colecciones → documentos**.
* Puedes guardar listas (arrays) y objetos dentro de documentos.
* Evita hacer documentos demasiado grandes.
* Usa IDs automáticos o personalizados.

---

Si quieres, puedo ayudarte a conectar esta estructura directamente con **Flutter (CRUD completo)** paso a paso 😉
