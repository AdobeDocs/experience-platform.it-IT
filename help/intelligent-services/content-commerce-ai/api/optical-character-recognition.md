---
keywords: OCR;presenza di testo;riconoscimento ottico dei caratteri
solution: Experience Platform
title: Presenza di testo e riconoscimento ottico dei caratteri
description: Nell’API Content and Commerce AI, il servizio di riconoscimento ottico dei caratteri (OCR, Text Presence / Optical Character Recognition) può indicare se un testo è presente in una determinata immagine. Se il testo è presente, OCR può restituire il testo.
exl-id: 85b976a7-0229-43e9-b166-cdbd213b867f
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 4%

---

# Presenza di testo e riconoscimento ottico dei caratteri

>[!NOTE]
>
>Content and Commerce AI è in versione beta. La documentazione è soggetta a modifiche.

Il servizio di riconoscimento ottico dei caratteri (OCR, Text Presence / Optical Character Recognition), quando viene fornita un&#39;immagine, può indicare se il testo è presente nell&#39;immagine. Se il testo è presente, OCR può restituire il testo.

L&#39;immagine seguente è stata utilizzata nella richiesta di esempio mostrata in questo documento:

![immagine di prova](../images/shef.jpeg)

**Formato API**

```http
POST /services/v1/predict
```

**Richiesta**

La richiesta seguente verifica se il testo è presente in base all’immagine di input fornita nel payload. Per ulteriori informazioni sui parametri di input mostrati, consulta la tabella riportata di seguito.

>[!CAUTION]
>
>`analyzer_id` determina quale [!DNL Sensei Content Framework] viene utilizzato. Verifica di avere il `analyzer_id` prima di fare la tua richiesta. Contatta il team beta di Content and Commerce AI per ricevere il tuo `analyzer_id` per questo servizio.

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
| `analyzer_id` | La [!DNL Sensei] ID del servizio in cui viene distribuita la richiesta. Questo ID determina quale tra [!DNL Sensei Content Frameworks] sono utilizzati. Per i servizi personalizzati, contatta il team Content and Commerce AI per configurare un ID personalizzato. | Sì |
| `application-id` | ID dell&#39;applicazione creata. | Sì |
| `data` | Matrice che contiene un oggetto JSON con ogni oggetto della matrice che rappresenta un’immagine passata. Eventuali parametri passati come parte di questa matrice sostituiscono i parametri globali specificati al di fuori della `data` array. È possibile ignorare tutte le proprietà rimanenti descritte in questa tabella all’interno di `data`. | Sì |
| `language` | Lingua del testo di input. Il valore predefinito è `en`. | No |
| `content-type` | Utilizzato per indicare se l’input fa parte del corpo della richiesta o di un url firmato per un bucket S3. Il valore predefinito di questa proprietà è `inline`. | No |
| `encoding` | Formato del file dell&#39;immagine di input. Attualmente è possibile elaborare solo immagini JPEG e PNG. Il valore predefinito di questa proprietà è `jpeg`. | No |
| `threshold` | La soglia del punteggio (da 0 a 1) al di sopra della quale devono essere restituiti i risultati. Utilizza il valore `0` per restituire tutti i risultati. Il valore predefinito di questa proprietà è `0`. | No |
| `top-N` | Il numero di risultati da restituire (non può essere un numero intero negativo). Utilizza il valore `0` per restituire tutti i risultati. Se utilizzato in combinazione con `threshold`, il numero di risultati restituiti è il minore tra i due set di limiti. Il valore predefinito di questa proprietà è `0`. | No |
| `custom` | Eventuali parametri personalizzati da trasmettere. Questa proprietà richiede un oggetto JSON valido per funzionare. | No |
| `content-id` | L&#39;ID univoco dell&#39;elemento dati restituito nella risposta. Se non viene passato, viene assegnato un ID generato automaticamente. | No |
| `content` | Il contenuto può essere un’immagine non elaborata (tipo di contenuto &quot;inline&quot;). <br> Se il contenuto è un file sul tipo di contenuto S3 (&#39;s3-bucket&#39;), passa l’URL firmato. | Sì |

**Risposta**

Una risposta corretta restituisce il testo rilevato nel `feature_value` array. Il testo viene letto e restituito dall’alto verso il basso da sinistra a destra. Ciò significa che se è stato rilevato &quot;Amo l&#39;Adobe&quot;, il payload restituisce &quot;I&quot;, &quot;amore&quot; e &quot;Adobe&quot; in oggetti separati. Nell’oggetto viene assegnato un `feature_name` che contiene la parola e un `feature_value` che contiene una metrica di affidabilità per quel testo.

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
