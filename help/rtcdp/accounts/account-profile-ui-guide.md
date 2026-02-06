---
keywords: profilo rtcdp;profili rtcdp;rtcdp identità;criteri di unione rtcdp;real-time customer profile
title: Guida dell’interfaccia utente del profilo account
description: Tramite l’utilizzo dei profili dell’account, Adobe Real-Time Customer Data Platform B2B edition consente di unificare le informazioni sull’account da più origini. Questa guida fornisce dettagli per interagire con i profili dell’account nell’interfaccia utente di Adobe Experience Platform.
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html#rtcdp-editions" newtab=true
feature: Profiles, B2B
exl-id: a05e8b84-026e-4482-a288-aa25b441bd69
source-git-commit: 5998adf98aa7250864983d7e4e629921633e1a1c
workflow-type: tm+mt
source-wordcount: '1608'
ht-degree: 0%

---

# Guida dell’interfaccia utente del profilo account

>[!NOTE]
>
>I profili dell’account sono disponibili solo per i clienti di Real-Time Customer Data Platform B2B edition. Per ulteriori informazioni su Real-Time CDP, incluse le funzionalità disponibili per ogni tipo di licenza, leggere la [panoramica di Real-Time CDP](../overview.md).

I profili account consentono di unificare le informazioni sull&#39;account provenienti da più origini. Questa visualizzazione unificata di un account riunisce i dati provenienti dai diversi canali di marketing e dai diversi sistemi attualmente utilizzati dalla tua organizzazione per archiviare le informazioni sull’account del cliente. Questo documento fornisce una guida all’interazione con i profili dell’account tramite le funzionalità di Real-Time CDP e B2B edition disponibili nell’interfaccia utente di Adobe Experience Platform.

Per ulteriori informazioni sulla creazione dei profili account nell&#39;ambito del flusso di lavoro B2B, consulta l&#39;[esercitazione end-to-end](../b2b-tutorial.md).

## Panoramica dei profili account {#account-profiles-overview}

Selezionare **[!UICONTROL Profiles]** in [!UICONTROL Accounts] nel menu di navigazione a sinistra per visualizzare la panoramica dei profili account. Nella scheda [!UICONTROL Overview], il dashboard mostra un grafico o un grafico con widget in un singolo punto di ingresso.

![Scheda Panoramica dei profili account con i profili evidenziati nell&#39;area di navigazione a sinistra e Panoramica.](images/b2b-account-profile-overview.png)

Per ulteriori informazioni, consulta la documentazione sul dashboard [[!UICONTROL Account Profiles]](../../dashboards/guides/account-profiles.md). Per ulteriori informazioni su come utilizzare i modelli di dati Approfondimenti per creare grafici personalizzati per le dashboard, consulta la documentazione di [Real-time Customer Data Platform Insights data model B2B edition](../../dashboards/data-models/cdp-insights-data-model-b2b.md).

## Configurare la corrispondenza lead-account {#configure-lead-to-account-matching}

>[!IMPORTANT]
>
> Solo gli amministratori di IA B2B possono abilitare, disabilitare e configurare il lead per il servizio di corrispondenza account. Dopo aver disabilitato il servizio, i risultati corrispondenti verranno eliminati entro 24 ore.

Per configurare la corrispondenza lead-account, selezionare **[!UICONTROL Profiles]** in [!UICONTROL Accounts] nel menu di navigazione a sinistra. Nella scheda **[!UICONTROL Overview]**, seleziona **[!UICONTROL Settings]** in alto a destra.

![Scheda Panoramica dei profili account con Impostazione evidenziata.](images/b2b-configuring-accounts-profile.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Account settings]**. Da qui selezionare l&#39;interruttore **[!UICONTROL Enable lead-to-account-matching]** per abilitare la funzione. Utilizzare il menu a discesa per selezionare **[!UICONTROL Daily]** per l&#39;impostazione **[!UICONTROL Matching cadence]**. Infine, selezionare le opzioni **[!UICONTROL Matching criteria]** pertinenti seguite da **[!UICONTROL Save]** per confermare le impostazioni e tornare alla schermata **[!UICONTROL Account Profiles]**.

>[!NOTE]
>
> L&#39;indirizzo non può essere utilizzato come unico criterio di corrispondenza. È necessario selezionare uno o più degli altri criteri di corrispondenza.

![Configura impostazioni account](images/b2b-configuring-account-settings.png)

Per ulteriori informazioni sulla corrispondenza lead-account, consulta [Lead to account matching in Real-Time CDP B2B overview](../../rtcdp/b2b-ai-ml-services/lead-to-account-matching.md).

## Sfogliare i profili account {#browse-account-profiles}

Per sfogliare i profili account, selezionare **[!UICONTROL Profiles]** in [!UICONTROL Accounts] nel menu di navigazione a sinistra.

Nella scheda **[!UICONTROL Browse]** è possibile esplorare i profili account utilizzando un ID account da un&#39;origine enterprise connessa oppure immettendo direttamente i dettagli dell&#39;origine.

![Utilizza l&#39;ID account per esplorare i profili](images/b2b-account-browse-by.png)

### Sfoglia per [!UICONTROL Connected enterprise source] {#browse-by-connected-enterprise-source}

Per sfogliare i profili account in base a un&#39;origine enterprise connessa, selezionare **[!UICONTROL Connected enterprise source]** dal menu a discesa **[!UICONTROL Browse by]**, quindi scegliere un&#39;origine connessa utilizzando il pulsante di selezione accanto al campo **[!UICONTROL Source]**.

![Sfogliare i profili dell&#39;account in base all&#39;origine aziendale connessa](images/b2b-account-browse.png)

Verrà aperta la finestra di dialogo **[!UICONTROL Select source]**, in cui è possibile selezionare un&#39;origine in base alle connessioni stabilite dall&#39;organizzazione.

>[!NOTE]
>
>È possibile che nell&#39;organizzazione siano configurate più origini per lo stesso provider di servizi (ad esempio, Marketo), pertanto è importante esaminare il nome della connessione, il sistema di origine e l&#39;istanza del sistema di origine per assicurarsi che la ricerca venga eseguita in base all&#39;istanza di origine corretta.

Per ulteriori informazioni sulla connessione delle origini aziendali, consulta la [panoramica delle origini](../sources/sources-overview.md).

È possibile scegliere un&#39;origine selezionando il pulsante di opzione accanto al nome della connessione e quindi utilizzare **[!UICONTROL Select]** per tornare alla scheda [!UICONTROL Browse].

![Seleziona flusso di lavoro di origine](images/b2b-account-select-source.png)

Con un&#39;origine selezionata, ora devi immettere un **[!UICONTROL Account ID]** correlato all&#39;origine. Ad esempio, la selezione di un’origine Salesforce richiede l’immissione di un ID account dall’istanza Salesforce per visualizzare il profilo account associato a tale ID.

>[!NOTE]
>
>Per gli ID account Marketo, è possibile fare riferimento a due tabelle di account, pertanto è necessario utilizzare una sintassi specifica per assicurarsi di visualizzare l’account corretto.
>
>La sintassi standard più comune è l&#39;ID account Marketo aggiunto da `.mkto_org` (ad esempio, `1234567.mkto_org`). I clienti Marketo Account-Based Marketing potrebbero disporre di valori aggiuntivi che possono essere trovati utilizzando l&#39;ID account Marketo aggiunto da `.mkto_account`. Se non sai con certezza quale sintassi utilizzare, rivolgiti al tuo amministratore Marketo.

![Selezione ID account](images/b2b-account-browse-id.png)

### Sfoglia per [!UICONTROL Others] {#browse-by-others}

Real-Time CDP, B2B edition supporta la possibilità di eseguire una ricerca diretta consentendo l&#39;immissione di **[!UICONTROL Source name]**, **[!UICONTROL Source instance]** e **[!UICONTROL Account ID]** per un account che si desidera visualizzare. Immettendo direttamente il nome e l’istanza di origine, fornisci il contesto necessario affinché Experience Platform possa cercare e visualizzare i dati corretti del profilo dell’account.

La capacità di eseguire una ricerca diretta è utile in circostanze in cui non è possibile una connessione sorgente diretta ai dati. Ad esempio, se nell’organizzazione sono in vigore criteri di governance dei dati che impediscono la connessione diretta a un sistema di gestione delle relazioni con i clienti, puoi esportare i dati in un sistema di archiviazione cloud e quindi acquisirli in Experience Platform.

Un altro esempio potrebbe essere che stai eseguendo una trasformazione sui dati tra il momento in cui esce da un sistema e entra in Experience Platform. Puoi utilizzare la funzionalità di ricerca diretta per fornire contesto per i dati (ad esempio per specificare che si tratta di dati di Marketo, nonostante il fatto che provengano da un bucket Amazon S3, ad esempio) in modo che il sistema sappia dove cercare i dati e come eseguirne correttamente il rendering.

Per avviare una ricerca diretta, selezionare **[!UICONTROL Others]** dal menu a discesa **[!UICONTROL Browse by]**, quindi immettere **[!UICONTROL Source name]**, **[!UICONTROL Source instance]** e **[!UICONTROL Account ID]** per l&#39;account che si desidera visualizzare.

![Cerca altri](images/b2b-account-browse-adhoc.png)

## Visualizza dettagli profilo account {#view-account-profile-details}

Dopo aver utilizzato la scheda **[!UICONTROL Browse]** per individuare un profilo account, selezionando **[!UICONTROL Profile ID]** si apre la scheda **[!UICONTROL Detail]** per il profilo account. Le informazioni di profilo visualizzate nella scheda **[!UICONTROL Detail]** sono state unite da più frammenti di profilo per formare un&#39;unica visualizzazione del singolo account. Ciò include i dettagli dell’account come attributi di base e dati dei social media.

I campi predefiniti visualizzati possono anche essere modificati a livello di organizzazione per visualizzare gli attributi di profilo dell’account preferiti.

>[!NOTE]
>
>Funzionalità simili sono disponibili per i profili dei clienti ed è stata creata una guida dettagliata con istruzioni per l’aggiunta e la rimozione di attributi, il ridimensionamento di pannelli, ecc. Per ulteriori informazioni, consulta la [guida alla personalizzazione dei dettagli del profilo](../../profile/ui/profile-customization.md).

![Visualizza dettagli profilo account](images/b2b-account-details.png)

Puoi visualizzare ulteriori dettagli relativi all’account selezionando un’altra delle schede disponibili. Queste schede includono attributi, persone e la scheda opportunità che mostra le opportunità aperte e chiuse relative all’account nei sistemi aziendali. Per ulteriori informazioni su ciascuna scheda, consulta le sezioni seguenti.

## Scheda Attributi {#attributes-tab}

Nella scheda **[!UICONTROL Attributes]** sono elencate tutte le informazioni sui record correlate all&#39;account. Ciò include dati di attributi provenienti da più origini che sono state unite per formare un’unica vista dell’account.

Oltre a poter visualizzare i dati in un elenco, è possibile utilizzare la barra di ricerca per cercare attributi specifici o visualizzare i dati del record come JSON.

![Scheda Attributi](images/b2b-account-attributes.png)

## Scheda Persone {#people-tab}

La scheda **[!UICONTROL People]** fornisce un elenco di singole persone associate all&#39;account. Queste persone possono essere contatti e lead di diversi sistemi aziendali gestiti da diversi team all’interno della tua organizzazione, ma in Real-Time CDP, B2B edition vengono presentate insieme come un unico elenco che ti consente di visualizzare una visione più olistica dei contatti del tuo account.

>[!NOTE]
>
>Nella scheda [!UICONTROL People] viene visualizzato un elenco di un massimo di 25 persone associate all&#39;account. Per gli account con più di 25 persone associate, il sistema mostra un campionamento casuale di 25 record.

Oltre a mostrare un&#39;istantanea delle informazioni per il contatto, ogni persona elencata include anche un collegamento **[!UICONTROL Profile ID]**, che è un collegamento cliccabile che consente di esplorare il Profilo cliente in tempo reale per quella persona. Per ulteriori informazioni sulla visualizzazione dei singoli profili cliente relativi ai tuoi account, visita la guida per [profili di esplorazione in Real-Time CDP, B2B edition](../profile/profile-browse.md).

![Scheda Persone](images/b2b-account-people.png)

## Scheda Opportunità {#opportunities-tab}

La scheda **[!UICONTROL Opportunities]** fornisce informazioni per le opportunità aperte e chiuse relative all&#39;account. Queste opportunità possono essere acquisite in Experience Platform da più origini, tuttavia Real-Time CDP, B2B edition consente agli esperti di marketing di vedere tutte queste opportunità insieme in un’unica posizione.

>[!NOTE]
>
>Nella scheda [!UICONTROL Opportunities] viene visualizzato un elenco di un massimo di 25 opportunità associate all&#39;account. Per gli account con più di 25 opportunità associate, il sistema mostra un campionamento casuale di 25 record.

Ogni opportunità include informazioni quali il nome, l&#39;importo, la fase e se l&#39;opportunità è aperta, chiusa, vinta o persa.

![Scheda opportunità account](images/b2b-account-opportunities.png)

## Scheda Account correlati {#related-accounts-tab}

La scheda **[!UICONTROL Related accounts]** fornisce informazioni su altri account che potrebbero essere correlati all&#39;account che si sta esplorando. Per informazioni approfondite sulla funzionalità, leggere la [panoramica degli account correlati](/help/rtcdp/b2b-ai-ml-services/related-accounts.md).

>[!NOTE]
>
>* Un gruppo di account correlati può avere un massimo di 30 profili di account. Se sono stati trovati più di 30 profili di account correlati, questi vengono arbitrariamente suddivisi in più gruppi, ciascuno dei quali non ha più di 30 membri. Il gruppo Account correlati di un profilo di account include sempre se stesso.
>* La scheda [!UICONTROL Related accounts] visualizza attualmente un elenco di un massimo di 25 account correlati associati all&#39;account che si sta esplorando. Si tratta di una limitazione che sarà affrontata in un aggiornamento futuro. Nonostante questo limite dell’interfaccia utente, quando utilizzi account correlati nelle definizioni dei segmenti, per gruppi di 30 profili di account correlati tutti i profili vengono utilizzati per il targeting.

Ogni account correlato include informazioni quali l’ID e il nome del profilo dell’account, la chiave di origine dell’account e ulteriori informazioni relative a home page, indirizzo, account principale, telefono, settore e ricavi annuali.

![Scheda Account correlati](images/b2b-account-related-accounts.png)

Puoi utilizzare gli account correlati in questo elenco a scopo di segmentazione. Consulta un [esempio di segmentazione](/help/rtcdp/segmentation/b2b.md#related-account) per scoprire come utilizzare gli account correlati per espandere la portata nelle definizioni dei segmenti.