# Quick Start Guide

## Uso Rápido de las Skills

### 1️⃣ Generar Casos de Prueba

```
@.claude/qa-senior-istqb.md

[Describe tu funcionalidad aquí]
```

**Ejemplo:**
```
@.claude/qa-senior-istqb.md

Funcionalidad de búsqueda de productos con:
- Filtros por categoría, precio, marca
- Ordenamiento por relevancia, precio, fecha
- Paginación de resultados
```

---

### 2️⃣ Automatizar con Playwright

```
@.claude/playwright-automation.md

[Pega tus casos de prueba o describe los pasos]
```

**Ejemplo:**
```
@.claude/playwright-automation.md

TC-SEARCH-001: Búsqueda básica
1. Ingresar "laptop" en buscador
2. Click en botón buscar
3. Verificar al menos 10 resultados
4. Verificar que todos contienen "laptop"
```

---

### 3️⃣ Flujo Completo (Diseño + Automatización)

**Paso 1:**
```
@.claude/qa-senior-istqb.md
@prompts/generate-test-cases.md

Feature: Recuperación de contraseña
- Usuario ingresa email
- Sistema envía link de recuperación
- Usuario crea nueva contraseña
```

**Paso 2:**
```
@.claude/playwright-automation.md
@prompts/generate-playwright-tests.md

[Copia los casos generados en Paso 1]
```

---

## Atajos en VSCode

1. **Abrir chat de Copilot**: `Ctrl + I` (Windows) / `Cmd + I` (Mac)
2. **Referenciar archivo**: Escribe `@` y selecciona el archivo
3. **Ejemplo**:
   ```
   @qa-senior-istqb.md diseña casos para login
   ```

---

## Video Tutorial (Próximamente)

[Aquí irá link a video demostrativo]
