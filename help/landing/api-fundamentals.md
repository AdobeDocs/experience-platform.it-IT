---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Nozioni di base sulle API di Experience Platform
description: Questo documento fornisce una breve panoramica di alcune delle tecnologie e sintassi sottostanti coinvolte con le API Experience Platform.
exl-id: cd69ba48-f78c-4da5-80d1-efab5f508756
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---

# Nozioni di base sulle API di Experience Platform

Le API Adobe Experience Platform utilizzano diverse tecnologie e sintassi di base importanti da comprendere per gestire in modo efficace le risorse [!DNL Platform] basate su JSON. Questo documento fornisce una breve panoramica di queste tecnologie, nonché collegamenti verso la documentazione esterna per ulteriori informazioni.

## Puntatore JSON {#json-pointer}

Il puntatore JSON è una sintassi stringa standardizzata ([RFC 6901](https://tools.ietf.org/html/rfc6901)) per l&#39;identificazione di valori specifici nei documenti JSON. Un puntatore JSON è una stringa di token separati da `/` caratteri che specificano le chiavi di oggetto o gli indici di matrice e i token possono essere una stringa o un numero. Le stringhe di puntatore JSON vengono utilizzate in molte operazioni PATCH per le API [!DNL Platform], come descritto più avanti in questo documento. Per ulteriori informazioni sul puntatore JSON, consulta la [documentazione Panoramica puntatore JSON](https://rapidjson.org/md_doc_pointer.html).

### Esempio di oggetto schema JSON

Il JSON seguente rappresenta uno schema XDM semplificato i cui campi possono essere referenziati utilizzando stringhe puntatore JSON. Si noti che tutti i campi aggiunti utilizzando gruppi di campi dello schema personalizzati (ad esempio `loyaltyLevel`) hanno lo spazio dei nomi sotto un oggetto `_{TENANT_ID}`, mentre i campi aggiunti utilizzando gruppi di campi di base (ad esempio `fullName`) non lo sono.

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

### Esempio di puntatori JSON basati su un oggetto schema

| Puntatore JSON | Risolve in |
| --- | --- |
| `"/title"` | `"Example schema"` |
| `"/properties/person/properties/name/properties/fullName"` | (Restituisce un riferimento al campo `fullName`, fornito da un gruppo di campi di base.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel"` | (Restituisce un riferimento al campo `loyaltyLevel`, fornito da un gruppo di campi personalizzato). |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>Quando si tratta degli attributi `xdm:sourceProperty` e `xdm:destinationProperty` dei descrittori [!DNL Experience Data Model] (XDM), le chiavi `properties` devono essere **escluse** dalla stringa del puntatore JSON. Per ulteriori informazioni, consulta la guida per gli sviluppatori API [!DNL Schema Registry] nella sezione [descrittori](../xdm/api/descriptors.md).

## Patch JSON {#json-patch}

Molte operazioni PATCH per le API [!DNL Platform] accettano oggetti Patch JSON per i payload di richiesta. La patch JSON è un formato standardizzato ([RFC 6902](https://tools.ietf.org/html/rfc6902)) per la descrizione delle modifiche apportate a un documento JSON. Consente di definire aggiornamenti parziali di JSON senza dover inviare l’intero documento nel corpo di una richiesta.

### Esempio di oggetto Patch JSON

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`: tipo di operazione patch. Sebbene la patch JSON supporti diversi tipi di operazioni, non tutte le operazioni PATCH nelle API [!DNL Platform] sono compatibili con ogni tipo di operazione. I tipi di operazioni disponibili sono:
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`: parte della struttura JSON da aggiornare, identificata con la notazione [JSON Pointer](#json-pointer).

A seconda del tipo di operazione indicato in `op`, l&#39;oggetto Patch JSON potrebbe richiedere proprietà aggiuntive. Per ulteriori informazioni sulle diverse operazioni Patch JSON e sulla sintassi richiesta, consulta la [documentazione Patch JSON](https://datatracker.ietf.org/doc/html/rfc6902).

## Schema JSON {#json-schema}

Lo schema JSON è un formato utilizzato per descrivere e convalidare la struttura dei dati JSON. [Experience Data Model (XDM)](../xdm/home.md) sfrutta le funzionalità dello schema JSON per applicare vincoli alla struttura e al formato dei dati acquisiti sull&#39;esperienza del cliente. Per ulteriori informazioni sullo schema JSON, consulta la [documentazione ufficiale](https://json-schema.org/).

## Passaggi successivi

In questo documento sono state introdotte alcune delle tecnologie e sintassi necessarie per la gestione delle risorse basate su JSON per [!DNL Experience Platform]. Per ulteriori informazioni sull&#39;utilizzo delle API di Platform, incluse le best practice, consulta la [guida introduttiva](api-guide.md). Per le risposte alle domande frequenti, fare riferimento alla [Guida alla risoluzione dei problemi di Platform](troubleshooting.md).
