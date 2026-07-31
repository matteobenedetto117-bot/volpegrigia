# Style guide — La volpe grigia

> Documento interno. Non va online, non va linkato da nessuna pagina pubblica.

## Identità del progetto

Sito personale di divulgazione culturale. Ogni pagina risponde a una domanda precisa — su scienze, ambiente, economia, società, storia, filosofia, letteratura, o qualsiasi altro tema. Nessun limite tematico. Tono chiaro e accessibile (livello liceo scientifico come riferimento di semplicità), mai banale — come un bravo professore che racconta, non che recita.

## Standard di riferimento

`lingua-al-verde-origine.html` è il livello di qualità da eguagliare o superare per **ogni** nuova pillola, non un'eccezione. Prima di scrivere, riletti quel file (testo e markup, non solo l'anteprima) e usalo come metro:

- **4 applet, tutte diverse tra loro e cucite su misura sull'argomento**: una scena SVG animata e cliccabile (la candela dell'asta), un esploratore di ipotesi con una barra di "solidità documentaria" che cambia a ogni selezione, una timeline narrativa con dettaglio ricco per ogni tappa, un confronto multilingua con traduzione letterale. Nessuna di queste è "un grafico a barre" o "uno slider" generico: ognuna racconta una parte diversa della risposta con un meccanismo diverso.
- **Testo denso di dettagli concreti**: nomi di persone, titoli di opere, anni precisi, citazioni dirette virgolettate («la candela è al verde», «nel tempo che abbrucia una piccolissima candela di cera tinta da piede di color verde»). Non frasi di raccordo generiche — ogni paragrafo aggiunge un fatto specifico che altrove non c'è.
- **Fonti nominate e circostanziate**, non solo "Treccani" o "FAO" ma titolo dell'articolo/libro, autore, anno, e quando possibile la citazione esatta che la fonte riporta.

Pagine come `ambiente-meccanizzazione-agricola.html` (applet: un grafico a barre, un confronto a barre orizzontali, uno slider — tutti variazioni dello stesso schema, testo che introduce ma non approfondisce) sono l'esempio di cosa NON ripetere. Non vanno riscritte retroattivamente, ma segnano lo standard precedente da abbandonare.

## Formato delle pillole

Ogni pagina è una **pillola**: si legge in **3-4 minuti** (raramente 5 se l'argomento lo richiede davvero), e la maggior parte del contenuto è visiva e interattiva. Il testo introduce, collega e **approfondisce con dettagli concreti** — le applet mostrano, il testo racconta ciò che l'applet non può mostrare (aneddoti, contesto, citazioni, implicazioni).

Struttura fissa, in quest'ordine:

1. **La domanda** — titolo in forma di domanda diretta
2. **La risposta in 2 righe** — evidenziata, subito visibile (risposta-box)
3. **Testo** — non un minimo indistinto: **5-8 paragrafi brevi in tutto l'articolo** (non 3-4), ognuno max 3-4 righe, mai due consecutivi (sempre separati da almeno un'applet). Più paragrafi = più fatti concreti distribuiti nel pezzo, non riempitivo: se un paragrafo non aggiunge un'informazione nuova, va tolto, non allungato.
4. **Applet / grafici / linee del tempo** — **almeno 3, idealmente 4**, di tipi diversi tra loro e pensate apposta per l'argomento (vedi sezione "Standard di riferimento"), sono il corpo principale
5. **Una frase da portarsi a casa** — chiude il pezzo, in corsivo (frase-finale)
6. **Fonti** — puntuali, con autore/titolo/anno, in fondo (sezione "Fonti dei dati", MAI assente)

**Regola aurea:** se una cosa si può mostrare con un'applet, non si spiega a parole. Ma il testo che resta deve valere la lettura, non essere solo collante.

## Applet interattive — regole tecniche

Sono il cuore di ogni pillola. Ogni pillola ne ha **almeno 3, idealmente 4**, di tipi diversi tra loro e non intercambiabili.

- Solo HTML + CSS + JavaScript vanilla (nessuna libreria esterna tranne Chart.js per i grafici, caricato da CDN come nelle pillole esistenti)
- Canvas API e SVG animato/interattivo sono ammessi e incoraggiati per le simulazioni — non solo Chart.js
- **Prima di scegliere il tipo di applet, chiediti: "qual è il meccanismo concreto di questo argomento, e come lo rendo manipolabile?"** (la candela che brucia, non solo la sua durata media in un grafico). Progetta l'interazione sull'argomento specifico, non pescando da una lista di template intercambiabili.
- Tipi possibili (elenco di ispirazione, non un menù a caselle da riempire meccanicamente):
  - **Scene animate/cliccabili in SVG** — un oggetto o processo concreto che l'utente aziona (accendere una candela, ruotare un pallone, far crollare una diga) con stati visivi che cambiano
  - **Esploratori di ipotesi/opzioni** — l'utente seleziona un'ipotesi tra varie e vede argomenti a favore/contro e un indicatore di quanto è solida (con criterio esplicitato in didascalia)
  - **Linee del tempo narrative** — non solo punti su un asse: ogni tappa ha un dettaglio specifico che si legge cliccandola
  - **Grafici dinamici** — Chart.js con dati reali, fonte sempre citata sotto
  - **Confronti multipli** — toggle o selettori che cambiano l'intera visualizzazione (es. confronto tra lingue, tra epoche, tra paesi), non solo due stati
  - **Calcolatori** — l'utente inserisce un valore e vede il risultato in tempo reale, con confronto ad altri valori noti
- Ogni applet ha: titolo, istruzione breve che invita all'azione ("Accendi la candela e prova a...", "Seleziona un'ipotesi per..."), didascalia con fonte puntuale

## Stile visivo

- **Sfondo**: `#fdfcf9` — **testo**: `#1c1c2e` — molto spazio bianco
- **Font**: Playfair Display per titoli, Source Sans 3 per corpo testo, da Google Fonts
- **Layout**: max-width 640px, centrato, responsive mobile-first
- **Densità**: tanto spazio bianco tra i blocchi — ogni applet respira
- Riusa sempre le stesse classi CSS di base delle pillole esistenti (`.tag`, `.risposta-box`, `.meta`, `.testo`, `.applet`, `.applet-header`, `.applet-titolo`, `.applet-istruzione`, `.applet-fonte`, `.frase-finale`, `.fonti`, `.home-link`) per coerenza strutturale — copia il blocco `<style>` da `lingua-al-verde-origine.html` come base e aggiungi solo le classi nuove che ti servono per l'applet specifica (es. `.asta-scena`, `.ipo-lista`, `.tl-track`: nomi descrittivi del contenuto, non rinominare le classi strutturali di base che già esistono).

### Registro colori per categoria

Riusa sempre lo stesso colore per la stessa categoria. Se una pillola introduce una categoria non ancora presente in questa tabella, scegli un colore distinto e coerente con la palette, poi **aggiungi la riga a questa tabella** (nel commit della pillola) così le pillole future restano coerenti.

| Categoria | Colore |
|---|---|
| Scienze | `#16a085` |
| Economia | `#2980b9` |
| Ambiente | `#27ae60` |
| Civica/Società | `#c0392b` |
| Storia | `#c0392b` |
| Salute | `#8e44ad` |
| Lingua | `#d35400` |
| Demografia | `#7f8c8d` |
| Neuroscienze | `#9b59b6` |
| Fisica | `#f39c12` |

## Cosa NON fare

- **Niente muri di testo** — nessun blocco di testo supera 4 righe consecutive
- **Niente paragrafi di puro raccordo** — ogni paragrafo deve contenere almeno un fatto, nome, data o citazione specifica; se dice solo "ora vediamo un altro aspetto", va riscritto o tolto
- **Niente applet intercambiabili** — se togliendo il titolo un'applet potrebbe appartenere a qualsiasi altra pillola del sito, non è abbastanza su misura
- **Niente elenchi puntati** come sostituto delle applet — se è una lista di dati, diventa un grafico o un esploratore cliccabile
- **Niente dati senza fonte citata puntualmente** (autore/titolo/anno, non solo il nome dell'ente) — mai, nessuna eccezione
- **Niente animazioni decorative** — ogni applet illustra un meccanismo preciso
- **Niente articoli oltre i 4-5 minuti** — se l'argomento è troppo grande, si divide in due pillole (segnalalo nel commit invece di forzare tutto in una pagina)

## Processo di produzione (versione automatizzata)

Questo processo gira senza supervisione umana (attività notturna schedulata), quindi il passaggio manuale Gemini Deep Research + NotebookLM è sostituito da ricerca autonoma:

1. **L'argomento** arriva dalla prima riga di `coda-argomenti.txt`.
2. **Ricerca**: fai sempre ricerca web autonoma prima di scrivere, anche per argomenti che sembrano "noti" — è la ricerca che fornisce i dettagli concreti (nomi, date, citazioni dirette) richiesti dallo standard di riferimento sopra, non solo i numeri. Usa più fonti quando possibile, preferisci fonti primarie/autorevoli (istituzioni, riviste scientifiche, enti statistici, testi originali quando reperibili), e riporta sempre la fonte puntuale (autore/titolo/anno) per ogni dato o citazione usata.
3. **Scrittura**: produci l'HTML completo della pillola seguendo la struttura fissa, le regole tecniche e lo standard di riferimento sopra. Prima di committare, rileggi il pezzo chiedendoti: "questa applet potrebbe stare pari pari in un'altra pillola?" — se sì, ripensala.

## Gestione del sito

File da mantenere nel repo:
- `index.html` — home page con tutte le pillole
- `articoli.json` — metadati di ogni pillola (domanda, risposta breve, categoria, nome file, data)
- `coda-argomenti.txt` — coda degli argomenti ancora da pubblicare, uno per riga, in ordine
- `style-guide.md` — questo documento, non va online

**Naming convention file pillola:** `categoria-domanda-breve.html` (categoria in minuscolo, poche parole chiave della domanda separate da trattino, senza accenti). Esempi: `scienze-quando-vita.html`, `economia-cos-e-inflazione.html`.

**Formato di `coda-argomenti.txt`:** una riga per argomento, campi separati da `|`: `Categoria|Domanda|Suggerimento`. Il terzo campo (suggerimento) è opzionale e può essere vuoto (`Categoria|Domanda|`): quando presente è una traccia di risposta o un punto di partenza per la ricerca fornito dall'utente, da verificare e approfondire comunque con ricerca autonoma, non da copiare così com'è. La categoria nella coda è quella da usare: se non è già nella tabella colori qui sopra, scegli un colore coerente e aggiungi la riga. Se una riga della coda fosse in un formato vecchio (solo testo, senza `|`), trattala come domanda con categoria da dedurre tu.

**Home page (`index.html`):** lista di tutte le pillole in ordine cronologico inverso (la più recente in cima), un unico flusso senza sezioni per categoria. Ogni voce mostra: domanda, risposta in 2 righe, categoria (tag colorato), data, tempo di lettura, link al file.

**Checklist prima di fare commit di una nuova pillola:**
- Almeno 3 applet (idealmente 4), tutte di tipo diverso e pensate su misura per l'argomento — nessuna sarebbe intercambiabile con un'altra pillola
- Il testo ha 5-8 paragrafi brevi, ognuno con almeno un fatto/nome/data/citazione concreta, mai riempitivo
- La sezione "Fonti dei dati" è presente, compilata, con autore/titolo/anno puntuali — se manca un dato reale, non pubblicare l'applet corrispondente
- `index.html` aggiornato con la nuova card in cima e contatore pillole incrementato
- `articoli.json` aggiornato con la nuova voce
- Nome file coerente con la naming convention e non duplicato
- Coerenza stilistica verificata con `lingua-al-verde-origine.html` (classi CSS di base riusate, stesso impianto visivo)
