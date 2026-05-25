# /prompts/recovery

## 1. Propósito
Concentrar prompts cortos, auditables y ejecutables para recovery, startup, fallback, reinicio y reconstrucción contextual N+1.

## 2. Qué archivos contiene
- `README.md`
- `.gitkeep`
- (playbooks de recovery en formato prompt)

## 3. Cuándo usarlo
Cuando existe pérdida parcial de contexto, reinicio de chat/Codex/VSCode o necesidad de recuperación rápida.

## 4. Qué NO debe hacerse
No incluir prompts largos ambiguos ni dependientes de memoria conversacional.

## 5. Fuente primaria
Codex.

## 6. Fuente secundaria
ChatGPT.

## 7. Relación con MA-AE, N+1, HS v0.9.9, ECOSISTEMA MA-AE BD / HS / MM / PDGD, SDLC, Prompt Registry
Recovery asegura continuidad operacional del SDLC y la transición v0.9.9→alcance MA-AE BD / HS / MM / PDGD con enfoque N+1.

## 8. Riesgos si se usa incorrectamente
Prompts no auditables pueden impedir reconstrucción confiable del contexto.

## 9. Compatibilidad
- ChatGPT: alta
- Codex Cloud: alta
- VSCode: alta (modo secundario)

## 10. Restricciones operacionales
Recovery documental; no ejecutar cambios de arquitectura ni features.
