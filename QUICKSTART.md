# QA Generate Case - Quick Start

Genera casos de prueba en 3 pasos.

---

## 🚀 Paso 1: Prepara tu Archivo de Tarea

**IMPORTANTE**: Solo archivos PDF y Excel son aceptados (formatos que usan los QA).

Exporta tu tarea de ClickUp en uno de estos formatos:

- ✅ **PDF** (.pdf) - Exportar desde ClickUp o imprimir a PDF
- ✅ **Excel** (.xlsx, .xls) - Exportar o crear manualmente
- ✅ **Google Drive** - Link compartido a archivo Excel/Sheets

### Mínimo Requerido

Tu archivo debe incluir:

**Para PDF**:
```
ID: CU-XXXXX
Tarea: [Nombre]

Descripción:
[Descripción de la tarea]

Criterios de Aceptación:
- Criterio 1
- Criterio 2
- Criterio 3
```

**Para Excel**:
| Campo | Valor |
|-------|-------|
| ID | CU-XXXXX |
| Descripción | ... |
| Criterio 1 | ... |
| Criterio 2 | ... |

### Ejemplo Completo

Ver [example-task.md](example-task.md) para un ejemplo detallado.

---

## 🎯 Paso 2: Invoca la Skill

En GitHub Copilot Chat:

```
@workspace Genera casos de prueba usando qa-generate-case
```

O simplemente:

```
Usa qa-generate-case
```

---

## 📎 Paso 3: Proporciona el Archivo

Cuando la skill te lo solicite:

### Opción A: Adjuntar Archivo PDF o Excel
1. Click en el ícono de adjuntar (📎)
2. Selecciona tu archivo PDF o Excel
3. Envía

### Opción B: Compartir Link de Google Drive
1. Abre tu archivo en Google Drive
2. Click en "Compartir" → "Cualquiera con el enlace puede ver"
3. Copia el enlace
4. Pégalo en el chat
5. Envía

---

## ✅ Resultado

Recibirás:

```markdown
# Casos de Prueba - [Nombre Tarea] (CU-XXXXX)

## Información de la Tarea
- ID: CU-XXXXX
- Nombre: [...]
- Commits encontrados: X
- Archivos modificados: X

## Alcance de Testing
[Archivos y commits analizados]

## Casos de Prueba Generados
[3-7 casos de prueba consolidados]

## Archivos para Validar
[Lista de archivos a testear]
```

---

## 💡 Tips Rápidos

### Para Mejores Resultados:

1. **Incluye el ID en commits**
   ```bash
   git commit -m "feat: add validation - CU-12345"
   ```

2. **Usa formato consistente**
   - Sección "Acceptance Criteria" claramente definida
   - Usa checkboxes `- [ ]` para criterios

3. **Archivo completo**
   - No edites ni resumas
   - Incluye toda la descripción

---

## 🔍 Qué Busca la Skill

### En tu Archivo:
- ✅ ID de ClickUp (CU-XXXXX, #XXXXX, etc.)
- ✅ Nombre/título de la tarea
- ✅ Descripción
- ✅ Criterios de aceptación

### En tu Código:
- ✅ Commits con el ID de ClickUp
- ✅ Archivos modificados en esos commits
- ✅ Referencias al ID en comentarios
- ✅ Código relevante a la tarea

---

## ⚡ Ejemplo Completo (2 minutos)

### 1. Exporta tu tarea como PDF o Excel:

**Ejemplo PDF**: `task-cu-12345.pdf`
```
ID: CU-12345
Tarea: Implementar validación de email

Descripción:
Agregar validación de email en registro

Criterios de Aceptación:
☐ Validar formato de email
☐ Mostrar error si es inválido
☐ Guardar en minúsculas
```

**O Excel**: `task-cu-12345.xlsx`
| Campo | Valor |
|-------|-------|
| ID | CU-12345 |
| Criterio 1 | Validar formato de email |
| Criterio 2 | Mostrar error si es inválido |
| Criterio 3 | Guardar en minúsculas |

### 2. En Copilot Chat:

```
@workspace Genera casos de prueba con qa-generate-case
```

### 3. Adjunta el archivo cuando se te pida

### 4. ¡Listo! 🎉

Recibirás casos de prueba listos para ejecutar.

**BONUS**: Al finalizar, la skill te preguntará si deseas exportar a Kualitee. Si aceptas, solo adjunta la plantilla en blanco y recibirás el archivo listo para importar.

---

## 🐛 Problemas Comunes

### "No se encontró el ID"
✅ Verifica que tu archivo incluye `ID:` o `CU-XXXXX`

### "No se encontraron commits"
✅ Normal si no usaste el ID en commits. La skill buscará por archivos modificados recientemente.

### "Formato no reconocido"
✅ Verifica que sea archivo PDF, Excel o link de Google Drive válido
✅ Asegúrate de incluir las secciones mínimas: ID, Descripción, Criterios de Aceptación

---

## 📚 Más Información

- [README.md](README.md) - Documentación completa
- [SKILL.md](SKILL.md) - Detalles técnicos
- [example-task.md](example-task.md) - Ejemplo de archivo

---

## ⏱️ Tiempo Total

- **Preparar archivo**: 30 segundos
- **Invocar skill**: 5 segundos
- **Adjuntar archivo**: 5 segundos
- **Generación**: 30-60 segundos

**Total: ~2 minutos** ⚡

---

¿Listo para probar? Crea tu archivo y ejecuta:

```
@workspace qa-generate-case
```
