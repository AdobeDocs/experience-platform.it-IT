---
keywords: ' Experience Platform;home;argomenti popolari'
solution: Experience Platform
title: Nozioni di base sulle API Adobe Experience Platform
topic: getting started
description: Questo documento fornisce una breve panoramica di alcune tecnologie e sintassi sottostanti coinvolte con  API di Experience Platform.
translation-type: tm+mt
source-git-commit: 5dad1fcc82707f6ee1bf75af6c10d34ff78ac311
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 1%

---


# Nozioni di base sulle API Adobe Experience Platform

Le API di Adobe Experience Platform utilizzano diverse tecnologie e sintassi di base importanti per gestire efficacemente le risorse [!DNL Platform] basate su JSON. Il presente documento fornisce una breve panoramica di queste tecnologie e collegamenti alla documentazione esterna per ulteriori informazioni.

## Puntatore JSON {#json-pointer}

JSON Pointer è una sintassi di stringa standard ([RFC 6901](https://tools.ietf.org/html/rfc6901)) per identificare valori specifici all&#39;interno dei documenti JSON. Un puntatore JSON è una stringa di token separati da `/` caratteri, che specificano le chiavi oggetto o gli indici di array e i token possono essere una stringa o un numero. Le stringhe Puntatore JSON vengono utilizzate in molte operazioni PATCH per le API [!DNL Platform], come descritto più avanti in questo documento. Per ulteriori informazioni su JSON Pointer, fare riferimento alla [JSON Pointer overview documentation](https://rapidjson.org/md_doc_pointer.html).

### Esempio di oggetto schema JSON

Il seguente JSON rappresenta uno schema XDM semplificato i cui campi possono essere utilizzati come riferimento utilizzando le stringhe JSON Pointer. Tenere presente che tutti i campi aggiunti utilizzando i mixin personalizzati (come `loyaltyLevel`) sono delimitati da un oggetto `_{TENANT_ID}`, mentre i campi aggiunti utilizzando i mixin di base (come `fullName`) non sono consentiti.

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
| `"/properties/person/properties/name/properties/fullName"` | (Restituisce un riferimento al campo `fullName`, fornito da un mixin di base.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel"` | (Restituisce un riferimento al campo `loyaltyLevel`, fornito da un mixin personalizzato.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>Quando si utilizzano gli attributi `xdm:sourceProperty` e `xdm:destinationProperty` dei descrittori [!DNL Experience Data Model] (XDM), tutte le chiavi `properties` devono essere **escluse** dalla stringa Puntatore JSON. Per ulteriori informazioni, consultate la guida per gli sviluppatori [!DNL Schema Registry] API nella sezione [descriptors](../xdm/api/descriptors.md).

## Patch JSON {#json-patch}

Esistono molte operazioni PATCH per le API [!DNL Platform] che accettano oggetti patch JSON per i payload di richiesta. La patch JSON è un formato standard ([RFC 6902](https://tools.ietf.org/html/rfc6902)) per descrivere le modifiche apportate a un documento JSON. Consente di definire aggiornamenti parziali a JSON senza dover inviare l’intero documento in un corpo della richiesta.

### Esempio di oggetto patch JSON

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`: Tipo di operazione della patch. Sebbene la patch JSON supporti diversi tipi di operazioni, non tutte le operazioni PATCH nelle API [!DNL Platform] sono compatibili con ogni tipo di operazione. I tipi di operazioni disponibili sono:
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`: La parte della struttura JSON da aggiornare, identificata utilizzando  [JSON ](#json-pointer) Pointernotation.

A seconda del tipo di operazione indicato in `op`, l&#39;oggetto Patch JSON potrebbe richiedere proprietà aggiuntive. Per ulteriori informazioni sulle diverse operazioni di patch JSON e sulla relativa sintassi richiesta, fare riferimento alla [documentazione relativa alla patch JSON](http://jsonpatch.com/).

## Schema JSON

Lo schema JSON è un formato utilizzato per descrivere e convalidare la struttura dei dati JSON. [Experience Data Model (XDM) ](../xdm/home.md) sfrutta le funzionalità dello schema JSON per applicare vincoli alla struttura e al formato dei dati esperienza cliente acquisiti. Per ulteriori informazioni sullo schema JSON, fare riferimento alla [documentazione ufficiale](https://json-schema.org/).

## Passaggi successivi

In questo documento sono state introdotte alcune tecnologie e sintassi per la gestione delle risorse basate su JSON per [!DNL Experience Platform]. Per ulteriori informazioni sull&#39;utilizzo delle [!DNL Platform] API, incluse le procedure ottimali e le risposte alle domande frequenti, consultare la [Guida alla risoluzione dei problemi della piattaforma](troubleshooting.md).