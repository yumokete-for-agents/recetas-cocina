# New Project Boilerplate — Reglas de copia

Al crear un **nuevo proyecto OpenCode**, aplicar este boilerplate mínimo:

## 1. Estructura de directorios

```
proyecto/
├── AGENTS.md
└── .opencode/
    ├── agents/
    │   ├── git-expert.md          # (copiar de proyecto existente)
    │   └── think-and-delegate.md  # (copiar de proyecto existente)
    └── skills/
        └── git-basic-rules/
            └── SKILL.md           # (copiar de proyecto existente)
```

## 2. Origen de cada archivo

| Archivo | Fuente | Dónde está |
|---|---|---|
| `.opencode/agents/git-expert.md` | `04-oc-expert-agents-builder` | `/root/opencode-projects/04-oc-expert-agents-builder/.opencode/agents/git-expert.md` |
| `.opencode/agents/think-and-delegate.md` | `04-oc-expert-agents-builder` | `/root/opencode-projects/04-oc-expert-agents-builder/.opencode/agents/think-and-delegate.md` |
| `.opencode/skills/git-basic-rules/SKILL.md` | `04-oc-expert-agents-builder` | `/root/opencode-projects/04-oc-expert-agents-builder/.opencode/skills/git-basic-rules/SKILL.md` |

## 3. AGENTS.md boilerplate

```markdown
# <Nombre Proyecto>

## Python: siempre usar venv
- Venv: `.venv/` en la raíz del proyecto.
- Activar: `.venv/bin/python` o `.venv/bin/pip`.
- NUNCA ejecutar Python fuera del venv.

## Reglas generales de ejecución

### Bash = último recurso
Preferir tools (Read, Write, Edit, Glob, Grep, Webfetch) antes que bash.

### Bash commands: límite estricto de tamaño
Cualquier comando bash que supere **200 caracteres** o **5 líneas** DEBE escribirse a un archivo temporal y ejecutarse desde ahí.

### Lecciones aprendidas
Usar `/lecciones-aprendidas` al finalizar tareas complejas.

### TodoWrite para tareas complejas
Para tareas con 3+ pasos: crear todolist, solo 1 tarea `in_progress`.

## Routing por agente autoritativo
| Agente | Dominio | Regla |
|---|---|---|
| `git-expert` | Toda operación git/gh (commit, push, tag, branch, merge, rebase, PR) | **Delegar siempre** |
| Cualquier agente | `git status`, `git diff` | Solo lectura — cualquiera puede |

## Skill obligatoria: git-basic-rules
- `.opencode/skills/git-basic-rules/`: todos los agentes (excepto `git-expert`) que puedan necesitar git DEBEN cargar esta skill.

## Agentes disponibles
- `.opencode/agents/git-expert.md`: autoridad exclusiva en git/gh. NO edita archivos ni ejecuta otro bash.
- `.opencode/agents/think-and-delegate.md`: agente primario orquestador. Planifica y delega todo mediante Task tool.

## Idioma
- Contenido en español.
```

## 4. Pasos (en orden)

1. `mkdir -p .opencode/agents .opencode/skills/git-basic-rules`
2. Copiar `git-expert.md`, `think-and-delegate.md`, `git-basic-rules/SKILL.md`
3. Crear `AGENTS.md` con el boilerplate adaptado
4. Crear venv si el proyecto usa Python: `python3 -m venv .venv`
5. `git init && git add -A && git commit -m "chore: initial boilerplate"`
6. Preguntar al usuario por remote antes de push
