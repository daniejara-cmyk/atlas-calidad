# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: tests\clientes.spec.js >> CP-E2E-05: cerrar sesión vuelve al login
- Location: tests\clientes.spec.js:18:1

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
  3  | // Antes de cada prueba iniciamos sesión (precondición del caso de prueba)
  4  | test.beforeEach(async ({ page }) => {
> 5  |   await page.goto("/login");
     |              ^ Error: page.goto: Protocol error (Page.navigate): Cannot navigate to invalid URL
  6  |   await page.getByTestId("input-nombre-usuario").fill("admin");
  7  |   await page.getByTestId("input-password").fill("admin");
  8  |   await page.getByTestId("button-login").click();
  9  |   await expect(page).toHaveURL(/\/home$/);
  10 | });
  11 |  
  12 | test("CP-E2E-04: el listado de clientes muestra los datos de la empresa", async ({ page }) => {
  13 |   await page.goto("/clientes");
  14 |   await expect(page.getByText("María González")).toBeVisible();
  15 |   await expect(page.getByText("Pedro Morales")).toBeVisible();
  16 | });
  17 |  
  18 | test("CP-E2E-05: cerrar sesión vuelve al login", async ({ page, isMobile }) => {
  19 |   test.skip(isMobile, "En móvil el botón queda dentro del menú lateral");
  20 |   await page.getByTestId("button-layout-logout").click();
  21 |   await expect(page).toHaveURL(/\/login$/);
  22 | });
  23 | 
```