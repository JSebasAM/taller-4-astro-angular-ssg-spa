# Guía de contribución

## Convención de commits

Este repositorio usa [Conventional Commits](https://www.conventionalcommits.org/es/v1.0.0/).

```
<tipo>(<ámbito opcional>): <descripción en imperativo>

[cuerpo opcional]
```

| Tipo       | Uso                                                 |
| ---------- | --------------------------------------------------- |
| `feat`     | Nueva funcionalidad                                 |
| `fix`      | Corrección de un error                              |
| `docs`     | Cambios solo en documentación                       |
| `ci`       | Cambios en workflows de GitHub Actions              |
| `test`     | Agregar o corregir pruebas                          |
| `chore`    | Mantenimiento, dependencias, configuración          |
| `refactor` | Cambio de código que no corrige ni agrega funciones |

Ejemplos:

```
feat(pokemon): add type filter
ci: add verify job after deploy
docs: update README with demo URL
```

## Flujo de trabajo

1. Trabaja desde la rama `master` (o una rama de feature que se integre a ella).
2. Antes de hacer commit ejecuta:
   ```bash
   cd Client-Angular
   npm run lint
   npm run format:check
   npm test
   ```
3. El push a `master` dispara el pipeline de GitHub Actions (build, deploy y verify del sitio Astro + Angular).
