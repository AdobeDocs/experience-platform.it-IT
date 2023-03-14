---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Nozioni di base sulle API di Experience Platform
description: Questo documento fornisce una breve panoramica di alcune delle tecnologie e sintassi sottostanti coinvolte con le API Experience Platform.
exl-id: cd69ba48-f78c-4da5-80d1-efab5f508756
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 2%

---

# Nozioni di base sulle API di Experience Platform

Le API di Adobe Experience Platform utilizzano diverse tecnologie e sintassi di base importanti da comprendere per gestire in modo efficace i file JSON [!DNL Platform] risorse. Questo documento fornisce una breve panoramica di queste tecnologie, nonché collegamenti verso la documentazione esterna per ulteriori informazioni.

## Puntatore JSON {#json-pointer}

Il puntatore JSON è una sintassi stringa standardizzata ([RFC 6901](https://tools.ietf.org/html/rfc6901)) per identificare valori specifici nei documenti JSON. Un puntatore JSON è una stringa di token separati da `/` caratteri, che specificano chiavi di oggetto o indici di matrice e i token possono essere una stringa o un numero. Le stringhe del puntatore JSON vengono utilizzate in molte operazioni PATCH per [!DNL Platform] come descritto più avanti in questo documento. Per ulteriori informazioni sul puntatore JSON, consulta [Panoramica del puntatore JSON](https://rapidjson.org/md_doc_pointer.html).

### Esempio di oggetto schema JSON

Il JSON seguente rappresenta uno schema XDM semplificato i cui campi possono essere referenziati utilizzando stringhe puntatore JSON. Tutti i campi aggiunti utilizzando gruppi di campi schema personalizzati (ad esempio `loyaltyLevel`) hanno namespace in una `_{TENANT_ID}` , mentre i campi che sono stati aggiunti utilizzando i gruppi di campi principali (come `fullName`) non lo sono.

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
| `"/properties/person/properties/name/properties/fullName"` | (Restituisce un riferimento al `fullName` , fornito da un gruppo di campi di base.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel"` | (Restituisce un riferimento al `loyaltyLevel` , fornito da un gruppo di campi personalizzato.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>Quando si tratta di `xdm:sourceProperty` e `xdm:destinationProperty` attributi di [!DNL Experience Data Model] Descrittori (XDM), qualsiasi `properties` le chiavi devono essere **escluso** dalla stringa del puntatore JSON. Consulta la [!DNL Schema Registry] Guida secondaria per gli sviluppatori API su [descrittori](../xdm/api/descriptors.md) per ulteriori informazioni.

## Patch JSON {#json-patch}

Esistono molte operazioni PATCH per [!DNL Platform] API che accettano oggetti Patch JSON per i payload di richieste. La patch JSON è un formato standardizzato ([RFC 6902](https://tools.ietf.org/html/rfc6902)) per descrivere le modifiche apportate a un documento JSON. Consente di definire aggiornamenti parziali di JSON senza dover inviare l’intero documento nel corpo di una richiesta.

### Esempio di oggetto Patch JSON

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`: tipo di operazione patch. Sebbene la patch JSON supporti diversi tipi di operazioni, non tutte le operazioni PATCH in [!DNL Platform] Le API sono compatibili con ogni tipo di operazione. I tipi di operazioni disponibili sono:
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`: parte della struttura JSON da aggiornare, identificata tramite [Puntatore JSON](#json-pointer) notazione.

A seconda del tipo di operazione indicato in `op`, l’oggetto Patch JSON potrebbe richiedere proprietà aggiuntive. Per ulteriori informazioni sulle diverse operazioni Patch JSON e sulla sintassi richiesta, consulta [Documentazione delle patch JSON](https://datatracker.ietf.org/doc/html/rfc6902).

## Schema JSON {#json-schema}

Lo schema JSON è un formato utilizzato per descrivere e convalidare la struttura dei dati JSON. [Experience Data Model (XDM)](../xdm/home.md) sfrutta le funzionalità dello schema JSON per applicare vincoli alla struttura e al formato dei dati acquisiti sull’esperienza del cliente. Per ulteriori informazioni sullo schema JSON, consulta [documentazione ufficiale](https://json-schema.org/).

## Passaggi successivi

In questo documento sono state introdotte alcune delle tecnologie e delle sintassi coinvolte nella gestione delle risorse basate su JSON per [!DNL Experience Platform]. Consulta la sezione [guida introduttiva](api-guide.md) per ulteriori informazioni sull’utilizzo delle API di Platform, incluse le best practice. Per le risposte alle domande frequenti, fare riferimento a [Guida alla risoluzione dei problemi di Platform](troubleshooting.md).
