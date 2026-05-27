# CDX-CNTXT-TCNC-OUT-YY — HS (Hub Sport)

## 0\) Identificación de fuente

* Fuente principal inspeccionada: repositorio local /workspace/by-iPV-Hub-Sport (rama work, estado runtime/SDLC actual).   
* Fuente de soporte operativo: RUNBOOK\_PCL\_HUB\_SPORT\_LSK.md (operación de presencia/PCL). 

---

## 1\) Snapshot técnico-operacional (runtime real)

### 1.1 Estado funcional declarado del producto

* HS está definido como MVP promocional visual, desacoplado del core operativo de matchmaking (sin pagos, sin generación de partidos, sin standings).   
* El runtime depende de conciliación entre dos fuentes: Equipos\_Inscritos (pre-inscritos) y Teams (inscritos). 

### 1.2 Fuente de datos activa

* useDemoData: false en config (intención: usar fuente real Apps Script/Sheets).   
* ID de spreadsheet configurado: 1TNg4Ogygzq9PF3OEzliCI5BGRveutwYADNB5LInKzPU.   
* URL runtime de bootstrap configurada a Apps Script.   
* La carga de eventos sí usa spreadsheetId explícito en getSettings. 

### 1.3 Resolución de pipeline de datos

* En real \+ eventAlias \!= ipv, si bootstrap regresa vacío o error, cae a real-empty-fallback (0 filas).   
* En ipv, si falla remoto, cae a dataset demo embebido.   
* La lectura remota actual ya envía event \+ spreadsheetId \+ preRegisteredSheet \+ teamsSheet hacia bootstrap. 

---

## 2\) Estado SDLC / Git / continuidad

### 2.1 Estado de rama y commits locales observados

* Rama activa inspeccionada: work.  
* Último commit local observado: Include spreadsheetId and sheet names in appsScript bootstrap request.  
* No se confirmó en esta corrida un branch remoto activo/estable para release desde este repo local (historial operacional previo muestra variabilidad de remotos en sesión).

Inferencia técnica: existe riesgo de divergencia local/remoto en el flujo operativo si no se fija baseline de ramas (main/dev) con política de sincronización antes de pruebas formales.

---

## 3\) Drift, deuda y riesgos (clasificación obligatoria)

## 3.1 CRÍTICA

1. Fallback silencioso a vacío en eventos no-IPV (modo real).  
   * Origen: resolveDataPipeline() retorna \[\] cuando bootstrap no trae filas para no-IPV.   
   * Impacto: UI muestra “sin pre-inscritos/inscritos”, bloqueando validación de negocio aunque exista data en Sheet.  
   * Riesgo: falso negativo operacional en pruebas/release.

## 3.2 ALTA

2. Contrato frontend↔Apps Script no verificado end-to-end para parámetros nuevos.  
   * Origen: frontend ahora envía spreadsheetId/preRegisteredSheet/teamsSheet.   
   * Impacto: si backend no consume estos params, el cambio no corrige el caso LSK.  
   * Riesgo: persistencia de vacío en real mode pese a patch local.  
3. Dependencia fuerte de event/alias en filtrado de filas.  
   * Origen: filas se filtran por rowMatchesEventAlias.   
   * Impacto: si la columna de evento en Sheet viene vacía o con variantes no normalizadas, puede excluir datos válidos.  
   * Riesgo: inconsistencia por data quality cross-sheet.

## 3.3 MEDIA

4. Documentación de fallback en README no coincide 100% con comportamiento no-IPV real.  
   * Origen: README describe fallback demo general; código no-IPV en real cae a vacío.   
   * Impacto: expectativas de QA/ops desalineadas.  
   * Riesgo: troubleshooting más lento.  
5. roomId en config contiene valor no limpio (tab/blank).  
   * Origen: roomId: " " en config.js; luego runtime lo normaliza con fallback.   
   * Impacto: comportamiento dependiente de normalización implícita.  
   * Riesgo: confusión en diagnóstico PCL.

## 3.4 BAJA

6. Naming de parámetro URL pudzle no estándar.  
   * Origen: parser URL usa pudzle, activa on/categoria.   
   * Impacto: menor, pero eleva fricción operativa/documental.  
   * Riesgo: errores de uso manual de URLs en QA.

## 3.5 OBSERVACIÓN

7. Runbook PCL está presente y útil, pero algunas rutas del README apuntan a estructura de worktree histórica.  
   * Origen: referencias a .worktrees/... en README.   
   * Impacto: puede no aplicar 1:1 en este checkout.  
   * Riesgo: confusión de onboarding técnico.

---

## 4\) Gaps detectados (no inventados)

* GAP-01: no se encontró SESSION\_LOG.md en el root actual del repo inspeccionado (solo mención documental).   
* GAP-02: no se validó en esta corrida respuesta real del endpoint Apps Script bootstrap para event=lsk con payload de producción (faltó prueba HTTP con credenciales/entorno de release).  
* GAP-03: no se verificó baseline freeze formal documentada (tag/release checklist con hash de runtime).

---

## 5\) Alineación técnica (TCNC)

* Alineación runtime parcial: configuración y pipeline existen para multi-evento con Sheets y PCL.   
* No alineado plenamente para readiness: caso real no-IPV sigue frágil por fallback a vacío \+ contrato backend no validado en entorno real.

---

## 6\) Observaciones SCRUM (accionables)

1. Historia técnica inmediata (P1): Validar contrato bootstrap en backend con params spreadsheetId/preRegisteredSheet/teamsSheet y evidencia de payload para event=lsk.  
2. Historia técnica (P1): Definir comportamiento de fallback no-IPV (vacío vs demo-controlado) y documentarlo de forma consistente en README \+ criterios QA.  
3. Historia técnica (P2): Hardening de normalización de alias de evento en ingestión para minimizar exclusión de filas por formato.  
4. Historia operativa (P2): Consolidar baseline de rama (dev/main/work), política de sync y check de divergencia local/remoto antes de cada test plan.

---

## 7\) Readiness estimada (TCNC)

* Runtime readiness HS v1.0: condicionada (bloqueador principal: validación de bootstrap real para no-IPV).  
* SDLC readiness: media-baja por riesgo de divergencia de rama/remoto y documentación parcialmente histórica.  
* Recovery/rollback readiness: media en PCL (runbook existe), baja para capa de datos de bootstrap multi-evento hasta cerrar evidencia de contrato.

