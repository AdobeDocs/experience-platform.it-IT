---
keywords: Destinazione hub eventi di Azure;hub eventi di Azure;azure eventub
title: Connessione Azure Event Hubs
description: Crea una connessione in uscita in tempo reale all'archivio  [!DNL Azure Event Hubs]  per inviare dati da Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: f98a389a-bce3-4a80-9452-6c7293d01de3
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '2087'
ht-degree: 5%

---

# Connessione [!DNL Azure Event Hubs]

## Panoramica {#overview}

>[!IMPORTANT]
>
> Questa destinazione è disponibile solo per [clienti Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/it/legal/product-descriptions/real-time-customer-data-platform.html).

[!DNL Azure Event Hubs] è una piattaforma di streaming di big data e un servizio di acquisizione di eventi. Può ricevere ed elaborare milioni di eventi al secondo. I dati inviati a un hub eventi possono essere trasformati e memorizzati utilizzando qualsiasi provider di analisi in tempo reale o adattatori di batch/archiviazione.

È possibile creare una connessione in uscita in tempo reale all&#39;archivio [!DNL Azure Event Hubs] per eseguire lo streaming dei dati da Adobe Experience Platform.

* Per ulteriori informazioni su [!DNL Azure Event Hubs], consulta la [documentazione di Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* Per connettersi a [!DNL Azure Event Hubs] a livello di programmazione, vedere l&#39;esercitazione sull&#39;API delle [destinazioni di streaming](../../api/streaming-destinations.md).
* Per connettersi a [!DNL Azure Event Hubs] tramite l&#39;interfaccia utente di Platform, vedere le sezioni seguenti.

![AWS Kinesis nell&#39;interfaccia utente](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## Casi d’uso {#use-cases}

Utilizzando destinazioni di streaming come [!DNL Azure Event Hubs], puoi inserire facilmente eventi di segmentazione di alto valore e attributi di profilo associati nei sistemi preferiti.

Ad esempio, un potenziale cliente ha scaricato un white paper che li qualifica come segmenti ad &quot;alta propensione alla conversione&quot;. Mappando il pubblico in cui rientra il potenziale cliente alla destinazione [!DNL Azure Event Hubs], riceverai questo evento in [!DNL Azure Event Hubs]. In questo caso, è possibile utilizzare un approccio fai-da-te e descrivere la logica di business oltre all&#39;evento, in base al principio che si potrebbe utilizzare al meglio con i sistemi IT aziendali.

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive quali tipi di pubblico puoi esportare in questa destinazione.

| Origine pubblico | Supportato | Descrizione |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati tramite il servizio di segmentazione [Experience Platform](../../../segmentation/home.md). |
| Caricamenti personalizzati | ✓ | Tipi di pubblico [importati](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata seleziona attributi profilo del [flusso di lavoro di attivazione della destinazione](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Indirizzo IP inserisco nell&#39;elenco Consentiti {#ip-address-allowlist}

Per soddisfare i requisiti di sicurezza e conformità dei clienti, Experience Platform inserire nell&#39;elenco Consentiti fornisce un elenco di IP statici che è possibile per la destinazione [!DNL Azure Event Hubs]. Per l&#39;elenco completo degli IP da elenco consentiti, consulta l&#39;[elenco Consentiti di indirizzo IP per le destinazioni di streaming](/help/destinations/catalog/streaming/ip-address-allow-list.md).

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Quando ti connetti a questa destinazione, devi fornire le seguenti informazioni:

### Informazioni di autenticazione {#authentication-information}

#### Autenticazione standard {#standard-authentication}

![Immagine della schermata dell&#39;interfaccia utente che mostra i campi completati per i dettagli di autenticazione standard di Azure Event Hubs](../../assets/catalog/cloud-storage/event-hubs/event-hubs-standard-authentication.png)

Se si seleziona il tipo **[!UICONTROL Autenticazione standard]** per connettersi all&#39;endpoint HTTP, immettere i campi seguenti e selezionare **[!UICONTROL Connetti alla destinazione]**:

* **[!UICONTROL Nome chiave SAS]**: nome della regola di autorizzazione, noto anche come nome della chiave SAS.
* **[!UICONTROL Chiave SAS]**: chiave primaria dello spazio dei nomi degli hub eventi. I `sasPolicy` a cui corrisponde `sasKey` devono avere i diritti **manage** configurati per compilare l&#39;elenco degli hub eventi. Scopri come eseguire l&#39;autenticazione in [!DNL Azure Event Hubs] con le chiavi SAS nella [documentazione di Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Spazio dei nomi]**: compila il tuo spazio dei nomi [!DNL Azure Event Hubs]. Scopri gli spazi dei nomi [!DNL Azure Event Hubs] nella [documentazione di Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).

#### Autenticazione con firma di accesso condiviso (SAS) {#sas-authentication}

![Immagine della schermata dell&#39;interfaccia utente che mostra i campi completati per i dettagli di autenticazione standard di Azure Event Hubs](../../assets/catalog/cloud-storage/event-hubs/event-hubs-sas-authentication.png)

Se si seleziona il tipo **[!UICONTROL Autenticazione standard]** per connettersi all&#39;endpoint HTTP, immettere i campi seguenti e selezionare **[!UICONTROL Connetti alla destinazione]**:

* **[!UICONTROL Nome chiave SAS]**: nome della regola di autorizzazione, noto anche come nome della chiave SAS.
* **[!UICONTROL Chiave SAS]**: chiave primaria dello spazio dei nomi degli hub eventi. I `sasPolicy` a cui corrisponde `sasKey` devono avere i diritti **manage** configurati per compilare l&#39;elenco degli hub eventi. Scopri come eseguire l&#39;autenticazione in [!DNL Azure Event Hubs] con le chiavi SAS nella [documentazione di Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Spazio dei nomi]**: compila il tuo spazio dei nomi [!DNL Azure Event Hubs]. Scopri gli spazi dei nomi [!DNL Azure Event Hubs] nella [documentazione di Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).
* **[!UICONTROL Nome hub eventi]**: immettere il nome [!DNL Azure Event Hub]. Scopri i nomi di [!DNL Azure Event Hubs] nella [documentazione di Microsoft](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub).

### Inserire i dettagli della destinazione {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_eventhubs_includesegmentnames"
>title="Includi nomi dei segmenti"
>abstract="Attiva o disattiva questa opzione se desideri che l’esportazione dei dati includa i nomi dei tipi di pubblico che stai esportando. Consulta la documentazione per vedere un esempio di esportazione dei dati con questa opzione selezionata."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_eventhubs_includesegmenttimestamps"
>title="Includi timestamp dei segmenti"
>abstract="Attiva o disattiva questa opzione se desideri che l’esportazione dei dati includa il timestamp UNIX al momento della creazione e dell’aggiornamento dei tipi di pubblico, nonché il timestamp UNIX al momento della mappatura dei tipi di pubblico sulla destinazione per l’attivazione. Consulta la documentazione per vedere un esempio di esportazione dei dati con questa opzione selezionata."

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

![Immagine della schermata dell&#39;interfaccia utente che mostra i campi completati per i dettagli di destinazione degli hub eventi di Azure](../../assets/catalog/cloud-storage/event-hubs/event-hubs-destination-details.png)

* **[!UICONTROL Nome]**: immettere un nome per la connessione a [!DNL Azure Event Hubs].
* **[!UICONTROL Descrizione]**: fornire una descrizione della connessione.  Esempi: &quot;Clienti di livello Premium&quot;, &quot;Clienti interessati al kitesurfing&quot;.
* **[!UICONTROL eventHubName]**: fornisci un nome per il flusso nella destinazione [!DNL Azure Event Hubs].
* **[!UICONTROL Includi nomi segmento]**: attiva questa opzione se vuoi che l&#39;esportazione dei dati includa i nomi dei tipi di pubblico che stai esportando. Per un esempio di esportazione di dati con questa opzione selezionata, consulta la sezione [Dati esportati](#exported-data) più avanti.
* **[!UICONTROL Includi marche temporali segmento]**: attiva questa opzione se desideri che l&#39;esportazione dei dati includa la marca temporale UNIX di quando i tipi di pubblico sono stati creati e aggiornati, nonché la marca temporale UNIX di quando i tipi di pubblico sono stati mappati alla destinazione per l&#39;attivazione. Per un esempio di esportazione di dati con questa opzione selezionata, consulta la sezione [Dati esportati](#exported-data) più avanti.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* [La valutazione dei criteri di consenso](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) non è attualmente supportata nelle esportazioni nella destinazione degli hub eventi di Azure. [Ulteriori informazioni](/help/destinations/ui/activate-streaming-profile-destinations.md#consent-policy-evaluation).

Per istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione, consulta [Attiva dati pubblico nelle destinazioni di esportazione del profilo di streaming](../../ui/activate-streaming-profile-destinations.md).

## Comportamento di esportazione del profilo {#profile-export-behavior}

Experience Platform ottimizza il comportamento di esportazione del profilo nella destinazione [!DNL Azure Event Hubs] per esportare i dati nella destinazione solo quando si sono verificati aggiornamenti rilevanti a un profilo in seguito alla qualificazione del pubblico o ad altri eventi significativi. I profili vengono esportati nella destinazione nelle seguenti situazioni:

* L’aggiornamento del profilo è stato determinato da una modifica nell’appartenenza al pubblico per almeno uno dei tipi di pubblico mappati alla destinazione. Ad esempio, il profilo è idoneo per uno dei tipi di pubblico mappati sulla destinazione o è uscito da uno dei tipi di pubblico mappati sulla destinazione.
* L&#39;aggiornamento del profilo è stato determinato da una modifica nella [mappa identità](/help/xdm/field-groups/profile/identitymap.md). Ad esempio, a un profilo che si era già qualificato per uno dei tipi di pubblico mappati sulla destinazione è stata aggiunta una nuova identità nell’attributo identity map.
* L’aggiornamento del profilo è stato determinato da una modifica degli attributi per almeno uno degli attributi mappati alla destinazione. Ad esempio, uno degli attributi mappati sulla destinazione nel passaggio di mappatura viene aggiunto a un profilo.

In tutti i casi descritti sopra, solo i profili in cui si sono verificati aggiornamenti rilevanti vengono esportati nella destinazione. Ad esempio, se un pubblico mappato al flusso di destinazione ha un centinaio di membri e cinque nuovi profili sono idonei per il segmento, l’esportazione nella destinazione è incrementale e include solo i cinque nuovi profili.

Tieni presente che tutti gli attributi mappati vengono esportati per un profilo, indipendentemente da dove si trovano le modifiche. Quindi, nell’esempio precedente, tutti gli attributi mappati per questi cinque nuovi profili verranno esportati anche se gli attributi stessi non sono stati modificati.

### Che cosa determina un’esportazione di dati e cosa è incluso nell’esportazione {#what-determines-export-what-is-included}

Per quanto riguarda i dati esportati per un determinato profilo, è importante comprendere i due diversi concetti di *ciò che determina un&#39;esportazione di dati nella [!DNL Azure Event Hubs] destinazione* e *quali dati sono inclusi nell&#39;esportazione*.

| Cosa determina un’esportazione di destinazione | Cosa è incluso nell’esportazione di destinazione |
|---------|----------|
| <ul><li>Gli attributi e i tipi di pubblico mappati fungono da spunto per un’esportazione di destinazione. Ciò significa che se uno dei tipi di pubblico mappati cambia stato (da `null` a `realized` o da `realized` a `exiting`) o se uno qualsiasi degli attributi mappati viene aggiornato, viene avviata un&#39;esportazione di destinazione.</li><li>Poiché al momento non è possibile mappare le identità alle destinazioni [!DNL Azure Event Hubs], le modifiche in qualsiasi identità su un determinato profilo determinano anche le esportazioni di destinazione.</li><li>Per modifica di un attributo si intende qualsiasi aggiornamento dell&#39;attributo, indipendentemente dal fatto che si tratti o meno dello stesso valore. Ciò significa che una sovrascrittura su un attributo è considerata una modifica anche se il valore stesso non è cambiato.</li></ul> | <ul><li>L&#39;oggetto `segmentMembership` include il pubblico mappato nel flusso di dati di attivazione, per il quale lo stato del profilo è cambiato a seguito di un evento di qualificazione o uscita dal pubblico. Tieni presente che altri tipi di pubblico non mappati per i quali il profilo si è qualificato possono far parte dell&#39;esportazione di destinazione, se tali tipi di pubblico appartengono allo stesso [criterio di unione](/help/profile/merge-policies/overview.md) del pubblico mappato nel flusso di dati di attivazione. </li><li>Sono incluse anche tutte le identità nell&#39;oggetto `identityMap` (l&#39;Experience Platform attualmente non supporta il mapping delle identità nella destinazione [!DNL Azure Event Hubs]).</li><li>Nell’esportazione della destinazione sono inclusi solo gli attributi mappati.</li></ul> |

{style="table-layout:fixed"}

Consideriamo ad esempio questo flusso di dati su una destinazione [!DNL Azure Event Hubs] in cui tre tipi di pubblico sono selezionati nel flusso di dati e quattro attributi sono mappati alla destinazione.

![Flusso di dati di destinazione di Amazon Kinesis](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Un&#39;esportazione di profilo nella destinazione può essere determinata da un profilo idoneo o in uscita da uno dei *tre segmenti mappati*. Tuttavia, nell&#39;esportazione dei dati, nell&#39;oggetto `segmentMembership` (vedi la sezione [Dati esportati](#exported-data) di seguito), potrebbero essere visualizzati altri tipi di pubblico non mappati, se quel particolare profilo è un membro di essi e se questi condividono lo stesso criterio di unione del pubblico che ha attivato l&#39;esportazione. Se un profilo è idoneo per il pubblico **Cliente con auto DeLorean** ma è anche membro dei segmenti **Guardato &quot;Ritorno al futuro&quot;** film e **Fantascienza**, anche questi altri due tipi di pubblico saranno presenti nell&#39;oggetto `segmentMembership` dell&#39;esportazione dati, anche se non sono mappati nel flusso di dati, se condividono lo stesso criterio di unione con il segmento **Cliente con auto DeLorean**.

Dal punto di vista degli attributi di profilo, eventuali modifiche ai quattro attributi mappati in precedenza determineranno un’esportazione di destinazione e uno qualsiasi dei quattro attributi mappati presenti nel profilo sarà presente nell’esportazione di dati.

## Recupero dati storici {#historical-data-backfill}

Quando aggiungi un nuovo pubblico a una destinazione esistente o quando crei una nuova destinazione e mappi i tipi di pubblico a essa, Experience Platform esporta i dati storici di qualificazione del pubblico nella destinazione. I profili qualificati per il pubblico *prima* che il pubblico sia stato aggiunto alla destinazione vengono esportati nella destinazione entro circa un&#39;ora.

## Dati esportati {#exported-data}

I dati di [!DNL Experience Platform] esportati arrivano nella destinazione di [!DNL Azure Event Hubs] in formato JSON. Ad esempio, l’esportazione seguente contiene un profilo idoneo per un determinato segmento, è membro di altri due segmenti ed è uscito da un altro segmento. L’esportazione include anche l’attributo del profilo nome, cognome, data di nascita e indirizzo e-mail personale. Le identità per questo profilo sono ECID e e-mail.

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
         "status":"realized"
      },
      "947c1c46-008d-40b0-92ec-3af86eaf41c1":{
         "lastQualificationTime":"2021-08-25T23:37:33Z",
         "status":"realized"
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

Di seguito sono riportati ulteriori esempi di dati esportati, a seconda delle impostazioni dell&#39;interfaccia utente selezionate nel flusso di destinazione di connessione per le opzioni **[!UICONTROL Includi nomi segmento]** e **[!UICONTROL Includi marche temporali segmento]**:

+++ L&#39;esempio di esportazione dei dati seguente include i nomi del pubblico nella sezione `segmentMembership`

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "realized",
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

+++ L&#39;esempio di esportazione dei dati seguente include i timestamp del pubblico nella sezione `segmentMembership`

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "realized",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
          }
        }
      }
```

+++

## Limiti e criteri per nuovi tentativi {#limits-retry-policy}

Nel 95% del tempo, Experience Platform tenta di offrire una latenza di velocità effettiva inferiore a 10 minuti per i messaggi inviati correttamente con una frequenza inferiore a 10.000 richieste al secondo per ogni flusso di dati a una destinazione HTTP.

In caso di richieste non riuscite alla destinazione API HTTP, Experience Platform memorizza le richieste non riuscite e tenta di inviarle all’endpoint due volte.

>[!MORELIKETHIS]
>
>* [Connettiti ad Azure Event Hub e attiva i dati utilizzando l&#39;API del servizio Flusso](../../api/streaming-destinations.md)
>* [Destinazione AWS Kinesis](./amazon-kinesis.md)
>* [Tipi e categorie di destinazione](../../destination-types.md)
