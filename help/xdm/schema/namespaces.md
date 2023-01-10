---
keywords: Experience Platform;home;argomenti popolari;schema;schema;xdm;modello dati esperienza;spazio dei nomi;spazi dei nomi;modalità compatibilità;fisso;
solution: Experience Platform
title: Namespace in Experience Data Model (XDM)
description: Scopri come lo spazio dei nomi in Experience Data Model (XDM) ti consente di estendere gli schemi e impedire conflitti di campo quando diversi componenti dello schema vengono riuniti.
exl-id: b351dfaf-5219-4750-a7a9-cf4689a5b736
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 1%

---

# Namespace in Experience Data Model (XDM)

A tutti i campi negli schemi Experience Data Model (XDM) è associato un namespace. Questi namespace ti consentono di estendere gli schemi ed evitare conflitti di campi man mano che diversi componenti dello schema vengono riuniti. Questo documento fornisce una panoramica dei namespace in XDM e del modo in cui vengono rappresentati in [API del Registro di sistema dello schema](../api/overview.md).

Lo spazio dei nomi consente di definire un campo in un namespace come qualcosa di diverso dallo stesso campo in un namespace diverso. In pratica, lo spazio dei nomi di un campo indica chi ha creato il campo (ad Adobe XDM standard), un fornitore o l’organizzazione).

Ad esempio, considera uno schema XDM che utilizza il [[!UICONTROL Dati di contatto personali] gruppo di campi](../field-groups/profile/demographic-details.md), che ha una `mobilePhone` del campo presente nel `xdm` spazio dei nomi. Nello stesso schema, puoi anche creare un `mobilePhone` in un altro spazio dei nomi (il tuo [ID tenant](../api/getting-started.md#know-your-tenant_id)). Entrambi questi campi possono coesistere e avere significati o vincoli sottostanti diversi.

## Sintassi di namespace

Le sezioni seguenti mostrano come gli spazi dei nomi vengono assegnati nella sintassi XDM.

### XDM standard {#standard}

La sintassi XDM standard fornisce informazioni approfondite sulla rappresentazione dei namespace negli schemi (tra cui [come vengono tradotte in Adobe Experience Platform](#compatibility)).

Utilizzo standard di XDM [JSON LD](https://json-ld.org/) sintassi per assegnare spazi dei nomi ai campi. Questo spazio dei nomi si presenta sotto forma di URI (ad esempio `https://ns.adobe.com/xdm` per `xdm` namespace) o come prefisso abbreviato configurato nel `@context` attributo di uno schema.

Di seguito è riportato uno schema di esempio per un prodotto con sintassi XDM standard. Ad eccezione di `@id` (l&#39;identificatore univoco definito dalla specifica JSON-LD), ogni campo in `properties` inizia con uno spazio dei nomi e termina con il nome del campo. Se si utilizza un prefisso abbreviato definito in `@context`, lo spazio dei nomi e il nome del campo sono separati da due punti (`:`). Se non si utilizza un prefisso , lo spazio dei nomi e il nome del campo sono separati da una barra (`/`).

```json
{
  "$id": "https://ns.adobe.com/xdm/schemas/mySchema",
  "title": "Product",
  "description": "Represents the definition of a Project",
  "@context": {
    "xdm": "https://ns.adobe.com/xdm",
    "repo": "http://ns.adobe.com/adobecloud/core/1.0/",
    "schema": "http://schema.org",
    "tenantId": "https://ns.adobe.com/tenantId"
  },
  "properties": {
    "@id": {
      "type": "string"
    },
    "xdm:sku": {
      "type": "string"
    },
    "xdm:name": {
      "type": "string"
    },
    "repo:createdDate": {
      "type": "string",
      "format": "datetime"
    },
    "https://ns.adobe.com/xdm/channels/application": {
      "type": "string"
    },
    "schema:latitude": {
      "type": "number"
    },
    "https://ns.adobe.com/vendorA/product/stockNumber": {
      "type": "string"
    },
    "tenantId:internalSku": {
      "type": "number"
    }
  }
}
```

| Proprietà | Descrizione |
| --- | --- |
| `@context` | Un oggetto che definisce i prefissi abbreviati che possono essere utilizzati al posto di un URI dello spazio dei nomi completo in `properties`. |
| `@id` | Un identificatore univoco per il record definito dalla [Specifiche JSON-LD](https://json-ld.org/spec/latest/json-ld/#node-identifiers). |
| `xdm:sku` | Esempio di campo che utilizza un prefisso abbreviato per indicare uno spazio dei nomi. In questo caso, `xdm` è lo spazio dei nomi (`https://ns.adobe.com/xdm`) e `sku` è il nome del campo. |
| `https://ns.adobe.com/xdm/channels/application` | Esempio di campo che utilizza l’URI dello spazio dei nomi completo. In questo caso, `https://ns.adobe.com/xdm/channels` è lo spazio dei nomi e `application` è il nome del campo. |
| `https://ns.adobe.com/vendorA/product/stockNumber` | I campi forniti dalle risorse fornitore utilizzano spazi dei nomi univoci. In questo esempio, `https://ns.adobe.com/vendorA/product` è lo spazio dei nomi del fornitore e `stockNumber` è il nome del campo. |
| `tenantId:internalSku` | I campi definiti dall’organizzazione utilizzano l’ID tenant univoco come namespace. In questo esempio, `tenantId` è lo spazio dei nomi del tenant (`https://ns.adobe.com/tenantId`) e `internalSku` è il nome del campo. |

{style=&quot;table-layout:auto&quot;}

### Modalità di compatibilità {#compatibility}

In Adobe Experience Platform, gli schemi XDM sono rappresentati in [Modalità di compatibilità](../api/appendix.md#compatibility) sintassi che non utilizza la sintassi JSON-LD per rappresentare i namespace. Platform converte invece lo spazio dei nomi in un campo principale (a partire da un trattino basso) e nidifica i campi al suo interno.

Ad esempio, XDM standard `repo:createdDate` viene convertito in `_repo.createdDate` e appariranno nella seguente struttura in Modalità compatibilità:

```json
"_repo": {
  "type": "object",
  "properties": {
    "createdDate": {
      "type": "string",
      "format": "datetime"
    }
  }
}
```

Campi che utilizzano `xdm` lo spazio dei nomi viene visualizzato come campi principali in `properties` e rilascia la `xdm:` prefisso che apparirà in [sintassi XDM standard](#standard). Ad esempio: `xdm:sku` è semplicemente elencato come `sku` invece.

Il seguente JSON rappresenta il modo in cui l’esempio di sintassi XDM standard mostrato sopra viene convertito in Modalità compatibilità.

```json
{
  "$id": "https://ns.adobe.com/xdm/schemas/mySchema",
  "title": "Product",
  "description": "Represents the definition of a Project",
  "properties": {
    "_id": {
      "type": "string"
    },
    "sku": {
      "type": "string"
    },
    "name": {
      "type": "string"
    },
    "_repo": {
      "type": "object",
      "properties": {
        "createdDate": {
          "type": "string",
          "format": "datetime"
        }
      }
    },
    "_channels": {
      "type": "object",
      "properties": {
        "application": {
          "type": "string"
        }
      }
    },
    "_schema": {
      "type": "object",
      "properties": {
        "application": {
          "type": "string"
        }
      }
    },
    "_vendorA": {
      "type": "object",
      "properties": {
        "product": {
          "type": "object",
          "properties": {
            "stockNumber": {
              "type": "string"
            }
          }
        }
      }
    },
    "_tenantId": {
      "type": "object",
      "properties": {
        "internalSku": {
          "type": "number"
        }
      }
    }
  }
}
```

## Passaggi successivi

Questa guida fornisce una panoramica dei namespace XDM e del modo in cui vengono rappresentati in JSON. Per ulteriori informazioni su come configurare gli schemi XDM utilizzando l’API, consulta la sezione [Guida all’API del registro dello schema](../api/overview.md).
