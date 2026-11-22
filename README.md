# Astro on Netlify Platform Starter

[Live Demo](https://astro-platform-starter.netlify.app/)

> **Nota da auditoria (2026-11-22):** este repositório é uma cópia não modificada do template
> [netlify-templates/astro-platform-starter](https://github.com/netlify-templates/astro-platform-starter)
> (nenhum commit do dono da conta). Ainda usa **Astro 4**, que tem vulnerabilidades críticas
> corrigidas só no Astro 7+; veja `docs/auditoria/AUDITORIA-2026-11-22.md`.
>
> - Build: `npm ci && npm run build` (Node 20 recomendado). CI: `.github/workflows/ci.yml` (build + `npm audit` informativo, sem deploy).
> - Não há testes automatizados (o template não traz).
> - Variáveis de ambiente (ver `.env.example`): `PUBLIC_DISABLE_UPLOADS` (`true` desativa upload no Blob Store); `CONTEXT` é definida pela própria Netlify.

A modern starter based on Astro.js, Tailwind, daisyUI, and [Netlify Core Primitives](https://docs.netlify.com/core/overview/#develop) (Edge Functions, Image CDN, Blob Store).

## Astro Commands

All commands are run from the root of the project, from a terminal:

| Command                   | Action                                           |
| :------------------------ | :----------------------------------------------- |
| `npm install`             | Installs dependencies                            |
| `npm run dev`             | Starts local dev server at `localhost:4321`      |
| `npm run build`           | Build your production site to `./dist/`          |
| `npm run preview`         | Preview your build locally, before deploying     |
| `npm run astro ...`       | Run CLI commands like `astro add`, `astro check` |
| `npm run astro -- --help` | Get help using the Astro CLI                     |

## Deploying to Netlify

[![Deploy to Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/netlify-templates/astro-platform-starter)

## Developing Locally

| Prerequisites             |
| :------------------------ |
| [Node.js](https://nodejs.org/) v18.14+. |
| (optional) [nvm](https://github.com/nvm-sh/nvm) for Node version management. |

1. Clone this repository, then run `npm install` in its root directory.

2. For the starter to have full functionality locally (e.g. edge functions, blob store), please ensure you have an up-to-date version of Netlify CLI. Run:

```
npm install netlify-cli@latest -g
```

3. Link your local repository to the deployed Netlify site. This will ensure you're using the same runtime version for both local development and your deployed site.

```
netlify link
```

4. Then, run the Astro.js development server via Netlify CLI:

```
netlify dev
```

If your browser doesn't navigate to the site automatically, visit [localhost:8888](http://localhost:8888).
