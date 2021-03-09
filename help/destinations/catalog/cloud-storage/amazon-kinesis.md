---
keywords: Amazon Kinesis;destinazione kinesis;kinesis
title: Connessione Amazon Kinesis
description: Crea una connessione in uscita in tempo reale all’archiviazione Amazon Kinesis per lo streaming dei dati da Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 32cb198bcf2c142b50c4b7a60282f0c923be06b1
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 2%

---


# (Beta) Connessione [!DNL Amazon Kinesis]

>[!IMPORTANT]
>
>La destinazione [!DNL Amazon Kinesis] in Platform è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

Il servizio [!DNL Kinesis Data Streams] di [!DNL Amazon Web Services] ti consente di raccogliere ed elaborare grandi flussi di record di dati in tempo reale.

Puoi creare una connessione in uscita in tempo reale allo storage [!DNL Amazon Kinesis] per lo streaming dei dati da Adobe Experience Platform.

* Per ulteriori informazioni su [!DNL Amazon Kinesis], consulta la [documentazione di Amazon](https://docs.aws.amazon.com/streams/latest/dev/introduction.html).
* Per connetterti a [!DNL Amazon Kinesis] a livello di programmazione, consulta l’ [esercitazione API sulle destinazioni di streaming](../../api/streaming-destinations.md) .
* Per effettuare la connessione a [!DNL Amazon Kinesis] utilizzando l’interfaccia utente di Platform, consulta le sezioni seguenti.

![Amazon Kinesis nell’interfaccia utente](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)

## Casi d’uso {#use-cases}

Utilizzando destinazioni di streaming come [!DNL Amazon Kinesis], puoi facilmente inserire nei tuoi sistemi selezionati eventi di segmentazione di alto valore e attributi di profilo associati.

Ad esempio, un prospect ha scaricato un white paper che li qualifica in un segmento &quot;alta propensione alla conversione&quot;. Mappando il segmento in cui il potenziale di crescita rientra nella destinazione [!DNL Amazon Kinesis], riceverai questo evento in [!DNL Amazon Kinesis]. In questo caso, è possibile utilizzare un approccio fai-da-te e descrivere la logica di business al di sopra dell&#39;evento, in quanto si ritiene che funzionerebbe meglio con i sistemi IT aziendali.

## Tipo di esportazione {#export-type}

**Basato su profilo** : stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto dalla schermata seleziona attributi del flusso di lavoro [ di attivazione della ](../../ui/activate-destinations.md#select-attributes)destinazione.

## Collegare la destinazione {#connect-destination}

Per istruzioni su come connettersi alle destinazioni di archiviazione cloud, incluse quelle supportate da [!DNL Amazon], consulta [Flusso di lavoro per le destinazioni di archiviazione cloud ](./workflow.md).

Per le destinazioni [!DNL Amazon Kinesis] , inserisci le seguenti informazioni nel flusso di lavoro crea destinazione :

### Nel passaggio Autenticazione {#authentication-step}

* **[!DNL Amazon Web Services]chiave di accesso e chiave** segreta: In  [!DNL Amazon Web Services], genera una  `access key - secret access key` coppia per concedere a Platform l’accesso al tuo  [!DNL Amazon Kinesis] account. Ulteriori informazioni sono disponibili nella [documentazione di Amazon Web Services](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **regione**: Indicare la  [!DNL Amazon Web Services] regione a cui inviare i dati.

![Campi di input nel passaggio dell’account](../../assets/catalog/cloud-storage/amazon-kinesis/account.png)

### Nel passaggio Configurazione {#setup-step}

* **Nome**: Specifica un nome per la connessione a  [!DNL Amazon Kinesis]
* **Descrizione**: Immetti una descrizione della connessione a  [!DNL Amazon Kinesis].
* **flusso**: Immetti il nome di un flusso di dati esistente nel tuo  [!DNL Amazon Kinesis] account. Platform esporta i dati in questo flusso.
* **[!UICONTROL Marketing actions]**: Le azioni di marketing indicano l’intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra azioni di marketing definite da Adobi o creare una tua azione di marketing. Per ulteriori informazioni sulle azioni di marketing, consulta la pagina [Governance dei dati in Adobe Experience Platform](../../../data-governance/policies/overview.md) . Per informazioni sulle singole azioni di marketing definite da Adobe, consulta la [Panoramica sui criteri di utilizzo dei dati](../../../data-governance/policies/overview.md).

![Campi di input nel passaggio di autenticazione](../../assets/catalog/cloud-storage/amazon-kinesis/setup.png)

<!--

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Attiva segmenti {#activate-segments}

Per informazioni sul flusso di lavoro di attivazione dei segmenti, consulta [Attivare profili e segmenti su una destinazione](../../ui/activate-destinations.md) .

## Dati esportati {#exported-data}

I dati esportati [!DNL Experience Platform] arrivano in [!DNL Amazon Kinesis] in formato JSON. Ad esempio, l’evento seguente contiene l’attributo di profilo dell’indirizzo e-mail di un pubblico qualificato per un determinato segmento ed uscito da un altro segmento. Le identità di questo potenziale cliente sono ECID e e-mail.

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
>* [Connettiti ad Amazon Kinesis e attiva i dati utilizzando l’API del servizio di flusso](../../api/streaming-destinations.md)
>* [Destinazione degli hub eventi di Azure](./azure-event-hubs.md)
>* [Tipi di destinazione e categorie](../../destination-types.md)

