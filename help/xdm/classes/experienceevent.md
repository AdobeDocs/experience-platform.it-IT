---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;profilo individuale;campi;schemi;schemi;mappa identità;mappa identità;mappa identità;schema schema;mappa schema;mappa;schema unione;unione
solution: Experience Platform
title: Classe ExperienceEvent XDM
topic-legacy: overview
description: Questo documento fornisce una panoramica della classe ExperienceEvent XDM.
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
translation-type: tm+mt
source-git-commit: 9b63b38e664e5776ca638f8ed407896f185bcab0
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 1%

---

# [!DNL XDM ExperienceEvent] Classe

[!DNL XDM ExperienceEvent] è una classe XDM standard che consente di creare un’istantanea con marca temporale del sistema quando si verifica un evento specifico o viene raggiunto un determinato insieme di condizioni.

Un evento di esperienza è un record di fatto di ciò che si è verificato, compreso il momento nel tempo e l&#39;identità dell&#39;individuo coinvolto. Gli eventi possono essere espliciti (azioni umane direttamente osservabili) o impliciti (generati senza un&#39;azione umana diretta) e sono registrati senza aggregazione o interpretazione. Per ulteriori informazioni di alto livello sull’utilizzo di questa classe nell’ecosistema della piattaforma, consulta la [panoramica XDM](../home.md#data-behaviors).

La classe [!DNL XDM ExperienceEvent] fornisce a uno schema diversi campi relativi alle serie temporali. I valori di alcuni di questi campi vengono compilati automaticamente al momento dell’acquisizione dei dati:

<img src="../images/classes/experienceevent.png" width="650" /><br />

| Proprietà | Descrizione |
| --- | --- |
| `_id` | Identificatore stringa univoco generato dal sistema per l&#39;evento. Questo campo viene utilizzato per tenere traccia dell’univocità di un singolo evento, prevenire la duplicazione dei dati e per cercare tale evento nei servizi a valle. Poiché questo campo è generato dal sistema, non deve essere fornito un valore esplicito durante l’inserimento dei dati.<br><br>È importante distinguere che questo campo  **non** rappresenta un&#39;identità correlata a una singola persona, ma piuttosto il record dei dati stessi. I dati di identità relativi a una persona devono essere invece relegati a [campi di identità](../schema/composition.md#identity). |
| `eventMergeId` | ID del batch acquisito che ha causato la creazione del record. Questo campo viene compilato automaticamente dal sistema al momento dell’inserimento dei dati. |
| `eventType` | Una stringa che indica il tipo di evento principale per il record. I valori accettati e le relative definizioni sono forniti nella sezione [appendice](#eventType). |
| `identityMap` | Campo mappa contenente un set di identità con spazi dei nomi per l’individuo a cui si applica l’evento. Questo campo viene aggiornato automaticamente dal sistema durante l’acquisizione dei dati di identità. Per utilizzare correttamente questo campo per [Profilo cliente in tempo reale](../../profile/home.md), non tentare di aggiornare manualmente il contenuto del campo nelle operazioni sui dati.<br /><br />Per ulteriori informazioni sul relativo caso d’uso, consulta la sezione sulle mappe di identità nelle  [nozioni di base sulla ](../schema/composition.md#identityMap) composizione degli schemi . |
| `timestamp` | Una marca temporale ISO 8601 di quando si è verificato l’evento, formattata in base alla sezione 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) della RFC 3339.[<br><br>Questa marca temporale può rappresentare  **** solo l&#39;osservazione dell&#39;evento stesso e deve verificarsi in passato. Se i casi di utilizzo della segmentazione richiedono l’uso di marche temporali che possono verificarsi in futuro (ad esempio una data di partenza), questi valori devono essere vincolati altrove nello schema Evento esperienza. |

## Mixins compatibili {#mixins}

>[!NOTE]
>
>I nomi di diversi mixin sono cambiati. Per ulteriori informazioni, consulta il documento sugli [aggiornamenti dei nomi mixin](../mixins/name-updates.md) .

Adobe fornisce diversi mixin standard da utilizzare con la classe [!DNL XDM ExperienceEvent] . Di seguito è riportato un elenco di alcuni mixin comunemente utilizzati per la classe:

* [[!UICONTROL End User ID Details]](../mixins/event/enduserids.md)
* [[!UICONTROL Environment Details]](../mixins/event/environment-details.md)

## Appendice

La sezione seguente contiene informazioni aggiuntive sulla classe [!UICONTROL XDM ExperienceEvent] .

### Valori accettati per xdm:eventType {#eventType}

La tabella seguente illustra i valori accettati per `xdm:eventType`, insieme alle relative definizioni:

| Valore | Definizione |
| --- | --- |
| `advertising.completes` | Una risorsa multimediale temporizzata è stata controllata al completamento. Questo non significa necessariamente che lo spettatore abbia guardato l&#39;intero video, dato che lo spettatore avrebbe potuto saltare in avanti. |
| `advertising.timePlayed` | Descrive il tempo trascorso da un utente su una specifica risorsa multimediale temporizzata. |
| `advertising.federated` | Indica se è stato creato un evento esperienza tramite la federazione di dati (condivisione di dati tra i clienti). |
| `advertising.clicks` | Fai clic su azioni su un annuncio. |
| `advertising.conversions` | Azioni predefinite eseguite da un cliente che attivano un evento per la valutazione delle prestazioni. |
| `advertising.firstQuartiles` | Un annuncio video digitale ha riprodotto fino al 25% della sua durata a velocità normale. |
| `advertising.impressions` | Impressioni di un annuncio pubblicitario per un cliente con il potenziale di essere visualizzato. |
| `advertising.midpoints` | Un annuncio video digitale ha riprodotto fino al 50% della sua durata a velocità normale. |
| `advertising.starts` | È iniziata la riproduzione di un annuncio video digitale. |
| `advertising.thirdQuartiles` | Un annuncio video digitale ha riprodotto fino al 75% della sua durata a velocità normale. |
| `web.webpagedetails.pageViews` | Una pagina web ha ricevuto una o più visualizzazioni. |
| `web.webinteraction.linkClicks` | Un collegamento è stato selezionato una o più volte. |
| `commerce.checkouts` | Si è verificato un evento di pagamento per un elenco di prodotti. Se in un processo di pagamento sono presenti più passaggi, può essere presente più di un evento di pagamento. Se sono presenti più passaggi, la marca temporale e la pagina/esperienza di riferimento per ogni evento vengono utilizzati per identificare ogni singolo evento (passaggio), rappresentato in ordine. |
| `commerce.productListAdds` | Un prodotto è stato aggiunto all’elenco dei prodotti o al carrello. |
| `commerce.productListOpens` | È stato inizializzato o creato un nuovo elenco di prodotti (carrello acquisti). |
| `commerce.productListRemovals` | Una o più voci di prodotto sono state rimosse da un elenco di prodotti o dal carrello. |
| `commerce.productListReopens` | Un cliente ha riattivato un elenco di prodotti (carrello acquisti) che non era più accessibile (abbandonato), ad esempio tramite un’attività di remarketing. |
| `commerce.productListViews` | Una o più visualizzazioni sono state ricevute da un elenco di prodotti o dal carrello acquisti. |
| `commerce.productViews` | Un prodotto ha ricevuto una o più visualizzazioni. |
| `commerce.purchases` | Un ordine è stato accettato. Questa è l’unica azione richiesta in una conversione di e-commerce. A un evento di acquisto deve essere fatto riferimento a un elenco di prodotti. |
| `commerce.saveForLaters` | Un elenco di prodotti è stato salvato per un utilizzo futuro, ad esempio un elenco dei desideri del prodotto. |
| `delivery.feedback` | Eventi di feedback per una consegna, ad esempio una consegna e-mail. |
| `message.feedback` | Eventi di feedback come sent/bounce/error per i messaggi inviati a un cliente. |
| `message.tracking` | Tracciamento di eventi come azioni aperte/clic/personalizzate sui messaggi inviati a un cliente. |
