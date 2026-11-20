# Préstamo de equipo UNICAH

**Estudiante:** Jese Manzanares  
**Número de cuenta:** 0715200300605

## Respuestas

### Paso 1. Catálogo de equipos

1. Si desmarco **Activo**, el equipo queda archivado y deja de aparecer en la lista normal. Lo puedo reactivar después y todavía aparece en los préstamos donde se usó.
2. Si duplico la Laptop Dell 01, `copy=False` evita que la copia se quede con el código `LAP-001`. Tengo que ponerle su propio código.

### Paso 2. Registro de préstamos

1. Con `_name` le doy nombre al modelo nuevo, `prestamo.prestamo`. Con `_inherit` trae de `mail.thread` el historial y los mensajes del chatter.
2. Cuando un préstamo pasa de Borrador a Prestado, el chatter muestra ese cambio porque el campo tiene `tracking=True`.

### Paso 3. Equipos del préstamo

1. El primer parámetro dice dónde están las líneas (`prestamo.linea`). El segundo indica qué campo de cada línea apunta al préstamo (`prestamo_id`).
2. Si borro el préstamo, también se borran las filas de su pestaña Equipos. Eso lo indica `ondelete="cascade"` en `prestamo_id`.

### Paso 4. Flujo de estados

1. Aunque el botón esté oculto, alguien puede llamar al método desde código. La comprobación en el servidor impide, por ejemplo, volver a prestar un registro que ya está Prestado.
2. `linea_ids.equipo_id` reúne los equipos que puse en el préstamo. Con un solo `write` puedo cambiarles el estado a todos.

### Paso 5. Reglas del préstamo

1. Puedo agregar un proyector disponible al borrador y que después alguien lo mande a mantenimiento. Por eso se revisa otra vez cuando pulso **Prestar**.
2. `@api.constrains` se ejecuta al guardar cambios en los campos que tiene indicados. `action_prestar` hace sus propias comprobaciones cuando intento entregar los equipos. Para los duplicados también hay una restricción en la base de datos que revisa cada línea.

### Paso 6. Contacto, kanban y búsqueda

1. Si arrastro la tarjeta a otra columna, Odoo intenta ponerle el estado de esa columna. Eso pasa porque las columnas del kanban se agrupan por `estado`.
2. Odoo busca los préstamos que tienen ese contacto en `partner_id`. Ese campo está en la tabla de préstamos, así que la tabla de contactos no necesita una columna nueva para `prestamo_ids`.
