<!--
NOTA: Este archivo es SOLO DE REFERENCIA para mostrar el contenido esperado.
En la práctica, los QA deben proporcionar archivos en formato PDF o Excel, 
o un link de Google Drive a un archivo Excel compartido.
-->

# Implementar Validación de Correo Electrónico

**ID**: CU-12345  
**Priority**: High  
**Status**: In Progress  
**Assignee**: Dev Team  
**Due Date**: 2026-04-30

---

## Description

Agregar validación de formato de correo electrónico en el formulario de registro de usuarios. La validación debe aplicarse tanto en el frontend como en el backend para garantizar la integridad de los datos.

### Context

Actualmente, el sistema no valida el formato del correo electrónico antes de guardarlo en la base de datos, lo que ha causado problemas con notificaciones y recuperación de contraseñas.

### Business Value

- Mejorar la calidad de los datos de usuarios
- Reducir errores en el envío de notificaciones
- Evitar registros con correos inválidos
- Cumplir con estándares de validación de datos

---

## Acceptance Criteria

- [ ] El campo email debe validar formato válido según estándar RFC 5322
- [ ] Mostrar mensaje de error específico si el formato es inválido
- [ ] Permitir solo correos con dominio válido
- [ ] Guardar el correo electrónico en minúsculas para evitar duplicados
- [ ] La validación debe ejecutarse en tiempo real (on blur) y al submit
- [ ] Mostrar indicador visual de validación correcta (✓)
- [ ] Prevenir el registro si el email es inválido
- [ ] Validación debe aplicarse también en el backend como medida de seguridad

---

## Technical Details

### Frontend Changes
- Archivo: `src/components/RegisterForm.js`
- Función: `validateEmail(email)`
- Validación en tiempo real con debounce de 300ms

### Backend Changes
- Archivo: `controllers/auth.js`
- Archivo: `utils/validators.js`
- Función: `isValidEmail(email)`
- Response code: 400 para emails inválidos

### Database Impact
- Tabla: `usuarios`
- Campo: `email` (debe ser lowercase antes de insert)

---

## Test Cases Required

- Validar emails válidos (múltiples formatos)
- Rechazar emails sin @
- Rechazar emails sin dominio
- Rechazar emails con caracteres especiales no permitidos
- Verificar conversión a minúsculas
- Validar mensajes de error apropiados
- Verificar que la validación backend funciona independientemente

---

## Dependencies

- Librería de validación: `validator.js` (ya instalada)
- No requiere cambios en la base de datos
- No requiere migración

---

## Risks & Considerations

- **Risk**: Usuarios existentes con emails inválidos no podrán actualizar su perfil
- **Mitigation**: Agregar script de limpieza de datos antes del deploy

---

## Design Mockup

Ver Figma: [Link to design]

---

## Related Tasks

- CU-12340: Implementar validación de contraseñas
- CU-12350: Agregar validación de teléfono

---

## Comments

**Dev Team (2026-04-20)**: Sugerimos usar la librería `validator.js` que ya está en el proyecto para consistencia.

**QA Team (2026-04-21)**: Necesitamos confirmar si la validación debe aplicarse también en el formulario de edición de perfil.

**Product Owner (2026-04-22)**: Sí, la validación debe aplicarse en todos los formularios donde se capture email.

---

## Definition of Done

- [ ] Código implementado y testeado
- [ ] Tests unitarios escritos y pasando
- [ ] Tests de integración completados
- [ ] Code review aprobado
- [ ] Casos de prueba QA ejecutados
- [ ] Documentación actualizada
- [ ] Deploy en ambiente de staging
- [ ] Validación en producción
