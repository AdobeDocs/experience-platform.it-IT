---
solution: Experience Platform
title: Esportare schemi XDM nell’interfaccia utente
description: Scoprite come esportare uno schema esistente in una sandbox o in un’organizzazione IMS diversa nell’interfaccia utente di Adobe Experience Platform.
topic: user guide
type: Tutorial
translation-type: tm+mt
source-git-commit: 2d6e833db7cd79135e6da4c68c9dca8cbed09ce4
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 0%

---


# Esportare schemi XDM nell’interfaccia utente

Tutte le risorse all&#39;interno della Libreria schema sono contenute in una sandbox specifica all&#39;interno di un&#39;organizzazione IMS. In alcuni casi, potrebbe essere utile condividere le risorse Experience Data Model (XDM) tra sandbox e organizzazioni IMS.

Per rispondere a questa esigenza, l&#39;area di lavoro [!UICONTROL Schemas] nell&#39;interfaccia utente di Adobe Experience Platform consente di generare un payload di esportazione per qualsiasi schema all&#39;interno della Libreria schema. Questo payload può quindi essere utilizzato in una chiamata all&#39;API del Registro di sistema dello schema per importare lo schema (e tutte le risorse dipendenti) in una sandbox di destinazione e in un&#39;organizzazione IMS.

>[!NOTE]
>
>È inoltre possibile utilizzare l&#39;API del Registro di sistema dello schema per esportare altre risorse oltre agli schemi, incluse classi, mixin e tipi di dati. Per ulteriori informazioni, consulta la guida sugli endpoint [di esportazione/importazione](../api/export-import.md).

## Prerequisiti

Mentre l&#39;interfaccia utente della piattaforma consente di esportare risorse XDM, è necessario utilizzare l&#39;API del Registro di sistema dello schema per importare tali risorse in altre sandbox o organizzazioni IMS per completare il flusso di lavoro. Per informazioni importanti sulle intestazioni di autenticazione necessarie prima di seguire questa guida, fare riferimento alla guida [guida introduttiva all&#39;API del Registro di sistema dello schema](../api/getting-started.md).

## Generazione di un payload di esportazione

Nell&#39;interfaccia utente della piattaforma, selezionate **[!UICONTROL Schemas]** nel menu di navigazione a sinistra. Nell&#39;area di lavoro [!UICONTROL Schemas], individuare lo schema da esportare e aprirlo in [!DNL Schema Editor].

>[!TIP]
>
>Per informazioni su come trovare la risorsa XDM desiderata, consultate la guida [Esplora risorse XDM](./explore.md).

Una volta aperto lo schema, selezionare l&#39;icona **[!UICONTROL Copy JSON]** (![Copia icona](../images/ui/export/icon.png)) in alto a destra del quadro.

![](../images/ui/export/copy-json.png)

Questo copia un payload JSON negli Appunti, generato in base alla struttura dello schema. Per lo schema &quot;[!DNL Loyalty Members]&quot; mostrato sopra, viene generato il seguente JSON:

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

Il payload assume la forma di un array, in cui ogni elemento di array è un oggetto che rappresenta una risorsa XDM personalizzata da esportare. Nell&#39;esempio precedente, sono inclusi il mixin personalizzato &quot;[!DNL Loyalty details]&quot; e lo schema &quot;[!DNL Loyalty Members]&quot;. Tutte le risorse di base utilizzate dallo schema non sono incluse nell&#39;esportazione, in quanto sono disponibili in tutte le sandbox e le organizzazioni IMS.

Ogni istanza dell&#39;ID tenant dell&#39;organizzazione viene visualizzata come `<XDM_TENANTID_PLACEHOLDER>` nel payload. Questi segnaposto verranno sostituiti automaticamente con il valore ID tenant appropriato a seconda della posizione in cui si esporta lo schema nel passaggio successivo.

## Importare la risorsa tramite l&#39;API

Dopo aver copiato il JSON di esportazione per lo schema, potete usarlo come payload per una richiesta di POST all&#39;endpoint `/import` nell&#39;API del Registro di sistema dello schema. Per informazioni dettagliate su come configurare la chiamata per l&#39;invio dello schema all&#39;organizzazione IMS e alla sandbox corretta, consultate la sezione sull [importazione di una risorsa XDM nell&#39;API](../api/export-import.md#import).

## Passaggi successivi

Seguendo questa guida, è stato esportato correttamente uno schema XDM in un&#39;organizzazione IMS o sandbox diversa. Per ulteriori informazioni sulle funzionalità dell&#39;interfaccia utente [!UICONTROL Schemas], fare riferimento alla [[!UICONTROL Schemas] panoramica dell&#39;interfaccia utente](./overview.md).