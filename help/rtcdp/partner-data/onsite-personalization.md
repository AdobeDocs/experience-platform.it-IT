---
title: Utilizzo del riconoscimento visitatori assistito dal partner per personalizzare le esperienze nel sito
description: Scopri come utilizzare il riconoscimento visitatori assistito dal partner per offrire esperienze personalizzate nel sito a chi lo visita.
source-git-commit: 9d7e8ef99a42e804896f5c9befcf98bb1c010606
workflow-type: tm+mt
source-wordcount: '2530'
ht-degree: 99%

---

# Utilizzo del riconoscimento visitatori assistito dal partner per personalizzare le esperienze nel sito

>[!AVAILABILITY]
>
>Questa funzionalità in versione è disponibile per i clienti che dispongono di una licenza per Real-Time CDP (App Service), Adobe Experience Platform Activation, Real-time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate. Ulteriori informazioni su questi pacchetti sono disponibili nelle [descrizioni dei prodotti](https://helpx.adobe.com/it/legal/product-descriptions.html). Contatta il tuo rappresentante Adobe per ulteriori informazioni.

Scopri come utilizzare il riconoscimento assistito dal partner per fornire esperienze personalizzate ai visitatori delle tue proprietà web. Usa questo tutorial per comprendere la sequenza di implementazione dei vari elementi in Experience Platform e altre soluzioni di Experience Cloud per mostrare un’esperienza personalizzata ai visitatori autenticati e non autenticati.

![Un’infografica che descrive come utilizzare gli attributi forniti dai partner per offrire esperienze personalizzate ai visitatori.](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-steps.png)

## Esempio di settore {#industry-example}

Ad esempio, prendi in considerazione un marchio di fai da te con tassi di autenticazione bassi. Questo marchio desidera offrire esperienze personalizzate ai nuovi visitatori, senza cronologia o autenticazione precedenti e senza la perdita di affidabilità dai cookie di terze parti.

Questo marchio sceglie di sfruttare la tecnologia di riconoscimento partner per riconoscere in modo probabilistico il visitatore e offrire un’esperienza più personalizzata. Questo consente di avere una valutazione anticipata, man mano che il visitatore si sposta lungo il funnel di marketing. Ad esempio, il marchio potrebbe utilizzare segnali demografici forniti dai partner per contenuti nel sito che attraggono persone che si sono trasferite di recente e offrono uno sconto sui prodotti fai da te più diffusi.

## Prerequisiti e pianificazione {#prerequisites-and-planning}

Quando prevedi di utilizzare gli attributi forniti dai partner per offrire esperienze personalizzate ai visitatori autenticati e non autenticati, prendi in considerazione i prerequisiti seguenti nel processo di pianificazione:

* Quali input sono previsti dalla tecnologia di riconoscimento partner in modo che possa creare livelli su attributi aggiuntivi?
* In che misura sei a tuo agio nel distribuire la personalizzazione in canali diversi e per diversi casi d’uso basati su attributi derivati in modo probabilistico rispetto ad attributi confermati deterministicamente?
* In che modo deve cambiare l’esperienza di un visitatore pre-autenticato ma riconosciuto durante l’autenticazione?

### Funzionalità dell’interfaccia utente, componenti della piattaforma e prodotti di Experience Cloud che utilizzerai {#ui-functionality-and-elements}

Per implementare correttamente questo caso d’uso, devi utilizzare più aree di Real-time Customer Data Platform e altre soluzioni Experience Cloud. Assicurati di disporre delle [autorizzazioni di controllo degli accessi basate su attributi](/help/access-control/abac/overview.md) per tutte queste aree o richiedi all’amministratore di sistema di concedere le autorizzazioni necessarie.

* Raccolta dati
   * [Adobe Experience Platform Web SDK](/help/edge/home.md)
   * [Tag](/help/tags/home.md)
   * [Stream di dati](/help/datastreams/overview.md)
* Gestione dei dati in Real-Time CDP
   * [Identità](/help/identity-service/namespaces.md)
   * [Schemi](/help/xdm/home.md)
   * [Etichette di utilizzo dei dati](/help/data-governance/labels/overview.md)
   * [Set di dati](/help/catalog/datasets/overview.md)
* Personalizzazione delle proprietà web
   * [Segmentazione Edge](/help/segmentation/ui/edge-segmentation.md)
   * [Destinazioni di personalizzazione Edge](/help/destinations/destination-types.md#edge-personalization-destinations)
   * [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) (o una piattaforma di personalizzazione a tua scelta. Questo tutorial sui casi d’uso mette in evidenza Adobe Target come motore di personalizzazione)

## Come utilizzare il caso d’uso: panoramica di alto livello {#achieve-the-use-case-high-level}

![Un’infografica che descrive come utilizzare gli attributi forniti dai partner per offrire esperienze personalizzate ai visitatori.](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-steps.png)

1. Come **cliente**, disponi di una licenza concessa dal **partner di dati** per poter recuperare informazioni in tempo reale su visitatori di siti web altrimenti anonimi.
2. Come **cliente**, implementi librerie lato client nelle proprietà per chiamare le API **partner** e configuri Web SDK o SDK Mobile per inviare i segnali forniti dai partner a Real-Time CDP.
3. Durante la navigazione nel sito web o nell’app, il **visitatore** è riconosciuto in modo probabilistico dal **partner**, che restituisce gli attributi insieme a un ID.
4. Real-Time CDP esegue la segmentazione Edge per valutare gli hit dell’evento in arrivo e i risultati persistenti rispetto all’[Identificatore ECID](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=it).
5. Adobe Target utilizza l’output della segmentazione Edge per restituire l’esperienza al **visitatore** per la personalizzazione durante la sessione.
6. L’evento viene salvato in modo permanente nel suo complesso per i flussi di lavoro a valle come l’analisi e il retargeting.

## Come utilizzare il caso d’uso: istruzioni dettagliate {#step-by-step-instructions}

Leggi le sezioni seguenti, che includono collegamenti a un ulteriore documentazione, per completare ciascuno dei passaggi descritti nella panoramica di alto livello qui sopra.

### Gestione dei dati: crea uno spazio dei nomi, uno schema e un set di dati di identità per gestire gli attributi dei dati {#data-management}

Per poter personalizzare l’esperienza dei visitatori non autenticati con il caso d’uso, è necessario prima impostare la struttura di gestione dei dati in Real-Time CDP per ricevere i dati in arrivo relativi all’evento in tempo reale e i dati di qualifica del pubblico.

#### Creare lo spazio dei nomi identità dell’ID partner

Innanzitutto, devi creare uno spazio dei nomi identità dell’ID partner. Passa a **[!UICONTROL Cliente]** > **[!UICONTROL Identità]** nella barra a sinistra, quindi seleziona **[!UICONTROL Crea spazio dei nomi identità]** nell’angolo superiore a destra dello schermo.

![Viene evidenziata la finestra di dialogo Crea spazio dei nomi identità con l’ID partner.](/help/rtcdp/assets/partner-data/onsite-personalization/create-identity-namespace.png)

Ulteriori informazioni su come [creare uno spazio dei nomi identità dell’ID partner](/help/rtcdp/partner-data/prospecting.md#create-partner-id-namespace).

#### Crea uno schema

Quindi, crea uno schema [!UICONTROL Evento esperienza] per memorizzare i dati della serie temporale che verranno successivamente raccolti dalle proprietà web e assicurati di utilizzare [!UICONTROL XDM ExperienceEvent] come classe base per lo schema. Ulteriori informazioni su come [creare uno schema utilizzando l’interfaccia utente di Experienci Platform](/help/xdm/ui/resources/schemas.md#create).

![L’area di lavoro Schemi con Crea schema ed evento Esperienza XDM evidenziati.](/help/rtcdp/assets/partner-data/onsite-personalization/create-experience-event-schema.png)

Durante la creazione dello schema e mentre [aggiungi gruppi di campi nello schema](/help/xdm/ui/resources/schemas.md#add-field-groups), prendi in considerazione di aggiungere i gruppi di campi [Visita pagina web](/help/xdm/field-groups/event/web-details.md) e [Mappa delle identità](/help/xdm/field-groups/profile/identitymap.md). Questo si aggiunge ad altri gruppi di campi applicabili alla proprietà digitale e alle pratiche di raccolta dei dati.

Inoltre, puoi creare o riutilizzare un gruppo di campi esistente e aggiungerlo allo schema per acquisire informazioni sul visitatore fornite dal partner. Scopri come [creare un gruppo di campi](/help/xdm/ui/resources/field-groups.md) e come [aggiungere campi](/help/xdm/ui/resources/field-groups.md) al gruppo di campi. Ad esempio, se ti aspetti di personalizzare in base agli approfondimenti forniti dal partner come fascia di età, status occupazionale, potenziale di spesa mensile o comportamenti di acquisto, includi i campi appropriati nel tuo gruppo di campi.

Se il partner dati fornisce un identificatore stabile per il visitatore e desideri inserirlo in Real-Time CDP, assicurati di disporre di un campo con nome appropriato per l’identificatore nel gruppo di campi personalizzato. Devi anche contrassegnare il campo come identità nello spazio dei nomi identità creato in precedenza. Ricorda anche di [abilitare lo schema da includere nel profilo](/help/xdm/ui/resources/schemas.md#profile).

#### Creare un set di dati

Successivamente, devi creare un set di dati per memorizzare i dati della serie temporale che raccogli dai visitatori delle tue proprietà web e che utilizzerai per la personalizzazione nel sito.

Consulta il tutorial su [come creare un set di dati](/help/catalog/datasets/user-guide.md#create) e ricorda di selezionare l’opzione per creare il set di dati da uno schema. Crea il set di dati in base allo schema creato nel passaggio precedente.

Analogamente al passaggio durante la creazione di uno schema, devi abilitare il set di dati da includere nel [!UICONTROL Profilo cliente in tempo reale]. Per ulteriori informazioni sull’abilitazione del set di dati per l’utilizzo nel [!UICONTROL Profilo cliente in tempo reale], consulta il [tutorial su come creare uno schema.](/help/xdm/tutorials/create-schema-ui.md#profile)

### Implementare la raccolta dati evento sulla proprietà web {#implement-data-collection}

Dopo aver configurato la configurazione di gestione dati, ora devi implementare la [raccolta dati](/help/collection/home.md) evento in tempo reale nella tua proprietà web. Devi dotare la tua proprietà di una libreria di raccolta dati Adobe, [!UICONTROL Web SDK], per raccogliere le chiamate evento in tempo reale e inviarle nuovamente a Real-Time CDP. Questo elemento è costituito da alcune attività separate in alcuni componenti della raccolta dati.

>[!IMPORTANT]
>
>Per recuperare gli attributi forniti dal partner, è necessario *integrare la tua proprietà web con le API del partner o con altri metodi per chiamare e recuperare gli attributi dai partner di dati in tempo reale*. Discuti di questo aspetto con il tuo partner preferito in quanto non è soggetto di questo tutorial.

Innanzitutto, utilizza il selettore dell’applicazione nell’angolo superiore a destra dello schermo per passare alla sezione **[!UICONTROL Raccolta dati]**.

>[!TIP]
>
> Se non riesci a visualizzare la sezione [!UICONTROL Raccolta dati] nel selettore dell’applicazione, contatta l’amministratore di sistema per richiedere l’accesso.

![Selettore dell’app per passare alla sezione Raccolta dati.](/help/rtcdp/assets/partner-data/onsite-personalization/app-switcher-data-collection.png)

La sezione **[!UICONTROL Raccolta dati]** dell’interfaccia utente è simile all’immagine riportata di seguito.

![Sezione Raccolta dati dell’interfaccia utente di Platform.](/help/rtcdp/assets/partner-data/onsite-personalization/data-collection-home.png)

#### Creare uno stream di dati

Come primo passaggio nella sezione raccolta dati, [crea un nuovo stream di dati](/help/datastreams/configure.md). Lo stream di dati è la base del modo in cui i dati vengono raccolti e indirizzati propriamente all’app di Adobe corretta, in questo caso Experience Platform.

Durante la creazione dello stream di dati, nel campo **[!UICONTROL Schema evento]**, seleziona lo schema creato in precedenza.

![Il selettore Schema evento evidenziato durante la configurazione di un nuovo stream di dati.](/help/rtcdp/assets/partner-data/onsite-personalization/event-schema-selector-datastream.png)

[Seleziona il set di dati dell’evento](/help/datastreams/configure.md#aep) creato in precedenza dal menu a discesa, seleziona le caselle accanto a **[!UICONTROL Segmentazione Edge]** e **[!UICONTROL Destinazioni di personalizzazione]**, e seleziona **[!UICONTROL Salva]**.

In questo scenario non è necessario selezionare un set di dati di profilo, in quanto si stanno inserendo dati di serie temporali basati su eventi.

#### Creare le proprietà dei tag

Pensa a una proprietà come a un contenitore che si riempie con estensioni, regole, elementi dati e librerie durante la distribuzione di tag sul sito.

Accedi a **[!UICONTROL Tag]** e seleziona **[!UICONTROL Nuova proprietà]**.

![Crea una nuova proprietà dei tag.](/help/rtcdp/assets/partner-data/onsite-personalization/create-tag-property.png)

Compila i campi obbligatori e seleziona **[!UICONTROL Salva]**.

![Compila i campi obbligatori per la nuova proprietà.](/help/rtcdp/assets/partner-data/onsite-personalization/tag-property-fields.png)

Ottieni informazioni complete su come [creare una proprietà dei tag](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/create-a-property.html?lang=it).

Successivamente, devi installare diverse estensioni all’interno della proprietà. Seleziona la proprietà dei tag e passa alla sezione [!UICONTROL Estensioni].

![Seleziona la nuova proprietà dei tag.](/help/rtcdp/assets/partner-data/onsite-personalization/select-tag-property.png)

Tieni presente che l’estensione [!UICONTROL Core] è già installata. È necessario installare altre due estensioni, come descritto nelle sezioni successive.

![Visualizza le estensioni installate.](/help/rtcdp/assets/partner-data/onsite-personalization/view-existing-extensions.png)

#### Installare l’estensione Web SDK

Questo tutorial indica come dotare il tuo sito web di Web SDK. Puoi anche utilizzare [SDK Mobile](https://developer.adobe.com/client-sdks/documentation/) nell’app per personalizzare l’esperienza per i visitatori dell’app.

![Visualizzazione dell’estensione Web SDK nel catalogo delle estensioni.](/help/rtcdp/assets/partner-data/onsite-personalization/web-sdk-extension.png)

Nella schermata per configurare il Web SDK, passa alla sezione **[!UICONTROL Stream di dati]** e fornisci informazioni sulla sandbox di Experience Platform in uso. Dal menu a discesa successivo, seleziona la sandbox appropriata e lo stream di dati creato nei passaggi precedenti. Puoi scegliere gli stessi valori sandbox e stream di dati per tutti gli altri ambienti. Lascia invariate le altre impostazioni e seleziona **[!UICONTROL Salva]**.

Ottieni informazioni complete su [come installare Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/tags-configuration/install-web-sdk.html?lang=it).

#### Installare l’estensione del servizio ID

Utilizza l’[estensione del servizio ID di Experience Cloud](/help/tags/extensions/client/id-service/overview.md) per creare un’identità di prime parti univoca basata su dispositivo per i visitatori in tutte le soluzioni Experience Cloud. Cerca **[!UICONTROL Servizio ID]** nel catalogo delle estensioni e installalo. Mantieni tutte le impostazioni predefinite durante l’installazione dell’estensione.

![Visualizzazione dell’estensione del servizio ID nel catalogo delle estensioni.](/help/rtcdp/assets/partner-data/onsite-personalization/id-service-extension.png)

#### Configurare gli ambienti

Quindi, passa alla sezione **[!UICONTROL Ambienti]** dal menu di navigazione a sinistra. In questo passaggio, devi collegare il tuo sito web ad Adobe Edge Network per recuperare e consegnare le informazioni sui visitatori in tempo reale.

Seleziona l’icona della casella a destra per l’ambiente di sviluppo e copia la versione standard dello snippet di codice JavaScript visualizzato in una finestra modale.

![Icona della casella selezionata evidenziata nella sezione Ambienti dell’interfaccia utente di Raccolta dati.](/help/rtcdp/assets/partner-data/onsite-personalization/select-box-icon.png)

Devi aggiungere questo snippet di codice nella parte superiore del sito web. Di conseguenza, il sito web effettuerà una chiamata alla rete Adobe Edge per recuperare la logica JavaScript che verrà caricata ed eseguita sulla pagina. Questo consente il funzionamento di funzionalità quali la generazione di ID visitatore, la raccolta di dati e la personalizzazione delle esperienze in tempo reale.

#### Impostare gli elementi dati

Gli elementi dati sono i blocchi costitutivi per il dizionario dei dati (o mappa dati). Un singolo elemento dati è una variabile il cui valore può essere mappato alle stringhe di query, agli URL, ai valori dei cookie, alle variabili JavaScript e così via. Consulta ulteriori informazioni sugli [elementi dati](/help/tags/ui/managing-resources/data-elements.md).

Ai fini di questo caso d’uso, devi impostare due elementi dati.

Innanzitutto, imposta un elemento `partnerData`. Passa alla sezione **[!UICONTROL Elementi dati]** e seleziona **[!UICONTROL Crea un nuovo elemento dati]**.

![Crea un nuovo elemento di dati.](/help/rtcdp/assets/partner-data/onsite-personalization/create-data-element.gif)

Assegna un nome all’elemento dati `partnerData`, lascia il valore [!UICONTROL estensione] come [!UICONTROL Core] e imposta **[!UICONTROL Tipo di elemento dati]** come **[!UICONTROL Variabile JavaScript]**. Inserisci `partnerData` nel campo con titolo **[!UICONTROL Nome variabile JavaScript]** e seleziona **[!UICONTROL Salva]**.

![Selezioni per configurare correttamente l’elemento dati partnerData evidenziate.](/help/rtcdp/assets/partner-data/onsite-personalization/create-partnerdata-data-element.png)

Per impostare il secondo elemento dati, assegna un nome alla nuova variabile `pageVisit`, imposta l’**[!UICONTROL estensione]** su **[!UICONTROL Adobe Experience Platform]** e scegli **[!UICONTROL Oggetto XDM]** come tipo di dati.

![Sono state evidenziate le selezioni per configurare correttamente l’elemento dati pageVisit.](/help/rtcdp/assets/partner-data/onsite-personalization/page-visit-data-element.png)

Dallo schema, seleziona gli attributi di terze parti corrispondenti ai valori previsti per il partner di dati. Quindi, seleziona il pulsante di opzione con titolo **[!UICONTROL Fornisci l’intero oggetto]**. Seleziona l’icona che assomiglia a un database e scegli l’elemento dati `partnerData` creato in precedenza.

#### Impostare le regole

Nella sezione **[!UICONTROL Regole]**, puoi configurare il sito web per inviare una richiesta di personalizzazione ad Adobe con gli attributi caricati negli elementi dati appena creati. Consulta ulteriori informazioni sulla [creazione di regole](/help/tags/ui/managing-resources/rules.md).

Seleziona **[!UICONTROL Crea nuova regola]**. Assegna a questa regola il nome **[!UICONTROL Personalizzazione]** e seleziona il segno + accanto a **[!UICONTROL Eventi]**. Seleziona **[!UICONTROL Fondo pagina]** come evento e salva.

![Selezioni per la parte del tipo di evento di una regola.](/help/rtcdp/assets/partner-data/onsite-personalization/add-events-rule.png)

Seleziona il segno + accanto ad **[!UICONTROL Azioni]**. Aggiorna l’estensione ad **[!UICONTROL Adobe Experience Platform Web SDK]** e imposta **[!UICONTROL Tipo di azione]** su **[!UICONTROL Invia evento]**.

![Selezioni per la parte del tipo di azione di una regola.](/help/rtcdp/assets/partner-data/onsite-personalization/add-action-rule.png)

Dal selettore a discesa **[!UICONTROL Tipo]** sulla destra, seleziona `web.webpagedetails.pageViews` come tipo di evento.

![Seleziona tipo di evento.](/help/rtcdp/assets/partner-data/onsite-personalization/add-pageview-type-rule.png)

Seleziona l’icona a forma di database accanto ai dati XDM e seleziona l’elemento dati `pageVisit`.

Scorri verso il basso l’elenco delle configurazioni di azioni e verifica di selezionare la casella con titolo **[!UICONTROL Esegui il rendering delle decisioni di personalizzazione visive]**. Questo è importante per consentire il rendering visivo nella pagina web delle esperienze distribuite tramite Adobe Target o altri prodotti simili. Seleziona **[!UICONTROL Mantieni modifiche]** e quindi **[!UICONTROL Salva]** la regola.

![Selezione della casella di controllo Esegui il rendering delle decisioni di personalizzazione visive.](/help/rtcdp/assets/partner-data/onsite-personalization/render-visual-personalization-toggle.png)

#### Impostare il flusso di lavoro di pubblicazione

Per distribuire questa configurazione alla pagina web, il passaggio successivo consiste nel creare una libreria che includa le risorse appena create. Consulta ulteriori informazioni sull’[impostazione di un flusso di pubblicazione](/help/tags/ui/publishing/publishing-flow.md).

Seleziona **[!UICONTROL Flusso di pubblicazione]** e quindi **[!UICONTROL Aggiungi libreria]**.

Seleziona **[!UICONTROL Aggiungi tutte le risorse modificate]**, assegna un nome alla libreria, imposta l’ambiente su **[!UICONTROL Sviluppo]** e seleziona **[!UICONTROL Salva e genera in sviluppo]**.

![Creare una libreria e distribuirla nell’ambiente di sviluppo](/help/rtcdp/assets/partner-data/onsite-personalization/create-publishing-workflow.gif)

#### Verificare il sito web

A questo punto, il sito web deve essere dotato di Web SDK completo. Per verificare che la raccolta dati funzioni come previsto, puoi accedere al tuo sito web e utilizzare gli strumenti di sviluppo del browser per controllare il traffico di rete.

Immetti `interact` nella casella di ricerca, aggiorna la pagina e dovresti vedere le chiamate di rete dal sito web alla rete Adobe Edge che si sta popolando.

![Visualizzazione degli eventi di rete popolati negli strumenti per sviluppatori.](/help/rtcdp/assets/partner-data/onsite-personalization/events-filtered.png)

### Personalizzazione {#personalization}

Ora puoi creare e attivare tipi di pubblico per la personalizzazione.

#### Impostare la segmentazione Edge

Configura la [segmentazione Edge](/help/segmentation/ui/edge-segmentation.md) in modo che l’appartenenza a un pubblico dei visitatori sia valutata in tempo reale, quando visitano la tua proprietà web.

Assicurati anche di impostare un [criterio di unione attivo su Edge](/help/destinations/ui/activate-edge-personalization-destinations.md#create-merge-policy) per i tipi di pubblico Edge.

#### Integrazione con Adobe Target o un’altra destinazione di personalizzazione personalizzata

Ora puoi effettuare l’integrazione con un motore di personalizzazione per mostrare contenuti personalizzati ai visitatori del tuo sito web o dell’app. A tal fine, Adobe consiglia di utilizzare la [destinazione Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md).

>[!IMPORTANT]
>
>Consulta il tutorial sull’[attivazione di tipi di pubblico per destinazioni di personalizzazione Edge](/help/destinations/ui/activate-edge-personalization-destinations.md) per una visualizzazione completa dei passaggi necessari per attivare i tipi di pubblico.

## Limitazioni e risoluzione dei problemi {#limitations-and-troubleshooting}

Durante l’esplorazione del caso d’uso descritto in questa pagina, tieni presente le seguenti limitazioni:

* Se utilizzi gli ID partner, tieni presente che non vengono utilizzati durante la creazione del [grafico identità](/help/identity-service/ui/identity-graph-viewer.md).

## Altri casi d’uso ottenuti tramite il supporto dei dati dei partner {#other-use-cases}

Esplora altri casi d’uso abilitati tramite il supporto dei dati dei partner in Real-Time CDP:

* [Puoi integrare i profili di prime parti con attributi di partner di dati affidabili, per migliorare la base di dati, acquisire nuove informazioni sulla base dei clienti e una migliore ottimizzazione del pubblico.](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
* Utilizza il supporto dati di terze parti in Real-Time CDP per [espandere la base di profili con i profili di potenziali clienti dei partner dati e interagisci con loro per acquisire o raggiungere nuovi clienti](/help/rtcdp/partner-data/prospecting.md).
* [Attivazione estesa di profili di potenziali clienti e tipi di pubblico di potenziali clienti](/help/destinations/ui/activate-prospect-audiences.md) per selezionare le destinazioni.