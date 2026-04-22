# Ejemplo: De Caso de Prueba Manual a Playwright

## Caso de Prueba Manual (ISTQB)

**ID:** TC-LOGIN-001  
**Título:** Login exitoso con credenciales válidas

**Precondiciones:**
- Sistema desplegado y accesible
- Usuario registrado: user@test.com / Pass123!

**Pasos:**
1. Navegar a la página de login
2. Ingresar email: user@test.com
3. Ingresar contraseña: Pass123!
4. Click en botón "Iniciar Sesión"

**Resultado Esperado:**
- Usuario redirigido al dashboard
- Mensaje de bienvenida visible
- URL contiene "/dashboard"

---

## Código Playwright Generado

```javascript
import { test, expect } from '@playwright/test';

test.describe('Login', () => {
  test('should login successfully with valid credentials', async ({ page }) => {
    await page.goto('/login');
    
    await page.getByTestId('email-input').fill('user@test.com');
    await page.getByTestId('password-input').fill('Pass123!');
    await page.getByRole('button', { name: 'Iniciar Sesión' }).click();
    
    await expect(page).toHaveURL(/.*dashboard/);
    await expect(page.getByText('Bienvenido')).toBeVisible();
  });
});
```

**Decisiones clave:**
- `getByTestId` para inputs (requiere data-testid en HTML)
- `getByRole` para botón (accesible y semántico)
- Verificación de URL + elemento UI para confirmación robusta

---

## Variante: Sin data-testid

Si el HTML no tiene `data-testid`:

```javascript
test('should login successfully with valid credentials', async ({ page }) => {
  await page.goto('/login');
  
  await page.getByLabel('Email').fill('user@test.com');
  await page.getByLabel('Contraseña').fill('Pass123!');
  await page.getByRole('button', { name: 'Iniciar Sesión' }).click();
  
  await expect(page).toHaveURL(/.*dashboard/);
  await expect(page.getByRole('heading', { name: /bienvenido/i })).toBeVisible();
});
```

---

## Caso Negativo

**ID:** TC-LOGIN-002  
**Título:** Login fallido con credenciales inválidas

```javascript
test('should show error with invalid credentials', async ({ page }) => {
  await page.goto('/login');
  
  await page.getByTestId('email-input').fill('wrong@test.com');
  await page.getByTestId('password-input').fill('WrongPass');
  await page.getByRole('button', { name: 'Iniciar Sesión' }).click();
  
  await expect(page.getByRole('alert')).toContainText('Credenciales incorrectas');
  await expect(page).toHaveURL('/login');
});
```
