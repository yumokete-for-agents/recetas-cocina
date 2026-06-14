# Recetas Cocina

Repositorio de recetas y conocimientos culinarios, gestionado por OpenCode. Incluye skills especializadas por técnica, un agente guía conversacional, y exportación a DOCX profesional.

## Skills disponibles

| Skill | Descripción |
|---|---|
| **chef-expert** | Mejora de recetas desde URL, exportación a .md y .docx |
| **guisos-carne** | Framework 5 fases para guisos de carne con patatas |
| **olla-presion** | Tiempos P1/P2 y adaptaciones para olla a presión |
| **pescados-guisos** | Guisos de pescado con patatas, perfiles regionales |
| **arroz-guisos** | Arroces secos, melosos y caldosos |
| **salteados-wok** | Técnica de salteado, marinados, salsas base |
| **asados-carne** | Horno, parrilla, barbacoa — cortes, puntos, técnicas |
| **asados-pescado** | Plancha, parrilla, horno, sal — tipos según textura |
| **plancha** | Cocción a la plancha por ingrediente (carnes, pescados, verduras, huevos, tofu, frutas) |
| **pasta-salsas** | Clasificación por base: tomate, nata, aceite, queso, ragùs, pesto |
| **sopas** | Caldos, cremas, purés, sopas frías e internacionales |
| **git-basic-rules** | Reglas de delegación git para agentes |

## Agentes

| Agente | Rol |
|---|---|
| **guia** | Asistente conversacional: sugiere recetas según ingredientes, planifica menús, genera lista de la compra, ayuda con la despensa base |
| **git-expert** | Autoridad exclusiva en git/gh (commit, push, PRs) |
| **think-and-delegate** | Orquestador primario |

## Estructura

```
.opencode/
├── agents/          # Agentes OpenCode
├── skills/          # Skills culinarios
│   ├── chef-expert/
│   │   ├── scripts/generar_docx.py
│   │   └── references/mejora-recetas.md
│   ├── guisos-carne/
│   ├── asados-carne/
│   ├── asados-pescado/
│   ├── pescados-guisos/
│   ├── olla-presion/
│   ├── arroz-guisos/
│   ├── salteados-wok/
│   ├── plancha/
│   ├── pasta-salsas/
│   ├── sopas/
│   └── git-basic-rules/
├── references/       # Documentación de referencia
├── AGENTS.md         # Instrucciones maestras del proyecto
recetas/              # Recetas generadas (.md)
```

## Requisitos

- Python 3.10+ (usar siempre el venv: `.venv/bin/python`)
- Pandoc (`/usr/bin/pandoc` v3.1.3+)
- `python-docx` instalado en el venv

## Uso básico

### Generar DOCX desde JSON

```bash
echo '{"titulo": "...", "raciones": 4, "ingredientes": [["400g", "carne"]], "pasos": [["Dorar", "Cocer..."]]}' \
  | .venv/bin/python .opencode/skills/chef-expert/scripts/generar_docx.py \
    --titulo "Receta" --output "receta.docx"
```

### Agente guía

Invocar al agente `guia` para planificar comidas, buscar recetas por ingredientes o generar lista de la compra.

## Seguridad alimentaria

Todas las recetas generadas incluyen avisos obligatorios según el ingrediente: pollo/pavo (74 °C), carne picada (71 °C), anisakis, Bacillus cereus en arroz, huevos crudos, contaminación cruzada y más.
