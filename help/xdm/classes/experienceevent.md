---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;identityMap;mappa identità;mappa identità;mappa identità;progettazione schema;mappa;mappare;modellazione eventi;modellazione eventi;best practice;eventi;eventi;
solution: Experience Platform
title: Classe XDM ExperienceEvent
description: Scopri la classe XDM ExperienceEvent e le best practice per la modellazione dei dati degli eventi.
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '2672'
ht-degree: 0%

---

# [!DNL XDM ExperienceEvent] classe

[!DNL XDM ExperienceEvent] è una classe XDM (Experience Data Model) standard. Utilizzare questa classe per creare uno snapshot con marca temporale del sistema quando si verifica un evento specifico o viene raggiunto un determinato set di condizioni.

Un evento esperienza è una registrazione fattuale di ciò che si è verificato, incluso il momento e l’identità dell’individuo coinvolto. Gli eventi possono essere espliciti (azioni umane direttamente osservabili) o impliciti (generati senza un&#39;azione umana diretta) e sono registrati senza aggregazione o interpretazione. Per ulteriori informazioni di alto livello sull&#39;utilizzo di questa classe nell&#39;ecosistema Platform, fare riferimento alla [panoramica XDM](../home.md#data-behaviors).

La classe [!DNL XDM ExperienceEvent] fornisce a uno schema diversi campi correlati a serie temporali. Due di questi campi (`_id` e `timestamp`) sono **obbligatori** per tutti gli schemi basati su questa classe, mentre gli altri sono facoltativi. I valori di alcuni campi vengono compilati automaticamente al momento dell’acquisizione dei dati.

![Struttura di XDM ExperienceEvent visualizzata nell&#39;interfaccia utente di Platform.](../images/classes/experienceevent/structure.png)

| Proprietà | Descrizione |
| --- | --- |
| `_id`<br>**(Obbligatorio)** | Il campo Classe evento esperienza `_id` identifica in modo univoco i singoli eventi acquisiti in Adobe Experience Platform. Questo campo viene utilizzato per tenere traccia dell’univocità di un singolo evento, evitare la duplicazione di dati e cercare tale evento nei servizi a valle.<br><br>Se vengono rilevati eventi duplicati, le applicazioni e i servizi Platform potrebbero gestire la duplicazione in modo diverso. Ad esempio, gli eventi duplicati nel servizio Profilo vengono eliminati se l&#39;evento con lo stesso `_id` esiste già nell&#39;archivio Profili.<br><br>In alcuni casi, `_id` può essere un [Identificatore univoco universale (UUID)](https://datatracker.ietf.org/doc/html/rfc4122) o [Identificatore univoco globale (GUID)](https://learn.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>Se si esegue il flusso di dati da una connessione di origine o si acquisiscono dati direttamente da un file Parquet, è necessario generare questo valore concatenando una determinata combinazione di campi che rendono l&#39;evento univoco. Esempi di eventi che possono essere concatenati includono ID primario, marca temporale, tipo di evento e così via. Il valore concatenato deve essere una stringa formattata `uri-reference`, il che significa che è necessario rimuovere i due punti. Successivamente, il valore concatenato deve essere sottoposto a hashing utilizzando SHA-256 o un altro algoritmo a tua scelta.<br><br>È importante distinguere che **questo campo non rappresenta un&#39;identità correlata a una singola persona**, ma il record dei dati stessi. I dati di identità relativi a una persona devono essere relegati a [campi di identità](../schema/composition.md#identity) forniti da gruppi di campi compatibili. |
| `eventMergeId` | Se si utilizza [Adobe Experience Platform Web SDK](/help/web-sdk/home.md) per acquisire i dati, questo rappresenta l&#39;ID del batch acquisito che ha causato la creazione del record. Questo campo viene compilato automaticamente dal sistema al momento dell’inserimento dei dati. L’utilizzo di questo campo al di fuori del contesto di un’implementazione Web SDK non è supportato. |
| `eventType` | Stringa che indica il tipo o la categoria dell&#39;evento. Questo campo può essere utilizzato se desideri distinguere diversi tipi di evento all’interno dello stesso schema e set di dati, ad esempio per distinguere un evento di visualizzazione prodotto da un evento add-to-shopping-cart per una società di vendita al dettaglio.<br><br>I valori standard per questa proprietà sono forniti nella [sezione dell&#39;appendice](#eventType), incluse le descrizioni del caso d&#39;uso previsto. Questo campo è un enum estensibile, il che significa che puoi utilizzare anche stringhe di tipo evento personalizzate per categorizzare gli eventi che stai tracciando.<br><br>`eventType` ti limita a utilizzare un solo evento per hit nell&#39;applicazione, pertanto devi utilizzare i campi calcolati per comunicare al sistema quale evento è più importante. Per ulteriori informazioni, consulta la sezione sulle [best practice per i campi calcolati](#calculated). |
| `producedBy` | Valore stringa che descrive il produttore o l’origine dell’evento. Questo campo può essere utilizzato per filtrare alcuni produttori di eventi, se necessario a scopo di segmentazione.<br><br>Alcuni valori suggeriti per questa proprietà sono forniti nella [sezione dell&#39;appendice](#producedBy). Questo campo è un enum estensibile, il che significa che puoi utilizzare anche stringhe personalizzate per rappresentare diversi produttori di eventi. |
| `identityMap` | Campo mappa che contiene un set di identità con spazio dei nomi per l’individuo a cui si applica l’evento. Questo campo viene aggiornato automaticamente dal sistema durante l’acquisizione dei dati di identità. Per utilizzare correttamente questo campo per [Real-Time Customer Profile](../../profile/home.md), non tentare di aggiornare manualmente il contenuto del campo nelle operazioni sui dati.<br /><br />Per ulteriori informazioni sul caso d&#39;uso, consulta la sezione sulle mappe di identità nelle [nozioni di base sulla composizione dello schema](../schema/composition.md#identityMap). |
| `timestamp`<br>**(Obbligatorio)** | Timestamp ISO 8601 del momento in cui si è verificato l&#39;evento, formattato come [RFC 3339 Sezione 5.6](https://datatracker.ietf.org/doc/html/rfc3339). Questo timestamp **deve** verificarsi in passato, ma **deve** avvenire dal 1970 in poi. Consulta la sezione seguente su [timestamp](#timestamps) per le best practice sull&#39;utilizzo di questo campo. |

{style="table-layout:auto"}

## Best practice per la modellazione degli eventi

Le sezioni seguenti descrivono le best practice per la progettazione di schemi Experience Data Model (XDM) basati su eventi in Adobe Experience Platform.

### Marca temporale {#timestamps}

Il campo `timestamp` radice di uno schema evento può **only** rappresentare l&#39;osservazione dell&#39;evento stesso e deve verificarsi nel passato. Tuttavia, l&#39;evento **must** si svolge dal 1970 in poi. Se i casi di utilizzo della segmentazione richiedono l’uso di marche temporali che possono verificarsi in futuro, questi valori devono essere vincolati altrove nello schema Evento esperienza.

Ad esempio, se un&#39;azienda del settore viaggi e ospitalità sta modellando un evento di prenotazione di un volo, il campo `timestamp` a livello di classe rappresenta il momento in cui è stato osservato l&#39;evento di prenotazione. Altre marche temporali correlate all’evento, come la data di inizio della prenotazione del viaggio, devono essere acquisite in campi separati forniti da gruppi di campi standard o personalizzati.

![Schema evento esperienza di esempio con prenotazione del volo e data di inizio evidenziate.](../images/classes/experienceevent/timestamps.png)

Mantenendo la marca temporale a livello di classe separata da altri valori di data e ora correlati negli schemi evento, puoi implementare casi di utilizzo di segmentazione flessibili, mantenendo al contempo un account con marca temporale dei percorsi di clienti nell’applicazione Experience.

### Utilizzo dei campi calcolati {#calculated}

Alcune interazioni nelle applicazioni di esperienza possono causare più eventi correlati che tecnicamente condividono la stessa marca temporale dell’evento e possono quindi essere rappresentati come un singolo record di evento. Ad esempio, se un cliente visualizza un prodotto sul sito Web, può verificarsi un record evento con due potenziali valori `eventType`: un evento &quot;visualizzazione prodotto&quot; (`commerce.productViews`) o un evento &quot;visualizzazione pagina&quot; generico (`web.webpagedetails.pageViews`). In questi casi, puoi utilizzare i campi calcolati per acquisire gli attributi più importanti quando più eventi vengono acquisiti in un singolo hit.

Utilizza [Preparazione dati di Adobe Experience Platform](../../data-prep/home.md) per mappare, trasformare e convalidare i dati da e verso XDM. Utilizzando le [funzioni di mappatura](../../data-prep/functions.md) disponibili fornite dal servizio, è possibile richiamare operatori logici per assegnare priorità, trasformare e/o consolidare dati da record con più eventi al momento dell&#39;acquisizione in Experience Platform. Nell&#39;esempio precedente, è possibile designare `eventType` come campo calcolato che assegnerebbe la priorità a una &quot;visualizzazione prodotto&quot; rispetto a una &quot;visualizzazione pagina&quot; ogni volta che si verificano entrambe.

Se acquisisci manualmente i dati in Platform tramite l’interfaccia utente, consulta la guida sui [campi calcolati](../../data-prep/ui/mapping.md#calculated-fields) per i passaggi specifici sulla creazione dei campi calcolati.

Se trasferisci dati a Platform utilizzando una connessione di origine, puoi configurare l’origine per utilizzare i campi calcolati. Per istruzioni su come implementare i campi calcolati durante la configurazione della connessione, consulta la [documentazione per l&#39;origine specifica](../../sources/home.md).

## Gruppi di campi di schema compatibili {#field-groups}

>[!NOTE]
>
>I nomi di diversi gruppi di campi sono stati modificati. Per ulteriori informazioni, consulta il documento sugli aggiornamenti del nome del gruppo di campi [](../field-groups/name-updates.md).

L&#39;Adobe fornisce diversi gruppi di campi standard da utilizzare con la classe [!DNL XDM ExperienceEvent]. Di seguito è riportato un elenco di alcuni gruppi di campi comunemente utilizzati per la classe:

* [[!UICONTROL Estensione completa Adobe Analytics ExperienceEvent]](../field-groups/event/analytics-full-extension.md)
* [[!UICONTROL Trasferimenti saldo]](../field-groups/event/balance-transfers.md)
* [[!UICONTROL Dettagli marketing campagna]](../field-groups/event/campaign-marketing-details.md)
* [[!UICONTROL Azioni scheda]](../field-groups/event/card-actions.md)
* [[!UICONTROL Dettagli canale]](../field-groups/event/channel-details.md)
* [[!UICONTROL Dettagli Commerce]](../field-groups/event/commerce-details.md)
* [[!UICONTROL Dettagli versamento]](../field-groups/event/deposit-details.md)
* [[!UICONTROL Dettagli permuta dispositivo]](../field-groups/event/device-trade-in-details.md)
* [[!UICONTROL Prenotazione ristorante]](../field-groups/event/dining-reservation.md)
* [[!UICONTROL Dettagli ID utente finale]](../field-groups/event/enduserids.md)
* [[!UICONTROL Dettagli ambiente]](../field-groups/event/environment-details.md)
* [[!UICONTROL Prenotazione del volo]](../field-groups/event/flight-reservation.md)
* [[!UICONTROL Consenso IAB TCF 2.0]](../field-groups/event/iab.md)
* [[!UICONTROL Prenotazione alloggio]](../field-groups/event/lodging-reservation.md)
* [[!UICONTROL Dettagli interazione MediaAnalytics]](../field-groups/event/mediaanalytics-interaction.md)
* [[!UICONTROL Dettagli richiesta preventivo]](../field-groups/event/quote-request-details.md)
* [[!UICONTROL Dettagli prenotazione]](../field-groups/event/reservation-details.md)
* [[!UICONTROL Dettagli Web]](../field-groups/event/web-details.md)

## Appendice

La sezione seguente contiene informazioni aggiuntive sulla classe [!UICONTROL XDM ExperienceEvent].

### Valori accettati per `eventType` {#eventType}

La tabella seguente illustra i valori accettati per `eventType` e le relative definizioni:

| Valore | Definizione |
| --- | --- |
| `advertising.clicks` | Questo evento tiene traccia di quando si verifica un&#39;azione per selezionare un annuncio pubblicitario. |
| `advertising.completes` | Questo evento tiene traccia di quando una risorsa multimediale a tempo è stata guardata fino al completamento. Questo non significa necessariamente che lo spettatore abbia guardato l&#39;intero video, poiché potrebbe aver saltato delle parti per andare avanti. |
| `advertising.conversions` | Questo evento tiene traccia di un’azione predefinita eseguita da un cliente che attiva un evento per la valutazione delle prestazioni. |
| `advertising.federated` | Questo evento tiene traccia di se un evento esperienza è stato creato tramite la federazione di dati (condivisione di dati tra clienti). |
| `advertising.firstQuartiles` | Questo evento tiene traccia di quando un annuncio video digitale è stato riprodotto a velocità normale per il 25% della sua durata. |
| `advertising.impressions` | Questo evento tiene traccia delle impression di un annuncio pubblicitario rivolto a un cliente potenzialmente visualizzato. |
| `advertising.midpoints` | Questo evento tiene traccia di quando un annuncio video digitale è stato riprodotto a velocità normale per il 50% della sua durata. |
| `advertising.starts` | Questo evento tiene traccia di quando un annuncio video digitale ha iniziato la riproduzione. |
| `advertising.thirdQuartiles` | Questo evento tiene traccia di quando un annuncio video digitale è stato riprodotto a velocità normale per il 75% della sua durata. |
| `advertising.timePlayed` | Questo evento tiene traccia della quantità di tempo trascorso da un utente su una specifica risorsa multimediale a tempo. |
| `application.close` | Questo evento tiene traccia di quando un’applicazione è stata chiusa o inviata in background. |
| `application.launch` | Questo evento tiene traccia di quando un’applicazione è stata avviata o portata in primo piano. |
| `commerce.backofficeCreditMemoIssued` | Questo evento tiene traccia di quando un avviso di credito è stato emesso a un cliente. |
| `commerce.backofficeOrderCancelled` | Questo evento tiene traccia di quando un processo di acquisto avviato in precedenza è stato terminato prima del completamento. |
| `commerce.backofficeOrderItemsShipped` | Questo evento tiene traccia di quando gli articoli acquistati sono stati fisicamente spediti al cliente. |
| `commerce.backofficeOrderPlaced` | Questo evento tiene traccia del posizionamento di un ordine. |
| `commerce.backofficeShipmentCompleted` | Questo evento tiene traccia del completamento dell&#39;intero processo di spedizione. |
| `commerce.checkouts` | Questo evento tiene traccia di quando si è verificato un evento di pagamento per un elenco di prodotti. Ci può essere più di un evento di pagamento se ci sono più passaggi in un processo di pagamento. Se sono presenti più passaggi, la marca temporale e la pagina/esperienza di riferimento per ciascun evento vengono utilizzate per identificare ogni singolo evento (passaggio), rappresentato in ordine. |
| `commerce.productListAdds` | Questo evento tiene traccia di quando un prodotto è stato aggiunto all’elenco dei prodotti o al carrello. |
| `commerce.productListOpens` | Questo evento tiene traccia di quando un nuovo elenco di prodotti (carrello) è stato inizializzato o creato. |
| `commerce.productListRemovals` | Questo evento tiene traccia di quando una voce di prodotto è stata rimossa da un elenco di prodotti o da un carrello. |
| `commerce.productListReopens` | Questo evento tiene traccia di quando un elenco di prodotti (carrello) non più accessibile (abbandonato) è stato riattivato da un cliente, ad esempio tramite un’attività di remarketing. |
| `commerce.productListViews` | Questo evento tiene traccia di quando un elenco di prodotti o un carrello ha ricevuto una visualizzazione. |
| `commerce.productViews` | Questo evento tiene traccia di quando un prodotto ha ricevuto una o più visualizzazioni. |
| `commerce.purchases` | Questo evento tiene traccia di quando un ordine è stato accettato. Questa è l’unica azione richiesta in una conversione commerce. Un evento di acquisto deve fare riferimento a un elenco di prodotti. |
| `commerce.saveForLaters` | Questo evento tiene traccia di quando un elenco di prodotti è stato salvato per un utilizzo futuro, ad esempio una lista di desideri di prodotto. |
| `decisioning.propositionDisplay` | Questo evento tiene traccia di quando una proposta decisionale è stata visualizzata a una persona. |
| `decisioning.propositionDismiss` | Questo evento tiene traccia di quando è stata presa la decisione di non partecipare all’offerta presentata. |
| `decisioning.propositionInteract` | Questo evento tiene traccia di quando una persona ha interagito con una proposta decisionale. |
| `decisioning.propositionSend` | Questo evento tiene traccia di quando è stato deciso di inviare a un potenziale cliente un consiglio o un&#39;offerta da prendere in considerazione. |
| `decisioning.propositionTrigger` | Questo evento tiene traccia dell’attivazione di un processo di proposta. Si è verificata una determinata condizione o azione per richiedere la presentazione di un’offerta. |
| `delivery.feedback` | Questo evento tiene traccia degli eventi di feedback per una consegna, ad esempio una consegna e-mail. |
| `directMarketing.emailBounced` | Questo evento tiene traccia di quando un’e-mail inviata a una persona non viene recapitata. |
| `directMarketing.emailBouncedSoft` | Questo evento tiene traccia dei mancati recapiti non permanenti di un’e-mail a una persona. |
| `directMarketing.emailClicked` | Questo evento tiene traccia di quando una persona ha fatto clic su un collegamento in un’e-mail di marketing. |
| `directMarketing.emailDelivered` | Questo evento tiene traccia di quando un’e-mail è stata consegnata correttamente al servizio e-mail di un utente. |
| `directMarketing.emailOpened` | Questo evento tiene traccia di quando una persona ha aperto un’e-mail di marketing. |
| `directMarketing.emailSent` | Questo evento tiene traccia di quando un’e-mail di marketing è stata inviata a una persona. |
| `directMarketing.emailUnsubscribed` | Questo evento tiene traccia di quando una persona ha annullato l’abbonamento a un’e-mail di marketing. |
| `inappmessageTracking.dismiss` | Questo evento tiene traccia di quando un messaggio in-app è stato chiuso. |
| `inappmessageTracking.display` | Questo evento traccia la visualizzazione di un messaggio in-app. |
| `inappmessageTracking.interact` | Questo evento tiene traccia di quando è stato interagito un messaggio in-app con. |
| `leadOperation.callWebhook` | Questo evento tiene traccia di quando un webhook è stato chiamato in risposta a un lead. |
| `leadOperation.changeCampaignStream` | Questo evento indica un cambiamento nella strategia di marketing o di coinvolgimento per un determinato lead di business. |
| `leadOperation.changeEngagementCampaignCadence` | Questo evento tiene traccia di quando si è verificato un cambiamento nella frequenza con cui un lead viene coinvolto in una campagna. |
| `leadOperation.convertLead` | Questo evento tiene traccia della conversione di un lead. |
| `leadOperation.interestingMoment` | Questo evento tiene traccia di quando è stato registrato un momento interessante per una persona. |
| `leadOperation.mergeLeads` | Questo evento tiene traccia di quando sono state consolidate informazioni provenienti da più lead che fanno riferimento alla stessa entità. |
| `leadOperation.newLead` | Questo evento tiene traccia di quando è stato creato un lead. |
| `leadOperation.scoreChanged` | Questo evento tiene traccia di quando il valore dell’attributo di punteggio del lead è stato modificato. |
| `leadOperation.statusInCampaignProgressionChanged` | Questo evento tiene traccia di quando lo stato di un lead in una campagna è cambiato. |
| `listOperation.addToList` | Questo evento tiene traccia di quando una persona è stata aggiunta a un elenco di marketing. |
| `listOperation.removeFromList` | Questo evento tiene traccia di quando una persona è stata rimossa da un elenco di marketing. |
| `media.adBreakComplete` | Questo evento traccia quando si è verificato un evento `adBreakComplete`. Questo evento viene attivato all’inizio di un’interruzione pubblicitaria. |
| `media.adBreakStart` | Questo evento traccia quando si è verificato un evento `adBreakStart`. Questo evento viene attivato al termine di un’interruzione pubblicitaria. |
| `media.adComplete` | Questo evento traccia quando si è verificato un evento `adComplete`. Questo evento viene attivato quando un annuncio è stato completato. |
| `media.adSkip` | Questo evento traccia quando si è verificato un evento `adSkip`. Questo evento viene attivato quando un annuncio viene saltato. |
| `media.adStart` | Questo evento traccia quando si è verificato un evento `adStart`. Questo evento viene attivato all&#39;avvio di un annuncio. |
| `media.bitrateChange` | Questo evento tiene traccia di quando si è verificato un evento `bitrateChange`. Questo evento viene attivato quando si verifica una modifica nella velocità bit. |
| `media.bufferStart` | Questo evento tiene traccia di quando si è verificato un evento `bufferStart`. Questo evento viene attivato quando il contenuto multimediale inizia a memorizzare in un buffer. |
| `media.chapterComplete` | Questo evento tiene traccia di quando si è verificato un evento `chapterComplete`. Questo evento viene attivato al completamento di un capitolo nel file multimediale. |
| `media.chapterSkip` | Questo evento tiene traccia di quando si è verificato un evento `chapterSkip`. Questo evento viene attivato quando un utente passa avanti o indietro a un’altra sezione o capitolo all’interno del contenuto multimediale. |
| `media.chapterStart` | Questo evento tiene traccia di quando si è verificato un evento `chapterStart`. Questo evento viene attivato all’inizio di una sezione o di un capitolo specifico all’interno del contenuto multimediale. |
| `media.downloaded` | Questo evento tiene traccia di quando si sono verificati contenuti multimediali scaricati. |
| `media.error` | Questo evento traccia quando si è verificato un evento `error`. Questo evento viene attivato quando si verifica un errore o un problema durante la riproduzione di contenuti multimediali. |
| `media.pauseStart` | Questo evento tiene traccia di quando si è verificato un evento `pauseStart`. Questo evento viene attivato quando un utente avvia una pausa nella riproduzione di contenuti multimediali. |
| `media.ping` | Questo evento traccia quando si è verificato un evento `ping`. In questo modo viene verificata la disponibilità di una risorsa multimediale. |
| `media.play` | Questo evento tiene traccia di quando si è verificato un evento `play`. Questo evento viene attivato durante la riproduzione del contenuto multimediale, indicando il consumo attivo da parte dell’utente. |
| `media.sessionComplete` | Questo evento tiene traccia di quando si è verificato un evento `sessionComplete`. Questo evento segna la fine di una sessione di riproduzione multimediale. |
| `media.sessionEnd` | Questo evento tiene traccia di quando si è verificato un evento `sessionEnd`. Questo evento indica la conclusione di una sessione multimediale. Questa conclusione può comportare la chiusura del lettore multimediale o l’interruzione della riproduzione. |
| `media.sessionStart` | Questo evento tiene traccia di quando si è verificato un evento `sessionStart`. Questo evento segna l’inizio di una sessione di riproduzione multimediale. Viene attivato quando un utente avvia la riproduzione di un file multimediale. |
| `media.statesUpdate` | Questo evento tiene traccia di quando si è verificato un evento `statesUpdate`. Le funzionalità di tracciamento dello stato del lettore possono essere collegate a un flusso audio o video. Gli stati standard sono: fullscreen, mute, closedCaptioning, pictureInPicture e inFocus. |
| `opportunityEvent.addToOpportunity` | Questo evento tiene traccia di quando una persona è stata aggiunta a un’opportunità. |
| `opportunityEvent.opportunityUpdated` | Questo evento tiene traccia di quando un’opportunità è stata aggiornata. |
| `opportunityEvent.removeFromOpportunity` | Questo evento tiene traccia di quando una persona è stata rimossa da un’opportunità. |
| `pushTracking.applicationOpened` | Questo evento tiene traccia di quando una persona ha aperto un’applicazione da una notifica push. |
| `pushTracking.customAction` | Questo evento tiene traccia di quando una persona ha selezionato un’azione personalizzata in una notifica push. |
| `web.formFilledOut` | Questo evento tiene traccia di quando una persona ha compilato un modulo su una pagina web. |
| `web.webinteraction.linkClicks` | Questo evento tiene traccia di quando un collegamento è stato selezionato una o più volte. |
| `web.webpagedetails.pageViews` | Questo evento tiene traccia di quando una pagina Web ha ricevuto una o più visualizzazioni. |
| `location.entry` | Questo evento tiene traccia dell’ingresso di una persona o di un dispositivo in una posizione specifica. |
| `location.exit` | Questo evento tiene traccia dell’uscita di una persona o di un dispositivo da una posizione specifica. |

{style="table-layout:auto"}

### Valori consigliati per `producedBy` {#producedBy}

Nella tabella seguente sono illustrati alcuni valori accettati per `producedBy`:

| Valore | Definizione |
| --- | --- |
| `self` | Autonomo |
| `system` | Sistema |
| `salesRef` | Rappresentante commerciale |
| `customerRep` | Rappresentante del cliente |
