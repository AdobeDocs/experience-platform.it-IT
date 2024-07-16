---
title: Nuovo coinvolgimento intelligente
description: Offri esperienze coinvolgenti e connesse durante i momenti chiave della conversione, per coinvolgere nuovamente in modo intelligente la clientela poco frequente.
feature: Use Cases
exl-id: 13f6dbc9-7471-40bf-824d-27922be0d879
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '3894'
ht-degree: 4%

---

# Coinvolgi nuovamente i tuoi clienti con intelligenza, per farli tornare

>[!NOTE]
>
>Questa è un’implementazione di esempio e gli esempi riportati in questa pagina, ad esempio la sintassi dei segmenti, sono meramente esempi. Utilizza gli esempi come guida, in quanto la tua implementazione potrebbe differire.

Coinvolgi nuovamente i clienti che hanno abbandonato una conversione in modo intelligente e responsabile. Coinvolgi i clienti meno esperti con esperienze per aumentare la conversione e il valore del ciclo di vita del client.

Utilizza considerazioni in tempo reale, prendi in considerazione tutte le qualità e i comportamenti dei consumatori e offri una riqualificazione rapida in base a eventi online e offline.

Di seguito è riportata una panoramica dell’architettura di alto livello dei vari componenti di Real-Time CDP e Journey Optimizer. Questo diagramma mostra il modo in cui i dati fluiscono attraverso le due app di Experience Platform, dalla raccolta dati al punto in cui vengono attivati tramite percorsi o campagne verso le destinazioni, per ottenere il caso d’uso descritto in questa pagina.

![Panoramica visiva di alto livello sul coinvolgimento intelligente.](../intelligent-re-engagement/images/step-by-step.png)

## Panoramica del caso d’uso {#overview}

Costruirai schemi, set di dati e tipi di pubblico mentre lavori attraverso esempi di scenari di ricoinvolgimento. Scoprirai anche le funzionalità necessarie per impostare i percorsi di esempio in [!DNL Adobe Journey Optimizer] e quelle necessarie per creare annunci pubblicitari a pagamento nelle destinazioni. Questa guida utilizza esempi di coinvolgimento dei clienti nei percorsi di casi d’uso descritti di seguito:

* **Scenario di abbandono della navigazione del prodotto** - Eseguire il targeting dei clienti che hanno abbandonato la navigazione del prodotto sia sul sito Web che sull&#39;app mobile.
* **Scenario carrello abbandonato** - Eseguire il targeting dei clienti che hanno inserito prodotti nel carrello ma non sono ancora stati acquistati sia sul sito Web che sull&#39;app mobile.
* **Scenario di conferma dell&#39;ordine** - Concentrati sugli acquisti di prodotti effettuati tramite il sito Web e l&#39;app mobile.

## Prerequisiti e pianificazione {#prerequisites-and-planning}

Una volta completati i passaggi per implementare il caso d’uso, utilizzerai le seguenti funzionalità di Real-Time CDP e Adobe Journey Optimizer (elencate nell’ordine in cui verranno utilizzate). Assicurati di disporre delle [autorizzazioni di controllo degli accessi basate su attributi](/help/access-control/home.md) per tutte queste aree o richiedi all’amministratore di sistema di concedere le autorizzazioni necessarie.

* [[!DNL Adobe Real-Time Customer Data Platform (Real-Time CDP)]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html) - Integra i dati tra le origini dati per alimentare la campagna. Questi dati vengono quindi utilizzati per creare i tipi di pubblico della campagna e far emergere elementi di dati personalizzati utilizzati nell’e-mail e nelle tessere delle promozioni web (ad esempio, nome o informazioni relative all’account). CDP viene utilizzato anche per attivare i tipi di pubblico tra e-mail e sul Web (tramite [!DNL Adobe Target]).
   * [Schemi](/help/xdm/home.md)
   * [Profili](/help/profile/home.md)
   * [Set di dati](/help/catalog/datasets/overview.md)
   * [Tipi di pubblico](/help/segmentation/home.md)
   * [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)
   * [Destinazioni](/help/destinations/home.md)

* [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer-learn/tutorials/introduction-to-journey-optimizer/introduction.html?lang=it) - Consente di fornire ai clienti esperienze connesse, contestuali e personalizzate.
   * [Attivatore evento o pubblico](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/collect-event-data/data-collection.html)
   * [Tipi di pubblico/Eventi](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/about-audiences.html?lang=it)
   * [Azioni Percorso](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)

## Come ottenere il caso d’uso {#achieve-use-case-instruction}

Di seguito è riportata una panoramica generale dei tre scenari di ricoinvolgimento di esempio.

>[!BEGINTABS]

>[!TAB Scenario di navigazione prodotto abbandonato]

Lo scenario di navigazione dei prodotti abbandonati è incentrato sulla navigazione dei prodotti abbandonati sia sul sito web che sull’app mobile. Questo scenario si attiva quando un prodotto viene visualizzato ma non acquistato o aggiunto al carrello. In questo esempio, il brand engagement viene attivato dopo tre giorni se non ci sono aggiunte di elenchi nelle ultime 24 ore.<p>![Panoramica visiva di alto livello dello scenario di ricerca intelligente dei prodotti abbandonato dal cliente.](../intelligent-re-engagement/images/re-engagement-journey.png "Panoramica visiva di alto livello dello scenario di navigazione prodotto abbandonato e intelligente per il cliente."){width="1920" zoomable="yes"}</p>

1. Puoi creare schemi e set di dati, quindi abilitare per [!UICONTROL Profilo].
2. Acquisisci i dati in Experience Platform tramite Web SDK, Mobile SDK o API. È possibile utilizzare anche il connettore Source di Analytics, ma potrebbe causare latenza del percorso.
3. Acquisisci dati aggiuntivi abilitati per il profilo, che possono essere collegati al visitatore autenticato dell’app web e mobile tramite grafici di identità.
4. Puoi creare tipi di pubblico mirati dall&#39;elenco dei profili per verificare se un **cliente** ha creato un coinvolgimento negli ultimi tre giorni.
5. Si crea un percorso di ricerca prodotti abbandonato in [!DNL Adobe Journey Optimizer].
6. Se necessario, collabora con il **partner dati** per l&#39;attivazione dei tipi di pubblico nelle destinazioni desiderate per i file multimediali a pagamento.
7. [!DNL Adobe Journey Optimizer] verifica il consenso e invia le varie azioni configurate.

>[!TAB Scenario carrello abbandonato]

Lo scenario del carrello abbandonato si applica quando i prodotti sono stati inseriti nel carrello ma non sono ancora stati acquistati sia sul sito web che sull’app mobile. Inoltre, le campagne Paid Media vengono avviate e interrotte utilizzando questo metodo.<p>![Panoramica visiva di alto livello dello scenario del carrello abbandonato dal cliente.](../intelligent-re-engagement/images/abandoned-cart-journey.png "Panoramica visiva di alto livello dello scenario del carrello abbandonato dal cliente."){width="1920" zoomable="yes"}</p>

1. Si creano schemi e set di dati, l&#39;abilitazione per [!UICONTROL Profilo].
2. Acquisisci i dati in Experience Platform tramite Web SDK, Mobile SDK o API. È possibile utilizzare anche il connettore Source di Analytics, ma potrebbe causare latenza del percorso.
3. Acquisisci dati aggiuntivi abilitati per il profilo, che possono essere collegati al visitatore autenticato dell’app web e mobile tramite grafici di identità.
4. Puoi creare tipi di pubblico mirati dall&#39;elenco dei profili per verificare se un **cliente** ha inserito un elemento nel carrello ma non ha completato l&#39;acquisto. L&#39;evento **[!UICONTROL Aggiungi al carrello]** avvia un timer che attende 30 minuti, quindi verifica la presenza di acquisti. Se non è stato effettuato alcun acquisto, il **cliente** viene aggiunto al pubblico **[!UICONTROL Abandon Cart]**.
5. Si crea un percorso di carrello abbandonato in [!DNL Adobe Journey Optimizer].
6. Se necessario, collabora con il **partner dati** per l&#39;attivazione dei tipi di pubblico nelle destinazioni desiderate per i file multimediali a pagamento.
7. [!DNL Adobe Journey Optimizer] verifica il consenso e invia le varie azioni configurate.

>[!TAB Scenario di conferma ordine]

Lo scenario di conferma dell’ordine si concentra sugli acquisti di prodotti effettuati tramite il sito web e l’app mobile.<p>![Panoramica visiva di alto livello dello scenario di conferma dell&#39;ordine cliente.](../intelligent-re-engagement/images/order-confirmation-journey.png "Panoramica visiva di alto livello dello scenario di conferma dell&#39;ordine cliente."){width="1920" zoomable="yes"}</p>

1. Puoi creare schemi e set di dati, quindi abilitare per [!UICONTROL Profilo].
2. Acquisisci i dati in Experience Platform tramite Web SDK, Mobile SDK o API. È possibile utilizzare anche il connettore Source di Analytics, ma potrebbe causare latenza del percorso.
3. Acquisisci dati aggiuntivi abilitati per il profilo, che possono essere collegati al visitatore autenticato dell’app web e mobile tramite grafici di identità.
4. È possibile creare un percorso di conferma in [!DNL Adobe Journey Optimizer].
5. [!DNL Adobe Journey Optimizer] invia un messaggio di conferma dell&#39;ordine utilizzando il canale preferito.

>[!ENDTABS]

Per completare ciascuno dei passaggi descritti nelle panoramiche di alto livello precedenti, leggere le sezioni seguenti, che offrono collegamenti a ulteriori informazioni e istruzioni più dettagliate.

### Creare schemi e specificare gruppi di campi {#schema-design}

Le risorse Experience Data Model (XDM) sono gestite nell&#39;area di lavoro [!UICONTROL Schemi] in [!DNL Adobe Experience Platform]. È possibile visualizzare ed esplorare le risorse di base fornite da [!DNL Adobe] (ad esempio i gruppi di campi) e creare risorse e schemi personalizzati per l&#39;organizzazione.

Per ulteriori informazioni sulla creazione di [schemi](/help/xdm/home.md), vedere l&#39;esercitazione [crea schema.](/help/xdm/tutorials/create-schema-ui.md) e [Modellare i dati sull&#39;esperienza del cliente con XDM](https://experienceleague.adobe.com/docs/courses/using/experienceplatform-d-1-2021-1-xdm.html).

Per il caso di utilizzo del ricoinvolgimento vengono utilizzate quattro progettazioni di schemi. Ogni schema richiede la configurazione di campi specifici. Devi abilitare lo schema per essere incluso nel Profilo cliente in tempo reale. Per ulteriori informazioni sull&#39;abilitazione dello schema per l&#39;utilizzo in Real-Time Customer Profile, leggere [enable a schema for Real-Time Customer Profile](/help/xdm/ui/resources/schemas.md#enable-a-schema-for-real-time-customer-profile) (Abilitare uno schema per Real-Time Customer Profile).

#### Schema attributi cliente

Questo schema viene utilizzato per strutturare e fare riferimento ai dati di profilo che compongono le informazioni sul cliente. Questi dati vengono generalmente acquisiti in [!DNL Adobe Experience Platform] tramite il sistema CRM o simile e sono necessari per fare riferimento ai dettagli dei clienti utilizzati per la personalizzazione, il consenso al marketing e le funzionalità avanzate di pubblico.

Lo schema di attributi del cliente è rappresentato da una classe [[!UICONTROL XDM Individual Profile]](/help/xdm/classes/individual-profile.md), che include i seguenti gruppi di campi:

+++Dati di contatto personali (gruppo di campi)

[Dettagli contatto personale](/help/xdm/field-groups/profile/personal-contact-details.md) è un gruppo di campi di schema standard per la classe Profilo individuale XDM che descrive le informazioni di contatto per una singola persona.

| Campi | Descrizione |
| --- | --- |
| `mobilePhone.number` | Il numero di telefono cellulare della persona, che verrà utilizzato per gli SMS. |
| `personalEmail.address` | Indirizzo e-mail della persona. |

+++

+++Dettagli di controllo del sistema Source esterno (gruppo di campi)

[External Source System Audit Attributes](/help/xdm/data-types/external-source-system-audit-attributes.md) è un tipo di dati XDM (Experience Data Model) standard che acquisisce i dettagli di controllo di un sistema di origine esterno.

+++

+++Gruppi di campi di consenso e preferenze (gruppo di campi)

Il gruppo di campi [Consensi e preferenze](/help/xdm/field-groups//profile/consents.md) fornisce un singolo campo di tipo oggetto, Consensi, per acquisire informazioni sul consenso e sulle preferenze.

| Campi | Requisito |
| --- | --- |
| `consents.marketing.email.val` | Obbligatorio |
| `consents.marketing.preferred` | Obbligatorio |
| `consents.marketing.push.val` | Obbligatorio |
| `consents.marketing.sms.val` | Obbligatorio |
| `consents.personalize.content.val` | Obbligatorio |
| `consents.share.val` | Obbligatorio |

+++

+++Dettagli test profilo (gruppo di campi)

Questo gruppo di campi ti consente di testare il percorso prima che venga pubblicato, utilizzando i profili di test. Per ulteriori informazioni sulla creazione di profili di test, leggere l&#39;esercitazione [creazione di profili di test](https://experienceleague.adobe.com/docs/journeys/using/building-journeys/about-journey-building/creating-test-profiles.html) e l&#39;esercitazione [verifica del percorso](https://experienceleague.adobe.com/docs/journeys/using/building-journeys/testing-the-journey.html).

+++

#### Schema transazioni digitali cliente

Questo schema viene utilizzato per strutturare e fare riferimento ai dati dell’evento che costituisce l’attività del cliente che si verifica sul sito web o sulle piattaforme digitali associate. Questi dati vengono in genere acquisiti in [!DNL Adobe Experience Platform] tramite [Web SDK](/help/web-sdk/home.md) e sono necessari per fare riferimento ai vari eventi di navigazione e conversione utilizzati per l&#39;attivazione di percorsi, l&#39;analisi dettagliata dei clienti online, le funzionalità avanzate del pubblico e la messaggistica personalizzata.

Lo schema delle transazioni digitali del cliente è rappresentato da una classe [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md).

+++XDM ExperienceEvent (classe)

La classe [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) include i seguenti gruppi di campi:

| Campi | Descrizione |
| --- | --- |
| `_id` | Identifica in modo univoco i singoli eventi acquisiti in [!DNL Adobe Experience Platform]. |
| `timestamp` | Una marca temporale ISO 8601 indicante quando si è verificato l’evento, formattata come indicato nella sezione 5.6 della RFC 3339. Questa marca temporale deve essere nel passato. |
| `eventType` | Stringa che indica il tipo di categoria per l’evento. |

+++

+++Dettagli ID utente finale (gruppo di campi)

Il gruppo di campi [Dettagli ID utente finale](/help/xdm/field-groups/event/enduserids.md) viene utilizzato per descrivere le informazioni sull&#39;identità di un individuo in diverse applicazioni di Adobe.

| Campi | Descrizione |
| --- | --- |
| `endUserIDs._experience.emailid.authenticatedState` | Stato di autenticazione dell’ID dell’indirizzo e-mail dell’utente finale. |
| `endUserIDs._experience.emailid.id` | ID indirizzo e-mail utente finale. |
| `endUserIDs._experience.emailid.namespace.code` | Codice spazio dei nomi dell’indirizzo e-mail dell’utente finale. |
| `endUserIDs._experience.mcid.authenticatedState` | Stato di autenticazione dell&#39;ID Marketing Cloud (MCID) [!DNL Adobe]. Il MCID è ora noto come ID Experience Cloud (ECID). |
| `endUserIDs._experience.mcid.id` | ID Marketing Cloud [!DNL Adobe] (MCID). Il MCID è ora noto come ID Experience Cloud (ECID). |
| `endUserIDs._experience.mcid.namespace.code` | Codice spazio dei nomi ID Marketing Cloud (MCID) [!DNL Adobe]. |

+++

+++Dettagli Commerce (gruppo di campi)

Il gruppo di campi [Dettagli Commerce](/help/xdm/field-groups/event/commerce-details.md) viene utilizzato per descrivere dati commerciali quali informazioni sul prodotto (SKU, nome, quantità) e operazioni standard del carrello (ordine, pagamento, abbandono).

| Campi | Descrizione |
| --- | --- |
| `commerce.cart.cartID` | Un ID per il carrello. |
| `commerce.order.orderType` | Oggetto che descrive il tipo di ordine del prodotto. |
| `commerce.order.payments.paymentAmount` | Oggetto che descrive l&#39;importo del pagamento dell&#39;ordine di prodotto. |
| `commerce.order.payments.paymentType` | Oggetto che descrive il tipo di pagamento dell&#39;ordine di prodotto. |
| `commerce.order.payments.transactionID` | ID transazione ordine prodotti oggetto. |
| `commerce.order.purchaseID` | Un ID acquisto ordine prodotto oggetto. |
| `productListItems.name` | Un elenco di nomi di articoli che rappresentano i prodotti selezionati da un cliente. |
| `productListItems.priceTotal` | Il prezzo totale del listino di articoli che rappresentano i prodotti selezionati da un cliente. |
| `productListItems.product` | I prodotti selezionati. |
| `productListItems.quantity` | Quantità di elenco di articoli che rappresentano i prodotti selezionati da un cliente. |

+++

+++Dettagli di controllo del sistema Source esterno (gruppo di campi)

External Source System Audit Attributes è un tipo di dati standard Experience Data Model (XDM) che acquisisce dettagli di audit su un sistema di origine esterno.

+++

#### Schema transazioni cliente offline

Questo schema viene utilizzato per strutturare e fare riferimento ai dati dell’evento che costituisce l’attività del cliente che si verifica su piattaforme al di fuori del sito web. Questi dati vengono generalmente acquisiti in [!DNL Adobe Experience Platform] da un POS (o sistema simile) e il più delle volte inviati in streaming a Platform tramite una connessione API. Il suo scopo è quello di fare riferimento ai vari eventi di conversione offline utilizzati per attivare percorsi, analisi approfondite dei clienti online e offline, funzionalità di pubblico avanzate e messaggi personalizzati.

Lo schema di transazioni cliente offline è rappresentato da una classe [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md).

+++XDM ExperienceEvent (classe)

La classe [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) include i seguenti gruppi di campi:

| Campi | Descrizione |
| --- | --- |
| `_id` | Identifica in modo univoco i singoli eventi acquisiti in [!DNL Adobe Experience Platform]. |
| `timestamp` | Una marca temporale ISO 8601 indicante quando si è verificato l’evento, formattata come indicato nella sezione 5.6 della RFC 3339. Questa marca temporale deve essere nel passato. |
| `eventType` | Stringa che indica il tipo di categoria per l’evento. |

+++

+++Dettagli Commerce (gruppo di campi)

Il gruppo di campi [Dettagli Commerce](/help/xdm/field-groups/event/commerce-details.md) viene utilizzato per descrivere dati commerciali quali informazioni sul prodotto (SKU, nome, quantità) e operazioni standard del carrello (ordine, pagamento, abbandono).

| Campi | Descrizione |
| --- | --- |
| `commerce.cart.cartID` | Un ID per il carrello. |
| `commerce.order.orderType` | Oggetto che descrive il tipo di ordine del prodotto. |
| `commerce.order.payments.paymentAmount` | Oggetto che descrive l&#39;importo del pagamento dell&#39;ordine di prodotto. |
| `commerce.order.payments.paymentType` | Oggetto che descrive il tipo di pagamento dell&#39;ordine di prodotto. |
| `commerce.order.payments.transactionID` | ID transazione ordine prodotti oggetto. |
| `commerce.order.purchaseID` | Un ID acquisto ordine prodotto oggetto. |
| `productListItems.name` | Un elenco di nomi di articoli che rappresentano i prodotti selezionati da un cliente. |
| `productListItems.priceTotal` | Il prezzo totale del listino di articoli che rappresentano i prodotti selezionati da un cliente. |
| `productListItems.product` | I prodotti selezionati. |
| `productListItems.quantity` | Quantità di elenco di articoli che rappresentano i prodotti selezionati da un cliente. |

+++

+++Dati di contatto personali (gruppo di campi)

[Dettagli contatto personale](/help/xdm/field-groups/profile/personal-contact-details.md) è un gruppo di campi di schema standard per la classe Profilo individuale XDM che descrive le informazioni di contatto per una singola persona.

| Campi | Descrizione |
| --- | --- |
| `mobilePhone.number` | Il numero di telefono cellulare della persona, che verrà utilizzato per gli SMS. |
| `personalEmail.address` | Indirizzo e-mail della persona. |

+++

+++Dettagli di controllo del sistema Source esterno (gruppo di campi)

External Source System Audit Attributes è un tipo di dati standard Experience Data Model (XDM) che acquisisce dettagli di audit su un sistema di origine esterno.

+++

#### Schema del connettore web Adobe

>[!NOTE]
>
>Questa è un&#39;implementazione facoltativa se si utilizza [[!DNL Adobe Analytics Source Connector]](/help/sources/connectors/adobe-applications/analytics.md).

Questo schema viene utilizzato per strutturare e fare riferimento ai dati dell’evento che costituisce l’attività del cliente che si verifica sul sito web o sulle piattaforme digitali associate. Questo schema è simile allo schema Transazioni digitali del cliente, ma differisce in quanto è destinato a essere utilizzato quando [Web SDK](/help/web-sdk/home.md) non è un&#39;opzione per la raccolta dati; pertanto, questo schema è necessario quando si utilizza [!DNL Adobe Analytics Source Connector] per inviare i dati online in [!DNL Adobe Experience Platform] come flusso di dati primario o secondario.

Lo schema del connettore Web [!DNL Adobe] è rappresentato da una classe [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md).

+++XDM ExperienceEvent (classe)

La classe [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) include i seguenti gruppi di campi:

| Campi | Descrizione |
| --- | --- |
| `_id` | Identifica in modo univoco i singoli eventi acquisiti in [!DNL Adobe Experience Platform]. |
| `timestamp` | Una marca temporale ISO 8601 indicante quando si è verificato l’evento, formattata come indicato nella sezione 5.6 della RFC 3339. Questa marca temporale deve essere nel passato. |
| `eventType` | Stringa che indica il tipo di categoria per l’evento. |

+++

Modello +++Adobe Analytics ExperienceEvent (gruppo di campi)

Il gruppo di campi [Adobe Analytics ExperienceEvent](/help/xdm/field-groups/event/analytics-full-extension.md) acquisisce le metriche comuni raccolte da Adobe Analytics.

| Campi | Descrizione |
| --- | --- |
| `endUserIDs._experience.emailid.authenticatedState` | Stato di autenticazione dell’ID dell’indirizzo e-mail dell’utente finale. |
| `endUserIDs._experience.emailid.id` | ID indirizzo e-mail utente finale. |
| `endUserIDs._experience.emailid.namespace.code` | Codice spazio dei nomi dell’indirizzo e-mail dell’utente finale. |
| `endUserIDs._experience.mcid.authenticatedState` | Stato di autenticazione dell&#39;ID Marketing Cloud (MCID) [!DNL Adobe]. Il MCID è ora noto come ID Experience Cloud (ECID). |
| `endUserIDs._experience.mcid.id` | ID Marketing Cloud [!DNL Adobe] (MCID). Il MCID è ora noto come ID Experience Cloud (ECID). |
| `endUserIDs._experience.mcid.namespace.code` | Codice spazio dei nomi ID Marketing Cloud (MCID) [!DNL Adobe]. |

+++

+++Dettagli di controllo del sistema Source esterno (gruppo di campi)

External Source System Audit Attributes è un tipo di dati standard Experience Data Model (XDM) che acquisisce dettagli di audit su un sistema di origine esterno.

+++

### Creare un set di dati da uno schema {#create-datasets}

Un set di dati è una struttura di archiviazione e gestione per un gruppo di dati. Ogni schema per scenari di ricoinvolgimento intelligente deve avere un proprio set di dati.

Per ulteriori informazioni su come creare un [set di dati](/help/catalog/datasets/overview.md) da uno schema, leggere la [Guida dell&#39;interfaccia utente dei set di dati](/help/catalog/datasets/user-guide.md).

>[!NOTE]
>
>Simile al passaggio per creare uno schema, devi abilitare il set di dati per essere incluso nel Profilo cliente in tempo reale. Per ulteriori informazioni sull&#39;abilitazione del set di dati per l&#39;utilizzo in Real-Time Customer Profile, vedere l&#39;esercitazione su [portare dati in Real-Time Customer Profile](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=it).

### Consenso e governance dei dati {#privacy-consent}

>[!IMPORTANT]
>
>Come requisito legale, è necessario dare ai clienti la possibilità di annullare l’abbonamento alla ricezione di comunicazioni da un marchio e garantire che questa scelta sia rispettata. Ulteriori informazioni sulle normative applicabili nella [Panoramica sulle normative sulla privacy](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html).

#### Criteri di consenso

Durante la creazione di un percorso di ricoinvolgimento, puoi aggiungere i seguenti [criteri di consenso](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/consent/overview.html):

* Se `consents.marketing.email.val = "Y"` allora può inviare un&#39;e-mail
* Se `consents.marketing.sms.val = "Y"` allora può inviare un SMS
* Se `consents.marketing.push.val = "Y"` allora può inviare
* Se `consents.share.val = "Y"` allora può annunciare

#### Etichettatura e applicazione della governance dei dati

Durante la creazione di un percorso di ricoinvolgimento, è consigliabile aggiungere le [etichette di governance dei dati](/help/data-governance/labels/overview.md) seguenti:

* Gli indirizzi e-mail personali vengono utilizzati come dati direttamente identificabili utilizzati per identificare o contattare una persona specifica anziché un dispositivo.
   * `personalEmail.address = I1`

#### Criteri di utilizzo dei dati

Nessun [criterio di utilizzo dati](/help/data-governance/policies/overview.md) richiesto per lo scenario di esplorazione prodotti abbandonato. Tuttavia, è necessario considerare quanto segue:

* Limita dati sensibili
* Limita Advertising in loco
* Limita targeting e-mail
* Limitare il targeting tra siti
* Limita la combinazione di dati direttamente identificabili con dati anonimi

### Creare tipi di pubblico {#create-audience}

Gli scenari di ricoinvolgimento utilizzano i tipi di pubblico per definire attributi o comportamenti specifici condivisi da un sottoinsieme di profili dall’archivio profili, al fine di distinguere un gruppo di persone commerciabile dalla base clienti. I tipi di pubblico possono essere creati in più modi in [!DNL Adobe Experience Platform].

Per ulteriori informazioni su come creare un pubblico, leggere la [guida dell&#39;interfaccia utente del servizio del pubblico](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html#create-audience).

Per ulteriori informazioni su come comporre direttamente [Tipi di pubblico](/help/segmentation/home.md), consulta la [Guida dell&#39;interfaccia utente Composizione pubblico](/help/segmentation/ui/audience-composition.md).

Per ulteriori informazioni su come creare tipi di pubblico tramite le definizioni di pubblico derivate da Platform, consulta la [guida dell&#39;interfaccia utente di Audience Builder](/help/segmentation/ui/segment-builder.md).

>[!BEGINTABS]

>[!TAB Scenario di navigazione prodotto abbandonato]

Questo pubblico viene creato come miglioramento del classico scenario &quot;Abbandono del carrello&quot;. Mentre l’abbandono del carrello in genere si concentra su un’aggiunta al carrello senza un acquisto successivo in un determinato periodo di tempo, questo pubblico cerca un impegno precedente, in particolare coloro che potrebbero aver navigato in un particolare prodotto ma non l’hanno aggiunto al carrello e non hanno avuto attività di follow-up sul sito entro un determinato intervallo di tempo. Questo pubblico aiuta a mantenere il tuo marchio &quot;top of mind&quot; per i clienti che soddisfano questi criteri di inclusione e può essere utilizzato anche per i clienti le cui proprietà digitali possono differire da un modello di e-commerce tradizionale.

+++Visualizzazione prodotto abbandonata senza coinvolgimento negli ultimi tre giorni

Il seguente evento viene utilizzato per lo scenario di navigazione del prodotto abbandonato, in cui gli utenti hanno visualizzato i prodotti online e non hanno partecipato (visite al sito, visite all’app, acquisto online, acquisto offline ed eventi di aggiunta al carrello) nei 3 giorni successivi.

Durante la configurazione del pubblico sono necessari i campi e le condizioni seguenti:

* `eventType: commerce.productViews`
* E `THEN` (evento sequenziale) escludono `eventType: commerce.productListAdds` E `application.launch` E `web.webpagedetails.pageViews` E `commerce.purchases` (inclusi sia online che offline)
   * `Timestamp: > 3 days after productView`
* `Timestamp: > 4 days`

+++

+++Visualizzazione prodotto con coinvolgimento negli ultimi tre giorni

Il seguente evento è utilizzato per lo scenario di navigazione del prodotto abbandonato, in cui gli utenti hanno visualizzato i prodotti online e hanno partecipato (visite al sito, visite all’app, acquisto online, acquisto offline ed eventi di aggiunta al carrello) nei 3 giorni successivi.

Durante la configurazione del pubblico sono necessari i campi e le condizioni seguenti:

* `eventType: commerce.productViews`
* E `THEN` (evento sequenziale) includono `eventType: commerce.productListAdds` O `application.launch` O `web.webpagedetails.pageViews` O `commerce.purchases` (questo include sia online che offline)
   * `Timestamp: > 3 days after productView`
* `Timestamp: > 4 days`
+++

+++Streaming del coinvolgimento nell’ultimo giorno

Il seguente evento viene utilizzato per lo scenario di navigazione del prodotto abbandonato in cui gli utenti si sono impegnati (visite al sito, visite all’app, acquisto online, acquisto offline ed eventi di aggiunta al carrello) nell’ultimo giorno.

Durante la configurazione del pubblico sono necessari i campi e le condizioni seguenti:

* `eventType: commerce.productListAdds OR application.launch OR web.webpagedetails.pageViews OR commerce.purchases`
   * `Timestamp: in last 1 day` (streaming)

+++

+++Batch di coinvolgimento negli ultimi tre giorni

Il seguente evento viene utilizzato per lo scenario di navigazione del prodotto abbandonato in cui gli utenti si sono impegnati (visite al sito, visite all’app, acquisto online, acquisto offline ed eventi di aggiunta al carrello) negli ultimi 3 giorni.

Durante la configurazione del pubblico sono necessari i campi e le condizioni seguenti:

* `EventType: commerce.productListAdds OR application.launch OR web.webpagedetails.pageViews OR commerce.purchases`
   * `Timestamp: in last 3 days` (batch)

+++

>[!TAB Scenario carrello abbandonato]

Questo pubblico viene creato per supportare lo scenario classico &quot;Abbandono del carrello&quot;. Il suo scopo è quello di trovare i clienti che hanno aggiunto un prodotto al carrello ma alla fine non hanno effettuato un acquisto. Questo tipo di pubblico contribuirà a mantenere non solo il tuo marchio &quot;top of mind&quot; per i tuoi clienti, ma anche i prodotti che hanno lasciato senza un acquisto successivo.

I seguenti eventi vengono utilizzati per lo scenario del carrello abbandonato in cui gli utenti hanno aggiunto un prodotto al carrello tra 1 e 4 giorni fa, ma non hanno completato l’acquisto o cancellato il carrello.

Durante la configurazione del pubblico sono necessari i campi e le condizioni seguenti:

* `eventType: commerce.productListAdds`
   * `Timestamp: >= 1 days before now AND <= 4 days before now `
* `eventType: commerce.purchases`
   * `Timestamp: <= 4 days before now`
* `eventType: commerce.productListRemovals`
   * `Timestamp: <= 4 days before now`

Il descrittore dello scenario del carrello abbandonato viene visualizzato come segue:

`Include eventType = commerce.productListAdds between 30 min and 1440 minutes before now. exclude eventType = commerce.purchases 30 minutes before now OR eventType = commerce.productListRemovals AND Cart ID equals Product List Adds1 Cart ID (the inclusion event).`

>[!TAB Scenario di conferma ordine]

Questo percorso non richiede la creazione di tipi di pubblico.

>[!ENDTABS]

### Configurazione del percorso in Adobe Journey Optimizer {#journey-setup}

>[!NOTE]
>
>[!DNL Adobe Journey Optimizer] non include tutti gli elementi visualizzati nei diagrammi. Tutti i [annunci multimediali a pagamento](/help/destinations/catalog/social/overview.md) sono creati in [!UICONTROL Destinazioni].

[[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html) ti aiuta a fornire ai tuoi clienti esperienze connesse, contestuali e personalizzate. Il percorso del cliente è l’intero processo di interazione del cliente con il marchio. Ogni percorso di casi d’uso richiede informazioni specifiche. Di seguito sono elencati i dati precisi necessari per ciascun percorso.

>[!BEGINTABS]

>[!TAB Scenario di navigazione prodotto abbandonato]

Lo scenario di navigazione dei prodotti abbandonati è incentrato sulla navigazione dei prodotti abbandonati sia sul sito web che sull’app mobile.<p>![Panoramica visiva di alto livello dello scenario di ricerca prodotti abbandonato dal cliente.](../intelligent-re-engagement/images/re-engagement-journey.png "Panoramica visiva di alto livello dello scenario di ricerca prodotti abbandonato dal cliente."){width="1920" zoomable="yes"}</p>

+++Eventi

Gli eventi consentono di attivare i percorsi in modo unitario per inviare messaggi in tempo reale all’utente che entra nel percorso. Per ulteriori informazioni sugli eventi, leggere la [guida generale agli eventi](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events.html).

* Evento 1: Visualizzazioni prodotto
   * Schema: Transazioni digitali del cliente
   * Campi:
      * `eventType`
   * Condizione:
      * `eventType = commerce.productViews`
      * Campi:
         * `eventType`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

* Evento 2: aggiungi al carrello
   * Schema: Transazioni digitali del cliente
   * Campi:
      * `eventType`
   * Condizione:
      * `eventType = commerce.productListAdds`
      * Campi:
         * `commerce.productListAdds.id`
         * `commerce.productListAdds.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `commerce.cart.cartID`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

* Evento 3: Brand Engagement
   * Schema: Transazioni digitali del cliente
   * Campi:
      * `eventType`
   * Condizione:
      * `eventType in application.launch, commerce.purchases, web.webpagedetails.pageViews`
      * Campi:
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `web.webpagedetails.URL`
         * `web.webpagedetails.isHomePage`
         * `web.webpagedetails.name`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`
         * `commerce.purchases.id`
         * `commerce.purchases.value`
         * `shipping.address.city`
         * `shipping.address.countryCode`
         * `shipping.address.postalCode`
         * `shipping.address.state`
         * `shipping.address.street1`
         * `shipping.address.street2`
         * `shipping.shipDate`
         * `shipping.trackingNumber`
         * `shipping.trackingURL`

+++

+++Logica chiave area di lavoro Percorso

La logica chiave dell’area di lavoro di percorso richiede di identificare eventi specifici e configurare le azioni da eseguire dopo che l’evento si è verificato.

* Logica di ingresso percorso
   * Evento visualizzazione prodotto

* Condizioni
   * Verifica la presenza di almeno un evento di acquisto online o offline dall’ultima visualizzazione del prodotto.
      * Schema: Transazioni digitali del cliente
      * `eventType = commerce.purchases`
      * `timestamp > timestamp of product last viewed`

   * Verifica la presenza di almeno un acquisto offline dall’ultima visualizzazione del prodotto:
      * Schema: Transazioni non in linea cliente
      * `eventType = commerce.purchases`
      * `timestamp > timestamp of product last viewed`

   * Condizioni: seleziona il canale di destinazione
      * E-mail
         * `consents.marketing.email.val = y`
      * Push
         * `consents.marketing.push.val=y`
      * SMS
         * `consents.marketing.sms.val = y`

   * Channel Personalization
      * Contenuto del canale personalizzato in base alla visualizzazione del prodotto.

+++

>[!TAB Scenario carrello abbandonato]

Lo scenario del carrello abbandonato riguarda i prodotti che sono stati inseriti nel carrello ma che non sono ancora stati acquistati sia sul sito web che sull’app mobile.<p>![Panoramica visiva di alto livello dello scenario del carrello abbandonato dal cliente.](../intelligent-re-engagement/images/abandoned-cart-journey.png "Panoramica visiva di alto livello dello scenario del carrello abbandonato dal cliente."){width="1920" zoomable="yes"}</p>

+++Eventi

Gli eventi consentono di attivare i percorsi in modo unitario per inviare messaggi in tempo reale all’utente che entra nel percorso. Per ulteriori informazioni sugli eventi, leggere la [guida generale agli eventi](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events.html).

* Evento 2: aggiungi al carrello
   * Schema: Transazioni digitali del cliente
   * Campi:
      * `eventType`
   * Condizione:
      * `eventType = commerce.productListAdds`
      * Campi:
         * `commerce.productListAdds.id`
         * `commerce.productListAdds.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `commerce.cart.cartID`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

* Evento 4: Acquisti online
   * Schema: Transazioni digitali del cliente
   * Campi:
      * `eventType`
   * Condizione:
      * `eventType = commerce.purchases`
      * Campi:
         * `commerce.purchases.id`
         * `commerce.purchases.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

* Evento 3: Brand Engagement
   * Schema: Transazioni digitali del cliente
   * Campi:
      * `eventType`
   * Condizione:
      * `eventType in application.launch, commerce.purchases, web.webpagedetails.pageViews`
      * Campi:
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `web.webpagedetails.URL`
         * `web.webpagedetails.isHomePage`
         * `web.webpagedetails.name`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`
         * `commerce.purchases.id`
         * `commerce.purchases.value`
         * `shipping.address.city`
         * `shipping.address.countryCode`
         * `shipping.address.postalCode`
         * `shipping.address.state`
         * `shipping.address.street1`
         * `shipping.address.street2`
         * `shipping.shipDate`
         * `shipping.trackingNumber`
         * `shipping.trackingURL`

+++

+++Logica chiave area di lavoro Percorso

La logica chiave dell’area di lavoro di percorso richiede di identificare eventi specifici e configurare le azioni da eseguire dopo che l’evento si è verificato.

* Logica di ingresso percorso
   * Evento `AddToCart`

* AuthenticatedState in Authenticated

* Condizione: acquisti offline dall’ultimo abbandono del carrello:
   * Schema: Transazioni non in linea cliente
   * `eventType = commerce.purchases`
   * `timestamp > timestamp of cart was last abandoned`

* Condizione: il carrello è stato cancellato dall’ultimo abbandono del carrello:
   * Schema: Transazioni digitali del cliente
   * `eventType = commerce.cartCleared`
   * `cartID` (ID del carrello)
   * `timestamp > timestamp of cart was last abandoned`

* Seleziona canale di destinazione (seleziona uno o più canali per una portata più ampia)
   * E-mail
      * `consents.marketing.email.val = y`
   * Push
      * `consents.marketing.push.val = y`
   * SMS
      * `consents.marketing.sms.val = y`
   * Channel Personalization
      * Visualizza informazioni dettagliate sul carrello e può visualizzare più prodotti in un formato tabella.

+++

>[!TAB Scenario di conferma ordine]

Lo scenario di conferma dell’ordine si concentra sugli acquisti di prodotti effettuati tramite il sito web e l’app mobile.<p>![Panoramica visiva di alto livello dello scenario di conferma dell&#39;ordine cliente.](../intelligent-re-engagement/images/order-confirmation-journey.png "Panoramica visiva di alto livello dello scenario di conferma dell&#39;ordine cliente."){width="1920" zoomable="yes"}</p>

+++Eventi

Gli eventi consentono di attivare i percorsi in modo unitario per inviare messaggi in tempo reale all’utente che entra nel percorso. Per ulteriori informazioni sugli eventi, leggere la [guida generale agli eventi](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events.html).

* Evento 4: Acquisti online
   * Schema: Transazioni digitali del cliente
   * Campi:
      * `eventType`
   * Condizione:
      * `eventType = commerce.purchases`
      * Campi:
         * `commerce.purchases.id`
         * `commerce.purchases.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

+++

+++Logica chiave area di lavoro Percorso

La logica chiave dell’area di lavoro di percorso richiede di identificare eventi specifici e configurare le azioni da eseguire dopo che l’evento si è verificato.

* Logica di ingresso percorso
   * Evento ordine

* Condizioni
   * Seleziona Canale di destinazione (seleziona uno o più canali per una portata più ampia).
      * La conferma dell’ordine è considerata utile in natura, pertanto il controllo del consenso è solitamente superfluo.
      * E-mail
      * Push
      * SMS

   * Personalization contenuto canale
      * Visualizza le informazioni sui dettagli dell’ordine e può visualizzare un elenco di prodotti utilizzando un formato tabella.

+++

>[!ENDTABS]

Per ulteriori informazioni sulla creazione di percorsi in [!DNL Adobe Journey Optimizer], leggere la [Guida introduttiva ai percorsi](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html).

### Impostazione di annunci multimediali a pagamento nelle destinazioni {#paid-media-ads}

Il framework delle destinazioni viene utilizzato per gli annunci multimediali a pagamento. Una volta verificato il consenso, questo viene inviato alle varie destinazioni configurate. Per ulteriori informazioni sulle destinazioni, leggere il documento [Panoramica sulle destinazioni](/help/destinations/home.md).

#### Dati richiesti per le destinazioni

Le destinazioni di esportazione del pubblico in streaming (come Facebook, Google Customer Match, Google DV360) supportano varie identità dai dati dei clienti:

* `personalEmail.address`
* `ECID`
* `mobilePhone.number`

Puoi attivare la navigazione nei prodotti abbandonati e abbandonare il pubblico del carrello per gli annunci multimediali a pagamento.

* Streaming/Triggered
   * [Advertising](/help/destinations/catalog/advertising/overview.md)/[File multimediali a pagamento e social](/help/destinations/catalog/social/overview.md)
   * [Dispositivi mobili](/help/destinations/catalog/mobile-engagement/overview.md)
   * [Destinazione streaming](/help/destinations/catalog/streaming/http-destination.md)
   * [Destinazione personalizzata creata con Destination SDK.](/help/destinations/destination-sdk/overview.md). Se sei un cliente di Real-Time CDP Ultimate, puoi anche creare una [destinazione personalizzata privata utilizzando Destination SDK](/help/destinations/destination-sdk/overview.md#productized-and-custom-integrations)

## Passaggi successivi {#next-steps}

Coinvolgendo nuovamente i clienti che hanno abbandonato una conversione in modo intelligente e responsabile, si spera di aver aumentato le conversioni e il valore del ciclo di vita del cliente.

Successivamente, puoi esplorare altri casi d&#39;uso supportati da Real-Time CDP, ad esempio [visualizzazione di contenuto personalizzato a utenti non autenticati](/help/rtcdp/partner-data/onsite-personalization.md) nelle proprietà Web.
