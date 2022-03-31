---
keywords: Experience Platform;guida introduttiva;ai contenuti;ai e-commerce;contenuto e ai-commerce;estrazione di parole chiave;estrazione di parole chiave
solution: Experience Platform
title: Estrazione di parole chiave nell’API Content and Commerce AI
topic-legacy: Developer guide
description: Il servizio di estrazione delle parole chiave, quando viene fornito un documento di testo, estrae automaticamente parole chiave o frasi chiave che descrivono al meglio l’oggetto del documento. Per estrarre le parole chiave, viene utilizzata una combinazione di algoritmi di riconoscimento delle entità con nome (NER) e di estrazione delle parole chiave senza supervisione.
exl-id: 56a2da96-5056-4702-9110-a1dfec56f0dc
source-git-commit: eae43834d1cd5931dd752b95023da7ac77668e56
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 4%

---

# Estrazione di parole chiave

>[!NOTE]
>
>[!DNL Content and Commerce AI] è in versione beta. La documentazione è soggetta a modifiche.

Il servizio di estrazione delle parole chiave, quando viene fornito un documento di testo, estrae automaticamente parole chiave o frasi chiave che descrivono al meglio l’oggetto del documento. Per estrarre le parole chiave, viene utilizzata una combinazione di algoritmi di riconoscimento delle entità con nome (NER) e di estrazione delle parole chiave senza supervisione.

Le entità denominate riconosciute da [!DNL Content and Commerce AI] sono elencati nella tabella seguente:

| Nome entità | Descrizione |
| --- | --- |
| PERSONA | Persone, incluse le finzioni. |
| NORP | Nazionalità o gruppi religiosi o politici. |
| GPE | Paesi, città e stati. |
| LOC | Posizioni non GPE, catene montuose, corpi idrici. |
| FAC | Edifici, aeroporti, autostrade, ponti, ecc. |
| ORO | Aziende, agenzie, istituzioni, ecc. |
| PRODOTTO | Oggetti, veicoli, alimenti, ecc. (Non servizi.) |
| EVENTO | Uragani, battaglie, guerre, eventi sportivi, ecc. |
| WORK_OF_ART | Titoli di libri, canzoni, ecc. |
| LEGGE | Documenti denominati creati in leggi. |
| LINGUA | Qualsiasi linguaggio denominato. |

>[!NOTE]
>
>Se prevedi di elaborare i PDF, passa alle istruzioni per [Estrazione di parole chiave PDF](#pdf-extraction) in questo documento. Inoltre, il supporto per tipi di file aggiuntivi come docx, ppt, amd xml è impostato per essere rilasciato in una data successiva.

**Formato API**

```http
POST /services/v1/predict
```

**Richiesta**

La richiesta seguente estrae parole chiave da un documento in base ai parametri di input forniti nel payload.

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

Per ulteriori informazioni sui parametri di input mostrati, consulta la tabella riportata di seguito.

>[!CAUTION]
>
>`analyzer_id` determina quale [!DNL Sensei Content Framework] viene utilizzato. Verifica di avere il `analyzer_id` prima di fare la tua richiesta. Per il servizio di estrazione delle parole chiave, la `analyzer_id` ID:
>`Feature:cintel-ner:Service-1a35aefb0f0f4dc0a3b5262370ebc709`

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
| `analyzer_id` | La [!DNL Sensei] ID del servizio in cui viene distribuita la richiesta. Questo ID determina quale tra [!DNL Sensei Content Frameworks] sono utilizzati. Per i servizi personalizzati, contatta il team Content and Commerce AI per configurare un ID personalizzato. | Sì |
| `application-id` | ID dell&#39;applicazione creata. | Sì |
| `data` | Matrice che contiene un oggetto JSON con ogni oggetto della matrice che rappresenta un documento. Eventuali parametri passati come parte di questa matrice sostituiscono i parametri globali specificati al di fuori della `data` array. È possibile ignorare tutte le proprietà rimanenti descritte in questa tabella all’interno di `data`. | Sì |
| `language` | Lingua del testo di input. Il valore predefinito è `en`. | No |
| `content-type` | Utilizzato per indicare se l’input fa parte del corpo della richiesta o di un url firmato per un bucket S3. Il valore predefinito di questa proprietà è `inline`. | Sì |
| `encoding` | Formato di codifica del testo di input. Questo può essere `utf-8` o `utf-16`. Il valore predefinito di questa proprietà è `utf-8`. | No |
| `threshold` | La soglia del punteggio (da 0 a 1) al di sopra della quale devono essere restituiti i risultati. Utilizza il valore `0` per restituire tutti i risultati. Il valore predefinito di questa proprietà è `0`. | No |
| `top-N` | Il numero di risultati da restituire (non può essere un numero intero negativo). Utilizza il valore `0` per restituire tutti i risultati. Se utilizzato in combinazione con `threshold`, il numero di risultati restituiti è il minore tra i due set di limiti. Il valore predefinito di questa proprietà è `0`. | No |
| `custom` | Eventuali parametri personalizzati da trasmettere. Questa proprietà richiede un oggetto JSON valido per funzionare. Consulta la sezione [appendice](#appendix) per ulteriori informazioni sui parametri personalizzati. | No |
| `content-id` | L&#39;ID univoco dell&#39;elemento dati restituito nella risposta. Se non viene passato, viene assegnato un ID generato automaticamente. | No |
| `content` | Il contenuto utilizzato dal servizio di estrazione delle parole chiave. Il contenuto può essere di tipo non elaborato (&quot;inline&quot;). <br> Se il contenuto è un file sul tipo di contenuto S3 (&#39;s3-bucket&#39;), passa l’url firmato. Quando il contenuto fa parte del corpo della richiesta, l’elenco degli elementi dati deve avere un solo oggetto. Se vengono passati più oggetti, viene elaborato solo il primo oggetto. | Sì |

**Risposta**

Una risposta corretta restituisce un oggetto JSON contenente le parole chiave estratte nel `response` array.

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

## Estrazione di parole chiave PDF {#pdf-extraction}

Il servizio di estrazione delle parole chiave supporta i PDF, tuttavia, è necessario utilizzare un nuovo AnalyzerID per i file PDF e modificare il tipo di documento in PDF. Per ulteriori informazioni, consulta l’esempio seguente.

**Formato API**

```http
POST /services/v1/predict
```

**Richiesta**

La richiesta seguente estrae parole chiave da un documento PDF in base ai parametri di input forniti nel payload.

>[!CAUTION]
>
>`analyzer_id` determina quale [!DNL Sensei Content Framework] viene utilizzato. Verifica di avere il `analyzer_id` prima di fare la tua richiesta. Per l’estrazione di parole chiave di PDF, l’ `analyzer_id` ID:
>`Feature:cintel-ner:Service-7a87cb57461345c280b62470920bcdc5`

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: multipart/form-data" \
  -H "cache-control: no-cache,no-cache" \
  -H "x-api-key: {API_KEY}" \
  -F file=@TestPDF.pdf \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
    "analyzer_id": "Feature:cintel-ner:Service-7a87cb57461345c280b62470920bcdc5",
    "parameters": {
      "application-id": "1234",
      "content-type": "file",
      "encoding": "pdf",
      "threshold": "0.01",
      "top-N": "0",
      "custom": {},
      "data": [{
        "content-id": "abc123",
        "content": "file",
        }]
      }
    }]
  }'
```

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| `analyzer_id` | La [!DNL Sensei] ID del servizio in cui viene distribuita la richiesta. Questo ID determina quale tra [!DNL Sensei Content Frameworks] sono utilizzati. Per i servizi personalizzati, contatta il team Content and Commerce AI per configurare un ID personalizzato. | Sì |
| `application-id` | ID dell&#39;applicazione creata. | Sì |
| `data` | Matrice che contiene un oggetto JSON con ogni oggetto della matrice che rappresenta un documento. Eventuali parametri passati come parte di questa matrice sostituiscono i parametri globali specificati al di fuori della `data` array. È possibile ignorare tutte le proprietà rimanenti descritte in questa tabella all’interno di `data`. | Sì |
| `language` | Lingua di input. Il valore predefinito è `en` (inglese). | No |
| `content-type` | Utilizzato per indicare il tipo di contenuto in input. Questo valore deve essere impostato su `file`. | Sì |
| `encoding` | Formato di codifica dell’input. Questo valore deve essere impostato su `pdf`. In un secondo momento saranno supportati altri tipi di codifica. | Sì |
| `threshold` | La soglia del punteggio (da 0 a 1) al di sopra della quale devono essere restituiti i risultati. Utilizza il valore `0` per restituire tutti i risultati. Il valore predefinito di questa proprietà è `0`. | No |
| `top-N` | Il numero di risultati da restituire (non può essere un numero intero negativo). Utilizza il valore `0` per restituire tutti i risultati. Se utilizzato in combinazione con `threshold`, il numero di risultati restituiti è il minore tra i due set di limiti. Il valore predefinito di questa proprietà è `0`. | No |
| `custom` | Eventuali parametri personalizzati da trasmettere. Questa proprietà richiede un oggetto JSON valido per funzionare. Consulta la sezione [appendice](#appendix) per ulteriori informazioni sui parametri personalizzati. | No |
| `content-id` | L&#39;ID univoco dell&#39;elemento dati restituito nella risposta. Se non viene passato, viene assegnato un ID generato automaticamente. | No |
| `content` | Questo valore deve essere impostato su `file`. | Sì |

**Risposta**

Una risposta corretta restituisce un oggetto JSON contenente le parole chiave estratte nel `response` array.

```json
{
  "statusCode": 200,
  "body": {
    "type": "JSON",
    "matchType": "strict",
    "json": {
      "status": 200,
      "content_id": "161hw2.pdf",
      "cas_responses": [
        {
          "status": 200,
          "analyzer_id": "Feature:cintel-ner:Service-7a87cb57461345c280b62470920bcdc5",
          "content_id": "161hw2.pdf",
          "result": {
            "response_type": "feature",
            "response": [
              {
                "feature_value": [
                  {
                    "feature_name": "status",
                    "feature_value": "success"
                  },
                  {
                    "feature_value": [
                      {
                        "feature_name": "delbick",
                        "feature_value": [
                          {
                            "feature_name": "score",
                            "feature_value": 0.03673855028832046
                          },
                          {
                            "feature_name": "type",
                            "feature_value": "KEYWORD"
                          }
                        ]
                      },
                      {
                        "feature_name": "Ci",
                        "feature_value": [
                          {
                            "feature_name": "score",
                            "feature_value": 0
                          },
                          {
                            "feature_name": "type",
                            "feature_value": "PERSON"
                          }
                        ]
                      }
                    ],
                    "feature_name": "labels"
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
  }
}
```

Per ulteriori informazioni e un esempio sull’utilizzo dell’estrazione di PDF contenente istruzioni su come impostare, implementare e integrare con il servizio cloud AEM. Visita il [Archivio github del processo di lavoro di estrazione di CCAI PDF](https://github.com/adobe/asset-compute-example-workers/tree/master/projects/worker-ccai-pdfextract).

## Appendice {#appendix}

La tabella seguente contiene i parametri disponibili che possono essere utilizzati da `custom`.

| Nome | Descrizione | Obbligatorio |
| --- | --- | --- |
| `min-n` | Numero minimo di parole necessarie nelle parole chiave. | No |
| `entity-types` | Tipi di entità da restituire. Vedere la tabella di riconoscimento entità denominata all&#39;inizio del documento. | No |
