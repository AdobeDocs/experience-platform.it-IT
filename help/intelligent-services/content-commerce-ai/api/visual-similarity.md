---
keywords: Visual similarity;visual similarity;ccai api
solution: Experience Platform
title: Similarità visiva
topic: Developer guide
description: Il servizio per similarità visiva, quando viene fornita un’immagine, trova automaticamente immagini visivamente simili da un catalogo.
translation-type: tm+mt
source-git-commit: 4f7b5ca50171f4948726c44dbf31025011adf35f
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 3%

---


# Similarità visiva

>[!NOTE]
>
>[!DNL Content and Commerce AI] è in versione beta. La documentazione è soggetta a modifiche.

Il servizio per similarità visiva, quando viene fornita un’immagine, trova automaticamente immagini visivamente simili da un catalogo.

L&#39;immagine seguente è stata utilizzata nella richiesta di esempio mostrata in questo documento:

![immagine di prova](../images/Query_Image.jpeg)

**Formato API**

```http
POST /services/v1/predict
```

**Richiesta**

La richiesta seguente recupera immagini visivamente simili da un catalogo, in base ai parametri di input forniti nel payload. Per ulteriori informazioni sui parametri di input, vedere la tabella sotto il payload di esempio.

>[!CAUTION]
>
>`analyzer_id` determina quale [!DNL Sensei Content Framework] viene utilizzato. Prima di effettuare la richiesta, verificare di disporre dei dati necessari `analyzer_id` . Contatta il team beta di Content and Commerce AI per ricevere il tuo `analyzer_id` servizio.

```SHELL
curl -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H 'Authorization: Bearer $API_TOKEN' \
  -H 'Content-Type: multipart/form-data' \
  -H 'cache-control: no-cache,no-cache' \
  -H 'x-api-key: $API_KEY' \
  -F file=@test_image.jpg \
  -F 'contentAnalyzerRequests={
   "enable_diagnostics":"true",
   "requests":[
     {
         "analyzer_id": "Feature:cintel-deep-product-search:Service-316a8cf750c6440396061c8f73a7a585",
         "parameters": {
          "application-id": "1234", 
          "content-type": "inline", 
          "encoding": "jpeg", 
          "threshold": "0", 
          "top-N": "0", 
          "custom": {}, 
          "data": [{
            "content-id": "0987", 
            "content": "inline-image", 
            "content-type": "inline", 
            "encoding": "jpeg", 
            "threshold": "0", 
            "top-N": "0", 
            "historic-metadata": [], 
            "custom": {}
            }]
          }
      }
    ]
}'
```

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| `analyzer_id` | L’ID [!DNL Sensei] del servizio in cui viene distribuita la richiesta. Questo ID determina quale dei due [!DNL Sensei Content Frameworks] vengono utilizzati. Per i servizi personalizzati, contattate il team di Content and Commerce AI per configurare un ID personalizzato. | Sì |
| `application-id` | ID dell’applicazione creata. | Sì |
| `data` | Un array che contiene un oggetto JSON con ogni oggetto nell&#39;array che rappresenta un&#39;immagine. Eventuali parametri passati come parte di questa matrice sovrascrivono i parametri globali specificati al di fuori della `data` matrice. Qualsiasi proprietà rimanente descritta in questa tabella può essere ignorata dall&#39;interno `data`. | Sì |
| `content-id` | L&#39;ID univoco per l&#39;elemento dati restituito nella risposta. Se non viene passato, viene assegnato un ID generato automaticamente. | No |
| `content` | Contenuto da analizzare dal servizio di somiglianza visiva. Se l’immagine fa parte del corpo della richiesta, usate `-F file=@<filename>` il comando curl per trasmettere l’immagine, lasciando questo parametro come una stringa vuota. <br> Se l&#39;immagine è un file su S3, passare l&#39;URL firmato. Quando il contenuto fa parte del corpo della richiesta, l&#39;elenco degli elementi dati deve avere un solo oggetto. Se vengono passati più oggetti, viene elaborato solo il primo oggetto. | Sì |
| `content-type` | Utilizzato per indicare se l&#39;input fa parte del corpo della richiesta o un URL firmato per un bucket S3. L&#39;impostazione predefinita di questa proprietà è `inline`. | No |
| `encoding` | Il formato file dell&#39;immagine di input. Attualmente è possibile elaborare solo immagini JPEG e PNG. L&#39;impostazione predefinita di questa proprietà è `jpeg`. | No |
| `threshold` | La soglia di punteggio (da 0 a 1) al di sopra della quale devono essere restituiti i risultati. Utilizzate il valore `0` per restituire tutti i risultati. L&#39;impostazione predefinita di questa proprietà è `0`. | No |
| `top-N` | Il numero di risultati da restituire (non può essere un numero intero negativo). Utilizzate il valore `0` per restituire tutti i risultati. Se utilizzato insieme a `threshold`, il numero di risultati restituiti è minore di uno dei due set di limiti. L&#39;impostazione predefinita di questa proprietà è `0`. | No |
| `custom` | Eventuali parametri personalizzati da passare. | No |
| `historic-metadata` | Un array che può essere trasmesso dai metadati. | No |

**Risposta**

Una risposta corretta restituisce un `response` array che contiene un e `feature_value` `feature_name` per ciascuna delle immagini visivamente simili presenti nel catalogo.

Nella risposta di esempio mostrata di seguito sono state restituite le seguenti immagini visivamente simili:

![immagini simili](../images/results.jpg)

```json
{
  "status": 200,
  "content_id": "test_image.jpg",
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:cintel-deep-product-search:Service-316a8cf750c6440396061c8f73a7a585",
      "content_id": "test_image.jpg",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_value": "678",
                "feature_name": "G34WS945.F1"
              },
              {
                "feature_value": "678",
                "feature_name": "1431RDM JANELLE RAW JACKE"
              },
              {
                "feature_value": "657",
                "feature_name": "GF4045877841 CARLA FLR"
              },
              {
                "feature_name": "1707-686-SGU PATCH XYZ",
                "feature_value": "657"
              },
              {
                "feature_name": "5495MJT AJA BLK",
                "feature_value": "646"
              },
              {
                "feature_name": "IDEAL",
                "feature_value": "645"
              },
              {
                "feature_value": "644",
                "feature_name": "HCAJRA439 CALI JEAN"
              },
              {
                "feature_name": "KT279RK-ONL",
                "feature_value": "644"
              },
              {
                "feature_name": "SP190404-ELLIS",
                "feature_value": "642"
              },
              {
                "feature_name": "GF4174848718 KENDALL DIS",
                "feature_value": "640"
              }
            ],
            "feature_name": "visual_similarity"
          }
        ]
      }
    }
  ],
  "error": []
}
```

