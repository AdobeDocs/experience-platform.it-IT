---
keywords: classificazione del testo;Classificazione del testo
solution: Experience Platform, Intelligent Services
title: Classificazione del testo in Content and Commerce API
topic: Developer guide
description: Il servizio classificazione testo, se dotato di frammento di testo, può classificarlo in una o più etichette. La classificazione può essere di tipo etichetta singola, etichetta multipla o gerarchico.
translation-type: tm+mt
source-git-commit: d10c00694b0a3b2a9da693bd59615b533cfae468
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 4%

---


# Classificazione del testo

>[!NOTE]
>
>Content and Commerce AI è in versione beta. La documentazione è soggetta a modifiche.

Il servizio classificazione testo, se dotato di frammento di testo, può classificarlo in una o più etichette. La classificazione può essere di tipo etichetta singola, etichetta multipla o gerarchico.

**Formato API**

```http
POST /services/v1/predict
```

**Richiesta**

La seguente richiesta classifica il testo di un frammento in base ai parametri di input forniti nel payload. Per ulteriori informazioni sui parametri di input, vedere la tabella sotto il payload di esempio.

>[!CAUTION]
>
>`analyzer_id` determina quale  [!DNL Sensei Content Framework] viene utilizzato. Prima di effettuare la richiesta, verificare di disporre del `analyzer_id` corretto. Contatta il team beta di Content and Commerce AI per ricevere la `analyzer_id` per questo servizio.

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
| `analyzer_id` | L&#39;ID del servizio [!DNL Sensei] in cui viene distribuita la richiesta. Questo ID determina quale delle [!DNL Sensei Content Frameworks] vengono utilizzate. Per i servizi personalizzati, contattate il team di Content and Commerce AI per configurare un ID personalizzato. | Sì |
| `application-id` | ID dell’applicazione creata. | Sì |
| `data` | Un array che contiene un oggetto JSON con ogni oggetto nell&#39;array che rappresenta un documento. Tutti i parametri passati come parte di questa matrice sostituiscono i parametri globali specificati all&#39;esterno dell&#39;array `data`. Qualsiasi proprietà rimanente descritta in questa tabella può essere ignorata dall&#39;interno di `data`. | Sì |
| `language` | Lingua del testo di input. Il valore predefinito è `en`. | No |
| `content-type` | Utilizzato per indicare se l&#39;input fa parte del corpo della richiesta o un URL firmato per un bucket S3. Il valore predefinito di questa proprietà è `inline`. | No |
| `encoding` | Formato di codifica del testo di input. Può essere `utf-8` o `utf-16`. Il valore predefinito di questa proprietà è `utf-8`. | No |
| `threshold` | La soglia di punteggio (da 0 a 1) al di sopra della quale devono essere restituiti i risultati. Utilizzare il valore `0` per restituire tutti i risultati. Il valore predefinito di questa proprietà è `0`. | No |
| `top-N` | Il numero di risultati da restituire (non può essere un numero intero negativo). Utilizzare il valore `0` per restituire tutti i risultati. Se utilizzato insieme a `threshold`, il numero di risultati restituiti è minore di uno dei due set di limiti. Il valore predefinito di questa proprietà è `0`. | No |
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
