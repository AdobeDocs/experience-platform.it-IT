---
title: Creare una connessione sorgente SAP Commerce nell’interfaccia utente
description: Scopri come creare una connessione sorgente SAP Commerce utilizzando l’interfaccia utente di Adobe Experience Platform.
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 99edb8b2bcd4225235038e966a367d91375c961a
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 1%

---

# Creare un [!DNL SAP Commerce] connessione sorgente nell’interfaccia utente

>[!NOTE]
>
>Il [!DNL SAP Commerce] sorgente in versione beta. Consulta la [panoramica sulle origini](../../../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di fonti etichettate beta.

Il seguente tutorial illustra i passaggi necessari per creare un [!DNL SAP Commerce] connessione sorgente da portare [[!DNL SAP] Fatturazione abbonamento](https://www.sap.com/products/financial-management/subscription-billing.html) contatti e dati dei clienti tramite l’interfaccia utente di Adobe Experience Platform.

## Introduzione {#getting-started}

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Experience Platform] organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di un [!DNL SAP Commerce] account, puoi saltare il resto di questo documento e passare all’esercitazione su [configurazione di un flusso di dati](../../dataflow/ecommerce.md).

### Raccogli le credenziali richieste {#gather-credentials}

Per connettersi [!DNL SAP Commerce] ad Experience Platform, è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| --- | --- |
| ID client | Il valore di `clientId` dalla chiave del servizio. |
| Segreto client | Il valore di `clientSecret` dalla chiave del servizio. |
| Endpoint token | Il valore di `url` dalla chiave del servizio, sarà simile a `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. |
| Area geografica | La posizione del centro dati. La regione è presente nel `url` e ha un valore simile a `eu10` o `us10`. Ad esempio, se `url` è `https://eu10.revenue.cloud.sap/api` avrà bisogno di `eu10`. |

Per ulteriori informazioni, fare riferimento al [[!DNL SAP Commerce] documentazione](https://help.sap.com/docs/CLOUD_TO_CASH_OD/987aec876092428f88162e438acf80d6/c5fcaf96daff4c7a8520188e4d8a1843.html).

### Creare uno schema di Platform {#create-platform-schema}

Prima di creare un [!DNL SAP Commerce] connessione sorgente, devi anche assicurarti di creare prima uno schema di Experience Platform da utilizzare per la sorgente. Guarda il tutorial su [creazione di uno schema di Platform](../../../../../xdm/schema/composition.md) per passaggi completi sulla creazione di uno schema.

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

## Connetti [!DNL SAP Commerce] account {#connect-account}

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Il [!UICONTROL Catalogo] Nella schermata vengono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Sotto *eCommerce* categoria, seleziona **[!UICONTROL Commerce SAP]**, quindi selezionare **[!UICONTROL Aggiungi dati]**.

![Schermata dell’interfaccia utente di Platform per il catalogo con scheda SAP Commerce](../../../../images/tutorials/create/ecommerce/sap-commerce/catalog-card.png)

Il **[!UICONTROL Connetti account SAP Commerce]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente {#existing-account}

Per utilizzare un account esistente, seleziona la [!DNL SAP Commerce] account con cui vuoi creare un nuovo flusso di dati, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![Schermata dell’interfaccia utente di Platform per collegare l’account SAP Commerce a un account esistente](../../../../images/tutorials/create/ecommerce/sap-commerce/existing.png)

### Nuovo account {#new-account}

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]** e quindi fornisci un nome, una descrizione facoltativa e le tue credenziali. Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![Schermata dell’interfaccia utente di Platform per collegare l’account SAP Commerce con un nuovo account](../../../../images/tutorials/create/ecommerce/sap-commerce/new.png)

### Selezionare i dati {#select-data}

Infine, seleziona il tipo di oggetto da acquisire in Platform.

| Tipo di oggetto | Descrizione |
| --- | --- |
| `Customers` | Le entità che dispongono di sottoscrizioni. |
| `Contacts` | I dettagli di contatto per i clienti. |

>[!BEGINTABS]

>[!TAB Clienti]

Per acquisire i dati del cliente, seleziona **[!UICONTROL Clienti]** come tipo di oggetto e quindi selezionare **[!UICONTROL Successivo]**.

![Schermata dell’interfaccia utente di Platform Commerce che mostra la configurazione con l’opzione Clienti selezionata](../../../../images/tutorials/create/ecommerce/sap-commerce/configuration-customers.png)

>[!TAB Contatti]

Per acquisire i dati di contatto, seleziona **[!UICONTROL Contatti]** come tipo di oggetto e quindi selezionare **[!UICONTROL Successivo]**.

![Schermata dell’interfaccia utente di Platform Commerce che mostra la configurazione con l’opzione Contatti selezionata](../../../../images/tutorials/create/ecommerce/sap-commerce/configuration-contacts.png)

>[!ENDTABS]

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione, hai stabilito una connessione con il tuo [!DNL SAP Commerce] account. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per inserire i dati in Platform](../../dataflow/ecommerce.md).

## Risorse aggiuntive {#additional-resources}

Le sezioni seguenti forniscono ulteriori risorse a cui puoi fare riferimento quando utilizzi il [!DNL SAP Commerce] sorgente.

### Mappatura {#mapping}

Platform fornisce consigli intelligenti per campi mappati automaticamente in base allo schema o al set di dati di destinazione selezionato. Puoi regolare manualmente le regole di mappatura in base ai tuoi casi d’uso. In base alle tue esigenze, puoi scegliere di mappare i campi direttamente o utilizzare le funzioni di preparazione dati per trasformare i dati sorgente in modo da derivare valori calcolati o calcolati. Per i passaggi completi sull’utilizzo dell’interfaccia mapper e dei campi calcolati, vedi la [Guida dell’interfaccia utente per la preparazione dati](../../../../../data-prep/ui/mapping.md).

Le configurazioni di mappatura per il flusso di dati variano a seconda dello schema e del tipo di oggetto selezionato per l’acquisizione.

>[!BEGINTABS]

>[!TAB Clienti]

Per i dati dei clienti, [!DNL SAP Commerce] utilizza [clienti](https://api.sap.com/api/BusinessPartner_APIs/path/GET_customers) e [relazioni cliente-contatti](https://api.sap.com/api/BusinessPartner_APIs/path/GET_relationships-customer-contacts) endpoint del [!DNL SAP Business Partners] API per recuperare i dati

Di seguito è riportato un esempio di configurazioni di mappatura per [!DNL SAP Commerce] flusso di dati per i dati dei clienti:

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

![Passaggio di mappatura del flusso di lavoro origini.](../../../../images/tutorials/create/ecommerce/sap-commerce/mapping-customers.png)

>[!TAB Contatti]

Per i dati di contatto, [!DNL SAP Commerce] utilizza [contatti](https://api.sap.com/api/BusinessPartner_APIs/path/GET_contacts) endpoint del [!DNL SAP Business Partners] API per recuperare i dati.

Di seguito è riportato un esempio di configurazioni di mappatura per [!DNL SAP Commerce] flusso di dati per i dati di contatto:

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

![Passaggio di mappatura del flusso di lavoro origini.](../../../../images/tutorials/create/ecommerce/sap-commerce/mapping-contacts.png)

>[!ENDTABS]

