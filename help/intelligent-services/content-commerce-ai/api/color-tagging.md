---
keywords: Experience Platform;guida introduttiva;contenuto ai;commerce ai;tagging contenuto;tagging colore;estrazione colore;
solution: Experience Platform
title: Assegnazione di tag colore nell’API di assegnazione tag contenuto
description: Il servizio di assegnazione tag colore, quando viene fornita un’immagine, può calcolare l’istogramma dei colori pixel e ordinarli in base ai colori dominanti in contenitori.
exl-id: 6b3b6314-cb67-404f-888c-4832d041f5ed
source-git-commit: b124ed97da8bde2a7fc4f10d350c81a47e096f29
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 5%

---

# Assegnazione di tag colore

Il servizio di assegnazione tag colore, quando viene fornita un’immagine, può calcolare un istogramma dei colori pixel e ordinarli in base ai colori dominanti in contenitori. I colori nei pixel dell’immagine sono inseriti in 40 colori predominanti che sono rappresentativi dello spettro di colori. Viene quindi calcolato un istogramma di valori di colore tra questi 40 colori. Il servizio è disponibile in due varianti:

**Assegnazione tag colore (immagine intera)**

Questo metodo estrae un istogramma a colori sull&#39;intera immagine.

**Applicazione di tag colore (con maschera)**

Questo metodo utilizza un sistema di estrazione in primo piano basato sull&#39;apprendimento profondo per identificare gli oggetti in primo piano. Il modello viene addestrato su un catalogo di immagini di e-commerce. Una volta estratto l&#39;oggetto di primo piano, viene calcolato un istogramma sui colori dominanti come descritto in precedenza.

Nell&#39;esempio riportato in questo documento è stata utilizzata l&#39;immagine seguente:

![immagine di prova](../images/QQAsset1.jpg)

**Formato API**

```http
POST /services/v2/predict
```

**Richiesta**

Nell&#39;esempio di richiesta seguente viene utilizzato il metodo full-image per l&#39;assegnazione dei tag colore.

La richiesta seguente estrae i colori da un’immagine in base ai parametri di input forniti nel payload. Per ulteriori informazioni sui parametri di input mostrati, consulta la tabella seguente il payload di esempio.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:cintel-image-classifier:Service-60887e328ded447d86e01122a4f19c58",
  "sensei:invocation_mode": "synchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:cintel-image-classifier:Service-60887e328ded447d86e01122a4f19c58"
      },
      "sensei:inputs": {
        "documents": [{
            "sensei:multipart_field_name": "infile_1",
            "dc:format": "image/jpg"
          }]
      },
      "sensei:params": {
        "application-id": "1234",
        "enable_mask": 0
      },
      "sensei:outputs":{
        "result" : {
          "sensei:multipart_field_name" : "result",
          "dc:format": "application/json"
        }
      }
    }
  ]
}' \
-F 'infile_1=@1431RDMJANELLERAWJACKE_2.jpg'
```

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| `application-id` | ID dell’applicazione creata. | Sì |
| `documents` | Elenco di elementi JSON in cui ogni elemento dell’elenco rappresenta un documento. | Sì |
| `top_n` | Numero di risultati da restituire (non può essere un numero intero negativo). Utilizza il valore `0` per restituire tutti i risultati. Se utilizzato in combinazione con `threshold`, il numero di risultati restituiti è il minore tra i due limiti impostati. Il valore predefinito per questa proprietà è `0`. | No |
| `min_coverage` | Soglia di copertura oltre la quale i risultati devono essere restituiti. Escludi il parametro per restituire tutti i risultati. | No |
| `resize_image` | Indica se l&#39;immagine di input deve essere ridimensionata. Per impostazione predefinita, le immagini vengono ridimensionate a 320*320 pixel prima dell&#39;applicazione del tag colore. A scopo di debug, possiamo consentire l’esecuzione del codice anche sull’immagine intera impostandolo su False. | No |
| `enable_mask` | Attiva/disattiva l&#39;assegnazione di tag colore nella maschera. | No |

| Nome | Tipo di dati | Obbligatorio | Impostazione predefinita | Valori | Descrizione |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | string | - | - | - | URL preceduto del documento da cui estrarre le frasi chiave. |
| `sensei:repoType` | string | - | - | HTTPS | Tipo di archivio in cui viene memorizzata l’immagine. |
| `sensei:multipart_field_name` | string | - | - | - | Utilizzalo quando trasmetti un file immagine come argomento multipart invece di utilizzare URL prefirmati. |
| `dc:format` | string | Sì | - | &quot;image/jpg&quot;, <br> image/jpeg <br>&quot;image/png&quot;, <br>&quot;image/tiff&quot; | La codifica dell’immagine viene verificata in base ai tipi di codifica di input consentiti prima dell’elaborazione. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli dei colori estratti. Ogni colore è rappresentato da un `feature_value` key, che contiene le seguenti informazioni:

- Un nome di colore
- Percentuale di visualizzazione del colore in relazione all&#39;immagine
- Valore RGB del colore

Nel primo oggetto di esempio riportato di seguito, `feature_value` di `Mud_Green,0.069,102,72,95` significa che il colore trovato è verde fango, verde fango si trova nel 6,9% dell&#39;immagine, e ha un valore RGB di 102,72,95.

```json
{
  "status": 200,
  "content_id": "test_image.jpg",
  "cas_responses": [
    {
{
  "statuses": [
    {
      "sensei:engine": "Feature:cintel-image-classifier:Service-60887e328ded447d86e01122a4f19c58",
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
  "request_id": "hsxycVq5Q9KbZ7MWrt6NXcSNWbonSLf3"
}

[
  {
    "request_element_id": "0",
    "colors": {
      "Mud_Green": {
        "coverage": 0.0694,
        "rgb": {
          "red": 102,
          "blue": 72,
          "green": 95
        }
      },
      "Dark_Brown": {
        "coverage": 0.1226,
        "rgb": {
          "red": 113,
          "blue": 77,
          "green": 84
        }
      },
      "Pink": {
        "coverage": 0.0731,
        "rgb": {
          "red": 234,
          "blue": 201,
          "green": 209
        }
      },
      "Dark_Gray": {
        "coverage": 0.1533,
        "rgb": {
          "red": 63,
          "blue": 58,
          "green": 59
        }
      },
      "Olive": {
        "coverage": 0.492,
        "rgb": {
          "red": 177,
          "blue": 126,
          "green": 170
        }
      },
      "Brown": {
        "coverage": 0.0896,
        "rgb": {
          "red": 141,
          "blue": 85,
          "green": 105
        }
      }
    }
  }
]
}
```
