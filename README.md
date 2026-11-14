# Taller 4 · Astro SSG + Angular SPA

[![Deploy to GitHub Pages](https://github.com/JSebasAM/taller-4-astro-angular-ssg-spa/actions/workflows/deploy.yml/badge.svg)](https://github.com/JSebasAM/taller-4-astro-angular-ssg-spa/actions/workflows/deploy.yml)

Monorepo que compara dos formas de renderizar la misma aplicación: un sitio estático generado con **Astro (SSG)** y una **SPA en Angular**. Ambos se publican en un **único sitio** de GitHub Pages con un solo workflow y un solo artefacto.

| Ruta                                                                                                             | Contenido                |
| ---------------------------------------------------------------------------------------------------------------- | ------------------------ |
| [`/taller-4-astro-angular-ssg-spa/`](https://JSebasAM.github.io/taller-4-astro-angular-ssg-spa/)                 | Sitio Astro (SSG)        |
| [`/taller-4-astro-angular-ssg-spa/angular/`](https://JSebasAM.github.io/taller-4-astro-angular-ssg-spa/angular/) | Aplicación Angular (SPA) |

> Captura de pantalla: pendiente de agregar en `docs/screenshot.png` (`![Captura](docs/screenshot.png)`).

## Tecnologías

- Astro 5 (SSG) con Bootstrap 5
- Angular 20 (componentes standalone, routing con hash)
- Jest (pruebas del cliente Angular), ESLint (`angular-eslint`) y Prettier
- GitHub Actions + GitHub Pages

## Estructura

```
.
├── Astro-SSG/        # Sitio estático (astro.config.mjs con site y base)
├── Client-Angular/   # SPA Angular (se publica en /angular/)
└── .github/workflows/deploy.yml
```

## Instalación y scripts

### Astro (`Astro-SSG`)

```bash
cd Astro-SSG
npm ci
npm run dev      # desarrollo
npm run build    # genera dist/
npm run preview  # sirve dist/
```

### Angular (`Client-Angular`)

```bash
cd Client-Angular
npm ci
npm start                 # desarrollo
npm run build             # build de producción
npm test                  # Jest
npm run test:coverage     # Jest con cobertura
npm run compodoc          # documentación
npm run lint              # ESLint
npm run format:check      # Prettier (solo verifica)
```

> El cliente Angular consulta una API en `http://localhost:3000` (`src/environments/environment.ts`). En GitHub Pages no existe ese servidor, por lo que las vistas que dependen de la API no cargarán datos reales.

## Despliegue

El workflow [`deploy.yml`](.github/workflows/deploy.yml) corre en cada push a `master` o manualmente:

1. **build**: construye Angular con `--base-href /taller-4-astro-angular-ssg-spa/angular/` (lint, formato y pruebas incluidos), construye Astro (`site` y `base: '/taller-4-astro-angular-ssg-spa/'`) y copia el resultado de Angular a `Astro-SSG/dist/angular/`. Se sube **un solo artefacto** (`Astro-SSG/dist`).
2. **deploy**: publica en GitHub Pages.
3. **verify**: `curl` con reintentos (~2 min) a `/` (marcador `Astro App`) y a `/angular/` (marcador `<app-root`).

Los enlaces del sitio Astro respetan el `base` (`import.meta.env.BASE_URL`) y el menú incluye un enlace a la SPA.

## Contribuir

Usa [Conventional Commits](CONTRIBUTING.md).
