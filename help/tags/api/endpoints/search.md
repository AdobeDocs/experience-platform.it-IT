---
title: Endpoint “search”
description: Scopri come effettuare chiamate all’endpoint /search nell’API di Reactor.
exl-id: 14eb8d8a-3b42-42f3-be87-f39e16d616f4
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 97%

---

# Endpoint “search”

L’endpoint `/search` nell’API di Reactor consente di trovare le risorse che corrispondono ai criteri desiderati, espressi come query.

È possibile cercare i seguenti tipi di risorse API, utilizzando la stessa struttura di dati dei documenti basati sulle risorse restituiti nell’API:

* `audit_events`
* `builds`
* `callbacks`
* `data_elements`
* `environments`
* `extension_packages`
* `extensions`
* `hosts`
* `libraries`
* `properties`
* `rule_components`
* `rules`

L’ambito di tutte le query corrisponde all’azienda corrente e alle proprietà accessibili.

>[!IMPORTANT]
>
>Avvertenze ed eccezioni applicabili alla funzionalità di ricerca:
>* I metadati non sono ricercabili e non vengono restituiti nei risultati della ricerca.
>* I campi dello schema per i delegati del pacchetto di estensione (azioni, condizioni, ecc.) sono ricercabili come testo, ma non come struttura di dati nidificata.
>* Le query di intervallo al momento supportano solo i numeri interi.

Per ulteriori informazioni su come utilizzare questa funzionalità, consulta la [guida alla ricerca](../guides/search.md).

## Introduzione

L’endpoint utilizzato in questa guida fa parte dell’[API di Reactor](https://www.adobe.io/experience-platform-apis/references/reactor/). Prima di continuare, consulta la [guida introduttiva](../getting-started.md) per informazioni importanti su come eseguire l’autenticazione nell’API.

## Eseguire una ricerca {#perform}

Per eseguire una ricerca, devi eseguire una richiesta POST.

**Formato API**

```http
POST /search
```

**Richiesta**

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "from": 0,
          "size": 25,
          "query": {
            "attributes.name": {
              "value": "Performance"
            },
            "attributes.revision_number": {
              "range": {
                "lte": "2",
                "gt": "0"
              }
            }
          },
          "sort": [
            {
              "attributes.revision_number": "desc"
            }
          ],
          "resource_types": [
            "data_elements",
            "rule_components"
          ]
        }
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `from` | Numero di risultati oltre i quali veranno inclusi nella risposta. |
| `size` | Quantità massima di risultati da restituire. I risultati non possono superare i 100 elementi. |
| `query` | Oggetto che rappresenta la query di ricerca. Per ogni proprietà di questo oggetto, la chiave deve rappresentare un percorso di campo da considerare per la query; il valore deve essere un oggetto le cui sottoproprietà determinano per cosa viene eseguita la query.<br><br>Per ogni percorso di campo, puoi utilizzare le seguenti sottoproprietà:<ul><li>`exists`: restituisce true se il campo esiste nella risorsa.</li><li>`value`: restituisce true se il valore del campo corrisponde al valore di questa proprietà.</li><li>`value_operator`: logica booleana utilizzata per determinare come deve essere gestita una query `value`. I valori consentiti sono `AND` e `OR`. Se non specificato, viene utilizzata la logica `AND`. Per ulteriori informazioni, consulta la sezione relativa alla [logica dell’operatore dei valori](#value-operator)</li><li>`range`: restituisce true se il valore del campo rientra in un intervallo numerico specifico. L’intervallo stesso è determinato dalle seguenti sottoproprietà:<ul><li>`gt`: maggiore del valore specificato, escluso il valore specificato stesso.</li><li>`gte`: maggiore o uguale al valore specificato.</li><li>`lt`: minore del valore specificato, escluso il valore specificato stesso.</li><li>`lte`: minore o uguale al valore specificato.</li></ul></li></ul> |
| `sort` | Matrice di oggetti che indica l’ordine in cui elencare i risultati. Ogni oggetto deve contenere una singola proprietà: la chiave rappresenta il percorso del campo in base al quale eseguire l’ordinamento; il valore rappresenta l’ordinamento (`asc` per crescente, `desc` per decrescente). |
| `resource_types` | Matrice di stringhe che indica i tipi di risorse specifici da cercare. |

{style="table-layout:auto"}

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco di risorse corrispondenti per la query. Per informazioni dettagliate sulle modalità in cui l’API determina le corrispondenze per valori specifici, consulta la sezione dell’appendice sulle [convenzioni di corrispondenza](#conventions).

```json
{
  "data": [
    {
      "id": "DE5d11b3ed301d4ce99b530a5121e392b2",
      "type": "data_elements",
      "attributes": {
        "created_at": "2020-12-14T17:36:09.045Z",
        "deleted_at": null,
        "dirty": true,
        "enabled": true,
        "name": "Performance Indicator",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:36:09.045Z",
        "clean_text": false,
        "default_value": null,
        "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
        "force_lower_case": false,
        "review_status": "unsubmitted",
        "storage_duration": null,
        "settings": "{\"elementProperty\":\"html\",\"elementSelector\":\".target-element\"}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/property"
          },
          "data": {
            "id": "PR97d92a379a5f48758947cdf44f607a0d",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/origin"
          },
          "data": {
            "id": "DE5d11b3ed301d4ce99b530a5121e392b2",
            "type": "data_elements"
          }
        },
        "extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/extension"
          },
          "data": {
            "id": "EX0348d463358c4c89afe726245576f112",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "updated_with_extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/updated_with_extension"
          },
          "data": {
            "id": "EX1cc78b39339242da82a0e0752fa53375",
            "type": "extensions"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d",
        "origin": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2",
        "self": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2",
        "extension": "https://reactor.adobe.io/extensions/EX0348d463358c4c89afe726245576f112"
      },
      "meta": {
        "latest_revision_number": 1
      }
    }
  ],
  "meta": {
    "total_hits": 1
  }
}
```

## Appendice

La sezione seguente contiene informazioni aggiuntive sull’utilizzo dell’endpoint `/search`.

### Logica dell’operatore del valore {#value-operator}

I valori delle query di ricerca sono suddivisi nei diversi termini che devono essere rilevati nei documenti indicizzati. Tra ciascun termine, si presume una relazione `AND`.

Quando utilizzi `AND` come `value_operator`, un valore di query `My Rule Holiday Sale` viene interpretato come documento con un campo contenente `My AND Rule AND Holiday AND Sale`.

Quando utilizzi `OR` come `value_operator`, un valore di query `My Rule Holiday Sale` viene interpretato come documento con un campo contenente `My OR Rule OR Holiday OR Sale`. Maggiore è il numero di termini corrispondenti rilevati, maggiore è il valore di `match_score`. A causa della natura della corrispondenza parziale dei termini, quando nulla corrisponde esattamente al valore desiderato, è possibile ottenere un set di risultati per una corrispondenza molto basilare, ad esempio considerando solo alcuni dei caratteri che compongono i termini cercati.

### Convenzioni per la corrispondenza nelle ricerche {#conventions}

Nella ricerca viene esaminata la rilevanza di un documento rispetto alla query fornita. Il modo in cui i dati del documento vengono analizzati e indicizzati influisce direttamente su questo aspetto.

La tabella seguente suddivide le convenzioni di corrispondenza per i tipi di campo più comuni:

| Tipo di campo | Convenzioni di corrispondenza |
| --- | --- |
| Stringhe | Testo con analisi parziale dei termini, senza distinzione tra maiuscole e minuscole |
| Valori enum | Corrispondenza esatta, distinzione tra maiuscole e minuscole |
| Interi | Corrispondenza esatta |
| Mobile | Corrispondenza esatta |
| Marca temporale | Corrispondenza esatta (formato DataOra) |
| Nomi visualizzati | Testo con analisi parziale dei termini, senza distinzione tra maiuscole e minuscole |

Nell’API sono disponibili convenzioni aggiuntive per campi specifici:

| Campo | Convenzioni di corrispondenza |
| --- | --- |
| `id` | Corrispondenza esatta, distinzione tra maiuscole e minuscole |
| `delegate_descriptor_id` | Corrispondenza esatta, con distinzione tra maiuscole e minuscole, con termini suddivisi da `::` |
| `name` | Corrispondenza esatta, distinzione tra maiuscole e minuscole |
| `settings` | Testo con analisi parziale dei termini, senza distinzione tra maiuscole e minuscole |
| `type` | Corrispondenza esatta, distinzione tra maiuscole e minuscole |
