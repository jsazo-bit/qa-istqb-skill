# Onboarding para Nuevos QA del Equipo

Bienvenido al equipo. Esta guía te llevará desde cero hasta usar las skills de QA-ISTQB en 15 minutos.

---

## ⏱️ Tiempo estimado: 15 minutos

---

## Paso 1: Instalar Herramientas (5 min)

### ✅ Visual Studio Code
Si no lo tienes:
1. Ir a https://code.visualstudio.com/
2. Descargar e instalar
3. Abrir VSCode

### ✅ Git
Verificar si está instalado:
```bash
git --version
```

Si no está instalado:
- **Windows**: https://git-scm.com/download/win
- **Mac**: `brew install git` o desde https://git-scm.com/
- **Linux**: `sudo apt install git`

### ✅ GitHub Copilot
1. En VSCode, presiona `Ctrl + Shift + X` (o `Cmd + Shift + X` en Mac)
2. Busca "GitHub Copilot"
3. Click en "Install"
4. Inicia sesión con tu cuenta de GitHub (asegúrate de tener acceso a Copilot)

---

## Paso 2: Clonar Skills (2 min)

Abre una terminal y ejecuta:

```bash
# Navega a tu carpeta de proyectos
cd Documents

# Clona el repositorio
git clone https://github.com/jsazo-bit/qa-istqb-skill.git

# Entra a la carpeta
cd qa-istqb-skill

# Abre en VSCode
code .
```

---

## Paso 3: Primera Prueba (3 min)

### 🧪 Test: Generar Casos de Prueba

1. **Abrir chat de Copilot:**
   - Presiona `Ctrl + I` (Windows/Linux)
   - O `Cmd + I` (Mac)

2. **Escribir en el chat:**
   ```
   @.claude/qa-senior-istqb.md
   
   Genera casos de prueba para un formulario de contacto con:
   - Nombre (obligatorio)
   - Email (obligatorio, válido)
   - Mensaje (obligatorio, máximo 500 caracteres)
   - Botón "Enviar"
   ```

3. **Presionar Enter y esperar**

**✅ Resultado esperado:**
Claude generará casos de prueba incluyendo:
- Casos positivos
- Validaciones de campos
- Límites de caracteres
- Formatos de email
- Sin explicaciones ISTQB innecesarias

---

## Paso 4: Segunda Prueba (3 min)

### 🤖 Test: Generar Código Playwright

1. **En el mismo chat, escribe:**
   ```
   @.claude/playwright-automation.md
   
   Automatiza este caso:
   
   TC-CONTACTO-001: Envío exitoso de formulario
   1. Navegar a /contacto
   2. Llenar nombre: "Juan Pérez"
   3. Llenar email: "juan@test.com"
   4. Llenar mensaje: "Consulta sobre servicios"
   5. Click en "Enviar"
   6. Verificar mensaje "Formulario enviado exitosamente"
   ```

2. **Presionar Enter**

**✅ Resultado esperado:**
Código Playwright limpio como:
```javascript
test('should submit contact form successfully', async ({ page }) => {
  await page.goto('/contacto');
  
  await page.getByLabel('Nombre').fill('Juan Pérez');
  await page.getByLabel('Email').fill('juan@test.com');
  await page.getByLabel('Mensaje').fill('Consulta sobre servicios');
  await page.getByRole('button', { name: 'Enviar' }).click();
  
  await expect(page.getByText('Formulario enviado exitosamente')).toBeVisible();
});
```

---

## Paso 5: Entender la Estructura (2 min)

```
qa-istqb-skill/
├── .claude/                    ← Las skills están aquí
│   ├── qa-senior-istqb.md     ← Para casos de prueba
│   └── playwright-automation.md ← Para automatización
│
├── prompts/                    ← Prompts predefinidos (opcional)
│   ├── generate-test-cases.md
│   └── generate-playwright-tests.md
│
├── scripts/
│   ├── example-workflow.md    ← Ejemplos completos
│   └── playwright.config.example.js
│
└── README.md, USAGE.md, etc.  ← Documentación
```

**Lo importante:**
- Siempre referenciar `.claude/qa-senior-istqb.md` para diseño de casos
- Siempre referenciar `.claude/playwright-automation.md` para automatización
- Usar `@` antes de la ruta del archivo

---

## ✅ Checklist de Onboarding

Marca cada ítem al completarlo:

- [ ] VSCode instalado
- [ ] Git instalado
- [ ] GitHub Copilot activo
- [ ] Repositorio clonado
- [ ] Test 1 exitoso: Casos de prueba generados
- [ ] Test 2 exitoso: Código Playwright generado
- [ ] Estructura de carpetas entendida
- [ ] Leí [USAGE.md](USAGE.md) (al menos sección de ejemplos)

---

## 🎯 Casos de Uso Comunes

### Caso 1: Nueva Feature
**Situación:** Product Manager te da una user story.

**Acción:**
```
@.claude/qa-senior-istqb.md

User Story: Como usuario quiero poder filtrar productos por precio
Criterios:
- Rango de precio con slider
- Botón "Aplicar filtro"
- Resultados se actualizan sin recargar página
```

---

### Caso 2: Automatizar Suite Existente
**Situación:** Tienes 10 casos manuales en Excel/Jira.

**Acción:**
```
@.claude/playwright-automation.md

[Copiar y pegar los casos de prueba]
```

---

### Caso 3: Optimizar Tests Lentos
**Situación:** Tus tests de Playwright son lentos.

**Acción:**
```
@.claude/playwright-automation.md

Optimiza este código eliminando waits innecesarios:
[Pegar código]
```

---

## 🆘 Problemas Comunes

### "No veo el archivo al escribir @"
**Solución:** Asegúrate de abrir la carpeta completa en VSCode:
- `File` → `Open Folder` → Selecciona `qa-istqb-skill`

### "Claude genera código pero no sigue la skill"
**Solución:** Verifica que pusiste el `@` antes de la ruta:
```
✅ @.claude/qa-senior-istqb.md
❌ .claude/qa-senior-istqb.md
```

### "Copilot dice que no está activo"
**Solución:** 
1. Click en ícono de Copilot (barra inferior)
2. Sign in con GitHub
3. Verifica tu suscripción en https://github.com/settings/copilot

---

## 📚 Próximos Pasos

1. **Lee** [USAGE.md](USAGE.md) para casos avanzados
2. **Revisa** [scripts/example-workflow.md](scripts/example-workflow.md) para ver flujos completos
3. **Experimenta** con tus propios casos de prueba
4. **Comparte** mejoras con el equipo

---

## 🤝 Contribuir

Si encuentras formas de mejorar las skills:

1. Edita el archivo `.md` correspondiente
2. Prueba que funcione
3. Commit y push:
   ```bash
   git add .
   git commit -m "improvement: mejor detección de edge cases"
   git push origin main
   ```

---

## 🎉 ¡Listo!

Ya estás preparado para usar las skills. Algunos tips finales:

- **Usa las skills desde el primer día** - Genera casos más completos
- **Sé específico** - Más contexto = mejores resultados
- **Itera** - Si el resultado no es perfecto, pide ajustes
- **Comparte** - Si encuentras patrones útiles, documéntalos

**¿Dudas?** Pregunta al equipo o crea un Issue en GitHub.

---

**Última actualización:** Abril 2026  
**Mantenedor:** [Tu equipo de QA]
