# QA Generate Case

Genera casos de prueba automáticamente desde **una o múltiples tareas** de ClickUp, integrando criterios de aceptación, análisis de commits y generación inteligente de casos de prueba.

## 🎯 Objetivo

Automatizar completamente el proceso de generación de casos de prueba QA:
1. **Lee** un archivo PDF/Excel con una o múltiples tareas de ClickUp
2. **Analiza** commits y código relacionados con cada ID de ClickUp específico
3. **Genera** casos de prueba para cada tarea usando qa-istqb-skill
4. **Entrega** casos de prueba organizados por tarea, listos para ejecutar

**✨ NUEVO**: Ahora soporta **múltiples tareas en un solo archivo**. La skill procesa cada tarea individualmente, buscando solo el código relacionado con su ID específico.

## ✨ Características

- ✅ **Un solo comando**: El QA solo invoca la skill
- ✅ **Múltiples tareas**: Procesa una o múltiples tareas en un solo archivo
- ✅ **Búsqueda inteligente**: Usa el ID de ClickUp para buscar commits relacionados
- ✅ **Lectura acotada**: Solo lee código relevante a cada ID (no todo el proyecto)
- ✅ **Extracción automática**: Lee ID, nombre, descripción y criterios de aceptación
- ✅ **Análisis de código**: Busca commits y cambios relacionados con cada ID
- ✅ **Integración con qa-istqb-skill**: Genera casos eficientes y consolidados
- ✅ **Múltiples formatos**: Soporta PDF, Excel y links de Google Drive
- ✅ **Output organizado**: Presenta casos agrupados por tarea
- ✅ **Exportación a Kualitee**: Genera plantilla lista para importar a la plataforma (NUEVO)

## 📦 Instalación

La skill ya está instalada en tu workspace en:
- Backend: `.agents/skills/qa-generate-case/`
- Frontend: `.agents/skills/qa-generate-case/`

## 🚀 Uso Rápido

### 1. Invocar la skill

En GitHub Copilot Chat, escribe:
```
@workspace Genera casos de prueba usando qa-generate-case
```

### 2. Proporcionar archivo de ClickUp

Cuando se te solicite, proporciona:
- **Opción A**: Adjunta el archivo PDF o Excel
- **Opción B**: Pega el link de Google Drive al archivo compartido

### 3. Revisar resultados

La skill generará:
- Resumen de la tarea
- Archivos modificados analizados
- Casos de prueba consolidados
- Lista de archivos para validar

### 4. Exportar a Kualitee (Opcional)

Al finalizar la generación, la skill te pedirá la plantilla de Kualitee:

```
¿Deseas exportar los casos a Kualitee?
```

Si aceptas:
1. **Proporciona** la plantilla de Kualitee en blanco (Excel o CSV)
2. **La skill llena** automáticamente la plantilla con todos los casos
3. **Descarga** el archivo listo para importar a Kualitee

---

## 📤 Exportación a Kualitee (NUEVO)

La skill ahora soporta exportación directa a plantillas de Kualitee.

### ¿Qué es Kualitee?

Kualitee es una plataforma de gestión de pruebas que permite importar casos de prueba mediante archivos Excel/CSV.

### Flujo de Exportación

1. **Generación de casos**: La skill genera los casos de prueba normalmente
2. **Solicitud de plantilla**: Al finalizar, pide la plantilla de Kualitee
3. **Llenado automático**: Mapea y llena todos los casos en la plantilla
4. **Archivo listo**: Genera archivo Excel/CSV listo para importar

### Estructura de la Plantilla

La plantilla típica de Kualitee incluye:

| Columna | Descripción | Ejemplo |
|---------|-------------|---------|
| Test Case ID | ID secuencial del caso | 1 |
| Build | ID del build/sprint | 868j6fb74 |
| Module | Módulo del sistema | Rendiciones |
| Test Scenario Name | Nombre del caso | TC-RENDSIN-001: Verificar... |
| Test Case Summary | Descripción completa | Validates: visualización, selección... |
| Requirement Title | Título del requisito | Nuevo tipo "Rendición sin depósito" |
| Requirement Summary | Resumen del requisito | Agregar nueva opción... |

**Columnas opcionales** (si la plantilla las incluye):
- Priority
- Test Steps
- Expected Result
- Preconditions
- Test Data
- Tags
- Assigned To
- Status

### Mapeo Automático

La skill mapea inteligentemente los campos:

```
Casos de Prueba → Plantilla Kualitee
─────────────────────────────────────
Numeración 1-N     → Test Case ID
ID ClickUp         → Build
Módulo detectado   → Module
TC-ID + Título     → Test Scenario Name
Validates + Info   → Test Case Summary
Nombre tarea       → Requirement Title
Descripción tarea  → Requirement Summary
Priority           → Priority
Steps              → Test Steps
Expected Result    → Expected Result
Preconditions      → Preconditions
Test Data          → Test Data
```

### Ejemplo de Exportación

**Input**: 4 tareas con 13 casos de prueba generados

**Output**: Archivo `casos_prueba_kualitee.xlsx`

```csv
Build,Module,Test Scenario Name,Test Scenario Summary,Requirement Title,Requirement Summary
868j6fb74,Rendiciones,TC-RENDSIN-001: Verificar visualización...,"Validates: Visualización, selección. Priority: Critical",Nuevo tipo "Rendición sin depósito",Agregar nueva opción...
868j6fb74,Rendiciones,TC-RENDSIN-002: Validar guardado...,"Validates: Registro BD, integridad. Priority: Critical",Nuevo tipo "Rendición sin depósito",Agregar nueva opción...
868j6fbxp,Facturas,TC-VISFAC-001: Verificar visualización facturas...,"Validates: Renderizado, performance. Priority: Critical",Visualizar facturas nuevo tipo,Asegurar que facturas...
```

### Importar en Kualitee

1. **Descarga** el archivo generado
2. **Accede** a Kualitee
3. **Ve a** Test Cases → Import
4. **Sube** el archivo Excel/CSV
5. **Mapea** las columnas (si es necesario)
6. **Importa** los casos
7. **Verifica** que se cargaron correctamente

### Ventajas

- ✅ **Cero trabajo manual**: No necesitas copiar/pegar casos
- ✅ **Importación directa**: Archivo listo para Kualitee
- ✅ **Preserva formato**: Mantiene estructura de la plantilla
- ✅ **Todos los campos**: Incluye pasos, resultados, datos de prueba
- ✅ **Organizado por tarea**: Fácil de asignar y gestionar

## 📄 Formatos de Archivo Soportados

**IMPORTANTE**: Los QA trabajan exclusivamente con archivos **PDF** y **Excel**. Esta skill está optimizada para estos formatos.

### Formato 1: Archivo PDF

**¿Cómo obtenerlo?**
- Exportar tarea desde ClickUp como PDF
- Imprimir a PDF desde el navegador
- Guardar documento de Word/Google Docs como PDF

**Contenido esperado**:
```
Tarea: Implementar validación de email
ID: CU-12345
Prioridad: High

Descripción:
Agregar validación de formato de correo electrónico en el formulario de registro.

Criterios de Aceptación:
☐ El campo email debe validar formato válido
☐ Mostrar mensaje de error si el formato es inválido
☐ Permitir solo correos con dominio válido
☐ Guardar correo en minúsculas
```

### Formato 2: Archivo Excel (.xlsx, .xls)

**¿Cómo crearlo?**
- Exportar desde ClickUp
- Crear manualmente desde plantilla
- Copiar información a Excel

**Estructura sugerida**:

| Campo | Valor |
|-------|-------|
| ID | CU-12345 |
| Tarea | Implementar validación de email |
| Prioridad | High |
| Descripción | Agregar validación de formato de correo electrónico en el formulario de registro |
| Criterio 1 | El campo email debe validar formato válido |
| Criterio 2 | Mostrar mensaje de error si el formato es inválido |
| Criterio 3 | Permitir solo correos con dominio válido |
| Criterio 4 | Guardar correo en minúsculas |

**O formato de tabla**:

| ID | Tarea | Descripción | Criterios de Aceptación |
|----|-------|-------------|-------------------------|
| CU-12345 | Implementar validación de email | Agregar validación... | 1. Validar formato válido<br>2. Mostrar mensaje de error<br>3. Solo dominios válidos<br>4. Guardar en minúsculas |

### Formato 3: Link de Google Drive (Excel/Sheets)

**¿Cómo compartirlo?**
1. Abrir archivo en Google Drive
2. Click en "Compartir"
3. Configurar "Cualquiera con el enlace puede ver"
4. Copiar el enlace
5. Pegar en el chat cuando se solicite

**Ejemplo de link**:
```
https://docs.google.com/spreadsheets/d/1ABC123xyz.../edit?usp=sharing
```

**Contenido**: Igual que Formato 2 (Excel)

## 📊 Ejemplo de Output

```markdown
# Casos de Prueba - Implementar validación de email (CU-12345)

## Información de la Tarea
- **ID**: CU-12345
- **Nombre**: Implementar validación de email
- **Descripción**: Agregar validación de formato de correo electrónico en el formulario de registro
- **Commits encontrados**: 3
- **Archivos modificados**: 2

## Alcance de Testing

### Archivos Modificados
- `controllers/auth.js` (líneas 45-67)
- `utils/validators.js` (líneas 12-28)

### Commits Relacionados
- `feat(auth): add email validation - CU-12345`
- `test(auth): add email validator tests - CU-12345`
- `fix(auth): handle edge cases in email validation - CU-12345`

## Casos de Prueba Generados

**TC-EMAIL-001**: Validar email con formato correcto
**Priority**: Critical
**Validates**: Formato válido, conversión a minúsculas, guardado correcto
**Test Data**: 
- email = "Test@Example.com"
- email = "user.name+tag@domain.co.uk"
**Steps**:
1. Ingresar email en el formulario de registro
2. Submit formulario
**Expected Result**: 
- Email aceptado
- Guardado como "test@example.com" (minúsculas)
- Usuario creado exitosamente

**TC-EMAIL-002**: Rechazar email con formato inválido
**Priority**: High
**Validates**: Validación de formato, mensajes de error, prevención de guardado
**Test Data**:
- email = "invalid.email"
- email = "@nodomain.com"
- email = "no@domain"
**Steps**:
1. Ingresar email inválido
2. Submit formulario
**Expected Result**:
- Error: "Formato de email inválido"
- Usuario no creado
- Campo email marcado con error

**TC-EMAIL-003**: Validar solo dominios válidos
**Priority**: High
**Validates**: Validación de dominio, rechazo de dominios inválidos
**Test Data**:
- email = "user@invalid-domain"
- email = "user@.com"
**Steps**:
1. Ingresar email con dominio inválido
2. Submit formulario
**Expected Result**:
- Error: "Dominio no válido"
- Usuario no creado

## Archivos para Validar Manualmente
- [ ] `controllers/auth.js` - Validación de email en registro
- [ ] `utils/validators.js` - Función validateEmail()

## Notas Adicionales
- Todos los criterios de aceptación fueron cubiertos
- 3 casos de prueba generados (vs 8-10 casos granulares)
- Tiempo estimado de ejecución: 5-7 minutos
```

---

## 📊 Ejemplo con Múltiples Tareas (NUEVO)

**Escenario**: Archivo Excel con 2 tareas del sprint 15

**Contenido del archivo** `tareas-sprint-15.xlsx`:

| ID Clickup | Tarea | Descripción | Criterios de aceptación |
|------------|-------|-------------|-------------------------|
| 868j6fb74 | Nuevo tipo "Rendición sin depósito" | Agregar nueva opción en "Tipo de Pago"... | CA-01: Given que el usuario accede al formulario...<br>CA-02: Given que el usuario selecciona... |
| 868j6fbxp | Visualizar facturas nuevo tipo | Asegurar que las facturas del nuevo tipo... | CA-01: Given que existen facturas...<br>CA-02: Given que se inicia el proceso... |

**Proceso automático**:

### Tarea 1 (868j6fb74):
1. Busca commits: `git log --grep="868j6fb74"`
2. Encuentra archivos: `controllers/tipoRendicion.js`, `routes/pago.js`
3. Lee SOLO esos archivos
4. Genera 4 casos de prueba

### Tarea 2 (868j6fbxp):
1. Busca commits: `git log --grep="868j6fbxp"`
2. Encuentra archivos: `controllers/factura.js`, `views/listaFacturas.js`
3. Lee SOLO esos archivos
4. Genera 3 casos de prueba

**Output consolidado**:

```markdown
# Casos de Prueba - Sprint 15

## Resumen General
- Total de tareas: 2
- Total de casos: 7
- Tiempo total: 18-22 minutos

---

## TAREA 1: Nuevo tipo "Rendición sin depósito" (868j6fb74)
[4 casos de prueba detallados]

---

## TAREA 2: Visualizar facturas nuevo tipo (868j6fbxp)
[3 casos de prueba detallados]
```

**Ventaja**: La skill aísla el código de cada tarea usando el ID de ClickUp, evitando leer todo el proyecto.

## 🔄 Flujo de Trabajo

```
┌─────────────────────────────────────────────────────────────┐
│ 1. QA invoca la skill qa-generate-case                      │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│ 2. Skill solicita archivo de ClickUp                        │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│ 3. Extrae: ID, nombre, descripción, ACs                     │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│ 4. Busca commits con el ID de ClickUp                       │
│    git log --grep="CU-xxxxx"                                 │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│ 5. Busca referencias al ID en el código                     │
│    grep_search para comentarios y documentación             │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│ 6. Lee archivos modificados relevantes                      │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│ 7. Consolida información en formato estructurado            │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│ 8. Invoca qa-istqb-skill con la información consolidada     │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│ 9. Presenta casos de prueba con contexto completo           │
└─────────────────────────────────────────────────────────────┘
```

## 🎯 Alcance

### ✅ Lo que hace esta skill:
- Extrae información de tareas de ClickUp
- Analiza commits y código relacionados
- Genera casos de prueba específicos para la tarea
- Identifica archivos a validar

### ❌ Lo que NO hace:
- Ejecutar los casos de prueba
- Generar tests de regresión completos
- Modificar código o commits
- Crear pruebas para múltiples tareas simultáneamente

## 🔍 Patrones de Búsqueda

### IDs de ClickUp reconocidos:
- `CU-12345`
- `#12345`
- `Task ID: 12345`
- `ID: CU-12345`

### Secciones de Criterios de Aceptación:
- `Acceptance Criteria`
- `Criterios de Aceptación`
- `AC:`
- Listas con `- [ ]`, `- ✓`, `•`, `1.`, `-`

## 🛠️ Integración con qa-istqb-skill

Esta skill es un **wrapper inteligente** que:
1. Prepara el contexto completo de la tarea
2. Extrae código y commits relevantes
3. Invoca qa-istqb-skill con información estructurada
4. Presenta resultados con contexto adicional

**Beneficio**: El QA solo ejecuta una skill, el resto es automático.

## 💡 Tips para Mejores Resultados

1. **Incluye el ID de ClickUp en tus commits**
   ```bash
   git commit -m "feat(auth): add validation - CU-12345"
   ```

2. **Usa formatos consistentes en ClickUp**
   - Siempre incluye sección de "Acceptance Criteria"
   - Usa checkboxes `- [ ]` para listas

3. **Proporciona el archivo completo**
   - Incluye toda la descripción de la tarea
   - No edites o resumas el contenido

4. **Valida el alcance**
   - Revisa los archivos identificados
   - Confirma que los commits son correctos

## 🐛 Troubleshooting

### Problema: No se encuentran commits
**Solución**: Verifica que usaste el ID de ClickUp en los mensajes de commit. Si no, la skill buscará por archivos modificados recientemente.

### Problema: Formato del archivo no reconocido
**Solución**: Asegúrate de proporcionar un archivo PDF, Excel (.xlsx, .xls) o un link de Google Drive válido. Otros formatos (Markdown, TXT, JSON) no son soportados.

### Problema: Demasiados archivos identificados
**Solución**: La skill filtra automáticamente por carpetas relevantes (controllers, models, routes, components, containers). Si necesitas más filtros, menciónalo.

### Problema: Criterios de aceptación incompletos
**Solución**: Asegúrate que el archivo incluye la sección completa de criterios de aceptación. Si están en otro formato, la skill preguntará.

## 📚 Documentación Adicional

Ver `SKILL.md` para:
- Detalles técnicos completos
- Configuración avanzada
- Personalización de patrones
- Comandos de terminal usados

## 🤝 Dependencias

Esta skill requiere:
- ✅ **qa-istqb-skill**: Instalada en `.agents/skills/qa-istqb-skill/`
- ✅ **Git**: Para análisis de commits
- ✅ **Acceso al workspace**: Para leer código fuente

## 📝 Versión

**1.0.0** - Versión inicial

## 👥 Autor

Created for QA Team

## 📄 Licencia

MIT

---

## 🚦 Quick Start de 30 Segundos

1. **Exporta/Guarda** tu tarea de ClickUp en PDF o Excel
2. **Invoca** `@workspace qa-generate-case`
3. **Adjunta** el archivo o pega el link de Drive cuando se te pida
4. **Recibe** casos de prueba listos para ejecutar

¡Eso es todo! 🎉
