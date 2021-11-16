---
keywords: Experience Platform;home;argomenti popolari;sorgenti;connettori;connettori sorgente;origini sdk;sdk;SDK
title: Configurare l’esplorazione delle specifiche per l’SDK di Origini
topic-legacy: overview
description: Questo documento fornisce una panoramica delle configurazioni da preparare per utilizzare l'SDK di Origini.
hide: true
hidefromtoc: true
source-git-commit: d98cf404fd1a4d150f202154aba87b0089418957
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 2%

---


# Configurare l’esplorazione delle specifiche per l’SDK di Origini

Le specifiche Esplora definiscono i parametri necessari per l&#39;esplorazione e l&#39;ispezione degli oggetti contenuti nella sorgente. Le specifiche Esplora definiscono anche il formato di risposta restituito quando gli oggetti vengono esplorati ed ispezionati.

>[!TIP]
>
>Le specifiche di Esplora sono codificate e puoi semplicemente copiare e incollare il payload riportato di seguito nelle specifiche di connessione.

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

| Esplorare le specifiche | Descrizione | Esempio |
| --- | --- | --- |
| `name` | Definisce il nome o l&#39;identificatore della specifica di esplorazione. | `Resource` |
| `type` | Definisce il tipo di specifica di esplorazione. | `Resource` |
| `requestSpec` | Contiene i parametri necessari per esplorare gli oggetti nella connessione. |
| `requestSpec.type` | Definisce il tipo di dati della specifica della richiesta. | `object` |
| `responseSpec` | Contiene i parametri che definiscono il formato del messaggio di risposta restituito rispetto a una chiamata di esplorazione. |
| `responseSpec.type` | Definisce il tipo di dati della specifica di risposta. | `object` |
| `responseSpec.properties` | Contiene informazioni relative alla formattazione del messaggio di risposta. |
| `responseSpec.properties.format` | Definisce la formattazione dello schema di risposta. | `object` |
| `responseSpec.properties.format.type` | Definisce il tipo di dati delle proprietà. | `string` |
| `responseSpec.schema` | Contiene informazioni relative alla formattazione dello schema di risposta. |
| `responseSpec.schema.type` | Definisce il tipo di dati dello schema. | `object` |
| `responseSpec.schema.properties` | Contiene informazioni sulle colonne, sul tipo e sugli elementi contenuti in uno schema. |
| `responseSpec.schema.properties.columns.items.properties.name` | Visualizza il nome del file. |
| `responseSpec.schema.properties.columns.items.properties.name.type` | Definisce il tipo di dati del nome del file. | `string` |

{style=&quot;table-layout:auto&quot;}

## Passaggi successivi

Con le specifiche di esplorazione compilate, è possibile procedere alla creazione di una specifica di connessione completa utilizzando [!DNL Flow Service] API. Consulta la sezione [[!DNL Sources SDK] Guida all’API](../api/api-overview.md) per ulteriori informazioni.