# Watoto Kenya ODV — Piano di migrazione a WordPress (aggiornato)

Aggiornato sulla versione attuale del sito (v27 dell'anteprima). Sostituisce il piano iniziale.
Inventario completo e leggibile da script: `WP-modello-contenuti.json`.

## 1. Cosa è cambiato rispetto al piano iniziale

| Punto | Piano iniziale | Stato attuale | Conseguenza |
|---|---|---|---|
| Pagine | 21 pagine + 10 news + 9 progetti | **81 pagine** (45 IT + 36 EN): 1 home, 9 pagine, 11 progetti, 22 news (13 in EN), 2 pagine legali per lingua | Il vecchio WXR e le bozze nell'archivio sono **obsoleti**: non vanno importati |
| Grafica | Tema verde dell'archivio | Blu notte + rosso e oro del logo, testate con foto, animazioni | Il vecchio tema (`watoto-kenya/`) non si riusa: si parte dal CSS/JS del sito attuale |
| Contenuti nuovi | — | Numeri in home, "Voci da Makobeni", 5×1000, Tre modi per aiutare, Dona online, Copia IBAN, Dove siamo, filtro news per anno, condividi, Privacy e Cookie | Servono blocchi e impostazioni globali nuovi (sezioni 3 e 4) |
| Galleria | non prevista | **da prevedere** | Nuovo tipo di contenuto e blocco (sezione 5) |
| Archivio storico | 13 articoli, alcuni danneggiati | 15 articoli ricostruiti + 7 punti con `[testo da completare]` + 45 file mancanti | Vanno chiusi prima dell'importazione (sezione 8) |

Decisioni confermate: tema classico PHP + editor a blocchi (Gutenberg) per i contenuti, due lingue con collegamento IT/EN, indirizzo `/en/`, staging separato dal sito in produzione.

## 2. Tipi di contenuto

| Tipo | Uso | Campi propri | Note |
|---|---|---|---|
| **Pagina** | Home, Chi siamo, Vision e Mission, Organizzazione, Bilancio, Collaborazioni, Contatti, Sostienici, News ed eventi, Progetti, Privacy, Cookie | foto di testata, sottotitolo, posizione della foto | Costruita con blocchi (sezione 3) |
| **Progetto** (CPT) | 11 schede + indice e archivio progetti | testata, sintesi, stato (attivo/archivio), immagini | L'elenco "Tutti i progetti" e le card in home si generano da qui |
| **News** (CPT) | 22 articoli IT, 13 EN | data, immagine, estratto, anno (automatico) | Filtro per anno e condividi diventano funzioni del tema |
| **Album** (CPT, nuovo) | Galleria fotografica | titolo, data, luogo, progetto collegato, foto con didascalia e testo alternativo | Sezione 5 |
| **Bilancio** (CPT, facoltativo) | 10 PDF dal 2015 al 2024 | anno, file PDF | Se si vuole aggiungere un anno senza toccare la pagina |

Tassonomie: `anno` (news, automatica dalla data), `categoria` (news: progetti, eventi, bilanci), `argomento` (album).

## 3. Blocchi su misura (dai 29 tipi di sezione del sito)

Ogni sezione del sito statico diventa un blocco con campi modificabili dallo staff. I nomi di classe CSS restano uguali, così la grafica non cambia.

| Blocco | Sezioni attuali | Campi |
|---|---|---|
| **Testata con foto** | `about-hero`, `article-hero`, `inner-hero`, `donation-hero` | foto, titolo, sottotitolo, etichetta, posizione foto. Altezza unica (660 px) decisa dal tema |
| **Hero con carosello** | `hero` (home) | fino a 5 slide: foto, testo alternativo, titolo, bottoni |
| **Testo + immagine** | `intro`, `about-story`, `article-layout` | titolo, testo, immagine, link |
| **Card di valori / numeri** | `about-values`, `stats` | 3–4 elementi con titolo e testo (numeri: valore, suffisso, descrizione) |
| **Card progetti / news** | `section wrap` (progetti), `news-section` | automatico dai CPT, con numero di card |
| **Voci** | `voices` | 3 schede: etichetta, citazione, firma, link a una news |
| **Fascia di invito (CTA)** | `support`, `about-callout` | titolo, testo, bottone, foto |
| **5×1000** | `cinque` | testo e codice fiscale (dalle impostazioni globali) |
| **Dona** | `online-card`, `bank-card`, `ways` | importi, link PayPal, dati bancari (dalle impostazioni globali) |
| **Dove siamo** | `where` | titolo, testo, link mappa |
| **Partner** | `partners-section`, `partners-group` | gruppi di loghi con nome e link |
| **Documenti** | `document-section` | anno, titolo, file |
| **Contatti** | `contact-layout`, `contact-form-section` | testi; modulo con invio vero |
| **Galleria** | nuovo | album, numero di foto, layout |
| **Testo legale** | `legal` | testo libero |

Script che restano com'è: menu mobile, carosello con pausa, conteggio numeri, comparsa animata, copia IBAN/link, rispetto di "riduci movimento". Si caricano solo dove servono.

## 4. Impostazioni globali (una sola volta, per lingua)

Pagina "Impostazioni Watoto" nel pannello, così chi aggiorna non tocca il codice:
- ragione sociale, indirizzo, codice fiscale, email, PEC;
- IBAN, banca, SWIFT, intestazione del conto (**da confermare**), causale;
- link PayPal e importi suggeriti; link newsletter; profili social;
- i 4 numeri della home e la loro fonte;
- testo del 5×1000;
- logo, colori, foto di default delle testate.

## 5. Galleria fotografica

- **Struttura:** ogni album è un contenuto con titolo, data, luogo e collegamento opzionale a un progetto. Le foto stanno nella libreria media, con didascalia e testo alternativo in italiano e inglese.
- **Pagina Galleria:** griglia di album con foto di copertina, filtro per argomento (Scuola, Alimentazione, Kit dignità, Eventi) e pagina del singolo album con griglia di miniature.
- **Visualizzazione ingrandita (lightbox):** leggera, senza librerie esterne, con tastiera, tasto Esc, focus gestito e frecce; rispetta "riduci movimento".
- **Velocità:** immagini WebP in più misure, caricamento differito, rapporto fisso per evitare scatti.
- **Home:** blocco "Ultimi album" facoltativo; gli stessi album possono comparire nelle schede progetto.
- **Privacy:** pubblicare foto di minori richiede il consenso dei genitori o di chi ne ha la tutela. Va deciso prima, con una regola semplice per lo staff (per esempio: nessun nome, nessun volto riconoscibile senza liberatoria). È la questione più importante della galleria.
- **Nel sito statico** non la aggiungiamo ora: la progettiamo in WordPress direttamente. Se vuoi vederne il disegno prima, posso preparare una pagina di prova.

## 6. Lingue

- Ogni contenuto italiano ha il collegamento alla sua versione inglese. Oggi la copertura è: pagine e progetti 1:1; news 13 su 22, con 2 coppie con indirizzi diversi (kit 8×1000, colazione per tutti).
- Le notizie senza traduzione restano solo in italiano, senza finta pagina inglese. Il selettore lingua porta alla home inglese.
- Le stringhe fisse dell'interfaccia ("Leggi la notizia", "Condividi", "Copia link", "Dona online", ecc.) vanno nel sistema di traduzione delle stringhe.
- **Plugin:** WPML (a pagamento) resta il più completo; Polylang gratuito basta per due lingue. Decisione da prendere prima di iniziare, perché cambia la struttura dei contenuti.
- Indirizzi: `/` per l'italiano, `/en/` per l'inglese, con hreflang e sitemap nel plugin SEO.

## 7. Funzioni che oggi non esistono davvero

- **Modulo contatti:** invio vero con protezione antispam e conferma di consegna.
- **Pagamento online:** collegamento PayPal; se in futuro si usano cookie, aggiornare Privacy e Cookie.
- **Newsletter:** servizio esterno con pagina di iscrizione; il tema mostra il link solo se impostato.
- **Sicurezza e backup:** aggiornamenti, backup automatici, limitazione dei tentativi di accesso, ruoli (redattore senza accesso al tema).
- **Velocità:** cache di pagina, immagini WebP, nessun font esterno, CSS/JS minimi (oggi 93–100 su Lighthouse: è il traguardo da mantenere).
- **Intestazioni di sicurezza** (CSP, ecc.): oggi nel file `_headers`/`.htaccess`; in WordPress vanno impostate dal server o da un plugin, evitando script e stili in linea.

## 8. Cose da chiudere nel sito statico prima di migrare

Sono già in elenco, e conviene farle ora perché dopo costano il doppio:
1. Link PayPal e dicitura del conto.
2. Le **foto vere** al posto di quelle illustrative (Makobeni, Autonomia, schede progetto, news con clip-art) e la dicitura "Immagini illustrative provvisorie".
3. I **7 testi** `[testo da completare]` e i **45 file** del vecchio sito (`MEDIA-MANCANTI.md`).
4. Conferma dei 4 numeri e del 5×1000 (elenco beneficiari).
5. Revisione legale di Privacy e Cookie.
6. Definire le regole sulla galleria e le liberatorie.

## 9. Come si fa il passaggio (in ordine)

1. **Staging:** WordPress pulito, stesso PHP dell'hosting finale, in un indirizzo separato (nessun accesso ai motori di ricerca).
2. **Tema classico:** partenza dal CSS/JS attuale (un file per lingua e per pagina, oggi già ottimizzati), header, footer, menu a due livelli, menu mobile.
3. **Blocchi e tipi di contenuto** (sezioni 2–4): prima i blocchi più usati (testata, testo+immagine, card, CTA), poi quelli specifici.
4. **Generatore di importazione:** uno script legge `WP-modello-contenuti.json` e l'HTML del sito e produce il file di importazione (WXR) con i contenuti già nei blocchi, i metadati SEO e i collegamenti di lingua. Si può rilanciare ogni volta che il sito statico cambia, finché non si passa a WordPress.
5. **Immagini:** caricamento nella libreria media con testi alternativi.
6. **Confronto pagina per pagina** con il sito statico (come per le testate): desktop, tablet, telefono.
7. **Funzioni** (sezione 7), poi **SEO**: titoli, descrizioni, dati strutturati, sitemap, reindirizzamenti dai vecchi indirizzi del sito attuale.
8. **Prove finali:** velocità, accessibilità (axe e tastiera), invio del modulo, lingue, link. Solo dopo, pubblicazione.

## 10. Cosa posso fare io e cosa no

- **Io:** tema, blocchi, tipi di contenuto, generatore di importazione, prove in un WordPress locale (installato in questo ambiente), confronto grafico, test.
- **Tu / l'hosting:** staging e hosting, installazione del tema e dell'importazione, plugin a pagamento (se WPML), foto e testi mancanti, liberatorie, collegamento PayPal e newsletter, prova del modulo su server vero.

## 11. Decisioni che mi servono

1. WPML o Polylang.
2. Hosting: quello del vecchio sito o uno nuovo.
3. Chi aggiornerà il sito (cambia quanto semplifichiamo i blocchi).
4. Album: si pubblicano foto con volti di minori? Con quali regole?
5. Bilanci: pagina semplice o CPT.
