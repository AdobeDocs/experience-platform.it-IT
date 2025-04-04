---
keywords: Experience Platform;home;argomenti popolari;schema;schema;xdm;experience data model;namespace;namespace;modalità compatibilità;mista;
solution: Experience Platform
title: Namespace in Experience Data Model (XDM)
description: Scopri come lo spazio dei nomi in Experience Data Model (XDM) consente di estendere gli schemi e prevenire conflitti di campi quando diversi componenti dello schema vengono uniti.
exl-id: b351dfaf-5219-4750-a7a9-cf4689a5b736
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---

# Namespace in Experience Data Model (XDM)

>[!IMPORTANT]
>
>In XDM, lo spazio dei nomi (l’argomento di questa pagina) viene utilizzato per distinguere i campi in uno schema. Questo è diverso dal concetto di spazio dei nomi delle identità in Identity Service, in cui lo spazio dei nomi viene utilizzato per distinguere i valori di identità. Per ulteriori informazioni, consulta la documentazione sullo spazio dei nomi [ in Identity Service](../../identity-service/features/namespaces.md).

A tutti i campi degli schemi Experience Data Model (XDM) è associato uno spazio dei nomi. Questi spazi dei nomi ti consentono di estendere gli schemi ed evitare conflitti di campi in quanto diversi componenti dello schema vengono uniti. Questo documento fornisce una panoramica degli spazi dei nomi in XDM e di come sono rappresentati nell&#39;API [Schema Registry](../api/overview.md).

Lo spazio dei nomi consente di definire un campo in uno spazio dei nomi con un significato diverso rispetto allo stesso campo in uno spazio dei nomi diverso. In pratica, lo spazio dei nomi di un campo indica chi ha creato il campo, ad esempio XDM standard (Adobe), un fornitore o la tua organizzazione.

Consideriamo ad esempio uno schema XDM che utilizza il gruppo di campi [[!UICONTROL Dettagli contatto personali]](../field-groups/profile/demographic-details.md), che ha un campo `mobilePhone` standard esistente nello spazio dei nomi `xdm`. Nello stesso schema, puoi anche creare un campo `mobilePhone` separato in un altro spazio dei nomi (il tuo [ID tenant](../api/getting-started.md#know-your-tenant_id)). Entrambi questi campi possono coesistere pur avendo significati o vincoli sottostanti diversi.

## Sintassi namespace

Le sezioni seguenti mostrano come gli spazi dei nomi vengono assegnati nella sintassi XDM.

### XDM standard {#standard}

La sintassi XDM standard fornisce ad insight informazioni sul modo in cui gli spazi dei nomi vengono rappresentati negli schemi (incluso [come vengono tradotti in Adobe Experience Platform](#compatibility)).

XDM standard utilizza la sintassi [JSON-LD](https://www.w3.org/TR/json-ld11/#basic-concepts) per assegnare spazi dei nomi ai campi. Questo spazio dei nomi ha la forma di un URI (ad esempio `https://ns.adobe.com/xdm` per lo spazio dei nomi `xdm`) o di un prefisso abbreviato configurato nell&#39;attributo `@context` di uno schema.

Di seguito è riportato uno schema di esempio per un prodotto con sintassi XDM standard. Ad eccezione di `@id` (l&#39;identificatore univoco definito dalla specifica JSON-LD), ogni campo in `properties` inizia con uno spazio dei nomi e termina con il nome del campo. Se si utilizza un prefisso abbreviato definito in `@context`, lo spazio dei nomi e il nome del campo sono separati da due punti (`:`). Se non si utilizza un prefisso, lo spazio dei nomi e il nome del campo sono separati da una barra (`/`).

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
| `@context` | Oggetto che definisce i prefissi abbreviati che possono essere utilizzati al posto dell&#39;URI completo dello spazio dei nomi in `properties`. |
| `@id` | Identificatore univoco del record definito dalla specifica [JSON-LD](https://www.w3.org/TR/json-ld11/#node-identifiers). |
| `xdm:sku` | Esempio di un campo che utilizza un prefisso abbreviato per indicare uno spazio dei nomi. In questo caso, `xdm` è lo spazio dei nomi (`https://ns.adobe.com/xdm`) e `sku` è il nome del campo. |
| `https://ns.adobe.com/xdm/channels/application` | Esempio di campo che utilizza l’URI completo dello spazio dei nomi. In questo caso, `https://ns.adobe.com/xdm/channels` è lo spazio dei nomi e `application` è il nome del campo. |
| `https://ns.adobe.com/vendorA/product/stockNumber` | I campi forniti dalle risorse fornitore utilizzano spazi dei nomi univoci. In questo esempio, `https://ns.adobe.com/vendorA/product` è lo spazio dei nomi del fornitore e `stockNumber` è il nome del campo. |
| `tenantId:internalSku` | I campi definiti dalla tua organizzazione utilizzano l’ID tenant univoco come spazio dei nomi. In questo esempio, `tenantId` è lo spazio dei nomi del tenant (`https://ns.adobe.com/tenantId`) e `internalSku` è il nome del campo. |

{style="table-layout:auto"}

### Modalità di compatibilità {#compatibility}

In Adobe Experience Platform, gli schemi XDM sono rappresentati nella sintassi [Modalità di compatibilità](../api/appendix.md#compatibility), che non utilizza la sintassi JSON-LD per rappresentare gli spazi dei nomi. Al contrario, Experience Platform converte lo spazio dei nomi in un campo principale (partendo da un carattere di sottolineatura) e nidifica i campi al di sotto di esso.

Ad esempio, l&#39;XDM standard `repo:createdDate` è convertito in `_repo.createdDate` e verrà visualizzato nella seguente struttura in modalità di compatibilità:

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

I campi che utilizzano lo spazio dei nomi `xdm` vengono visualizzati come campi radice in `properties` e rilasciano il prefisso `xdm:` che apparirebbe nella [sintassi XDM standard](#standard). Ad esempio, `xdm:sku` è semplicemente elencato come `sku`.

Il seguente codice JSON rappresenta il modo in cui la sintassi XDM standard mostrata sopra viene tradotta in modalità di compatibilità.

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

Questa guida fornisce una panoramica degli spazi dei nomi XDM e del modo in cui vengono rappresentati in JSON. Per ulteriori informazioni su come configurare gli schemi XDM utilizzando l&#39;API, consulta la [Guida all&#39;API del registro degli schemi](../api/overview.md).
