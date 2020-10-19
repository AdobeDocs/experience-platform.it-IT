---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;identityMap;identity map;Identity map;Schema design;map;Map;union schema;union
solution: Experience Platform
title: Classe ExperienceEvent XDM
topic: overview
description: Questo documento fornisce una panoramica della classe ExperienceEvent XDM.
translation-type: tm+mt
source-git-commit: b7b57c0b70b1af3a833f0386bc809bb92c9b50f8
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 0%

---


# [!DNL XDM ExperienceEvent] class

[!DNL XDM ExperienceEvent] è una classe XDM standard che consente di creare uno snapshot con marca temporale del sistema quando si verifica un evento specifico o viene raggiunto un determinato insieme di condizioni.

Un Evento esperienza è un record di fatti relativi a quanto è accaduto, compreso il momento nel tempo e l&#39;identità dell&#39;individuo coinvolto. Gli eventi possono essere espliciti (azioni umane direttamente osservabili) o impliciti (generati senza un&#39;azione umana diretta) e sono registrati senza aggregazione o interpretazione. Per ulteriori informazioni di alto livello sull&#39;utilizzo di questa classe nell&#39;ecosistema della piattaforma, fare riferimento alla panoramica [](../home.md#data-behaviors)XDM.

La [!DNL XDM ExperienceEvent] classe stessa fornisce a uno schema diversi campi relativi alle serie temporali. I valori di alcuni di questi campi vengono compilati automaticamente al momento dell&#39;assimilazione dei dati:

<img src="../images/classes/experienceevent.png" width="650" /><br />

| Proprietà | Descrizione |
| --- | --- |
| `_id` | Identificatore di stringa univoco generato dal sistema per l&#39;evento. Questo campo viene utilizzato per tenere traccia dell&#39;univocità di un singolo evento, per impedire la duplicazione dei dati e per ricercare tale evento nei servizi a valle. Poiché questo campo è generato dal sistema, non deve essere fornito un valore esplicito durante l&#39;assimilazione dei dati.<br><br>È importante distinguere che questo campo **non** rappresenta un&#39;identità relativa a una singola persona, ma piuttosto il record dei dati stessi. I dati di identità relativi a una persona devono essere relegati ai campi [di](../schema/composition.md#identity) identità. |
| `eventMergeId` | ID del batch assimilato che ha causato la creazione del record. Questo campo viene compilato automaticamente dal sistema al momento dell&#39;inserimento dei dati. |
| `eventType` | Una stringa che indica il tipo di evento principale per il record. I valori accettati e le relative definizioni sono forniti nella sezione [dell&#39;](#eventType)appendice. |
| `identityMap` | Campo mappa che contiene un insieme di identità con nome per l&#39;individuo a cui si applica l&#39;evento. Questo campo viene aggiornato automaticamente dal sistema durante l&#39;acquisizione dei dati di identità. Per utilizzare correttamente questo campo per il profilo [cliente in tempo](../../profile/home.md)reale, non tentare di aggiornare manualmente il contenuto del campo nelle operazioni di dati.<br /><br />Per ulteriori informazioni sul caso di utilizzo, vedere la sezione sulle mappe di identità nelle [nozioni di base della composizione](../schema/composition.md#identityMap) dello schema. |
| `timestamp` | L&#39;ora in cui si è verificato l&#39;evento o l&#39;osservazione. |

## Mixer compatibili {#mixins}

 Adobe offre diversi mixin standard da utilizzare con la [!DNL XDM ExperienceEvent] classe. Di seguito è riportato un elenco di alcuni mixin comunemente utilizzati per la classe:

* [[!UICONTROL ExperienceEvent EndUserIDs]](../mixins/event/enduserids.md)
* [[!UICONTROL ExperienceEvent environment details]](../mixins/event/environment-details.md)

## Appendice

La sezione seguente contiene informazioni aggiuntive sulla [!UICONTROL XDM ExperienceEvent] classe.

### Valori accettati per xdm:eventType {#eventType}

Nella tabella seguente sono riportati i valori accettati per `xdm:eventType`, con le relative definizioni:

| Valore | Definizione |
| --- | --- |
| `advertising.completes` | Una risorsa multimediale temporizzata è stata controllata al completamento. Ciò non significa necessariamente che il visualizzatore abbia guardato l’intero video, poiché il visualizzatore avrebbe potuto saltare in avanti. |
| `advertising.timePlayed` | Descrive il tempo trascorso da un utente su una risorsa multimediale temporizzata specifica. |
| `advertising.federated` | Indica se un evento esperienza è stato creato tramite la federazione di dati (condivisione di dati tra i clienti). |
| `advertising.clicks` | Fate clic sulle azioni presenti in un annuncio pubblicitario. |
| `advertising.conversions` | Azioni predefinite eseguite da un cliente che attiva un evento per la valutazione delle prestazioni. |
| `advertising.firstQuartiles` | Un annuncio video digitale ha riprodotto fino al 25% della sua durata a velocità normale. |
| `advertising.impressions` | Impression(e) di un annuncio pubblicitario per un cliente con il potenziale di essere visualizzato. |
| `advertising.midpoints` | Un annuncio video digitale ha riprodotto fino al 50% della sua durata a velocità normale. |
| `advertising.starts` | La riproduzione di un annuncio video digitale è iniziata. |
| `advertising.thirdQuartiles` | Un annuncio video digitale ha riprodotto fino al 75% della sua durata a velocità normale. |
| `web.webpagedetails.pageViews` | Una pagina Web ha ricevuto una o più visualizzazioni. |
| `web.webinteraction.linkClicks` | A un collegamento sono stati ricevuti uno o più clic. |
| `commerce.checkouts` | Si è verificato un evento di checkout per un elenco di prodotti. Se in un processo di estrazione sono presenti più passaggi, può verificarsi più di un evento di estrazione. Se sono presenti più passaggi, la marca temporale e la pagina/esperienza di riferimento per ogni evento vengono utilizzati per identificare ogni singolo evento (passaggio), rappresentato nell&#39;ordine. |
| `commerce.productListAdds` | Un prodotto è stato aggiunto all&#39;elenco dei prodotti o al carrello. |
| `commerce.productListOpens` | È stato inizializzato o creato un nuovo elenco di prodotti (carrello acquisti). |
| `commerce.productListRemovals` | Una o più voci di prodotto sono state rimosse da un elenco di prodotti o da un carrello. |
| `commerce.productListReopens` | Un elenco di prodotti (carrello acquisti) non più accessibile (abbandonato) è stato riattivato da un cliente, ad esempio tramite un&#39;attività di remarketing. |
| `commerce.productListViews` | Una o più viste sono state ricevute da un elenco di prodotti o da un carrello. |
| `commerce.productViews` | Un prodotto ha ricevuto una o più visualizzazioni. |
| `commerce.purchases` | Un ordine è stato accettato. Questa è l&#39;unica azione richiesta in una conversione di commercio. A un evento di acquisto deve essere fatto riferimento a un elenco di prodotti. |
| `commerce.saveForLaters` | Un elenco di prodotti è stato salvato per uso futuro, ad esempio un elenco di prodotti. |
| `delivery.feedback` | Eventi di feedback per una consegna, ad esempio una consegna tramite e-mail. |
| `message.feedback` | Eventi di feedback come inviati/rimbalzi/errori per i messaggi inviati a un cliente. |
| `message.tracking` | Tracciamento di eventi quali azioni di apertura/clic/personalizzato sui messaggi inviati a un cliente. |