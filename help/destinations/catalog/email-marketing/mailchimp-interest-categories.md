---
title: Categorie di interesse Mailchimp
description: Mailchimp (noto anche come Intuit Mailchimp) è un popolare piattaforma di automazione del marketing e servizio di e-mail marketing utilizzato dalle aziende per gestire e parlare con i contatti (clienti, clienti o altre parti interessate) utilizzando mailing list e campagne di e-mail marketing. Utilizza questo connettore per ordinare i contatti in base ai loro interessi e preferenze.
last-substantial-update: 2023-05-24T00:00:00Z
exl-id: bdce8295-7305-4d54-81c1-7fa3e580ce70
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '2299'
ht-degree: 2%

---

# Connessione [!DNL Mailchimp Interest Categories]

[[!DNL Mailchimp]](https://mailchimp.com) è una piattaforma di automazione del marketing e un servizio di marketing via e-mail utilizzato dalle aziende per gestire e comunicare con i contatti *(clienti, clienti o altre parti interessate)* tramite mailing list e campagne di marketing via e-mail. Utilizza questo connettore per ordinare i contatti in base ai loro interessi e preferenze.

[!DNL Mailchimp Interest Categories] utilizza [tipi di pubblico](https://mailchimp.com/help/getting-started-audience/), [gruppi](https://mailchimp.com/help/getting-started-with-groups/) e categorie di interesse *(noti anche come nomi di gruppi o titoli di gruppi)*. Ogni gruppo [!DNL Mailchimp] è un elenco di categorie di interesse. I contatti sono associati a una categoria di interesse quando si sottoscrivono una o più categorie di interesse tramite un modulo di iscrizione sul sito Web. All’interno di un pubblico, puoi anche organizzare i contatti in gruppi e associarli a categorie di interesse, che possono quindi essere utilizzate per creare segmenti. Puoi utilizzare questi tipi di pubblico per trasmettere e-mail di campagne mirate ai contatti abbonati.

<!--
Compared to [!DNL Mailchimp Tags] which you would use for internal classification, [!DNL Mailchimp Interest Categories] is meant to manage subscriptions to topics of interest that your contacts might be interested in. *Note, Experience Platform also has a connection for [!DNL Mailchimp Tags], you can check it out on the [[!DNL Mailchimp Tags]](/help/destinations/catalog/email-marketing/mailchimp-tags.md) page.*
-->

Questa [!DNL Adobe Experience Platform] [destinazione](/help/destinations/home.md) utilizza l&#39;API [[!DNL Mailchimp batch subscribe or unsubscribe API]](https://mailchimp.com/developer/marketing/api/lists/batch-subscribe-or-unsubscribe/) per creare [categorie di interesse](https://mailchimp.com/developer/marketing/api/interest-categories/) e quindi aggiungere i contatti di ciascuno dei tipi di pubblico di Platform selezionati in una categoria di interesse corrispondente. È possibile **aggiungere nuovi contatti** o **aggiornare le informazioni di [!DNL Mailchimp] contatti esistenti**, quindi **aggiungerli o rimuoverli dai gruppi desiderati** all&#39;interno di un pubblico [!DNL Mailchimp] esistente dopo averli attivati all&#39;interno di un nuovo segmento. [!DNL Mailchimp Interest Groups] utilizza i nomi del pubblico selezionati da Platform come categorie di interesse in [!DNL Mailchimp].

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare la destinazione [!DNL Mailchimp Interest Categories], ecco un esempio di caso d&#39;uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Invia e-mail ai contatti per campagne di marketing {#use-case-send-emails}

Il reparto vendite di un sito Web di articoli sportivi vuole trasmettere una campagna di marketing via e-mail a un elenco di contatti che si sono identificati come interessati al calcio. Gli elenchi dei contatti sono separati come batch nell’esportazione dei dati ricevuti dal team di sviluppo del sito web e devono quindi essere tracciati. Il team identifica un pubblico [!DNL Mailchimp] esistente e inizia a creare i tipi di pubblico Experienci Platform in cui vengono aggiunti i contatti di ogni elenco. Dopo aver inviato questi tipi di pubblico a [!DNL Mailchimp Interest Categories], se non esistono contatti nel pubblico [!DNL Mailchimp] selezionato, questi vengono aggiunti a un gruppo con il nome del pubblico a cui appartiene il contatto. Se esistono già contatti nel pubblico o nel gruppo [!DNL Mailchimp], le relative informazioni vengono aggiornate. Una volta inviati i dati a [!DNL Mailchimp Interest Categories], il team vendite può selezionare e inviare l&#39;e-mail della campagna di marketing al gruppo di interesse di calcio all&#39;interno del pubblico [!DNL Mailchimp].

## Prerequisiti {#prerequisites}

Consultare le sezioni seguenti per eventuali prerequisiti da impostare in Experience Platform e [!DNL Mailchimp] e per informazioni da raccogliere prima di utilizzare la destinazione [!DNL Mailchimp Interest Categories].

### Prerequisiti in Experience Platform {#prerequisites-in-experience-platform}

Prima di attivare i dati nella destinazione [!DNL Mailchimp Interest Categories], è necessario disporre di uno [schema](/help/xdm/schema/composition.md), un [set di dati](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) e [segmenti](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) creati in [!DNL Experience Platform].

### Prerequisiti per la destinazione [!DNL Mailchimp Interest Categories] {#prerequisites-destination}

Per esportare i dati da Platform al tuo account [!DNL Mailchimp], tieni presente i seguenti prerequisiti:

#### Devi avere un account [!DNL Mailchimp] {#prerequisites-account}

Prima di poter creare una destinazione [!DNL Mailchimp Interest Categories], è necessario assicurarsi di disporre di un account [!DNL Mailchimp]. Se non ne hai già una, visita la [[!DNL Mailchimp] pagina di iscrizione](https://login.mailchimp.com/signup/) per registrarti e creare il tuo account.

#### Raccogli la chiave API [!DNL Mailchimp] {#gather-credentials}

È necessaria la [!DNL Mailchimp] **chiave API** per autenticare la destinazione [!DNL Mailchimp Interest Categories] in base all&#39;account [!DNL Mailchimp]. La **chiave API** funge da **password** quando [autentichi la destinazione](#authenticate).

Se non disponi della tua **chiave API**, accedi al tuo account e fai riferimento alla [[!DNL Mailchimp] documentazione di generazione della chiave API](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key) per crearne una.

Esempio di chiave API: `0123456789abcdef0123456789abcde-us14`.

>[!IMPORTANT]
>
>Se generi la **chiave API**, annotala in quanto non potrai più accedervi dopo la generazione.

#### Identificare il data center [!DNL Mailchimp] {#identify-data-center}

Successivamente, è necessario identificare il data center [!DNL Mailchimp]. Per eseguire questa operazione, accedere all&#39;account [!DNL Mailchimp] e passare alla **sezione delle chiavi API** dell&#39;account.

Il valore è la prima parte dell’URL visualizzato nel browser. Se l&#39;URL è *https://`us14`.mailchimp.com/account/api/*, il datacenter è `us14`.

È inoltre aggiunto alla chiave API nel formato *key-dc*; se la chiave API è `0123456789abcdef0123456789abcde-us14`, il datacenter è `us14`.

Annotare il valore del datacenter *(`us14` in questo esempio)*, è necessario questo valore quando si [compilano i dettagli della destinazione](#destination-details).

Per ulteriori informazioni, consulta la [[!DNL Mailchimp] documentazione di base](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-structure).

### Guardrail {#guardrails}

Ciascuno dei tipi di pubblico di [!DNL Mailchimp] può contenere fino a 60 nomi di gruppo (o categorie di interesse) in un singolo gruppo o in più gruppi all&#39;interno dello stesso pubblico. Per eventuali chiarimenti richiesti, consulta [!DNL Mailchimp] [gruppi](https://mailchimp.com/help/getting-started-with-groups/). Quando si raggiunge questo limite, viene visualizzato un messaggio di errore `400 BAD_REQUEST Cannot have more than 60 interests per list (Across all categories)` dall&#39;API [!DNL Mailchimp].

Per informazioni dettagliate sui limiti imposti dall&#39;API [!DNL Mailchimp], consultare inoltre [!DNL Mailchimp] [limiti di tariffa](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-limits).

## Identità supportate {#supported-identities}

[!DNL Mailchimp] supporta l&#39;attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| E-mail | Indirizzo e-mail di contatto | Obbligatorio |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | <ul><li>Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati *(ad esempio: indirizzo e-mail, numero di telefono, cognome)*, in base al mapping dei campi.</li><li> Per ogni pubblico selezionato in Platform, lo stato del segmento [!DNL Mailchimp Interest Categories] corrispondente viene aggiornato da Platform in base allo stato del pubblico.</li></ul> |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Quando un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
>
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

In **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]**, cerca [!DNL Mailchimp Interest Categories]. In alternativa, puoi trovarlo nella categoria **[!UICONTROL E-mail marketing]**.

### Autenticarsi nella destinazione {#authenticate}

Per eseguire l&#39;autenticazione nella destinazione, compilare i campi obbligatori e selezionare **[!UICONTROL Connetti alla destinazione]**.

| Campo | Descrizione |
| --- | --- |
| **[!UICONTROL Nome utente]** | Nome utente [!DNL Mailchimp Interest Categories]. |
| **[!UICONTROL Password]** | La [!DNL Mailchimp] **chiave API**, annotata nella sezione [Raccogli [!DNL Mailchimp] credenziali](#gather-credentials).<br> La chiave API assume la forma di `{KEY}-{DC}`, dove la parte `{KEY}` fa riferimento al valore annotato nella sezione [[!DNL Mailchimp] Chiave API](#gather-credentials) e la parte `{DC}` fa riferimento al [[!DNL Mailchimp] datacenter](#identify-data-center). <br>È possibile fornire la porzione `{KEY}` o l&#39;intero modulo.<br> Ad esempio, se la chiave API è <br>*`0123456789abcdef0123456789abcde-us14`*,<br> puoi fornire *`0123456789abcdef0123456789abcde`*o *`0123456789abcdef0123456789abcde-us14`*come valore. |

{style="table-layout:auto"}

![Schermata dell&#39;interfaccia utente di Platform che mostra come eseguire l&#39;autenticazione.](../../assets/catalog/email-marketing/mailchimp-interest-categories/authenticate-destination.png)

Se i dettagli forniti sono validi, nell&#39;interfaccia utente viene visualizzato lo stato **[!UICONTROL Connesso]** con un segno di spunta verde. A questo punto è possibile procedere al passaggio successivo.

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

![Schermata dell&#39;interfaccia utente di Platform che mostra i dettagli della destinazione.](../../assets/catalog/email-marketing/mailchimp-interest-categories/destination-details.png)

| Campo | Descrizione |
| --- | --- |
| **[!UICONTROL Nome]** | Un nome con cui riconoscerai questa destinazione in futuro. |
| **[!UICONTROL Descrizione]** | Una descrizione che ti aiuterà a identificare questa destinazione in futuro. |
| **[!UICONTROL Data center]** | Il tuo account [!DNL Mailchimp] `data center`. Per ulteriori informazioni, consulta la sezione [Identificare [!DNL Mailchimp] il centro dati](#identify-data-center). |
| **[!UICONTROL Nome pubblico (selezionare prima il centro dati)]** | Dopo aver selezionato il **[!UICONTROL centro dati]**, questo menu a discesa viene compilato automaticamente con i nomi del pubblico del tuo account [!DNL Mailchimp]. Seleziona il pubblico da aggiornare con i dati di Platform. |
| **[!UICONTROL Categoria di interesse (selezionare prima il centro dati e il nome del pubblico)]** | Dopo aver selezionato **[!UICONTROL Nome pubblico]**, questo menu a discesa viene compilato automaticamente con i nomi delle categorie dei gruppi di interesse dell&#39;account [!DNL Mailchimp]. Seleziona il nome della categoria da aggiornare con i dati di Platform. |

{style="table-layout:auto"}

>[!TIP]
>
> Se la chiave API fornita nel campo **[!UICONTROL Password]** o il valore **[!UICONTROL Data center]** non sono corretti, l&#39;interfaccia utente visualizza una risposta di errore API [!DNL Mailchimp]: *`No options are available. Please verify the values selected for the following dependent fields: dataCenter`* come illustrato di seguito. In questo caso, non puoi selezionare un valore dal campo **[!UICONTROL Nome pubblico (seleziona prima il centro dati)]**. Per correggere questo errore, specifica i valori corretti.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Leggi [Attivare profili e tipi di pubblico nelle destinazioni di esportazione del pubblico di streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per le istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione.

### Considerazioni sulla mappatura ed esempio {#mapping-considerations-example}

Per inviare correttamente i dati sul pubblico da Adobe Experience Platform alla destinazione [!DNL Mailchimp Interest Categories], è necessario eseguire il passaggio di mappatura dei campi. La mappatura consiste nella creazione di un collegamento tra i campi dello schema Experience Data Model (XDM) nell’account Platform e i corrispondenti equivalenti dalla destinazione.

Per mappare correttamente i campi XDM ai campi di destinazione [!DNL Mailchimp Interest Categories], effettua le seguenti operazioni:

1. Nel passaggio **[!UICONTROL Mapping]**, seleziona **[!UICONTROL Aggiungi nuovo mapping]**. Ora è possibile visualizzare una nuova riga di mappatura sullo schermo.
1. Nella finestra **[!UICONTROL Seleziona campo di origine]**, scegli la categoria **[!UICONTROL Seleziona attributi]** e seleziona l&#39;attributo XDM oppure scegli lo spazio dei nomi **[!UICONTROL Seleziona identità]** e seleziona un&#39;identità.
1. Nella finestra **[!UICONTROL Seleziona campo di destinazione]**, scegli **[!UICONTROL Seleziona spazio dei nomi identità]** e seleziona un&#39;identità oppure scegli **[!UICONTROL Seleziona attributi]** categoria e seleziona dall&#39;elenco di attributi popolati dall&#39;API [!DNL Mailchimp]. *Tutti gli attributi personalizzati aggiunti al pubblico [!DNL Mailchimp] selezionato saranno disponibili per la selezione come campi di destinazione.*

   Di seguito sono indicate le mappature disponibili tra lo schema del profilo XDM e [!DNL Mailchimp Interest Categories]:
| Campo Source | Campo di destinazione | Note |
| — | — | — |
|`IdentityMap: Email`|`Identity: email`| Obbligatorio: sì |
|`xdm: person.name.firstName`|`Attribute: FNAME`| |
|`xdm: person.name.lastName`|`Attribute: LNAME`| |
|`xdm: person.birthDayAndMonth`|`Attribute: BIRTHDAY`| |

   Inoltre, `ADDRESS` è un campo di destinazione speciale noto come `merge field` all&#39;interno del tuo pubblico [!DNL Mailchimp]. La [[!DNL Mailchimp] documentazione](https://mailchimp.com/developer/marketing/docs/merge-fields/) definisce le chiavi richieste come `addr1`, `city`, `state` e `zip` e le chiavi facoltative `addr2` e `country`. I valori per questi campi devono essere stringhe. Se è presente uno dei mapping di campi `ADDRESS`, la destinazione passa l&#39;oggetto `ADDRESS` all&#39;API [!DNL Mailchimp] per l&#39;aggiornamento. Il valore predefinito di qualsiasi campo `ADDRESS` non mappato è `NULL`, ad eccezione del paese che utilizza `US` come impostazione predefinita.

   Le mappature disponibili per il campo `ADDRESS` sono le seguenti:

   | Campo origine | Campo di destinazione |
   | --- | --- |
   | `xdm: workAddress.street1` | `Attribute: ADDRESS.addr1` |
   | `xdm: workAddress.street2` | `Attribute: ADDRESS.addr2` |
   | `xdm: workAddress.city` | `Attribute: ADDRESS.city` |
   | `xdm: workAddress.state` | `Attribute: ADDRESS.state` |
   | `xdm: workAddress.postalCode` | `Attribute: ADDRESS.zip` |
   | `xdm: workAddress.country` | `Attribute: ADDRESS.country` |

   Ad esempio, si desidera aggiornare il valore per `country` con i valori del campo indirizzo esistente del contatto `addr1`, `city`, `state` e `zip` come `132, My Street, Kingston`, `New York`, `New York` e `12401`. Per aggiornare `country` è necessario passare i valori esistenti con le modifiche *(se presenti)* e il nuovo valore per paese. I valori nel set di dati devono essere `132, My Street, Kingston`, `New York`, `New York`, `12401` e `US`. Per ripetere, se passi solo `country` e non fornisci valori per `addr1`, `city`, `state` e `zip`, verranno sovrascritti da `NULL`.

   Di seguito è riportato un esempio con le mappature completate:
   ![Esempio di schermata dell&#39;interfaccia utente di Platform che mostra le mappature dei campi.](../../assets/catalog/email-marketing/mailchimp-interest-categories/mappings.png)

Dopo aver fornito le mappature per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Convalidare l’esportazione dei dati {#exported-data}

Per verificare di aver impostato correttamente la destinazione, segui i passaggi seguenti:

* Accedi al tuo account [[!DNL Mailchimp]](https://login.mailchimp.com/). Passare quindi alla pagina **[!DNL Audience]**. Espandere il menu **[!DNL Manage Contacts]** e selezionare **[!DNL Groups]**.

![Schermata dell&#39;interfaccia utente Mailchimp che mostra la pagina del gruppo di tipi di pubblico.](../../assets/catalog/email-marketing/mailchimp-interest-categories/audience-groups.png)

* Seleziona il Gruppo e controlla se i tipi di pubblico selezionati sono creati come categorie con il nome del pubblico di Platform, che può essere seguito da un suffisso generato automaticamente.
   * Questa destinazione utilizza i nomi dei segmenti selezionati per creare la categoria di interesse utilizzando l&#39;[[!DNL Mailchimp] Aggiungi API categoria di interesse](https://mailchimp.com/developer/marketing/api/interest-categories/add-interest-category/). Se crei una nuova destinazione e attivi di nuovo gli stessi tipi di pubblico, [!DNL Mailchimp] aggiunge un suffisso per distinguere i segmenti esistenti da quelli nuovi.
* I contatti le cui e-mail non esistevano nel gruppo vengono aggiunti alla categoria appena creata.
* Per i contatti già presenti nel gruppo, i dati del campo attributo vengono aggiornati e il contatto viene aggiunto alla categoria appena creata.

![Schermata dell&#39;interfaccia utente di Mailchimp che mostra le categorie del gruppo di pubblico.](../../assets/catalog/email-marketing/mailchimp-interest-categories/audience-groups-category.png)

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Errori e risoluzione problemi {#errors-and-troubleshooting}

### Errore riscontrato se la chiave API [!DNL Mailchimp] o i valori del centro dati non sono corretti {#incorrect-credentials-error}

Se la chiave API fornita nel campo **[!UICONTROL Password]** o il valore **[!UICONTROL Data center]** non sono corretti, l&#39;interfaccia utente visualizza una risposta di errore API [!DNL Mailchimp]: *`No options are available. Please verify the values selected for the following dependent fields: dataCenter`* come illustrato di seguito. In questo caso, non è possibile selezionare un valore dal campo **[!UICONTROL Nome pubblico (selezionare prima il centro dati)]**.

![Schermata dell&#39;interfaccia utente di Platform che mostra un errore se la chiave API Mailchimp o i valori del centro dati non sono corretti.](../../assets/catalog/email-marketing/mailchimp-interest-categories/error.png)

Per correggere questo errore e procedere al passaggio successivo, è necessario fornire i valori corretti. Consulta [Identificare [!DNL Mailchimp] il centro dati](#identify-data-center) e
[Raccogli [!DNL Mailchimp] le sezioni della chiave API](#gather-credentials) se hai bisogno di assistenza.

### Errore riscontrato se viene superato il limite di nomi di gruppo [!DNL Mailchimp] {#group-name-limits-error}

Durante la creazione della destinazione, è possibile che vengano visualizzati i seguenti messaggi di errore: *`Cannot have more than 60 interests per list (Across all categories)`* o *`400 BAD_REQUEST`*. Ciò si verifica quando si superano i 60 nomi di gruppo (o categorie di interesse) in un singolo gruppo o in più gruppi all&#39;interno dello stesso limite di pubblico, come descritto nella sezione [guardrail](#guardrails). Per correggere questo errore, assicurarsi di non superare il limite di nomi di gruppo in [!DNL Mailchimp].

### [!DNL Mailchimp] codici di stato ed errore

Per un elenco completo dei codici di stato e di errore con relative spiegazioni, consultare la [[!DNL Mailchimp] pagina errori](https://mailchimp.com/developer/marketing/docs/errors/).

## Risorse aggiuntive {#additional-resources}

Di seguito sono riportate ulteriori informazioni utili dalla documentazione di [!DNL Mailchimp]:
* [Guida introduttiva a [!DNL Mailchimp]](https://mailchimp.com/help/getting-started-with-mailchimp/)
* [Guida introduttiva ai tipi di pubblico](https://mailchimp.com/help/getting-started-audience/)
* [Crea un pubblico](https://mailchimp.com/help/create-audience/)
* [Guida introduttiva ai gruppi](https://mailchimp.com/help/getting-started-with-groups/)
* [Crea un nuovo gruppo di pubblico](https://mailchimp.com/help/create-new-audience-group/)
* [Categorie di interessi](https://mailchimp.com/developer/marketing/api/interest-categories/)
* [API marketing](https://mailchimp.com/developer/marketing/api/)
