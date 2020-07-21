---
title: destinazione Amazon Kinesis
seo-title: destinazione Amazon Kinesis
description: Crea una connessione in uscita in tempo reale con l'archivio Amazon Kinesis per lo streaming dei dati da  Adobe Experience Platform.
seo-description: Crea una connessione in uscita in tempo reale con l'archivio Amazon Kinesis per lo streaming dei dati da  Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: b96286f6a06f0583b45343a513ee64f0025d79a7
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 2%

---


# (Beta) [!DNL Amazon Kinesis] destinazione


>[!IMPORTANT]
>
>La [!DNL Amazon Kinesis] destinazione in Adobe Real-time CDP è attualmente in versione beta. La documentazione e la funzionalità sono soggette a modifiche.

## Panoramica {#overview}

Il [!DNL Kinesis Data Streams] servizio [!DNL Amazon Web Services] consente di raccogliere ed elaborare grandi flussi di record di dati in tempo reale.

È possibile creare una connessione in uscita in tempo reale allo [!DNL Amazon Kinesis] storage per lo streaming dei dati da  Adobe Experience Platform.

* Per ulteriori informazioni su [!DNL Amazon Kinesis]questo argomento, consultate la documentazione [di](https://docs.aws.amazon.com/streams/latest/dev/introduction.html)Amazon.
* Per connettersi a [!DNL Amazon Kinesis] utilizzando le chiamate API, consulta l’esercitazione [API](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md)Streaming destinations.
* Per collegarsi [!DNL Amazon Kinesis] utilizzando l&#39;interfaccia utente Adobe Real-time CDP, consulta le sezioni riportate di seguito.

![Amazon Kinesis nell’interfaccia utente](/help/rtcdp/destinations/assets/aws-kinesis-destination.png)


## Casi d’uso {#use-cases}

Utilizzando destinazioni di streaming come [!DNL Amazon Kinesis], potete facilmente inserire nei sistemi di vostra scelta eventi di segmentazione di alto valore e attributi di profilo associati.

Ad esempio, un potenziale ha scaricato un white paper che li qualifica come segmento &quot;alta propensione alla conversione&quot;. Mappando il segmento in cui il potenziale rientra nella [!DNL Amazon Kinesis] destinazione, si riceverebbe questo evento in [!DNL Amazon Kinesis]. È possibile utilizzare un approccio &quot;fai da te&quot; e descrivere la logica di business in cima all&#39;evento, come si pensa che funzionerebbe meglio con i sistemi IT aziendali.

## Destinazione Connect {#connect-destination}

Consulta Flusso di lavoro delle destinazioni di archiviazione [Cloud ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)per istruzioni su come connettersi alle destinazioni di archiviazione cloud, comprese quelle supportate da [!DNL Amazon].

Per [!DNL Amazon Kinesis] le destinazioni, immetti le seguenti informazioni nel flusso di lavoro di creazione della destinazione:

### Nel passaggio Autenticazione {#authentication-step}

* **[!DNL Amazon Web Services]chiave di accesso e chiave **segreta: In[!DNL Amazon Web Services], generate una coppia chiave di accesso - chiave di accesso segreta per consentire ad Adobe Real-time CDP di accedere al vostro[!DNL Amazon Kinesis]account. Ulteriori informazioni sono disponibili nella documentazione[](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)Amazon Web Services.
* **regione**: Indicare la [!DNL Amazon Web Services] regione in cui trasmettere i dati in streaming.

![Campi di input nel passaggio dell’account](/help/rtcdp/destinations/assets/aws-kinesis-account-step.png)

### Nel passaggio Configurazione {#setup-step}

* **Nome**: Specifica un nome per la connessione a [!DNL Amazon Kinesis]
* **Descrizione**: Fornire una descrizione della connessione a [!DNL Amazon Kinesis].
* **stream**: Specifica il nome di un flusso di dati esistente nel tuo [!DNL Amazon Kinesis] account. Adobe Real-time CDP esporta i dati in questo flusso.

![Campi di input nel passaggio di autenticazione](/help/rtcdp/destinations/assets/aws-kinesis-setup-step.png)

<!--

>[!IMPORTANT]
>
>Adobe Real-time CDP needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Attivare i segmenti {#activate-segments}

Consulta [Attivare profili e segmenti su una destinazione](/help/rtcdp/destinations/activate-destinations.md) per informazioni sul flusso di lavoro di attivazione dei segmenti.

## Dati esportati {#exported-data}

I [!DNL Experience Platform] dati esportati vengono inviati in formato [!DNL Amazon Kinesis] JSON. Ad esempio, l&#39;evento seguente contiene l&#39;attributo di profilo dell&#39;indirizzo e-mail di un&#39;audience qualificata per un determinato segmento ed uscita da un altro segmento. Le identità di questo potenziale sono ECID ed e-mail.

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
>* [Connessione ad Amazon Kinesis e attivazione dei dati tramite chiamate API](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md)
>* [Destinazione Hubs evento Azure](/help/rtcdp/destinations/azure-event-hubs-destination.md)
>* [Tipi e categorie di destinazione](/help/rtcdp/destinations/destination-types.md)

