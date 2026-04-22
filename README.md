# qa-istqb-skill

Skills para generación y automatización de casos de prueba

🎓 **[Nuevo en el Equipo?](TEAM-ONBOARDING.md)** | ⚡ **[Instalación](INSTALLATION.md)** | 📖 **[Guía de Uso](USAGE.md)** | 🚀 **[Quick Start](QUICKSTART.md)**

## Skills Disponibles

### 1. QA Senior ISTQB (Efficient Mode)
Generación de casos de prueba consolidados y eficientes - mínima cantidad con máxima cobertura.

**Filosofía:** Equipos QA que validan proyectos rápidamente necesitan casos consolidados, no listas exhaustivas.

**Características:**
- ✅ **Consolidación inteligente**: 1 caso valida 2-4 flujos relacionados
- ✅ **Mínimo necesario**: 3-7 casos para features típicas (no 15-20)
- ✅ **Criterio senior**: 10+ años de experiencia aplicada
- ✅ **ISTQB silencioso**: Técnicas aplicadas sin explicaciones teóricas
- ✅ **Cero ruido**: Solo información precisa y ejecutable
- ✅ **Estrictamente pedido**: Se ajusta al prompt sin inventar
- ✅ **Sugiere gaps**: Máximo 2 preguntas críticas
- ✅ **Priorizado por riesgo**: Critical > High > Medium > Low

**Qué obtienes:**
- Casos que cubren happy path + negatives + boundaries + edges
- Rápidos de ejecutar (QA puede validar en minutos)
- Consolidados: Login valida credenciales + sesión + navegación + UI
- Sin redundancias ni casos obvios

**Qué NO obtienes:**
- Un caso por cada validación (demasiado granular)
- Testing combinatorial exhaustivo
- Edge cases de baja probabilidad
- Explicaciones ISTQB

**Archivo:** `.claude/qa-senior-istqb.md`

### 2. Playwright Automation
Transformación de casos de prueba manuales en código automatizado Playwright.
- Código eficiente y mantenible
- Selectores estables (testid > role > label)
- Estructura clara (Arrange-Act-Assert)
- Explicaciones mínimas, código autodocumentado

**Archivo:** `.claude/playwright-automation.md`

## Estructura

- `.claude/` - Configuración de las skills
  - `qa-senior-istqb.md` - Skill para diseño de casos de prueba
  - `playwright-automation.md` - Skill para automatización
- `prompts/` - Plantillas de prompts
  - `generate-test-cases.md` - Generación de casos ISTQB
  - `generate-playwright-tests.md` - Generación de código Playwright
- `scripts/` - Scripts de utilidades
- `Cómo Usar las Skills

### Método Rápido
En tu chat con Claude, referencia la skill que necesitas:

```
@.claude/qa-senior-istqb.md

Genera casos de prueba para [tu funcionalidad]
```

o

```
@.claude/playwright-automation.md

Automatiza estos casos de prueba: [tus casos]
```

### Guías Detalladas
- **[USAGE.md](USAGE.md)**: Guía completa con ejemplos y mejores prácticas
- **[QUICKSTART.md](QUICKSTART.md)**: Inicio rápido en 3 pasos
- **[example-workflow.md](scripts/example-workflow.md)**: Ejemplo paso a paso

## Instalación Rápida

```bash
git clone https://github.com/jsazo-bit/qa-istqb-skill.git
cd qa-istqb-skill
code .
```

📋 **[Guía de Instalación Completa](INSTALLATION.md)** - Paso a paso con troubleshooting y configuración

### Verificar Instalación

Abre el chat de Copilot (`Ctrl + I`) y escribe:
```
@.claude/qa-senior-istqb.md

Genera casos de prueba para login básico
```
### Automatizar con Playwright
Usa la skill **Playwright Automation** y el prompt `generate-playwright-tests.md`
