---
keywords: classificazione del testo;classificazione del testo
solution: Experience Platform
title: Classificazione del testo nell’API Content and Commerce AI
description: Se si assegna un frammento di testo, il servizio di classificazione del testo può classificarlo in una o più etichette. La classificazione può essere a etichetta singola, a etichetta multipla o gerarchica.
exl-id: f240519a-0d83-4309-91e4-4e48be7955a1
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 4%

---

# Classificazione del testo

>[!NOTE]
>
>Content and Commerce AI è in versione beta. La documentazione è soggetta a modifiche.

Se si assegna un frammento di testo, il servizio di classificazione del testo può classificarlo in una o più etichette. La classificazione può essere a etichetta singola, a etichetta multipla o gerarchica.

**Formato API**

```http
POST /services/v1/predict
```

**Richiesta**

La seguente richiesta classifica il testo da un frammento in base ai parametri di input forniti nel payload. Per ulteriori informazioni sui parametri di input mostrati, consulta la tabella riportata di seguito.

>[!CAUTION]
>
>`analyzer_id` determina quale [!DNL Sensei Content Framework] viene utilizzato. Verifica di avere il `analyzer_id` prima di fare la tua richiesta. Contatta il team beta di Content and Commerce AI per ricevere il tuo `analyzer_id` per questo servizio.

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
| `analyzer_id` | La [!DNL Sensei] ID del servizio in cui viene distribuita la richiesta. Questo ID determina quale tra [!DNL Sensei Content Frameworks] sono utilizzati. Per i servizi personalizzati, contatta il team Content and Commerce AI per configurare un ID personalizzato. | Sì |
| `application-id` | ID dell&#39;applicazione creata. | Sì |
| `data` | Matrice che contiene un oggetto JSON con ogni oggetto della matrice che rappresenta un documento. Eventuali parametri passati come parte di questa matrice sostituiscono i parametri globali specificati al di fuori della `data` array. È possibile ignorare tutte le proprietà rimanenti descritte in questa tabella all’interno di `data`. | Sì |
| `language` | Lingua del testo di input. Il valore predefinito è `en`. | No |
| `content-type` | Utilizzato per indicare se l’input fa parte del corpo della richiesta o di un url firmato per un bucket S3. Il valore predefinito di questa proprietà è `inline`. | No |
| `encoding` | Formato di codifica del testo di input. Questo può essere `utf-8` o `utf-16`. Il valore predefinito di questa proprietà è `utf-8`. | No |
| `threshold` | La soglia del punteggio (da 0 a 1) al di sopra della quale devono essere restituiti i risultati. Utilizza il valore `0` per restituire tutti i risultati. Il valore predefinito di questa proprietà è `0`. | No |
| `top-N` | Il numero di risultati da restituire (non può essere un numero intero negativo). Utilizza il valore `0` per restituire tutti i risultati. Se utilizzato in combinazione con `threshold`, il numero di risultati restituiti è il minore tra i due set di limiti. Il valore predefinito di questa proprietà è `0`. | No |
| `custom` | Eventuali parametri personalizzati da trasmettere. Questa proprietà richiede un oggetto JSON valido per funzionare. | No |
| `content-id` | L&#39;ID univoco dell&#39;elemento dati restituito nella risposta. Se non viene passato, viene assegnato un ID generato automaticamente. | No |
| `content` | Contenuto utilizzato dal servizio di classificazione del testo. Il contenuto può essere in formato testo non elaborato (tipo di contenuto &quot;inline&quot;). <br> Se il contenuto è un file sul tipo di contenuto S3 (&#39;s3-bucket&#39;), passa l’url firmato. | Sì |

**Risposta**

Una risposta corretta restituisce il testo classificato in una matrice di risposta.

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
