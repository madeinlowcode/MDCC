# MDCC V2 — Pocket Guide

Checklist prático e fluxos essenciais do método + regras.

## Fluxo Geral (3 dias)
1. Repository scan → PRD → Planos (frontend/backend/db)
2. Aprovação → TDD (RED→GREEN→REFACTOR) → Tests (Playwright MCP)
3. Atualizar status → Validação → Deploy (staging) → Documentação

Referências: TDD (MDCC-V2.md#regras-tdd), E2E (MDCC-V2.md#regras-playwright), Status (MDCC-V2.md#regras-status).

## Dia 1 — Fundamentos
- [ ] Scan do repositório e análise inicial (docs/analysis)
- [ ] PRD aprovado (docs/prd/product-requirements.md)
- [ ] Planos modulares criados (docs/plan/)
- [ ] Setup inicial de projeto + testes
- [ ] 30% tarefas core iniciadas

## Dia 2 — Construção
- [ ] 70% funcionalidades MVP implementadas
- [ ] Integração frontend↔backend funcionando
- [ ] Testes básicos rodando (unit + integration)
- [ ] E2E inicial com Playwright MCP

## Dia 3 — Fechamento
- [ ] 100% MVP funcional
- [ ] E2E completos e passando
- [ ] Deploy em staging concluído
- [ ] Documentação essencial pronta

## TDD — Ciclo Rápido
- RED: escreva teste que falha (tests/*) — ver prompts 3.1/3.2 (prompts.md#prompt-3-1)
- GREEN: implemente o mínimo para passar
- REFACTOR: melhore sem quebrar testes

## E2E — Playwright MCP
- [ ] Configurar fixtures e ambiente (local/staging)
- [ ] Happy path: Login → Ação → Validação → Logout
- [ ] Erros: inputs inválidos, timeouts, sessão expirada
- [ ] Acessibilidade básica (teclado, aria, sr)
- [ ] Screenshots em falha

## Status Flow
AGUARDANDO_APROVACAO → APROVADO → EM_DESENVOLVIMENTO → TESTANDO → AGUARDANDO_VALIDACAO → CONCLUÍDO

## Estrutura de Pastas (mínimo)
project/
├─ docs/
│  ├─ analysis/
│  ├─ prd/
│  ├─ plan/
│  └─ test/
├─ src/
├─ tests/
│  ├─ e2e/
│  ├─ integration/
│  └─ unit/
└─ AI.md

## Segurança — Deve Fazer
- [ ] Variáveis sensíveis em .env (nunca em código)
- [ ] RLS/Policies no DB (Supabase)
- [ ] Rate limiting em APIs públicas
- [ ] Separar chaves públicas/serviço
- [ ] Sanitização/validação de entradas

## Deploy — Checklist
- [ ] .env.example atualizado
- [ ] Testes unit/integration/E2E passando
- [ ] README + docs de API atualizados
- [ ] Otimizações de build (lazy, tree shaking, imagens)
- [ ] Status: READY / NOT_READY

## Atalhos
- Método + Regras: MDCC-V2.md#parte-a-metodo
- Regras (TDD/Playwright/Status): MDCC-V2.md#parte-b-regras
- Prompts: prompts.md#top

