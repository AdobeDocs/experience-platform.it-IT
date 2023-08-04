---
title: Utilizzo del riconoscimento dei visitatori con l'ausilio dei partner per personalizzare le esperienze in loco
description: Scopri come utilizzare il riconoscimento dei visitatori supportato dai partner per offrire esperienze personalizzate nel sito ai visitatori.
hide: true
hidefromtoc: true
source-git-commit: f63cddc1158e739ce26e0ce1d3d54b491bd80c06
workflow-type: tm+mt
source-wordcount: '2493'
ht-degree: 7%

---

# Utilizzare il riconoscimento dei visitatori supportato dai partner per personalizzare le esperienze nel sito

Scopri come utilizzare il riconoscimento supportato dai partner per fornire esperienze personalizzate ai visitatori delle tue proprietà web. Usa questa esercitazione per comprendere la sequenza di implementazione dei vari elementi in Experienci Platform e altre soluzioni di Experience Cloud per mostrare un’esperienza personalizzata ai visitatori autenticati e non autenticati.

![Un’infografica che descrive come utilizzare gli attributi forniti dai partner per fornire esperienze personalizzate ai visitatori.](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-steps.png)

## Esempio di settore {#industry-example}

Ad esempio, considera un marchio di miglioramento della casa con tassi di autenticazione bassi. Questo brand desidera offrire esperienze personalizzate ai nuovi visitatori, senza cronologia o autenticazione precedenti e senza la perdita di affidabilità dai cookie di terze parti.

Questo brand sceglie di sfruttare la tecnologia di riconoscimento dei partner per riconoscere probabilisticamente il visitatore e offrire un’esperienza più personalizzata. Questo consente di avere una considerazione anticipata, man mano che il visitatore scende lungo il funnel di marketing. Ad esempio, il brand potrebbe utilizzare segnali demografici forniti dai partner per contenuti nel sito che attraggono persone che si sono trasferite di recente e offrono uno sconto sui prodotti fai-da-te più diffusi.

## Prerequisiti e pianificazione {#prerequisites-and-planning}

Quando prevedi di utilizzare gli attributi forniti dai partner per fornire esperienze personalizzate ai visitatori autenticati e non autenticati, considera i seguenti prerequisiti nel processo di pianificazione:

* Quali input sono previsti dalla tecnologia di riconoscimento del partner in modo che possa creare livelli su attributi aggiuntivi?
* In che misura sei a tuo agio nel distribuire la personalizzazione in canali diversi e per diversi casi d’uso basati su attributi derivati probabilisticamente rispetto ad attributi confermati deterministicamente?
* In che modo deve cambiare l’esperienza di un visitatore pre-autenticato ma riconosciuto durante l’autenticazione?

### Funzionalità dell’interfaccia utente, componenti della piattaforma e prodotti di Experience Cloud che utilizzerai {#ui-functionality-and-elements}

Per implementare correttamente questo caso d’uso, devi utilizzare più aree di Real-time Customer Data Platform e altre soluzioni Experience Cloud. Assicurati di disporre dei [autorizzazioni di controllo degli accessi basate su attributi](/help/access-control/abac/overview.md) per tutte queste aree o richiedere all&#39;amministratore di sistema di concedere le autorizzazioni necessarie.

* Raccolta dati
   * [Adobe Experience Platform Web SDK](/help/edge/home.md)
   * [Tag](/help/tags/home.md)
   * [Stream di dati](/help/datastreams/overview.md)
* Gestione dei dati in Real-Time CDP
   * [Identità](/help/identity-service/namespaces.md)
   * [Schemi](/help/xdm/home.md)
   * [Etichette di utilizzo dati](/help/data-governance/labels/overview.md)
   * [Set di dati](/help/catalog/datasets/overview.md)
* Personalizzazione delle proprietà web
   * [Segmentazione Edge](/help/segmentation/ui/edge-segmentation.md)
   * [Destinazioni di personalizzazione Edge](/help/destinations/destination-types.md#edge-personalization-destinations)
   * [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) (o una piattaforma di personalizzazione a tua scelta. Questo tutorial evidenzia Adobe Target come motore di personalizzazione)

## Come utilizzare il caso d’uso: panoramica di alto livello {#achieve-the-use-case-high-level}

![Un’infografica che descrive come utilizzare gli attributi forniti dai partner per fornire esperienze personalizzate ai visitatori.](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-steps.png)

1. As a **cliente**, la licenza viene concessa da **partner dati** la possibilità di recuperare informazioni in tempo reale su visitatori di siti web altrimenti anonimi.
2. As a **cliente**, distribuisci librerie lato client nelle proprietà da chiamare **partner** e configuri Web SDK o Mobile SDK per inviare i segnali forniti dai partner a Real-Time CDP.
3. Durante la navigazione nel sito web o nell’app, il **visitatore** è riconosciuto probabilisticamente dal **partner**, che restituisce gli attributi insieme a un ID.
4. Real-Time CDP esegue la segmentazione Edge per valutare gli hit dell’evento in arrivo e i risultati persistenti rispetto al [Identificatore ECID](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=it).
5. Adobe Target utilizza l’output della segmentazione Edge per restituire l’esperienza al **visitatore** per la personalizzazione durante la sessione.
6. L’evento viene mantenuto nella sua interezza per i flussi di lavoro a valle come l’analisi e il retargeting.

## Come utilizzare il caso d’uso: istruzioni dettagliate {#step-by-step-instructions}

Leggi le sezioni seguenti, che includono collegamenti a un ulteriore documentazione, per completare ciascuno dei passaggi descritti nella panoramica di alto livello qui sopra.

### Gestione dei dati: crea uno spazio dei nomi, uno schema e un set di dati di identità per gestire gli attributi dei dati {#data-management}

Per poter personalizzare l’esperienza dei visitatori non autenticati con il caso d’uso, devi prima impostare la struttura di gestione dei dati in Real-Time CDP per ricevere i dati in arrivo relativi all’evento in tempo reale e alla qualifica del pubblico.

#### Creare lo spazio dei nomi dell’identità dell’ID partner

Innanzitutto, devi creare uno spazio dei nomi di identità dell’ID partner. Accedi a **[!UICONTROL Cliente]** > **[!UICONTROL Identità]** nella barra a sinistra, quindi seleziona **[!UICONTROL Creare lo spazio dei nomi delle identità]** nell&#39;angolo superiore destro dello schermo.

![Viene evidenziata la finestra di dialogo Crea spazio dei nomi dell’identità con ID partner.](/help/rtcdp/assets/partner-data/onsite-personalization/create-identity-namespace.png)

Ulteriori informazioni su come [creare uno spazio dei nomi dell’identità dell’ID partner](/help/rtcdp/partner-data/prospecting.md#create-partner-id-namespace).

#### Creare uno schema

Quindi, crea un&#39; [!UICONTROL Evento esperienza] schema per memorizzare i dati della serie temporale che verranno successivamente raccolti dalle proprietà web e assicurati di utilizzare [!UICONTROL XDM ExperienceEvent] come classe base per lo schema. Scopri come [creare uno schema tramite l’interfaccia utente di Experienci Platform](/help/xdm/ui/resources/schemas.md#create).

![L’area di lavoro Schemi con Crea schema ed evento Esperienza XDM evidenziato.](/help/rtcdp/assets/partner-data/onsite-personalization/create-experience-event-schema.png)

Durante la creazione dello schema e [aggiungi gruppi di campi a nello schema](/help/xdm/ui/resources/schemas.md#add-field-groups), provare ad aggiungere [Visita pagina web](/help/xdm/field-groups/event/web-details.md) e [Mappa identità](/help/xdm/field-groups/profile/identitymap.md) gruppi di campi. Questo si aggiunge ad altri gruppi di campi applicabili alla proprietà digitale e alle pratiche di raccolta dei dati.

Inoltre, puoi creare o riutilizzare un gruppo di campi esistente e aggiungerlo allo schema per acquisire informazioni sul visitatore fornite dal partner. Scopri come [creare un gruppo di campi](/help/xdm/ui/resources/field-groups.md) e come [aggiungi campi](/help/xdm/ui/resources/field-groups.md) al gruppo di campi. Ad esempio, se ti aspetti di personalizzare in base alle informazioni fornite dal partner come fascia di età, stato di impiego, potere di spesa mensile o comportamenti di acquisto, chiedi al tuo gruppo di campi di includere i campi appropriati.

Se il partner dati fornisce un identificatore stabile per il visitatore e desideri inserirlo in Real-Time CDP, assicurati di disporre di un campo con nome appropriato per l’identificatore nel gruppo di campi personalizzato. Devi anche contrassegnare il campo come identità nello spazio dei nomi delle identità creato in precedenza. Ricorda anche a [abilitare lo schema da includere nel profilo](/help/xdm/ui/resources/schemas.md#profile).

#### Creare un set di dati

Successivamente, devi creare un set di dati per memorizzare i dati della serie temporale che raccogli dai visitatori delle tue proprietà web e che userai per la personalizzazione nel sito.

Leggi l’esercitazione su [come creare un set di dati](/help/catalog/datasets/user-guide.md#create) e ricorda di selezionare l’opzione per creare il set di dati da uno schema. Crea il set di dati in base allo schema creato nel passaggio precedente.

Simile al passaggio durante la creazione di uno schema, devi abilitare il set di dati da includere nel [!UICONTROL Profilo cliente in tempo reale]. Per ulteriori informazioni sull’abilitazione del set di dati per l’utilizzo in [!UICONTROL Profilo cliente in tempo reale], leggi [tutorial su come creare uno schema.](/help/xdm/tutorials/create-schema-ui.md#profile)

### Implementare la raccolta dati evento sulla proprietà web {#implement-data-collection}

Dopo aver configurato la configurazione di gestione dati, ora devi implementare l’evento in tempo reale [raccolta dati](/help/collection/home.md) nella tua proprietà web. Devi dotare la tua proprietà di una libreria di raccolta dati Adobe: [!UICONTROL SDK per web] : per raccogliere le chiamate evento in tempo reale e inviarle nuovamente a Real-Time CDP. Questo elemento è costituito da alcune attività separate in alcuni componenti di raccolta dati.

>[!IMPORTANT]
>
>Per recuperare gli attributi forniti dal partner, è necessario *integra la tua proprietà web con le API dei partner o con altri metodi per richiamare e recuperare gli attributi dai partner dati in tempo reale*. Discuta di questo aspetto con il tuo partner preferito in quanto non è soggetto a questa esercitazione.

Innanzitutto, utilizza il selettore dell’applicazione nell’angolo superiore destro dello schermo per passare al **[!UICONTROL Raccolta dati]** sezione.

>[!TIP]
>
>Contatta l’amministratore di sistema per richiedere l’accesso se non riesci a visualizzare [!UICONTROL Raccolta dati] nel commutatore dell&#39;applicazione.

![Commutatore dell’app per passare alla sezione Raccolta dati.](/help/rtcdp/assets/partner-data/onsite-personalization/app-switcher-data-collection.png)

Il **[!UICONTROL Raccolta dati]** dell’interfaccia utente è simile all’immagine riportata di seguito.

![Sezione Raccolta dati dell’interfaccia utente di Platform.](/help/rtcdp/assets/partner-data/onsite-personalization/data-collection-home.png)

#### Creare un flusso di dati

Come primo passaggio nella sezione raccolta dati, [creare un nuovo flusso di dati](/help/datastreams/configure.md). Il flusso di dati è la base del modo in cui i dati vengono raccolti e indirizzati correttamente all’app di Adobe corretta, in questo Experience Platform.

Durante la creazione dello stream di dati, nella **[!UICONTROL Schema evento]** , seleziona lo schema creato in precedenza.

![Il selettore schema eventi è evidenziato durante la configurazione di un nuovo stream di dati.](/help/rtcdp/assets/partner-data/onsite-personalization/event-schema-selector-datastream.png)

[Seleziona il set di dati dell’evento](/help/datastreams/configure.md#aep) creato in precedenza dal menu a discesa, seleziona le caselle accanto a **[!UICONTROL Segmentazione Edge]** e **[!UICONTROL Destinazioni di personalizzazione]**, e seleziona **[!UICONTROL Salva]**.

In questo scenario non è necessario selezionare un set di dati di profilo, in quanto si stanno inserendo dati di serie temporali basati su eventi.

#### Crea proprietà tag

Considera una proprietà come un contenitore che si riempie con estensioni, regole, elementi dati e librerie durante la distribuzione di tag nel sito.

Accedi a **[!UICONTROL Tag]** e seleziona **[!UICONTROL Nuova proprietà]**.

![Crea una nuova proprietà tag.](/help/rtcdp/assets/partner-data/onsite-personalization/create-tag-property.png)

Compila i campi obbligatori e seleziona **[!UICONTROL Salva]**.

![Compila i campi obbligatori per la nuova proprietà.](/help/rtcdp/assets/partner-data/onsite-personalization/tag-property-fields.png)

Informazioni complete su come [creare una proprietà tag](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/create-a-property.html).

Successivamente, devi installare diverse estensioni all&#39;interno della proprietà. Seleziona la proprietà tag e passa alla [!UICONTROL Estensioni] sezione.

![Seleziona la nuova proprietà tag.](/help/rtcdp/assets/partner-data/onsite-personalization/select-tag-property.png)

Tieni presente che [!UICONTROL Core] l&#39;estensione è già installata. È necessario installare altre due estensioni, come descritto nelle sezioni successive.

![Visualizzare le estensioni installate.](/help/rtcdp/assets/partner-data/onsite-personalization/view-existing-extensions.png)

#### Installare l’estensione Web SDK

Questo tutorial indica come dotare il tuo sito web di Web SDK. Puoi anche utilizzare [SDK per dispositivi mobili](https://developer.adobe.com/client-sdks/documentation/) nell’app per personalizzare l’esperienza per i visitatori dell’app.

![Visualizzazione dell&#39;estensione Web SDK nel catalogo delle estensioni.](/help/rtcdp/assets/partner-data/onsite-personalization/web-sdk-extension.png)

Nella schermata per configurare l’SDK per web, passa a **[!UICONTROL Flussi di dati]** e fornire informazioni sulla sandbox di Experience Platform in uso. Dal menu a discesa successivo, seleziona la sandbox appropriata e lo stream di dati creato nei passaggi precedenti. Puoi scegliere gli stessi valori sandbox e stream di dati per tutti gli altri ambienti. Lascia invariate le altre impostazioni e seleziona **[!UICONTROL Salva]**.

Ottieni informazioni complete su [come installare Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/tags-configuration/install-web-sdk.html).

#### Estensione del servizio ID di installazione

Utilizza il [Estensione del servizio ID Experience Cloud](/help/tags/extensions/client/id-service/overview.md) per creare un’identità di prima parte univoca basata su dispositivo per i visitatori in tutte le soluzioni Experience Cloud. Cerca **[!UICONTROL Servizio ID]** nel catalogo delle estensioni e installarlo. Mantieni tutte le impostazioni predefinite durante l’installazione dell’estensione.

![Visualizzazione dell&#39;estensione del servizio ID nel catalogo delle estensioni.](/help/rtcdp/assets/partner-data/onsite-personalization/id-service-extension.png)

#### Configurare gli ambienti

Quindi, passa al **[!UICONTROL Ambienti]** dal menu di navigazione a sinistra. In questo passaggio, devi collegare il tuo sito web ad Adobe Edge Network per recuperare e consegnare le informazioni sui visitatori in tempo reale.

Seleziona l’icona della casella a destra per l’ambiente di sviluppo e copia la versione standard dello snippet di codice JavaScript visualizzato in una finestra modale.

![L’icona della casella Seleziona è evidenziata nella sezione Ambienti dell’interfaccia utente di Data Collection.](/help/rtcdp/assets/partner-data/onsite-personalization/select-box-icon.png)

Devi aggiungere questo frammento di codice nella parte superiore del sito web. Di conseguenza, il sito web effettuerà una chiamata alla rete Adobe Edge per recuperare la logica JavaScript che verrà caricata ed eseguita sulla pagina. Questo consente il funzionamento di funzionalità quali la generazione di ID visitatore, la raccolta di dati e la personalizzazione delle esperienze in tempo reale.

#### Impostare gli elementi dati

Gli elementi dati sono i blocchi costitutivi per il dizionario dati (o mappa dati). Un singolo elemento dati è una variabile il cui valore può essere mappato alle stringhe di query, agli URL, ai valori dei cookie, alle variabili JavaScript e così via. Ulteriori informazioni su [elementi dati](/help/tags/ui/managing-resources/data-elements.md).

Ai fini di questo caso d’uso, devi impostare due elementi dati.

Innanzitutto, imposta una `partnerData` elemento. Accedi a **[!UICONTROL Elementi dati]** sezione e seleziona **[!UICONTROL Creare un nuovo elemento dati]**.

![Crea un nuovo elemento dati.](/help/rtcdp/assets/partner-data/onsite-personalization/create-data-element.gif)

Denomina l’elemento dati `partnerData`, lascia il [!UICONTROL estensione] valore come [!UICONTROL Core], e impostare **[!UICONTROL Tipo di elemento dati]** as **[!UICONTROL Variabile JavaScript]**. Invio `partnerData` nel campo con titolo **[!UICONTROL Nome variabile JavaScript]** e seleziona **[!UICONTROL Salva]**.

![Sono state evidenziate le selezioni per configurare correttamente l’elemento dati partnerData.](/help/rtcdp/assets/partner-data/onsite-personalization/create-partnerdata-data-element.png)

Per impostare il secondo elemento dati, assegna un nome alla nuova variabile `pageVisit`, imposta **[!UICONTROL Estensione]** a **[!UICONTROL Adobe Experience Platform]** e scegli **[!UICONTROL Oggetto XDM]** come tipo di dati.

![Sono state evidenziate le selezioni per configurare correttamente l’elemento dati pageVisit.](/help/rtcdp/assets/partner-data/onsite-personalization/page-visit-data-element.png)

Dallo schema, seleziona gli attributi di terze parti corrispondenti ai valori previsti per il partner dati. Quindi, seleziona il pulsante di opzione con titolo **[!UICONTROL Fornisci l&#39;intero oggetto]**. Selezionare l&#39;icona dell&#39;aspetto di un database e scegliere `partnerData` elemento dati creato in precedenza.

#### Impostare le regole

In **[!UICONTROL Regole]** sezione, puoi configurare il sito web per inviare una richiesta di personalizzazione ad Adobe con gli attributi caricati negli elementi dati appena creati. Ulteriori informazioni su [creazione di regole](/help/tags/ui/managing-resources/rules.md).

Seleziona **[!UICONTROL Crea nuova regola]**. Denomina questa regola **[!UICONTROL Personalizzazione]** e seleziona il segno + accanto a **[!UICONTROL Eventi]**. Seleziona **[!UICONTROL Page Bottom]** come evento e salva.

![Selezioni per la parte del tipo di evento di una regola.](/help/rtcdp/assets/partner-data/onsite-personalization/add-events-rule.png)

Seleziona il segno + accanto a **[!UICONTROL Azioni]**. Aggiornare l’estensione a **[!UICONTROL Adobe Experience Platform Web SDK]** e imposta **[!UICONTROL Tipo di azione]** a **[!UICONTROL Invia evento]**.

![Selezioni per la parte del tipo di azione di una regola.](/help/rtcdp/assets/partner-data/onsite-personalization/add-action-rule.png)

Dalla sezione **[!UICONTROL Tipo]** a discesa a destra, seleziona `web.webpagedetails.pageViews` come tipo di evento.

![Seleziona il tipo di evento.](/help/rtcdp/assets/partner-data/onsite-personalization/add-pageview-type-rule.png)

Fai clic sull’icona del database accanto ai dati XDM e seleziona la `pageVisit` elemento dati.

Scorri verso il basso l’elenco delle configurazioni di azioni e accertati di selezionare la casella con titolo **[!UICONTROL Eseguire il rendering delle decisioni di personalizzazione visiva]**. Questo è importante per consentire alle esperienze consegnate tramite Adobe Target o altri prodotti simili di essere visualizzate visivamente sulla pagina web. Seleziona **[!UICONTROL Mantieni modifiche]**, e quindi **[!UICONTROL Salva]** la regola.

![Seleziona la casella di controllo Rendering delle decisioni di personalizzazione visiva.](/help/rtcdp/assets/partner-data/onsite-personalization/render-visual-personalization-toggle.png)

#### Configurare il flusso di lavoro di pubblicazione

Per distribuire questa configurazione alla pagina web, il passaggio successivo consiste nel creare una libreria che includa le risorse appena create. Ulteriori informazioni su [impostazione di un flusso di pubblicazione](/help/tags/ui/publishing/publishing-flow.md).

Seleziona **[!UICONTROL Flusso di pubblicazione]** e poi **[!UICONTROL Aggiungi libreria]**.

Seleziona **[!UICONTROL Aggiungi tutte le risorse modificate]**, assegna un nome alla libreria, imposta l’ambiente su **[!UICONTROL Sviluppo]** e seleziona **[!UICONTROL Salva e genera in sviluppo]**.

![Creare una libreria e distribuirla nell’ambiente di sviluppo](/help/rtcdp/assets/partner-data/onsite-personalization/create-publishing-workflow.gif)

#### Verifica il sito web

A questo punto, il sito web deve essere dotato di strumenti completi con Web SDK. Per verificare che la raccolta dati funzioni come previsto, puoi accedere al tuo sito web e utilizzare gli strumenti di sviluppo del browser per controllare il traffico di rete.

Input `interact` nella casella di ricerca, aggiorna la pagina e dovresti vedere le chiamate di rete dal sito web alla rete Adobe Edge che si sta popolando.

![Visualizzazione degli eventi di rete popolati negli strumenti per sviluppatori.](/help/rtcdp/assets/partner-data/onsite-personalization/events-filtered.png)

### Personalizzazione {#personalization}

Ora puoi creare e attivare tipi di pubblico per la personalizzazione.

#### Impostare la segmentazione Edge

Configurazione [segmentazione Edge](/help/segmentation/ui/edge-segmentation.md) in questo modo l’appartenenza del pubblico dei visitatori viene valutata in tempo reale, quando visitano la tua proprietà web.

Assicurati anche di impostare un [criterio di unione attivo-su-spigolo](/help/destinations/ui/activate-edge-personalization-destinations.md#create-merge-policy) per i tipi di pubblico edge.

#### Integrare con Adobe Target o un’altra destinazione di personalizzazione personalizzata

Ora puoi effettuare l’integrazione con un motore di personalizzazione per visualizzare contenuti personalizzati ai visitatori del tuo sito web o dell’app. L’Adobe consiglia di utilizzare [Destinazione Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) a tal fine.

>[!IMPORTANT]
>
>Leggi l’esercitazione su [attivazione di tipi di pubblico per destinazioni di personalizzazione edge](/help/destinations/ui/activate-edge-personalization-destinations.md) per una visualizzazione completa dei passaggi necessari per attivare i tipi di pubblico.

## Limitazioni e risoluzione dei problemi {#limitations-and-troubleshooting}

Durante l’esplorazione del caso d’uso descritto in questa pagina, tieni presente le seguenti limitazioni:

* Se utilizzi gli ID partner, tieni presente che non vengono utilizzati durante la creazione [grafo delle identità](/help/identity-service/ui/identity-graph-viewer.md).

## Altri casi d’uso ottenuti tramite il supporto dei dati dei partner {#other-use-cases}

Esplora altri casi d’uso abilitati tramite il supporto dei dati dei partner in Real-Time CDP:

* [Puoi integrare i profili di prime parti con attributi di partner di dati affidabili, per migliorare la base di dati, acquisire nuove informazioni sulla base dei clienti e una migliore ottimizzazione del pubblico.](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
* Utilizzare il supporto dati di terze parti in Real-Time CDP per [espandi la base di profili con i profili prospect dei partner dati e interagisci con loro per acquisire o raggiungere nuovi clienti](/help/rtcdp/partner-data/prospecting.md).
* (**Disponibile a breve**) [!BADGE Beta]{type=Informative}**Attivazione estesa** che utilizza gli ID partner per pubblicare ecosistemi che non accettano PII o PII con hash.