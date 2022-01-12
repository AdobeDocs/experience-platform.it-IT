---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Experience Platform di base API
topic-legacy: getting started
description: Questo documento fornisce una breve panoramica di alcune tecnologie e sintassi sottostanti coinvolte con le API di Experience Platform.
exl-id: cd69ba48-f78c-4da5-80d1-efab5f508756
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 2%

---

# Experience Platform di base API

Le API di Adobe Experience Platform utilizzano diverse tecnologie e sintassi di base importanti da comprendere per gestire in modo efficace i contenuti basati su JSON [!DNL Platform] risorse. Questo documento fornisce una breve panoramica di queste tecnologie e collegamenti alla documentazione esterna per ulteriori informazioni.

## Puntatore JSON {#json-pointer}

JSON Pointer è una sintassi di stringa standardizzata ([RFC 6901](https://tools.ietf.org/html/rfc6901)) per identificare valori specifici all’interno di documenti JSON. Un puntatore JSON è una stringa di token separati da `/` caratteri che specificano le chiavi dell’oggetto o gli indici della matrice e i token possono essere una stringa o un numero. Le stringhe del puntatore JSON vengono utilizzate in molte operazioni PATCH per [!DNL Platform] API, come descritto più avanti in questo documento. Per ulteriori informazioni sul puntatore JSON, consulta [Documentazione generale sul puntatore JSON](https://rapidjson.org/md_doc_pointer.html).

### Esempio di oggetto schema JSON

Il seguente JSON rappresenta uno schema XDM semplificato ai cui campi può essere fatto riferimento utilizzando le stringhe JSON Pointer. Tieni presente che tutti i campi aggiunti utilizzando i gruppi di campi dello schema personalizzato, ad esempio `loyaltyLevel`) sono precedute da un namespace `_{TENANT_ID}` oggetto , mentre i campi che sono stati aggiunti utilizzando i gruppi di campi principali, ad esempio `fullName`) non lo sono.

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

### Esempio di puntatori JSON basati sull’oggetto schema

| Puntatore JSON | Risolve in |
| --- | --- |
| `"/title"` | `"Example schema"` |
| `"/properties/person/properties/name/properties/fullName"` | (Restituisce un riferimento a `fullName` campo , fornito da un gruppo di campi di base.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel"` | (Restituisce un riferimento a `loyaltyLevel` campo, fornito da un gruppo di campi personalizzato.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>Quando si tratta di `xdm:sourceProperty` e `xdm:destinationProperty` attributi [!DNL Experience Data Model] (XDM), eventuali descrittori `properties` le chiavi devono essere **esclusi** dalla stringa Puntatore JSON. Consulta la sezione [!DNL Schema Registry] Guida secondaria per sviluppatori API su [descrittori](../xdm/api/descriptors.md) per ulteriori informazioni.

## Patch JSON {#json-patch}

Sono disponibili numerose operazioni PATCH per [!DNL Platform] API che accettano oggetti patch JSON per i payload della richiesta. La patch JSON è un formato standard ([RFC 6902](https://tools.ietf.org/html/rfc6902)) per descrivere le modifiche apportate a un documento JSON. Ti consente di definire aggiornamenti parziali a JSON senza dover inviare l’intero documento nel corpo di una richiesta.

### Esempio di oggetto Patch JSON

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`: Tipo di operazione patch. Mentre la patch JSON supporta diversi tipi di operazioni, non tutte le operazioni PATCH in [!DNL Platform] Le API sono compatibili con ogni tipo di operazione. I tipi di operazioni disponibili sono:
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`: La parte della struttura JSON da aggiornare, identificata utilizzando [Puntatore JSON](#json-pointer) notazione.

A seconda del tipo di operazione indicato in `op`, l’oggetto Patch JSON potrebbe richiedere proprietà aggiuntive. Per ulteriori informazioni sulle diverse operazioni di patch JSON e la relativa sintassi richiesta, consulta la [Documentazione sulle patch JSON](https://datatracker.ietf.org/doc/html/rfc6902).

## Schema JSON {#json-schema}

Lo schema JSON è un formato utilizzato per descrivere e convalidare la struttura dei dati JSON. [Experience Data Model (XDM)](../xdm/home.md) sfrutta le funzionalità dello schema JSON per applicare vincoli alla struttura e al formato dei dati sulla customer experience acquisiti. Per ulteriori informazioni sullo schema JSON, consulta [documentazione ufficiale](https://json-schema.org/).

## Passaggi successivi

In questo documento sono state introdotte alcune delle tecnologie e delle sintassi necessarie per la gestione delle risorse basate su JSON per [!DNL Experience Platform]. Fai riferimento a [guida introduttiva](api-guide.md) per ulteriori informazioni sull’utilizzo delle API di Platform, incluse le best practice. Per le risposte alle domande frequenti, consulta la sezione [Guida alla risoluzione dei problemi di Platform](troubleshooting.md).
