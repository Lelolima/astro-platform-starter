# Auditoria 2026-11-22 — astro-platform-starter

## Diagnóstico (estado anterior)

- **Origem:** cópia do template `netlify-templates/astro-platform-starter` (não é fork no GitHub). `git log`: 139 commits, todos de mantenedores da Netlify e bots (renovate/dependabot); **nenhum commit do dono da conta** → não há código próprio.
- **Stack:** Astro 4.16, React 18, Tailwind 3 + daisyUI, adaptador Netlify 5 (SSR, Edge Functions, Blobs, Image CDN).
- **Instala/compila:** `npm ci` OK; `npm run build` → `Complete!`.
- **Testes:** nenhum no template.
- **CI:** nenhum workflow (`gh run list` vazio).
- **Segredos:** busca por regex em todo o histórico — nada encontrado (gitleaks indisponível).
- **Dependências:** `npm audit` → **28 vulnerabilidades (2 low, 7 moderate, 17 high, 2 critical)**. As críticas/altas principais estão no próprio `astro` (<=7.4.4: XSS refletido em server islands, bypass de middleware/CSRF, leitura arbitrária de arquivos no dev server, entre outras) e no `sharp`/libvips; a correção exige `astro@7` e `@astrojs/netlify@8` (majors).

| # | Problema | Severidade |
|---|----------|-----------|
| 1 | Astro 4 com vulnerabilidades críticas/altas, correção só em majors | P0 (não corrigido: exige migração) |
| 2 | Vulnerabilidades transitivas com correção compatível | P0 (corrigido) |
| 3 | Sem CI | P2 (corrigido) |
| 4 | README não indica a origem, variáveis de ambiente nem os riscos | P2 (corrigido) |

## Mudanças

- `npm audit fix` (sem `--force`, só versões compatíveis): **28 → 14** vulnerabilidades (7 moderate, 5 high, 2 critical).
- CI: `npm ci` + `npm run build` + `npm audit` informativo; `permissions: contents: read`; actions fixadas por SHA; **sem deploy**.
- README: nota de origem/estado; `.env.example` com `PUBLIC_DISABLE_UPLOADS` (sem segredos).

## Testes executados

- `npm ci` → OK. `npm run build` antes e depois do `audit fix` → `Complete!`.
- `npm audit` antes → 28; depois → 14.

## Riscos residuais e decisões do dono

- As 14 vulnerabilidades restantes (2 críticas) só saem migrando Astro 4 → 7 e adaptadores (o `@astrojs/tailwind` foi descontinuado nas versões novas). Não foi feito porque é uma migração de várias versões major num template sem código próprio, e o upstream da Netlify mantém versões atualizadas.
- Opções: (a) re-sincronizar com o template upstream atual; (b) arquivar o repositório se não for usado; (c) autorizar a migração. Se houver um site Netlify publicado a partir dele, a prioridade é alta (bypass de middleware/XSS são exploráveis em SSR).
