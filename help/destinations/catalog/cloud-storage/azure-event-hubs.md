---
keywords: Destinazione hub eventi Azure;hub eventi azure;azure eventhub
title: (Beta) [!DNL Azure Event Hubs] connection
description: Crea una connessione in uscita in tempo reale al tuo [!DNL Azure Event Hubs] archiviazione per lo streaming dei dati dall'Experience Platform.
exl-id: f98a389a-bce3-4a80-9452-6c7293d01de3
source-git-commit: b0c2c8313e05d1316f23dc15d99893e1887f8dcf
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 1%

---

# (Beta) [!DNL Azure Event Hubs] connection

## Panoramica {#overview}

>[!IMPORTANT]
>
>La [!DNL Azure Event Hubs] la destinazione in Platform è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

[!DNL Azure Event Hubs] è una piattaforma per lo streaming di dati e un servizio per l’acquisizione di eventi. Può ricevere ed elaborare milioni di eventi al secondo. I dati inviati a un hub eventi possono essere trasformati e memorizzati utilizzando qualsiasi provider di analisi in tempo reale o adattatori di batch/storage.

Puoi creare una connessione in uscita in tempo reale al tuo [!DNL Azure Event Hubs] archiviazione per lo streaming dei dati da Adobe Experience Platform.

* Per ulteriori informazioni [!DNL Azure Event Hubs], vedi [Documentazione di Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* Per connettersi a [!DNL Azure Event Hubs] a livello di programmazione, consulta [Esercitazione API per lo streaming delle destinazioni](../../api/streaming-destinations.md).
* Per connettersi a [!DNL Azure Event Hubs] utilizzando l’interfaccia utente di Platform, consulta le sezioni seguenti.

![AWS Kinesis nell’interfaccia utente](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## Casi di utilizzo {#use-cases}

Utilizzando destinazioni di streaming come [!DNL Azure Event Hubs], puoi facilmente inserire nei tuoi sistemi di scelta gli eventi di segmentazione di alto valore e gli attributi di profilo associati.

Ad esempio, un prospect ha scaricato un white paper che li qualifica in un segmento &quot;alta propensione alla conversione&quot;. Mappando il segmento in cui rientra il potenziale di crescita [!DNL Azure Event Hubs] destinazione, riceverai questo evento in [!DNL Azure Event Hubs]. In questo caso, è possibile utilizzare un approccio fai-da-te e descrivere la logica di business al di sopra dell&#39;evento, in quanto si ritiene che funzionerebbe meglio con i sistemi IT aziendali.

## Tipo di esportazione {#export-type}

**Basato su profilo** - si esportano tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto dalla schermata Seleziona attributi del [flusso di lavoro di attivazione del pubblico](../../ui/activate-streaming-profile-destinations.md#select-attributes).

## Collegati alla destinazione {#connect}

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Quando [configurazione](../../ui/connect-destination.md) questa destinazione, devi fornire le seguenti informazioni:

* **[!UICONTROL Nome chiave SAS]** e **[!UICONTROL Chiave SAS]**: Immettere il nome e la chiave della chiave SAS. Informazioni sull&#39;autenticazione in [!DNL Azure Event Hubs] con le chiavi SAS nel [Documentazione di Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Namespace]**: Riempi il tuo [!DNL Azure Event Hubs] spazio dei nomi. Scopri [!DNL Azure Event Hubs] spazi dei nomi nel [Documentazione di Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).
* **[!UICONTROL Nome]**: Immettere un nome per la connessione a [!DNL Azure Event Hubs].
* **[!UICONTROL Descrizione]**: Fornire una descrizione della connessione.  Esempi: &quot;Clienti di livello Premium&quot;, &quot;Maschi interessati al kitesurfing&quot;.
* **[!UICONTROL eventHubName]**: Fornisci un nome per il flusso al tuo [!DNL Azure Event Hubs] destinazione.

## Attiva i segmenti in questa destinazione {#activate}

Vedi [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo in streaming](../../ui/activate-streaming-profile-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

## Comportamento dell’esportazione del profilo {#profile-export-behavior}

Experience Platform ottimizza il comportamento di esportazione del profilo nella destinazione Azure Event Hubs, in modo da esportare i dati nella destinazione solo quando si sono verificati aggiornamenti rilevanti a un profilo in seguito alla qualifica del segmento o altri eventi significativi. I profili vengono esportati nella destinazione nelle situazioni seguenti:

* L’aggiornamento del profilo è stato attivato da una modifica dell’appartenenza al segmento per almeno uno dei segmenti mappati alla destinazione. Ad esempio, il profilo si è qualificato per uno dei segmenti mappati alla destinazione o è uscito da uno dei segmenti mappati alla destinazione.
* L&#39;aggiornamento del profilo è stato attivato da una modifica nella [mappa identità](/help/xdm/field-groups/profile/identitymap.md). Ad esempio, a un profilo già qualificato per uno dei segmenti mappati alla destinazione è stata aggiunta una nuova identità nell’attributo di mappa identità.
* L’aggiornamento del profilo è stato attivato da una modifica degli attributi per almeno uno degli attributi mappati alla destinazione. Ad esempio, uno degli attributi mappati alla destinazione nel passaggio di mappatura viene aggiunto a un profilo.

In tutti i casi descritti in precedenza, vengono esportati nella destinazione solo i profili in cui si sono verificati aggiornamenti rilevanti. Ad esempio, se un segmento mappato al flusso di destinazione ha un centinaio di membri e cinque nuovi profili sono qualificati per il segmento, l’esportazione nella destinazione è incrementale e include solo i cinque nuovi profili.

Tieni presente che tutti gli attributi mappati vengono esportati per un profilo, indipendentemente da dove si trovino le modifiche. Nell’esempio precedente, quindi, tutti gli attributi mappati per questi cinque nuovi profili verranno esportati anche se gli attributi stessi non sono cambiati.

## Dati esportati {#exported-data}

Esportazione [!DNL Experience Platform] i dati si aprono in [!DNL Azure Event Hubs] in formato JSON. Ad esempio, l’evento seguente contiene l’attributo di profilo dell’indirizzo e-mail di un pubblico qualificato per un determinato segmento ed uscito da un altro segmento. Le identità di questo potenziale cliente sono ECID e e-mail.

```json
{
  "person": {
    "birthDate": "YYYY-MM-DD",
    "name": {
      "firstName": "John",
      "lastName": "Doe"
    }
  },
  "personalEmail": {
    "address": "john.doe@acme.com"
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
>* [Destinazione AWS Kinesis](./amazon-kinesis.md)
>* [Tipi di destinazione e categorie](../../destination-types.md)

