---
name: qa-generate-case
description: Genera casos de prueba automáticamente desde tareas de ClickUp analizando código, commits y criterios de aceptación
---

# QA Generate Case

Genera casos de prueba automáticamente integrando información de ClickUp con análisis de código y commits.

## Objetivo

Automatizar la generación de casos de prueba QA para **una o múltiples tareas** de ClickUp extrayendo:
- ID de ClickUp (para buscar commits relacionados)
- Nombre de la tarea
- Descripción
- Criterios de aceptación (CA-01, CA-02, etc.)

Y combinándolos con:
- Análisis de commits relacionados (usando el ID de ClickUp)
- Cambios en el código fuente (solo lo relacionado al ID)
- Generación de casos de prueba usando qa-istqb-skill

**IMPORTANTE**: El archivo puede contener **MÚLTIPLES TAREAS**. La skill debe procesarlas TODAS, una por una, generando casos de prueba para cada tarea individualmente.

## Flujo de Trabajo

### Paso 1: Solicitar Archivo de Tarea

**IMPORTANTE**: Al invocar esta skill, SIEMPRE solicitar al usuario el archivo con la información de la tarea de ClickUp.

**FORMATOS ACEPTADOS**:
- ✅ Archivo PDF (.pdf)
- ✅ Archivo Excel (.xlsx, .xls)
- ✅ Link de Google Drive a archivo Excel compartido

**NO se aceptan**: Archivos Markdown (.md), texto plano (.txt) o JSON (.json)

Usa `vscode_askQuestions` para pedir:
```
¿Puedes proporcionar el archivo con la información de la tarea de ClickUp?

Formatos aceptados:
- Archivo PDF
- Archivo Excel (.xlsx, .xls)
- Link de Google Drive a archivo Excel compartido

El archivo debe contener:
- ID de ClickUp
- Nombre de la tarea
- Descripción
- Criterios de aceptación
```

### Paso 2: Extraer Información del Archivo

**IMPORTANTE**: El archivo puede contener UNA o MÚLTIPLES tareas. La skill debe:
1. Identificar cuántas tareas hay en el archivo
2. Extraer información de CADA tarea individualmente
3. Procesar cada tarea por separado

Para **CADA TAREA** en el archivo, extraer:

1. **ID de ClickUp**: Buscar patrones como:
   - `868j6fb74` (formato alfanumérico)
   - `CU-xxxxx`
   - `#xxxxx`
   - `Task ID: xxxxx`
   - Cualquier formato de ID de ClickUp
   - **CRUCIAL**: Este ID se usará para buscar commits y acotar el código a analizar

2. **Nombre de la tarea**: Buscar campos como:
   - Columna "Tarea" en Excel
   - "Task Name:"
   - "Título:"
   - Texto después del ID

3. **Descripción**: Buscar sección de descripción:
   - Columna "Descripción" en Excel
   - "Description:"
   - Párrafos explicativos de la tarea

4. **Criterios de Aceptación**: Buscar específicamente:
   - Columna "Criterios de aceptación" en Excel
   - Formato: `CA-01:`, `CA-02:`, `CA-03:`, etc.
   - Formato BDD: `Given...When...Then...`
   - "Acceptance Criteria:"
   - "Criterios de Aceptación:"
   - Lista de items con checkboxes o viñetas

**Ejemplo de estructura esperada en Excel**:

| ID Clickup | Tarea | Descripción | Criterios de aceptación |
|------------|-------|-------------|-------------------------|
| 868j6fb74 | Nuevo tipo "Rendición sin depósito" | Agregar nueva opción... | CA-01: Given que...<br>CA-02: Given que... |
| 868j6fbxp | Visualizar facturas nuevo tipo | Asegurar que las facturas... | CA-01: Given que...<br>CA-02: Given que... |

**Procesamiento**:
- Si el archivo tiene 1 tarea: procesar esa tarea
- Si el archivo tiene N tareas: procesar las N tareas, una por una

### Paso 3: Analizar Código y Commits (POR CADA TAREA)

**CRUCIAL**: Para CADA tarea identificada, buscar cambios relacionados con su ID de ClickUp específico.
Esto permite **acotar la lectura del código** solo a lo relevante para esa tarea, en lugar de leer todo el proyecto.

Para cada tarea con ID = `<CLICKUP_ID>`:

#### Búsqueda en Commits
```bash
git log --all --grep="<CLICKUP_ID>" --oneline
git log --all --grep="<CLICKUP_ID>" --name-only
```

Ejemplo:
```bash
git log --all --grep="868j6fb74" --oneline
git log --all --grep="868j6fb74" --name-only
```

Extraer:
- Mensajes de commit que contienen el ID
- Archivos modificados en esos commits
- Scope de los cambios (controllers, models, views, etc.)

#### Búsqueda en Código
Usar `grep_search` para encontrar referencias al ID en:
- Comentarios en el código
- Nombres de branches
- Documentación

Buscar patrones:
- `// 868j6fb74`
- `<!-- 868j6fb74 -->`
- `# 868j6fb74`
- `/* 868j6fb74 */`

#### Leer Solo Archivos Relevantes
Una vez identificados los archivos modificados en los commits:
- Leer SOLO esos archivos
- Enfocarse en las líneas/funciones modificadas
- NO leer todo el proyecto

**Beneficio**: Si el archivo tiene 10 tareas, solo se analiza el código relacionado con cada tarea específica, no todo el proyecto 10 veces.

### Paso 4: Consolidar Información (POR CADA TAREA)

Para cada tarea procesada, crear un resumen estructurado:

```markdown
## Tarea ClickUp: <ID>

### Información General
- **ID**: <CLICKUP_ID>
- **Nombre**: <TASK_NAME>
- **Descripción**: <DESCRIPTION>

### Criterios de Aceptación
<ACCEPTANCE_CRITERIA>
CA-01: Given...When...Then...
CA-02: Given...When...Then...
CA-03: Given...When...Then...

### Análisis de Cambios

#### Commits Relacionados (con ID: <CLICKUP_ID>)
- <Commit 1>
- <Commit 2>
...

#### Archivos Modificados (solo los del ID específico)
- <File 1>
- <File 2>
...

#### Código Relevante
<Resumen de los cambios más importantes encontrados en esos archivos>
```

**Si hay múltiples tareas**: Repetir este proceso para cada una.

### Paso 5: Generar Casos de Prueba (POR CADA TAREA)

**CRUCIAL**: Invocar la skill `qa-istqb-skill` UNA VEZ POR CADA TAREA.

Leer el archivo:
`c:\Users\herki\Documents\Proyectos\Rendición sin deposito\rendicion-de-facturas-backend\.agents\skills\qa-istqb-skill\prompts\generate-test-cases.md`

Para cada tarea, proporcionar como input:
1. Criterios de aceptación extraídos (CA-01, CA-02, etc.)
2. Código fuente modificado (solo archivos encontrados con el ID)
3. Descripción de la tarea
4. Contexto de los commits (solo los que contienen el ID)

**Formato del Input para qa-istqb-skill** (por tarea):
```
Feature: <TASK_NAME>
ID ClickUp: <CLICKUP_ID>

Description:
<TASK_DESCRIPTION>

Acceptance Criteria:
<ACCEPTANCE_CRITERIA>
CA-01: Given...When...Then...
CA-02: Given...When...Then...

Code Changes (archivos encontrados con el ID <CLICKUP_ID>):
<RELEVANT_CODE>

Commits (que contienen el ID <CLICKUP_ID>):
<COMMIT_MESSAGES>
```

**Iteración**: Si el archivo tiene 5 tareas, invocar qa-istqb-skill 5 veces, una por cada tarea.

### Paso 6: Presentar Resultados

Entregar al QA un documento consolidado con TODAS las tareas:

```markdown
# Casos de Prueba - [Archivo de Tareas ClickUp]

## Resumen General
- **Total de tareas procesadas**: N
- **Tareas**: <ID-1>, <ID-2>, ..., <ID-N>

---

## TAREA 1: <TASK_NAME_1> (<CLICKUP_ID_1>)

### Información de la Tarea
[Resumen de la tarea 1]

### Alcance de Testing
[Archivos y funcionalidades afectadas por ID-1]

### Casos de Prueba Generados
[Casos de prueba de qa-istqb-skill para tarea 1]

### Archivos a Validar
[Lista de archivos modificados para testing de tarea 1]

---

## TAREA 2: <TASK_NAME_2> (<CLICKUP_ID_2>)

### Información de la Tarea
[Resumen de la tarea 2]

### Alcance de Testing
[Archivos y funcionalidades afectadas por ID-2]

### Casos de Prueba Generados
[Casos de prueba de qa-istqb-skill para tarea 2]

### Archivos a Validar
[Lista de archivos modificados para testing de tarea 2]

---

...(repetir para cada tarea)...

---

## Resumen Final

### Total de Casos de Prueba Generados
- Tarea 1: X casos
- Tarea 2: Y casos
- ...
- **TOTAL**: Z casos

### Tiempo Estimado de Ejecución
- Tarea 1: A minutos
- Tarea 2: B minutos
- ...
- **TOTAL**: C minutos
```

---

### Paso 7: Solicitar y Llenar Plantilla de Kualitee

**IMPORTANTE**: Una vez generados todos los casos de prueba, solicitar la plantilla de Kualitee para exportar los casos.

Usar `vscode_askQuestions` para pedir:
```
Los casos de prueba han sido generados exitosamente.

Para importarlos a Kualitee, necesito la plantilla Excel/CSV.

¿Puedes proporcionar la plantilla de Kualitee en blanco?

Formatos aceptados:
- Archivo Excel (.xlsx, .xls)
- Archivo CSV (.csv)

Una vez recibida, la llenaré con los casos de prueba generados.
```

**Estructura esperada de la plantilla Kualitee:**

La plantilla típicamente contiene estas columnas:
- `Test Case ID` - Identificador secuencial del caso de prueba (1, 2, 3...)
- `Build` - Identificador del build/sprint
- `Module` - Módulo del sistema
- `Test Scenario Name` - Nombre del caso de prueba
- `Test Case Summary` - Resumen/descripción del caso
- `Requirement Title` - Título del requisito/tarea
- `Requirement Summary` - Resumen del requisito

**Otras columnas posibles** (dependiendo de la configuración de Kualitee):
- `Priority` - Prioridad del caso (Critical, High, Medium, Low)
- `Test Steps` - Pasos de prueba
- `Expected Result` - Resultado esperado
- `Preconditions` - Precondiciones
- `Test Data` - Datos de prueba
- `Tags` - Etiquetas
- `Assigned To` - Asignado a
- `Status` - Estado

### Procesamiento de la Plantilla

Una vez recibida la plantilla:

1. **Leer la plantilla** (Excel o CSV)
2. **Identificar las columnas** disponibles
3. **Mapear los casos de prueba generados** a las columnas de la plantilla

**Mapeo de campos:**

| Campo de Casos de Prueba | Columna Kualitee | Ejemplo |
|-------------------------|------------------|---------|
| Numeración secuencial | Test Case ID | 1 |
| ID de Tarea ClickUp | Build | 868j6fb74 |
| Módulo/Área afectada | Module | Rendiciones |
| TC-ID + Título | Test Scenario Name | TC-RENDSIN-001: Verificar visualización... |
| Descripción completa | Test Case Summary | Validates: visualización, selección... |
| Nombre de la tarea | Requirement Title | Nuevo tipo "Rendición sin depósito" |
| Descripción de la tarea | Requirement Summary | Agregar nueva opción en "Tipo de Pago"... |
| Priority | Priority | Critical |
| Steps | Test Steps | 1. Acceder al formulario<br>2. Click en Tipo de Pago... |
| Expected Result | Expected Result | Nueva opción visible, seleccionable... |
| Preconditions | Preconditions | Usuario autenticado... |
| Test Data | Test Data | Usuario con perfil de rendición |

4. **Llenar la plantilla** fila por fila con cada caso de prueba
5. **Mantener el formato** original de la plantilla (columnas, encabezados)
6. **Generar archivo de salida** con el mismo formato (Excel o CSV)

### Ejemplo de Llenado

**Plantilla recibida (vacía):**
```csv
Test Case ID,Build,Module,Test Scenario Name,Test Case Summary,Requirement Title,Requirement Summary
```

**Plantilla llena (con casos de prueba):**
```csv
Test Case ID,Build,Module,Test Scenario Name,Test Case Summary,Requirement Title,Requirement Summary
1,868j6fb74,Rendiciones,TC-RENDSIN-001: Verificar visualización de nueva opción,"Validates: Visualización en dropdown, selección funcional, integración con opciones existentes. Priority: Critical","Nuevo tipo ""Rendición sin depósito""","Agregar nueva opción en ""Tipo de Pago"" llamado ""Rendición sin depósito"""
2,868j6fb74,Rendiciones,TC-RENDSIN-002: Validar guardado y persistencia,"Validates: Registro en BD, validaciones backend, integridad de datos. Priority: Critical","Nuevo tipo ""Rendición sin depósito""","Agregar nueva opción en ""Tipo de Pago"" llamado ""Rendición sin depósito"""
3,868j6fbxp,Facturas,TC-VISFAC-001: Verificar visualización de facturas,"Validates: Renderizado, datos mostrados, performance. Priority: Critical",Visualizar facturas nuevo tipo rendición,Asegurar que facturas del nuevo tipo se visualizan correctamente
...
```

### Paso 8: Entregar Plantilla Lista

Una vez llenada la plantilla, informar al usuario:

```
✅ Plantilla de Kualitee completada exitosamente

📊 Resumen:
- Total de casos exportados: N
- Tareas incluidas: <ID-1>, <ID-2>, ...
- Archivo generado: casos_prueba_kualitee.xlsx (o .csv)

El archivo está listo para:
1. Descargar
2. Importar directamente a Kualitee
3. Comenzar a trabajar los casos de prueba en la plataforma

Próximos pasos:
1. Descarga el archivo generado
2. Accede a Kualitee
3. Importa el archivo usando la función de importación
4. Verifica que los casos se cargaron correctamente
5. Asigna los casos al equipo de QA
```

---

## Formato de Archivo Esperado

**IMPORTANTE**: Los QA solo manejan archivos PDF y Excel. Esta skill está diseñada para estos formatos.

### Formato 1: Archivo PDF
Archivo PDF exportado desde ClickUp o cualquier herramienta de gestión de tareas que contenga:
- ID de la tarea (CU-XXXXX o similar)
- Nombre/título de la tarea
- Descripción
- Criterios de aceptación (listados o en bullet points)

**Procesamiento**:
- Usar herramientas de lectura de PDF para extraer texto
- Buscar patrones de ID, secciones de descripción y criterios de aceptación

### Formato 2: Archivo Excel (.xlsx, .xls)
Archivo Excel con información estructurada de la tarea:

**Opción A - Una hoja con campos clave-valor**:
| Campo | Valor |
|-------|-------|
| ID | CU-12345 |
| Nombre | Implementar validación de correo |
| Descripción | Agregar validación de formato... |
| Criterio 1 | El campo email debe validar formato válido |
| Criterio 2 | Mostrar mensaje de error si el formato es inválido |
| ... | ... |

**Opción B - Formato de tabla de tareas (MÚLTIPLES TAREAS)**:
| ID Clickup | Tarea | Descripción | Criterios de aceptación |
|------------|-------|-------------|-------------------------|
| 868j6fb74 | Nuevo tipo "Rendición sin depósito" | Agregar nueva opción... | CA-01: Given que...<br>CA-02: Given que... |
| 868j6fbxp | Visualizar facturas nuevo tipo | Asegurar que las facturas... | CA-01: Given que...<br>CA-02: Given que... |

**IMPORTANTE**: Este formato permite múltiples tareas en un solo archivo. La skill procesará TODAS las filas, una por una.

**Procesamiento**:
- Leer archivo Excel usando herramientas apropiadas
- Identificar TODAS las filas con tareas (cada fila = una tarea)
- Para cada fila: extraer ID, Tarea, Descripción, Criterios
- Procesar cada tarea individualmente

### Formato 3: Link de Google Drive a Excel
Link compartido de Google Drive a archivo Excel:

**Ejemplo**: `https://docs.google.com/spreadsheets/d/[ID]/edit?usp=sharing`

**Procesamiento**:
1. Verificar que el link tiene permisos de lectura
2. Usar APIs o herramientas para leer el contenido del archivo
3. Procesar igual que Formato 2 (Excel)

**Requisitos del link**:
- Debe tener permisos de "Cualquiera con el enlace puede ver"
- Debe ser un archivo Excel/Google Sheets
- Debe contener la información de la tarea

---

## Reglas de Extracción

### Patrones de ID de ClickUp
- `868j6fb74` (formato alfanumérico de ClickUp)
- `CU-\d+` (formato CU-12345)
- `#\d{5,}` (formato #12345)
- `Task ID: \w+`
- Cualquier combinación de letras y números (8-12 caracteres)

### Patrones de Criterios de Aceptación
Buscar secciones con:
- `CA-01:`, `CA-02:`, `CA-03:` (formato común de CAs)
- Formato BDD: `Given...When...Then...`
- `Acceptance Criteria`
- `Criterios de Aceptación`
- `AC:`
- Listas precedidas por `- [ ]`, `- ✓`, `•`, `1.`, `-`

### Procesamiento de Commits
1. Buscar commits con el ID en el mensaje
2. Si no hay commits con ID, buscar commits en el rango de fechas de la tarea
3. Filtrar commits por archivos modificados relevantes al proyecto

---

## Limitaciones y Alcance

### ✅ Esta skill SE LIMITA a:
- Extraer información de la tarea de ClickUp
- Analizar commits y código relacionados
- Generar casos de prueba para ESA tarea específica

### ❌ Esta skill NO debe:
- Generar casos de prueba para otras tareas
- Crear tests de regresión completos
- Modificar código o commits
- Ejecutar los casos de prueba

---

## Ejemplo Completo de Uso

**Usuario ejecuta:**
```
Invocar skill: clickup-test-generator
```

**Skill pregunta:**
```
¿Puedes proporcionar el archivo con la información de la tarea de ClickUp?
```

**Usuario proporciona archivo Excel:**
```
tareas-sprint-15.xlsx
```

**Contenido del archivo (2 tareas en formato tabla)**:

| ID Clickup | Tarea | Descripción | Criterios de aceptación |
|------------|-------|-------------|-------------------------|
| 868j6fb74 | Nuevo tipo "Rendición sin depósito" | Agregar nueva opción en "Tipo de Pago" llamado "Rendición sin depósito"... | CA-01: Given que el usuario accede al formulario de pagos When selecciona el campo "Tipo de Pago" Then debe visualizar la nueva opción "Rendición sin depósito"<br>CA-02: Given que el usuario selecciona "Rendición sin depósito" When guarda la rendición Then el backend debe registrar correctamente el nuevo tipo |
| 868j6fbxp | Visualizar facturas nuevo tipo rendición | Asegurar que las facturas del nuevo tipo se visualizan correctamente... | CA-01: Given que existen facturas con tipo "Rendición sin depósito" When el usuario accede a la vista Then dichas facturas deben visualizarse correctamente<br>CA-02: Given que se inicia el proceso de aprobación When existen facturas del tipo "Rendición sin depósito" Then el sistema debe agruparlas por usuario |

**Skill ejecuta:**

**ITERACIÓN 1 - TAREA 1 (868j6fb74):**
1. Lee fila 1: ID=868j6fb74, nombre="Nuevo tipo...", descripción, CAs
2. Busca commits: `git log --grep="868j6fb74"`
3. Encuentra 3 commits con archivos: `controllers/tipoRendicion.js`, `routes/pago.js`, `models/rendicion.js`
4. Lee SOLO esos 3 archivos (no todo el proyecto)
5. Consolida información
6. Invoca qa-istqb-skill con los datos de esta tarea
7. Genera 4 casos de prueba para tarea 1

**ITERACIÓN 2 - TAREA 2 (868j6fbxp):**
1. Lee fila 2: ID=868j6fbxp, nombre="Visualizar facturas...", descripción, CAs
2. Busca commits: `git log --grep="868j6fbxp"`
3. Encuentra 2 commits con archivos: `controllers/factura.js`, `views/listaFacturas.js`
4. Lee SOLO esos 2 archivos
5. Consolida información
6. Invoca qa-istqb-skill con los datos de esta tarea
7. Genera 3 casos de prueba para tarea 2

**Output final consolidado:**
```markdown
# Casos de Prueba - Sprint 15 (Rendición sin Depósito)

## Resumen General
- **Total de tareas procesadas**: 2
- **IDs**: 868j6fb74, 868j6fbxp
- **Total de commits analizados**: 5
- **Archivos únicos modificados**: 5

---

## TAREA 1: Nuevo tipo "Rendición sin depósito" (868j6fb74)

### Información de la Tarea
- **ID**: 868j6fb74
- **Nombre**: Nuevo tipo "Rendición sin depósito"
- **Commits encontrados**: 3
- **Archivos modificados**: 
  - controllers/tipoRendicion.js
  - routes/pago.js
  - models/rendicion.js

### Criterios de Aceptación
- CA-01: Given que el usuario accede al formulario de pagos When selecciona el campo "Tipo de Pago" Then debe visualizar la nueva opción "Rendición sin depósito"
- CA-02: Given que el usuario selecciona "Rendición sin depósito" When guarda la rendición Then el backend debe registrar correctamente el nuevo tipo

### Casos de Prueba Generados

**TC-RENDSIN-001**: Verificar visualización de nueva opción "Rendición sin depósito" en formulario
**Priority**: Critical
**Validates**: Visualización en dropdown, integración con opciones existentes, accesibilidad
**Preconditions**: Usuario autenticado en sistema, formulario de pagos cargado
**Test Data**: Usuario con permisos de rendición
**Steps**:
1. Acceder al formulario de informar pago
2. Click en el campo "Tipo de Pago"
3. Verificar que aparece la opción "Rendición sin depósito"
4. Verificar que las opciones existentes siguen presentes
**Expected Result**: 
- Nueva opción "Rendición sin depósito" visible en el dropdown
- Opciones existentes no afectadas
- Opción seleccionable

**TC-RENDSIN-002**: Validar guardado de rendición con tipo "sin depósito" en backend
**Priority**: Critical
**Validates**: Registro en BD, validaciones backend, integridad de datos
**Test Data**: Rendición completa con tipo="Rendición sin depósito"
**Steps**:
1. Completar formulario de rendición
2. Seleccionar tipo "Rendición sin depósito"
3. Ingresar monto y datos requeridos
4. Guardar rendición
5. Consultar BD directamente
**Expected Result**:
- Rendición guardada con tipo correcto
- No errores en backend (verificar logs)
- Tipos existentes no afectados

**TC-RENDSIN-003**: Verificar validaciones de negocio con nuevo tipo
**Priority**: High
**Validates**: Comportamiento igual a rendiciones con depósito, validaciones aplicadas
**Test Data**: Rendiciones válidas e inválidas con nuevo tipo
**Steps**:
1. Crear rendición con tipo "sin depósito" con monto válido
2. Crear rendición con tipo "sin depósito" con monto inválido (negativo, cero)
3. Crear rendición con tipo "sin depósito" sin archivos adjuntos
4. Verificar comportamiento vs tipo "con depósito"
**Expected Result**:
- Mismas validaciones aplicadas a ambos tipos
- Errores mostrados consistentemente
- Comportamiento idéntico salvo diferenciación por tipo

**TC-RENDSIN-004**: Validar diferenciación entre tipos en reportes y listados
**Priority**: Medium
**Validates**: Identificación visual del tipo, filtros, reportes
**Steps**:
1. Crear rendición tipo "sin depósito"
2. Acceder a listado de rendiciones
3. Verificar que se muestra el tipo correcto
4. Aplicar filtro por tipo
**Expected Result**:
- Tipo mostrado claramente
- Filtros funcionan correctamente
- Diferenciación visual clara

### Archivos para Validar
- [ ] controllers/tipoRendicion.js - Lógica de guardado
- [ ] routes/pago.js - Endpoint de creación
- [ ] models/rendicion.js - Modelo de datos

---

## TAREA 2: Visualizar facturas nuevo tipo rendición (868j6fbxp)

### Información de la Tarea
- **ID**: 868j6fbxp
- **Nombre**: Visualizar facturas nuevo tipo rendición
- **Commits encontrados**: 2
- **Archivos modificados**:
  - controllers/factura.js
  - views/listaFacturas.js

### Criterios de Aceptación
- CA-01: Given que existen facturas con tipo "Rendición sin depósito" When el usuario accede a la vista Then dichas facturas deben visualizarse correctamente
- CA-02: Given que se inicia el proceso de aprobación When existen facturas del tipo "Rendición sin depósito" Then el sistema debe agruparlas por usuario

### Casos de Prueba Generados

**TC-VISFAC-001**: Verificar visualización correcta de facturas tipo "sin depósito" en listado
**Priority**: Critical
**Validates**: Renderizado de facturas, datos mostrados, performance
**Preconditions**: Existen facturas con tipo "Rendición sin depósito" en BD
**Test Data**: 3-5 facturas con nuevo tipo, 3-5 facturas con tipo normal
**Steps**:
1. Acceder a vista de todas las facturas
2. Verificar que las facturas tipo "sin depósito" aparecen
3. Verificar que muestran toda la información esperada
4. Comparar con facturas tipo "con depósito"
**Expected Result**:
- Todas las facturas tipo "sin depósito" visibles
- Información completa mostrada (monto, fecha, usuario, estado)
- No errores de renderizado
- Performance aceptable (< 2 segundos)

**TC-VISFAC-002**: Validar agrupación por usuario en proceso de aprobación
**Priority**: Critical
**Validates**: Lógica de agrupación, comportamiento igual a tipo "con depósito"
**Test Data**: 
- Usuario A: 2 facturas "sin depósito", 1 factura "con depósito"
- Usuario B: 3 facturas "sin depósito"
**Steps**:
1. Iniciar proceso de aprobación masiva
2. Verificar agrupación de facturas usuario A
3. Verificar agrupación de facturas usuario B
4. Comparar lógica de agrupación con tipo "con depósito"
**Expected Result**:
- Facturas "sin depósito" agrupadas por usuario
- Mismo comportamiento que tipo "con depósito"
- Separación clara entre usuarios
- Agrupación no mezcla tipos

**TC-VISFAC-003**: Verificar integración con funcionalidades existentes
**Priority**: High
**Validates**: Filtros, ordenamiento, búsqueda, exportación
**Steps**:
1. Aplicar filtro de búsqueda a facturas "sin depósito"
2. Ordenar por fecha/monto
3. Exportar facturas a Excel
4. Verificar paginación
**Expected Result**:
- Todas las funcionalidades existentes funcionan
- No errores con nuevo tipo
- Datos exportados correctos

### Archivos para Validar
- [ ] controllers/factura.js - Lógica de listado y agrupación
- [ ] views/listaFacturas.js - Vista de renderizado

---

## Resumen Final

### Métricas de Testing
- **Total de tareas**: 2
- **Total de casos de prueba**: 7 casos
  - Tarea 1 (868j6fb74): 4 casos
  - Tarea 2 (868j6fbxp): 3 casos
- **Distribución por prioridad**:
  - Critical: 4 casos
  - High: 2 casos
  - Medium: 1 caso

### Tiempo Estimado de Ejecución
- Tarea 1: 10-12 minutos
- Tarea 2: 8-10 minutos
- **Total**: 18-22 minutos

### Archivos Totales a Validar
- controllers/tipoRendicion.js
- routes/pago.js
- models/rendicion.js
- controllers/factura.js
- views/listaFacturas.js

### Cobertura
- ✅ Todos los criterios de aceptación cubiertos
- ✅ Validación frontend y backend
- ✅ Casos positivos y negativos
- ✅ Integración con funcionalidades existentes
```

**TC-002**: Rechazar correos con formato inválido
...

## Archivos para Validar
- controllers/auth.js (líneas 45-67)
- utils/validators.js (líneas 12-28)
```

---

## Integración con qa-istqb-skill

Esta skill es un **wrapper** que prepara el contexto para qa-istqb-skill.

**Flujo:**
1. `qa-generate-case` → Extrae info de ClickUp + código
2. `qa-generate-case` → Prepara input estructurado
3. `qa-istqb-skill` → Genera casos de prueba eficientes
4. `qa-generate-case` → Presenta resultados con contexto

---

## Notas para el QA

- **Un solo comando**: Solo necesitas invocar esta skill
- **Proporciona el archivo**: Cuando se te pida, adjunta el archivo de ClickUp
- **Revisa el alcance**: Verifica que los archivos analizados son correctos
- **Valida los ACs**: Confirma que todos los criterios fueron considerados

---

## Comandos de Terminal Usados

La skill puede ejecutar estos comandos automáticamente:

```bash
# Buscar commits por ID
git log --all --grep="CU-xxxxx" --oneline

# Ver archivos modificados
git log --all --grep="CU-xxxxx" --name-only --pretty=format:

# Ver contenido de commits
git log --all --grep="CU-xxxxx" -p

# Buscar referencias en código
git log --all -S"CU-xxxxx" --oneline
```

---

## Configuración

Si necesitas personalizar patrones de búsqueda, modifica:

```markdown
### Custom Patterns (Opcional)

ID Pattern: `CUSTOM-\d+`
AC Pattern: `Custom Criteria:`
Commit Pattern: `[CUSTOM-\d+]`
```

---

## Troubleshooting

**Problema**: No se encuentra el ID en commits
- **Solución**: Buscar por nombre de tarea o por rango de fechas

**Problema**: El archivo no tiene formato claro
- **Solución**: Pedir al usuario que especifique manualmente los criterios de aceptación

**Problema**: Demasiados archivos modificados
- **Solución**: Filtrar solo por archivos en las carpetas relevantes (controllers, models, routes)

---

## Versión

1.0.0

## Autor

Created for QA Team - Integration with qa-istqb-skill

## Licencia

MIT
