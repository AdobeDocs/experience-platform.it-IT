---
title: Creare una connessione sorgente SAP Commerce nell'interfaccia utente
description: Scopri come creare una connessione sorgente SAP Commerce utilizzando l’interfaccia utente di Adobe Experience Platform.
badge: Beta
exl-id: 6484e51c-77cd-4dbd-9c68-0a4e3372da33
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 3%

---

# Crea una connessione sorgente [!DNL SAP Commerce] nell&#39;interfaccia utente

>[!NOTE]
>
>L&#39;origine [!DNL SAP Commerce] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo di origini con etichetta beta, vedere la [panoramica origini](../../../../home.md#terms-and-conditions).

Il seguente tutorial illustra i passaggi necessari per creare una connessione di origine [!DNL SAP Commerce] per portare i contatti di [[!DNL SAP] Subscription Billing](https://www.sap.com/products/financial-management/subscription-billing.html) e i dati dei clienti tramite l&#39;interfaccia utente di Adobe Experience Platform.

## Introduzione {#getting-started}

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di un account [!DNL SAP Commerce] valido, puoi saltare il resto di questo documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/ecommerce.md).

### Raccogli le credenziali richieste {#gather-credentials}

Per connettere [!DNL SAP Commerce] a Experience Platform, è necessario fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| --- | --- |
| ID client | Il valore di `clientId` dalla chiave del servizio. |
| Segreto client | Il valore di `clientSecret` dalla chiave del servizio. |
| Endpoint token | Il valore di `url` dalla chiave del servizio sarà simile a `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. |
| Area geografica | La posizione del centro dati. L&#39;area è presente in `url` e ha un valore simile a `eu10` o `us10`. Ad esempio, se `url` è `https://eu10.revenue.cloud.sap/api`, sarà necessario `eu10`. |

Per ulteriori informazioni, consulta la [[!DNL SAP Commerce] documentazione](https://help.sap.com/docs/CLOUD_TO_CASH_OD/987aec876092428f88162e438acf80d6/c5fcaf96daff4c7a8520188e4d8a1843.html).

### Creare uno schema di Platform {#create-platform-schema}

Prima di creare una connessione di origine [!DNL SAP Commerce], è inoltre necessario assicurarsi di creare uno schema di Experience Platform da utilizzare per l&#39;origine. Consulta il tutorial su [creazione di uno schema di Platform](../../../../../xdm/schema/composition.md) per i passaggi completi sulla creazione di uno schema.

Espandi la sezione seguente per visualizzare un esempio di schema.

+++ Visualizza esempio di schema

```
{
  "_extconndev": {
    "addresses": [
      {
        "addressUUID": "{ADDRESS_UUID}",
        "city": "Burnaby",
        "country": "Canada",
        "email": "chandni@acme.com",
        "houseNumber": "27",
        "isDefault": false,
        "phone": "123-456-7890",
        "postalCode": "V3J 1X9",
        "state": "British Columbia",
        "street": "Beresford"
      }
    ],
    "changedAt": "1687204041",
    "changedBy": "vero@acme.com",
    "contactNumber": "123-456-7980",
    "corporateInfo": {
      "company": "acme"
    },
    "createAt": "1687204041",
    "createdBy": "vero@acme.com",
    "customReferences": [
      {
        "id": "Sample value",
        "typeCode": "Sample value"
      }
    ],
    "customerNumber": "Sample value",
    "customerType": "Sample value",
    "defaultAddress": {
      "addressUUID": "Sample value",
      "city": "North Vancouver",
      "country": "Canada",
      "email": "chandni@acme.come",
      "houseNumber": "34",
      "isDefault": false,
      "phone": "123-456-7890",
      "postalCode": "V7H 2P1",
      "state": "British Columbia",
      "street": "Maple"
    },
    "externalObjectReferences": [
      {
        "externalId": "{EXTERNAL_ID}",
        "externalIdTypeCode": "{EXTERNAL_ID_TYPE_CODE}",
        "externalSystemId": "{EXTERNAL_SYSTEM_ID}"
      }
    ],
    "markets": [
      {
        "active": false,
        "country": "USA",
        "currency": "USD",
        "marketId": "Sample value",
        "priceinfo": {
          "incoterms": "{INCO_TERMS}",
          "incotermsLocation": "{INCO_TERMS_LOCATION}",
          "priceGroup": "{PRICE_GROUP}",
          "priceListType": "{PRICE_LIST_TYPE}"
        },
        "salesArea": {
          "distributionChannel": "{DISTRIBUTION_CHANNEL}",
          "division": "{DIVISION}",
          "salesOrganization": "{SALES_ORGANIZATION}"
        }
      }
    ],
    "personalInfo": {
      "firstName": "Chandni",
      "lastName": "Kaur"
    }
  },
  "_id": "/uri-reference",
  "_repo": {
    "createDate": "2004-10-23T12:00:00-06:00",
    "modifyDate": "2004-10-23T12:00:00-06:00"
  },
  "createdByBatchID": "/uri-reference",
  "modifiedByBatchID": "/uri-reference",
  "personID": "{PERSON_ID}",
  "repositoryCreatedBy": "kevin@acme.com",
  "repositoryLastModifiedBy": "kevin@acme.com"
}
```

+++

## Connetti il tuo account [!DNL SAP Commerce] {#connect-account}

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Nella schermata [!UICONTROL Catalogo] sono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria *eCommerce*, selezionare **[!UICONTROL SAP Commerce]**, quindi **[!UICONTROL Add data]**.

![Schermata dell&#39;interfaccia utente di Platform per il catalogo con scheda SAP Commerce](../../../../images/tutorials/create/ecommerce/sap-commerce/catalog-card.png)

Viene visualizzata la pagina **[!UICONTROL Connetti account SAP Commerce]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente {#existing-account}

Per utilizzare un account esistente, seleziona l&#39;account [!DNL SAP Commerce] con cui vuoi creare un nuovo flusso di dati, quindi seleziona **[!UICONTROL Successivo]** per continuare.

![Schermata dell&#39;interfaccia utente di Platform per collegare l&#39;account SAP Commerce a un account esistente](../../../../images/tutorials/create/ecommerce/sap-commerce/existing.png)

### Nuovo account {#new-account}

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci un nome, una descrizione facoltativa e le tue credenziali. Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![Schermata dell&#39;interfaccia utente di Platform per collegare l&#39;account SAP Commerce con un nuovo account](../../../../images/tutorials/create/ecommerce/sap-commerce/new.png)

### Selezionare i dati {#select-data}

Infine, seleziona il tipo di oggetto da acquisire in Platform.

| Tipo di oggetto | Descrizione |
| --- | --- |
| `Customers` | Le entità che dispongono di sottoscrizioni. |
| `Contacts` | I dettagli di contatto per i clienti. |

>[!BEGINTABS]

>[!TAB Clienti]

Per acquisire i dati del cliente, seleziona **[!UICONTROL Clienti]** come tipo di oggetto, quindi seleziona **[!UICONTROL Successivo]**.

![Schermata dell&#39;interfaccia utente di Platform per SAP Commerce che mostra la configurazione con l&#39;opzione Clienti selezionata](../../../../images/tutorials/create/ecommerce/sap-commerce/configuration-customers.png)

>[!TAB Contatti]

Per acquisire i dati di contatto, seleziona **[!UICONTROL Contatti]** come tipo di oggetto, quindi seleziona **[!UICONTROL Successivo]**.

![Schermata dell&#39;interfaccia utente di Platform per SAP Commerce con l&#39;opzione di configurazione con contatti selezionata](../../../../images/tutorials/create/ecommerce/sap-commerce/configuration-contacts.png)

>[!ENDTABS]

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL SAP Commerce]. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per inserire dati in Platform](../../dataflow/ecommerce.md).

## Risorse aggiuntive {#additional-resources}

Le sezioni seguenti forniscono ulteriori risorse a cui fare riferimento quando si utilizza l&#39;origine [!DNL SAP Commerce].

### Mappatura {#mapping}

Platform fornisce consigli intelligenti per campi mappati automaticamente in base allo schema o al set di dati di destinazione selezionato. Puoi regolare manualmente le regole di mappatura in base ai tuoi casi d’uso. In base alle tue esigenze, puoi scegliere di mappare i campi direttamente o utilizzare le funzioni di preparazione dati per trasformare i dati sorgente in modo da derivare valori calcolati o calcolati. Per i passaggi completi sull&#39;utilizzo dell&#39;interfaccia mapper e dei campi calcolati, consulta la [guida dell&#39;interfaccia utente della preparazione dati](../../../../../data-prep/ui/mapping.md).

Le configurazioni di mappatura per il flusso di dati variano a seconda dello schema e del tipo di oggetto selezionato per l’acquisizione.

>[!BEGINTABS]

>[!TAB Clienti]

Per i dati del cliente, [!DNL SAP Commerce] utilizza gli endpoint [clienti](https://api.sap.com/api/BusinessPartner_APIs/path/GET_customers) e [relazioni cliente-contatti](https://api.sap.com/api/BusinessPartner_APIs/path/GET_relationships-customer-contacts) dell&#39;API [!DNL SAP Business Partners] per recuperare i dati

Di seguito è riportato un esempio di configurazioni di mappatura per il flusso di dati [!DNL SAP Commerce] per i dati dei clienti:

| Campo di destinazione | Descrizione |
| --- | --- |
| `customerNumber` | Il numero del cliente. |
| `corporateInfo` | Il numero del cliente. |
| `customerType` | Il tipo di cliente. |
| `createdAt` | Un timestamp che indica quando è stato creato il cliente. |
| `changedAt` | Un timestamp che indica quando il cliente è stato aggiornato l’ultima volta. |
| `markets[*].country` | I mercati dei clienti, recuperati come oggetto array. |
| `addresses[*].email` | Le e-mail associate ai diversi indirizzi del cliente, recuperate come oggetto array. |
| `addresses[*].city` | Città associate ai diversi indirizzi del cliente, recuperate come oggetto array. |
| `addresses[*].addressUUID` | L’ID è associato ai diversi indirizzi del cliente, recuperati come oggetto array. |
| `externalObjectReferences[*].externalSystemId` | Dati aggiuntivi, recuperati come oggetto array. |
| `externalObjectReferences[*].externalId` | Dati aggiuntivi, recuperati come oggetto array. |
| `customReferences[*].id` | Dati aggiuntivi, recuperati come oggetto array. |
| `customReferences[*].typeCode` | Dati aggiuntivi, recuperati come oggetto array. |

![Passaggio di mappatura del flusso di lavoro di origine.](../../../../images/tutorials/create/ecommerce/sap-commerce/mapping-customers.png)

>[!TAB Contatti]

Per i dati di contatto, [!DNL SAP Commerce] utilizza l&#39;endpoint [contacts](https://api.sap.com/api/BusinessPartner_APIs/path/GET_contacts) dell&#39;API [!DNL SAP Business Partners] per recuperare i dati.

Di seguito è riportato un esempio di configurazioni di mappatura per il flusso di dati [!DNL SAP Commerce] per i dati di contatto:

| Campo di destinazione | Descrizione |
| --- | --- |
| `contactNumber` | Il numero del contatto. |
| `createdAt` | Timestamp che indica quando è stato creato il contatto. |
| `changedAt` | Timestamp che indica quando è stato eseguito l’ultimo aggiornamento del contatto. |
| `personalInfo.lastName` | Cognome del contatto. |
| `personalInfo.firstName` | Nome del contatto. |
| `externalObjectReferences[*].externalSystemId` | Dati aggiuntivi, recuperati come oggetto array. |
| `externalObjectReferences[*].externalId` | Dati aggiuntivi, recuperati come oggetto array. |
| `externalObjectReferences[*].externalIdTypeCode` | Dati aggiuntivi, recuperati come oggetto array. |

![Passaggio di mappatura del flusso di lavoro di origine.](../../../../images/tutorials/create/ecommerce/sap-commerce/mapping-contacts.png)

>[!ENDTABS]
