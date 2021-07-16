---
title: Endpoint di ricerca
description: Scopri come effettuare chiamate all’endpoint /search nell’API di Reactor.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 2%

---

# Endpoint di ricerca

L’endpoint `/search` nell’API di Reactor fornisce un modo per trovare le risorse che corrispondono ai criteri desiderati, espressi come query.

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

Tutte le query hanno ambito per la società corrente e le proprietà accessibili.

>[!IMPORTANT]
>
>La funzionalità di ricerca presenta le seguenti avvertenze ed eccezioni:
>* meta non è ricercabile e non viene restituito nei risultati della ricerca.
>* Campi dello schema per i delegati del pacchetto di estensione (azioni, condizioni, ecc.) sono ricercabili come testo, non come struttura dati nidificata.
>* Le query di intervallo al momento supportano solo i numeri interi.


Per ulteriori informazioni su come utilizzare questa funzionalità, consulta la [guida alla ricerca](../guides/search.md).

## Introduzione

L&#39;endpoint utilizzato in questa guida fa parte dell&#39; [API del reattore](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). Prima di continuare, controlla la [guida introduttiva](../getting-started.md) per informazioni importanti su come eseguire l&#39;autenticazione nell&#39;API.

## Recupera un elenco di regole {#list}

Puoi recuperare un elenco di regole appartenenti a una proprietà effettuando una richiesta di GET.

**Formato API**

```http
GET /properties/{PROPERTY_ID}/rules
```

| Parametro | Descrizione |
| --- | --- |
| `PROPERTY_ID` | La proprietà `id` di cui si desidera elencare i componenti. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Utilizzando i parametri di query, le regole elencate possono essere filtrate in base ai seguenti attributi:<ul><li>`created_at`</li><li>`dirty`</li><li>`enabled`</li><li>`name`</li><li>`origin_id`</li><li>`published`</li><li>`published_at`</li><li>`revision_number`</li><li>`updated_at`</li></ul>Per ulteriori informazioni, consulta la guida sulle [risposte relative al filtro](../guides/filtering.md) .

**Richiesta**

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data" : {
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
| `from` | Il numero di risultati per cui eseguire l&#39;offset della risposta. |
| `size` | La quantità massima di risultati da restituire. I risultati non possono superare i 100 elementi. |
| `query` | Oggetto che rappresenta la query di ricerca. Per ogni proprietà di questo oggetto, la chiave deve rappresentare un percorso di campo per la query e il valore deve essere un oggetto le cui sottoproprietà determinano per cosa eseguire la query.<br><br>Per ogni percorso di campo, puoi utilizzare le seguenti sottoproprietà:<ul><li>`exists`: Restituisce true se il campo esiste nella risorsa.</li><li>`value`: Restituisce true se il valore del campo corrisponde al valore di questa proprietà.</li><li>`value_operator`: Logica booleana utilizzata per determinare come deve essere gestita una  `value` query. I valori consentiti sono `AND` e `OR`. Se viene escluso, viene utilizzata la logica `AND`. Per ulteriori informazioni, consulta la sezione relativa alla logica dell’operatore di valore [e](#value-operator)</li><li>`range` Restituisce true se il valore del campo rientra in un intervallo numerico specifico. L’intervallo stesso è determinato dalle seguenti sottoproprietà:<ul><li>`gt`: Maggiore del valore specificato, non incluso.</li><li>`gte`: Maggiore o uguale al valore specificato.</li><li>`lt`: Minore del valore specificato, non incluso.</li><li>`lte`: Minore o uguale al valore specificato.</li></ul></li></ul> |
| `sort` | Matrice di oggetti che indica l’ordine in cui ordinare i risultati. Ogni oggetto deve contenere una singola proprietà: la chiave rappresenta il percorso del campo in base al quale eseguire l’ordinamento e il valore rappresenta l’ordinamento (`asc` per crescente, `desc` per decrescente). |
| `resource_types` | Matrice di stringhe che indica i tipi di risorse specifici da cercare. |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce un elenco di risorse corrispondenti per la query. Per informazioni dettagliate sulle modalità in cui l&#39;API determina le corrispondenze per valori specifici, consulta la sezione dell&#39;appendice sulle [convenzioni di corrispondenza](#conventions).

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

La sezione seguente contiene informazioni aggiuntive sull’utilizzo dell’endpoint `/search` .

### Logica operatore valore {#value-operator}

I valori delle query di ricerca sono suddivisi in termini da confrontare con i documenti indicizzati. Tra ciascun termine, si presume una relazione `AND`.

Quando utilizzi `AND` come `value_operator`, un valore di query di `My Rule Holiday Sale` viene interpretato come documento con un campo contenente `My AND Rule AND Holiday AND Sale`.

Quando utilizzi `OR` come `value_operator`, un valore di query di `My Rule Holiday Sale` viene interpretato come documento con un campo contenente `My OR Rule OR Holiday OR Sale`. Maggiore è il numero di termini corrispondenti, maggiore è il valore di `match_score`. A causa della natura della corrispondenza parziale dei termini, quando nulla corrisponde esattamente al valore desiderato, è possibile ottenere un set di risultati in cui il valore corrisponde solo a un livello di base, ad esempio alcuni caratteri di testo.

### Convenzioni corrispondenti {#conventions}

La ricerca si occupa di rispondere alla rilevanza di un documento per una query fornita. Il modo in cui i dati del documento vengono analizzati e indicizzati influisce direttamente su questo aspetto.

La tabella seguente suddivide le convenzioni di corrispondenza per i tipi di campo comuni:

| Tipo di campo | Convenzioni di corrispondenza |
| --- | --- |
| Stringhe | Testo con analisi parziale dei termini, senza distinzione tra maiuscole e minuscole |
| Valori enum | Corrispondenza esatta, distinzione tra maiuscole e minuscole |
| Interi | Corrispondenza esatta |
| Mobile | Corrispondenza esatta |
| Marca temporale | Corrispondenza esatta (formato DateTime) |
| Nomi visualizzati | Testo con analisi parziale dei termini, senza distinzione tra maiuscole e minuscole |

Nell’API sono disponibili convenzioni aggiuntive per campi specifici:

| Campo | Convenzioni di corrispondenza |
| --- | --- |
| `id` | Corrispondenza esatta, distinzione tra maiuscole e minuscole |
| `delegate_descriptor_id` | Corrispondenza esatta, con distinzione tra maiuscole e minuscole, con termini suddivisi in `::` |
| `name` | Corrispondenza esatta, distinzione tra maiuscole e minuscole |
| `settings` | Testo con analisi parziale dei termini, senza distinzione tra maiuscole e minuscole |
| `type` | Corrispondenza esatta, distinzione tra maiuscole e minuscole |