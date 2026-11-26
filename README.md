<p align="center">
  <a href="https://ag.tavardt.com/it/">
    <img src="https://ag.tavardt.com/img/tavardt-banner.png" alt="TAVARDT" width="1024" />
  </a>
</p>

# Validatore di Dati Strutturati e Schema.org

[![Validatore Schema](https://img.shields.io/badge/TAVARDT-Schema.org%20Validator-5b3cf5.svg)](https://tools.tavardt.com/it/validatore-schema-markup/)
[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Motore tecnico per la validazione di dati strutturati Schema.org nei formati JSON-LD e Microdati, verificando relazioni tra entità, proprietà obbligatorie ed idoneità per i risultati avanzati.

Lo strumento estrae le strutture semantiche dagli ambienti web in produzione per individuare errori di sintassi JSON, schemi lacunosi ed omissioni di proprietà essenziali richieste dai motori di ricerca e dai sistemi di intelligenza artificiale. Sviluppato senza dipendenze software esterne, opera nativamente da riga di comando Python e all'interno delle pipeline di CI/CD.

***

## Capacità di Validazione Semantica ed Entità Supportate

I motori di ricerca e i flussi di recupero neurale fanno affidamento su dati strutturati espliciti per contestualizzare aziende, accertare le firme autoriali ed esporre rich snippet. Errori di sintassi o assenza di proprietà fondamentali comportano la perdita immediata della visibilità avanzata nelle pagine dei risultati.

* **Estrazione Completa dei Dati Strutturati**: Analisi automatizzata di blocchi JSON-LD (`application/ld+json`) e riconoscimento di annotazioni Microdati (`itemscope`, `itemtype`) nel codice sorgente.
* **Gestione di Grafi Semantici**: Navigazione trasparente di gerarchie complesse basate su `@graph`, risolvendo nodi di entità interconnesse nelle applicazioni web moderne.
* **Controllo dei Modelli Schema.org**: Verifica della presenza delle proprietà obbligatorie nelle classi primarie: Organization, LocalBusiness, WebSite, Article, NewsArticle, BlogPosting, Product, BreadcrumbList e FAQPage.
* **Audit di Sintassi e Correttezza**: Sistema di penalizzazioni deduttive per JSON malformato (-20 punti), assenza di JSON-LD (-40 punti), mancanza di entità identificabili (-30 punti) e omissione di campi raccomandati (-5 punti ciascuno).
* **Indice Numerico di Qualità Semantica**: Punteggio oggettivo da 0 a 100 che classifica il livello di conformità in OPTIMAL, WARNING o CRITICAL fornendo indicazioni di bonifica prioritizzate.

***

## Matrice di Ispezione delle Entità Semantiche

<table>
  <thead>
    <tr>
      <th align="left">Classe di Entità</th>
      <th align="left">Proprietà Obbligatorie</th>
      <th align="left">Regola di Penalizzazione</th>
      <th align="left">Impatto sui Risultati Avanzati e sull'Indexazione</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Organization</strong></td>
      <td><code>name</code>, <code>url</code></td>
      <td>-5 Punti per proprietà mancante</td>
      <td>Identifica l'entità aziendale e stabilisce il riferimento canonico nei grafi di conoscenza.</td>
    </tr>
    <tr>
      <td><strong>LocalBusiness</strong></td>
      <td><code>name</code>, <code>address</code></td>
      <td>-5 Punti per proprietà mancante</td>
      <td>Essenziale per il posizionamento locale, la presenza sulle mappe e le ricerche di prossimità.</td>
    </tr>
    <tr>
      <td><strong>WebSite</strong></td>
      <td><code>name</code>, <code>url</code></td>
      <td>-5 Punti per proprietà mancante</td>
      <td>Abilita il box di ricerca sitelinks e definisce il perimetro ufficiale del dominio.</td>
    </tr>
    <tr>
      <td><strong>Article / NewsArticle</strong></td>
      <td><code>headline</code>, <code>author</code></td>
      <td>-5 Punti per proprietà mancante</td>
      <td>Qualifica per l'inclusione nel carosello Notizie Principali e l'ancoraggio delle fonti negli LLM.</td>
    </tr>
    <tr>
      <td><strong>BlogPosting</strong></td>
      <td><code>headline</code>, <code>author</code></td>
      <td>-5 Punti per proprietà mancante</td>
      <td>Attesta la paternità editoriale e la cronologia temporale delle pubblicazioni.</td>
    </tr>
    <tr>
      <td><strong>Product</strong></td>
      <td><code>name</code>, <code>offers</code></td>
      <td>-5 Punti per proprietà mancante</td>
      <td>Attiva i rich snippet con prezzi di vendita, disponibilità a magazzino e recensioni.</td>
    </tr>
    <tr>
      <td><strong>BreadcrumbList</strong></td>
      <td><code>itemListElement</code></td>
      <td>-5 Punti per proprietà mancante</td>
      <td>Mostra percorsi di navigazione gerarchici leggibili nelle SERP al posto degli URL grezzi.</td>
    </tr>
    <tr>
      <td><strong>FAQPage</strong></td>
      <td><code>mainEntity</code></td>
      <td>-5 Punti per proprietà mancante</td>
      <td>Genera sezioni di domande e risposte a fisarmonica visibili nei risultati di ricerca.</td>
    </tr>
  </tbody>
</table>

***

## Installazione e Guida Rapida all'Uso

Richiede Python 3.8 o superiore sfruttando unicamente i moduli della libreria standard (`sys`, `re`, `json`, `ssl`, `argparse`, `urllib.request`, `urllib.error`). Non è richiesta alcuna installazione aggiuntiva tramite pip.

Clonare il repository ed eseguire la verifica sul dominio prescelto:

```bash
git clone https://github.com/TAVARDT-Italia/schema-markup-validator-it.git
cd schema-markup-validator-it
python schema_validator.py esempio.it
```

Per ottenere i risultati in formato strutturato JSON:

```bash
python schema_validator.py esempio.it -j
```

Ispezionare i domini impostando un intervallo di timeout personalizzato:

```bash
python schema_validator.py https://esempio.it -j -t 12
```

Esempio di payload JSON ottenuto:

```json
{
  "target": "https://esempio.it",
  "score": 95,
  "status": "OPTIMAL",
  "json_ld_blocks": 1,
  "entities": [
    "Organization",
    "WebSite"
  ],
  "microdata_detected": false,
  "issues": [
    "Entity 'Organization' is missing recommended property: url"
  ],
  "recommendations": [
    "Add missing property 'url' to 'Organization' entity."
  ]
}
```

Fasce di classificazione della qualità:

* **Punteggio da 85 a 100 (OPTIMAL)**: Dati strutturati di alto livello con copertura esaustiva delle entità e totale assenza di errori di sintassi.
* **Punteggio da 65 a 84 (WARNING)**: Omissioni minori di proprietà o schemi parziali che possono limitare l'ottenimento di rich snippet.
* **Punteggio da 0 a 64 (CRITICAL)**: Sintassi JSON corrotta, assenza di dati strutturati o schemi inaccessibili che richiedono correzione tempestiva.

***

## Domande Frequenti (FAQ Tecnico)

### Per quale motivo il formato JSON-LD è preferibile rispetto ai Microdati per i rich snippet e i sistemi IA?
Il formato JSON-LD mantiene i dati strutturati in script indipendenti, consentendone la manutenzione senza modificare la struttura grafica visibile agli utenti. Inoltre, i principali motori di ricerca e i crawler IA consigliano JSON-LD perché può essere inserito dinamicamente e analizzato senza il costo computazionale del rendering visivo.

### In che modo il validatore gestisce le matrici `@graph` nelle implementazioni JSON-LD complesse?
Quando rileva la chiave `@graph`, lo strumento esamina l'array di sotto-oggetti dichiarati, verificando i requisiti di ciascuna entità in modo ricorsivo. Ciò garantisce una convalida completa dei grafi semantici interconnessi.

### Quali penalizzazioni algoritmiche vengono applicate a fronte di errori nei dati strutturati?
Il software sottrae 40 punti se non individua alcun blocco JSON-LD, 20 punti per ciascun blocco contenente sintassi JSON non valida e 30 punti se non rileva entità riconosciute. Inoltre, ogni proprietà raccomandata assente deduce 5 punti dalla valutazione iniziale di 100.

### Come procede lo script nell'analisi semantica senza impiegare un browser headless?
Il software invia richieste HTTP GET mirate specificando un User-Agent identificativo, acquisendo il codice HTML della pagina. Espressioni regolari ottimizzate isolano il contenuto dei tag script, processato poi dal modulo JSON nativo in una frazione di secondo.

### Come possono i team di sviluppo integrare questa validazione nei controlli automatizzati di CI/CD?
Eseguendo `schema_validator.py` con l'opzione `-j`, i sistemi di compilazione possono raccogliere il JSON e analizzarlo mediante jq. È possibile stabilire regole che interrompono la pipeline qualora il punteggio scenda al di sotto di 85 o compaiano elementi nell'elenco `issues`.

***

## Consulenza in Architettura Semantica e Grafi di Conoscenza

Per la modellazione di dati strutturati, l'ingegneria dei grafi di conoscenza e l'allineamento con gli standard W3C in Italia, contattare gli specialisti di **TAVARDT Italia**.

***

## Link Utili

* **Portale Aziendale:** https://ag.tavardt.com/it/
* **Suite di Diagnostica:** https://tools.tavardt.com/it/
* **Contatto Tecnico:** https://ag.tavardt.com/it/contatto/

***

### Licenza
Rilasciato sotto licenza MIT.

***

© 2026 TAVARDT. Tutti i diritti riservati.
