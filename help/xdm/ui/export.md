---
solution: Experience Platform
title: Esportare gli schemi XDM nell’interfaccia utente
description: Scopri come esportare uno schema esistente in una sandbox o organizzazione diversa nell’interfaccia utente di Adobe Experience Platform.
type: Tutorial
exl-id: c467666d-55bc-4134-b8f4-7758d49c4786
source-git-commit: 0f0842c1d14ce42453b09bf97e1f3690448f6e9a
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 11%

---

# Esportare gli schemi XDM nell’interfaccia utente {#export-xdm-schemas-in-the-UI}

>[!CONTEXTUALHELP]
>id="platform_xdm_copyjsonstructure"
>title="Copia struttura JSON"
>abstract="Genera un payload di esportazione per lo schema scelto copiando la struttura JSON negli appunti. Utilizza questa funzione per esportare i dettagli di qualsiasi schema della libreria degli schemi. Questo JSON esportato può quindi essere utilizzato per importare lo schema e tutte le risorse correlate in una sandbox o organizzazione diversa. In questo modo la condivisione e il riutilizzo degli schemi tra ambienti diversi diventano semplici ed efficienti."

Tutte le risorse all’interno della Libreria schemi sono contenute in una sandbox specifica all’interno di un’organizzazione. In alcuni casi, potrebbe essere utile condividere risorse Experience Data Model (XDM) tra sandbox e organizzazioni.

Per soddisfare questa esigenza, l&#39;area di lavoro [!UICONTROL Schemi] nell&#39;interfaccia utente di Adobe Experience Platform consente di generare un payload di esportazione per qualsiasi schema all&#39;interno della raccolta schemi. Questo payload può quindi essere utilizzato in una chiamata all’API Schema Registry per importare lo schema (e tutte le risorse dipendenti) in una sandbox e un’organizzazione di destinazione.

>[!NOTE]
>
>È inoltre possibile utilizzare l’API Schema Registry per esportare altre risorse oltre agli schemi, tra cui classi, gruppi di campi di schema e tipi di dati. Per ulteriori informazioni, consulta la [guida dell&#39;endpoint di esportazione](../api/export.md).

## Prerequisiti

Anche se l’interfaccia utente di Platform consente di esportare risorse XDM, è necessario utilizzare l’API Schema Registry per importare tali risorse in altre sandbox o organizzazioni per completare il flusso di lavoro. Consulta la guida [guida introduttiva all&#39;API Schema Registry](../api/getting-started.md) per informazioni importanti sulle intestazioni di autenticazione richieste prima di seguire questa guida.

## Generare un payload di esportazione {#generate-export-payload}

I payload di esportazione possono essere generati nell&#39;interfaccia utente di Platform dal pannello dei dettagli nella scheda [!UICONTROL Sfoglia] o direttamente dall&#39;area di lavoro dello schema nell&#39;Editor di schema.

Per generare un payload di esportazione, seleziona **[!UICONTROL Schemi]** nell&#39;area di navigazione a sinistra. Nell&#39;area di lavoro [!UICONTROL Schemi], selezionare la riga dello schema da esportare per visualizzare i dettagli dello schema nella barra laterale a destra.

>[!TIP]
>
>Per informazioni dettagliate su come trovare la risorsa XDM che stai cercando, consulta la guida su [esplorazione delle risorse XDM](./explore.md).

Quindi, seleziona l&#39;icona **[!UICONTROL Copia JSON]** (![Copia icona](../images/ui/export/icon.png)) tra le opzioni disponibili.

![Area di lavoro Schemi con una riga di schema e [!UICONTROL Copia in JSON] evidenziata.](../images/ui/export/copy-json.png)

Questo copia un payload JSON negli Appunti, generato in base alla struttura dello schema. Per lo schema &quot;[!DNL Loyalty Members]&quot; mostrato sopra, viene generato il seguente JSON:

+++Seleziona per espandere un esempio di payload JSON

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

+++

È inoltre possibile copiare il payload selezionando [!UICONTROL Altro] in alto a destra nell&#39;Editor di schema. Un menu a discesa fornisce due opzioni: [!UICONTROL Copia struttura JSON] e [!UICONTROL Elimina schema].

>[!NOTE]
>
>Non è possibile eliminare uno schema se è abilitato per il profilo o se a esso sono associati set di dati.

![Editor schemi con [!UICONTROL Altro] e [!UICONTROL Copia in JSON] evidenziati.](../images/ui/export/schema-editor-copy-json.png)

Il payload assume la forma di un array; ogni elemento dell’array è un oggetto che rappresenta una risorsa XDM personalizzata da esportare. Nell&#39;esempio precedente, il gruppo di campi personalizzato &quot;[!DNL Loyalty details]&quot; e lo schema &quot;[!DNL Loyalty Members]&quot; sono inclusi. Tutte le risorse core utilizzate dallo schema non vengono incluse nell’esportazione, in quanto sono disponibili in tutte le sandbox e le organizzazioni.

Tieni presente che ogni istanza dell&#39;ID tenant della tua organizzazione viene visualizzata come `<XDM_TENANTID_PLACEHOLDER>` nel payload. Questi segnaposto verranno sostituiti automaticamente con il valore ID tenant appropriato a seconda di dove importi lo schema nel passaggio successivo.

## Importare la risorsa utilizzando l’API {#import-resource-with-api}

Dopo aver copiato il JSON di esportazione per lo schema, puoi utilizzarlo come payload per una richiesta POST all&#39;endpoint `/rpc/import` nell&#39;API Schema Registry. Consulta la [guida dell&#39;endpoint di importazione](../api/import.md) per informazioni dettagliate su come configurare la chiamata per inviare lo schema all&#39;organizzazione e alla sandbox desiderate.

## Passaggi successivi

Seguendo questa guida, hai esportato correttamente uno schema XDM in un’organizzazione o sandbox diversa. Per ulteriori informazioni sulle funzionalità dell&#39;interfaccia utente di [!UICONTROL Schemi], fare riferimento alla panoramica dell&#39;interfaccia utente di [[!UICONTROL Schemi]](./overview.md).
