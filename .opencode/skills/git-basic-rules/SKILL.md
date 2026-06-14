---
name: git-basic-rules
description: "REGLA OBLIGATORIA: Toda operacion git (commit, push, tag, branch, merge, rebase, PRs) DEBE ser delegada a git-expert. Ningun agente puede ejecutar git commands directamente. Cargar esta skill en todos los agentes que puedan necesitar git."
---

# SKILL OBLIGATORIA: Reglas de Git y Delegación

## Regla Fundamental (OBLIGATORIA)

**Toda operación git (commit, push, tag, branch, merge, rebase, PR, clone, stash) DEBE ser delegada al agente `git-expert`.**

Ningún agente (excepto el propio `git-expert`) puede ejecutar comandos `git` o `gh` directamente. La única excepción es `git status` y `git diff` para consultas rápidas de solo lectura.

## Por Qué

1. **Consistencia**: git-expert conoce y aplica las reglas del proyecto (no force push, tags únicos, tags inmutables)
2. **Seguridad**: Evita errores como force push, tags duplicados, o merges mal hechos
3. **Responsabilidad única**: Cada agente se enfoca en su dominio

## Cómo Delegar

Usa el `task` tool o `@git-expert` con la descripción de la operación.

## Tabla de Responsabilidades

| Operación | Responsable | Excepción |
|-----------|-------------|-----------|
| `git status`, `git diff` | Cualquier agente (solo lectura) | Lectura segura |
| `git add`, `git commit` | **git-expert** | Solo si el usuario dice explícitamente "hazlo tú" |
| `git push` | **git-expert** | — |
| `git tag` | **git-expert** | — |
| `git branch`, `git checkout` | **git-expert** | — |
| `git merge`, `git rebase` | **git-expert** | — |
| `gh pr`, `gh issue` | **git-expert** | — |
| `git clone`, `git stash` | **git-expert** | — |
| Editar código fuente | El agente correspondiente | git-expert NO edita |

## Excepción: Órdenes Explícitas del Usuario

Si el usuario dice explícitamente "haz el commit tú" o similar, el agente PUEDE ejecutar git directamente. Pero por defecto, la regla es delegar.

## git-expert NO necesita esta skill

El agente `git-expert` ya tiene estas reglas integradas en su system prompt. Esta skill es para LOS DEMÁS AGENTES, para que sepan que deben delegar.

## Reglas Adicionales

### 1. NUNCA usar `git push --force`

**Prohibido en todas las ramas**, especialmente `main/master`. Si hay errores tras un push: crear commit correctivo.

**Excepción**: Solo si el usuario lo pide explícitamente Y es consciente.

### 2. NUNCA repetir números de versión

Cada tag DEBE ser único. Formato: `X.Y.Z`

### 3. Tags son inmutables

- **Nunca retagger** un commit existente
- Si hay error en un tag, crear uno nuevo con la siguiente versión
