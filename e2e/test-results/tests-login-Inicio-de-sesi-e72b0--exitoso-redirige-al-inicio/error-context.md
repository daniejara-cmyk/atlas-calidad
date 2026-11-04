# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: tests\login.spec.js >> Inicio de sesión >> CP-E2E-01: login exitoso redirige al inicio
- Location: tests\login.spec.js:4:3

# Error details

```
Error: page.goto: Protocol error (Page.navigate): Cannot navigate to invalid URL
Call log:
  - navigating to "/login", waiting until "load"

```

# Test source

```ts
  1  | const { test, expect } = require("@playwright/test");
  2  |  
  3  | test.describe("Inicio de sesión", () => {
  4  |   test("CP-E2E-01: login exitoso redirige al inicio", async ({ page }) => {
> 5  |     await page.goto("/login");
     |                ^ Error: page.goto: Protocol error (Page.navigate): Cannot navigate to invalid URL
  6  |     await page.getByTestId("input-nombre-usuario").fill("admin");
  7  |     await page.getByTestId("input-password").fill("admin");
  8  |     await page.getByTestId("button-login").click();
  9  |  
  10 |     await expect(page).toHaveURL(/\/home$/);
  11 |     await expect(page.getByText("Sesión iniciada")).toBeVisible();
  12 |   });
  13 |  
  14 |   test("CP-E2E-02: login con contraseña incorrecta muestra error", async ({ page }) => {
  15 |     await page.goto("/login");
  16 |     await page.getByTestId("input-nombre-usuario").fill("admin");
  17 |     await page.getByTestId("input-password").fill("clave-equivocada");
  18 |     await page.getByTestId("button-login").click();
  19 |  
  20 |     await expect(page.getByText("Credenciales inválidas").first()).toBeVisible();
  21 |     await expect(page).toHaveURL(/\/login$/);
  22 |   });
  23 |  
  24 |   test("CP-E2E-03: una ruta privada sin sesión redirige al login", async ({ page }) => {
  25 |     await page.goto("/clientes");
  26 |     await expect(page).toHaveURL(/\/login$/);
  27 |   });
  28 | });
  29 | 
```