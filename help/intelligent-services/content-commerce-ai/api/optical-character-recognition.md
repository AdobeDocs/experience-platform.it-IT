---
keywords: OCR;presenza di testo;riconoscimento ottico dei caratteri
solution: Experience Platform, Intelligent Services
title: Presenza di testo e riconoscimento ottico dei caratteri
topic: Developer guide
description: Nell'API Content and Commerce AI, il servizio di riconoscimento ottico dei caratteri (OCR, Text Presence / Optical Character Recognition) può indicare se in una determinata immagine è presente del testo. Se il testo è presente, OCR può restituire il testo.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 3%

---


# Presenza di testo e riconoscimento ottico dei caratteri

>[!NOTE]
>
>Content and Commerce AI è in versione beta. La documentazione è soggetta a modifiche.

Il servizio di riconoscimento ottico dei caratteri (OCR, Text Presence / Optical Character Recognition), quando viene fornita un&#39;immagine, può indicare se nell&#39;immagine è presente del testo. Se il testo è presente, OCR può restituire il testo.

L&#39;immagine seguente è stata utilizzata nella richiesta di esempio mostrata in questo documento:

![immagine di prova](../images/shef.jpeg)

**Formato API**

```http
POST /services/v1/predict
```

**Richiesta**

La seguente richiesta verifica se è presente del testo in base all&#39;immagine di input fornita nel payload. Per ulteriori informazioni sui parametri di input, vedere la tabella sotto il payload di esempio.

>[!CAUTION]
>
>`analyzer_id` determina quale  [!DNL Sensei Content Framework] viene utilizzato. Prima di effettuare la richiesta, verificare di disporre del `analyzer_id` corretto. Contatta il team beta di Content and Commerce AI per ricevere la `analyzer_id` per questo servizio.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: multipart/form-data" \
  -H "cache-control: no-cache,no-cache" \
  -H "x-api-key: {API_KEY}" \
  -F file=@TestImage.jpg \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
    "analyzer_id": "Feature:image-text-extractor-ocr:Service-b0675160421e404ca3c7ca60f46a5b29",
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
    }]
  }'
```

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| `analyzer_id` | L&#39;ID del servizio [!DNL Sensei] in cui viene distribuita la richiesta. Questo ID determina quale delle [!DNL Sensei Content Frameworks] vengono utilizzate. Per i servizi personalizzati, contattate il team di Content and Commerce AI per configurare un ID personalizzato. | Sì |
| `application-id` | ID dell’applicazione creata. | Sì |
| `data` | Un array che contiene un oggetto JSON con ogni oggetto nell&#39;array che rappresenta un&#39;immagine passata. Tutti i parametri passati come parte di questa matrice sostituiscono i parametri globali specificati all&#39;esterno dell&#39;array `data`. Qualsiasi proprietà rimanente descritta in questa tabella può essere ignorata dall&#39;interno di `data`. | Sì |
| `language` | Lingua del testo di input. Il valore predefinito è `en`. | No |
| `content-type` | Utilizzato per indicare se l&#39;input fa parte del corpo della richiesta o un URL firmato per un bucket S3. Il valore predefinito di questa proprietà è `inline`. | No |
| `encoding` | Il formato file dell&#39;immagine di input. Attualmente è possibile elaborare solo immagini JPEG e PNG. Il valore predefinito di questa proprietà è `jpeg`. | No |
| `threshold` | La soglia di punteggio (da 0 a 1) al di sopra della quale devono essere restituiti i risultati. Utilizzare il valore `0` per restituire tutti i risultati. Il valore predefinito di questa proprietà è `0`. | No |
| `top-N` | Il numero di risultati da restituire (non può essere un numero intero negativo). Utilizzare il valore `0` per restituire tutti i risultati. Se utilizzato insieme a `threshold`, il numero di risultati restituiti è minore di uno dei due set di limiti. Il valore predefinito di questa proprietà è `0`. | No |
| `custom` | Eventuali parametri personalizzati da passare. Questa proprietà richiede un oggetto JSON valido per funzionare. | No |
| `content-id` | L&#39;ID univoco per l&#39;elemento dati restituito nella risposta. Se non viene passato, viene assegnato un ID generato automaticamente. | No |
| `content` | Il contenuto può essere un’immagine non in linea (tipo di contenuto &quot;in linea&quot;). <br> Se il contenuto è un file su S3 (tipo di contenuto s3-bucket), trasmettere l&#39;URL firmato. | Sì |

**Risposta**

Una risposta corretta restituisce il testo rilevato nell&#39;array `feature_value`. Il testo viene letto e riportato in alto da sinistra a destra. Questo significa che se &quot;Amo  Adobe&quot; è stato rilevato, il payload restituisce &quot;I&quot;, &quot;love&quot;, e &quot; Adobe&quot; in oggetti separati. Nell&#39;oggetto vi viene assegnato un `feature_name` contenente la parola e un `feature_value` contenente una metrica di confidenza per quel testo.

```json
{
  "status": 200,
  "content_id": "TestImage.jpg",
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:image-text-extractor-ocr:Service-b0675160421e404ca3c7ca60f46a5b29",
      "content_id": "TestImage.jpg",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_value": "yes",
                "feature_name": "has_text"
              },
              {
                "feature_value": "0.977",
                "feature_name": "CHEF"
              },
              {
                "feature_value": "success",
                "feature_name": "text_processing_status"
              }
            ],
            "feature_name": "ocr"
          }
        ]
      }
    }
  ],
  "error": []
}
```
