# Style guide — La volpe grigia

> Documento interno. Non va online, non va linkato da nessuna pagina pubblica.

## Identità del progetto

Sito personale di divulgazione culturale. Ogni pagina risponde a una domanda precisa — su scienze, ambiente, economia, società, storia, filosofia, letteratura, o qualsiasi altro tema. Nessun limite tematico. Tono chiaro e accessibile (livello liceo scientifico come riferimento di semplicità), mai banale — come un bravo professore che racconta, non che recita.

## Formato delle pillole

Ogni pagina è una **pillola**: risponde a una sola domanda, si legge in **3-4 minuti massimo**, e la maggior parte del contenuto è visiva e interattiva. Il testo serve a introdurre e collegare — non a spiegare tutto. Spiegano le applet.

Struttura fissa, in quest'ordine:

1. **La domanda** — titolo in forma di domanda diretta
2. **La risposta in 2 righe** — evidenziata, subito visibile (risposta-box)
3. **Testo breve** — massimo 3-4 paragrafi in tutto l'articolo, mai consecutivi (sempre separati da almeno un'applet), ogni paragrafo max 4 righe
4. **Applet / grafici / linee del tempo** — **almeno 2-3 per pillola**, di tipi diversi, sono il corpo principale
5. **Una frase da portarsi a casa** — chiude il pezzo, in corsivo (frase-finale)
6. **Fonti** — compatte, in fondo (sezione "Fonti dei dati", MAI assente)

**Regola aurea:** se una cosa si può mostrare con un'applet, non si spiega a parole.

## Applet interattive — regole tecniche

Sono il cuore di ogni pillola. Ogni pillola ne ha **almeno 2-3**, di tipi diversi tra loro.

- Solo HTML + CSS + JavaScript vanilla (nessuna libreria esterna tranne Chart.js per i grafici, caricato da CDN come nelle pillole esistenti)
- Canvas API ammesso per simulazioni
- Tipi ammessi:
  - **Linee del tempo interattive** — scorrimento, eventi cliccabili con dettaglio
  - **Simulazioni animate** — oggetti che reagiscono a click o slider, illustrano un processo
  - **Grafici dinamici** — Chart.js con dati reali, fonte sempre citata sotto
  - **Mappe concettuali cliccabili** — schema SVG con nodi espandibili
  - **Confronti interattivi** — toggle, slider, side-by-side con dati reali
  - **Calcolatori** — l'utente inserisce un valore e vede il risultato in tempo reale
- Ogni applet ha: titolo, istruzione breve ("Clicca per simulare" / "Seleziona per confrontare"), didascalia con fonte

## Stile visivo

- **Sfondo**: `#fdfcf9` — **testo**: `#1c1c2e` — molto spazio bianco
- **Font**: Playfair Display per titoli, Source Sans 3 per corpo testo, da Google Fonts
- **Layout**: max-width 640px, centrato, responsive mobile-first
- **Densità**: tanto spazio bianco tra i blocchi — ogni applet respira
- Riusa sempre le stesse classi CSS delle pillole esistenti (`.tag`, `.risposta-box`, `.meta`, `.testo`, `.applet`, `.applet-header`, `.applet-titolo`, `.applet-istruzione`, `.applet-fonte`, `.frase-finale`, `.fonti`, `.home-link`) per coerenza totale — copia il blocco `<style>` da una pillola recente come base e adatta solo ciò che serve per la nuova applet.

### Registro colori per categoria

Riusa sempre lo stesso colore per la stessa categoria. Se una pillola introduce una categoria non ancora presente in questa tabella, scegli un colore distinto e coerente con la palette, poi **aggiungi la riga a questa tabella** (nel commit della pillola) così le pillole future restano coerenti.

| Categoria | Colore |
|---|---|
| Scienze | `#16a085` |
| Economia | `#2980b9` |
| Ambiente | `#27ae60` |
| Civica/Società | `#c0392b` |
| Storia | `#c0392b` |

## Cosa NON fare

- **Niente muri di testo** — nessun blocco di testo supera 4 righe consecutive
- **Niente elenchi puntati** come sostituto delle applet — se è una lista di dati, diventa un grafico
- **Niente dati senza fonte citata** — mai, nessuna eccezione
- **Niente animazioni decorative** — ogni applet illustra un concetto preciso
- **Niente articoli oltre i 4 minuti** — se l'argomento è troppo grande, si divide in due pillole (segnalalo nel commit invece di forzare tutto in una pagina)

## Processo di produzione (versione automatizzata)

Questo processo gira senza supervisione umana (attività notturna schedulata), quindi il passaggio manuale Gemini Deep Research + NotebookLM è sostituito da ricerca autonoma:

1. **L'argomento** arriva dalla prima riga di `coda-argomenti.txt`.
2. **Valutazione**: se il tema richiede dati aggiornati o fonti autorevoli (dati quantitativi recenti, argomenti tecnici con sfumature rilevanti, o temi dove un errore sarebbe grave: finanza pubblica, salute, diritto, dati ambientali), fai ricerca web autonoma (strumenti di ricerca/fetch disponibili) prima di scrivere. Usa più fonti quando possibile, preferisci fonti primarie/autorevoli (istituzioni, riviste scientifiche, enti statistici), e riporta sempre la fonte esplicita per ogni dato citato o usato in un'applet.
3. **Scrittura**: produci l'HTML completo della pillola seguendo la struttura fissa e le regole tecniche sopra.

## Gestione del sito

File da mantenere nel repo:
- `index.html` — home page con tutte le pillole
- `articoli.json` — metadati di ogni pillola (domanda, risposta breve, categoria, nome file, data)
- `coda-argomenti.txt` — coda degli argomenti ancora da pubblicare, uno per riga, in ordine
- `style-guide.md` — questo documento, non va online

**Naming convention file pillola:** `categoria-domanda-breve.html` (categoria in minuscolo, poche parole chiave della domanda separate da trattino, senza accenti). Esempi: `scienze-quando-vita.html`, `economia-cos-e-inflazione.html`.

**Home page (`index.html`):** lista di tutte le pillole in ordine cronologico inverso (la più recente in cima), un unico flusso senza sezioni per categoria. Ogni voce mostra: domanda, risposta in 2 righe, categoria (tag colorato), data, tempo di lettura, link al file.

**Checklist prima di fare commit di una nuova pillola:**
- La sezione "Fonti dei dati" è presente e compilata — se manca un dato reale, non pubblicare l'applet corrispondente
- `index.html` aggiornato con la nuova card in cima e contatore pillole incrementato
- `articoli.json` aggiornato con la nuova voce
- Nome file coerente con la naming convention e non duplicato
- Coerenza stilistica verificata con almeno una pillola recente già pubblicata
