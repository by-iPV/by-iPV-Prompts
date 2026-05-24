# /prompts/freeze

## 1. Propósito
Documentar freeze operacional, baseline NO TOUCH y referencias PRE-v1.0 (v0.9.9 stable).

## 2. Qué archivos contiene
- `README.md`
- `.gitkeep`
- (prompts de freeze y control de alcance)

## 3. Cuándo usarlo
Antes de cambios sensibles, durante ventanas de estabilización y para proteger baseline.

## 4. Qué NO debe hacerse
No abrir nuevas features ni redefinir arquitectura.

## 5. Fuente primaria
Codex.

## 6. Fuente secundaria
ChatGPT.

## 7. Relación con MA-AE, N+1, HS v0.9.9, ECOSISTEMA MA-AE BD / HS / MM / PDGD, SDLC, Prompt Registry
Freeze conserva integridad de HS v0.9.9, acota transición a ECOSISTEMA MA-AE BD / HS / MM / PDGD y define límites operativos para N+1.

## 8. Riesgos si se usa incorrectamente
Relajar freeze puede introducir regresiones o desviación de alcance PRE-v1.0.

## 9. Compatibilidad
- ChatGPT: media
- Codex Cloud: alta
- VSCode: media

## 10. Restricciones operacionales
Aplicar política NO TOUCH y mantener registro estrictamente documental.
