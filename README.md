# qa-istqb-skill

Skills para generación y automatización de casos de prueba

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
- `.vscode/` - Configuración del workspace

## Uso

### Generar Casos de Prueba (Manual)
Usa la skill **QA Senior ISTQB** y el prompt `generate-test-cases.md`

### Automatizar con Playwright
Usa la skill **Playwright Automation** y el prompt `generate-playwright-tests.md`
