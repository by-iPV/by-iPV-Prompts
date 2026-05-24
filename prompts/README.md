# Prompt Registry — ECOSISTEMA MA-AE BD / HS / MM / PDGD

## 1) Qué es Prompt Registry
`/prompts` es el registro versionado institucional del ecosistema MA-AE BD / HS / MM / PDGD para preservar prompts operacionales, conceptuales y de recovery con trazabilidad Git.

## 2) Por qué GitHub es fuente oficial
GitHub proporciona versionado, historial auditable, diff verificable, restauración por commit y continuidad multi-entorno; por ello es la fuente oficial persistente.

## 3) Por qué Codex Cloud NO es memoria persistente
Codex Cloud se usa como entorno de ejecución y asistencia, pero no garantiza persistencia contextual completa entre reinicios/sesiones.

## 4) Por qué VSCode/Codex local NO es fuente oficial
VSCode local y extensiones pueden degradarse, perder estado o depender de almacenamiento no gobernado; por diseño no sustituyen el repositorio versionado.

## 5) Componentes recuperables (no oficiales)
Pueden existir y recuperarse parcialmente:
- tasks
- workspace state
- extension storage
- cache
- metadata

## 6) Por qué recovery local NO debe bloquear ECOSISTEMA MA-AE BD / HS / MM / PDGD
La continuidad de ECOSISTEMA MA-AE BD / HS / MM / PDGD depende de artefactos versionados y runbooks; el recovery local es auxiliar y no puede frenar operación.

## 7) Estrategia operacional
- **Ruta principal:** Codex Cloud + GitHub.
- **Ruta secundaria:** VSCode local recovery.

## 8) Relación con TRC, TCNC, MA-AE, N+1, Freeze, Recovery
- **TRC:** contexto conceptual portable y validación conceptual.
- **TCNC:** contexto técnico-operacional portable y validación técnica.
- **MA-AE:** marco de alineación y gobierno entre actores/agentes.
- **N+1:** base para migración incremental y continuidad futura.
- **Freeze:** preserva baseline y límites PRE-v1.0.
- **Recovery:** reconstrucción rápida de contexto ejecutable.

## 9) Reglas NO TOUCH
- No alterar runtime desde Prompt Registry.
- No subir `.env`.
- No subir secretos.
- No subir cache local.
- No subir logs runtime.
- No subir workspace temp.
- No subir `.wrangler`.
- No duplicar conversaciones completas.
- No usar Prompt Registry para almacenar chats enteros.
- No usar prompts como reemplazo de RUNBOOK.

## 10) Política de prompts versionados
Todo prompt institucional debe registrarse por archivo versionado, con cambios trazados vía commit y naming estable.

## 11) Política de continuidad contextual
La continuidad depende de prompts + runbooks + historial Git, no de memoria conversacional temporal.

## 12) Política de recovery operacional
Recovery se ejecuta desde artefactos cortos, auditables y versionados en `/prompts/recovery`.

## 13) Política PRE-v1.0
Mantener baseline v0.9.9 stable freeze; evitar redefiniciones estructurales y nuevas features desde este registro.

## 14) Política POST-v1.0
Extender prompts por etapas N+1 con control de cambios, revisión y compatibilidad cruzada ChatGPT/Codex/VSCode.

## Estrategia para VSCode local (recovery secundario)
VSCode local se clasifica como **recovery secundario** y **NO** como fuente oficial.

Puede contener:
- tasks locales
- contexto runtime
- estado del workspace
- snapshots parciales
- referencias repo
- cache Codex
- metadata local

Ubicaciones frecuentes:
- `%APPDATA%`
- `%USERPROFILE%`
- `.vscode`
- extension storage
- Codex cache
- workspace storage

Aun con recuperación local disponible, la persistencia oficial permanece en:
**GitHub + `/prompts` + RUNBOOK**.
