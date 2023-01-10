---
keywords: Experience Platform;guida introduttiva;ai contenuti;ai e-commerce;contenuto e ai-commerce;estrazione colore;estrazione colore
solution: Experience Platform
title: Estrazione del colore nell’API Content and Commerce AI
description: Il servizio di estrazione del colore, quando viene fornita un'immagine, può calcolare l'istogramma dei colori dei pixel e ordinarli in blocchi in base ai colori dominanti.
exl-id: 6b3b6314-cb67-404f-888c-4832d041f5ed
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 2%

---

# Estrazione colore

>[!NOTE]
>
>[!DNL Content and Commerce AI] è in versione beta. La documentazione è soggetta a modifiche.

Il servizio di estrazione del colore, quando viene fornita un&#39;immagine, può calcolare un istogramma di colori pixel e ordinarli in blocchi in base a colori dominanti. I colori nei pixel dell&#39;immagine sono inseriti in 40 colori predominanti che sono rappresentativi dello spettro di colori. Un istogramma di valori di colore viene quindi calcolato tra i 40 colori. Il servizio ha due varianti:

**Estrazione colore (immagine completa)**

Questo metodo estrae un istogramma di colore sull&#39;intera immagine.

**Estrazione colore (con maschera)**

Questo metodo utilizza un estrattore in primo piano basato su apprendimento profondo per identificare gli oggetti in primo piano. Il modello viene addestrato su un catalogo di immagini e-commerce. Una volta estratto l’oggetto in primo piano, viene calcolato un istogramma sui colori dominanti come descritto in precedenza.

L&#39;immagine seguente è stata utilizzata nell&#39;esempio mostrato in questo documento:

![immagine di prova](../images/QQAsset1.jpg)

**Formato API**

```http
POST /services/v1/predict
```

**Richiesta**

La richiesta di esempio seguente utilizza il metodo full-image per l’estrazione del colore.

La richiesta seguente estrae i colori da un’immagine in base ai parametri di input forniti nel payload. Per ulteriori informazioni sui parametri di input mostrati, consulta la tabella riportata di seguito.

>[!CAUTION]
>
>`analyzer_id` determina quale [!DNL Sensei Content Framework] viene utilizzato. Verifica di avere il `analyzer_id` prima di fare la tua richiesta. Per il servizio di estrazione del colore, la `analyzer_id` ID:
>`Feature:image-color-histogram:Service-6fe52999293e483b8e4ae9a95f1b81a7`

```SHELL
curl -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: multipart/form-data' \
  -H 'x-api-key: {API_KEY}' \
  -H 'cache-control: no-cache,no-cache' \
  -F file=@test_image.jpg \
  -F 'contentAnalyzerRequests={
   "enable_diagnostics":"true",
   "requests":[
     {
         "analyzer_id": "Feature:image-color-histogram:Service-6fe52999293e483b8e4ae9a95f1b81a7",
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
            "custom": {"exclude_mask": 1}
            }]
          }
      }
    ]
}'
```

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| `analyzer_id` | La [!DNL Sensei] ID del servizio in cui viene distribuita la richiesta. Questo ID determina quale tra [!DNL Sensei Content Frameworks] sono utilizzati. Per i servizi personalizzati, contatta il team Content and Commerce AI per configurare un ID personalizzato. | Sì |
| `application-id` | ID dell&#39;applicazione creata. | Sì |
| `data` | Matrice che contiene oggetti JSON. Ogni oggetto dell&#39;array rappresenta un&#39;immagine. Eventuali parametri passati come parte di questa matrice sostituiscono i parametri globali specificati al di fuori della `data` array. È possibile ignorare tutte le proprietà rimanenti descritte in questa tabella all’interno di `data`. | Sì |
| `content-id` | L&#39;ID univoco dell&#39;elemento dati restituito nella risposta. Se non viene passato, viene assegnato un ID generato automaticamente. | No |
| `content` | Contenuto da analizzare dal servizio di estrazione del colore. Nel caso in cui l&#39;immagine faccia parte del corpo della richiesta, utilizza `-F file=@<filename>` nel comando curl per passare l&#39;immagine, lasciando questo parametro come stringa vuota. <br> Se l&#39;immagine è un file su S3, passa l&#39;url firmato. Quando il contenuto fa parte del corpo della richiesta, l’elenco degli elementi dati deve avere un solo oggetto. Se vengono passati più oggetti, viene elaborato solo il primo oggetto. | Sì |
| `content-type` | Utilizzato per indicare se l’input fa parte del corpo della richiesta o di un url firmato per un bucket S3. Il valore predefinito di questa proprietà è `inline`. | No |
| `encoding` | Formato del file dell&#39;immagine di input. Attualmente è possibile elaborare solo immagini JPEG e PNG. Il valore predefinito di questa proprietà è `jpeg`. | No |
| `threshold` | La soglia del punteggio (da 0 a 1) al di sopra della quale devono essere restituiti i risultati. Utilizza il valore `0` per restituire tutti i risultati. Il valore predefinito di questa proprietà è `0`. | No |
| `top-N` | Il numero di risultati da restituire (non può essere un numero intero negativo). Utilizza il valore `0` per restituire tutti i risultati. Se utilizzato in combinazione con `threshold`, il numero di risultati restituiti è il minore tra i due set di limiti. Il valore predefinito di questa proprietà è `0`. | No |
| `custom` | Eventuali parametri personalizzati da trasmettere. | No |
| `historic-metadata` | Matrice che può essere passata ai metadati. | No |

**Risposta**

Una risposta corretta restituisce i dettagli dei colori estratti. Ogni colore è rappresentato da un `feature_value` , che contiene le seguenti informazioni:

- Un nome di colore
- Percentuale visualizzata in relazione all&#39;immagine
- Valore RGB del colore

Nel primo oggetto di esempio sottostante, il `feature_value` di `White,0.59,251,251,243` significa che il colore trovato è bianco, il bianco si trova nel 59% dell&#39;immagine e ha un valore RGB di 251.251.243.

```json
{
  "status": 200,
  "content_id": "test_image.jpg",
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:image-color-histogram:Service-e952f4acd7c2425199b476a2eb459635",
      "content_id": "test_image.jpg",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_name": "color_name_and_rgb",
                "feature_value": "White,0.59,251,251,243"
              },
              {
                "feature_value": "Orange,0.30,248,169,48",
                "feature_name": "color_name_and_rgb"
              },
              {
                "feature_name": "color_name_and_rgb",
                "feature_value": "Mustard,0.08,251,199,77"
              },
              {
                "feature_name": "color_name_and_rgb",
                "feature_value": "Gold,0.02,250,191,55"
              }
            ],
            "feature_name": "color"
          }
        ]
      }
    }
  ],
  "error": []
}
```

| Proprietà | Descrizione |
| --- | --- |
| `content_id` | Nome dell’immagine caricata nella richiesta POST. |
| `feature_value` | Matrice i cui oggetti contengono chiavi con lo stesso nome di proprietà. Queste chiavi contengono una stringa che rappresenta il nome del colore, una percentuale che questo colore appare in relazione all&#39;immagine inviata nel `content_id`e il valore RGB del colore. |
