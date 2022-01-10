---
keywords: Amazon Kinesis;destinazione kinesis;kinesis
title: Connessione Amazon Kinesis
description: Crea una connessione in uscita in tempo reale all’archiviazione Amazon Kinesis per lo streaming dei dati da Adobe Experience Platform.
exl-id: b40117ef-6ad0-48a9-bbcb-97c6f6d1dce3
source-git-commit: f7f3bc229ddad046dca5ea8d2889942fc9cb2cab
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

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

## Tipo di esportazione {#export-type}

**Basato su profilo** - si esportano tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto dalla schermata Seleziona attributi del [flusso di lavoro di attivazione del pubblico](../../ui/activate-streaming-profile-destinations.md#select-attributes).

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

Experience Platform ottimizza il comportamento di esportazione del profilo nella destinazione Amazon Kinesis, in modo da esportare i dati nella destinazione solo quando si sono verificati aggiornamenti rilevanti a un profilo in seguito alla qualifica del segmento o altri eventi significativi. I profili vengono esportati nella destinazione nelle situazioni seguenti:

* L’aggiornamento del profilo è stato attivato da una modifica dell’appartenenza al segmento per almeno uno dei segmenti mappati alla destinazione. Ad esempio, il profilo si è qualificato per uno dei segmenti mappati alla destinazione o è uscito da uno dei segmenti mappati alla destinazione.
* L&#39;aggiornamento del profilo è stato attivato da una modifica nella [mappa identità](/help/xdm/field-groups/profile/identitymap.md). Ad esempio, a un profilo già qualificato per uno dei segmenti mappati alla destinazione è stata aggiunta una nuova identità nell’attributo di mappa identità.
* L’aggiornamento del profilo è stato attivato da una modifica degli attributi per almeno uno degli attributi mappati alla destinazione. Ad esempio, uno degli attributi mappati alla destinazione nel passaggio di mappatura viene aggiunto a un profilo.

In tutti i casi descritti in precedenza, vengono esportati nella destinazione solo i profili in cui si sono verificati aggiornamenti rilevanti. Ad esempio, se un segmento mappato al flusso di destinazione ha un centinaio di membri e cinque nuovi profili sono qualificati per il segmento, l’esportazione nella destinazione è incrementale e include solo i cinque nuovi profili.

Tieni presente che tutti gli attributi mappati vengono esportati per un profilo, indipendentemente da dove si trovino le modifiche. Nell’esempio precedente, quindi, tutti gli attributi mappati per questi cinque nuovi profili verranno esportati anche se gli attributi stessi non sono cambiati.

## Dati esportati {#exported-data}

Esportazione [!DNL Experience Platform] i dati si aprono in [!DNL Amazon Kinesis] in formato JSON. Ad esempio, l’evento seguente contiene l’attributo di profilo dell’indirizzo e-mail di un pubblico qualificato per un determinato segmento ed uscito da un altro segmento. Le identità di questo potenziale cliente sono ECID e e-mail.

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
>* [Connettiti ad Amazon Kinesis e attiva i dati utilizzando l’API del servizio di flusso](../../api/streaming-destinations.md)
>* [Destinazione degli hub eventi di Azure](./azure-event-hubs.md)
>* [Tipi di destinazione e categorie](../../destination-types.md)

