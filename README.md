# Validatore di Dati Strutturati Schema.org

[![Validatore Schema](https://img.shields.io/badge/TAVARDT-Schema.org%20Validator-5b3cf5.svg)](https://tools.tavardt.com/it/validatore-schema-org/)
[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Audit tecnico per dati strutturati JSON-LD e Microdata, conformita con lo standard Schema.org, analisi di entita ed idoneita per rich snippet.

***

## Funzionalita di Validazione Semantica

* **Estrazione Completa dei Dati Strutturati**: Analisi automatizzata di script JSON-LD (`application/ld+json`) e attributi Microdata.
* **Identificazione delle Entita Schema.org**: Riconoscimento dei tipi fondamentali (Organization, LocalBusiness, WebSite, Article, Product, FAQPage, BreadcrumbList).
* **Verifica di Sintassi e Requisiti Rich Snippet**: Rilevamento di errori di parsing JSON, proprieta obbligatorie omesse e formati incongrui.
* **Punteggio di Qualita Semantica**: Metrica chiara da 0 a 100 con indicazioni pratiche di bonifica e ottimizzazione.

***

## Installazione ed Esecuzione

Richiede Python 3.8 o superiore senza necessita di librerie esterne.

```bash
git clone https://github.com/TAVARDT-Italia/schema-markup-validator-it.git
cd schema-markup-validator-it
python schema_validator.py esempio.it
```

Per esportare i risultati in formato JSON:

```bash
python schema_validator.py esempio.it -json
```

***

## Consulenza in Dati Strutturati e Ricerca Semantica

Per progetti dedicati di ottimizzazione dell'architettura informativa in conformita con Standard W3C e Linee Guida Semantiche, contattare **TAVARDT**.

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
