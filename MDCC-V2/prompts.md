<a id="top"></a>
# MDCC V2 — Manual de Prompts (Passo a Passo)

Este arquivo reúne apenas os prompts operacionais do método, em ordem de execução.
Os conteúdos completos do método e das regras estão em `MDCC-V2/MDCC-V2.md`.

---


<a id="prompt-1-1"></a>
### Prompt 1.1 - Análise Inicial do Repositório
```
Analise todo o repositório atual e identifique:
1. Tecnologias já instaladas
2. Estrutura de pastas existente
3. Dependências configuradas
4. Arquivos de configuração presentes

Após análise, crie um relatório em docs/analysis/initial-scan.md com:
- Stack tecnológica identificada
- Configurações existentes
- Sugestões de melhorias
- Dependências faltantes para o MVP
```


<a id="prompt-1-2"></a>
### Prompt 1.2 - Criação do PRD
```
Com base no objetivo do projeto: [DESCREVA SEU PROJETO AQUI]

Crie um PRD completo em docs/prd/product-requirements.md seguindo esta estrutura:

# PRD - [Nome do Projeto]

## 1. Visão do Produto
- Problema a resolver
- Solução proposta
- Público-alvo

## 2. MVP - Funcionalidades Essenciais (Máximo 5)
- [ ] Funcionalidade 1
- [ ] Funcionalidade 2
- [ ] Funcionalidade 3

## 3. Funcionalidades Futuras (Pós-MVP)
- Listar recursos para versões futuras

## 4. Stack Tecnológica
### Frontend:
- Framework: [Next.js/React/Vue]
- UI: [Tailwind/Shadcn/MUI]
- Estado: [Zustand/Redux/Context]

### Backend:
- Runtime: [Node.js/Bun/Deno]
- Framework: [Express/Fastify/Hono]
- Auth: [NextAuth/Supabase Auth/Clerk]

### Database:
- Principal: [Supabase/PostgreSQL/SQLite]
- Cache: [Redis/Memory]

## 5. Requisitos Não-Funcionais
- Performance esperada
- Segurança básica
- Responsividade

## 6. Critérios de Sucesso do MVP
- Métricas de validação
- Prazo: 3 dias
```

---


<a id="prompt-2-1"></a>
### Prompt 2.1 - Planejamento Frontend
```
Baseado no PRD, crie o plano de desenvolvimento frontend em docs/plan/frontend-plan.md:

# Plano de Desenvolvimento Frontend

## Componentes do MVP

### 1. [Nome do Componente]
**Status:** [ ] Aguardando Aprovação | [ ] Aprovado | [ ] Em Desenvolvimento | [ ] Testando | [ ] Concluído

#### Tarefas:
- [ ] **T1.1** - Setup inicial do componente
  - Status: AGUARDANDO_APROVACAO
  - Descrição: [detalhar]
  - Dependências: Nenhuma
  
- [ ] **T1.2** - Implementar lógica principal
  - Status: AGUARDANDO_APROVACAO
  - Descrição: [detalhar]
  - Dependências: T1.1

- [ ] **T1.3** - Estilização e responsividade
  - Status: AGUARDANDO_APROVACAO
  - Descrição: [detalhar]
  - Dependências: T1.2

- [ ] **T1.4** - Testes com Playwright
  - Status: AGUARDANDO_APROVACAO
  - Descrição: [detalhar]
  - Dependências: T1.3

### Ordem de Execução Sugerida:
1. Componentes sem dependências primeiro
2. Componentes de autenticação
3. Componentes de UI principais
4. Integrações
```


<a id="prompt-2-2"></a>
### Prompt 2.2 - Planejamento Backend
```
Baseado no PRD, crie o plano de desenvolvimento backend em docs/plan/backend-plan.md:

# Plano de Desenvolvimento Backend

## APIs do MVP

### 1. Autenticação
**Status:** [ ] Aguardando Aprovação | [ ] Aprovado | [ ] Em Desenvolvimento | [ ] Testando | [ ] Concluído

#### Tarefas:
- [ ] **B1.1** - Setup do sistema de auth
  - Status: AGUARDANDO_APROVACAO
  - Endpoints: POST /auth/register, POST /auth/login, POST /auth/logout
  - Dependências: Database configurado

- [ ] **B1.2** - Middleware de autenticação
  - Status: AGUARDANDO_APROVACAO
  - Descrição: Verificação de JWT/Session
  - Dependências: B1.1

- [ ] **B1.3** - Testes de integração
  - Status: AGUARDANDO_APROVACAO
  - Cobertura: 100% dos endpoints
  - Dependências: B1.2

### 2. [Próximo Módulo]
[Continuar estrutura similar]
```


<a id="prompt-2-3"></a>
### Prompt 2.3 - Planejamento Database
```
Crie o schema do banco de dados em docs/plan/database-schema.md:

# Schema do Banco de Dados

## Configuração Supabase/Convex

### Tabelas do MVP:

#### users
- id: uuid PRIMARY KEY
- email: string UNIQUE NOT NULL
- password_hash: string (se não usar OAuth)
- created_at: timestamp
- updated_at: timestamp

#### [outras_tabelas]

### RLS (Row Level Security) - Supabase:
```sql
-- Políticas de segurança
```

### Migrations:
1. 001_create_users.sql
2. 002_create_[tabela].sql
```

---


<a id="prompt-3-1"></a>
### Prompt 3.1 - Ciclo TDD para Frontend
```
Para a tarefa [ID_TAREFA] do componente [NOME_COMPONENTE]:

Siga o ciclo TDD:

1. RED - Escreva o teste primeiro:
   - Crie o arquivo de teste em tests/e2e/[componente].spec.ts
   - Use Playwright MCP para simular interação real do usuário
   - O teste deve falhar inicialmente

2. GREEN - Implemente o mínimo necessário:
   - Crie o componente com a funcionalidade mínima
   - Faça o teste passar

3. REFACTOR - Melhore o código:
   - Otimize a implementação
   - Mantenha os testes passando
   - Adicione edge cases

Após completar o ciclo:
- Atualize o status da tarefa para TESTANDO
- Documente o resultado em docs/test/[componente]-test.md
- Aguarde minha validação antes de marcar como CONCLUÍDO
```


<a id="prompt-3-2"></a>
### Prompt 3.2 - Ciclo TDD para Backend
```
Para a tarefa [ID_TAREFA] da API [NOME_ENDPOINT]:

Ciclo TDD Backend:

1. RED - Teste de integração primeiro:
   ```typescript
   // tests/api/[endpoint].test.ts
   describe('POST /api/[endpoint]', () => {
     it('should return expected data', async () => {
       // teste que deve falhar
     });
   });
   ```

2. GREEN - Implementação mínima:
   - Crie o endpoint
   - Implemente lógica básica
   - Conecte ao banco se necessário

3. REFACTOR:
   - Adicione validações
   - Melhore tratamento de erros
   - Otimize queries

Use Playwright MCP para testar a API através da UI quando aplicável.
Documente em docs/test/api-[endpoint]-test.md
```

---


<a id="prompt-4-1"></a>
### Prompt 4.1 - Configuração Playwright MCP
```
Configure o Playwright MCP para testes E2E:

1. Inicialize o Playwright com MCP
2. Configure os ambientes de teste (local/staging)
3. Crie os fixtures base em tests/fixtures/

Para cada componente/feature testado:
- Simule o comportamento real do usuário
- Teste casos de sucesso e falha
- Valide acessibilidade básica
- Capture screenshots em caso de falha

Documente todos os testes executados em docs/test/
```


<a id="prompt-4-2"></a>
### Prompt 4.2 - Teste de Fluxo Completo
```
Após implementar [FUNCIONALIDADE], execute teste E2E completo:

1. Teste o fluxo happy path:
   - Login → Ação principal → Validação → Logout

2. Teste edge cases:
   - Dados inválidos
   - Conexão lenta
   - Sessão expirada

3. Gere relatório em docs/test/[funcionalidade]-e2e.md:
   ```markdown
   # Teste E2E - [Funcionalidade]
   
   ## Status: AGUARDANDO_VALIDACAO
   
   ### Cenários Testados:
   - [x] Happy path
   - [x] Erro de validação
   - [ ] Timeout de rede (pendente)
   
   ### Issues Encontradas:
   - Issue #1: [descrição]
   
   ### Melhorias Sugeridas:
   - [sugestão]
   ```
```

---


<a id="prompt-5-1"></a>
### Prompt 5.1 - Checklist de Validação
```
Para cada tarefa marcada como TESTANDO, verifique:

## Checklist de Validação - [Tarefa ID]

### Funcionalidade:
- [ ] Atende aos requisitos do PRD
- [ ] Funciona em diferentes navegadores
- [ ] Responsivo em mobile/tablet/desktop

### Qualidade:
- [ ] Código limpo e comentado
- [ ] Sem console.logs desnecessários
- [ ] Performance aceitável (<3s load)

### Testes:
- [ ] Playwright tests passando
- [ ] Cobertura adequada
- [ ] Edge cases tratados

### Status Final:
- [ ] APROVADO - Marcar como CONCLUÍDO
- [ ] REQUER_AJUSTES - Listar ajustes necessários
```

---


<a id="prompts-especiais"></a>
## PROMPTS ESPECIAIS


<a id="prompt-especial-supabase"></a>
### Database - Supabase
```
Configure Supabase para o projeto:

1. Crie as tabelas conforme schema em docs/plan/database-schema.md
2. Configure RLS (Row Level Security) para todas as tabelas
3. Crie as functions/triggers necessários
4. Configure o cliente Supabase no projeto:
   - Frontend: @supabase/supabase-js
   - Backend: @supabase/supabase-js com service key
5. Implemente helpers para operações comuns
6. Teste as políticas de segurança com Playwright
```

<a id="prompt-especial-convex"></a>
### Database - Convex
```
Configure Convex para o projeto:

1. Inicialize Convex: npx convex dev
2. Crie os schemas em convex/schema.ts
3. Implemente as mutations em convex/mutations/
4. Implemente as queries em convex/queries/
5. Configure autenticação Convex
6. Crie os hooks React para Convex
7. Teste reatividade com Playwright
```

<a id="prompt-especial-deploy"></a>
### Deploy Rápido (Vercel/Netlify)
```
Prepare o projeto para deploy do MVP:

1. Verifique variáveis de ambiente necessárias
2. Configure build commands corretos
3. Otimize bundle size (tree shaking, lazy loading)
4. Configure preview deployments
5. Setup CI/CD básico com testes
6. Documente URLs e acessos em docs/deploy.md
```

---


<a id="comando-inicial-master"></a>
## 🎯 COMANDO INICIAL MASTER

Use este comando para iniciar qualquer projeto:

```
Vamos criar um MVP de [DESCRIÇÃO DO PROJETO] em 3 dias.

1. Analise o repositório atual
2. Crie o PRD focado em MVP (máximo 5 features)
3. Gere os planos modulares (auth sempre primeiro)
4. Aguarde minha aprovação dos planos
5. Inicie desenvolvimento com TDD
6. Use Playwright MCP para todos os testes
7. Documente tudo em docs/

Stack preferida: [Next.js + Supabase + Tailwind] ou [sua stack]

Lembre-se: MVP funcional > Features complexas
```

---

*Método criado para desenvolvimento ágil com Claude Code - Versão 1.0*
