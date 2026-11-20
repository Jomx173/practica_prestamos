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
