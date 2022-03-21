---
keywords: Amazon Kinesis;destinazione kinesis;kinesis
title: (Beta) Connessione Amazon Kinesis
description: Crea una connessione in uscita in tempo reale all’archiviazione Amazon Kinesis per lo streaming dei dati da Adobe Experience Platform.
exl-id: b40117ef-6ad0-48a9-bbcb-97c6f6d1dce3
source-git-commit: c2e726a7e66267bf8f301014ae30dedd7472c693
workflow-type: tm+mt
source-wordcount: '1298'
ht-degree: 1%

---

# (Beta) [!DNL Amazon Kinesis] connection

## Panoramica {#overview}

>[!IMPORTANT]
>
>La [!DNL Amazon Kinesis] la destinazione in Platform è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

La [!DNL Kinesis Data Streams] servizio [!DNL Amazon Web Services] consente di raccogliere ed elaborare grandi flussi di record di dati in tempo reale.

Puoi creare una connessione in uscita in tempo reale al tuo [!DNL Amazon Kinesis] archiviazione per lo streaming dei dati da Adobe Experience Platform.

* Per ulteriori informazioni [!DNL Amazon Kinesis], vedi [Documentazione di Amazon](https://docs.aws.amazon.com/streams/latest/dev/introduction.html).
* Per connettersi a [!DNL Amazon Kinesis] a livello di programmazione, consulta [Esercitazione API per lo streaming delle destinazioni](../../api/streaming-destinations.md).
* Per connettersi a [!DNL Amazon Kinesis] utilizzando l’interfaccia utente di Platform, consulta le sezioni seguenti.

![Amazon Kinesis nell’interfaccia utente](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)

## Casi d’uso {#use-cases}

Utilizzando destinazioni di streaming come [!DNL Amazon Kinesis], puoi facilmente inserire nei tuoi sistemi di scelta gli eventi di segmentazione di alto valore e gli attributi di profilo associati.

Ad esempio, un prospect ha scaricato un white paper che li qualifica in un segmento &quot;alta propensione alla conversione&quot;. Mappando il segmento in cui rientra il potenziale di crescita [!DNL Amazon Kinesis] destinazione, riceverai questo evento in [!DNL Amazon Kinesis]. In questo caso, è possibile utilizzare un approccio fai-da-te e descrivere la logica di business al di sopra dell&#39;evento, in quanto si ritiene che funzionerebbe meglio con i sistemi IT aziendali.

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata seleziona attributi profilo del [flusso di lavoro di attivazione della destinazione](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequenza delle esportazioni | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Obbligatorio [!DNL Amazon Kinesis] permissions {#required-kinesis-permission}

Per connettere ed esportare correttamente i dati al tuo [!DNL Amazon Kinesis] flussi, Experience Platform richiede autorizzazioni per le seguenti azioni:

* `kinesis:ListStreams`
* `kinesis:PutRecord`
* `kinesis:PutRecords`

Queste autorizzazioni sono organizzate tramite [!DNL Kinesis] e vengono controllati da Platform una volta configurata la destinazione Kinesis nell’interfaccia utente di Platform.

L’esempio seguente visualizza i diritti di accesso minimi necessari per esportare correttamente i dati in un [!DNL Kinesis] destinazione.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kinesis:ListStreams",
                "kinesis:PutRecord",
                "kinesis:PutRecords"
            ],
            "Resource": [
                "arn:aws:kinesis:us-east-2:901341027596:stream/*"
            ]
        }
    ]
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `kinesis:ListStreams` | Un’azione che elenca i flussi di dati Kinesis di Amazon. |
| `kinesis:PutRecord` | Azione che scrive un singolo record di dati in un flusso di dati Kinesis. |
| `kinesis:PutRecords` | Azione che scrive più record di dati in un flusso di dati Kinesis in una singola chiamata. |

Per ulteriori informazioni sul controllo dell&#39;accesso per [!DNL Kinesis] flussi di dati, leggi quanto segue [[!DNL Kinesis] documento](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

## Collegati alla destinazione {#connect}

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Quando [configurazione](../../ui/connect-destination.md) questa destinazione, devi fornire le seguenti informazioni:

* **[!DNL Amazon Web Services]chiave di accesso e chiave segreta**: In [!DNL Amazon Web Services], genera un `access key - secret access key` per concedere a Platform l’accesso al tuo [!DNL Amazon Kinesis] conto. Ulteriori informazioni nel [Documentazione di Amazon Web Services](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **regione**: Indicare quale [!DNL Amazon Web Services] da regione a flusso di dati.
* **Nome**: Specifica un nome per la connessione a [!DNL Amazon Kinesis]
* **Descrizione**: Fornire una descrizione della connessione a [!DNL Amazon Kinesis].
* **flusso**: Immetti il nome di un flusso di dati esistente nel tuo [!DNL Amazon Kinesis] conto. Platform esporta i dati in questo flusso.

<!--

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Attiva i segmenti in questa destinazione {#activate}

Vedi [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo in streaming](../../ui/activate-streaming-profile-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

## Comportamento dell’esportazione del profilo {#profile-export-behavior}

Experience Platform ottimizza il comportamento di esportazione del profilo nel tuo [!DNL Amazon Kinesis] per esportare i dati nella destinazione solo quando si sono verificati aggiornamenti rilevanti a un profilo in seguito alla qualifica del segmento o ad altri eventi significativi. I profili vengono esportati nella destinazione nelle situazioni seguenti:

* L’aggiornamento del profilo è stato determinato da una modifica dell’appartenenza al segmento per almeno uno dei segmenti mappati alla destinazione. Ad esempio, il profilo si è qualificato per uno dei segmenti mappati alla destinazione o è uscito da uno dei segmenti mappati alla destinazione.
* L&#39;aggiornamento del profilo è stato determinato da una modifica nel [mappa identità](/help/xdm/field-groups/profile/identitymap.md). Ad esempio, a un profilo già qualificato per uno dei segmenti mappati alla destinazione è stata aggiunta una nuova identità nell’attributo di mappa identità.
* L&#39;aggiornamento del profilo è stato determinato da una modifica degli attributi per almeno uno degli attributi mappati alla destinazione. Ad esempio, uno degli attributi mappati alla destinazione nel passaggio di mappatura viene aggiunto a un profilo.

In tutti i casi descritti in precedenza, vengono esportati nella destinazione solo i profili in cui si sono verificati aggiornamenti rilevanti. Ad esempio, se un segmento mappato al flusso di destinazione ha un centinaio di membri e cinque nuovi profili sono qualificati per il segmento, l’esportazione nella destinazione è incrementale e include solo i cinque nuovi profili.

Tieni presente che tutti gli attributi mappati vengono esportati per un profilo, indipendentemente da dove si trovino le modifiche. Nell’esempio precedente, quindi, tutti gli attributi mappati per questi cinque nuovi profili verranno esportati anche se gli attributi stessi non sono cambiati.

### Cosa determina un’esportazione di dati e cosa è incluso nell’esportazione {#what-determines-export-what-is-included}

Per quanto riguarda i dati esportati per un determinato profilo, è importante comprendere i due diversi concetti di *determina un’esportazione di dati nel tuo [!DNL Amazon Kinesis] destinazione* e *quali dati sono inclusi nell&#39;esportazione*.

| Cosa determina un’esportazione di destinazione | Contenuto dell’esportazione di destinazione |
|---------|----------|
| <ul><li>Gli attributi e i segmenti mappati fungono da spunto per un’esportazione di destinazione. Ciò significa che, se uno dei segmenti mappati cambia stato (da null a Realizzato o da Realizzato/Esistente a Uscire) o qualsiasi attributo mappato viene aggiornato, verrà avviata un’esportazione di destinazione.</li><li>Poiché le identità non possono attualmente essere mappate su [!DNL Amazon Kinesis] le destinazioni, le modifiche apportate a qualsiasi identità in un determinato profilo determinano anche le esportazioni di destinazione.</li><li>Una modifica per un attributo è definita come qualsiasi aggiornamento sull&#39;attributo, che sia o meno lo stesso valore. Ciò significa che una sovrascrittura su un attributo viene considerata una modifica anche se il valore stesso non è stato modificato.</li></ul> | <ul><li>Tutti i segmenti (con lo stato di appartenenza più recente), indipendentemente dal fatto che siano mappati nel flusso di dati o meno, sono inclusi nel `segmentMembership` oggetto.</li><li>Tutte le identità nel `identityMap` sono inclusi anche gli oggetti (l&#39;Experience Platform attualmente non supporta la mappatura dell&#39;identità nel [!DNL Amazon Kinesis] destinazione).</li><li>Solo gli attributi mappati sono inclusi nell’esportazione di destinazione.</li></ul> |

{style=&quot;table-layout:fixed&quot;}

Ad esempio, considera questo flusso di dati come un [!DNL Amazon Kinesis] destinazione in cui tre segmenti sono selezionati nel flusso di dati e quattro attributi sono mappati sulla destinazione.

![Flusso di dati di destinazione di Amazon Kinesis](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Un’esportazione di profilo verso la destinazione può essere determinata da un profilo che qualifica o esce da uno dei *tre segmenti mappati*. Tuttavia, nell’esportazione dei dati, nella `segmentMembership` oggetto (vedere [Dati esportati](#exported-data) di seguito), potrebbero essere visualizzati altri segmenti non mappati, se quel particolare profilo è membro di essi. Se un profilo è idoneo per il segmento Cliente con DeLorean Cars ma è anche membro dei segmenti Orologio &quot;Torna al futuro&quot; film e appassionati di fantascienza, allora questi altri due segmenti saranno anche presenti nel `segmentMembership` oggetto dell’esportazione dei dati, anche se non sono mappati nel flusso di dati.

Dal punto di vista degli attributi del profilo, eventuali modifiche ai quattro attributi mappati sopra determineranno un’esportazione di destinazione e uno qualsiasi dei quattro attributi mappati presenti sul profilo sarà presente nell’esportazione dei dati.

## Dati esportati {#exported-data}

Esportazione [!DNL Experience Platform] i dati arrivano nel tuo [!DNL Amazon Kinesis] destinazione in formato JSON. Ad esempio, l’esportazione seguente contiene un profilo qualificato per un determinato segmento, è membro di altri due segmenti ed è uscita da un altro segmento. L’esportazione include anche il nome dell’attributo del profilo, il cognome, la data di nascita e l’indirizzo e-mail personale. Le identità di questo profilo sono ECID ed e-mail.

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
   "ups":{
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93":{
         "lastQualificationTime":"2022-01-11T21:24:39Z",
         "status":"exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae":{
         "lastQualificationTime":"2022-01-02T23:37:33Z",
         "status":"existing"
      },
      "947c1c46-008d-40b0-92ec-3af86eaf41c1":{
         "lastQualificationTime":"2021-08-25T23:37:33Z",
         "status":"existing"
      },
      "5114d758-ce71-43ba-b53e-e2a91d67b67f":{
         "lastQualificationTime":"2022-01-11T23:37:33Z",
         "status":"realized"
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
>* [Connettiti ad Amazon Kinesis e attiva i dati utilizzando l’API del servizio di flusso](../../api/streaming-destinations.md)
>* [Destinazione degli hub eventi di Azure](./azure-event-hubs.md)
>* [Tipi di destinazione e categorie](../../destination-types.md)

