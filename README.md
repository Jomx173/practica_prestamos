# Préstamo de equipo UNICAH

**Estudiante:** Jese Manzanares  
**Número de cuenta:** 0715200300605

## Respuestas

### Paso 1. Catálogo de equipos

1. Al desmarcar Activo, el equipo queda archivado y desaparece de las búsquedas normales. Se puede reactivar y conserva sus vínculos con los préstamos.
2. `copy=False` evita que Odoo copie el código de inventario al duplicar un equipo. El usuario debe proporcionar un código para el nuevo registro.

### Paso 2. Registro de préstamos

1. `_name` registra el nuevo modelo `prestamo.prestamo`. `_inherit` incorpora el comportamiento de `mail.thread`, incluido el historial del chatter.
2. `tracking=True` registra los cambios de estado con el valor anterior y el nuevo en el chatter.

### Paso 3. Equipos del préstamo

1. `prestamo.linea` es el modelo de las líneas. `prestamo_id` es el campo inverso que enlaza cada línea con su préstamo.
2. Al borrar un préstamo, se eliminan sus líneas mediante `ondelete="cascade"` en `prestamo_id`.

### Paso 4. Flujo de estados

1. Ocultar un botón afecta la interfaz. El método también puede invocarse mediante RPC o desde código, así que verifica el estado en el servidor.
2. El acceso encadenado reúne los registros de equipo de las líneas. `write` aplica el mismo estado a todo ese conjunto de registros.

### Paso 5. Reglas del préstamo

1. El dominio filtra las opciones al seleccionarlas. Un equipo puede salir de disponibilidad después de guardar el borrador, por lo que el servidor vuelve a verificarlo al prestar.
2. Odoo llama a `@api.constrains` al crear o actualizar un registro cuando se escriben los campos declarados. La validación de `action_prestar` se ejecuta al intentar entregar el préstamo. La restricción de unicidad también valida cambios directos en las líneas.

### Paso 6. Contacto, kanban y búsqueda

1. Al arrastrar una tarjeta a otra columna, Odoo intenta guardar el estado de la columna destino, porque el kanban está agrupado por `estado`.
2. `prestamo_ids` es un `One2many` inverso. La relación se guarda en la columna `partner_id` de la tabla de préstamos.
