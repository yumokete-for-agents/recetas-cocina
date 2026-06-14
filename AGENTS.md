# Recetas Cocina

## Python: siempre usar venv
- **NUNCA** ejecutar Python fuera del venv del proyecto.
- Venv: `.venv/` en la raíz del proyecto.
- Activar: `.venv/bin/python` o `.venv/bin/pip`.
- Dependencia `python-docx` ya instalada en el venv.

## Generar DOCX
- Usar `chef-expert/scripts/generar_docx.py`, NO `generar_receta.py` (hardcoded, one-off).
- El script acepta JSON por stdin:
  ```bash
  echo '{...}' | .venv/bin/python chef-expert/scripts/generar_docx.py --titulo "Nombre" --output "receta.docx"
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
Toda receta final debe incluir sección **"Micro-ajustes según tu gusto"** con variaciones de textura, punto, sabor y sustituciones. Ver `chef-expert/references/mejora-recetas.md` para el listado completo.

## Sustituciones probadas (documentar en cada receta)
- Tomate + pimiento → asadillo (~100 g / 4 rac)
- Cebolla fresca → zanahoria (1 med) + cebolla en polvo (1 cdta rehidratada)
- Vino blanco → caldo de carne + 1 cda vinagre de vino

## Framework general de guisos
- Para diseñar guisos de carne con patatas desde cero o adaptar recetas, usar `chef-expert/references/guisos-generales.md`.
- El framework cubre: tabla de carnes con tiempos P1/P2, perfiles de sofrito regionales, maridaje de líquidos, proporciones por ración, micro-ajustes transversales, y checklist de diseño.
- Aplicar la estructura universal: Sellar → Sofreír → Desglasar → 1ª cocción (carne) → 2ª cocción (+ patatas) → Reposo.

## Skills
- `chef-expert/`: flujo general de mejora y exportación de recetas (skill local).
- `.opencode/skills/olla-presion/`: conocimiento específico de olla a presión, adaptaciones y sustituciones (skill local).
- `.opencode/skills/pescados-guisos/`: conocimiento específico de guisos de pescado con patatas — tipos de pescado, tiempos, perfiles regionales, fumet, micro-ajustes, errores comunes.
- `.opencode/skills/arroz-guisos/`: conocimiento específico de arroces secos, melosos y caldosos — proporciones líquido/arroz, clasificación por textura, variedades de grano, técnica universal, perfiles regionales, micro-ajustes y errores comunes.

## Idioma
- Todo el contenido (recetas, docs, código) en español.
