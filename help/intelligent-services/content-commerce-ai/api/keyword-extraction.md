---
keywords: Experience Platform;getting started;content ai;commerce ai;content and commerce ai;keyword extraction;Keyword extraction
solution: Experience Platform
title: Estrazione colore
topic: Developer guide
description: Quando viene fornito un documento di testo, il servizio di estrazione delle parole chiave estrae automaticamente le parole chiave o le frasi chiave che meglio descrivono l’oggetto del documento. Per estrarre le parole chiave, viene utilizzata una combinazione di algoritmi di riconoscimento delle entità con nome (NER) e di estrazione delle parole chiave senza supervisione.
translation-type: tm+mt
source-git-commit: e69f4e8ddc0fe5f7be2b2b2bd89c09efdfca8e75
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 3%

---


# Estrazione di parole chiave

>[!NOTE]
>
>[!DNL Content and Commerce AI] è in versione beta. La documentazione è soggetta a modifiche.

Quando viene fornito un documento di testo, il servizio di estrazione delle parole chiave estrae automaticamente le parole chiave o le frasi chiave che meglio descrivono l’oggetto del documento. Per estrarre le parole chiave, viene utilizzata una combinazione di algoritmi di riconoscimento delle entità con nome (NER) e di estrazione delle parole chiave senza supervisione.

**Estrazione di parole chiave non supervisionata**

Per l&#39;estrazione di parole chiave non supervisionate, viene utilizzato [[!DNL YAKE]](http://yake.inesctec.pt/) . [!DNL YAKE] è un metodo di estrazione automatico delle parole chiave rapido e accurato, utilizzato per selezionare le parole chiave più importanti da un documento. Gli [!DNL YAKE] estratti delle parole chiave vengono quindi filtrati per selezionare solo frasi noun.

**Riconoscimento entità denominato**

Per il riconoscimento di entità con nome, viene utilizzato il modello OntoNotes di [[!DNL spaCy]](https://spacy.io/). Questo modello assegna vettori token specifici per il contesto, tag di parte del discorso (POS), analisi delle dipendenze ed entità denominate. Il modello OntoNotes è uno dei [!DNL spaCy] modelli di base. Ulteriori informazioni sul modello OntoNotes sono disponibili [qui](https://spacy.io/models/en).

Le entità denominate riconosciute da [!DNL Content and Commerce AI] sono elencate nella tabella seguente:

| Nome entità | Descrizione |
| --- | --- |
| PERSONA | Persone, comprese quelle fittizie. |
| NORP | Nazionalità o gruppi religiosi o politici. |
| GPE | Paesi, città e stati. |
| LOC | Località non GPE, catene montuose, corpi idrici. |
| FAC | Edifici, aeroporti, autostrade, ponti, ecc. |
| ORG | Società, agenzie, istituzioni, ecc. |
| PRODOTTO | Oggetti, veicoli, alimenti, ecc. (Non servizi.) |
| EVENTO | Uragani denominati, battaglie, guerre, eventi sportivi, ecc. |
| WORK_OF_ART | Titoli di libri, canzoni, ecc. |
| LEGGE | Documenti denominati creati in leggi. |
| LINGUA | Qualsiasi lingua con nome. |

I risultati di [!DNL OntoNotes] vengono combinati con le parole chiave di [!DNL YAKE], e vengono quindi restituiti in ordine classifica in base alla loro importanza.

**Formato API**

```http
POST /services/v1/predict
```

**Richiesta**

La richiesta seguente estrae le parole chiave da un documento in base ai parametri di input forniti nel payload.

JSON semplificato del file di input:

```json
{
  "application-id": "1234",
  "language": "en",
  "content-type": "inline",
  "encoding": "utf-8",
  "threshold": 0.01,
  "top-N": 10,
  "custom": {
    "min-n": 2,
    "entity-types": ["PERSON"]
  },
  "data": [
    {
      "content-id": "abc123",
      "content": "But an influential faction on the ATP player council, which is chaired by Novak Djokovic, staged a rebellion against Kermodes regime in the spring, and he will leave the post on Dec 31"
    }
  ]
}
```

Per ulteriori informazioni sui parametri di input, vedere la tabella sotto il payload di esempio.

>[!CAUTION]
>
>`analyzer_id` determina quale [!DNL Sensei Content Framework] viene utilizzato. Prima di effettuare la richiesta, verificare di disporre dei dati necessari `analyzer_id` .

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: multipart/form-data" \
  -H "cache-control: no-cache,no-cache" \
  -H "x-api-key: {API_KEY}" \
  -F file="{
    \"application-id\": \"1234\", 
    \"language\": \"en\", 
    \"content-type\": \"inline\", 
    \"encoding\": \"utf-8\",
    \"threshold\": 0.01,
    \"top-N\": 10,
    \"custom\": {
        \"min-n\": 2,
        \"entity-types\": [\"PERSON\"]
      },
    \"data\": [{
      \"content-id\": \"abc123\", 
      \"content\": \"But an influential faction on the ATP player council, which is chaired by Novak Djokovic, staged a rebellion against Kermodes regime in the spring, and he will leave the post on Dec 31\"
      }]
    }" \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
         "analyzer_id": "Feature:cintel-ner:Service-1a35aefb0f0f4dc0a3b5262370ebc709",
         "parameters": {}
    }]
}'
```

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| `analyzer_id` | L’ID [!DNL Sensei] del servizio in cui viene distribuita la richiesta. Questo ID determina quale dei due [!DNL Sensei Content Frameworks] vengono utilizzati. | Sì |
| `application-id` | ID dell&#39;applicazione creata. | Sì |
| `data` | Un array che contiene un oggetto JSON con ogni oggetto nell&#39;array che rappresenta un documento. Eventuali parametri passati come parte di questa matrice sovrascrivono i parametri globali specificati al di fuori della `data` matrice. Qualsiasi proprietà rimanente descritta in questa tabella può essere ignorata dall&#39;interno `data`. | Sì |
| `language` | Lingua del testo di input. Il valore predefinito è `en`. | No |
| `content-type` | Utilizzato per indicare se l&#39;input fa parte del corpo della richiesta o un URL firmato per un bucket S3. L&#39;impostazione predefinita di questa proprietà è `inline`. | Sì |
| `encoding` | Formato di codifica del testo di input. Questo può essere `utf-8` o `utf-16`. L&#39;impostazione predefinita di questa proprietà è `utf-8`. | No |
| `threshold` | La soglia di punteggio (da 0 a 1) al di sopra della quale devono essere restituiti i risultati. Utilizzate il valore `0` per restituire tutti i risultati. L&#39;impostazione predefinita di questa proprietà è `0`. | No |
| `top-N` | Il numero di risultati da restituire (non può essere un numero intero negativo). Utilizzate il valore `0` per restituire tutti i risultati. Se utilizzato insieme a `threshold`, il numero di risultati restituiti è minore di uno dei due set di limiti. L&#39;impostazione predefinita di questa proprietà è `0`. | No |
| `custom` | Eventuali parametri personalizzati da passare. Questa proprietà richiede un oggetto JSON valido per funzionare. Per ulteriori informazioni sui parametri personalizzati, consultate l&#39; [appendice](#appendix) . | No |
| `content-id` | L&#39;ID univoco per l&#39;elemento dati restituito nella risposta. Se non viene passato, viene assegnato un ID generato automaticamente. | No |
| `content` | Contenuto utilizzato dal servizio di estrazione delle parole chiave. Il contenuto può essere in formato non elaborato (tipo di contenuto &quot;inline&quot;). <br> Se il contenuto è un file su S3 (tipo di contenuto s3-bucket), passare l&#39;URL firmato. Quando il contenuto fa parte del corpo della richiesta, l&#39;elenco degli elementi dati deve avere un solo oggetto. Se vengono passati più oggetti, viene elaborato solo il primo oggetto. | Sì |

**Risposta**

Una risposta corretta restituisce un oggetto JSON contenente le parole chiave estratte nell&#39; `response` array.

```json
{
  "status": 200,
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:cintel-ner:Service-1a35aefb0f0f4dc0a3b5262370ebc709",
      "content_id": "",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_value": "success",
                "feature_name": "status"
              },
              {
                "feature_name": "labels",
                "feature_value": [
                  {
                    "feature_name": "atp player",
                    "feature_value": [
                      {
                        "feature_value": "KEYWORD",
                        "feature_name": "type"
                      },
                      {
                        "feature_value": 0.007743432063478832,
                        "feature_name": "score"
                      }
                    ]
                  },
                  {
                    "feature_name": "Novak Djokovic",
                    "feature_value": [
                      {
                        "feature_name": "type",
                        "feature_value": "PERSON"
                      },
                      {
                        "feature_name": "score",
                        "feature_value": 0
                      }
                    ]
                  },
                  {
                    "feature_value": [
                      {
                        "feature_name": "type",
                        "feature_value": "KEYWORD"
                      },
                      {
                        "feature_value": 0.00899321792126428,
                        "feature_name": "score"
                      }
                    ],
                    "feature_name": "player council"
                  },
                  {
                    "feature_value": [
                      {
                        "feature_value": "KEYWORD",
                        "feature_name": "type"
                      },
                      {
                        "feature_value": 0.007743432063478832,
                        "feature_name": "score"
                      }
                    ],
                    "feature_name": "kermodes regime"
                  },
                  {
                    "feature_value": [
                      {
                        "feature_name": "type",
                        "feature_value": "KEYWORD"
                      },
                      {
                        "feature_name": "score",
                        "feature_value": 0.0006052376660884209
                      }
                    ],
                    "feature_name": "atp player council"
                  }
                ]
              }
            ],
            "feature_name": "abc123"
          }
        ]
      }
    }
  ],
  "error": []
}
```

## Appendice {#appendix}

La tabella seguente contiene i parametri disponibili che è possibile utilizzare dall&#39;interno `custom`.

| Nome | Descrizione | Obbligatorio |
| --- | --- | --- |
| `min-n` | Il numero minimo di parole necessarie nelle parole chiave. | No |
| `entity-types` | Tipi di entità da restituire. Vedere la tabella di riconoscimento delle entità con nome all&#39;inizio del documento. | No |