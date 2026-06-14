---
name: chef-expert
description: >
  Mejora recetas desde URLs web y genera archivos .md y .docx.
  Úsalo cuando el usuario pase una URL de receta y pida mejorarla,
  adaptarla o exportarla a formato documento. Incluye análisis de
  proporciones, técnicas, tiempos y sugerencias de mejora. El flujo
  es: (1) recibir URL, (2) extraer la receta, (3) mejorarla y
  conversar con el usuario para adaptarla, (4) generar .md y .docx.
---

# Chef Expert

## Workflow

### 1. Recibir URL
El usuario proporciona una URL de receta de cualquier web.

### 2. Extraer receta
Usa `webfetch` para obtener el contenido de la URL.
Analiza y estructura:
- Nombre del plato
- Raciones
- Ingredientes (cantidad + unidad + ingrediente)
- Pasos de elaboración
- Tiempos y temperaturas
- Consejos adicionales

### 3. Mejorar la receta
Aplica criterios de mejora (ver `references/mejora-recetas.md`):
- Proporciones y平衡 de sabores
- Técnicas culinarias (sellado, desglasado, reposo, etc.)
- Optimización de tiempos
- Claridad y estructura de la explicación
- Sugerencias de variaciones y micro-ajustes
- Para guisos de carne, cargar skill `.opencode/skills/guisos-carne/`

### 4. Conversar con el usuario
Presenta la receta mejorada al usuario y ofrece adaptaciones:
- ¿Cambiar algún ingrediente?
- ¿Ajustar tiempos?
- ¿Variaciones (vegano, sin gluten, picante, etc.)?
- ¿Número de raciones diferente?
El usuario responde y tú ajustas la receta.

### 5. Generar archivos
Una vez aprobada la receta final, genera:

**Markdown (.md):** Receta completa en español con formato markdown limpio.

**DOCX (.docx):** Usa el script `scripts/generar_docx.py`:
```bash
python3 scripts/generar_docx.py --titulo "..." --output "ruta.docx"
```
El script acepta un JSON con la receta por stdin. Pasa los datos
de la receta como JSON, por ejemplo:
```bash
echo '{
  "titulo": "Título",
  "raciones": 4,
  "ingredientes": [["500 g", "Ingrediente 1"], ...],
  "pasos": [["1. Título paso", "Cuerpo del paso"], ...],
  "ajustes": [["Variación", "Descripción"], ...],
  "consejos": ["Consejo 1", ...],
  "etiquetas": ["rápida", "olla presión"]
}' | python3 scripts/generar_docx.py --titulo "Título" --output "receta.docx"
```

## Recursos

### scripts/generar_docx.py
Script reutilizable que genera un documento DOCX profesional con:
- Título centrado con color
- Subtítulo con raciones
- Tabla de ingredientes con estilo
- Pasos numerados con encabezados
- Sección de micro-ajustes
- Consejos en formato lista

### references/mejora-recetas.md
Criterios y estándares para mejorar recetas: proporciones, técnicas,
optimización de tiempos, variaciones y micro-ajustes.
