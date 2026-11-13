# Regole comuni per i siti drme.tech

Versione 1 — valide per tutti i repository di siti. Ogni repo di sito le richiama dal proprio `CLAUDE.md`.
Precedenza in caso di conflitto: richiesta esplicita del titolare → `CLAUDE.md` del sito → questo file.

---

## 1. Flusso di lavoro

1. `main` = produzione. Nessun push diretto su `main`, mai.
2. Ogni modifica parte da un branch dedicato: `feat/…`, `fix/…`, `content/…`, `chore/…`.
3. Ogni branch si integra con una Pull Request.
4. Cloudflare Pages genera un'anteprima per ogni PR: va aperta e controllata prima del merge.
5. Il merge su `main` lo approva il titolare. Il deploy in produzione parte da solo dopo il merge.
6. Staging, se serve: repo o progetto Pages separato; si porta in produzione con una PR verso il repo di produzione.

## 2. Regole per Claude

Prima di ogni modifica:
- Spiegare in 2–4 righe **cosa cambia per chi visita il sito** (non cosa cambia nel codice).
- Elencare le pagine e le lingue toccate.

Durante:
- Lavorare sempre su un branch nuovo e aprire una PR. Mai push su `main`, mai force-push su branch altrui.
- Eseguire la build in locale (`npm run build`) prima di aprire la PR; se fallisce, non aprire la PR.
- Un argomento per PR. Niente modifiche "di passaggio" non richieste.

Dopo:
- Riportare il link all'anteprima della PR e cosa è stato controllato (desktop, mobile, tutte le lingue).
- Non fare merge senza conferma esplicita del titolare.

Vietato:
- Pubblicare nomi di clienti, progetti riservati, dati personali del titolare o contenuti presi da email/Notion senza autorizzazione esplicita.
- Inserire testi direttamente nel codice (vedi §5).
- Aggiungere tracker, script di terze parti o cookie senza richiesta esplicita.

Descrizione PR (modello):
```
## Cosa cambia per chi visita il sito
…
## Pagine / lingue toccate
…
## Controlli fatti
- [ ] build locale ok
- [ ] anteprima desktop
- [ ] anteprima mobile (~400 px)
- [ ] tutte le lingue
```

## 3. Interfaccia

- Layout responsive: nessuno scroll orizzontale a 400 px; margine laterale minimo 16 px.
- Contenuti leggibili: righe di testo ~65 caratteri, gerarchia chiara h1 → h2 → h3, un solo h1 per pagina.
- Navigazione: stesse voci, stesso ordine, in tutte le pagine e lingue; voce attiva evidenziata.
- Accessibilità: contrasto AA, focus visibile da tastiera, `alt` su ogni immagine significativa (`alt=""` se decorativa), `lang` corretto sull'`<html>`.
- Movimento: animazioni solo se utili e disattivate con `prefers-reduced-motion`.
- Link esterni e email: l'indirizzo email è sempre visibile come testo, il `mailto:` è solo un aiuto.
- Ogni pagina ha `<title>`, `meta description` e tag Open Graph (titolo, descrizione, immagine 1200×630) per le anteprime su WhatsApp/LinkedIn.

## 4. Stile visivo

- Colori brand:
  - Blu: `#1877F2`
  - Testo scuro / "dr", "e" su sfondo chiaro: `#11141A`
  - Fondo scuro: `#0A0E18`
  - Bianco: `#FFFFFF`
- Logo: "dr" ed "e" nel colore del testo (nero su chiaro, bianco su scuro); "m" e ".tech" sempre blu. Icona: "d" pixel bianca a tratto singolo su quadrato blu arrotondato. Mai ricolorare, deformare o ricomporre il logo.
- Sottotitolo del logo: `drommer electronics`, minuscolo, Poppins Bold, larghezza pari a "drme.tech".
- Carattere: Poppins (Google Fonts) con fallback `system-ui, sans-serif`.
- Colori definiti solo come variabili CSS in `:root`; nessun colore letterale nei componenti.
- Tono dei testi: tecnico, diretto, frasi brevi, voce attiva. Niente superlativi vuoti.

## 5. Lingue e testi

- Tutti i testi visibili stanno in `locales/<lingua>.json` (es. `it.json`, `en.json`). Il codice e i template contengono solo chiavi.
- Lingua predefinita: italiano (`/`); altre lingue in sottocartella (`/en/`).
- Ogni chiave esiste in tutte le lingue: la build fallisce se ne manca una.
- Una nuova pagina o sezione = chiavi nuove in **tutti** i file lingua nella stessa PR.
- Segnaposto non ancora definitivi: scritti come `[[NOME]]` e segnalati nella descrizione della PR.

## 6. File e versioni

- Asset consegnati fuori dal repo (logo, immagini, documenti) includono il numero di versione nel nome: `nome_vN.ext`.
- Dentro il repo gli asset usati dal sito hanno nomi stabili (es. `logo.png`); la storia la tiene git.
