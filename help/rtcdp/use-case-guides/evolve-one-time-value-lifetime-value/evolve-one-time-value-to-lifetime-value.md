---
title: Valorizzazione del cliente una tantum in base al valore del ciclo di vita
description: Scopri come creare campagne personalizzate per offrire i migliori prodotti o servizi complementari in base agli attributi, al comportamento e agli acquisti precedenti di un cliente specifico.
feature: Use Cases
exl-id: 45f72b5e-a63b-44ac-a186-28bac9cdd442
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '3179'
ht-degree: 2%

---

# Valorizzazione del cliente una tantum in base al valore del ciclo di vita

>[!IMPORTANT]
> 
>* Questa pagina presenta un esempio di implementazione di Real-Time CDP e Adobe Journey Optimizer per ottenere il caso d’uso descritto. Utilizza le figure, i criteri di qualificazione e altri campi forniti nella pagina come guida, non come cifre prescrittive.
>* Per completare questo caso d’uso, devi disporre della licenza per Real-Time CDP e Adobe Journey Optimizer. Ulteriori informazioni sono disponibili nella sezione [prerequisiti e pianificazione](#prerequisites-and-planning) più avanti.

Implementa il caso d’uso &quot;one-time customer value to lifetime value&quot; per promuovere il brand engagement e la brand loyalty. Crea un&#39;esperienza cliente connessa su più canali o percorsi utilizzando la potenza di Experience Platform, potenziata da [Real-Time CDP](/help/rtcdp/home.md) e [Journey Optimizer](https://experienceleague.adobe.com/it/docs/journey-optimizer/using/ajo-home).

Gli utenti tipo a cui stai eseguendo il targeting sono i visitatori non frequenti delle tue proprietà che hanno effettuato alcuni acquisti negli ultimi tre mesi.

Considera questi clienti che visitano le tue proprietà e acquistano occasionalmente i prodotti o i servizi che offri. Potresti creare campagne personalizzate che attraggano questi clienti in modo che il tuo marchio possa offrire loro un valore a lungo termine invece di un valore unico. Scopri come:

* Raccolta e gestione dei dati
* Creare tipi di pubblico
* Crea percorsi per indirizzare questi tipi di pubblico in Adobe Journey Optimizer e attivarli in Real-Time CDP.

![Panoramica visiva di alto livello dell&#39;evoluzione del valore una tantum in valore del ciclo di vita.](../evolve-one-time-value-lifetime-value/images/diagram-business-use-case.png){zoomable="yes"}

## Prerequisiti e pianificazione {#prerequisites-and-planning}

Considerando che internamente hai definito un obiettivo e un obiettivo di business per aumentare la brand loyalty. Questo può tradursi nell’esecuzione di un caso d’uso per stimolare il coinvolgimento e la fedeltà dei clienti.

Per ottenere questo risultato, la tecnologia necessaria è costituita dalle due app di Experience Platform [Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=it) e [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=it). Di seguito sono elencati vari elementi di funzionalità e interfaccia utente delle due app che utilizzerai durante l’implementazione del caso d’uso.

>[!TIP]
>
>Assicurati di disporre delle [autorizzazioni di controllo degli accessi basate su attributi](/help/access-control/abac/end-to-end-guide.md) per tutte queste aree o richiedi all’amministratore di sistema di concedere le autorizzazioni necessarie.

* [[!DNL Adobe Real-Time Customer Data Platform (Real-Time CDP)]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html): integra i dati tra le origini dati per alimentare la campagna. Questi dati vengono quindi utilizzati per creare i tipi di pubblico della campagna e far emergere elementi di dati personalizzati utilizzati nell’e-mail e nelle tessere delle promozioni web (ad esempio, nome o informazioni relative all’account). Infine, Real-Time CDP viene utilizzato anche per attivare i tipi di pubblico su destinazioni di media a pagamento.
   * [Schemi](/help/xdm/home.md)
   * [Profili](/help/profile/home.md)
   * [Set di dati](/help/catalog/datasets/overview.md)
   * [Tipi di pubblico](/help/segmentation/home.md)
   * [Destinazioni](/help/destinations/home.md)
* [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html): progetta i percorsi, configura i trigger e crea i messaggi giusti per indirizzare i visitatori.
   * [Attivatore evento o pubblico](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/collect-event-data/data-collection.html)
   * [Tipi di pubblico ed eventi](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/about-audiences.html?lang=it)
   * [Percorsi](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)

## Architettura Real-Time CDP e Journey Optimizer

Di seguito è riportata una panoramica dell’architettura di alto livello dei vari componenti di Real-Time CDP e Journey Optimizer. Questo diagramma mostra il modo in cui i dati fluiscono attraverso le due app di Experience Platform, dalla raccolta dati al punto in cui vengono attivati tramite percorsi o campagne verso le destinazioni, per ottenere il caso d’uso descritto in questa pagina.

![Panoramica visiva di alto livello dell&#39;architettura.](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/architecture-diagram.png){zoomable="yes"}

## Come utilizzare il caso d’uso: panoramica di alto livello {#achieve-the-use-case-high-level}

Di seguito è riportata una panoramica generale del flusso di lavoro, una combinazione di un flusso di lavoro di percorso e un flusso di lavoro di attivazione.

Nel flusso di lavoro di esempio illustrato di seguito, puoi cercare i clienti che soddisfano determinati criteri e vuoi invitarli a tornare al sito web o all’app. Stai cercando di impostarli su un percorso in cui, invece di un’attività limitata sulla proprietà, restituiscano in modo più ricorrente. Stai tentando di riportarli nella tua proprietà e una volta tornati, puoi farli entrare nel percorso per effettuare acquisti ricorrenti sul tuo sito. La campagna configurata qui è limitata a un coinvolgimento con i clienti al mese.

Inizia inviando un messaggio al tuo pubblico di clienti di alto valore e a bassa frequenza. Controlla quindi se hanno ricevuto questo messaggio negli ultimi trenta giorni. In caso contrario, puoi inserirli in un percorso riguardante, ad esempio, un nuovo programma di abbonamento. Potrai quindi attendere alcuni giorni (sette giorni in questo esempio). Trascorso questo periodo, se non hanno acquistato l’abbonamento di cui hai ricevuto il messaggio, puoi inviare annunci multimediali a pagamento tramite destinazioni. Se l’abbonamento è stato acquistato, puoi richiedere l’inserimento di un percorso di conferma dell’ordine, completando in tal modo il caso d’uso.

>[!IMPORTANT]
>
>Come descritto più avanti in questa pagina, con un [gruppo di campi di consenso dedicato nello schema](#customer-attributes-schema) e con [l&#39;implementazione dei criteri di consenso](#privacy-consent), tutte le azioni e i flussi di lavoro vengono implementati in modo da garantire la privacy e il consenso.

>[!BEGINSHADEBOX]

![Panoramica visiva di alto livello dell&#39;evoluzione del valore una tantum in valore del ciclo di vita.](../evolve-one-time-value-lifetime-value/images/step-by-step.png){zoomable="yes"}

1. Puoi creare schemi e set di dati, quindi contrassegnarli per [!UICONTROL Profilo].
2. I dati vengono raccolti e integrati in Experience Platform tramite Web SDK, Mobile Edge SDK o API. È possibile utilizzare anche il connettore dati di Analytics, ma potrebbe causare latenza del percorso.
3. Carichi i profili in Real-Time CDP e definisci criteri di governance per assicurarne l’utilizzo responsabile.
4. Puoi creare tipi di pubblico mirati dall’elenco dei profili per verificare la presenza di clienti con valori elevati e bassa frequenza.
5. Si creano due percorsi in [!DNL Adobe Journey Optimizer], uno per segnalare agli utenti un nuovo programma di abbonamento e un altro per inviare loro un messaggio di conferma dell&#39;acquisto in un secondo momento.
6. Se lo desideri, puoi attivare il pubblico di clienti che non hanno acquistato l’abbonamento per le destinazioni desiderate dei contenuti multimediali a pagamento.

>[!ENDSHADEBOX]

## Come ottenere il caso d’uso {#achieve-use-case-instruction}

Per completare ciascuno dei passaggi della panoramica di alto livello precedente, leggere le sezioni seguenti, che offrono collegamenti a ulteriori informazioni e istruzioni più dettagliate.

### Funzionalità ed elementi dell’interfaccia utente che utilizzerai {#ui-functionality-and-elements}

Dopo aver completato i passaggi per implementare il caso d’uso, utilizzerai gli elementi Real-Time CDP, la funzionalità Adobe Journey Optimizer e l’interfaccia utente elencati all’inizio del presente documento. Verificare di disporre delle autorizzazioni di controllo dell&#39;accesso basate su attributi necessarie per tutte queste aree o richiedere all&#39;amministratore di sistema di concedere le autorizzazioni necessarie.

### Creare una struttura di schema e specificare i gruppi di campi {#schema-design}

Le risorse Experience Data Model (XDM) sono gestite nell&#39;area di lavoro [!UICONTROL Schemi] in [!DNL Adobe Experience Platform]. Puoi visualizzare ed esplorare le risorse di base fornite da [!DNL Adobe] (ad esempio, [!UICONTROL gruppi di campi]) e creare risorse e schemi personalizzati per la tua organizzazione.

Per ulteriori informazioni sulla creazione di [schemi](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=it), leggere l&#39;esercitazione [crea schema.](/help/xdm/tutorials/create-schema-ui.md)

In questa implementazione di esempio puoi utilizzare diversi schemi per il caso d’uso al fine di convertire il valore una tantum in valore del ciclo di vita. Ogni schema include campi obbligatori specifici da impostare e alcuni campi suggeriti.

In base a implementazioni di esempio, Adobe consiglia di creare i tre schemi seguenti per eseguire questo caso d’uso:

* [Schema degli attributi del cliente](#customer-attributes-schema) (uno schema di profilo)
* [Schema transazioni digitali cliente](#customer-digital-transactions-schema) (schema evento esperienza)
* [Schema transazioni cliente offline](#customer-offline-transactions-schema) (schema evento esperienza)

#### Schema attributi cliente {#customer-attributes-schema}

Utilizza questo schema per strutturare e fare riferimento ai dati di profilo che compongono le informazioni sul cliente. Questi dati vengono generalmente acquisiti in [!DNL Adobe Experience Platform] tramite il sistema CRM o simile e sono necessari per fare riferimento ai dettagli dei clienti utilizzati per la personalizzazione, il consenso al marketing e le funzionalità di segmentazione avanzate.

![Schema attributi cliente con gruppi di campi evidenziati](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/customer-attributes-schema.png)

Lo schema di attributi del cliente è rappresentato da una classe [!UICONTROL XDM Individual Profile], che include i seguenti gruppi di campi:

+++Dettagli demografici (gruppo di campi)

[Dettagli demografici](/help/xdm/field-groups/profile/demographic-details.md) è un gruppo di campi di schema standard per la classe Profilo individuale XDM. Il gruppo di campi fornisce un oggetto persona a livello principale, i cui sottocampi descrivono informazioni su una singola persona.

+++

+++Dati di contatto personali (gruppo di campi)

[Dettagli contatto personale](/help/xdm/field-groups/profile/personal-contact-details.md) è un gruppo di campi di schema standard per la classe Profilo individuale XDM, che descrive le informazioni di contatto per una singola persona.

+++

+++Dettagli di controllo del sistema Source esterno (gruppo di campi)

[External Source System Audit Attributes](/help/xdm/data-types/external-source-system-audit-attributes.md) è un tipo di dati XDM (Experience Data Model) standard che acquisisce i dettagli di controllo di un sistema di origine esterno.

+++

+++Gruppi di campi di consenso e preferenze (gruppo di campi)

[Il gruppo di campi Consensi e preferenze](/help/xdm/field-groups/profile/consents.md) fornisce un singolo campo di tipo oggetto, Consensi, per acquisire informazioni sul consenso e sulle preferenze.

+++

#### Schema transazioni digitali cliente {#customer-digital-transactions-schema}

Questo schema viene utilizzato per strutturare e fare riferimento ai dati dell’evento che costituisce l’attività del cliente che si verifica sul sito web o su altre piattaforme digitali associate. Questi dati vengono generalmente acquisiti in [!DNL Adobe Experience Platform] tramite [Web SDK](/help/web-sdk/home.md) e sono necessari per fare riferimento ai vari eventi di navigazione e conversione utilizzati per l&#39;attivazione di percorsi, per l&#39;analisi dettagliata dei clienti online e per funzionalità di segmentazione avanzate.

![Schema transazioni digitali cliente con gruppi di campi evidenziati](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/customer-digital-transactions-schema.png)

Lo schema delle transazioni digitali del cliente è rappresentato da una classe [!UICONTROL XDM ExperienceEvent], che include i seguenti gruppi di campi:

+++Adobe Experience Platform Web SDK ExperienceEvent (gruppo di campi)

| Campi | Requisito |
| --- | --- |
| `device.model` | Consigliato |
| `environment.browserDetails.userAgent` | Consigliato |

+++

+++Dettagli Web (gruppo di campi)

[Dettagli Web](/help/xdm/field-groups/event/web-details.md) è un gruppo di campi di schema standard per la classe XDM ExperienceEvent, utilizzato per descrivere informazioni relative a eventi di dettagli Web come interazione, dettagli di pagina e referrer.

+++

+++Evento esperienza del consumatore (gruppo di campi)

Questo gruppo di campi include varie informazioni sulle azioni, ad esempio eventi di acquisto o di navigazione, eseguite dagli utenti sulla proprietà Web.

| Campo | Requisito |
| --- | --- |
| `commerce.cart.cartID` | Consigliato |
| `commerce.cart.cartSource` | Consigliato |
| `commerce.cartAbandons.id` | Consigliato |
| `commerce.cartAbandons.value` | Consigliato |
| `commerce.order.orderType` | Consigliato |
| `commerce.order.payments.paymentAmount` | Consigliato |
| `commerce.order.payments.paymentType` | Consigliato |
| `commerce.order.payments.transactionID` | Consigliato |
| `commerce.order.priceTotal` | Consigliato |
| `commerce.order.purchaseID` | Consigliato |
| `commerce.productListAdds.id` | Consigliato |
| `commerce.productListAdds.value` | Consigliato |
| `commerce.productListOpens.id` | Consigliato |
| `commerce.productListOpens.value` | Consigliato |
| `commerce.productListRemoval.id` | Consigliato |
| `commerce.productListRemoval.value` | Consigliato |
| `commerce.productListViews.id` | Consigliato |
| `commerce.productListViews.value` | Consigliato |
| `commerce.productViews.id` | Consigliato |
| `commerce.productViews.value` | Consigliato |
| `commerce.purchases.id` | Consigliato |
| `commerce.purchases.value` | Consigliato |
| `marketing.campaignGroup` | Consigliato |
| `marketing.campaignName` | Consigliato |
| `marketing.trackingCode` | Consigliato |
| `productListItems.name` | Consigliato |
| `productListItems.priceTotal` | Consigliato |
| `productListItems.product` | Consigliato |
| `productListItems.quantity` | Consigliato |

+++

+++Dettagli ID utente finale (gruppo di campi)

Il gruppo di campi [Dettagli ID utente finale](/help/xdm/field-groups/event/enduserids.md) include varie informazioni sugli utenti, ad esempio se sono autenticati sul sito durante la visita e informazioni sulla loro identità.

+++

+++Dettagli di controllo del sistema Source esterno (gruppo di campi)

External Source System Audit Attributes è un tipo di dati standard Experience Data Model (XDM) che acquisisce dettagli di audit su un sistema di origine esterno.

+++

#### Schema transazioni cliente offline {#customer-offline-transactions-schema}

Questo schema viene utilizzato per strutturare e fare riferimento ai dati dell’evento che costituisce l’attività del cliente che si verifica su piattaforme al di fuori del sito web. Questi dati vengono generalmente acquisiti in [!DNL Adobe Experience Platform] da un POS (o sistema simile) e il più delle volte inviati in streaming a Platform tramite una connessione API. Leggi informazioni sull&#39;[acquisizione batch](/help/ingestion/batch-ingestion/getting-started.md). Il suo scopo è quello di fare riferimento ai vari eventi di conversione offline utilizzati per attivare percorsi, analisi approfondite dei clienti online e offline e funzionalità di segmentazione avanzate.

![Schema transazioni cliente offline con gruppi di campi evidenziati](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/customer-offline-transactions-schema.png)

Lo schema di transazioni cliente offline è rappresentato da una classe [!UICONTROL XDM ExperienceEvent], che include i seguenti gruppi di campi:

+++Dettagli Commerce (gruppo di campi)

[Dettagli Commerce](/help/xdm/field-groups/event/commerce-details.md) è un gruppo di campi di schema standard per la classe [!DNL XDM ExperienceEvent], utilizzato per descrivere dati commerciali quali informazioni sul prodotto (SKU, nome, quantità) e operazioni standard del carrello (ordine, pagamento, abbandono).

+++

+++Dati di contatto personali (gruppo di campi)

[[!UICONTROL Dettagli contatto personale]](/help/xdm/field-groups/profile/personal-contact-details.md) è un gruppo di campi dello schema standard per la classe [!DNL XDM Individual Profile], che descrive le informazioni di contatto per una singola persona.

+++

+++Dettagli di controllo del sistema Source esterno (gruppo di campi)

External Source System Audit Attributes è un tipo di dati standard Experience Data Model (XDM) che acquisisce dettagli di audit su un sistema di origine esterno.

+++

#### Schema del connettore web Adobe {#adobe-web-connector-schema}

>[!NOTE]
>
>Questa è un&#39;implementazione facoltativa se si utilizza [!DNL Adobe Analytics Data Connector].

Questo schema viene utilizzato per strutturare e fare riferimento ai dati dell’evento che costituisce l’attività del cliente che si verifica sul sito web o su altre piattaforme digitali associate. Questo schema è simile allo schema Customer Digital Transactions ma differisce in quanto può essere utilizzato quando Web SDK non è un’opzione per la raccolta di dati. È quindi possibile utilizzare questo schema quando si utilizza [!DNL Adobe Analytics Data Connector] per inviare i dati online a [!DNL Adobe Experience Platform] come flusso di dati primario o secondario.

![Adobe schema connettore Web con gruppi di campi evidenziati](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/adobe-web-schema.png)

Lo schema del connettore Web [!DNL Adobe] è rappresentato da una classe [!UICONTROL XDM ExperienceEvent], che include i seguenti gruppi di campi:

Modello +++Adobe Analytics ExperienceEvent (gruppo di campi)

[[!UICONTROL Estensione completa Adobe Analytics ExperienceEvent]](/help/xdm/field-groups/event/analytics-full-extension.md) è un gruppo di campi di schema standard che acquisisce metriche comuni raccolte da Adobe Analytics.

+++

### Creare un set di dati da uno schema {#dataset-from-schema}

Un set di dati è una struttura di archiviazione e gestione per un gruppo di dati. Ogni schema utilizzato per eseguire questa implementazione di esempio ha un singolo set di dati.

Per ulteriori informazioni su come creare un [set di dati](/help/catalog/datasets/overview.md) da uno schema, leggere la [Guida dell&#39;interfaccia utente dei set di dati](/help/catalog/datasets/user-guide.md).

>[!NOTE]
>
>Simile al passaggio per creare uno schema, devi abilitare il set di dati per essere incluso nel Profilo cliente in tempo reale. Per ulteriori informazioni sull&#39;abilitazione del set di dati per l&#39;utilizzo in Real-Time Customer Profile, leggere l&#39;esercitazione [create schema.](/help/xdm/tutorials/create-schema-ui.md#profile).

### Privacy, consenso e governance dei dati {#privacy-consent}

#### Criteri di consenso

>[!IMPORTANT]
>
>Come requisito legale, è necessario dare ai clienti la possibilità di annullare l’abbonamento alla ricezione di comunicazioni da un marchio e garantire che questa scelta sia rispettata. Ulteriori informazioni sulle normative applicabili nella [Panoramica sulle normative sulla privacy](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html).

Prendi in considerazione l&#39;implementazione dei seguenti [criteri di consenso](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/consent/overview.html) e la richiesta del consenso ai visitatori prima di contattarli:

* Se `consents.marketing.email.val = "Y"` allora può inviare un&#39;e-mail
* Se `consents.marketing.sms.val = "Y"` allora può inviare un SMS
* Se `consents.marketing.push.val = "Y"` allora può inviare
* Se `consents.share.val = "Y"` allora può annunciare

#### Etichetta e applicazione della governance dei dati

Valuta di aggiungere e applicare le [etichette di governance dei dati](/help/data-governance/labels/overview.md) seguenti:

* Gli indirizzi e-mail personali vengono utilizzati come dati direttamente identificabili utilizzati per identificare o contattare una persona specifica anziché un dispositivo.
   * `personalEmail.address = I1`

#### Politiche di marketing

Nessun [criterio di marketing](/help/data-governance/policies/overview.md) richiesto per i percorsi creati nell&#39;ambito di questo caso d&#39;uso. Tuttavia, puoi considerare i seguenti criteri come desiderato:

* Limita dati sensibili
* Limita Advertising in loco
* Limita targeting e-mail
* Limitare il targeting tra siti
* Limita la combinazione di dati direttamente identificabili con dati anonimi

### Creare tipi di pubblico {#create-audiences}

Questo caso d’uso richiede la creazione di due tipi di pubblico per definire attributi o comportamenti specifici condivisi da un sottoinsieme di profili dall’archivio profili, al fine di distinguere un gruppo di persone commerciabile. In Adobe Experience Platform è possibile creare i tipi di pubblico in diversi modi:

* Per informazioni su come creare un pubblico, consulta la [Guida dell&#39;interfaccia utente di Audience Service](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html#create-audience).
* Per informazioni su come comporre [tipi di pubblico](/help/segmentation/home.md), consulta la [guida dell&#39;interfaccia utente per la composizione del pubblico](/help/segmentation/ui/audience-composition.md).
* Per informazioni su come creare tipi di pubblico tramite le definizioni dei segmenti derivate da Platform, consulta la [guida dell&#39;interfaccia utente di Audience Builder](/help/segmentation/ui/segment-builder.md).

In particolare, devi creare e utilizzare due tipi di pubblico in diversi passaggi del caso d’uso, come illustrato nell’immagine seguente.

![Tipi di pubblico evidenziati.](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/audiences-highlighted-in-diagram.png){zoomable="yes"}

>[!BEGINTABS]

>[!TAB Pubblico idoneo per Adobe Journey Optimizer]

Questo pubblico di alto valore e a bassa frequenza include i profili a cui desideri raggiungere tramite un percorso, per far conoscere loro un nuovo programma di abbonamento. Di seguito sono riportati i dettagli dei tipi di pubblico:

* Descrizione: profili che hanno speso più di $ 250 in aggregato negli ultimi 3 mesi
* Campi e condizioni necessari nel pubblico:
   * Evento: `commerce.order.payments.paymentamount`
* Somma aggregata: >= $250
   * Tipo evento: `commerce.purchases`
* Timestamp: meno di 3 mesi prima di ora


>[!TAB Pubblico multimediale a pagamento]

Questo pubblico viene creato per includere i profili che hanno speso complessivamente più di 250 $ negli ultimi 3 mesi e che non hanno effettuato un acquisto negli ultimi 7 giorni. Di seguito sono riportati i dettagli dei tipi di pubblico:

* Descrizione: profili che hanno speso complessivamente più di 250 $ negli ultimi 3 mesi e che non hanno effettuato un acquisto negli ultimi 7 giorni.
* Campi e condizioni necessari:
   * Tipo evento: `journey.feedback`
      * Operando: = true
   * Evento: `experience.journeyOrchestration.stepEvents.nodeName`
      * Operando: = JourneyStepEventTracker - Abbonamento non acquistato
      * Timestamp: negli ultimi 7 giorni
   * EventType non: `commerce.purchases`
      * Timestamp: &lt;= 7 giorni prima di ora
   * Evento: SKU
      * Valore: = `subscription`

>[!ENDTABS]

### Configurazione del percorso in Adobe Journey Optimizer {#journey-setup}

>[!NOTE]
>
>[!DNL Adobe Journey Optimizer] non include tutti gli elementi visualizzati nei diagrammi. Tutti gli [annunci multimediali a pagamento](/help/destinations/catalog/social/overview.md) sono creati nelle [!UICONTROL destinazioni] [area di lavoro](/help/destinations/ui/destinations-workspace.md).

[[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html) ti aiuta a fornire ai tuoi clienti esperienze connesse, contestuali e personalizzate. Il percorso del cliente è l’intero processo di interazione del cliente con il marchio. Ogni percorso di casi d’uso richiede informazioni specifiche.

Per eseguire questo caso d’uso, è necessario creare due percorsi separati:

* Il percorso del ciclo di vita, che include il messaggio inviato ai clienti a valore elevato e bassa frequenza
* Il percorso di conferma dell’ordine per gli utenti che rispondono alla chiamata e acquistano un abbonamento.

![Percorsi evidenziati.](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/journeys-highlighted-in-diagram.png){zoomable="yes"}

Di seguito sono elencati i dati precisi necessari per ogni ramo del Percorso.

>[!BEGINTABS]

>[!TAB Percorso durata]

Il percorso &quot;lifetime&quot; si rivolge al pubblico di clienti di alto valore e a bassa frequenza che non sono stati presi di mira negli ultimi 30 giorni. Viene visualizzato un messaggio a questi clienti e quindi, se dopo 7 giorni non effettuano ancora l’acquisto, puoi includere i non acquirenti in un pubblico a cui puoi mostrare annunci multimediali a pagamento. Se acquistano, puoi impostare gli acquirenti su un percorso di conferma dell’ordine, descritto nella scheda separata.

![Panoramica visiva di alto livello del percorso a vita.](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/lifetime-journey.png "Panoramica visiva di alto livello del percorso con valore una tantum per l&#39;intero ciclo di vita."){zoomable="yes"}

+++Logica di Percorso dettagliata

Il percorso mostrato sopra segue la logica seguente.

1. Read audience: utilizza un&#39;[attività Read audience](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience.html?lang=en) per il primo pubblico creato nella sezione dei tipi di pubblico precedente.

2. Condizione - Canale preferito: utilizza un’[attività condizione](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity.html) per determinare come contattare i clienti tramite e-mail, SMS o notifiche push. Utilizza tre attività di azione per creare i tre rami.

3. Attendi: utilizza un&#39;attività [attendi](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience.html) per attendere che ascolti gli acquisti.

4. Condizione - Abbonamento acquistato negli ultimi 7 giorni?: utilizza un’attività condizione per ascoltare gli acquisti di prodotti negli ultimi sette giorni.

5. JourneyStepEventTracker - Abbonamento non acquistato: usa [un&#39;azione personalizzata](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions.html) per i visitatori che non hanno ancora acquistato il tuo abbonamento, nonostante abbiano ricevuto il tuo messaggio. Come parte della condizione personalizzata alla fine del percorso, creare un evento `journey.feedback` e aggiungerlo a un set di dati basato sullo schema [!UICONTROL Evento passaggio Percorso]. Utilizzerai questo evento per segmentare il pubblico che non ha acquistato l’abbonamento e che puoi targetizzare tramite annunci multimediali a pagamento.

+++

>[!TAB Percorso di conferma ordine]

Il percorso di conferma dell’ordine si concentra sul fatto che un acquisto sia stato effettuato tramite il sito web o l’app mobile. Dopo che un cliente ha completato con successo l’acquisto di, ad esempio, un abbonamento con la tua azienda, puoi impostarlo su un percorso di conferma dell’ordine.

![Panoramica visiva di alto livello del percorso di conferma ordini cliente.](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/order-confirmation-journey.png "Panoramica visiva di alto livello del percorso di conferma ordini cliente."){zoomable="yes"}

+++Logica Percorso

Utilizza gli eventi, i campi e le azioni suggeriti di seguito nel percorso di conferma:

* Il percorso viene attivato da un evento di acquisto online
   * Schema: Transazioni digitali del cliente
   * Campi:
      * `EventType`
   * Condizione:
      * `EventType = commerce.purchases`
      * Campi:
         * `Commerce.purchases.id`
         * `Commerce.purchases.value`
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

+++Logica del Percorso di chiavi

* Logica di ingresso percorso
   * Evento ordine

* Condizioni
   * Seleziona Canale di destinazione (puoi selezionare uno o più canali per una portata più ampia).
      * La conferma dell’ordine è considerata utile in natura, pertanto il controllo del consenso è solitamente superfluo.
      * E-mail
      * Push
      * SMS

   * Personalization contenuto canale
      * Visualizza le informazioni sui dettagli dell’ordine e può visualizzare un elenco di prodotti utilizzando un formato tabella.

+++

>[!ENDTABS]

Per ulteriori informazioni sulla creazione di percorsi in [!DNL Adobe Journey Optimizer], leggere la guida introduttiva di [percorsi](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html).

### Impostare una destinazione per la visualizzazione degli annunci multimediali a pagamento {#paid-media-ads}

Alcuni utenti potrebbero non aver acquistato l’abbonamento anche dopo aver ricevuto un messaggio sul nuovo programma. Dopo aver atteso per un certo numero di giorni (sette in questo caso d’uso di esempio), puoi decidere di mostrare annunci multimediali a pagamento a tali utenti, per incoraggiarli ad acquistare l’abbonamento.

Utilizza il framework delle destinazioni in Real-Time CDP per gli annunci multimediali a pagamento. Seleziona una delle numerose destinazioni pubblicitarie disponibili per visualizzare gli annunci multimediali a pagamento ai tuoi clienti e attivare il pubblico multimediale a pagamento [creato in precedenza](#create-audiences) in una destinazione a tua scelta. Visualizza una panoramica delle destinazioni [advertising](/help/destinations/catalog/advertising/overview.md) e [social](/help/destinations/catalog/social/overview.md) disponibili.

Per informazioni su come attivare i dati nelle destinazioni (ad esempio [The Trade Desk](/help/destinations/catalog/advertising/tradedesk.md) o [Google Customer Match](/help/destinations/catalog/advertising/google-customer-match.md)), consulta la documentazione seguente:

* [Creare una nuova connessione di destinazione](/help/destinations/ui/connect-destination.md)
* [Attiva i dati del pubblico nelle destinazioni di esportazione del pubblico in streaming](/help/destinations/ui/activate-segment-streaming-destinations.md)

## Passaggi successivi {#next-steps}

Impostando gli utenti a bassa frequenza e a valore elevato su un percorso e visualizzando gli annunci multimediali a pagamento in un sottoinsieme di essi, si spera di averne convertiti alcuni da clienti a valore aggiunto a vita, migliorando in tal modo la brand loyalty e le metriche di coinvolgimento dei clienti.

Successivamente, puoi esplorare altri casi d&#39;uso supportati da Real-Time CDP, ad esempio [coinvolgere nuovamente i clienti in modo intelligente](/help/rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md) o [visualizzare contenuti personalizzati a utenti non autenticati](/help/rtcdp/partner-data/onsite-personalization.md) nelle tue proprietà Web.
