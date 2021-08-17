---
keywords: Destinazione hub eventi Azure;hub eventi azure;azure eventhub
title: (Beta) Connessione a !DNL Azure Event Hubs]
description: Crea una connessione in uscita in tempo reale all’archivio !DNL Azure Event Hubs] per lo streaming dei dati dall’Experience Platform.
exl-id: f98a389a-bce3-4a80-9452-6c7293d01de3
source-git-commit: 15ea3ab9370541c35b874414a8753e8812eea9c6
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 2%

---

# (Beta) Connessione [!DNL Azure Event Hubs]

## Panoramica {#overview}

>[!IMPORTANT]
>
>La destinazione [!DNL Azure Event Hubs] in Platform è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

[!DNL Azure Event Hubs] è una piattaforma per lo streaming di dati e un servizio per l’acquisizione di eventi. Può ricevere ed elaborare milioni di eventi al secondo. I dati inviati a un hub eventi possono essere trasformati e memorizzati utilizzando qualsiasi provider di analisi in tempo reale o adattatori di batch/storage.

Puoi creare una connessione in uscita in tempo reale allo storage [!DNL Azure Event Hubs] per lo streaming dei dati da Adobe Experience Platform.

* Per ulteriori informazioni su [!DNL Azure Event Hubs], consulta la [documentazione Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* Per connetterti a [!DNL Azure Event Hubs] a livello di programmazione, consulta l’ [esercitazione API sulle destinazioni di streaming](../../api/streaming-destinations.md) .
* Per effettuare la connessione a [!DNL Azure Event Hubs] utilizzando l’interfaccia utente di Platform, consulta le sezioni seguenti.

![AWS Kinesis nell’interfaccia utente](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## Casi d’uso {#use-cases}

Utilizzando destinazioni di streaming come [!DNL Azure Event Hubs], puoi facilmente inserire nei tuoi sistemi selezionati eventi di segmentazione di alto valore e attributi di profilo associati.

Ad esempio, un prospect ha scaricato un white paper che li qualifica in un segmento &quot;alta propensione alla conversione&quot;. Mappando il segmento in cui il potenziale di crescita rientra nella destinazione [!DNL Azure Event Hubs], riceverai questo evento in [!DNL Azure Event Hubs]. In questo caso, è possibile utilizzare un approccio fai-da-te e descrivere la logica di business al di sopra dell&#39;evento, in quanto si ritiene che funzionerebbe meglio con i sistemi IT aziendali.

## Tipo di esportazione {#export-type}

**Basato su profilo** : stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto dalla schermata seleziona attributi del flusso di lavoro [ di attivazione della ](../../ui/activate-destinations.md#select-attributes)destinazione.

## Collegati alla destinazione {#connect}

Per connetterti a questa destinazione, segui i passaggi descritti nel [tutorial sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Durante la [configurazione](../../ui/connect-destination.md) di questa destinazione, è necessario fornire le seguenti informazioni:

* **[!UICONTROL Nome chiave]** SAS e chiave  **[!UICONTROL SAS]**: Immettere il nome e la chiave della chiave SAS. Informazioni sull&#39;autenticazione in [!DNL Azure Event Hubs] con chiavi SAS nella [documentazione Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Namespace]**: Inserisci lo  [!DNL Azure Event Hubs] spazio dei nomi. Ulteriori informazioni sui namespace [!DNL Azure Event Hubs] nella [documentazione Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).
* **[!UICONTROL Nome]**: Immetti un nome per la connessione a  [!DNL Azure Event Hubs].
* **[!UICONTROL Descrizione]**: Fornire una descrizione della connessione.  Esempi: &quot;Clienti di livello Premium&quot;, &quot;Maschi interessati al kitesurfing&quot;.
* **[!UICONTROL eventHubName]**: Specifica un nome per il flusso alla  [!DNL Azure Event Hubs] destinazione.

## Attiva i segmenti in questa destinazione {#activate}

Per istruzioni sull’attivazione dei segmenti di pubblico nelle destinazioni, consulta [Attivare profili e segmenti in una destinazione](../../ui/activate-destinations.md) .

## Dati esportati {#exported-data}

I dati esportati [!DNL Experience Platform] arrivano in [!DNL Azure Event Hubs] in formato JSON. Ad esempio, l’evento seguente contiene l’attributo di profilo dell’indirizzo e-mail di un pubblico qualificato per un determinato segmento ed uscito da un altro segmento. Le identità di questo potenziale cliente sono ECID e e-mail.

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
>* [Connettersi agli hub eventi di Azure e attivare i dati utilizzando l’API del servizio di flusso](../../api/streaming-destinations.md)
* [Destinazione AWS Kinesis](./amazon-kinesis.md)
* [Tipi di destinazione e categorie](../../destination-types.md)

