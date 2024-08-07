---
keywords: Experience Platform;home;argomenti popolari;origini;connettori;sorgente connettori;sorgenti sdk;sdk;SDK
title: Configurare le specifiche di esplorazione per le origini self-service (SDK batch)
description: Questo documento fornisce una panoramica delle configurazioni da preparare per utilizzare Self-Service Sources (SDK batch).
exl-id: 423a7e56-9dd1-4071-bd26-ee4f9f206122
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 1%

---

# Configurare le specifiche di esplorazione per le origini self-service (SDK batch)

Esplora specifiche definisce i parametri necessari per l&#39;esplorazione e l&#39;ispezione degli oggetti contenuti nell&#39;origine. Esplora le specifiche definisce anche il formato di risposta restituito quando gli oggetti vengono esplorati e ispezionati.

>[!TIP]
>
>Le specifiche di esplorazione sono hardcoded e puoi semplicemente copiare e incollare il payload sottostante secondo le specifiche di connessione.

```json
"exploreSpec": {
  "name": "Resource",
  "type": "Resource",
  "requestSpec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object"
  },
  "responseSpec": {
    "$schema": "http: //json-schema.org/draft-07/schema#",
    "type": "object",
    "properties": {
      "format": {
        "type": "string"
      },
      "schema": {
        "type": "object",
        "properties": {
          "columns": {
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "name": {
                  "type": "string"
                },
                "type": {
                  "type": "string"
                }
              }
            }
          }
        }
      },
      "data": {
        "type": "array",
        "items": {
          "type": "object"
        }
      }
    }
  }
}
```

| Esplora le specifiche | Descrizione | Esempio |
| --- | --- | --- |
| `name` | Definisce il nome o l&#39;identificatore della specifica di esplorazione. | `Resource` |
| `type` | Definisce il tipo di specifica di esplorazione. | `Resource` |
| `requestSpec` | Contiene i parametri necessari per esplorare gli oggetti nella connessione. |
| `requestSpec.type` | Definisce il tipo di dati della specifica della richiesta. | `object` |
| `responseSpec` | Contiene i parametri che definiscono il formato del messaggio di risposta restituito rispetto a una chiamata di esplorazione. |
| `responseSpec.type` | Definisce il tipo di dati della specifica di risposta. | `object` |
| `responseSpec.properties` | Contiene informazioni sulla formattazione del messaggio di risposta. |
| `responseSpec.properties.format` | Definisce la formattazione dello schema di risposta. | `object` |
| `responseSpec.properties.format.type` | Definisce il tipo di dati delle proprietà. | `string` |
| `responseSpec.schema` | Contiene informazioni sulla formattazione dello schema di risposta. |
| `responseSpec.schema.type` | Definisce il tipo di dati dello schema. | `object` |
| `responseSpec.schema.properties` | Contiene informazioni sulle colonne, il tipo e gli elementi contenuti in uno schema. |
| `responseSpec.schema.properties.columns.items.properties.name` | Visualizza il nome del file. |
| `responseSpec.schema.properties.columns.items.properties.name.type` | Definisce il tipo di dati del nome del file. | `string` |

{style="table-layout:auto"}

## Passaggi successivi

Dopo aver popolato le specifiche di esplorazione, è possibile creare una specifica di connessione completa utilizzando l&#39;API [!DNL Flow Service]. Per ulteriori informazioni, consulta la [guida dell&#39;API Self-Serve Sources (Batch SDK)](../api/api-overview.md).
