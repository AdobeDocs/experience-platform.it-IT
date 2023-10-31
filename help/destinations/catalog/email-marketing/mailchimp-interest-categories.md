---
title: Categorie di interesse Mailchimp
description: Mailchimp (noto anche come Intuit Mailchimp) è un popolare piattaforma di automazione del marketing e servizio di e-mail marketing utilizzato dalle aziende per gestire e parlare con i contatti (clienti, clienti o altre parti interessate) utilizzando mailing list e campagne di e-mail marketing. Utilizza questo connettore per ordinare i contatti in base ai loro interessi e preferenze.
last-substantial-update: 2023-05-24T00:00:00Z
exl-id: bdce8295-7305-4d54-81c1-7fa3e580ce70
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '2392'
ht-degree: 2%

---

# Connessione [!DNL Mailchimp Interest Categories]

[[!DNL Mailchimp]](https://mailchimp.com) è una piattaforma di automazione del marketing e un servizio di e-mail marketing utilizzato dalle aziende per gestire e comunicare con i contatti *(clienti, clienti o altre parti interessate)* utilizzo di mailing list e campagne di e-mail marketing. Utilizza questo connettore per ordinare i contatti in base ai loro interessi e preferenze.

[!DNL Mailchimp Interest Categories] utilizza [audience](https://mailchimp.com/help/getting-started-audience/), [gruppi](https://mailchimp.com/help/getting-started-with-groups/), e categorie di interesse *(noti anche come nomi di gruppi o titoli di gruppi)*. Ogni [!DNL Mailchimp] gruppo è un elenco di categorie di interesse. I contatti sono associati a una categoria di interesse quando si sottoscrivono una o più categorie di interesse tramite un modulo di iscrizione sul sito Web. All’interno di un pubblico, puoi anche organizzare i contatti in gruppi e associarli a categorie di interesse, che possono quindi essere utilizzate per creare segmenti. Puoi utilizzare questi tipi di pubblico per trasmettere e-mail di campagne mirate ai contatti abbonati.

<!--
Compared to [!DNL Mailchimp Tags] which you would use for internal classification, [!DNL Mailchimp Interest Categories] is meant to manage subscriptions to topics of interest that your contacts might be interested in. *Note, Experience Platform also has a connection for [!DNL Mailchimp Tags], you can check it out on the [[!DNL Mailchimp Tags]](/help/destinations/catalog/email-marketing/mailchimp-tags.md) page.*
-->

Questo [!DNL Adobe Experience Platform] [destinazione](/help/destinations/home.md) utilizza [[!DNL Mailchimp batch subscribe or unsubscribe API]](https://mailchimp.com/developer/marketing/api/lists/batch-subscribe-or-unsubscribe/) API da creare [categorie di interesse](https://mailchimp.com/developer/marketing/api/interest-categories/) e quindi aggiungi i contatti di ciascuno dei tipi di pubblico di Platform selezionati in una categoria di interesse corrispondente. È possibile **aggiungi nuovi contatti** o **aggiorna le informazioni di esistenti [!DNL Mailchimp] contatti**, quindi **aggiungerli o rimuoverli dai gruppi desiderati** all&#39;interno di un [!DNL Mailchimp] dopo averli attivati all’interno di un nuovo segmento. [!DNL Mailchimp Interest Groups] utilizza i nomi del pubblico selezionati da Platform come categorie di interesse in [!DNL Mailchimp].

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare il [!DNL Mailchimp Interest Categories] destinazione: ecco un caso d’uso di esempio che i clienti di Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Invia e-mail ai contatti per campagne di marketing {#use-case-send-emails}

Il reparto vendite di un sito Web di articoli sportivi vuole trasmettere una campagna di marketing via e-mail a un elenco di contatti che si sono identificati come interessati al calcio. Gli elenchi dei contatti sono separati come batch nell’esportazione dei dati ricevuti dal team di sviluppo del sito web e devono quindi essere tracciati. Il team identifica un [!DNL Mailchimp] e inizia a creare i tipi di pubblico Experienci Platform in cui vengono aggiunti i contatti di ogni elenco. Dopo aver inviato questi tipi di pubblico a [!DNL Mailchimp Interest Categories], se non esistono contatti nel [!DNL Mailchimp] audience vengono aggiunti a un gruppo con il nome del pubblico a cui appartiene il contatto. Se esistono già contatti in [!DNL Mailchimp] pubblico o gruppo, le relative informazioni vengono aggiornate. Una volta inviati i dati a [!DNL Mailchimp Interest Categories], il team di vendita può selezionare e inviare l&#39;e-mail della campagna di marketing al gruppo di interesse di calcio all&#39;interno del [!DNL Mailchimp] pubblico.

## Prerequisiti {#prerequisites}

Consulta le sezioni seguenti per eventuali prerequisiti da impostare in Experienci Platform e [!DNL Mailchimp] e per le informazioni che è necessario raccogliere prima di lavorare con [!DNL Mailchimp Interest Categories] destinazione.

### Prerequisiti in Experienci Platform {#prerequisites-in-experience-platform}

Prima di attivare i dati in [!DNL Mailchimp Interest Categories] destinazione, è necessario disporre di un [schema](/help/xdm/schema/composition.md), a [set di dati](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), e [segmenti](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) creato in [!DNL Experience Platform].

### Prerequisiti per [!DNL Mailchimp Interest Categories] destinazione {#prerequisites-destination}

Prendi nota dei seguenti prerequisiti per esportare i dati da Platform al tuo [!DNL Mailchimp] account:

#### È necessario disporre di [!DNL Mailchimp] account {#prerequisites-account}

Prima di creare un [!DNL Mailchimp Interest Categories] destinazione, devi prima assicurarti di disporre di un [!DNL Mailchimp] account. Se non ne hai già uno, visita il [[!DNL Mailchimp] pagina di registrazione](https://login.mailchimp.com/signup/) per registrarti e creare il tuo account.

#### Raccogli [!DNL Mailchimp] Chiave API {#gather-credentials}

Hai bisogno del tuo [!DNL Mailchimp] **Chiave API** per autenticare [!DNL Mailchimp Interest Categories] destinazione rispetto al tuo [!DNL Mailchimp] account. Il **Chiave API** funge da **Password** quando [autentica la destinazione](#authenticate).

Se non si dispone di **Chiave API**, Accedi al tuo account e fai riferimento alla [[!DNL Mailchimp] Generare la chiave API](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key) per crearne una.

Un esempio di chiave API è `0123456789abcdef0123456789abcde-us14`.

>[!IMPORTANT]
>
>Se si genera **Chiave API**, annotalo in quanto non potrai più accedervi dopo la generazione.

#### Identificare [!DNL Mailchimp] data center {#identify-data-center}

Quindi, devi identificare il tuo [!DNL Mailchimp] data center. Per eseguire questa operazione, accedi al tuo [!DNL Mailchimp] account e passare al **Sezione chiavi API** del tuo account.

Il valore è la prima parte dell’URL visualizzato nel browser. Se l’URL è *https://`us14`.mailchimp.com/account/api/*, il centro dati è `us14`.

È anche aggiunto alla chiave API nel modulo *key-dc*; se la chiave API è `0123456789abcdef0123456789abcde-us14`, il centro dati è `us14`.

Annotare il valore del centro dati *(`us14` in questo esempio)*, questo valore è necessario quando [compila i dettagli della destinazione](#destination-details).

Per ulteriori informazioni, consultare [[!DNL Mailchimp] Documentazione di base](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-structure).

### Guardrail {#guardrails}

Ognuno dei [!DNL Mailchimp] i tipi di pubblico possono contenere fino a 60 nomi di gruppo (o categorie di interesse) in un singolo gruppo o in più gruppi all’interno dello stesso pubblico. Fai riferimento a [!DNL Mailchimp] [gruppi](https://mailchimp.com/help/getting-started-with-groups/) per eventuali chiarimenti richiesti. Quando raggiungi questo limite, ottieni un `400 BAD_REQUEST Cannot have more than 60 interests per list (Across all categories)` messaggio come risposta di errore da [!DNL Mailchimp] API.

Inoltre, fai riferimento a [!DNL Mailchimp] [limiti di tariffa](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-limits) per informazioni dettagliate sui limiti imposti dalla [!DNL Mailchimp] API.

## Identità supportate {#supported-identities}

[!DNL Mailchimp] supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| E-mail | Indirizzo e-mail di contatto | Obbligatorio |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | <ul><li>Stai esportando tutti i membri di un segmento, insieme ai campi schema desiderati *ad esempio: indirizzo e-mail, numero di telefono, cognome*, in base alla mappatura del campo.</li><li> Per ogni pubblico selezionato in Platform, la [!DNL Mailchimp Interest Categories] Lo stato del segmento viene aggiornato con il relativo stato del pubblico da Platform.</li></ul> |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Quando un profilo viene aggiornato in Experienci Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni su [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connetti alla destinazione {#connect}

>[!IMPORTANT]
>
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

Entro **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]**, cerca [!DNL Mailchimp Interest Categories]. In alternativa, è possibile posizionarlo sotto il **[!UICONTROL E-mail marketing]** categoria.

### Autentica nella destinazione {#authenticate}

Per eseguire l’autenticazione nella destinazione, compila i campi richiesti di seguito e seleziona **[!UICONTROL Connetti alla destinazione]**.

| Campo | Descrizione |
| --- | --- |
| **[!UICONTROL Nome utente]** | Il tuo [!DNL Mailchimp Interest Categories] nome utente. |
| **[!UICONTROL Password]** | Il tuo [!DNL Mailchimp] **Chiave API**, che hai annotato in [Raccogli [!DNL Mailchimp] credenziali](#gather-credentials) sezione.<br> La chiave API assume la forma di `{KEY}-{DC}`, in cui `{KEY}` porzione si riferisce al valore annotato in basso nel [[!DNL Mailchimp] Chiave API](#gather-credentials) sezione e `{DC}` porzione si riferisce al [[!DNL Mailchimp] data center](#identify-data-center). <br>È possibile specificare `{KEY}` parte o l&#39;intero modulo.<br> Ad esempio, se la chiave API è <br>*`0123456789abcdef0123456789abcde-us14`*,<br> puoi fornire *`0123456789abcdef0123456789abcde`*o *`0123456789abcdef0123456789abcde-us14`*come valore. |

{style="table-layout:auto"}

![Schermata dell’interfaccia utente di Platform che mostra come eseguire l’autenticazione.](../../assets/catalog/email-marketing/mailchimp-interest-categories/authenticate-destination.png)

Se i dettagli forniti sono validi, nell’interfaccia utente viene visualizzato un **[!UICONTROL Connesso]** con un segno di spunta verde. A questo punto è possibile procedere al passaggio successivo.

### Inserisci i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

![Schermata dell’interfaccia utente di Platform che mostra i dettagli della destinazione.](../../assets/catalog/email-marketing/mailchimp-interest-categories/destination-details.png)

| Campo | Descrizione |
| --- | --- |
| **[!UICONTROL Nome]** | Un nome con cui riconoscerai questa destinazione in futuro. |
| **[!UICONTROL Descrizione]** | Una descrizione che ti aiuterà a identificare questa destinazione in futuro. |
| **[!UICONTROL Data center]** | Il tuo [!DNL Mailchimp] account `data center`. Consulta la sezione [Identificare [!DNL Mailchimp] data center](#identify-data-center) sezione per eventuali indicazioni. |
| **[!UICONTROL Nome pubblico (seleziona prima il centro dati)]** | Dopo aver selezionato il **[!UICONTROL Data center]**, questo menu a discesa viene compilato automaticamente con i nomi del pubblico del tuo [!DNL Mailchimp] account. Seleziona il pubblico da aggiornare con i dati di Platform. |
| **[!UICONTROL Categoria di interesse (seleziona prima il centro dati e il nome del pubblico)]** | Dopo aver selezionato il **[!UICONTROL Nome pubblico]**, questo menu a discesa viene compilato automaticamente con i nomi delle categorie dei gruppi di interesse del tuo [!DNL Mailchimp] account. Seleziona il nome della categoria da aggiornare con i dati di Platform. |

{style="table-layout:auto"}

>[!TIP]
>
> Se la chiave API fornita in **[!UICONTROL Password]** o il **[!UICONTROL Data center]** non sono corretti, nell’interfaccia utente viene visualizzato un tag [!DNL Mailchimp] Risposta di errore API: *`No options are available. Please verify the values selected for the following dependent fields: dataCenter`* come mostrato di seguito. In questo caso, non è possibile selezionare un valore dal **[!UICONTROL Nome pubblico (seleziona prima il centro dati)]** campo. Per correggere questo errore, specifica i valori corretti.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva il pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario **[!UICONTROL Visualizza grafico delle identità]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Letto [Attiva profili e tipi di pubblico nelle destinazioni di esportazione del pubblico in streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per istruzioni sull’attivazione dei tipi di pubblico in questa destinazione.

### Considerazioni sulla mappatura ed esempio {#mapping-considerations-example}

Per inviare correttamente i dati sul pubblico da Adobe Experience Platform a [!DNL Mailchimp Interest Categories] destinazione, devi passare attraverso il passaggio di mappatura campo. La mappatura consiste nella creazione di un collegamento tra i campi dello schema Experience Data Model (XDM) nell’account Platform e i corrispondenti equivalenti dalla destinazione.

Per mappare correttamente i campi XDM su [!DNL Mailchimp Interest Categories] campi di destinazione, segui i passaggi seguenti:

1. In **[!UICONTROL Mappatura]** passaggio, seleziona **[!UICONTROL Aggiungi nuova mappatura]**. Ora è possibile visualizzare una nuova riga di mappatura sullo schermo.
1. In **[!UICONTROL Seleziona campo di origine]** finestra, scegli la **[!UICONTROL Seleziona attributi]** e selezionare l&#39;attributo XDM o scegliere il **[!UICONTROL Seleziona lo spazio dei nomi dell’identità]** e seleziona un’identità.
1. In **[!UICONTROL Seleziona campo di destinazione]** finestra, scegli la **[!UICONTROL Seleziona lo spazio dei nomi dell’identità]** e seleziona un’identità o scegli **[!UICONTROL Seleziona attributi]** e selezionarli dall&#39;elenco di attributi compilato dalla [!DNL Mailchimp] API. *Tutti gli attributi personalizzati aggiunti al [!DNL Mailchimp] Il pubblico sarà disponibile anche per la selezione come campi di destinazione.*

   Le mappature disponibili tra lo schema del profilo XDM e [!DNL Mailchimp Interest Categories] sono i seguenti: | Campo di origine | Campo di destinazione | Note | | — | — | — | |`IdentityMap: Email`|`Identity: email`| Obbligatorio: Sì | |`xdm: person.name.firstName`|`Attribute: FNAME`| | |`xdm: person.name.lastName`|`Attribute: LNAME`| | |`xdm: person.birthDayAndMonth`|`Attribute: BIRTHDAY`| |

   Inoltre, `ADDRESS` è un campo di destinazione speciale noto come `merge field` all&#39;interno del [!DNL Mailchimp] pubblico. Il [[!DNL Mailchimp] documentazione](https://mailchimp.com/developer/marketing/docs/merge-fields/) definisce le chiavi richieste come `addr1`, `city`, `state`, e `zip`, e i tasti opzionali `addr2` e `country`. I valori per questi campi devono essere stringhe. Se una delle `ADDRESS` sono presenti mappature di campo, la destinazione passa il `ADDRESS` oggetto al [!DNL Mailchimp] API per l’aggiornamento. Qualsiasi `ADDRESS` il valore predefinito dei campi non mappati è `NULL` ad eccezione del paese il cui valore predefinito è `US`.

   Le mappature disponibili per `ADDRESS` sono i seguenti:

   | Campo di origine | Campo di destinazione |
   | --- | --- |
   | `xdm: workAddress.street1` | `Attribute: ADDRESS.addr1` |
   | `xdm: workAddress.street2` | `Attribute: ADDRESS.addr2` |
   | `xdm: workAddress.city` | `Attribute: ADDRESS.city` |
   | `xdm: workAddress.state` | `Attribute: ADDRESS.state` |
   | `xdm: workAddress.postalCode` | `Attribute: ADDRESS.zip` |
   | `xdm: workAddress.country` | `Attribute: ADDRESS.country` |

   Ad esempio, desideri aggiornare il valore per `country` con il campo indirizzo esistente del contatto `addr1`, `city`, `state`, e `zip` valori come `132, My Street, Kingston`, `New York`, `New York` e `12401`. Per aggiornare `country` è necessario trasmettere i valori esistenti con le modifiche *(se presente)* e il nuovo valore per il paese. Pertanto, i valori nel set di dati dovrebbero essere `132, My Street, Kingston`, `New York`, `New York`, `12401`, e `US`. Per ripetere, se si passa solo `country` e non forniscono valori per `addr1`, `city`, `state`, e `zip` verranno sovrascritti da `NULL`.

   Di seguito è riportato un esempio con le mappature completate:
   ![Esempio di schermata dell’interfaccia utente di Platform che mostra le mappature dei campi.](../../assets/catalog/email-marketing/mailchimp-interest-categories/mappings.png)

Una volta completate le mappature per la connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Convalidare l’esportazione dei dati {#exported-data}

Per verificare di aver impostato correttamente la destinazione, segui i passaggi seguenti:

* Accedi al tuo [[!DNL Mailchimp]](https://login.mailchimp.com/) account. Quindi, passa alla **[!DNL Audience]** pagina. Quindi, espandi **[!DNL Manage Contacts]** menu e seleziona **[!DNL Groups]**.

![Schermata dell’interfaccia utente Mailchimp che mostra la pagina Gruppo di pubblico.](../../assets/catalog/email-marketing/mailchimp-interest-categories/audience-groups.png)

* Seleziona il Gruppo e controlla se i tipi di pubblico selezionati sono creati come categorie con il nome del pubblico di Platform, che può essere seguito da un suffisso generato automaticamente.
   * Questa destinazione utilizza i nomi dei segmenti selezionati per creare la categoria di interessi utilizzando [[!DNL Mailchimp] Aggiungi API per categoria di interessi](https://mailchimp.com/developer/marketing/api/interest-categories/add-interest-category/). Se crei una nuova destinazione e attivi di nuovo gli stessi tipi di pubblico, [!DNL Mailchimp] aggiunge un suffisso per distinguere tra i segmenti esistenti e quelli nuovi.
* I contatti le cui e-mail non esistevano nel gruppo vengono aggiunti alla categoria appena creata.
* Per i contatti già presenti nel gruppo, i dati del campo attributo vengono aggiornati e il contatto viene aggiunto alla categoria appena creata.

![Schermata dell’interfaccia utente di Mailchimp che mostra le categorie del gruppo di pubblico.](../../assets/catalog/email-marketing/mailchimp-interest-categories/audience-groups-category.png)

## Utilizzo dei dati e governance {#data-usage-governance}

Tutti [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, consulta la sezione [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Errori e risoluzione problemi {#errors-and-troubleshooting}

### Errore riscontrato se [!DNL Mailchimp] I valori della chiave API o del centro dati non sono corretti {#incorrect-credentials-error}

Se la chiave API fornita in **[!UICONTROL Password]** o il **[!UICONTROL Data center]** non sono corretti, nell’interfaccia utente viene visualizzato un tag [!DNL Mailchimp] Risposta di errore API: *`No options are available. Please verify the values selected for the following dependent fields: dataCenter`* come mostrato di seguito. In questo caso, non è possibile selezionare un valore dal **[!UICONTROL Nome pubblico (seleziona prima il centro dati)]** campo.

![Schermata dell’interfaccia utente di Platform che mostra l’errore se la chiave API Mailchimp o i valori del centro dati non sono corretti.](../../assets/catalog/email-marketing/mailchimp-interest-categories/error.png)

Per correggere questo errore e procedere al passaggio successivo, è necessario fornire i valori corretti. Consulta la sezione [Identificare [!DNL Mailchimp] data center](#identify-data-center) e
[Raccogli [!DNL Mailchimp] Chiave API](#gather-credentials) sezioni in caso di necessità di assistenza.

### Errore riscontrato se [!DNL Mailchimp] è stato superato il limite di nomi di gruppo {#group-name-limits-error}

Quando crei la destinazione, potresti ricevere i seguenti messaggi di errore: *`Cannot have more than 60 interests per list (Across all categories)`* o *`400 BAD_REQUEST`*. Ciò si verifica quando si superano i 60 nomi di gruppo (o categorie di interesse) in un singolo gruppo o in più gruppi all&#39;interno dello stesso limite di pubblico, come descritto in [guardrail](#guardrails) sezione. Per correggere questo errore, assicurati di non superare il limite del nome del gruppo in [!DNL Mailchimp].

### [!DNL Mailchimp] Codici di stato ed errore

Consulta la sezione [[!DNL Mailchimp] pagina errori](https://mailchimp.com/developer/marketing/docs/errors/) per un elenco completo dei codici di stato e di errore, con relative spiegazioni.

## Risorse aggiuntive {#additional-resources}

Ulteriori informazioni utili da [!DNL Mailchimp] la documentazione è riportata di seguito:
* [Guida introduttiva a [!DNL Mailchimp]](https://mailchimp.com/help/getting-started-with-mailchimp/)
* [Guida introduttiva a Audiences](https://mailchimp.com/help/getting-started-audience/)
* [Creare un pubblico](https://mailchimp.com/help/create-audience/)
* [Guida introduttiva ai gruppi](https://mailchimp.com/help/getting-started-with-groups/)
* [Crea un nuovo gruppo di pubblico](https://mailchimp.com/help/create-new-audience-group/)
* [Categorie di interesse](https://mailchimp.com/developer/marketing/api/interest-categories/)
* [API di marketing](https://mailchimp.com/developer/marketing/api/)
