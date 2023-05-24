---
keywords: Experience Platform;guida introduttiva;contenuto;tagging contenuto;tagging colore;estrazione colore;
solution: Experience Platform
title: Assegnazione di tag colore nell’API di assegnazione tag contenuto
description: Il servizio di assegnazione tag colore, quando viene fornita un’immagine, può calcolare l’istogramma dei colori pixel e ordinarli in base ai colori dominanti in contenitori.
exl-id: 6b3b6314-cb67-404f-888c-4832d041f5ed
source-git-commit: fd8891bdc7d528e327d2a72c2427f7bbc6dc8a03
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 5%

---

# Assegnazione di tag colore

Il servizio di assegnazione tag colore, quando viene fornita un’immagine, può calcolare un istogramma dei colori pixel e ordinarli in base ai colori dominanti in contenitori. I colori nei pixel dell’immagine sono inseriti in 40 colori predominanti che sono rappresentativi dello spettro di colori. Viene quindi calcolato un istogramma di valori di colore tra questi 40 colori. Il servizio è disponibile in due varianti:

**Assegnazione tag colore (immagine intera)**

Questo metodo estrae un istogramma a colori sull&#39;intera immagine.

**Applicazione di tag colore (con maschera)**

Questo metodo utilizza un sistema di estrazione in primo piano basato sull&#39;apprendimento profondo per identificare gli oggetti in primo piano. Una volta estratti gli oggetti di primo piano, viene calcolato un istogramma sui colori dominanti sia per le regioni di primo piano che per quelle di sfondo, insieme all&#39;intera immagine.

**Estrazione del tono**

Oltre alle varianti di cui sopra, puoi configurare il servizio per il recupero di un istogramma di toni per:

- Immagine complessiva (quando si utilizza una variante immagine completa)
- L’immagine complessiva e le aree di primo piano e sfondo (quando si utilizza la variante con il mascheramento)

Nell&#39;esempio riportato in questo documento è stata utilizzata l&#39;immagine seguente:

![immagine di prova](../images/QQAsset1.jpg)

**Formato API**

```http
POST /services/v2/predict
```

**Richiesta: variante immagine completa**

La richiesta di esempio seguente utilizza il metodo dell’immagine intera per l’assegnazione di tag colore ed estrae i colori da un’immagine in base ai parametri di input forniti nel payload. Per ulteriori informazioni sui parametri di input mostrati, consulta la tabella seguente il payload di esempio.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
  "sensei:invocation_mode": "synchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72"
      },
      "sensei:inputs": {
        "documents": [{
            "sensei:multipart_field_name": "infile_1",
            "dc:format": "image/jpg"
          }]
      },
      "sensei:params": {
        "top_n": 5,
        "min_coverage": 0.005      
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

**Risposta: variante immagine completa**

In caso di esito positivo, la risposta restituisce i dettagli dei colori estratti. Ogni colore è rappresentato da un `feature_value` key, che contiene le seguenti informazioni:

- Un nome di colore
- Percentuale di visualizzazione del colore in relazione all&#39;immagine
- Valore RGB del colore

`"White":{"coverage":0.5834,"rgb":{"red":254,"green":254,"blue":243}}`significa che il colore trovato è bianco, che si trova nel 58,34% dell&#39;immagine e ha un valore RGB medio di 254, 254, 243.

```json
{
    "statuses": [{
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
        "invocations": [{
            "sensei:outputs": {
                "result": {
                    "sensei:multipart_field_name": "result",
                    "dc:format": "application/json"
                }
            },
            "message": null,
            "status": "200"
        }]
    }],
    "request_id": "bfpzaJxKDxtgxpjUj5QDrN1jasjUw2RM"
}  
 
[{
    "overall": {
        "colors": {
            "White": {
                "coverage": 0.5834,
                "rgb": {
                    "red": 254,
                    "green": 254,
                    "blue": 243
                }
            },
            "Orange": {
                "coverage": 0.254,
                "rgb": {
                    "red": 249,
                    "green": 165,
                    "blue": 45
                }
            },
            "Gold": {
                "coverage": 0.0817,
                "rgb": {
                    "red": 253,
                    "green": 188,
                    "blue": 58
                }
            },
            "Mustard": {
                "coverage": 0.0727,
                "rgb": {
                    "red": 253,
                    "green": 207,
                    "blue": 84
                }
            },
            "Cream": {
                "coverage": 0.0082,
                "rgb": {
                    "red": 253,
                    "green": 236,
                    "blue": 174
                }
            }
        }
    }
}]
```

Il risultato qui presenta un colore estratto nella regione &quot;complessiva&quot; dell’immagine.

**Richiesta: variante immagine mascherata**

Nell&#39;esempio di richiesta seguente viene utilizzato il metodo di mascheramento per l&#39;assegnazione di tag colore. Questa funzione è abilitata impostando `enable_mask` parametro a `true` nella richiesta.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
  "sensei:invocation_mode": "synchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72"
      },
      "sensei:inputs": {
        "documents": [{
            "sensei:multipart_field_name": "infile_1",
            "dc:format": "image/jpg"
          }]
      },
      "sensei:params": {
        "top_n": 5,
        "min_coverage": 0.005,
        "enable_mask": true,
        "retrieve_tone": true     
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

>[!NOTE]
>
>Inoltre, il `retrieve_tone` Il parametro è impostato anche su `true` nella richiesta precedente. Questo consente di recuperare un istogramma di distribuzione del tono su toni caldi, neutri e freddi nelle aree generali, di primo piano e di sfondo dell&#39;immagine.

**Risposta - Variante immagine mascherata**

```json
{
    "statuses": [{
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
        "invocations": [{
            "sensei:outputs": {
                "result": {
                    "sensei:multipart_field_name": "result",
                    "dc:format": "application/json"
                }
            },
            "message": null,
            "status": "200"
        }]
    }],
    "request_id": "gpeCyJsrJvOWd94WwZOyPBPrKi2BQyla"
}  
 
 
[{
    "overall": {
        "colors": {
            "White": {
                "coverage": 0.5834,
                "rgb": {
                    "red": 254,
                    "green": 254,
                    "blue": 243
                }
            },
            "Orange": {
                "coverage": 0.254,
                "rgb": {
                    "red": 249,
                    "green": 165,
                    "blue": 45
                }
            },
            "Gold": {
                "coverage": 0.0817,
                "rgb": {
                    "red": 253,
                    "green": 188,
                    "blue": 58
                }
            },
            "Mustard": {
                "coverage": 0.0727,
                "rgb": {
                    "red": 253,
                    "green": 207,
                    "blue": 84
                }
            },
            "Cream": {
                "coverage": 0.0082,
                "rgb": {
                    "red": 253,
                    "green": 236,
                    "blue": 174
                }
            }
        },
        "tones": {
            "warm": 0.4084,
            "neutral": 0.5916,
            "cool": 0
        }
    },
    "foreground": {
        "colors": {
            "Orange": {
                "coverage": 0.6022,
                "rgb": {
                    "red": 249,
                    "green": 165,
                    "blue": 45
                }
            },
            "Gold": {
                "coverage": 0.1935,
                "rgb": {
                    "red": 253,
                    "green": 188,
                    "blue": 58
                }
            },
            "Mustard": {
                "coverage": 0.1722,
                "rgb": {
                    "red": 253,
                    "green": 207,
                    "blue": 84
                }
            },
            "Cream": {
                "coverage": 0.0173,
                "rgb": {
                    "red": 253,
                    "green": 235,
                    "blue": 170
                }
            },
            "Yellow": {
                "coverage": 0.0148,
                "rgb": {
                    "red": 254,
                    "green": 229,
                    "blue": 117
                }
            }
        },
        "tones": {
            "warm": 0.9827,
            "neutral": 0.0173,
            "cool": 0
        }
    },
    "background": {
        "colors": {
            "White": {
                "coverage": 0.9923,
                "rgb": {
                    "red": 254,
                    "green": 254,
                    "blue": 243
                }
            },
            "Dark_Brown": {
                "coverage": 0.0077,
                "rgb": {
                    "red": 83,
                    "green": 68,
                    "blue": 57
                }
            }
        },
        "tones": {
            "warm": 0,
            "neutral": 1.0,
            "cool": 0
        }
    }
}]
```

Oltre ai colori dell&#39;immagine complessiva, è ora possibile visualizzare anche i colori delle aree di primo piano e di sfondo. Poiché il recupero del tono è abilitato per ciascuna delle regioni sopra indicate, è anche possibile recuperare l&#39;istogramma di un tono.

**Parametri di input**

| Nome | Tipo di dati | Obbligatorio | Impostazione predefinita | Valori | Descrizione |
| --- | --- | --- | --- | --- | --- |
| `documents` | array (Document-Object) | Sì | - | Vedi sotto | Elenco di elementi JSON con ogni elemento nell’elenco che rappresenta un documento. |
| `top_n` | number | No | 0 | Numero intero non negativo | Numero di risultati da restituire. 0, per restituire tutti i risultati. Se utilizzato insieme a threshold, il numero di risultati restituiti sarà inferiore a uno dei due limiti. |
| `min_coverage` | number | No | 0.05 | Numero reale | Soglia di copertura oltre la quale i risultati devono essere restituiti. Escludi parametro per restituire tutti i risultati. |
| `resize_image` | number | No | True | Vero/Falso | Indica se ridimensionare o meno l&#39;immagine di input. Per impostazione predefinita, le immagini vengono ridimensionate a 320*320 pixel prima dell&#39;esecuzione dell&#39;estrazione del colore. A scopo di debug, possiamo consentire l’esecuzione del codice anche sull’immagine intera impostandola su `False`. |
| `enable_mask` | number | No | False | Vero/Falso | Attiva/disattiva l&#39;estrazione del colore |
| `retrieve_tone` | number | No | False | Vero/Falso | Attiva/disattiva l&#39;estrazione del tono |

**Oggetto Document**

| Nome | Tipo di dati | Obbligatorio | Impostazione predefinita | Valori | Descrizione |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | string | - | - | - | URL predefinito del documento. |
| `sensei:repoType` | string | - | - | HTTPS | Tipo di archivio in cui viene memorizzata l’immagine. |
| `sensei:multipart_field_name` | string | - | - | - | Utilizzalo quando trasmetti il file immagine come argomento multipart invece di utilizzare URL prefirmati. |
| `dc:format` | string | Sì | - | &quot;image/jpg&quot;,<br>image/jpeg<br>&quot;image/png&quot;,<br>&quot;image/tiff&quot; | La codifica dell’immagine viene verificata in base ai tipi di codifica di input consentiti prima dell’elaborazione. |