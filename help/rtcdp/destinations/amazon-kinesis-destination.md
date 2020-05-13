---
title: destinazione Amazon Kinesis
seo-title: destinazione Amazon Kinesis
description: Crea una connessione in uscita in tempo reale con il tuo archivio Amazon Kinesis per lo streaming dei dati da Adobe Experience Platform.
seo-description: Crea una connessione in uscita in tempo reale con il tuo archivio Amazon Kinesis per lo streaming dei dati da Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: a18f89531cf024f61b054b47a660bd26766bebf6
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 0%

---


# destinazione Amazon Kinesis

## Panoramica {#overview}

Il [!DNL Kinesis Data Streams] servizio di Amazon Web Services consente di raccogliere ed elaborare grandi flussi di record di dati in tempo reale.

È possibile creare una connessione in uscita in tempo reale allo [!DNL Amazon Kinesis] storage per lo streaming dei dati da Adobe Experience Platform.

* Per ulteriori informazioni su [!DNL Amazon Kinesis]questo argomento, consultate la documentazione [di](https://docs.aws.amazon.com/streams/latest/dev/introduction.html)Amazon.
* Per connettersi a [!DNL Amazon Kinesis] utilizzando le chiamate API, consulta l’esercitazione [API]Streaming destinations.
* Per collegarsi [!DNL Amazon Kinesis] utilizzando l&#39;interfaccia utente Adobe Real-time CDP, consulta le sezioni riportate di seguito.

![Amazon Kinesis nell’interfaccia utente](/help/rtcdp/destinations/assets/aws-kinesis-destination.png)


## Casi d’uso {#use-cases}

Utilizzando le destinazioni di streaming come Amazon Kinesis, potete facilmente inserire nei vostri sistemi di scelta eventi di segmentazione di alto valore e attributi di profilo associati.

Ad esempio, un potenziale ha scaricato un white paper che li qualifica come segmento &quot;alta propensione alla conversione&quot;. Mappando il segmento in cui il potenziale rientra nella destinazione Amazon Kinesis, si riceverà questo evento in Amazon Kinesis. È possibile utilizzare un approccio &quot;fai da te&quot; e descrivere la logica di business in cima all&#39;evento, come si pensa che funzionerebbe meglio con i sistemi IT aziendali.

## Destinazione Connect {#connect-destination}

Consulta Flusso di lavoro delle destinazioni di archiviazione [Cloud ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)per istruzioni su come connettersi alle destinazioni di archiviazione cloud, comprese quelle supportate da [!DNL Amazon].

Per [!DNL Amazon Kinesis] le destinazioni, immetti le seguenti informazioni nel flusso di lavoro di creazione della destinazione:

### Nel passaggio Account {#account-step}

* **Chiave di accesso e chiave** segreta di Amazon Web Services: In [!DNL Amazon Web Services], generate una coppia chiave di accesso - chiave di accesso segreta per consentire ad Adobe Real-time CDP di accedere al vostro [!DNL Amazon Kinesis] account. Ulteriori informazioni sono disponibili nella documentazione [](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)Amazon Web Services.
* **regione**: Indicare la [!DNL Amazon Web Services] regione in cui trasmettere i dati in streaming.

![Campi di input nel passaggio dell’account](/help/rtcdp/destinations/assets/aws-kinesis-account-step.png)

### Nel passaggio Autenticazione {#authentication-step}

* **Nome**: Specifica un nome per la connessione a [!DNL Amazon Kinesis]
* **Descrizione**: Fornire una descrizione della connessione a [!DNL Amazon Kinesis].
* **stream**: Specifica il nome del flusso di dati esistente nel tuo [!DNL Amazon Kinesis] account. Adobe Real-time CDP esporta i dati in questo flusso.

![Campi di input nel passaggio di autenticazione](/help/rtcdp/destinations/assets/aws-kinesis-authentication-step.png)

<!--

>[!IMPORTANT]
>
>Adobe Real-time CDP needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Attivare i segmenti {#activate-segments}

Consulta [Attivare profili e segmenti su una destinazione](/help/rtcdp/destinations/activate-destinations.md) per informazioni sul flusso di lavoro di attivazione dei segmenti.

## Dati esportati {#exported-data}

I dati della piattaforma Experience vengono esportati in formato [!DNL Amazon Kinesis] JSON. Ad esempio, un evento contenente l&#39;identità e-mail con hash di un&#39;audience che è uscita da un determinato segmento potrebbe essere simile al seguente:

```
{
   "segmentMembership":{
      "ups":{
         "7841ba61-23c1-4bb3-a495-00d695fe1e93":{
            "lastQualificationTime":"2020-03-03T21:24:39Z",
            "status":"exited"
         }
      }
   }
},
"identityMap":{
   "email_lc_sha256":[
      {
         "id":"655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
         "id":"66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
   ]
},
```



>[!MORELIKETHIS]
>
>* Collegamento all’esercitazione API Amazon Kinesis
>* [Destinazione Hubs evento Azure](/help/rtcdp/destinations/azure-event-hubs-destination.md)
>* [Tipi e categorie di destinazione](/help/rtcdp/destinations/destination-types.md)

