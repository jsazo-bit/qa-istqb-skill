# Instalación de QA-ISTQB Skills en Visual Studio Code

Guía paso a paso para instalar y usar las skills de generación de casos de prueba y automatización con Playwright.

---

## Prerrequisitos

Antes de comenzar, asegúrate de tener instalado:

- ✅ **Visual Studio Code** (versión 1.85 o superior)
- ✅ **Git** (para clonar el repositorio)
- ✅ **GitHub Copilot** (extensión de VSCode) - [Instalar aquí](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot)

---

## Instalación Paso a Paso

### 1. Clonar el Repositorio

Abre una terminal (PowerShell, CMD, o Terminal de VSCode) y ejecuta:

```bash
cd Documents  # o la carpeta donde quieras guardar las skills
git clone https://github.com/jsazo-bit/qa-istqb-skill.git
```

Esto creará una carpeta `qa-istqb-skill` con todas las skills.

---

### 2. Verificar Estructura de Archivos

Navega a la carpeta y verifica que existan estos archivos:

```
qa-istqb-skill/
├── .claude/
│   ├── qa-senior-istqb.md          ← Skill para casos de prueba
│   └── playwright-automation.md     ← Skill para automatización
├── prompts/
│   ├── generate-test-cases.md
│   └── generate-playwright-tests.md
├── scripts/
│   └── example-workflow.md
├── README.md
├── USAGE.md
└── QUICKSTART.md
```

---

### 3. Abrir en Visual Studio Code

Opción A - Desde la terminal:
```bash
cd qa-istqb-skill
code .
```

Opción B - Desde VSCode:
1. `File` → `Open Folder`
2. Selecciona la carpeta `qa-istqb-skill`

---

### 4. Verificar GitHub Copilot

1. Abre el panel de Copilot:
   - **Windows/Linux**: `Ctrl + I`
   - **Mac**: `Cmd + I`

2. Si no tienes Copilot instalado:
   - Ve a Extensions (`Ctrl + Shift + X`)
   - Busca "GitHub Copilot"
   - Click en "Install"
   - Inicia sesión con tu cuenta de GitHub

---

### 5. Probar la Instalación

#### Test 1: Generar Casos de Prueba

1. Abre el chat de Copilot (`Ctrl + I`)
2. Escribe `@` y verás una lista de archivos
3. Selecciona `.claude/qa-senior-istqb.md`
4. Escribe después:
   ```
   Genera casos de prueba para un formulario de registro con:
   - Nombre, email, contraseña
   - Validación de email único
   - Contraseña mínimo 8 caracteres
   ```
5. Presiona Enter

**Resultado esperado:** Claude generará casos de prueba siguiendo principios ISTQB, sin explicaciones innecesarias.

#### Test 2: Generar Código Playwright

1. Abre el chat de Copilot (`Ctrl + I`)
2. Escribe:
   ```
   @.claude/playwright-automation.md
   
   Automatiza este caso:
   TC-001: Login exitoso
   1. Ir a /login
   2. Ingresar email: test@example.com
   3. Ingresar contraseña: Pass123
   4. Click en "Iniciar Sesión"
   5. Verificar redirección a /dashboard
   ```
3. Presiona Enter

**Resultado esperado:** Claude generará código Playwright limpio y eficiente.

---

## Configuración Opcional (Recomendada)

### A. Crear Workspace Settings

Para que las skills estén siempre disponibles en este proyecto, crea o edita `.vscode/settings.json`:

```json
{
  "github.copilot.enable": {
    "*": true,
    "markdown": true
  },
  "files.associations": {
    "*.md": "markdown"
  }
}
```

### B. Crear Snippets para Uso Rápido

Crea `.vscode/snippets.code-snippets`:

```json
{
  "Load QA ISTQB Skill": {
    "prefix": "qa-istqb",
    "body": [
      "@.claude/qa-senior-istqb.md",
      "",
      "${1:Describe la funcionalidad aquí}"
    ],
    "description": "Cargar skill de casos de prueba ISTQB"
  },
  "Load Playwright Skill": {
    "prefix": "qa-playwright",
    "body": [
      "@.claude/playwright-automation.md",
      "",
      "${1:Pega tus casos de prueba aquí}"
    ],
    "description": "Cargar skill de automatización Playwright"
  }
}
```

Ahora puedes escribir `qa-istqb` o `qa-playwright` en el chat y autocompletar.

---

## Uso Diario

### Método 1: Referencia Directa (Más Común)

En el chat de Copilot:

```
@.claude/qa-senior-istqb.md

[Tu descripción de funcionalidad]
```

### Método 2: Con Prompts Predefinidos

```
@.claude/qa-senior-istqb.md
@prompts/generate-test-cases.md

[Tu código o criterios de aceptación]
```

### Método 3: En Comentarios del Código

Dentro de un archivo `.spec.js`:

```javascript
// @.claude/playwright-automation.md
// Automatiza el flujo de checkout
```

Luego usa Copilot Inline (`Ctrl + I` con cursor en la línea) y pedirá generar el código.

---

## Trabajar en Equipo

### Actualizar Skills

Cuando el equipo actualice las skills en GitHub:

```bash
cd qa-istqb-skill
git pull origin main
```

### Compartir Mejoras

Si mejoras una skill:

```bash
git add .
git commit -m "improvement: [descripción]"
git push origin main
```

---

## Troubleshooting

### ❌ "No encuentro el archivo al escribir @"

**Solución:** Asegúrate de haber abierto la carpeta `qa-istqb-skill` como workspace en VSCode.

1. `File` → `Open Folder`
2. Selecciona `qa-istqb-skill`

---

### ❌ "Claude no sigue las instrucciones de la skill"

**Solución:** Verifica que el archivo se haya referenciado correctamente:

```
@.claude/qa-senior-istqb.md  ✅ Correcto

.claude/qa-senior-istqb.md   ❌ Falta el @
qa-senior-istqb.md           ❌ Falta la ruta
```

---

### ❌ "GitHub Copilot no está activo"

**Solución:**

1. Click en el ícono de Copilot en la barra inferior de VSCode
2. Verifica que tu suscripción esté activa
3. Si dice "Copilot is inactive", inicia sesión nuevamente

---

### ❌ "Las skills están en otra carpeta"

**Solución:** Puedes usar rutas absolutas o relativas:

```
@C:/Users/tu-usuario/qa-istqb-skill/.claude/qa-senior-istqb.md
```

O mejor, abre ese folder como workspace.

---

## Atajos de Teclado Útiles

| Acción | Windows/Linux | Mac |
|--------|--------------|-----|
| Abrir chat Copilot | `Ctrl + I` | `Cmd + I` |
| Copilot inline | `Alt + \` | `Option + \` |
| Aceptar sugerencia | `Tab` | `Tab` |
| Ver siguiente sugerencia | `Alt + ]` | `Option + ]` |
| Comandos VSCode | `Ctrl + Shift + P` | `Cmd + Shift + P` |

---

## Recursos Adicionales

- 📖 [Guía de Uso Completa](USAGE.md)
- 🚀 [Quick Start](QUICKSTART.md)
- 💡 [Ejemplo de Flujo Completo](scripts/example-workflow.md)
- 🐛 [Reportar Problemas](https://github.com/jsazo-bit/qa-istqb-skill/issues)

---

## Contacto y Soporte

Si tienes problemas con la instalación o uso de las skills:

1. Revisa la [documentación completa](USAGE.md)
2. Busca en [Issues del repositorio](https://github.com/jsazo-bit/qa-istqb-skill/issues)
3. Crea un nuevo Issue describiendo tu problema
4. Contacta al equipo de QA interno

---

## Checklist de Instalación ✅

Marca cada paso al completarlo:

- [ ] Git instalado
- [ ] VSCode instalado (v1.85+)
- [ ] GitHub Copilot instalado y activo
- [ ] Repositorio clonado
- [ ] Carpeta abierta en VSCode
- [ ] Test 1 exitoso (generar casos de prueba)
- [ ] Test 2 exitoso (generar código Playwright)
- [ ] Workspace settings configurado (opcional)
- [ ] Snippets creados (opcional)

**¡Felicidades! Ya puedes usar las skills de QA-ISTQB** 🎉
