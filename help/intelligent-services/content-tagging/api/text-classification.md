---
keywords: classificazione testo;Classificazione testo
solution: Experience Platform
title: Classificazione del testo nell’API di IA per l’analisi dei contenuti e del commercio
description: Il servizio di classificazione del testo, se gli viene fornito un frammento di testo, può classificarlo in una o più etichette. La classificazione può essere single-label, multi-label o gerarchica.
exl-id: f240519a-0d83-4309-91e4-4e48be7955a1
source-git-commit: 081e31727b4e78126e60896b3b850c5589526152
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 4%

---

# Classificazione testo

>[!NOTE]
>
>IA per l’e-commerce di contenuti è in versione beta. La documentazione è soggetta a modifiche.

Il servizio di classificazione del testo, se gli viene fornito un frammento di testo, può classificarlo in una o più etichette. La classificazione può essere single-label, multi-label o gerarchica.

**Formato API**

```http
POST /services/v1/predict
```

**Richiesta**

La seguente richiesta classifica il testo di un frammento in base ai parametri di input forniti nel payload. Per ulteriori informazioni sui parametri di input mostrati, consulta la tabella seguente il payload di esempio.

>[!CAUTION]
>
>`analyzer_id` determina quale [!DNL Sensei Content Framework] viene utilizzato. Verifica di disporre dei `analyzer_id` prima di effettuare la richiesta. Contatta il team beta di IA per l’analisi dei contenuti e del commercio per ricevere il `analyzer_id` per questo servizio.

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
| `analyzer_id` | Il [!DNL Sensei] ID del servizio in cui è distribuita la richiesta. Questo ID determina quale [!DNL Sensei Content Frameworks] vengono utilizzati. Per i servizi personalizzati, contatta il team di IA per l’analisi dei contenuti e del commercio per impostare un ID personalizzato. | Sì |
| `application-id` | ID dell’applicazione creata. | Sì |
| `data` | Matrice che contiene un oggetto JSON con ogni oggetto nella matrice che rappresenta un documento. Qualsiasi parametro passato come parte di questa matrice sostituisce i parametri globali specificati al di fuori della `data` array. Una qualsiasi delle proprietà rimanenti descritte di seguito in questa tabella può essere ignorata dall&#39;interno di `data`. | Sì |
| `language` | Lingua del testo di input. Il valore predefinito è `en`. | No |
| `content-type` | Utilizzato per indicare se l’input fa parte del corpo della richiesta o è un URL firmato per un bucket S3. Il valore predefinito per questa proprietà è `inline`. | No |
| `encoding` | Formato di codifica del testo di input. Questo può essere `utf-8` o `utf-16`. Il valore predefinito per questa proprietà è `utf-8`. | No |
| `threshold` | La soglia di punteggio (da 0 a 1) al di sopra della quale è necessario restituire i risultati. Utilizza il valore `0` per restituire tutti i risultati. Il valore predefinito per questa proprietà è `0`. | No |
| `top-N` | Il numero di risultati da restituire (non può essere un numero intero negativo). Utilizza il valore `0` per restituire tutti i risultati. Se utilizzato in combinazione con `threshold`, il numero di risultati restituiti è il minore tra i due limiti impostati. Il valore predefinito per questa proprietà è `0`. | No |
| `custom` | Eventuali parametri personalizzati da trasmettere. Questa proprietà richiede un oggetto JSON valido per funzionare. | No |
| `content-id` | L’ID univoco dell’elemento dati restituito nella risposta. Se non viene passato, viene assegnato un ID generato automaticamente. | No |
| `content` | Contenuto utilizzato dal servizio di classificazione testo. Il contenuto può essere testo non elaborato (tipo di contenuto &quot;inline&quot;). <br> Se il contenuto è un file su S3 (tipo di contenuto &quot;s3-bucket&quot;), passa l’URL firmato. | Sì |

**Risposta**

In caso di esito positivo, la risposta restituisce il testo classificato in una matrice di risposta.

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
