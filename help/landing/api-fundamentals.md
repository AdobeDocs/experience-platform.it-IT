---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Nozioni di base sulle API Adobe Experience Platform
topic: getting started
translation-type: tm+mt
source-git-commit: fac4b3d02a6e58a9d2c298f9b849fa7345e4fa93
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 2%

---


# Nozioni di base sulle API Adobe Experience Platform

Le API di Adobe Experience Platform utilizzano diverse tecnologie e sintassi di base importanti per gestire efficacemente le risorse basate su JSON [!DNL Platform] . Il presente documento fornisce una breve panoramica di queste tecnologie e collegamenti alla documentazione esterna per ulteriori informazioni.

## Puntatore JSON {#json-pointer}

JSON Pointer è una sintassi di stringa standard ([RFC 6901](https://tools.ietf.org/html/rfc6901)) per identificare valori specifici all&#39;interno dei documenti JSON. Un puntatore JSON è una stringa di token separati da `/` caratteri, che specificano le chiavi oggetto o gli indici di array e i token possono essere una stringa o un numero. Le stringhe Puntatore JSON vengono utilizzate in molte operazioni PATCH per [!DNL Platform] le API, come descritto più avanti in questo documento. Per maggiori informazioni su JSON Pointer, consulta la documentazione [sulla panoramica di](https://rapidjson.org/md_doc_pointer.html)JSON Pointer.

### Esempio di oggetto schema JSON

Il seguente JSON rappresenta uno schema XDM semplificato i cui campi possono essere utilizzati come riferimento utilizzando le stringhe JSON Pointer. Tenere presente che tutti i campi aggiunti utilizzando mixin personalizzati (come `loyaltyLevel`ad esempio) sono delimitati da un `_{TENANT_ID}` oggetto, mentre i campi aggiunti utilizzando i mixin di base (come `fullName`) non lo sono.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/85a4bdaa168b01bf44384e049fbd3d2e9b2ffaca440d35b9",
  "meta:altId": "_{TENANT_ID}.schemas.85a4bdaa168b01bf44384e049fbd3d2e9b2ffaca440d35b9",
  "meta:resourceType": "schemas",
  "version": "1.0",
  "title": "Example schema",
  "type": "object",
  "description": "This is an example schema.",
  "properties": {
    "_{TENANT_ID}": {
      "type": "object",
      "properties": {
        "loyaltyLevel": {
          "title": "Loyalty Level",
          "description": "",
          "type": "string",
          "isRequired": false,
          "enum": [
            "platinum",
            "gold",
            "silver",
            "bronze"
          ]
        }
      }
    },
    "person": {
      "title": "Person",
      "description": "An individual actor, contact, or owner.",
      "type": "object",
      "properties": {
        "name": {
          "title": "Full name",
          "description": "The person's full name.",
          "type": "object",
          "properties": {
            "fullName": {
              "title": "Full name",
              "type": "string",
              "description": "The full name of the person, in writing order most commonly accepted in the language of the name.",
            },
            "suffix": {
              "title": "Suffix",
              "type": "string",
              "description": "A group of letters provided after a person's name to provide additional information. The `suffix` is used at the end of someones name. For example Jr., Sr., M.D., PhD, I, II, III, etc.",
            }
          },
          "meta:referencedFrom": "https://ns.adobe.com/xdm/context/person-name",
          "meta:xdmField": "xdm:name"
        }
      }
    }
  }
}
```

### Esempio di puntatori JSON basati sull&#39;oggetto schema

| Puntatore JSON | Risolve a |
| --- | --- |
| `"/title"` | `"Example schema"` |
| `"/properties/person/properties/name/properties/fullName"` | (Restituisce un riferimento al `fullName` campo, fornito da un mixin di base.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel"` | (Restituisce un riferimento al `loyaltyLevel` campo, fornito da un mixin personalizzato.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>Quando si utilizzano gli `xdm:sourceProperty` attributi e `xdm:destinationProperty` gli attributi dei descrittori [!DNL Experience Data Model] (XDM), qualsiasi `properties` chiave deve essere **esclusa** dalla stringa Puntatore JSON. Per ulteriori informazioni, consulta la guida per gli sviluppatori di [!DNL Schema Registry] API in [descrittori](../xdm/api/descriptors.md) .

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

In questo documento sono state introdotte alcune tecnologie e sintassi relative alla gestione delle risorse basate su JSON per [!DNL Experience Platform]. Per ulteriori informazioni sull&#39;utilizzo delle [!DNL Platform] API, comprese le procedure ottimali e le risposte alle domande frequenti, consultate la guida alla risoluzione dei problemi della [piattaforma](troubleshooting.md).