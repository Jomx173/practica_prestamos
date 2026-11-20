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
