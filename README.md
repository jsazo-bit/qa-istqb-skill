# qa-istqb-skill

Skills para generación y automatización de casos de prueba

🎓 **[Nuevo en el Equipo?](TEAM-ONBOARDING.md)** | ⚡ **[Instalación](INSTALLATION.md)** | 📖 **[Guía de Uso](USAGE.md)** | 🚀 **[Quick Start](QUICKSTART.md)**

## Skills Disponibles

### 1. QA Senior ISTQB
Generación de casos de prueba siguiendo principios ISTQB.
- Diseño preciso de test cases
- Cobertura basada en riesgos
- Identificación de edge cases
- Enfoque práctico, sin sobre-explicaciones

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
