# Exportación a Kualitee - Guía Completa

## 📋 Flujo Completo de Uso

### Paso 1: Generar Casos de Prueba

```
@workspace Genera casos de prueba usando qa-generate-case
```

### Paso 2: Proporcionar Archivo de Tareas

Adjuntar PDF/Excel con las tareas de ClickUp.

**Ejemplo de archivo**:
- Tarea 1: 868j6fb74 - Nuevo tipo "Rendición sin depósito"
- Tarea 2: 868j6fbxp - Visualizar facturas nuevo tipo
- Tarea 3: 868j6fcht - Agregar columna para ver rendiciones
- Tarea 4: 868j6fdk1 - Ver columna en Gestión de tesorería

### Paso 3: Revisión de Casos Generados

La skill genera 13 casos de prueba consolidados y presenta el resumen.

### Paso 4: Solicitud de Plantilla Kualitee

```
✅ Casos de prueba generados exitosamente

📊 Resumen:
- Total de tareas: 4
- Total de casos: 13
- Tiempo estimado: 45 minutos

🎯 Exportar a Kualitee

¿Deseas exportar los casos a la plataforma Kualitee?

Si aceptas, necesito que proporciones la plantilla de Kualitee en blanco (Excel o CSV).
Una vez recibida, la llenaré automáticamente con todos los casos generados.

Formatos aceptados:
- Excel (.xlsx, .xls)
- CSV (.csv)
```

### Paso 5: Proporcionar Plantilla Kualitee

Usuario adjunta archivo `plantilla_kualitee.xlsx` (en blanco)

**Estructura de la plantilla**:
```csv
Test Case ID,Build,Module,Test Scenario Name,Test Case Summary,Requirement Title,Requirement Summary,Priority,Test Steps,Expected Result,Preconditions
```

### Paso 6: Llenado Automático

La skill lee la plantilla y llena cada caso de prueba:

**Ejemplo de llenado para TC-RENDSIN-001**:

| Campo | Valor |
|-------|-------|
| Test Case ID | 1 |
| Build | 868j6fb74 |
| Module | Rendiciones |
| Test Scenario Name | TC-RENDSIN-001: Verificar visualización y selección de "Rendición sin depósito" |
| Test Case Summary | Validates: Visualización en dropdown, selección funcional, integración con opciones existentes. Priority: Critical |
| Requirement Title | Nuevo tipo "Rendición sin depósito" |
| Requirement Summary | Agregar nueva opción en "Tipo de Pago" llamado "Rendición sin depósito" |
| Priority | Critical |
| Test Steps | 1. Acceder al módulo "Informar pago"<br>2. Localizar el campo "Tipo de Pago"<br>3. Click en el selector<br>4. Verificar opciones<br>5. Seleccionar "Rendición sin depósito" |
| Expected Result | Nueva opción visible, seleccionable, sin errores de renderizado |
| Preconditions | Usuario autenticado con permisos de rendición |

### Paso 7: Archivo Generado

```
✅ Plantilla de Kualitee completada exitosamente

📊 Resumen de Exportación:
- Archivo generado: casos_prueba_rendicion_sin_deposito.xlsx
- Total de casos exportados: 13
- Tareas incluidas: 868j6fb74, 868j6fbxp, 868j6fcht, 868j6fdk1
- Formato: Excel compatible con Kualitee
- Columnas llenadas: 10/10

📥 El archivo está listo para descargar e importar a Kualitee

Próximos pasos:
1. Descarga el archivo generado
2. Accede a Kualitee → Test Cases → Import
3. Sube el archivo Excel
4. Verifica el mapeo de columnas
5. Importa los casos
6. Asigna al equipo de QA
```

---

## 📊 Ejemplo de Archivo Generado

**Archivo**: `casos_prueba_rendicion_sin_deposito.xlsx`

### Contenido (primeras 3 filas)

```csv
Build,Module,Test Scenario Name,Test Scenario Summary,Requirement Title,Requirement Summary,Priority,Test Steps,Expected Result,Preconditions
868j6fb74,Rendiciones,TC-RENDSIN-001: Verificar visualización y selección de "Rendición sin depósito","Validates: Visualización en dropdown, selección funcional, integración con opciones existentes","Nuevo tipo ""Rendición sin depósito""","Agregar nueva opción en ""Tipo de Pago"" llamado ""Rendición sin depósito""",Critical,"1. Acceder al módulo ""Informar pago""
2. Localizar el campo ""Tipo de Pago""
3. Click en el selector
4. Verificar que aparece ""Rendición sin depósito""
5. Verificar opciones existentes
6. Seleccionar ""Rendición sin depósito""
7. Verificar selección correcta","- Nueva opción visible
- Opciones existentes intactas
- Selección funcional
- Sin errores de renderizado",Usuario autenticado con permisos de rendición
868j6fb74,Rendiciones,TC-RENDSIN-002: Validar guardado y persistencia de rendición con tipo "sin depósito","Validates: Registro en BD, validaciones backend, integridad de datos, no afectación de tipos existentes","Nuevo tipo ""Rendición sin depósito""","Agregar nueva opción en ""Tipo de Pago"" llamado ""Rendición sin depósito""",Critical,"1. Completar formulario de rendición
2. Seleccionar tipo ""Rendición sin depósito""
3. Ingresar monto y adjuntar facturas
4. Guardar rendición
5. Verificar respuesta HTTP
6. Consultar BD directamente
7. Verificar tipo_rendicion
8. Verificar tipos existentes","- Rendición guardada
- tipo_rendicion = ""Rendición sin depósito"" en BD
- Sin errores en logs
- Tipos existentes funcionan",Formulario completo y válido
868j6fbxp,Facturas,TC-VISFAC-001: Verificar visualización correcta de facturas tipo "sin depósito" en vista principal,"Validates: Renderizado, datos mostrados, performance, integración con facturas existentes",Visualizar facturas nuevo tipo rendición,Asegurar que las facturas del nuevo tipo se visualizan correctamente en el sistema,Critical,"1. Acceder a vista de ""Todas las facturas""
2. Verificar facturas tipo ""sin depósito"" aparecen
3. Verificar información completa
4. Comparar con tipo ""con depósito""
5. Verificar tiempo de carga
6. Verificar paginación","- Todas las facturas visibles
- Información completa
- Sin errores de renderizado
- Performance < 3 segundos
- Paginación funcional",Existen facturas con tipo "Rendición sin depósito" en BD
```

---

## 🎯 Importación en Kualitee

### Paso a Paso

#### 1. Acceder a Kualitee
- URL: https://tu-empresa.kualitee.com
- Login con credenciales de QA

#### 2. Navegar a Test Cases
- Menu → Test Management → Test Cases
- Click en botón "Import"

#### 3. Subir Archivo
- Click "Choose File"
- Seleccionar `casos_prueba_rendicion_sin_deposito.xlsx`
- Click "Upload"

#### 4. Mapeo de Columnas

Kualitee mostrará un preview. Verificar que el mapeo sea correcto:

| Columna del Archivo | Campo Kualitee | ✓ |
|---------------------|----------------|---|
| Build | Build | ✓ |
| Module | Module | ✓ |
| Test Scenario Name | Test Case Name | ✓ |
| Test Scenario Summary | Description | ✓ |
| Requirement Title | Requirement | ✓ |
| Priority | Priority | ✓ |
| Test Steps | Steps | ✓ |
| Expected Result | Expected Result | ✓ |
| Preconditions | Preconditions | ✓ |

#### 5. Importar
- Click "Import"
- Esperar confirmación
- Verificar mensaje: "13 test cases imported successfully"

#### 6. Verificación
- Navegar a Test Cases
- Filtrar por Build "868j6fb74"
- Verificar que aparecen 4 casos
- Abrir un caso y verificar contenido completo

#### 7. Asignación
- Seleccionar casos importados
- Click "Bulk Actions" → "Assign"
- Seleccionar QA team members
- Click "Assign"

---

## 🔧 Configuración de la Plantilla

### Plantilla Básica (Mínimo)

```csv
Build,Module,Test Scenario Name,Test Scenario Summary,Requirement Title,Requirement Summary
```

### Plantilla Completa (Recomendada)

```csv
Build,Module,Test Scenario Name,Test Scenario Summary,Requirement Title,Requirement Summary,Priority,Test Steps,Expected Result,Preconditions,Test Data,Tags,Assigned To,Status
```

### Personalización

Si tu instancia de Kualitee usa nombres de columnas diferentes:

1. **Exporta** un caso de prueba desde Kualitee
2. **Usa** ese archivo como plantilla
3. **Borra** las filas de datos (mantén solo headers)
4. **Proporciona** esa plantilla a la skill

La skill se adaptará automáticamente a tus columnas específicas.

---

## 💡 Tips y Mejores Prácticas

### 1. Preparación de Plantilla
- Usa la plantilla exportada directamente desde tu Kualitee
- Asegúrate que esté en blanco (solo headers)
- Verifica que no tenga filas ocultas

### 2. Campos Obligatorios
Kualitee típicamente requiere:
- Build ✓
- Module ✓
- Test Scenario Name ✓

Los demás son opcionales pero recomendados.

### 3. Formato de Pasos
Los pasos se exportan en formato texto con saltos de línea:
```
1. Paso uno
2. Paso dos
3. Paso tres
```

Kualitee los reconoce automáticamente.

### 4. Prioridades
Mapeo estándar:
- Critical → Critical
- High → High
- Medium → Medium
- Low → Low

### 5. Tags Automáticos
La skill puede agregar tags basados en:
- ID de ClickUp (ej: "868j6fb74")
- Módulo (ej: "Rendiciones")
- Tipo de prueba (ej: "Frontend", "Backend")

---

## ❓ Troubleshooting

### Problema: Columnas no coinciden

**Síntoma**: Kualitee no mapea correctamente las columnas

**Solución**: 
1. Exporta un caso desde Kualitee
2. Usa ese archivo como plantilla
3. La skill se adaptará

### Problema: Caracteres especiales

**Síntoma**: Texto con comillas o saltos de línea no se importa bien

**Solución**: 
- La skill escapa automáticamente caracteres especiales
- Si persiste, usa formato Excel (.xlsx) en lugar de CSV

### Problema: Archivo muy grande

**Síntoma**: Kualitee rechaza archivo con 50+ casos

**Solución**:
- Importa en lotes (25 casos por archivo)
- Menciona esto al proporcionar la plantilla

### Problema: Campos vacíos

**Síntoma**: Algunas filas tienen campos en blanco

**Solución**:
- Verifica que la tarea original tenía toda la información
- Campos opcionales pueden estar vacíos (es normal)

---

## 📈 Métricas y Seguimiento

### Post-Importación

Una vez importados los casos en Kualitee:

1. **Asignar** casos al equipo
2. **Crear** test runs
3. **Ejecutar** casos
4. **Reportar** resultados
5. **Generar** métricas de cobertura

### Dashboard Recomendado

- Total de casos por módulo
- Casos por prioridad
- Casos ejecutados vs pendientes
- Pass rate por tarea de ClickUp
- Bugs encontrados por caso

---

## 🎉 Beneficios

### Antes (Manual)
1. Leer tareas de ClickUp
2. Copiar criterios de aceptación
3. Escribir casos en Kualitee uno por uno
4. Formatear pasos y resultados
5. Asignar campos manualmente

**Tiempo**: ~30 minutos por tarea = 2 horas para 4 tareas

### Ahora (Automatizado)
1. Adjuntar archivo PDF de ClickUp
2. Adjuntar plantilla Kualitee
3. Importar archivo generado

**Tiempo**: ~5 minutos total

**Ahorro**: 95% de tiempo

---

## 🚀 Próximos Pasos

Después de importar los casos:

1. ✅ **Revisar** casos importados en Kualitee
2. ✅ **Asignar** a QA team members
3. ✅ **Crear** test run para el sprint
4. ✅ **Ejecutar** casos de prueba
5. ✅ **Reportar** bugs encontrados
6. ✅ **Actualizar** estado en Kualitee
7. ✅ **Generar** reporte de cobertura

---

## 📞 Soporte

Si tienes problemas con la exportación:

1. Verifica que la plantilla tiene el formato correcto
2. Asegúrate que Kualitee acepta importaciones
3. Revisa permisos de usuario en Kualitee
4. Contacta al administrador de Kualitee si persiste

---

**Versión**: 1.0.0  
**Última actualización**: Abril 2026  
**Compatible con**: Kualitee Cloud y On-Premise
