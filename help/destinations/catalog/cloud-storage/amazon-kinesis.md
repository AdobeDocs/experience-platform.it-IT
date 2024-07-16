---
keywords: Amazon Kinesis;destinazione cinesi;kinesis
title: Connessione Amazon Kinesis
description: Crea una connessione in uscita in tempo reale allo storage Amazon Kinesis per inviare dati da Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: b40117ef-6ad0-48a9-bbcb-97c6f6d1dce3
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1984'
ht-degree: 5%

---

# Connessione [!DNL Amazon Kinesis]

## Panoramica {#overview}

>[!IMPORTANT]
>
> Questa destinazione è disponibile solo per [clienti Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/it/legal/product-descriptions/real-time-customer-data-platform.html).

Il servizio [!DNL Kinesis Data Streams] di [!DNL Amazon Web Services] consente di raccogliere ed elaborare flussi di dati di grandi dimensioni in tempo reale.

È possibile creare una connessione in uscita in tempo reale all&#39;archivio [!DNL Amazon Kinesis] per eseguire lo streaming dei dati da Adobe Experience Platform.

* Per ulteriori informazioni su [!DNL Amazon Kinesis], consulta la [documentazione di Amazon](https://docs.aws.amazon.com/streams/latest/dev/introduction.html).
* Per connettersi a [!DNL Amazon Kinesis] a livello di programmazione, vedere l&#39;esercitazione sull&#39;API delle [destinazioni di streaming](../../api/streaming-destinations.md).
* Per connettersi a [!DNL Amazon Kinesis] tramite l&#39;interfaccia utente di Platform, vedere le sezioni seguenti.

![Amazon Kinesis nell&#39;interfaccia utente](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)

## Casi d’uso {#use-cases}

Utilizzando destinazioni di streaming come [!DNL Amazon Kinesis], puoi inserire facilmente eventi di segmentazione di alto valore e attributi di profilo associati nei sistemi preferiti.

Ad esempio, un potenziale cliente ha scaricato un white paper che li qualifica come segmenti ad &quot;alta propensione alla conversione&quot;. Mappando il pubblico in cui rientra il potenziale cliente alla destinazione [!DNL Amazon Kinesis], riceverai questo evento in [!DNL Amazon Kinesis]. In questo caso, è possibile utilizzare un approccio fai-da-te e descrivere la logica di business oltre all&#39;evento, in base al principio che si potrebbe utilizzare al meglio con i sistemi IT aziendali.

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

Per soddisfare i requisiti di sicurezza e conformità dei clienti, Experience Platform inserire nell&#39;elenco Consentiti fornisce un elenco di IP statici che è possibile per la destinazione [!DNL Amazon Kinesis]. Per l&#39;elenco completo degli IP da elenco consentiti, consulta l&#39;[elenco Consentiti di indirizzo IP per le destinazioni di streaming](/help/destinations/catalog/streaming/ip-address-allow-list.md).

## Autorizzazioni [!DNL Amazon Kinesis] richieste {#required-kinesis-permission}

Per connettersi ed esportare correttamente i dati nei flussi [!DNL Amazon Kinesis], Experience Platform necessita delle autorizzazioni per le azioni seguenti:

* `kinesis:ListStreams`
* `kinesis:PutRecord`
* `kinesis:PutRecords`

Queste autorizzazioni sono organizzate tramite la console [!DNL Kinesis] e vengono verificate da Platform dopo che la destinazione Kinesis è stata configurata nell&#39;interfaccia utente di Platform.

Nell&#39;esempio seguente vengono visualizzati i diritti di accesso minimi necessari per esportare correttamente i dati in una destinazione [!DNL Kinesis].

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
| `kinesis:ListStreams` | Azione che elenca i flussi di dati di Amazon Kinesis. |
| `kinesis:PutRecord` | Azione che scrive un singolo record di dati in un flusso di dati Kinesis. |
| `kinesis:PutRecords` | Azione che scrive più record di dati in un flusso di dati Kinesis in una singola chiamata. |

{style="table-layout:auto"}

Per ulteriori informazioni sul controllo dell&#39;accesso per [!DNL Kinesis] flussi di dati, leggere il seguente [[!DNL Kinesis] documento](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Quando ti connetti a questa destinazione, devi fornire le seguenti informazioni:

### Informazioni di autenticazione {#authentication-information}

Immettere i campi seguenti e selezionare **[!UICONTROL Connetti alla destinazione]**:

![Immagine della schermata dell&#39;interfaccia utente che mostra i campi completati per i dettagli di autenticazione di Amazon Kinesis](../../assets/catalog/cloud-storage/amazon-kinesis/kinesis-authentication-fields.png)

* Chiave di accesso **[!DNL Amazon Web Services]e chiave segreta**: in [!DNL Amazon Web Services], genera una coppia `access key - secret access key` per concedere a Platform l&#39;accesso al tuo account [!DNL Amazon Kinesis]. Ulteriori informazioni sono disponibili nella [documentazione di Amazon Web Services](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL Area]**: indicare a quale area [!DNL Amazon Web Services] inviare i dati in streaming.

### Inserire i dettagli della destinazione {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_kinesis_includesegmentnames"
>title="Includi nomi dei segmenti"
>abstract="Attiva o disattiva questa opzione se desideri che l’esportazione dei dati includa i nomi dei tipi di pubblico che stai esportando. Consulta la documentazione per vedere un esempio di esportazione dei dati con questa opzione selezionata."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_kinesis_includesegmenttimestamps"
>title="Includi timestamp dei segmenti"
>abstract="Attiva o disattiva questa opzione se desideri che l’esportazione dei dati includa il timestamp UNIX al momento della creazione e dell’aggiornamento dei tipi di pubblico, nonché il timestamp UNIX al momento della mappatura dei tipi di pubblico sulla destinazione per l’attivazione. Consulta la documentazione per vedere un esempio di esportazione dei dati con questa opzione selezionata."

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

![Immagine della schermata dell&#39;interfaccia utente che mostra i campi completati per i dettagli della destinazione Amazon Kinesis](../../assets/catalog/cloud-storage/amazon-kinesis/kinesis-destination-details.png)

* **[!UICONTROL Nome]**: specifica un nome per la connessione a [!DNL Amazon Kinesis]
* **[!UICONTROL Descrizione]**: fornire una descrizione per la connessione a [!DNL Amazon Kinesis].
* **[!UICONTROL Flusso]**: fornisci il nome di un flusso di dati esistente nel tuo account [!DNL Amazon Kinesis]. Platform esporterà i dati in questo flusso.
* **[!UICONTROL Includi nomi segmento]**: attiva questa opzione se vuoi che l&#39;esportazione dei dati includa i nomi dei tipi di pubblico che stai esportando. Per un esempio di esportazione di dati con questa opzione selezionata, consulta la sezione [Dati esportati](#exported-data) più avanti.
* **[!UICONTROL Includi marche temporali segmento]**: attiva questa opzione se desideri che l&#39;esportazione dei dati includa la marca temporale UNIX di quando i tipi di pubblico sono stati creati e aggiornati, nonché la marca temporale UNIX di quando i tipi di pubblico sono stati mappati alla destinazione per l&#39;attivazione. Per un esempio di esportazione di dati con questa opzione selezionata, consulta la sezione [Dati esportati](#exported-data) più avanti.

<!--

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* [La valutazione dei criteri di consenso](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) non è attualmente supportata nelle esportazioni nella destinazione Amazon Kinesis. [Ulteriori informazioni](/help/destinations/ui/activate-streaming-profile-destinations.md#consent-policy-evaluation).

Per istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione, consulta [Attiva dati pubblico nelle destinazioni di esportazione del profilo di streaming](../../ui/activate-streaming-profile-destinations.md).

## Comportamento di esportazione del profilo {#profile-export-behavior}

Experience Platform ottimizza il comportamento di esportazione del profilo nella destinazione [!DNL Amazon Kinesis] per esportare i dati nella destinazione solo quando si sono verificati aggiornamenti rilevanti a un profilo in seguito alla qualificazione del pubblico o ad altri eventi significativi. I profili vengono esportati nella destinazione nelle seguenti situazioni:

* L’aggiornamento del profilo è stato determinato da una modifica nell’appartenenza al pubblico per almeno uno dei tipi di pubblico mappati alla destinazione. Ad esempio, il profilo è idoneo per uno dei tipi di pubblico mappati sulla destinazione o è uscito da uno dei tipi di pubblico mappati sulla destinazione.
* L&#39;aggiornamento del profilo è stato determinato da una modifica nella [mappa identità](/help/xdm/field-groups/profile/identitymap.md). Ad esempio, a un profilo che si era già qualificato per uno dei tipi di pubblico mappati sulla destinazione è stata aggiunta una nuova identità nell’attributo identity map.
* L’aggiornamento del profilo è stato determinato da una modifica degli attributi per almeno uno degli attributi mappati alla destinazione. Ad esempio, uno degli attributi mappati sulla destinazione nel passaggio di mappatura viene aggiunto a un profilo.

In tutti i casi descritti sopra, solo i profili in cui si sono verificati aggiornamenti rilevanti vengono esportati nella destinazione. Ad esempio, se un pubblico mappato al flusso di destinazione ha un centinaio di membri e cinque nuovi profili sono idonei per il segmento, l’esportazione nella destinazione è incrementale e include solo i cinque nuovi profili.

Tieni presente che tutti gli attributi mappati vengono esportati per un profilo, indipendentemente da dove si trovano le modifiche. Quindi, nell’esempio precedente, tutti gli attributi mappati per questi cinque nuovi profili verranno esportati anche se gli attributi stessi non sono stati modificati.

### Che cosa determina un’esportazione di dati e cosa è incluso nell’esportazione {#what-determines-export-what-is-included}

Per quanto riguarda i dati esportati per un determinato profilo, è importante comprendere i due diversi concetti di *ciò che determina un&#39;esportazione di dati nella [!DNL Amazon Kinesis] destinazione* e *quali dati sono inclusi nell&#39;esportazione*.

| Cosa determina un’esportazione di destinazione | Cosa è incluso nell’esportazione di destinazione |
|---------|----------|
| <ul><li>Gli attributi e i tipi di pubblico mappati fungono da spunto per un’esportazione di destinazione. Ciò significa che se uno dei tipi di pubblico mappati cambia stato (da `null` a `realized` o da `realized` a `exiting`) o se uno qualsiasi degli attributi mappati viene aggiornato, viene avviata un&#39;esportazione di destinazione.</li><li>Poiché al momento non è possibile mappare le identità alle destinazioni [!DNL Amazon Kinesis], le modifiche in qualsiasi identità su un determinato profilo determinano anche le esportazioni di destinazione.</li><li>Per modifica di un attributo si intende qualsiasi aggiornamento dell&#39;attributo, indipendentemente dal fatto che si tratti o meno dello stesso valore. Ciò significa che una sovrascrittura su un attributo è considerata una modifica anche se il valore stesso non è cambiato.</li></ul> | <ul><li>L&#39;oggetto `segmentMembership` include il pubblico mappato nel flusso di dati di attivazione, per il quale lo stato del profilo è cambiato a seguito di un evento di qualificazione o uscita dal pubblico. Tieni presente che altri tipi di pubblico non mappati per i quali il profilo si è qualificato possono far parte dell&#39;esportazione di destinazione, se tali tipi di pubblico appartengono allo stesso [criterio di unione](/help/profile/merge-policies/overview.md) del pubblico mappato nel flusso di dati di attivazione. </li><li>Sono incluse anche tutte le identità nell&#39;oggetto `identityMap` (l&#39;Experience Platform attualmente non supporta il mapping delle identità nella destinazione [!DNL Amazon Kinesis]).</li><li>Nell’esportazione della destinazione sono inclusi solo gli attributi mappati.</li></ul> |

{style="table-layout:fixed"}

Consideriamo ad esempio questo flusso di dati su una destinazione [!DNL Amazon Kinesis] in cui tre tipi di pubblico sono selezionati nel flusso di dati e quattro attributi sono mappati alla destinazione.

![Flusso di dati di destinazione di Amazon Kinesis](../../assets/catalog/http/profile-export-example-dataflow.png)

Un&#39;esportazione di profilo nella destinazione può essere determinata da un profilo idoneo o in uscita da uno dei *tre segmenti mappati*. Tuttavia, nell&#39;esportazione dei dati, nell&#39;oggetto `segmentMembership` (vedi la sezione [Dati esportati](#exported-data) di seguito), potrebbero essere visualizzati altri tipi di pubblico non mappati, se quel particolare profilo è un membro di essi e se questi condividono lo stesso criterio di unione del pubblico che ha attivato l&#39;esportazione. Se un profilo è idoneo per il pubblico **Cliente con auto DeLorean** ma è anche membro del pubblico **Guardato &quot;Ritorno al futuro&quot;** e **Fantascienza**, anche questi altri due tipi di pubblico saranno presenti nell&#39;oggetto `segmentMembership` dell&#39;esportazione dati, anche se non sono mappati nel flusso di dati, se condividono lo stesso criterio di unione con il segmento **Cliente con auto DeLorean**.

Dal punto di vista degli attributi di profilo, eventuali modifiche ai quattro attributi mappati in precedenza determineranno un’esportazione di destinazione e uno qualsiasi dei quattro attributi mappati presenti nel profilo sarà presente nell’esportazione di dati.

## Recupero dati storici {#historical-data-backfill}

Quando aggiungi un nuovo pubblico a una destinazione esistente o quando crei una nuova destinazione e mappi i tipi di pubblico a essa, Experience Platform esporta i dati storici di qualificazione del pubblico nella destinazione. I profili qualificati per il pubblico *prima* che il pubblico sia stato aggiunto alla destinazione vengono esportati nella destinazione entro circa un&#39;ora.

## Dati esportati {#exported-data}

I dati di [!DNL Experience Platform] esportati arrivano nella destinazione di [!DNL Amazon Kinesis] in formato JSON. Ad esempio, l’esportazione seguente contiene un profilo idoneo per un determinato segmento, è membro di altri due segmenti ed è uscito da un altro segmento. L’esportazione include anche l’attributo del profilo nome, cognome, data di nascita e indirizzo e-mail personale. Le identità per questo profilo sono ECID e e-mail.

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
>* [Connettiti ad Amazon Kinesis e attiva i dati utilizzando l&#39;API del servizio Flusso](../../api/streaming-destinations.md)
>* [Destinazione hub eventi Azure](./azure-event-hubs.md)
>* [Tipi e categorie di destinazione](../../destination-types.md)
