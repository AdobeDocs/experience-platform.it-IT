---
keywords: Destinazione hub eventi Azure;hub eventi azure;azure eventhub
title: Connessione hub eventi di Azure
description: Crea una connessione in uscita in tempo reale al tuo [!DNL Azure Event Hubs] archiviazione per lo streaming dei dati dall'Experience Platform.
exl-id: f98a389a-bce3-4a80-9452-6c7293d01de3
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '2004'
ht-degree: 0%

---

# [!DNL Azure Event Hubs] connection

## Panoramica {#overview}

>[!IMPORTANT]
>
> Questa destinazione è disponibile solo per [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) clienti.

[!DNL Azure Event Hubs] è una piattaforma per lo streaming di dati e un servizio per l’acquisizione di eventi. Può ricevere ed elaborare milioni di eventi al secondo. I dati inviati a un hub eventi possono essere trasformati e memorizzati utilizzando qualsiasi provider di analisi in tempo reale o adattatori di batch/storage.

Puoi creare una connessione in uscita in tempo reale al tuo [!DNL Azure Event Hubs] archiviazione per lo streaming dei dati da Adobe Experience Platform.

* Per ulteriori informazioni [!DNL Azure Event Hubs], vedi [Documentazione di Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* Per connettersi a [!DNL Azure Event Hubs] a livello di programmazione, consulta [Esercitazione API per lo streaming delle destinazioni](../../api/streaming-destinations.md).
* Per connettersi a [!DNL Azure Event Hubs] utilizzando l’interfaccia utente di Platform, consulta le sezioni seguenti.

![AWS Kinesis nell’interfaccia utente](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## Casi di utilizzo {#use-cases}

Utilizzando destinazioni di streaming come [!DNL Azure Event Hubs], puoi facilmente inserire nei tuoi sistemi di scelta gli eventi di segmentazione di alto valore e gli attributi di profilo associati.

Ad esempio, un prospect ha scaricato un white paper che li qualifica in un segmento &quot;alta propensione alla conversione&quot;. Mappando il segmento in cui rientra il potenziale di crescita [!DNL Azure Event Hubs] destinazione, riceverai questo evento in [!DNL Azure Event Hubs]. In questo caso, è possibile utilizzare un approccio fai-da-te e descrivere la logica di business al di sopra dell&#39;evento, in quanto si ritiene che funzionerebbe meglio con i sistemi IT aziendali.

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata seleziona attributi profilo del [flusso di lavoro di attivazione della destinazione](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequenza delle esportazioni | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## inserire nell&#39;elenco Consentiti indirizzo IP {#ip-address-allowlist}

Per soddisfare i requisiti di sicurezza e conformità dei clienti, Experience Platform fornisce un elenco di IP statici che puoi inserire nell&#39;elenco Consentiti per [!DNL Azure Event Hubs] destinazione. Fai riferimento a [ELENCO CONSENTITI di indirizzi IP per le destinazioni di streaming](/help/destinations/catalog/streaming/ip-address-allow-list.md) per l’elenco completo degli IP da inserire nell&#39;elenco Consentiti.

## Collegati alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Quando ti connetti a questa destinazione, devi fornire le seguenti informazioni:

### Informazioni di autenticazione {#authentication-information}

#### Autenticazione standard {#standard-authentication}

![Immagine della schermata dell’interfaccia utente che mostra i campi completati per i dettagli di autenticazione standard degli hub eventi di Azure](../../assets/catalog/cloud-storage/event-hubs/event-hubs-standard-authentication.png)

Se selezioni la **[!UICONTROL Autenticazione standard]** digita per connettersi all’endpoint HTTP, immetti i campi seguenti e seleziona **[!UICONTROL Connetti alla destinazione]**:

* **[!UICONTROL Nome chiave SAS]**: Nome della regola di autorizzazione, noto anche come nome della chiave SAS.
* **[!UICONTROL Chiave SAS]**: Chiave primaria dello spazio dei nomi Hubs evento. La `sasPolicy` che `sasKey` corrisponde a **gestire** diritti configurati per popolare l’elenco Hub eventi. Informazioni sull&#39;autenticazione in [!DNL Azure Event Hubs] con le chiavi SAS nel [Documentazione di Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Namespace]**: Riempi il tuo [!DNL Azure Event Hubs] spazio dei nomi. Scopri [!DNL Azure Event Hubs] spazi dei nomi nel [Documentazione di Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).

#### Autenticazione SAS (Shared Access Signature) {#sas-authentication}

![Immagine della schermata dell’interfaccia utente che mostra i campi completati per i dettagli di autenticazione standard degli hub eventi di Azure](../../assets/catalog/cloud-storage/event-hubs/event-hubs-sas-authentication.png)

Se selezioni la **[!UICONTROL Autenticazione standard]** digita per connettersi all’endpoint HTTP, immetti i campi seguenti e seleziona **[!UICONTROL Connetti alla destinazione]**:

* **[!UICONTROL Nome chiave SAS]**: Nome della regola di autorizzazione, noto anche come nome della chiave SAS.
* **[!UICONTROL Chiave SAS]**: Chiave primaria dello spazio dei nomi Hubs evento. La `sasPolicy` che `sasKey` corrisponde a **gestire** diritti configurati per popolare l’elenco Hub eventi. Informazioni sull&#39;autenticazione in [!DNL Azure Event Hubs] con le chiavi SAS nel [Documentazione di Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Namespace]**: Riempi il tuo [!DNL Azure Event Hubs] spazio dei nomi. Scopri [!DNL Azure Event Hubs] spazi dei nomi nel [Documentazione di Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).
* **[!UICONTROL Namespace]**: Riempi il tuo [!DNL Azure Event Hubs] spazio dei nomi. Scopri [!DNL Azure Event Hubs] spazi dei nomi nel [Documentazione di Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).

### Compila i dettagli della destinazione {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_eventhubs_includesegmentnames"
>title="Includi nomi dei segmenti"
>abstract="Attiva/disattiva se desideri che l’esportazione dei dati includa i nomi dei segmenti che stai esportando. Visualizza la documentazione di un esempio di esportazione dei dati con questa opzione selezionata."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_eventhubs_includesegmenttimestamps"
>title="Includi marche temporali del segmento"
>abstract="Attiva/disattiva se desideri che l’esportazione dei dati includa la marca temporale UNIX al momento della creazione e dell’aggiornamento dei segmenti, nonché la marca temporale UNIX al momento della mappatura dei segmenti alla destinazione per l’attivazione. Visualizza la documentazione di un esempio di esportazione dei dati con questa opzione selezionata."

Per configurare i dettagli della destinazione, compila i campi obbligatori e facoltativi riportati di seguito. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

![Immagine della schermata dell’interfaccia utente che mostra i campi completati per i dettagli della destinazione Azure Event Hubs](../../assets/catalog/cloud-storage/event-hubs/event-hubs-destination-details.png)

* **[!UICONTROL Nome]**: Immettere un nome per la connessione a [!DNL Azure Event Hubs].
* **[!UICONTROL Descrizione]**: Fornire una descrizione della connessione.  Esempi: &quot;Clienti di livello Premium&quot;, &quot;Clienti interessati a kitesurfing&quot;.
* **[!UICONTROL eventHubName]**: Fornisci un nome per il flusso al tuo [!DNL Azure Event Hubs] destinazione.
* **[!UICONTROL Includi nomi dei segmenti]**: Attiva/disattiva se desideri che l’esportazione dei dati includa i nomi dei segmenti che stai esportando. Per un esempio di esportazione di dati con questa opzione selezionata, consulta [Dati esportati](#exported-data) più avanti.
* **[!UICONTROL Includi marche temporali del segmento]**: Attiva/disattiva se desideri che l’esportazione dei dati includa la marca temporale UNIX al momento della creazione e dell’aggiornamento dei segmenti, nonché la marca temporale UNIX al momento della mappatura dei segmenti alla destinazione per l’attivazione. Per un esempio di esportazione di dati con questa opzione selezionata, consulta [Dati esportati](#exported-data) più avanti.

### Abilitare gli avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati nella tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere le notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [iscrizione agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completati i dettagli della connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Vedi [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo in streaming](../../ui/activate-streaming-profile-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

## Comportamento dell’esportazione del profilo {#profile-export-behavior}

Experience Platform ottimizza il comportamento di esportazione del profilo nel tuo [!DNL Azure Event Hubs] per esportare i dati nella destinazione solo quando si sono verificati aggiornamenti rilevanti a un profilo in seguito alla qualifica del segmento o ad altri eventi significativi. I profili vengono esportati nella destinazione nelle situazioni seguenti:

* L’aggiornamento del profilo è stato determinato da una modifica dell’appartenenza al segmento per almeno uno dei segmenti mappati alla destinazione. Ad esempio, il profilo si è qualificato per uno dei segmenti mappati alla destinazione o è uscito da uno dei segmenti mappati alla destinazione.
* L&#39;aggiornamento del profilo è stato determinato da una modifica nel [mappa identità](/help/xdm/field-groups/profile/identitymap.md). Ad esempio, a un profilo già qualificato per uno dei segmenti mappati alla destinazione è stata aggiunta una nuova identità nell’attributo di mappa identità.
* L&#39;aggiornamento del profilo è stato determinato da una modifica degli attributi per almeno uno degli attributi mappati alla destinazione. Ad esempio, uno degli attributi mappati alla destinazione nel passaggio di mappatura viene aggiunto a un profilo.

In tutti i casi descritti in precedenza, vengono esportati nella destinazione solo i profili in cui si sono verificati aggiornamenti rilevanti. Ad esempio, se un segmento mappato al flusso di destinazione ha un centinaio di membri e cinque nuovi profili sono qualificati per il segmento, l’esportazione nella destinazione è incrementale e include solo i cinque nuovi profili.

Tieni presente che tutti gli attributi mappati vengono esportati per un profilo, indipendentemente da dove si trovino le modifiche. Nell’esempio precedente, quindi, tutti gli attributi mappati per questi cinque nuovi profili verranno esportati anche se gli attributi stessi non sono cambiati.

### Cosa determina un’esportazione di dati e cosa è incluso nell’esportazione {#what-determines-export-what-is-included}

Per quanto riguarda i dati esportati per un determinato profilo, è importante comprendere i due diversi concetti di *determina un’esportazione di dati nel tuo [!DNL Azure Event Hubs] destinazione* e *quali dati sono inclusi nell&#39;esportazione*.

| Cosa determina un’esportazione di destinazione | Contenuto dell’esportazione di destinazione |
|---------|----------|
| <ul><li>Gli attributi e i segmenti mappati fungono da spunto per un’esportazione di destinazione. Ciò significa che, se uno dei segmenti mappati cambia stato (da null a Realizzato o da Realizzato/Esistente a Uscire) o qualsiasi attributo mappato viene aggiornato, verrà avviata un’esportazione di destinazione.</li><li>Poiché le identità non possono attualmente essere mappate su [!DNL Azure Event Hubs] le destinazioni, le modifiche apportate a qualsiasi identità in un determinato profilo determinano anche le esportazioni di destinazione.</li><li>Una modifica per un attributo è definita come qualsiasi aggiornamento sull&#39;attributo, che sia o meno lo stesso valore. Ciò significa che una sovrascrittura su un attributo viene considerata una modifica anche se il valore stesso non è stato modificato.</li></ul> | <ul><li>Tutti i segmenti (con lo stato di appartenenza più recente), indipendentemente dal fatto che siano mappati nel flusso di dati o meno, sono inclusi nel `segmentMembership` oggetto.</li><li>Tutte le identità nel `identityMap` sono inclusi anche gli oggetti (l&#39;Experience Platform attualmente non supporta la mappatura dell&#39;identità nel [!DNL Azure Event Hubs] destinazione).</li><li>Solo gli attributi mappati sono inclusi nell’esportazione di destinazione.</li></ul> |

{style=&quot;table-layout:fixed&quot;}

Ad esempio, considera questo flusso di dati come un [!DNL Azure Event Hubs] destinazione in cui tre segmenti sono selezionati nel flusso di dati e quattro attributi sono mappati sulla destinazione.

![Flusso di dati di destinazione di Amazon Kinesis](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Un’esportazione di profilo verso la destinazione può essere determinata da un profilo che qualifica o esce da uno dei *tre segmenti mappati*. Tuttavia, nell’esportazione dei dati, nella `segmentMembership` oggetto (vedere [Dati esportati](#exported-data) di seguito), potrebbero essere visualizzati altri segmenti non mappati, se quel particolare profilo è membro di essi. Se un profilo è idoneo per il segmento Cliente con DeLorean Cars ma è anche membro dei segmenti Orologio &quot;Torna al futuro&quot; film e appassionati di fantascienza, allora questi altri due segmenti saranno anche presenti nel `segmentMembership` oggetto dell’esportazione dei dati, anche se non sono mappati nel flusso di dati.

Dal punto di vista degli attributi del profilo, eventuali modifiche ai quattro attributi mappati sopra determineranno un’esportazione di destinazione e uno qualsiasi dei quattro attributi mappati presenti sul profilo sarà presente nell’esportazione dei dati.

## Recupero dati storici {#historical-data-backfill}

Quando aggiungi un nuovo segmento a una destinazione esistente o quando crei una nuova destinazione e mappi segmenti su di essa, Experience Platform esporta i dati storici di qualificazione dei segmenti alla destinazione. Profili qualificati per il segmento *prima* il segmento aggiunto alla destinazione viene esportato nella destinazione entro circa un’ora.

## Dati esportati {#exported-data}

Esportazione [!DNL Experience Platform] i dati arrivano nel tuo [!DNL Azure Event Hubs] destinazione in formato JSON. Ad esempio, l’esportazione seguente contiene un profilo qualificato per un determinato segmento, è membro di altri due segmenti ed è uscita da un altro segmento. L’esportazione include anche il nome dell’attributo del profilo, il cognome, la data di nascita e l’indirizzo e-mail personale. Le identità di questo profilo sono ECID ed e-mail.

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

Di seguito sono riportati ulteriori esempi di dati esportati, a seconda delle impostazioni dell’interfaccia utente selezionate nel flusso di destinazione di connessione per il **[!UICONTROL Includi nomi dei segmenti]** e **[!UICONTROL Includi marche temporali del segmento]** opzioni:

+++ L’esempio di esportazione dei dati riportato di seguito include i nomi dei segmenti nel `segmentMembership` sezione

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "existing",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
            "name": "First name equals John"
          }
        }
      }
```

+++

+++ L’esempio di esportazione dei dati riportato di seguito include le marche temporali del segmento nel `segmentMembership` sezione

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "existing",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
          }
        }
      }
```

+++

## Limiti e nuovo criterio {#limits-retry-policy}

Nel 95% del tempo, Experience Platform tenta di offrire una latenza di throughput inferiore a 10 minuti per i messaggi inviati con successo con un tasso di meno di 10 mila richieste al secondo per ogni flusso di dati a una destinazione HTTP.

In caso di richieste non riuscite alla destinazione API HTTP, Experience Platform memorizza le richieste non riuscite e tenta due volte di inviare le richieste all’endpoint.

>[!MORELIKETHIS]
>
>* [Connettersi agli hub eventi di Azure e attivare i dati utilizzando l’API del servizio di flusso](../../api/streaming-destinations.md)
>* [Destinazione AWS Kinesis](./amazon-kinesis.md)
>* [Tipi di destinazione e categorie](../../destination-types.md)

