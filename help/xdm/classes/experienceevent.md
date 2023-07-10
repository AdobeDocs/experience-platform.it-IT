---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;identityMap;mappa identità;mappa identità;mappa identità;progettazione schema;mappa;mappare;modellazione eventi;modellazione eventi;best practice;eventi;eventi;
solution: Experience Platform
title: Classe XDM ExperienceEvent
description: Questo documento fornisce una panoramica della classe XDM ExperienceEvent e delle best practice per la modellazione dei dati degli eventi.
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: d648a2151060d1013a6bce7a8180378400337829
workflow-type: tm+mt
source-wordcount: '1880'
ht-degree: 1%

---

# [!DNL XDM ExperienceEvent] classe

[!DNL XDM ExperienceEvent] è una classe XDM (Experience Data Model) standard che consente di creare un’istantanea con marca temporale del sistema quando si verifica un evento specifico o viene raggiunto un determinato set di condizioni.

Un evento esperienza è una registrazione fattuale di ciò che si è verificato, incluso il momento e l’identità dell’individuo coinvolto. Gli eventi possono essere espliciti (azioni umane direttamente osservabili) o impliciti (generati senza un&#39;azione umana diretta) e sono registrati senza aggregazione o interpretazione. Per ulteriori informazioni di alto livello sull’utilizzo di questa classe nell’ecosistema Platform, consulta [Panoramica di XDM](../home.md#data-behaviors).

Il [!DNL XDM ExperienceEvent] La classe stessa fornisce a uno schema diversi campi relativi a serie temporali. Due campi (`_id` e `timestamp`) sono **obbligatorio** per tutti gli schemi basati sulla classe, mentre gli altri sono facoltativi. I valori di alcuni campi vengono compilati automaticamente al momento dell’acquisizione dei dati.

![Struttura di XDM ExperienceEvent visualizzata nell’interfaccia utente di Platform](../images/classes/experienceevent/structure.png)

| Proprietà | Descrizione |
| --- | --- |
| `_id`<br>**(Obbligatorio)** | La classe dell’evento esperienza `_id` questo campo identifica in modo univoco i singoli eventi acquisiti in Adobe Experience Platform. Questo campo viene utilizzato per tenere traccia dell’univocità di un singolo evento, evitare la duplicazione di dati e cercare tale evento nei servizi a valle.<br><br>Se vengono rilevati eventi duplicati, le applicazioni e i servizi Platform possono gestire la duplicazione in modo diverso.  Ad esempio, gli eventi duplicati nel servizio Profilo vengono eliminati se l’evento con lo stesso `_id` esiste già nell’archivio profili.<br><br>In alcuni casi, `_id` può essere un [Identificatore univoco universale (UUID)](https://tools.ietf.org/html/rfc4122) o [Identificatore univoco globale (GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>Se esegui lo streaming dei dati da una connessione di origine o l’acquisizione diretta da un file Parquet, è necessario generare questo valore concatenando una determinata combinazione di campi che rendono univoco l’evento, ad esempio un ID primario, una marca temporale, un tipo di evento e così via. Il valore concatenato deve essere un `uri-reference` stringa formattata, ovvero è necessario rimuovere i due punti. Successivamente, il valore concatenato deve essere sottoposto a hashing utilizzando SHA-256 o un altro algoritmo a tua scelta.<br><br>È importante distinguere questo **questo campo non rappresenta un’identità correlata a una singola persona**, ma piuttosto la registrazione dei dati stessi. I dati di identità relativi a una persona dovrebbero essere relegati a [campi di identità](../schema/composition.md#identity) fornite da gruppi di campi compatibili. |
| `eventMergeId` | Se utilizzi il [Adobe Experience Platform Web SDK](../../edge/home.md) per acquisire i dati, rappresenta l’ID del batch acquisito che ha causato la creazione del record. Questo campo viene compilato automaticamente dal sistema al momento dell’inserimento dei dati. L’utilizzo di questo campo al di fuori del contesto di un’implementazione Web SDK non è supportato. |
| `eventType` | Stringa che indica il tipo o la categoria dell&#39;evento. Questo campo può essere utilizzato se desideri distinguere diversi tipi di evento all’interno dello stesso schema e set di dati, ad esempio per distinguere un evento di visualizzazione prodotto da un evento add-to-shopping-cart per una società di vendita al dettaglio.<br><br>I valori standard per questa proprietà sono forniti nel [sezione dell&#39;appendice](#eventType), incluse le descrizioni del caso d’uso previsto. Questo campo è un enum estensibile, il che significa che puoi utilizzare anche stringhe di tipo evento personalizzate per categorizzare gli eventi che stai tracciando.<br><br>`eventType` limita l’utilizzo di un solo evento per hit nell’applicazione; pertanto, è necessario utilizzare campi calcolati per comunicare al sistema quale evento è più importante. Per ulteriori informazioni, consulta la sezione su [best practice per i campi calcolati](#calculated). |
| `producedBy` | Valore stringa che descrive il produttore o l’origine dell’evento. Questo campo può essere utilizzato per filtrare alcuni produttori di eventi, se necessario a scopo di segmentazione.<br><br>Alcuni valori suggeriti per questa proprietà sono forniti nel [sezione dell&#39;appendice](#producedBy). Questo campo è un enum estensibile, il che significa che puoi utilizzare anche stringhe personalizzate per rappresentare diversi produttori di eventi. |
| `identityMap` | Campo mappa che contiene un set di identità con spazio dei nomi per l’individuo a cui si applica l’evento. Questo campo viene aggiornato automaticamente dal sistema durante l’acquisizione dei dati di identità. Per utilizzare correttamente questo campo per [Profilo cliente in tempo reale](../../profile/home.md), non tentare di aggiornare manualmente il contenuto del campo nelle operazioni sui dati.<br /><br />Consulta la sezione sulle mappe di identità in [nozioni di base sulla composizione dello schema](../schema/composition.md#identityMap) per ulteriori informazioni sul caso d’uso. |
| `timestamp`<br>**(Obbligatorio)** | Una marca temporale ISO 8601 del momento in cui si è verificato l’evento, formattata come da [RFC 3339 Sezione 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). Questa marca temporale deve essere nel passato. Vedi la sezione seguente su [marche temporali](#timestamps) per le best practice sull’utilizzo di questo campo. |

{style="table-layout:auto"}

## Best practice per la modellazione degli eventi

Le sezioni seguenti descrivono le best practice per la progettazione di schemi Experience Data Model (XDM) basati su eventi in Adobe Experience Platform.

### Marca temporale {#timestamps}

La radice `timestamp` campo di uno schema evento può **solo** rappresenta l’osservazione dell’evento stesso e deve verificarsi nel passato. Se i casi di utilizzo della segmentazione richiedono l’uso di marche temporali che possono verificarsi in futuro, questi valori devono essere vincolati altrove nello schema Evento esperienza.

Ad esempio, se un’azienda nel settore dei viaggi e dell’ospitalità sta modellando un evento di prenotazione di un volo, il `timestamp` rappresenta il momento in cui è stato osservato l’evento di prenotazione. Altre marche temporali correlate all’evento, come la data di inizio della prenotazione del viaggio, devono essere acquisite in campi separati forniti da gruppi di campi standard o personalizzati.

![Un esempio di schema di evento esperienza con prenotazione del volo e data di inizio evidenziati.](../images/classes/experienceevent/timestamps.png)

Mantenendo la marca temporale a livello di classe separata da altri valori di data e ora correlati negli schemi evento, puoi implementare casi di utilizzo di segmentazione flessibili, mantenendo al contempo un account con marca temporale dei percorsi di clienti nell’applicazione Experience.

### Utilizzo dei campi calcolati {#calculated}

Alcune interazioni nelle applicazioni di esperienza possono causare più eventi correlati che tecnicamente condividono la stessa marca temporale dell’evento e possono quindi essere rappresentati come un singolo record di evento. Ad esempio, se un cliente visualizza un prodotto sul sito web, questo può causare un record di evento con due potenziali `eventType` valori: un evento &quot;product view&quot; (`commerce.productViews`) o un evento generico di &quot;visualizzazione pagina&quot; (`web.webpagedetails.pageViews`). In questi casi, puoi utilizzare i campi calcolati per acquisire gli attributi più importanti quando più eventi vengono acquisiti in un singolo hit.

[Preparazione dati di Adobe Experience Platform](../../data-prep/home.md) consente di mappare, trasformare e convalidare i dati da e verso XDM. Utilizzo del [funzioni di mappatura](../../data-prep/functions.md) fornito dal servizio, è possibile richiamare operatori logici per assegnare priorità, trasformare e/o consolidare dati da record con più eventi al momento dell’acquisizione in Experience Platform. Nell’esempio precedente, puoi designare `eventType` come campo calcolato che dà priorità a una &quot;visualizzazione prodotto&quot; rispetto a una &quot;visualizzazione pagina&quot; ogni volta che si verificano entrambe.

Se acquisisci manualmente i dati in Platform tramite l’interfaccia utente, consulta la guida su [campi calcolati](../../data-prep/ui/mapping.md#calculated-fields) per passaggi specifici su come creare campi calcolati.

Se trasferisci dati a Platform utilizzando una connessione di origine, puoi configurare l’origine per utilizzare i campi calcolati. Consulta la sezione [documentazione per la fonte specifica](../../sources/home.md) per istruzioni su come implementare i campi calcolati durante la configurazione della connessione.

## Gruppi di campi di schema compatibili {#field-groups}

>[!NOTE]
>
>I nomi di diversi gruppi di campi sono stati modificati. Vedi il documento su [aggiornamenti nome gruppo di campi](../field-groups/name-updates.md) per ulteriori informazioni.

L&#39;Adobe fornisce diversi gruppi di campi standard da utilizzare con [!DNL XDM ExperienceEvent] classe. Di seguito è riportato un elenco di alcuni gruppi di campi comunemente utilizzati per la classe:

* [[!UICONTROL Estensione completa Adobe Analytics ExperienceEvent]](../field-groups/event/analytics-full-extension.md)
* [[!UICONTROL Trasferimenti saldo]](../field-groups/event/balance-transfers.md)
* [[!UICONTROL Dettagli di marketing della campagna]](../field-groups/event/campaign-marketing-details.md)
* [[!UICONTROL Azioni carta]](../field-groups/event/card-actions.md)
* [[!UICONTROL Dettagli canale]](../field-groups/event/channel-details.md)
* [[!UICONTROL Dettagli Commerce]](../field-groups/event/commerce-details.md)
* [[!UICONTROL Dettagli versamento]](../field-groups/event/deposit-details.md)
* [[!UICONTROL Dettagli sulla permuta dei dispositivi]](../field-groups/event/device-trade-in-details.md)
* [[!UICONTROL Prenotazione ristorante]](../field-groups/event/dining-reservation.md)
* [[!UICONTROL Dettagli ID utente finale]](../field-groups/event/enduserids.md)
* [[!UICONTROL Dettagli dell’ambiente]](../field-groups/event/environment-details.md)
* [[!UICONTROL Prenotazione del volo]](../field-groups/event/flight-reservation.md)
* [[!UICONTROL Consenso IAB TCF 2.0]](../field-groups/event/iab.md)
* [[!UICONTROL Prenotazione alloggio]](../field-groups/event/lodging-reservation.md)
* [[!UICONTROL Dettagli richiesta preventivo]](../field-groups/event/quote-request-details.md)
* [[!UICONTROL Dettagli prenotazione]](../field-groups/event/reservation-details.md)
* [[!UICONTROL Dettagli web]](../field-groups/event/web-details.md)

## Appendice

La sezione seguente contiene informazioni aggiuntive sulle [!UICONTROL XDM ExperienceEvent] classe.

### Valori accettati per `eventType` {#eventType}

La tabella seguente illustra i valori accettati per `eventType`, insieme alle relative definizioni:

| Valore | Definizione |
| --- | --- |
| `advertising.clicks` | Azioni di clic su un annuncio pubblicitario. |
| `advertising.completes` | Una risorsa multimediale a tempo è stata guardata fino al completamento. Questo non significa necessariamente che lo spettatore abbia guardato l&#39;intero video, poiché potrebbe aver saltato delle parti per andare avanti. |
| `advertising.conversions` | Azioni predefinite eseguite da un cliente che attivano un evento per la valutazione delle prestazioni. |
| `advertising.federated` | Indica se un evento esperienza è stato creato tramite la federazione di dati (condivisione di dati tra clienti). |
| `advertising.firstQuartiles` | Un annuncio video digitale è stato riprodotto a velocità normale per il 25% della sua durata. |
| `advertising.impressions` | Impression di un annuncio pubblicitario rivolto a un cliente potenzialmente visualizzato. |
| `advertising.midpoints` | Un annuncio video digitale è stato riprodotto a velocità normale per il 50% della sua durata. |
| `advertising.starts` | È stata avviata la riproduzione di un annuncio video digitale. |
| `advertising.thirdQuartiles` | Un annuncio video digitale è stato riprodotto a velocità normale per il 75% della sua durata. |
| `advertising.timePlayed` | Descrive la quantità di tempo trascorso da un utente su una specifica risorsa multimediale a tempo. |
| `application.close` | Un&#39;applicazione è stata chiusa o inviata in background. |
| `application.launch` | Applicazione avviata o messa in primo piano. |
| `commerce.checkouts` | Si è verificato un evento di pagamento per un elenco di prodotti. Ci può essere più di un evento di pagamento se ci sono più passaggi in un processo di pagamento. Se sono presenti più passaggi, la marca temporale e la pagina/esperienza di riferimento per ciascun evento vengono utilizzate per identificare ogni singolo evento (passaggio), rappresentato in ordine. |
| `commerce.productListAdds` | Un prodotto è stato aggiunto all’elenco dei prodotti o al carrello. |
| `commerce.productListOpens` | È stato inizializzato o creato un nuovo elenco di prodotti (carrello). |
| `commerce.productListRemovals` | Una o più voci prodotto sono state rimosse da un elenco di prodotti o da un carrello. |
| `commerce.productListReopens` | Un elenco di prodotti (carrello) non più accessibile (abbandonato) è stato riattivato da un cliente, ad esempio tramite un’attività di remarketing. |
| `commerce.productListViews` | Un elenco di prodotti o un carrello ha ricevuto una o più visualizzazioni. |
| `commerce.productViews` | Un prodotto ha ricevuto una o più visualizzazioni. |
| `commerce.purchases` | Un ordine è stato accettato. Questa è l’unica azione richiesta in una conversione commerce. Un evento di acquisto deve fare riferimento a un elenco di prodotti. |
| `commerce.saveForLaters` | Un elenco di prodotti è stato salvato per un utilizzo futuro, ad esempio una lista di desideri del prodotto. |
| `decisioning.propositionDisplay` | Una proposta decisionale è stata visualizzata a una persona. |
| `decisioning.propositionInteract` | Una persona ha interagito con una proposta decisionale. |
| `delivery.feedback` | Eventi di feedback per una consegna, ad esempio una consegna e-mail. |
| `directMarketing.emailBounced` | Un’e-mail a una persona non recapitata. |
| `directMarketing.emailBouncedSoft` | Un’e-mail a una persona non recapitata in modo permanente. |
| `directMarketing.emailClicked` | Una persona ha fatto clic su un collegamento in un’e-mail di marketing. |
| `directMarketing.emailDelivered` | Un messaggio e-mail è stato recapitato al servizio e-mail dell&#39;utente |
| `directMarketing.emailOpened` | Una persona ha aperto un’e-mail di marketing. |
| `directMarketing.emailUnsubscribed` | Persona che ha annullato l’abbonamento a un’e-mail di marketing. |
| `inappmessageTracking.dismiss` | Un messaggio in-app è stato ignorato. |
| `inappmessageTracking.display` | È stato visualizzato un messaggio in-app. |
| `inappmessageTracking.interact` | È stato interagito un messaggio in-app con. |
| `leadOperation.callWebhook` | È stato chiamato un webhook in risposta a un lead. |
| `leadOperation.convertLead` | Un lead è stato convertito. |
| `leadOperation.interestingMoment` | È stato registrato un momento interessante per una persona. |
| `leadOperation.newLead` | È stato creato un lead. |
| `leadOperation.scoreChanged` | Il valore dell’attributo di punteggio del lead è stato modificato. |
| `leadOperation.statusInCampaignProgressionChanged` | Lo stato di un lead in una campagna è cambiato. |
| `listOperation.addToList` | Persona aggiunta a un elenco di marketing. |
| `listOperation.removeFromList` | Una persona è stata rimossa da un elenco di marketing. |
| `message.feedback` | Eventi di feedback come inviato/non recapitato/errore per messaggi inviati a un cliente. |
| `message.tracking` | Tracciamento di eventi come azioni di apertura/clic/personalizzate sui messaggi inviati a un cliente. |
| `opportunityEvent.addToOpportunity` | Una persona è stata aggiunta a un’opportunità. |
| `opportunityEvent.opportunityUpdated` | Un’opportunità è stata aggiornata. |
| `opportunityEvent.removeFromOpportunity` | Una persona è stata rimossa da un&#39;opportunità. |
| `pushTracking.applicationOpened` | Una persona ha aperto un’applicazione da una notifica push. |
| `pushTracking.customAction` | Una persona ha fatto clic su un’azione personalizzata in una notifica push. |
| `web.formFilledOut` | Una persona ha compilato un modulo su una pagina web. |
| `web.webinteraction.linkClicks` | Un collegamento è stato selezionato una o più volte. |
| `web.webpagedetails.pageViews` | Una pagina Web ha ricevuto una o più visualizzazioni. |

{style="table-layout:auto"}

### Valori consigliati per `producedBy` {#producedBy}

Nella tabella seguente sono illustrati alcuni valori accettati per `producedBy`:

| Valore | Definizione |
| --- | --- |
| `self` | Autonomo |
| `system` | Sistema |
| `salesRef` | Rappresentante commerciale |
| `customerRep` | Rappresentante del cliente |
