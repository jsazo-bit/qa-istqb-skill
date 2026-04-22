# 🚀 Instalación Rápida para el Equipo

Comparte estas instrucciones con tu equipo QA.

---

## ⚡ Instalación en 1 Comando

```bash
npx skills add https://github.com/jsazo-bit/qa-istqb-skill
```

**¡Eso es todo!** Las skills se instalan automáticamente.

---

## ✅ Verificar Instalación

### Windows (PowerShell):
```powershell
ls ~/.agents/skills/qa-istqb-skill
```

### Mac/Linux:
```bash
ls ~/.agents/skills/qa-istqb-skill
```

Deberías ver:
```
.claude/
  qa-senior-istqb.md
  playwright-automation.md
prompts/
scripts/
README.md
```

---

## 🎯 Usar las Skills

### En VSCode con Copilot:

1. **Abrir chat** (`Ctrl + I` o `Cmd + I`)

2. **Para generar casos de prueba:**
   ```
   @qa-senior-istqb.md
   
   Feature: Login con email y contraseña
   - Validación de campos requeridos
   - Manejo de credenciales inválidas
   - Recordar sesión
   ```

3. **Para automatizar con Playwright:**
   ```
   @playwright-automation.md
   
   TC-001: Login exitoso
   1. Ir a /login
   2. Ingresar email: test@example.com
   3. Ingresar password: Test123!
   4. Click "Iniciar Sesión"
   Esperado: Redirección a /dashboard
   ```

---

## 📊 Qué Obtienes

✅ **Casos consolidados**: 3-7 casos en lugar de 15-20  
✅ **Ejecución rápida**: 60-75% menos tiempo  
✅ **Cobertura completa**: Happy path + negatives + boundaries + edges  
✅ **Código limpio**: Playwright best practices  

---

## 🆘 Problemas Comunes

### "npx no reconocido"
**Solución:** Instalar Node.js desde https://nodejs.org/

### "Skills no se encuentran en @"
**Solución:** Las skills se instalan en `~/.agents/skills/`, no en tu proyecto local. Usa el nombre del archivo directamente:
```
@qa-senior-istqb.md
```

### "Necesito actualizar las skills"
**Solución:**
```bash
npx skills update qa-istqb-skill
```

---

## 📚 Documentación Completa

- [Installation Guide](INSTALLATION.md) - Guía detallada
- [Team Onboarding](TEAM-ONBOARDING.md) - Onboarding 15 min
- [Usage Guide](USAGE.md) - Casos de uso
- [Examples](scripts/example-senior-qa-output.md) - Ejemplos reales

---

## 💬 Soporte

¿Preguntas? Abre un issue en:
https://github.com/jsazo-bit/qa-istqb-skill/issues

---

**Última actualización:** Abril 2026  
**Repositorio:** https://github.com/jsazo-bit/qa-istqb-skill
