---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: ' Principi di base delle API Adobi Experience Platform'
topic: getting started
translation-type: tm+mt
source-git-commit: 2e5668a8b1d5fb831188fbd4e453b9f4aa7474df
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 2%

---


#  Principi di base delle API Adobi Experience Platform

 API di Adobe Experience Platform utilizzano diverse tecnologie e sintassi di base importanti per gestire efficacemente le risorse basate su JSON [!DNL Platform] . Il presente documento fornisce una breve panoramica di queste tecnologie e collegamenti alla documentazione esterna per ulteriori informazioni.

## Puntatore JSON {#json-pointer}

JSON Pointer è una sintassi di stringa standard ([RFC 6901](https://tools.ietf.org/html/rfc6901)) per identificare valori specifici all&#39;interno dei documenti JSON. Un puntatore JSON è una stringa di token separati da `/` caratteri, che specificano le chiavi oggetto o gli indici di array e i token possono essere una stringa o un numero. Le stringhe Puntatore JSON vengono utilizzate in molte operazioni PATCH per [!DNL Platform] le API, come descritto più avanti in questo documento. Per maggiori informazioni su JSON Pointer, consulta la documentazione [sulla panoramica di](https://rapidjson.org/md_doc_pointer.html)JSON Pointer.

### Esempio di oggetto schema JSON

```json
{
    "type": "object",
    "title": "Loyalty Member Details",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Loyalty Program Mixin.",
    "definitions": {
        "loyalty": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "loyaltyId": {
                            "title": "Loyalty Identifier",
                            "type": "string",
                            "description": "Loyalty Identifier.",
                            "meta:xdmType": "string"
                        },
                        "loyaltyLevel": {
                            "title": "Loyalty Level",
                            "description": "The current loyalty program level to which the individual member belongs.",
                            "type": "string",
                            "enum": [
                                "platinum",
                                "gold",
                                "silver",
                                "bronze"
                            ],
                            "meta:enum": {
                                "platinum": "Platinum",
                                "gold": "Gold",
                                "silver": "Silver",
                                "bronze": "Bronze"
                            },
                            "meta:xdmType": "string"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    }
}
```

### Esempio di puntatori JSON basati sull&#39;oggetto schema

| Puntatore JSON | Risolve a |
|--- | ---|
| `"/title"` | &quot;Dettagli membro fedeltà&quot; |
| `"/definitions/loyalty"` | (Restituisce il contenuto dell&#39; `loyalty` oggetto) |
| `"/definitions/loyalty/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/definitions/loyalty/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!Nota]
>Quando si utilizzano gli `xdm:sourceProperty` attributi e `xdm:destinationProperty` gli attributi dei descrittori [!DNL Experience Data Model] (XDM), qualsiasi `properties` chiave deve essere **esclusa** dalla stringa Puntatore JSON. Per ulteriori informazioni, consulta la Guida secondaria per gli sviluppatori di API del Registro di sistema dello schema sui [descrittori](../xdm/api/descriptors.md) .

## Patch JSON

Esistono molte operazioni PATCH per [!DNL Platform] le API che accettano oggetti JSON Patch per i payload di richiesta. La patch JSON è un formato standard ([RFC 6902](https://tools.ietf.org/html/rfc6902)) per descrivere le modifiche a un documento JSON. Consente di definire aggiornamenti parziali a JSON senza dover inviare l’intero documento in un corpo della richiesta.

### Esempio di oggetto patch JSON

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`: Tipo di operazione della patch. Sebbene la patch JSON supporti diversi tipi di operazioni, non tutte le operazioni PATCH nelle [!DNL Platform] API sono compatibili con ogni tipo di operazione. I tipi di operazioni disponibili sono:
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`: La parte della struttura JSON da aggiornare, identificata utilizzando la notazione [JSON Pointer](#json-pointer) .

A seconda del tipo di operazione indicato in `op`, l&#39;oggetto Patch JSON potrebbe richiedere proprietà aggiuntive. Per ulteriori informazioni sulle diverse operazioni di patch JSON e sulla relativa sintassi richiesta, consulta la documentazione [relativa alla patch](http://jsonpatch.com/)JSON.

## Schema JSON

Lo schema JSON è un formato utilizzato per descrivere e convalidare la struttura dei dati JSON. [Experience Data Model (XDM)](../xdm/home.md) sfrutta le funzionalità dello schema JSON per applicare vincoli alla struttura e al formato dei dati esperienza cliente acquisiti. Per ulteriori informazioni sullo schema JSON, consulta la documentazione [](https://json-schema.org/)ufficiale.

## Passaggi successivi

In questo documento sono state introdotte alcune tecnologie e sintassi relative alla gestione delle risorse basate su JSON per [!DNL Experience Platform]. Per ulteriori informazioni sull&#39;utilizzo delle [!DNL Platform] API, comprese le procedure ottimali e le risposte alle domande frequenti, consultare la guida [alla risoluzione dei problemi di](troubleshooting.md)Platform.