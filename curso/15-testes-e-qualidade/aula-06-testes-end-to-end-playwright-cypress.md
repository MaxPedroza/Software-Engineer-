# Aula 6 — Testes end-to-end (Playwright/Cypress)

**Duração:** ~25 min · **Módulo 15**

## Objetivo
Automatizar fluxos reais do usuário no navegador com Playwright.

## Teoria
- **E2E** testa o sistema completo (frontend + backend + banco) pelo ponto de vista do usuário. Poucos, focados em **jornadas críticas** (login, criar tarefa, checkout).
- **Playwright** (Microsoft): Chromium, Firefox e WebKit; auto-wait; trace viewer; paralelismo. **Cypress**: alternativa popular, roda dentro do navegador.
- **Locators resilientes**: prefira `getByRole`, `getByLabel`, `getByText` (refletem o que o usuário vê e reforçam acessibilidade) a seletores CSS frágeis; `data-testid` como último recurso.
- Nunca use `sleep`: Playwright espera automaticamente; `expect` faz retentativas (web-first assertions).
- Dados de teste previsíveis; cada teste independente.
- Instalação: `npm init playwright@latest`; execução: `npx playwright test`; relatório: `npx playwright show-report`.

## Exemplo
```ts
// tests/tarefas.spec.ts
import { test, expect } from '@playwright/test';

test.beforeEach(async ({ page }) => {
  await page.goto('http://localhost:5173');
});

test('cria e conclui uma tarefa', async ({ page }) => {
  await page.getByLabel('Nova tarefa').fill('Estudar Playwright');
  await page.getByRole('button', { name: 'Adicionar' }).click();

  const item = page.getByRole('listitem').filter({ hasText: 'Estudar Playwright' });
  await expect(item).toBeVisible();

  await item.getByRole('checkbox').check();
  await expect(item.getByRole('checkbox')).toBeChecked();
});

test('mostra erro quando a API falha', async ({ page }) => {
  await page.route('**/tarefas', route => route.fulfill({ status: 500 }));
  await page.reload();
  await expect(page.getByRole('alert')).toContainText('Erro');
});
```
Versão Python equivalente: `pip install pytest-playwright` e `page.get_by_role("button", name="Adicionar").click()`.

## Exercício
1. Escreva um E2E de login com sucesso e outro com senha errada.
2. Configure `webServer` no `playwright.config.ts` para subir o frontend automaticamente.
3. Rode com `--trace on` e inspecione o trace de um teste.

## Checklist
- [ ] Uso locators por papel/rótulo
- [ ] Evito esperas fixas (`sleep`)
- [ ] Restrinjo E2E às jornadas críticas
