---
title: (Beta) Destinazione degli hub eventi di Azure
seo-title: (Beta) Destinazione degli hub eventi di Azure
description: Crea una connessione in uscita in tempo reale all'archivio degli hub eventi di Azure per lo streaming dei dati dal Experience Platform .
seo-description: Crea una connessione in uscita in tempo reale all'archivio degli hub eventi di Azure per lo streaming dei dati dal Experience Platform .
translation-type: tm+mt
source-git-commit: b96286f6a06f0583b45343a513ee64f0025d79a7
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 2%

---


# (Beta) [!DNL Azure Event Hubs] destinazione

>[!IMPORTANT]
>
>La [!DNL Azure Event Hubs] destinazione in  Adobe CDP in tempo reale è attualmente in versione beta. La documentazione e la funzionalità sono soggette a modifiche.

## Panoramica {#overview}

[!DNL Azure Event Hubs] è una grande piattaforma di streaming dati e un servizio di caricamento eventi. Può ricevere ed elaborare milioni di eventi al secondo. I dati inviati a un hub eventi possono essere trasformati e memorizzati utilizzando qualsiasi provider di analisi in tempo reale o adattatori di batch/storage.

È possibile creare una connessione in uscita in tempo reale allo [!DNL Azure Event Hubs] storage per lo streaming dei dati da  Adobe Experience Platform.

* Per ulteriori informazioni [!DNL Azure Event Hubs], consulta la documentazione [](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about)Microsoft.
* Per connettersi a [!DNL Azure Event Hubs] utilizzando le chiamate API, consulta l’esercitazione [API](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md)Streaming destinations.
* Per connettersi a [!DNL Azure Event Hubs] utilizzando l&#39;interfaccia utente CDP in tempo reale del Adobe , vedere le sezioni seguenti.

![Kinesis AWS nell&#39;interfaccia utente](/help/rtcdp/destinations/assets/azure-event-hubs-destination.png)

## Casi d’uso {#use-cases}

Utilizzando destinazioni di streaming come [!DNL Azure Event Hubs], potete facilmente inserire nei sistemi di vostra scelta eventi di segmentazione di alto valore e attributi di profilo associati.

Ad esempio, un potenziale ha scaricato un white paper che li qualifica come segmento &quot;alta propensione alla conversione&quot;. Mappando il segmento in cui il potenziale rientra nella [!DNL Azure Event Hubs] destinazione, si riceverebbe questo evento in [!DNL Azure Event Hubs]. È possibile utilizzare un approccio &quot;fai da te&quot; e descrivere la logica di business in cima all&#39;evento, come si pensa che funzionerebbe meglio con i sistemi IT aziendali.

## Destinazione Connect {#connect-destination}

Consulta Flusso di lavoro delle destinazioni di archiviazione [Cloud ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)per istruzioni su come connettersi alle destinazioni di archiviazione cloud, comprese [!DNL Azure Event Hubs]le destinazioni.

Per [!DNL Azure Event Hubs] le destinazioni, immetti le seguenti informazioni nel flusso di lavoro di creazione della destinazione:

### Nel passaggio Autenticazione {#authentication-step}

* **[!UICONTROL SAS Key Name]** e **[!UICONTROL SAS Key]**: Inserisci il nome e la chiave della chiave SAS. Informazioni sull&#39;autenticazione con [!DNL Azure Event Hubs] le chiavi SAS nella documentazione [](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)Microsoft.
* **[!UICONTROL Namespace]**: Compilare lo [!DNL Azure Event Hubs] spazio dei nomi. Ulteriori informazioni sugli [!DNL Azure Event Hubs] spazi dei nomi nella documentazione [di](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace)Microsoft.

![Input richiesto nel passaggio di autenticazione](/help/rtcdp/destinations/assets/event-hubs-authentication.png)

### Nel passaggio Configurazione {#setup-step}

* **[!UICONTROL Name]**: Compilate un nome per la connessione a [!DNL Azure Event Hubs].
* **[!UICONTROL Description]**: Fornire una descrizione della connessione.  Esempi: &quot;Clienti di livello Premium&quot;, &quot;Maschi interessati a kitesurfing&quot;.
* **[!UICONTROL eventHubName]**: Specifica un nome per il flusso alla [!DNL Azure Event Hubs] destinazione.

![Dati richiesti nel passaggio di configurazione](/help/rtcdp/destinations/assets/event-hubs-setup-step.png)

## Attivare i segmenti {#activate-segments}

Consulta [Attivare profili e segmenti su una destinazione](/help/rtcdp/destinations/activate-destinations.md) per informazioni sul flusso di lavoro di attivazione dei segmenti.


## Dati esportati {#exported-data}

I [!DNL Experience Platform] dati esportati vengono inviati in formato [!DNL Azure Event Hubs] JSON. Ad esempio, l&#39;evento seguente contiene l&#39;attributo di profilo dell&#39;indirizzo e-mail di un&#39;audience qualificata per un determinato segmento ed uscita da un altro segmento. Le identità di questo potenziale sono ECID ed e-mail.

```
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
>* [Connessione ad Azure Event Hubs e attivazione dei dati tramite chiamate API](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md)
>* [Destinazione Kinesis AWS](/help/rtcdp/destinations/amazon-kinesis-destination.md)
>* [Tipi e categorie di destinazione](/help/rtcdp/destinations/destination-types.md)