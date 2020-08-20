---
keywords: text classification;Text classification
solution: Experience Platform
title: Endpoint API classificazione testo
topic: Developer guide
description: Il servizio classificazione testo, se dotato di frammento di testo, può classificarlo in una o più etichette. La classificazione può essere di tipo etichetta singola, etichetta multipla o gerarchico.
translation-type: tm+mt
source-git-commit: e69f4e8ddc0fe5f7be2b2b2bd89c09efdfca8e75
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 4%

---


# Classificazione del testo

>[!NOTE]
>
>Content and Commerce AI è in versione beta. La documentazione è soggetta a modifiche.

Il servizio classificazione testo, se dotato di frammento di testo, può classificarlo in una o più etichette. La classificazione può essere di tipo etichetta singola, etichetta multipla o gerarchico.

La classificazione del testo utilizza un modello basato su [FastText](https://fasttext.cc/) che è stato addestrato utilizzando dati personalizzati.

**Formato API**

```http
POST /services/v1/predict
```

**Richiesta**

La seguente richiesta classifica il testo di un frammento in base ai parametri di input forniti nel payload. Per ulteriori informazioni sui parametri di input, vedere la tabella sotto il payload di esempio.

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
    \"data\": [{
      \"content-id\": \"abc123\", 
      \"content\": \"Server and Workstation Processors, Microcode Update is a self-extracting executable file containing the latest beta microcode updates (System Configuration Data) and software license agreement.\"
      }]
    }" \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
         "analyzer_id": "Feature:cintel-text-classifier:Service-38a4cc7b286449e6bc1977f59df01b47",
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
| `content-type` | Utilizzato per indicare se l&#39;input fa parte del corpo della richiesta o un URL firmato per un bucket S3. L&#39;impostazione predefinita di questa proprietà è `inline`. | No |
| `encoding` | Formato di codifica del testo di input. Questo può essere `utf-8` o `utf-16`. L&#39;impostazione predefinita di questa proprietà è `utf-8`. | No |
| `threshold` | La soglia di punteggio (da 0 a 1) al di sopra della quale devono essere restituiti i risultati. Utilizzate il valore `0` per restituire tutti i risultati. L&#39;impostazione predefinita di questa proprietà è `0`. | No |
| `top-N` | Il numero di risultati da restituire (non può essere un numero intero negativo). Utilizzate il valore `0` per restituire tutti i risultati. Se utilizzato insieme a `threshold`, il numero di risultati restituiti è minore di uno dei due set di limiti. L&#39;impostazione predefinita di questa proprietà è `0`. | No |
| `custom` | Eventuali parametri personalizzati da passare. Questa proprietà richiede un oggetto JSON valido per funzionare. | No |
| `content-id` | L&#39;ID univoco per l&#39;elemento dati restituito nella risposta. Se non viene passato, viene assegnato un ID generato automaticamente. | No |
| `content` | Il contenuto utilizzato dal servizio di classificazione del testo. Il contenuto può essere in formato non elaborato (tipo di contenuto &quot;inline&quot;). <br> Se il contenuto è un file su S3 (tipo di contenuto s3-bucket), passare l&#39;URL firmato. | Sì |

**Risposta**

Una risposta corretta restituisce il testo classificato in un array di risposte.

```json
{
  "status": 200,
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:cintel-text-classifier:Service-38a4cc7b286449e6bc1977f59df01b47",
      "content_id": "",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_name": "abc123",
            "feature_value": [
              {
                "feature_value": [
                  {
                    "feature_value": 0.6899315714836121,
                    "feature_name": "Embedded & IoT"
                  }
                ],
                "feature_name": "labels"
              },
              {
                "feature_name": "status",
                "feature_value": "success"
              }
            ]
          }
        ]
      }
    }
  ],
  "error": []
}
```
