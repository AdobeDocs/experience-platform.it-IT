---
keywords: Destinazione hub eventi di Azure;hub eventi di azzure;azure eventhub
title: (Beta) Destinazione degli hub eventi di Azure
seo-title: (Beta) Destinazione degli hub eventi di Azure
description: Crea una connessione in uscita in tempo reale all'archivio degli hub eventi di Azure per lo streaming dei dati dal Experience Platform .
seo-description: Crea una connessione in uscita in tempo reale all'archivio degli hub eventi di Azure per lo streaming dei dati dal Experience Platform .
translation-type: tm+mt
source-git-commit: 97c0a9f4726ec85b7a72dc682fbd201a6152c1ba
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 2%

---


# (Beta) [!DNL Azure Event Hubs] destinazione

>[!IMPORTANT]
>
>La destinazione [!DNL Azure Event Hubs] in Platform è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

## Panoramica {#overview}

[!DNL Azure Event Hubs] è una grande piattaforma di streaming dati e un servizio di caricamento eventi. Può ricevere ed elaborare milioni di eventi al secondo. I dati inviati a un hub eventi possono essere trasformati e memorizzati utilizzando qualsiasi provider di analisi in tempo reale o adattatori di batch/storage.

È possibile creare una connessione in uscita in tempo reale allo storage [!DNL Azure Event Hubs] per lo streaming dei dati da Adobe Experience Platform.

* Per ulteriori informazioni su [!DNL Azure Event Hubs], consultare la [documentazione Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* Per connettersi a [!DNL Azure Event Hubs] utilizzando le chiamate API, consulta l&#39; [esercitazione API delle destinazioni di streaming](../../api/streaming-destinations.md).
* Per connettersi a [!DNL Azure Event Hubs] utilizzando l&#39;interfaccia utente della piattaforma, consulta le sezioni riportate di seguito.

![Kinesis AWS nell&#39;interfaccia utente](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## Casi d’uso {#use-cases}

Utilizzando le destinazioni di streaming come [!DNL Azure Event Hubs], potete facilmente inserire nei vostri sistemi di scelta eventi di segmentazione di alto valore e attributi di profilo associati.

Ad esempio, un potenziale ha scaricato un white paper che li qualifica come segmento &quot;alta propensione alla conversione&quot;. Mappando il segmento in cui il potenziale rientra nella destinazione [!DNL Azure Event Hubs], si riceverebbe questo evento in [!DNL Azure Event Hubs]. È possibile utilizzare un approccio &quot;fai da te&quot; e descrivere la logica di business in cima all&#39;evento, come si pensa che funzionerebbe meglio con i sistemi IT aziendali.

## Tipo di esportazione {#export-type}

**Basato**  su profilo: si esportano tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata degli attributi selezionati del flusso di lavoro [ di attivazione della ](../../ui/activate-destinations.md#select-attributes)destinazione.

## Destinazione Connect {#connect-destination}

Per istruzioni su come connettersi alle destinazioni di archiviazione cloud, incluso [!DNL Azure Event Hubs], vedere [Flusso di lavoro delle destinazioni di archiviazione cloud ](./workflow.md).

Per le destinazioni [!DNL Azure Event Hubs], immetti le seguenti informazioni nel flusso di lavoro di creazione della destinazione:

### Nel passaggio Autenticazione {#authentication-step}

* **[!UICONTROL SAS Key Name]** e  **[!UICONTROL SAS Key]**: Inserisci il nome e la chiave della chiave SAS. Informazioni sull&#39;autenticazione a [!DNL Azure Event Hubs] con chiavi SAS nella [documentazione Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Namespace]**: Compilare lo  [!DNL Azure Event Hubs] spazio dei nomi. Ulteriori informazioni sugli spazi dei nomi [!DNL Azure Event Hubs] nella [documentazione Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).

![Input richiesto nel passaggio di autenticazione](../../assets/catalog/cloud-storage/event-hubs/authentication.png)

### Nel passaggio di configurazione {#setup-step}

* **[!UICONTROL Name]**: Compilate un nome per la connessione a  [!DNL Azure Event Hubs].
* **[!UICONTROL Description]**: Fornire una descrizione della connessione.  Esempi: &quot;Clienti di livello Premium&quot;, &quot;Maschi interessati a kitesurfing&quot;.
* **[!UICONTROL eventHubName]**: Specifica un nome per il flusso alla  [!DNL Azure Event Hubs] destinazione.

![Dati richiesti nel passaggio di configurazione](../../assets/catalog/cloud-storage/event-hubs/setup.png)

## Attivare i segmenti {#activate-segments}

Per informazioni sul flusso di lavoro di attivazione dei segmenti, vedere [Attivare profili e segmenti in una destinazione](../../ui/activate-destinations.md).

## Dati esportati {#exported-data}

I dati esportati [!DNL Experience Platform] vengono inviati in [!DNL Azure Event Hubs] in formato JSON. Ad esempio, l&#39;evento seguente contiene l&#39;attributo di profilo dell&#39;indirizzo e-mail di un&#39;audience qualificata per un determinato segmento ed uscita da un altro segmento. Le identità di questo potenziale sono ECID ed e-mail.

```json
{
  "person": {
    "email": "yourstruly@adobe.con"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "existing"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```


>[!MORELIKETHIS]
>
>* [Connessione ad Azure Event Hubs e attivazione dei dati tramite chiamate API](../../api/streaming-destinations.md)
>* [Destinazione Kinesis AWS](./amazon-kinesis.md)
>* [Tipi e categorie di destinazione](../../destination-types.md)