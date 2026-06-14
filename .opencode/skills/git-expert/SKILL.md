---
name: git-expert
description: >
  Gestión de git para proyectos de recetas: commits, push, pull requests,
  resolución de conflictos, y buenas prácticas. Úsalo para cualquier
  operación git dentro del proyecto.
---

# Git Expert — Proyecto Recetas

## Commits

### Formato de mensajes
```
tipo: descripción breve (max 72 chars)

Cuerpo opcional con detalles si el commit es complejo.
```

**Tipos**:
- `feat:` — nueva receta, skill, o funcionalidad
- `fix:` — corrección de error en receta, script, o documentación
- `docs:` — cambios solo en documentación
- `refactor:` — cambio interno sin cambio funcional
- `chore:` — mantenimiento, dependencias, config

### Reglas
- **No usar `--no-verify` ni `--no-gpg-sign`** a menos que el usuario lo pida explícitamente.
- **No hacer `git commit --amend`** a menos que sea estrictamente necesario (commit falló por hook, y no se ha pusheado).
- **No commitear archivos sensibles** (.env, credentials, tokens).
- Verificar siempre con `git status` y `git diff` antes de commitear.

## Push

- Usar `git push` sin argumentos tras el primer push con `-u`.
- No hacer `git push --force` a `main` sin confirmación explícita del usuario.
- Si el push es rechazado por divergencia: preguntar al usuario antes de hacer pull/rebase.

## Pull Requests

Estructura del cuerpo:
```markdown
## Summary
<1-3 líneas describiendo qué cambia y por qué>

## Changes
- <lista de cambios>
```

- Usar `gh pr create` con HEREDOC para el cuerpo.
- No crear PR sin verificar el diff completo contra la rama base.

## Ramas

- `main` — siempre estable, todo lo que se pusha debe funcionar.
- Para cambios experimentales: crear ramas con nombre descriptivo (`feat/nueva-receta`, `fix/tiempo-coccion`).

## Seguridad

- No modificar `git config` global — solo local al repo si es necesario.
- No exponer tokens ni URLs con credenciales en outputs o commits.
