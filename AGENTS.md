# Recetas Cocina

## Python: siempre usar venv
- **NUNCA** ejecutar Python fuera del venv del proyecto.
- Venv: `.venv/` en la raíz del proyecto.
- Activar: `.venv/bin/python` o `.venv/bin/pip`.
- **Para instalar nuevas dependencias**: `.venv/bin/pip install <paquete>`.
- Dependencia `python-docx` ya instalada en el venv.
- Pandoc disponible como binario del sistema (`/usr/bin/pandoc` v3.1.3).

## Reglas generales de ejecución

### Bash = último recurso
Preferir tools (Read, Write, Edit, Glob, Grep, Webfetch) antes que bash. Usar bash solo para git, python docx, npm, docker y comandos del sistema.

### Bash commands: límite estricto de tamaño
Cualquier comando bash que supere **200 caracteres** o **5 líneas** DEBE escribirse a un archivo temporal y ejecutarse desde ahí. No pasar como string inline al Bash tool.

### Lecciones aprendidas
Usar `/lecciones-aprendidas` al finalizar tareas complejas para capturar conocimiento y reglas antes de que se pierdan en el historial de la sesión.

### TodoWrite para tareas complejas
Para tareas con 3+ pasos: crear todolist al inicio, mantener solo 1 tarea `in_progress`, marcar `completed` inmediatamente.

## Generar DOCX
- Usar `.opencode/skills/chef-expert/scripts/generar_docx.py`, NO `generar_receta.py` (hardcoded, one-off).
- El script acepta JSON por stdin:
  ```bash
  echo '{...}' | .venv/bin/python .opencode/skills/chef-expert/scripts/generar_docx.py --titulo "Nombre" --output "receta.docx"
  ```
- **Siempre** usar `.venv/bin/python`, nunca `python3` global.
- Campos del JSON: `titulo`, `raciones`, `ingredientes` ([[cant, ing], ...]), `pasos` ([[tit, cuerpo], ...]), `ajustes` ([[nom, desc], ...]), `consejos` ([str, ...]), `etiquetas` ([str, ...]).

### Reglas para estructurar el JSON del DOCX

**Ingredientes**: incluir TODOS incluso aceite, sal, agua. Cada fila es `["cantidad", "ingrediente"`.

**Pasos**: dividir en pasos atómicos. Cada paso tiene título corto (ej. "Dorar la carne") y cuerpo descriptivo con tiempos. Si hay variante por nivel de presión (1 vs 2), explicitarlo:

```json
["4. Primera cocción (solo la carne)", "Cubre con agua...\n• Presión 1: 10 min\n• Presión 2: 8 min"]
```

**Ajustes (micro-ajustes)**: incluir SIEMPRE al menos estas categorías:
- Punto de patata (más entera / más deshecha)
- Punto de carne (más melosa / al dente)
- Grosor de caldo (espeso / ligero)
- Potenciar sabor (más pimentón, picante)
- Sustituciones (sin vino, etc.)

**Consejos**: incluir tiempo total real, punto ideal de carne, congelación, variante olla normal.

**Etiquetas**: usar al menos: tipo de olla (`olla presión`, `olla normal`), tipo de carne, tiempo estimado.

## Olla a presión — reglas fijas para los tiempos
- **Contar desde que silba**: el tiempo empieza cuando la olla alcanza presión y emite vapor estable, no antes.
- **Fuego**: máximo hasta presión, luego bajar a **medio-bajo** (solo mantener vapor).
- **Presión 1 (baja, ~0.7 bar)**: carnes gelatinosas (carrillera, jarrete, morcillo).
- **Presión 2 (alta, ~1 bar)**: carnes duras, caldos.
- Olla sin selector → usar tiempos de Presión 2 reduciendo 2 min sobre Presión 1.
- Incluir siempre **ambos tiempos** (P1 y P2/sin selector) en los pasos.

## Micro-ajustes — obligatorios
Toda receta final debe incluir sección **"Micro-ajustes según tu gusto"** con variaciones de textura, punto, sabor y sustituciones. Ver `.opencode/skills/chef-expert/references/mejora-recetas.md` para el listado completo.

## Sustituciones probadas (documentar en cada receta)
- Tomate + pimiento → asadillo (~100 g / 4 rac)
- Cebolla fresca → zanahoria (1 med) + cebolla en polvo (1 cdta rehidratada)
- Vino blanco → caldo de carne + 1 cda vinagre de vino

## Framework general de guisos
- Para diseñar guisos de carne con patatas desde cero o adaptar recetas, cargar skill `.opencode/skills/guisos-carne/`.
- La skill cubre: estructura universal 5 fases, tabla de carnes con tiempos P1/P2, perfiles de sofrito regionales, maridaje de líquidos, proporciones por ración, micro-ajustes transversales, y checklist de diseño.

## Skills
- `.opencode/skills/chef-expert/`: flujo general de mejora y exportación de recetas (skill local).
- `nuevo-proyecto/`: inicialización de proyectos OpenCode desde cero. Contiene orígenes exactos de agentes/skills, boilerplate AGENTS.md y pasos de setup (skill local).
- `.opencode/skills/guisos-carne/`: framework completo para diseñar y adaptar guisos de carne con patatas.
- `.opencode/skills/olla-presion/`: conocimiento específico de olla a presión, adaptaciones y sustituciones (skill local).
- `.opencode/skills/pescados-guisos/`: conocimiento específico de guisos de pescado con patatas — tipos de pescado, tiempos, perfiles regionales, fumet, micro-ajustes, errores comunes.
- `.opencode/skills/arroz-guisos/`: conocimiento específico de arroces secos, melosos y caldosos — proporciones líquido/arroz, clasificación por textura, variedades de grano, técnica universal, perfiles regionales, micro-ajustes y errores comunes.
- `.opencode/skills/salteados-wok/`: conocimiento específico de salteados al wok/sartén — orden de incorporación, cortes, marinados, salsas base, combinaciones, técnica de fuego alto, micro-ajustes y errores comunes.
- `.opencode/skills/asados-carne/`: conocimiento experto sobre asados de carne al horno, parrilla y barbacoa — cortes, técnicas directa/indirecta, temperaturas, dry rubs, perfiles regionales, maderas, punto de cocción.
- `.opencode/skills/asados-pescado/`: conocimiento experto sobre asados de pescado y marisco — tipos según textura, técnicas (parrilla, plancha, sal, papillote), tiempos por grosor, salsas, perfiles regionales.
- `.opencode/skills/plancha/`: conocimiento experto sobre cocción a la plancha (mínima grasa, fuego alto) — técnicas específicas por ingrediente: carnes, pescados, mariscos, verduras, huevos, setas, tofu, frutas. Cada sección con temperatura, tiempo y punto óptimo.
- `.opencode/skills/pasta-salsas/`: conocimiento experto sobre salsas para pasta — clasificación por base (tomate, nata, aceite, queso, ragùs, verduras, pescado, pesto), técnica de emulsión, maridaje salsa-forma, proporciones, quesos y errores comunes.
- `.opencode/skills/sopas/`: conocimiento experto sobre sopas, caldos y cremas — clasificación por textura y base, técnicas de fondo, espesores, emulsionado, guarnición, caldos internacionales y errores comunes.

## Agentes externos copiados
- `.opencode/agents/git-expert.md`: autoridad exclusiva en git/gh. Delegar siempre commits, push, tags, PRs. No edita archivos ni ejecuta otro bash.
- `.opencode/agents/think-and-delegate.md`: agente primario orquestador. Planifica y delega todo mediante Task tool. Pide permiso para tareas modificadoras.

## Routing por agente autoritativo
| Agente | Dominio | Regla |
|---|---|---|
| `git-expert` | Toda operación git/gh (commit, push, tag, branch, merge, rebase, PR) | **Delegar siempre** |
| Cualquier agente | `git status`, `git diff` | Solo lectura segura — cualquiera puede |

## Skill obligatoria: git-basic-rules
- `.opencode/skills/git-basic-rules/`: todos los agentes (excepto `git-expert`) que puedan necesitar git DEBEN cargar esta skill.
- Sin ella, los agentes no sabrán que deben delegar en `git-expert`.
- `git-expert` ya tiene estas reglas en su system prompt; no necesita la skill.

## Idioma
- Todo el contenido (recetas, docs, código) en español.

## Avisos de seguridad alimentaria — obligatorios en cada receta
Toda receta debe incluir **avisos de seguridad** cuando aplique. No asumir que el usuario lo sabe.

| Ingrediente | Advertencia | Por qué |
|---|---|---|
| **Pollo / pavo / aves** | Cocer hasta 74 °C en el centro (muslo). No servir rosado ni poco hecho. | Salmonella y Campylobacter causan intoxicación grave. Solo la temperatura interna mata las bacterias. |
| **Carne picada** (hamburguesas, albóndigas, pates, salchichas caseras) | Cocer hasta 71 °C en el centro. No servir poco hecho. | La molienda distribuye bacterias de la superficie al interior. No basta con sellar. |
| **Cerdo** (filete, lomo, presa) | Puede servirse rosado (63 °C) si es pieza entera. **Carne picada de cerdo**: 71 °C. | Triquinosis y otras parasitosis. El cerdo moderno es seguro a 63 °C en pieza entera, pero picada requiere 71 °C (misma razón que vacuno picado). |
| **Pescado crudo / poco hecho** (carpaccio, tartar, ceviche, sushi) | Usar pescado previamente congelado (-20 °C 48h o -35 °C 15h) o de acuicultura certificada. | Anisakis: parásito presente en pescado salvaje. La congelación mata las larvas. |
| **Huevos** (yema cruda o poco cuajada) | Advertir a embarazadas, niños, ancianos e inmunodeprimidos. Usar huevos pasteurizados si hay duda. | Salmonella en huevo puede causar infección grave en poblaciones vulnerables. |
| **Recalentar sobras** | Calentar hasta 74 °C en el centro, no solo "que humee". | Bacterias que sobreviven a la refrigeración (Listeria, Bacillus) requieren temperatura alta para morir. |
| **Arroz cocido** (Bacillus cereus) | Refrigerar el arroz cocido **antes de 2 horas** a temperatura ambiente. No recalentar más de una vez. Consumir en 24 h. | Bacillus cereus forma esporas que sobreviven a la cocción. Si el arroz se enfría lentamente, las esporas germinan y producen toxinas resistentes al calor que el recalentado no elimina. |
| **Congelación / descongelación** | Descongelar en nevera (nunca a temperatura ambiente). No recongelar carne/pescado descongelado. | La superficie alcanza temperatura de riesgo (4-60 °C) mientras el centro sigue congelado, multiplicando bacterias. |
| **Contaminación cruzada** | Tablas y cuchillos separados para carne cruda y vegetales. Lavar manos tras tocar carne/pescado crudo. | Bacterias de alimentos crudos se transfieren a alimentos listos para comer y se multiplican sin cocción adicional. |
