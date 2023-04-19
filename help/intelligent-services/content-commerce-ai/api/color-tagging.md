---
keywords: Experience Platform;guida introduttiva;contenuto;assegnazione tag contenuti;assegnazione tag colore;estrazione colore;
solution: Experience Platform
title: Assegnazione di tag colore nell’API per l’assegnazione tag dei contenuti
description: Il servizio di assegnazione dei colori, quando viene fornita un’immagine, può calcolare l’istogramma dei colori dei pixel e ordinarli in blocchi in base ai colori dominanti.
exl-id: 6b3b6314-cb67-404f-888c-4832d041f5ed
source-git-commit: fd8891bdc7d528e327d2a72c2427f7bbc6dc8a03
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 5%

---

# Assegnazione tag colore

Il servizio di assegnazione tag colore, quando viene fornita un’immagine, può calcolare un istogramma di colori pixel e ordinarli in blocchi in base a colori dominanti. I colori nei pixel dell&#39;immagine sono inseriti in 40 colori predominanti che sono rappresentativi dello spettro di colori. Un istogramma di valori di colore viene quindi calcolato tra i 40 colori. Il servizio ha due varianti:

**Assegnazione tag colore (immagine completa)**

Questo metodo estrae un istogramma di colore sull&#39;intera immagine.

**Assegnazione tag colore (con maschera)**

Questo metodo utilizza un estrattore in primo piano basato su apprendimento profondo per identificare gli oggetti in primo piano. Una volta estratti gli oggetti in primo piano, viene calcolato un istogramma sui colori dominanti sia per le aree in primo piano che per quelle di sfondo, insieme all’intera immagine.

**Estrazione del tono**

Oltre alle varianti sopra menzionate, puoi configurare il servizio per recuperare un istogramma di toni per:

- Immagine complessiva (quando si utilizza la variante immagine completa)
- Immagine complessiva, aree in primo piano e di sfondo (quando si utilizza la variante con maschera)

L&#39;immagine seguente è stata utilizzata nell&#39;esempio mostrato in questo documento:

![immagine di prova](../images/QQAsset1.jpg)

**Formato API**

```http
POST /services/v2/predict
```

**Richiesta - variante immagine completa**

L’esempio di richiesta seguente utilizza il metodo dell’immagine completa per l’assegnazione di tag colore ed estrae i colori da un’immagine in base ai parametri di input forniti nel payload. Per ulteriori informazioni sui parametri di input mostrati, consulta la tabella riportata di seguito.

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

**Risposta - variante immagine completa**

Una risposta corretta restituisce i dettagli dei colori estratti. Ogni colore è rappresentato da un `feature_value` , che contiene le seguenti informazioni:

- Un nome di colore
- Percentuale visualizzata in relazione all&#39;immagine
- Valore RGB del colore

`"White":{"coverage":0.5834,"rgb":{"red":254,"green":254,"blue":243}}`significa che il colore trovato è bianco, che si trova nel 58,34% dell&#39;immagine, e ha un valore RGB medio di 254, 254, 243.

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

Notate che il risultato qui ha il colore estratto sulla regione immagine &quot;complessiva&quot;.

**Richiesta - variante immagine mascherata**

L’esempio di richiesta seguente utilizza il metodo di mascheramento per l’assegnazione di tag colore. Questa opzione è abilitata impostando la variabile `enable_mask` parametro a `true` nella richiesta.

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
>Inoltre, la `retrieve_tone` anche il parametro è impostato su `true` nella richiesta di cui sopra. Questo ci permette di recuperare un istogramma di distribuzione del tono su toni caldi, neutri e freddi nelle aree generali, in primo piano e di sfondo dell&#39;immagine.

**Risposta: variante immagine mascherata**

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

Oltre ai colori dell&#39;immagine complessiva, ora è possibile vedere anche i colori provenienti dalle aree in primo piano e di sfondo. Poiché il recupero dei toni è abilitato per ciascuna delle aree di cui sopra, puoi anche recuperare l’istogramma di un tono.

**Parametri di input**

| Nome | Tipo di dati | Obbligatorio | Impostazione predefinita | Valori | Descrizione |
| --- | --- | --- | --- | --- | --- |
| `documents` | array (Document-Object) | Sì | - | Vedi sotto | Elenco di elementi JSON con ogni elemento dell’elenco che rappresenta un documento. |
| `top_n` | number | No | 0 | Numero intero non negativo | Numero di risultati da restituire. 0, per restituire tutti i risultati. Se utilizzato insieme alla soglia, il numero di risultati restituiti sarà inferiore a uno dei due limiti. |
| `min_coverage` | number | No | 0.05 | Numero reale | Soglia di copertura oltre la quale è necessario restituire i risultati. Escludi parametro per restituire tutti i risultati. |
| `resize_image` | number | No | True | True/False | Se ridimensionare o meno l’immagine di input. Per impostazione predefinita, le immagini vengono ridimensionate a 320*320 pixel prima dell’estrazione del colore. A scopo di debug possiamo consentire l’esecuzione del codice anche su immagine completa, impostando questo su `False`. |
| `enable_mask` | number | No | False | True/False | Abilita/disabilita l’estrazione del colore |
| `retrieve_tone` | number | No | False | True/False | Abilita/disabilita l’estrazione del tono |

**Oggetto Document**

| Nome | Tipo di dati | Obbligatorio | Impostazione predefinita | Valori | Descrizione |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | string | - | - | - | URL del documento firmato. |
| `sensei:repoType` | string | - | - | HTTPS | Tipo di repository in cui viene memorizzata l&#39;immagine. |
| `sensei:multipart_field_name` | string | - | - | - | Utilizzalo quando trasmetti il file immagine come argomento multiparte invece di utilizzare gli URL prefirmati. |
| `dc:format` | string | Sì | - | &quot;image/jpg&quot;,<br>&quot;image/jpeg&quot;,<br>&quot;image/png&quot;,<br>&quot;image/tiff&quot; | La codifica delle immagini viene controllata in base ai tipi di codifica di input consentiti prima di essere elaborata. |