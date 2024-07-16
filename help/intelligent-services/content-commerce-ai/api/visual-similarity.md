---
keywords: Somiglianza visiva;somiglianza visiva;API ccai
solution: Experience Platform
title: Somiglianza visiva nell’API di IA per l’analisi dei contenuti e dei Commerce
description: Il servizio di somiglianza visiva, quando si fornisce un’immagine, trova automaticamente immagini visivamente simili da un catalogo.
exl-id: fe31d9be-ee42-44fa-b83f-3b8a718cb4e3
source-git-commit: b124ed97da8bde2a7fc4f10d350c81a47e096f29
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 3%

---

# Somiglianza visiva

>[!NOTE]
>
>[!DNL Content and Commerce AI] è in versione beta. La documentazione è soggetta a modifiche.

Il servizio di somiglianza visiva, quando si fornisce un’immagine, trova automaticamente immagini visivamente simili da un catalogo.

L’immagine seguente è stata utilizzata nella richiesta di esempio mostrata in questo documento:

![immagine di prova](../images/Query_Image.jpeg)

**Formato API**

```http
POST /services/v1/predict
```

**Richiesta**

La richiesta seguente recupera immagini visivamente simili da un catalogo, in base ai parametri di input forniti nel payload. Per ulteriori informazioni sui parametri di input mostrati, consulta la tabella seguente il payload di esempio.

>[!CAUTION]
>
>`analyzer_id` determina quale [!DNL Sensei Content Framework] viene utilizzato. Prima di effettuare la richiesta, verifica di disporre di `analyzer_id` corretti. Contatta il team beta di IA per l&#39;analisi dei contenuti e di Commerce per ricevere `analyzer_id` per questo servizio.

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
| `analyzer_id` | L&#39;ID del servizio [!DNL Sensei] in cui è distribuita la richiesta. Questo ID determina quale dei [!DNL Sensei Content Frameworks] viene utilizzato. Per i servizi personalizzati, contatta il team di IA per la gestione dei contenuti e di Commerce per impostare un ID personalizzato. | Sì |
| `application-id` | ID dell’applicazione creata. | Sì |
| `data` | Matrice che contiene un oggetto JSON con ogni oggetto nell’array che rappresenta un’immagine. Qualsiasi parametro passato come parte di questo array sostituisce i parametri globali specificati all&#39;esterno dell&#39;array `data`. Una qualsiasi delle proprietà rimanenti descritte di seguito in questa tabella può essere ignorata dall&#39;interno di `data`. | Sì |
| `content-id` | L’ID univoco dell’elemento dati restituito nella risposta. Se non viene passato, viene assegnato un ID generato automaticamente. | No |
| `content` | Il contenuto da analizzare tramite il servizio di somiglianza visiva. Nel caso in cui l&#39;immagine faccia parte del corpo della richiesta, utilizza `-F file=@<filename>` nel comando curl per passare l&#39;immagine, lasciando questo parametro come una stringa vuota. <br> Se l&#39;immagine è un file su S3, passare l&#39;URL firmato. Quando il contenuto fa parte del corpo della richiesta, l’elenco degli elementi dati deve avere un solo oggetto. Se vengono passati più oggetti, viene elaborato solo il primo oggetto. | Sì |
| `content-type` | Utilizzato per indicare se l’input fa parte del corpo della richiesta o è un URL firmato per un bucket S3. Il valore predefinito per questa proprietà è `inline`. | No |
| `encoding` | Il formato di file dell&#39;immagine di input. Attualmente è possibile elaborare solo immagini JPEG e PNG. Il valore predefinito per questa proprietà è `jpeg`. | No |
| `threshold` | La soglia di punteggio (da 0 a 1) al di sopra della quale è necessario restituire i risultati. Utilizzare il valore `0` per restituire tutti i risultati. Il valore predefinito per questa proprietà è `0`. | No |
| `top-N` | Il numero di risultati da restituire (non può essere un numero intero negativo). Utilizzare il valore `0` per restituire tutti i risultati. Se utilizzato insieme a `threshold`, il numero di risultati restituiti è il minore tra i due limiti impostati. Il valore predefinito per questa proprietà è `0`. | No |
| `custom` | Eventuali parametri personalizzati da trasmettere. | No |
| `historic-metadata` | Array che può essere passato ai metadati. | No |

**Risposta**

In caso di esito positivo, la risposta restituisce un array `response` che contiene `feature_value` e `feature_name` per ciascuna delle immagini visivamente simili trovate nel catalogo.

Le seguenti immagini visivamente simili sono state restituite nella risposta di esempio mostrata di seguito:

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
