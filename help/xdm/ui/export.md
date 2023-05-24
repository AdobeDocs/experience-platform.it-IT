---
solution: Experience Platform
title: Esportare gli schemi XDM nell’interfaccia utente
description: Scopri come esportare uno schema esistente in una sandbox o organizzazione diversa nell’interfaccia utente di Adobe Experience Platform.
type: Tutorial
exl-id: c467666d-55bc-4134-b8f4-7758d49c4786
source-git-commit: bed627b945c5392858bcc2dce18e9bbabe8bcdb6
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# Esportare gli schemi XDM nell’interfaccia utente

Tutte le risorse all’interno della Libreria schemi sono contenute in una sandbox specifica all’interno di un’organizzazione. In alcuni casi, potrebbe essere utile condividere risorse Experience Data Model (XDM) tra sandbox e organizzazioni.

Per soddisfare questa esigenza, [!UICONTROL Schemi] Nell’interfaccia utente di Adobe Experience Platform, Workspace consente di generare un payload di esportazione per qualsiasi schema in nella Libreria schemi. Questo payload può quindi essere utilizzato in una chiamata all’API Schema Registry per importare lo schema (e tutte le risorse dipendenti) in una sandbox e un’organizzazione di destinazione.

>[!NOTE]
>
>È inoltre possibile utilizzare l’API Schema Registry per esportare altre risorse oltre agli schemi, tra cui classi, gruppi di campi di schema e tipi di dati. Consulta la [guida dell’endpoint di esportazione](../api/export.md) per ulteriori informazioni.

## Prerequisiti

Anche se l’interfaccia utente di Platform consente di esportare risorse XDM, è necessario utilizzare l’API Schema Registry per importare tali risorse in altre sandbox o organizzazioni per completare il flusso di lavoro. Consulta la guida su [guida introduttiva all’API Schema Registry](../api/getting-started.md) per informazioni importanti sulle intestazioni di autenticazione richieste prima di seguire questa guida.

## Generare un payload di esportazione {#generate-export-payload}

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Schemi]** nel menu di navigazione a sinistra. All&#39;interno del [!UICONTROL Schemi] nell’area di lavoro, seleziona la riga dello schema da esportare per visualizzare i dettagli dello schema nella barra laterale a destra.

>[!TIP]
>
>Consulta la guida su [esplorazione delle risorse XDM](./explore.md) per informazioni dettagliate su come trovare la risorsa XDM che stai cercando.

Quindi, seleziona la **[!UICONTROL Copia JSON]** icona (![Copia icona](../images/ui/export/icon.png)) dalle opzioni disponibili.

![L’area di lavoro Schemi con una riga di schema e [!UICONTROL Copia in JSON] evidenziato.](../images/ui/export/copy-json.png)

Questo copia un payload JSON negli Appunti, generato in base alla struttura dello schema. Per il &quot;[!DNL Loyalty Members]&quot; mostrato sopra, viene generato il seguente JSON:

```json
[
  {
    "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
    "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.mixins.9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
    "meta:resourceType": "mixins",
    "version": "1.0",
    "title": "Loyalty details",
    "type": "object",
    "description": "",
    "definitions": {
      "customFields": {
        "type": "object",
        "properties": {
          "_<XDM_TENANTID_PLACEHOLDER>": {
            "type": "object",
            "properties": {
              "loyalty": {
                "title": "Loyalty",
                "description": "",
                "type": "object",
                "isRequired": false,
                "required": [
                  
                ],
                "properties": {
                  "loyaltyId": {
                    "title": "Loyalty ID",
                    "description": "",
                    "type": "string",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "meta:xdmType": "string"
                  },
                  "memberSince": {
                    "title": "Member Since",
                    "description": "",
                    "type": "string",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "format": "date",
                    "meta:xdmType": "date"
                  },
                  "points": {
                    "title": "Points",
                    "description": "",
                    "type": "integer",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "meta:xdmType": "int"
                  },
                  "loyaltyLevel": {
                    "title": "Loyalty Level",
                    "description": "",
                    "type": "string",
                    "isRequired": false,
                    "required": [
                      
                    ],
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
            "meta:xdmType": "object"
          }
        },
        "meta:xdmType": "object"
      }
    },
    "allOf": [
      {
        "$ref": "#/definitions/customFields",
        "type": "object",
        "meta:xdmType": "object"
      }
    ],
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:intendedToExtend": [
      
    ],
    "meta:xdmType": "object",
    "meta:sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
    "meta:sandboxType": "production"
  },
  {
    "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/schemas/1e5a739ded8fd1d766a0e06e881a38031874dddd1c7020ad",
    "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.schemas.1e5a739ded8fd1d766a0e06e881a38031874dddd1c7020ad",
    "meta:resourceType": "schemas",
    "version": "1.4",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Describes customers who are members of a loyalty program.",
    "allOf": [
      {
        "$ref": "https://ns.adobe.com/xdm/context/profile",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/xdm/mixins/profile-consents",
        "type": "object",
        "meta:xdmType": "object"
      }
    ],
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
      "https://ns.adobe.com/xdm/context/profile-person-details",
      "https://ns.adobe.com/xdm/context/profile-personal-details",
      "https://ns.adobe.com/xdm/common/auditable",
      "https://ns.adobe.com/xdm/data/record",
      "https://ns.adobe.com/xdm/context/profile",
      "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
      "https://ns.adobe.com/xdm/mixins/profile-consents"
    ],
    "meta:xdmType": "object",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
    "meta:sandboxType": "production",
    "meta:immutableTags": [
      
    ]
  }
]
```

Il payload assume la forma di un array; ogni elemento dell’array è un oggetto che rappresenta una risorsa XDM personalizzata da esportare. Nell’esempio precedente, l’opzione &quot;[!DNL Loyalty details]&quot; gruppo di campi personalizzato e &quot;[!DNL Loyalty Members]&quot;sono inclusi. Tutte le risorse core utilizzate dallo schema non vengono incluse nell’esportazione, in quanto sono disponibili in tutte le sandbox e le organizzazioni.

Ogni istanza dell’ID tenant dell’organizzazione viene visualizzata come `<XDM_TENANTID_PLACEHOLDER>` nel payload. Questi segnaposto verranno sostituiti automaticamente con il valore ID tenant appropriato a seconda di dove importi lo schema nel passaggio successivo.

## Importare la risorsa utilizzando l’API

Dopo aver copiato il JSON di esportazione per lo schema, puoi utilizzarlo come payload per una richiesta POST al `/rpc/import` nell’API Schema Registry. Consulta la [importa guida dell’endpoint](../api/import.md) per informazioni dettagliate su come configurare la chiamata per inviare lo schema all’organizzazione e alla sandbox desiderate.

## Passaggi successivi

Seguendo questa guida, hai esportato correttamente uno schema XDM in un’organizzazione o sandbox diversa. Per ulteriori informazioni sulle funzionalità di [!UICONTROL Schemi] interfaccia utente, fare riferimento a [[!UICONTROL Schemi] Panoramica dell’interfaccia utente](./overview.md).
