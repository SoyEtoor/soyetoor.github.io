# Plantillas de issues

## Epic

**Título:** `[EPIC] E## - <nombre de épica>`

**Body:**
- Contexto y objetivo de negocio
- Alcance incluido / excluido
- Features hijas (checklist)
- Dependencias
- Criterios de cierre de épica

**Labels sugeridos:** `type:epic`, `priority:P1|P2|P3`, `domain:*`

---

## Feature

**Título:** `[FEATURE] F### - <nombre de feature>`

**Body:**
- Epic padre: `E##`
- Objetivo funcional
- Criterios de aceptación
- Tasks hijas (checklist)
- Riesgos / dependencias

**Labels sugeridos:** `type:feature`, `priority:P1|P2|P3`, `domain:*`

---

## Task

**Título:** `[TASK] T### - <nombre de task>`

**Body:**
- Feature padre: `F###`
- Epic relacionada: `E##`
- Definición de terminado (DoD)
- Dependencias técnicas
- Estimación relativa (S/M/L)

**Labels sugeridos:** `type:task`, `priority:P1|P2|P3`, `status:todo`, `domain:*`
