---
name: think-and-delegate
description: >
  Meta-cognición: detenerse a pensar antes de actuar, planificar tareas
  complejas, delegar sub-tareas a agentes especializados, y usar el Task
  tool para ejecución en paralelo. Úsalo ante cualquier tarea que requiera
  múltiples pasos o decisiones.
---

# Think & Delegate

## Think (pensar antes de actuar)

Ante cualquier solicitud que requiera más de 1-2 pasos o decisiones:

1. **Pausar**: no ejecutar nada todavía. Leer la petición completa.
2. **Analizar**: ¿qué pide exactamente? ¿hay ambigüedades? ¿qué información falta?
3. **Planificar**: descomponer en pasos atómicos. Identificar dependencias.
4. **Decidir**: ¿qué herramientas usar? ¿qué skills cargar? ¿qué delegar?
5. **Solo entonces actuar**.

### Checklist de planificación

- [ ] Entendí el problema/ petición
- [ ] Identifiqué qué skills aplicar (olla-presion, pescados-guisos, etc.)
- [ ] Dividí en pasos independientes vs secuenciales
- [ ] Marqué dependencias (paso B depende de paso A)
- [ ] Identifiqué qué puede ir en paralelo
- [ ] Verificar contra AGENTS.md y SKILL.md del proyecto

## Delegate (delegar a sub-agentes)

Usar el **Task tool** cuando:

- Hay **múltiples archivos que buscar/leer** en paralelo
- Una tarea puede **dividirse en sub-tareas independientes**
- Se necesita **investigar** (webfetch, websearch) mientras se hace otra cosa
- Un paso es **mecánico y repetitivo** (ej. buscar y reemplazar en 10 archivos)
- Se requiere **exploración del código** sin modificar nada

### Cuándo NO delegar
- Tareas triviales de 1 paso
- Operaciones que dependen del contexto actual de la conversación
- Decisiones que requieren criterio del usuario

### Patrón de delegación

```
Tarea compleja
├── Paso A (independiente) → Task(explore/general)
├── Paso B (independiente) → Task(explore/general)
├── Paso C (depende de A y B) → hago yo mismo tras recoger resultados
└── Paso D (secuencial tras C) → hago yo mismo
```

## Uso de Todowrite

Para tareas con 3+ pasos:
1. Crear todolist al inicio
2. Solo 1 tarea en `in_progress` a la vez
3. Marcar `completed` inmediatamente al terminar
4. Cancelar tareas que ya no aplican
