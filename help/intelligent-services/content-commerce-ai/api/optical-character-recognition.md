---
keywords: OCR;presenza di testo;riconoscimento ottico dei caratteri
solution: Experience Platform
title: Presenza di testo e riconoscimento ottico dei caratteri
description: Nell’API di assegnazione tag contenuto, il servizio di riconoscimento ottico dei caratteri (OCR, Text Presence/Optical Character Recognition) può indicare se un testo è presente in una determinata immagine. Se il testo è presente, OCR può restituire il testo.
exl-id: 85b976a7-0229-43e9-b166-cdbd213b867f
source-git-commit: 82722ddf7ff543361177b555fffea730a7879886
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 4%

---

# Presenza di testo e riconoscimento ottico dei caratteri

Il servizio di riconoscimento della presenza di testo/del carattere ottico (OCR), quando viene fornita un&#39;immagine, può indicare se il testo è presente nell&#39;immagine. Se il testo è presente, OCR può restituire il testo.

L&#39;immagine seguente è stata utilizzata nella richiesta di esempio mostrata in questo documento:

![Immagine di esempio](../images/sample_image.png)

**Formato API**

```http
POST /services/v2/predict
```

**Richiesta**

La richiesta seguente verifica se il testo è presente in base all’immagine di input fornita nel payload. Per ulteriori informazioni sui parametri di input mostrati, consulta la tabella riportata di seguito.

Esecuzione con immagine in linea:

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F file=@sample_image.png \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
  "sensei:invocation_mode": "asynchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690"
      },
      "sensei:inputs": {
        "documents": [
        {
          "sensei:multipart_field_name": "file",
          "dc:format": "image/jpg"
        }
        ]
      },
      "sensei:params": {
        "correct_with_dictionary": true,
        "min_probability": 0.2,
        "min_relevance": 0.01,
        "filter_with_dictionary": true
      },
      "sensei:outputs":{
        "result" : {
          "sensei:multipart_field_name" : "result",
          "dc:format": "application/json"
        }
      }
    }
  ]
}'
```

**Risposta**

Una risposta corretta restituisce il testo rilevato nel `tags` elenco per ogni immagine passata nella richiesta. Se non c&#39;è testo in una determinata immagine, `is_text_present` è 0 e `tags` è un elenco vuoto.

[result0, result1, ...]: elenco delle risposte per ciascun documento di input. Ogni risultato è un decreto con le chiavi:

1. request_element_id: indice corrispondente al file di input per questa risposta, 0 per la prima immagine nell’elenco dei documenti della richiesta, 1 per la successiva e così via.
2. tag: elenco di dizionari, ogni dizionario ha due chiavi: testo, che è una parola riconosciuta dall’immagine, e rilevanza, calcolata come frazione dell’area del riquadro di delimitazione del testo estratto rispetto all’immagine completa. 0,01 tradurrebbe in un testo che occupa almeno l’1% dell’immagine.
3. is_text_present: 0 o 1 a seconda se il testo è presente nell’immagine. Se i tag sono 0, l’elenco è vuoto.

```json
{
  "contentAnalyzerResponse": {
    "statuses": [
      {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
        "invocations": [
          {
            "sensei:outputs": {
              "result": {
                "sensei:multipart_field_name": "result",
                "dc:format": "application/json"
              }
            },
            "message": null,
            "status": "200"
          }
        ]
      }
    ],
    "request_id": "dttklFR7DPtMtEmjlRSx5BYP5WGg3tTx"
  },
  "result": [
    {
      "is_text_present": 1,
      "tags": [
        {
          "text": "yosemite",
          "relevance": 0.06
        }
      ],
      "request_element_id": 0
    }
  ]
}
```

**Richiesta**

La richiesta seguente verifica se il testo è presente in base all’immagine di input fornita nel payload. Per ulteriori informazioni sui parametri di input mostrati, consulta la tabella riportata di seguito.

Esecuzione con URL:

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
  "sensei:invocation_mode": "asynchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690"
      },
      "sensei:inputs": {
        "documents": [
        {
          "repo:path": <IMG_URL_PATH>,
          "sensei:repoType": "HTTP",
          "dc:format": "image/jpg"
        }
        ]
      },
      "sensei:params": {
        "correct_with_dictionary": true
      },
      "sensei:outputs":{
        "result" : {
          "sensei:multipart_field_name" : "result",
          "dc:format": "application/json"
        }
      }
    }
  ]
}'
```

```json
{
  "contentAnalyzerResponse": {
    "statuses": [
      {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
        "invocations": [
          {
            "sensei:outputs": {
              "result": {
                "sensei:multipart_field_name": "result",
                "dc:format": "application/json"
              }
            },
            "message": null,
            "status": "200"
          }
        ]
      }
    ],
    "request_id": "ZbdhcK0JqS4Wg1wGdlEHGR3JOm530YNn"
  },
  "result": [
    {
      "is_text_present": 0,
      "tags": [],
      "request_element_id": 0
    }
  ]
}
```

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| `documents` | Elenco di elementi JSON con ogni elemento dell’elenco che rappresenta un’immagine. Tutti i parametri passati come parte di questo elenco, sovrascrivono il parametro globale specificato al di fuori dell’elenco, per l’elemento elenco corrispondente. | Sì |
| `sensei:multipart_field_name` | nome_campo da cui leggere il percorso del file di input. | Sì |
| `repo:path` | URL della risorsa immagine preselezionato. | Sì |
| `sensei:repoType` | &quot;HTTP&quot; (per presigned-url). | No |
| `dc:format` | Formato codificato dell&#39;immagine di input. Per la codifica delle immagini sono consentiti solo formati immagine come jpeg, jpg, png e tiff. Il formato dc:viene confrontato con i formati consentiti. | No |
| `correct_with_dictionary` | Se correggere le parole con un dizionario inglese? Se non è attivato, è possibile che le parole non inglesi vengano riconosciute. Il valore predefinito è True: attivato.) Nota che quando il dizionario è attivato, non è necessario che si ottenga sempre una parola inglese. Cerchiamo di correggerlo, ma se non è possibile entro una certa distanza di modifica, restituiamo la parola originale. | No |
| `filter_with_dictionary` | Se filtrare le parole in modo che contengano solo le parole dal dizionario inglese? Se questa opzione è attivata, le parole restituite appariranno sempre al grande inglese , che comprende 470.000 parole. | No |
| `min_probability` | Qual è la probabilità minima per le parole riconosciute? Il servizio restituisce solo le parole estratte dall&#39;immagine e con una probabilità maggiore di min_probabilità. Il valore predefinito è impostato su 0,2. | No |
| `min_relevance` | Qual è la rilevanza minima per le parole riconosciute? Il servizio restituisce solo le parole estratte dall&#39;immagine e con una rilevanza maggiore di min_relevant . Il valore predefinito è impostato su 0,01. La rilevanza viene calcolata come frazione dell’area del riquadro di delimitazione del testo estratto rispetto all’immagine completa. 0,01 tradurrebbe in un testo che occupa almeno l’1% dell’immagine. | No |

| Nome | Tipo di dati | Obbligatorio | Impostazione predefinita | Valori | Descrizione |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | string | - | - | - | URL dell’immagine da cui estrarre il testo. |
| `sensei:repoType` | string | - | - | HTTPS | Tipo di repository in cui viene memorizzata l&#39;immagine. |
| `sensei:multipart_field_name` | string | - | - | - | Utilizzalo quando trasmetti l’immagine come argomento multiparte invece di utilizzare url con prefisso. |
| `dc:format` | string | Sì | - | &quot;image/jpg&quot;, <br>&quot;image/jpeg&quot;, <br>&quot;image/png&quot;, <br>&quot;image/tiff&quot; | La codifica delle immagini viene controllata in base ai tipi di codifica di input consentiti prima di essere elaborata. |