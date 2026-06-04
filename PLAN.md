# Plan: Crear archivos B1 (Komplett y Hoeren-Sprechen)

## Context

El usuario ha trabajado durante esta sesion en dos archivos HTML autonomos de practica de aleman nivel B2:

- `b2-deutsch-komplett.html` (584 lineas) — 350 ejercicios escritos/lectura en 7 secciones (Grammatik, Wortschatz, Konjunktiv II, Passiv, Konnektoren, Leseverstehen, Textsorten)
- `b2-hoeren-sprechen.html` (~1115 lineas) — practica de audicion y habla con Web Speech API: Richtig/Falsch, Diktat, Textverstehen, Aussprache, Freie Antwort, Situation

Ambos archivos fueron re-estilizados con la paleta de TiyaGolfClub (verde `#81B29A`, amarillo `#F2CC8F`, naranja hover `#E07A5F`, fondo blanco/crema, tipografia DM Sans, esquinas redondeadas) y los emojis UI fueron reemplazados por Bootstrap Icons (CDN v1.11.3).

Ahora el usuario quiere los **mismos archivos pero nivel B1**, manteniendo identicas la arquitectura, el CSS y la logica de JavaScript. Solo cambia el contenido (ejercicios) y el nivel difficulty (vocabulario y gramatica mas basico, temas mas cotidianos).

Volumen confirmado por el usuario:
- B1 Komplett: **50 ejercicios x 7 secciones = 350**, con secciones **adaptadas al syllabus B1 oficial**
- B1 H&S: **50 por modulo** (50 RF + 50 Diktat + 10 textos x 5 preguntas TV + 50 Aussprache + 50 Freie Antwort + 50 Situation)

## Approach

**Estrategia de implementacion**: copiar la estructura completa de los archivos B2 (CSS + HTML + JS), cambiando solo:

1. Titulo (`<title>` y `<h1>`)
2. Texto del eyebrow/subtitulo
3. Arrays de datos con contenido B1
4. Total de progreso si difiere (el contador `/350` en `pbar` por ejemplo)

Esto garantiza:
- Mismo estilo visual (TiyaGolfClub)
- Misma funcionalidad (tabs, paginacion, scoring, Web Speech API, acuracidad palabra-por-palabra)
- Mismos Bootstrap Icons

### Archivo 1: `b1-deutsch-komplett.html`

Estructura identica al B2. Solo se reemplaza el array `SECTIONS` con contenido B1.

**Secciones B1 propuestas** (adaptadas al syllabus oficial Goethe-Zertifikat B1 / telc B1):

| # | Seccion | Subtemas |
|---|---------|----------|
| 01 | **Grammatik & Artikel** | Bestimmter/unbestimmter Artikel, Possessivartikel, Adjektivendungen (einfach), Komparativ/Superlativ, Pronomen |
| 02 | **Verben** | Modalverben (Praesens, Praeteritum), Reflexivverben, Trennbare Verben, Imperativ, Konjugation unregelmaessiger Verben |
| 03 | **Zeitformen** | Praesens, Perfekt (haben/sein), Praeteritum, Plusquamperfekt (Einfuehrung), Futur I (einfach) |
| 04 | **Praepositionen & Kasus** | Akkusativ-/Dativ-/Wechselpraepositionen, einfache Genitiv-Konstruktionen, Praepositionalverben (denken an, warten auf...) |
| 05 | **Konnektoren & Satzbau** | und, aber, denn, oder, sondern, weil, dass, wenn, obwohl, deshalb, trotzdem, damit, als, nachdem, bevor |
| 06 | **Wortschatz & Leseverstehen** | Alltagsthemen (Familie, Wohnen, Arbeit, Reisen, Gesundheit, Essen, Hobbys), Synonyme/Antonyme, kurze Texte B1 |
| 07 | **Textsorten & Schreiben** | Informelle E-Mail/Brief, persoenlicher Brief, kurze Mitteilung, Einladung/Absage, Beschreibung, Formelle Anfrage (einfach) |

Cada seccion: 50 ejercicios mezcla de `mc` (multiple choice), `fill` (input), `transform` (textarea).

**Cambios estructurales puntuales**:
- `<title>`: `B1 Deutsch — 350 Uebungen`
- `<h1>`: `Deutsches B1 — Komplettheft`
- eyebrow span: `Pruefungsvorbereitung · 350 Uebungen · Niveau B1`
- En la funcion `updateScore()`, la division `Math.min(100,Math.round(state.answered.size/350*100))` permanece igual (350 ejercicios totales)

### Archivo 2: `b1-hoeren-sprechen.html`

Estructura identica al B2. Solo cambian los arrays de datos:

| Array | Cantidad | Contenido B1 |
|-------|----------|--------------|
| `RF` (Richtig/Falsch) | 50 | Afirmaciones sencillas sobre Alemania, geografia, cultura, costumbres |
| `DK` (Diktat) | 50 | Frases cortas con vocabulario alltaglich, sin clausulas complejas |
| `TV` (Textverstehen) | 10 textos x 5 preguntas | Textos cortos sobre: Wohnen, Reisen, Arbeit, Hobbys, Schule, Gesundheit, Essen, Familie, Sport, Umwelt |
| `PR` (Aussprache) | 50 | Palabras y frases cortas con sonidos tipicos del aleman (ae, oe, ue, ch, sch, sp, st, ie, ei) |
| `FR` (Freie Antwort) | 50 | Preguntas simples: "Was machst du in deiner Freizeit?", "Beschreibe deine Familie", etc. |
| `SI` (Situation) | 50 | Situaciones cotidianas: Beim Arzt, Im Restaurant, Beim Einkaufen, An der Rezeption, Beim Termin vereinbaren |

**Cambios estructurales puntuales**:
- `<title>`: `B1 Hoeren & Sprechen — 50 Uebungen`
- `<h1>`: `Hoeren & Sprechen` (mismo)
- eyebrow: `B1 · Pruefungsvorbereitung · 50 Uebungen je Modul`
- Las funciones `evalFree`, `evalSitu`, `evalPron` se mantienen igual (los umbrales B1 vs B2 son ligeramente mas indulgentes para B1 pero pueden quedar igual; los criterios B2 son razonables para B1 tambien si el contenido es B1)

## Files to Create

Tres archivos nuevos:

- `index.html` — pagina menu/indice para navegar entre niveles y modulos
- `b1-deutsch-komplett.html` — copia estructural de `b2-deutsch-komplett.html` con `SECTIONS` reemplazado
- `b1-hoeren-sprechen.html` — copia estructural de `b2-hoeren-sprechen.html` con `RF`, `DK`, `TV`, `PR`, `FR`, `SI` reemplazados

### Archivo 3: `index.html` (menu principal)

Pagina de aterrizaje con estilo TiyaGolfClub que organiza visualmente los 4 archivos de practica disponibles.

**Estructura**:

```
HEADER (sticky)
  eyebrow: "Deutsch lernen · Pruefungsvorbereitung"
  h1: "Deutsch fuer alle Niveaus"

HERO / INTRO seccion corta (1 parrafo)
  Texto: "Waehle dein Niveau und beginne mit dem Training. Jedes Modul
  enthaelt mehrere Hundert Uebungen mit sofortigem Feedback."

LEVEL CARDS GRID (responsive: 1col mobile, 2col tablet+)

  CARD: B1
    eyebrow: NIVEAU B1 · Mittelstufe Grundkenntnisse
    h2: "B1 — Mittelstufe"
    p: Beschreibung ("Festige deine Grundkenntnisse...")
    Modulo links:
      - "Komplettheft (350 Uebungen)" -> b1-deutsch-komplett.html
        icon: bi-journal-text + chip "Schreiben & Lesen"
      - "Hoeren & Sprechen (50 je Modul)" -> b1-hoeren-sprechen.html
        icon: bi-mic-fill + chip "Audio · Mikrofon"

  CARD: B2
    eyebrow: NIVEAU B2 · Selbstaendige Sprachverwendung
    h2: "B2 — Selbstaendige Stufe"
    p: Beschreibung
    Modulo links:
      - "Komplettheft (350 Uebungen)" -> b2-deutsch-komplett.html
      - "Hoeren & Sprechen (50 je Modul)" -> b2-hoeren-sprechen.html

FOOTER (sticky bottom)
  Pequeno texto: "Webspeech API erforderlich fuer Hoeren & Sprechen"
```

**Decisiones de diseno**:
- Reutilizar las mismas variables CSS root del estilo TiyaGolfClub (`--primary`, `--btn-bg`, `--btn-hover`, `--secondary`)
- Cargar Bootstrap Icons CDN (mismo enlace que los otros archivos)
- Cards con `border-radius: 20px`, sombra suave, hover con `border-left: 4px solid var(--primary)`
- Los modulos dentro de cada card son `<a>` con iconos bi-* y estilo de chip
- B1 con un acento visual ligeramente distinto al B2 (e.g. card B1 con borde `--primary`, card B2 con borde `--btn-hover`) para distinguir niveles
- Sin JavaScript (es pagina estatica de navegacion)
- Responsive media queries iguales a los otros archivos

**Estructura de archivos resultante**:
```
Deutsch lernen/
  index.html              <- NUEVO (menu principal)
  b1-deutsch-komplett.html  <- NUEVO
  b1-hoeren-sprechen.html   <- NUEVO
  b2-deutsch-komplett.html  (existente)
  b2-hoeren-sprechen.html   (existente)
  TiyaGolfClub-1.0.0/     (referencia de estilo, no se toca)
```

## Implementation Notes

1. **Reutilizacion de codigo**: el CSS, helpers JS (`$id`, `colorLabel`, `updateScores`, `setPlayBtn`, `createRec`, `evalPron`, `evalFree`, `evalSitu`, `renderExercise`, `checkMC`, `checkFill`, `checkTransform`, etc.) se copian sin cambios desde los archivos B2.

2. **Bootstrap Icons**: se mantienen las mismas iconos `bi-*` ya integrados (mic, play, stop, check-circle, exclamation, etc.).

3. **Estilo TiyaGolfClub**: misma paleta y tipografia. Las variables CSS root quedan identicas.

4. **Difficulty B1 vs B2 en ejercicios**:
   - B1: vocabulario cotidiano (Familie, Essen, Wohnen), oraciones de 8-12 palabras, gramatica al nivel A2-B1
   - Las oraciones de RF y Diktat seran mas cortas
   - Los textos TV seran de 60-90 palabras (vs ~120-150 en B2)
   - Las situaciones (SI) seran mas comunes y cotidianas (vs argumentativas en B2)

5. **Tamano de archivos esperado**:
   - `b1-deutsch-komplett.html`: ~600 lineas (similar al B2)
   - `b1-hoeren-sprechen.html`: ~1100 lineas (similar al B2)
   - Total contenido nuevo: ~70-90 KB de datos B1

## Verification

Para validar los archivos creados:

1. Abrir `index.html` en navegador (Chrome/Edge recomendado por Web Speech API)
2. **Index**:
   - Verificar que las 2 cards (B1, B2) aparecen con los 4 botones de modulo
   - Verificar que los enlaces navegan correctamente a cada archivo
   - Verificar que el estilo coincide con TiyaGolfClub (paleta, tipografia, esquinas redondeadas)
   - Verificar responsive en mobile (cards apiladas) vs desktop (2 columnas)
3. **B1 Komplett**:
   - Verificar que los 7 tabs aparecen con contadores 50
   - Hacer click en cada tab y verificar que renderiza los ejercicios
   - Responder algunos MC/fill/transform y verificar que el scoring funciona
   - Verificar paginacion (10 ejercicios por pagina, 5 paginas por seccion)
   - Verificar la barra de progreso inferior
4. **B1 Hoeren & Sprechen**:
   - Verificar que los modos Hoeren y Sprechen cambian
   - Probar audio playback en RF, DK, TV (requiere SpeechSynthesis)
   - Probar microfono en Aussprache, Freie Antwort, Situation (requiere SpeechRecognition)
   - Verificar que las recomendaciones aparecen con los icons bi-*
   - Verificar que los Bootstrap Icons cargan correctamente (CDN)

## Out of Scope

- No se modifican los archivos B2 existentes (solo se enlazan desde `index.html`)
- No se internacionaliza la UI (queda en aleman como los B2)
- No se anaden persistencia (localStorage) ni autenticacion
- No se anaden niveles adicionales (A1, A2, C1, C2) en esta iteracion — el `index.html` se disena pensando en una extension futura facil
