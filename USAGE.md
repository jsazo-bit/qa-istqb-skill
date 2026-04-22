# Guía de Uso de las Skills QA-ISTQB

## ¿Cómo usar las skills?

Las skills son instrucciones especializadas que mejoran la capacidad de Claude para tareas específicas. Para usarlas, debes **cargarlas explícitamente** en tu conversación.

---

## Método 1: Carga Directa (Recomendado)

Copia y pega el contenido de la skill al inicio de tu conversación con Claude:

### Para Casos de Prueba (ISTQB)

```
@.claude/qa-senior-istqb.md

Genera casos de prueba para la funcionalidad de login que incluye:
- Email y contraseña
- Botón "Iniciar Sesión"
- Validación de campos requeridos
- Redirección al dashboard tras login exitoso
```

### Para Automatización (Playwright)

```
@.claude/playwright-automation.md

Convierte estos casos de prueba en código Playwright:

TC-001: Login exitoso
- Navegar a /login
- Ingresar email: user@test.com
- Ingresar contraseña: Pass123
- Click en "Iniciar Sesión"
- Verificar redirección a /dashboard
```

---

## Método 2: Con Prompts Preparados

Usa los prompts de la carpeta `prompts/`:

### Generar Casos de Prueba

```
@.claude/qa-senior-istqb.md
@prompts/generate-test-cases.md

Feature: Checkout de carrito de compras
Aceptación:
- Usuario puede agregar productos al carrito
- Calcular total con impuestos
- Procesar pago con tarjeta
- Enviar confirmación por email
```

### Generar Tests Playwright

```
@.claude/playwright-automation.md
@prompts/generate-playwright-tests.md

TC-CART-001: Agregar producto al carrito
1. Navegar a catálogo de productos
2. Click en producto "Laptop HP"
3. Click en "Agregar al carrito"
4. Verificar contador de carrito muestra "1"
5. Verificar mensaje "Producto agregado"
```

---

## Método 3: Referencia en Prompt

Menciona la skill directamente en tu prompt:

```
Actúa usando la skill "Playwright Automation" del repositorio qa-istqb-skill.

Necesito automatizar el flujo de registro de usuario:
1. Llenar formulario con nombre, email, contraseña
2. Aceptar términos y condiciones
3. Click en "Registrarse"
4. Verificar email de confirmación
```

---

## Ejemplos Prácticos

### Ejemplo 1: Diseño de Casos de Prueba

**Input:**
```
@.claude/qa-senior-istqb.md

Sistema de gestión de facturas. El usuario puede:
- Crear factura con items
- Calcular subtotal e impuestos
- Guardar como borrador o emitir
- Enviar por email al cliente

Genera casos de prueba cubriendo flujos principales y edge cases.
```

**Output esperado:**
Claude generará casos siguiendo principios ISTQB, incluyendo:
- Particiones de equivalencia
- Valores límite
- Casos negativos
- Sin explicaciones teóricas innecesarias

---

### Ejemplo 2: Automatización con Playwright

**Input:**
```
@.claude/playwright-automation.md

TC-FAC-001: Crear factura simple
Precondiciones: Usuario autenticado
1. Click en "Nueva Factura"
2. Seleccionar cliente "ACME Corp"
3. Agregar item: "Servicio Consultoría - $500"
4. Click en "Guardar"
5. Verificar mensaje "Factura creada exitosamente"
6. Verificar factura aparece en listado

Genera código Playwright.
```

**Output esperado:**
Código limpio con:
- Selectores estables
- Assertions claras
- Estructura Arrange-Act-Assert
- Comentarios solo si es necesario

---

## Combinación de Ambas Skills

Puedes usar ambas en secuencia:

```
Fase 1 - Diseño:
@.claude/qa-senior-istqb.md
Diseña casos de prueba para checkout con múltiples métodos de pago.

Fase 2 - Automatización:
@.claude/playwright-automation.md
Toma los casos anteriores y genera código Playwright.
```

---

## Tips para Mejores Resultados

1. **Sé específico**: Proporciona contexto sobre la funcionalidad
2. **Incluye criterios de aceptación**: Ayuda a generar casos relevantes
3. **Menciona tecnologías**: Si usas React, Angular, etc.
4. **Indica selectores disponibles**: Si tienes data-testid, roles ARIA, etc.
5. **Pide iteración**: "Agrega casos para errores de red" o "Optimiza los selectores"

---

## Preguntas Frecuentes

**Q: ¿Las skills se pueden usar en VSCode con Copilot?**  
R: Sí, usa el símbolo `@` para referenciar archivos en el chat de Copilot.

**Q: ¿Funcionan con otras herramientas además de Playwright?**  
R: La skill de automatización está optimizada para Playwright, pero los principios aplican a Selenium, Cypress, etc. Puedes pedir adaptaciones.

**Q: ¿Puedo modificar las skills?**  
R: Sí, son archivos markdown editables. Adapta según tus necesidades.

**Q: ¿Cómo actualizo si hay cambios en el repo?**  
R: `git pull origin main` para obtener las últimas versiones.

---

## Integración en CI/CD

Para uso en pipelines, crea scripts que referencien las skills:

```bash
# Ejemplo: Generar tests desde archivo de casos
cat test-cases.md | claude --skill .claude/playwright-automation.md > tests/generated.spec.js
```

---

## Recursos Adicionales

- **Ejemplo completo**: Ver `scripts/example-workflow.md`
- **Config Playwright**: Ver `scripts/playwright.config.example.js`
- **Issues/Sugerencias**: https://github.com/jsazo-bit/qa-istqb-skill/issues
