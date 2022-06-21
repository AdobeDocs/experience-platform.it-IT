---
solution: Experience Platform
title: Esportare gli schemi XDM nell’interfaccia utente
description: Scopri come esportare uno schema esistente in un’organizzazione sandbox o IMS diversa nell’interfaccia utente di Adobe Experience Platform.
topic-legacy: user guide
type: Tutorial
exl-id: c467666d-55bc-4134-b8f4-7758d49c4786
source-git-commit: 2a58236031834bbe298576e2fcab54b04ec16ac3
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---

# Esportare schemi XDM nell’interfaccia utente

Tutte le risorse all’interno della Libreria schema sono contenute in una sandbox specifica all’interno di un’organizzazione IMS. In alcuni casi, puoi condividere risorse Experience Data Model (XDM) tra le sandbox e le organizzazioni IMS.

Per rispondere a questa esigenza, il [!UICONTROL Schemi] L’area di lavoro nell’interfaccia utente di Adobe Experience Platform consente di generare un payload di esportazione per qualsiasi schema all’interno della Libreria schema. Questo payload può quindi essere utilizzato in una chiamata all’API del Registro di sistema dello schema per importare lo schema (e tutte le risorse dipendenti) in una sandbox di destinazione e nell’organizzazione IMS.

>[!NOTE]
>
>È inoltre possibile utilizzare l’API del Registro di sistema dello schema per esportare altre risorse oltre agli schemi, tra cui classi, gruppi di campi dello schema e tipi di dati. Consulta la sezione [guida all’endpoint per l’esportazione](../api/export.md) per ulteriori informazioni.

## Prerequisiti

Sebbene l’interfaccia utente di Platform consenta di esportare risorse XDM, è necessario utilizzare l’API del Registro di sistema dello schema per importare tali risorse in altre sandbox o organizzazioni IMS per completare il flusso di lavoro. Consulta la guida su [guida introduttiva all’API del Registro di sistema dello schema](../api/getting-started.md) per informazioni importanti sulle intestazioni di autenticazione richieste prima di seguire questa guida.

## Generare un payload di esportazione

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Schemi]** nella navigazione a sinistra. All&#39;interno di [!UICONTROL Schemi] area di lavoro, individuare lo schema da esportare e aprirlo nel [!DNL Schema Editor].

>[!TIP]
>
>Consulta la guida su [esplorazione delle risorse XDM](./explore.md) per informazioni su come trovare la risorsa XDM desiderata.

Una volta aperto lo schema, seleziona la **[!UICONTROL Copia JSON]** icona (![Icona Copia](../images/ui/export/icon.png)) in alto a destra nell’area di lavoro.

![](../images/ui/export/copy-json.png)

Questo copia un payload JSON negli Appunti, generato in base alla struttura dello schema. Per &quot;[!DNL Loyalty Members]&quot; schema mostrato sopra, viene generato il seguente JSON:

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

Il payload si presenta come una matrice e ogni elemento della matrice è un oggetto che rappresenta una risorsa XDM personalizzata da esportare. Nell&#39;esempio precedente, il &quot;[!DNL Loyalty details]&quot; gruppo di campi personalizzati e &quot;[!DNL Loyalty Members]&quot; schema incluso. Tutte le risorse di base utilizzate dallo schema non sono incluse nell’esportazione, in quanto sono disponibili in tutte le sandbox e le organizzazioni IMS.

Tieni presente che ogni istanza dell’ID tenant dell’organizzazione viene visualizzata come `<XDM_TENANTID_PLACEHOLDER>` nel payload. Questi segnaposto verranno sostituiti automaticamente con il valore ID tenant appropriato a seconda della posizione in cui si importa lo schema nel passaggio successivo.

## Importare la risorsa utilizzando l’API

Dopo aver copiato il JSON di esportazione per lo schema, puoi utilizzarlo come payload per una richiesta POST al `/rpc/import` endpoint nell&#39;API del Registro di sistema dello schema. Consulta la sezione [guida all’importazione di endpoint](../api/import.md) per informazioni su come configurare la chiamata per l’invio dello schema all’organizzazione IMS e alla sandbox desiderate.

## Passaggi successivi

Seguendo questa guida, hai esportato correttamente uno schema XDM in un’organizzazione IMS o sandbox diversa. Per ulteriori informazioni sulle funzionalità del [!UICONTROL Schemi] Interfaccia utente, fai riferimento alla [[!UICONTROL Schemi] Panoramica dell’interfaccia utente](./overview.md).
