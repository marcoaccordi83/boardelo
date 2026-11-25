# BoardElo, la pagina per gli amici (installabile)

Una piccola app web che si installa sul telefono con la sua icona (il podio con i meeple e i dadi), si apre a schermo intero e mostra la classifica anche senza rete (con l'ultimo dato salvato). I dati arrivano da Apps Script, quindi si aggiornano da soli appena inserisci una partita dal master.

## Cosa c'è in questa cartella

| File | A cosa serve |
|---|---|
| `index.html` | la pagina (classifica, Stasera, storico, statistiche) |
| `config.js` | **l'unica riga da modificare**: l'indirizzo di Apps Script |
| `manifest.webmanifest` | nome, colori e icone dell'app |
| `sw.js` | permette l'installazione e il funzionamento senza rete |
| `icons/` | l'icona in tutte le misure |

Nella cartella `icons` ci sono: `icon-192.png` e `icon-512.png` (icona normale, con angoli arrotondati), `icon-maskable-512.png` (versione adattabile per Android, con più margine), `apple-touch-icon.png` (iPhone), `favicon-32.png` e `favicon.ico` (scheda del browser, ritagliata sul meeple con la corona perché resti leggibile a pochi pixel).

## Parte 1: aggiorna Apps Script (5 minuti)

1. Sostituisci il contenuto di **Code.gs** e di **MasterJS** con i nuovi file.
2. **Distribuisci > Gestisci distribuzioni > matita > Nuova versione** per **entrambe** le distribuzioni.
3. Prova: apri in una **finestra in incognito** l'indirizzo della distribuzione Amici seguito da `?action=data`, per esempio `https://script.google.com/macros/s/.../exec?action=data`. Deve comparire un testo che inizia con `{"players":[`. Se compare una pagina di accesso a Google o un errore, la distribuzione non è su "Chiunque" (se usi l'account della scuola, l'amministratore potrebbe bloccarlo: in quel caso rifai il progetto con il Gmail personale).

## Parte 2: pubblica su GitHub (10 minuti)

1. Vai su **github.com** e crea un account (meglio con l'indirizzo personale).
2. In alto a destra: **+ > New repository**. Nome: `boardelo`. Scegli **Public**. Premi **Create repository**.
3. Nella pagina del repository clicca **uploading an existing file**. Trascina dentro **tutto il contenuto di questa cartella**, cioè `index.html`, `config.js`, `sw.js`, `manifest.webmanifest` e la cartella `icons`. Poi in fondo **Commit changes**.
4. Apri `config.js` su GitHub, clicca la matita, sostituisci `INSERISCI-QUI-L-INDIRIZZO-DI-APPS-SCRIPT` con l'indirizzo della distribuzione **Amici** (quello che finisce con `/exec`, **senza** `?m=1`), lasciando le virgolette. **Commit changes**.
5. **Settings > Pages**. Sotto "Build and deployment", Source: **Deploy from a branch**. Branch: **main**, cartella **/ (root)**. **Save**.
6. Dopo 1-2 minuti, in alto nella stessa pagina compare l'indirizzo, del tipo `https://TUONOME.github.io/boardelo/`. Aprilo.
7. Torna sul master > scheda **Dati** > "Indirizzo della pagina per gli amici": incolla questo indirizzo e premi **Salva indirizzo**. Da ora i messaggi WhatsApp lo useranno.

## Installare sul telefono

- **Android (Chrome)**: all'apertura compare il riquadro "Installa BoardElo" con il pulsante **Installa l'app**.
- **iPhone (Safari)**: tocca **Condividi** > **Aggiungi alla schermata Home**. Su iPhone Apple non permette un pulsante automatico, quindi il riquadro mostra i passaggi.
- Se il link viene aperto dentro WhatsApp, va prima aperto nel browser (menu ⋮ o icona della bussola > "Apri nel browser").

## Da sapere

- **Il repository è pubblico**, quindi chiunque lo trovi può leggere `config.js` e quindi l'indirizzo dei dati. Può solo **leggere** la classifica (nomi e punteggi). Non può modificare niente. Le Pages gratuite di GitHub richiedono un repository pubblico.
- **Aggiornare l'app**: per cambiare un file, aprilo su GitHub > matita > Commit. Perché i telefoni scarichino anche la cache nuova, cambia il numero `VERSION` in `sw.js` (ora è `v2`, poi `v3` e così via).
- **Cambiare l'indirizzo dei dati**: basta modificare `config.js`.
- **Cambiare icona**: sostituisci i file in `icons` con gli stessi nomi e cambia `VERSION` in `sw.js`. Sui telefoni dove l'app è già installata l'icona si aggiorna solo reinstallandola.
- La pagina Amici di Apps Script (azzurra) continua a funzionare e resta come riserva.
