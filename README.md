# VEF Framework React Docs

Official documentation site for `vef-framework-react`, built with Docusaurus.

- Site: `https://coldsmirk.github.io/vef-framework-react-docs/`
- Default locale: English
- Simplified Chinese locale: `https://coldsmirk.github.io/vef-framework-react-docs/zh-Hans/`

## Stack

- Docusaurus 3.9.2
- React 19
- TypeScript
- pnpm

## Local Development

Install dependencies:

```bash
pnpm install
```

Start the Chinese site locally:

```bash
pnpm start
```

Start the English site locally:

```bash
pnpm start:en
```

Start the Chinese locale explicitly:

```bash
pnpm start:zh
```

## Build And Preview

Build all locales:

```bash
pnpm build
```

Preview the production build:

```bash
pnpm serve
```

## Repository Structure

```text
docs/                                  # English source docs
i18n/zh-Hans/                          # Chinese translations
src/                                   # Docusaurus pages and theme code
static/                                # Static assets
docusaurus.config.ts                   # Site configuration
sidebars.ts                            # Sidebar config
```

## Notes

- The site is served at `/vef-framework-react-docs/`, with English at the root path and Chinese under `/zh-Hans/`
- Use `pnpm build && pnpm serve` when checking multi-locale output
- This repository is the documentation site only; framework source code lives in the main `vef-framework-react` repository

## Deploy

- Push to `main` to trigger the GitHub Pages workflow
- GitHub Pages is served from `https://coldsmirk.github.io/vef-framework-react-docs/`
