---
title: Best practice per l’adesione alle licenze di gestione dati
description: Scopri le best practice da seguire e gli strumenti che puoi utilizzare per gestire al meglio i diritti alle licenze con Adobe Experience Platform.
exl-id: f23bea28-ebd2-4ed4-aeb1-f896d30d07c2
source-git-commit: 1f3cf3cc57342a23dae2d69c883b5768ec2bba57
workflow-type: tm+mt
source-wordcount: '2957'
ht-degree: 1%

---

# Best practice per l’adesione alle licenze di gestione dati

Adobe Experience Platform è un sistema aperto che trasforma i tuoi dati in solidi profili cliente da aggiornare in tempo reale e utilizza informazioni basate sull’intelligenza artificiale per aiutarti a fornire le esperienze giuste su ogni canale. Puoi acquisire dati di diversi tipi, volumi e storie in Experience Platform utilizzando le origini, quindi gestire tali dati per casi di utilizzo che vanno dalla segmentazione e personalizzazione all’analisi e all’apprendimento automatico.

Experience Platform offre licenze che stabiliscono il numero di profili che è possibile creare e la quantità di dati che è possibile inserire. Data la capacità di inserire qualsiasi origine, volume o cronologia di dati, è possibile superare i diritti di licenza man mano che i volumi di dati aumentano.

Leggi questa guida per le best practice da seguire e gli strumenti che puoi utilizzare per gestire al meglio i diritti alle licenze con Experience Platform.

## Riepilogo delle funzioni {#summary-of-features}

Utilizza le best practice e gli strumenti descritti in questo documento per gestire al meglio l’utilizzo dei diritti di licenza in Experience Platform. Questo documento viene aggiornato con l’aggiunta di nuove funzioni che forniscono visibilità e controllo a tutti i clienti Experience Platform.

La tabella seguente illustra l’elenco delle funzioni attualmente disponibili per gestire al meglio il diritto all’utilizzo della licenza.

| Funzione | Descrizione |
| --- | --- |
| [Interfaccia utente set di dati - Conservazione dei dati di Experience Event](../../catalog/datasets/user-guide.md#data-retention-policy) | Configura un periodo di conservazione fisso per i dati nel data lake e nell’archivio profili. I record vengono eliminati al termine del periodo di conservazione configurato. |
| [Attiva/Disattiva set di dati per Real-Time Customer Profile](../../catalog/datasets/user-guide.md) | Abilita o disabilita l’acquisizione di set di dati in Real-Time Customer Profile. |
| [Scadenze eventi esperienza nell&#39;archivio profili](../../profile/event-expirations.md) | Applica un tempo di scadenza per tutti gli eventi acquisiti in un set di dati abilitato per il profilo. Per abilitare questa funzione, contatta il team del tuo account Adobe o l’Assistenza clienti. |
| [Filtri per la preparazione dati di Adobe Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-real-time-customer-profile) | Applica i filtri [!DNL Kafka] per escludere i dati non necessari dall&#39;acquisizione. |
| [Filtri del connettore di origine di Adobe Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) | Applica i filtri della connessione di origine di Audience Manager per escludere i dati non necessari dall’acquisizione. |
| [Filtri dati inoltro eventi](../../tags/ui/event-forwarding/overview.md) | Applica i filtri [!DNL Kafka] lato server per escludere i dati non necessari dall&#39;acquisizione.  Per ulteriori informazioni, consulta la documentazione sulle [regole tag](../../tags/ui/managing-resources/rules.md). |
| [Interfaccia utente dashboard utilizzo licenze](../../dashboards/guides/license-usage.md#license-usage-dashboard-data) | Monitora il consumo di prodotti Experience Platform da parte della tua organizzazione rispetto ai diritti concessi in licenza. Accedi a istantanee sull’utilizzo giornaliero, tendenze predittive e dati dettagliati a livello di sandbox per supportare la gestione proattiva delle licenze. |
| [API report di sovrapposizione set di dati](../../profile/tutorials/dataset-overlap-report.md) | Restituisce i set di dati che contribuiscono maggiormente al pubblico indirizzabile. |
| [API report di sovrapposizione identità](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) | Restituisce gli spazi dei nomi di identità che contribuiscono maggiormente al pubblico indirizzabile. |
| [Scadenze dati profilo pseudonimo](../../profile/pseudonymous-profiles.md) | Configura i tempi di scadenza dei dati per i profili pseudonimi e rimuovi automaticamente i dati dall’archivio profili. |

{style="table-layout:auto"}

## Informazioni sull’archiviazione dei dati in Experience Platform

Experience Platform è composto principalmente da due archivi di dati: il data lake e l’archivio profili.

Il data lake ha principalmente i seguenti scopi:

* Funge da area di gestione temporanea per l’onboarding dei dati in Experience Platform;
* Funge da archiviazione dei dati a lungo termine per tutti i dati di Experience Platform;
* Abilita casi d’uso come analisi dei dati e data science.

L&#39;**archivio profili** è il luogo in cui vengono creati i profili dei clienti e ha principalmente le seguenti finalità:

* Funge da archivio dati per i profili utilizzati per supportare esperienze in tempo reale;
* Abilita casi d’uso come segmentazione, attivazione e personalizzazione.

>[!NOTE]
>
>L&#39;accesso a [!DNL data lake] può dipendere dallo SKU del prodotto acquistato. Per ulteriori informazioni sugli SKU dei prodotti, contatta il tuo rappresentante Adobe.

## Utilizzo delle licenze {#license-usage}

Quando si concede la licenza ad Experience Platform, si dispone di diritti di utilizzo della licenza che variano a seconda dello SKU:

**[!DNL Addressable Audience]**: numero totale di profili cliente contrattualmente consentiti in Experience Platform, inclusi i profili noti e pseudonimi.

**[!DNL Total Data Volume]**: la quantità totale di dati disponibili per Real-Time Customer Profile da utilizzare nei flussi di lavoro di coinvolgimento.

La disponibilità di queste metriche e la definizione specifica di ciascuna di esse varia a seconda delle licenze acquistate dalla tua organizzazione.

## Dashboard utilizzo licenze

L’interfaccia utente di Adobe Experience Platform fornisce una dashboard tramite la quale puoi visualizzare un’istantanea dei dati relativi alla licenza della tua organizzazione per Experience Platform. I dati nel dashboard vengono visualizzati esattamente come appaiono nel momento specifico in cui è stata acquisita l’istantanea. L’istantanea non è né un’approssimazione né un campione di dati e il dashboard non viene aggiornato in tempo reale.

Per ulteriori informazioni, consulta la guida su [utilizzo del dashboard utilizzo licenze nell&#39;interfaccia utente di Experience Platform](../../dashboards/guides/license-usage.md#license-usage-dashboard-data).

## Best practice per la gestione dei dati

Le sezioni seguenti descrivono le best practice da seguire per gestire meglio i dati.

### Comprensione dei dati

Non tutti i dati sono uguali in Adobe Experience Platform. Alcuni dati possono essere densi, ma di valore basso, mentre altri possono essere sparsi, ma di valore elevato. Alcuni dati potrebbero perdere valore non appena vengono generati, mentre altri potrebbero essere preziosi per mesi, se non anni.

Esistono tre dimensioni da considerare per comprendere il valore dei dati:

| Dimensione | Descrizione | Esempio |
| --- | --- | --- |
| Volume | Rappresenta la quantità e la totalità dei dati acquisiti. | Clic web: volume elevato e fedeltà moderata. Il valore può diminuire rapidamente. |
| Intervallo temporale | Rappresenta il periodo di tempo in cui i dati acquisiti continuano a rimanere preziosi. | Acquisti offline: volume e fedeltà moderati, ma possono essere utili per lunghi periodi di tempo. |
| Fedeltà | Rappresenta la ricchezza dei dati rispetto alle informazioni. | Account del cliente: volumi ridotti, ma fedeltà elevata. Può essere utile anche oltre la durata di vita di un cliente. |

### Strumenti di gestione dati {#data-management-tools}

Esistono due scenari centrali da considerare per garantire che l’utilizzo dei dati rimanga entro i limiti di licenza spettante:

### Quali dati inserire in Experience Platform?

I dati possono essere acquisiti in uno o più sistemi in Experience Platform, ovvero nell&#39;archivio [!DNL data lake] e/o Profilo. Ciò significa che in entrambi i sistemi possono esistere dati diversi per una varietà di casi d’uso diversi. Ad esempio, potrebbe essere utile conservare i dati storici in [!DNL data lake], ma non nell&#39;archivio profili. Per selezionare i dati da inviare all’archivio profili, abilita un set di dati per l’acquisizione del profilo.

>[!NOTE]
>
>L&#39;accesso a [!DNL data lake] può dipendere dallo SKU del prodotto acquistato. Per ulteriori informazioni sugli SKU dei prodotti, contatta il tuo rappresentante Adobe.

### Quali dati conservare?

Per rimuovere i dati diventati obsoleti per i tuoi casi d’uso, puoi applicare sia i filtri di acquisizione dei dati che le regole di scadenza. In genere, i dati comportamentali (come i dati di Analytics) occupano una quantità di spazio di archiviazione significativamente maggiore rispetto ai dati dei record (come i dati CRM). Ad esempio, molti utenti di Experience Platform hanno fino al 90% dei profili compilati dai soli dati comportamentali, rispetto a quelli dei dati dei record. Pertanto, la gestione dei dati comportamentali è fondamentale per garantire la conformità all’interno dei diritti di licenza.

Esistono diversi strumenti che puoi sfruttare per rispettare i diritti di utilizzo delle licenze:

* [Filtri di acquisizione](#ingestion-filters)
* [Archivio profili](#profile-service)

### Servizio identità e pubblico indirizzabile {#identity-service}

I grafici delle identità non vengono conteggiati per il diritto totale al pubblico indirizzabile, perché il pubblico indirizzabile si riferisce al numero totale di profili cliente.

Tuttavia, i limiti del grafo delle identità possono influenzare il pubblico indirizzabile a causa della suddivisione delle identità. Ad esempio, se l’ECID più vecchio viene rimosso dal grafico, ECID continuerà a esistere in Real-Time Customer Profile come profilo pseudonimo. Puoi impostare [Scadenze dati profilo pseudonimo](../../profile/pseudonymous-profiles.md) per aggirare questo comportamento. Per ulteriori informazioni, leggere [guardrail per i dati del servizio Identity](../../identity-service/guardrails.md).

### Filtri di acquisizione {#ingestion-filters}

I filtri di acquisizione consentono di inserire solo i dati necessari per i casi d’uso e di escludere tutti gli eventi non necessari.

| Filtro di acquisizione | Descrizione |
| --- | --- |
| Filtro origine Adobe Audience Manager | Quando crei una connessione di origine Adobe Audience Manager, puoi scegliere quali segmenti e caratteristiche inserire nel profilo cliente in [!DNL data lake] e in tempo reale, anziché acquisire i dati di Audience Manager nella loro interezza. Per ulteriori informazioni, consulta la guida sulla [creazione di una connessione di origine Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md). |
| Preparazione dati di Adobe Analytics | È possibile utilizzare le funzionalità [!DNL Data Prep] durante la creazione di una connessione di origine Analytics per filtrare i dati non necessari per i casi d&#39;uso. Tramite [!DNL Data Prep], puoi definire quali attributi/colonne devono essere pubblicati nel profilo. È inoltre possibile fornire istruzioni condizionali per informare Experience Platform se i dati devono essere pubblicati nel profilo o solo in [!DNL data lake]. Per ulteriori informazioni, consulta la guida sulla [creazione di una connessione di origine Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |
| Supporto per abilitare/disabilitare i set di dati per il profilo | Per acquisire dati nel Profilo cliente in tempo reale, devi abilitare un set di dati da utilizzare nell’archivio Profili. In questo modo, aggiungi alle tue [!DNL Addressable Audience] e [!DNL Total Data Volume] adesioni. Una volta che un set di dati non è più necessario per i casi di utilizzo del profilo cliente, puoi disabilitare l’integrazione del set di dati con Profilo per garantire che i dati rimangano conformi alla licenza. Per ulteriori informazioni, consulta la guida su [abilitazione e disabilitazione dei set di dati per il profilo](../../catalog/datasets/enable-for-profile.md). |
| Esclusione di dati da Web SDK e Mobile SDK | Esistono due tipi di dati raccolti da Web e Mobile SDK: dati raccolti automaticamente e dati raccolti esplicitamente dallo sviluppatore. Per gestire meglio la conformità della licenza, puoi disabilitare la raccolta automatica dei dati nella configurazione di SDK tramite l’impostazione del contesto. I dati personalizzati possono anche essere rimossi o non impostati dallo sviluppatore. |
| Esclusione dei dati di inoltro lato server | Se invii dati ad Experience Platform utilizzando l’inoltro lato server, puoi escludere i dati inviati rimuovendo la mappatura in un’azione della regola per escluderla in tutti gli eventi oppure aggiungendo condizioni alla regola in modo che i dati vengano attivati solo per determinati eventi. Per ulteriori informazioni, consulta la documentazione su [eventi e condizioni](/help/tags/ui/managing-resources/rules.md#events-and-conditions-if). |
| Filtrare i dati a livello di origine | Puoi utilizzare operatori logici e di confronto per filtrare i dati a livello di riga dalle origini prima di creare una connessione e acquisire dati in Experience Platform. Per ulteriori informazioni, leggere la guida su [filtrare i dati a livello di riga per un&#39;origine utilizzando l&#39; [!DNL Flow Service] API](../../sources/tutorials/api/filter.md). |

{style="table-layout:auto"}

### Archivio profili {#profile-service}

L’archivio Profili è composto dai seguenti componenti:

| Componente archivio profili | Descrizione |
| --- | --- |
| Frammenti di profilo | Ogni profilo cliente è composto da più **frammenti di profilo** che sono stati uniti per formare un&#39;unica visualizzazione del cliente. Ad esempio, se un cliente interagisce con il tuo marchio su più canali, la tua organizzazione avrà più **frammenti di profilo** relativi a quel singolo cliente che appaiono in più set di dati. Quando questi frammenti vengono acquisiti in Experience Platform, vengono uniti utilizzando il grafico delle identità per creare un singolo profilo per quel cliente. **I frammenti di profilo** sono costituiti da uno spazio dei nomi di identità come identificatore, con dati di record e/o dati di serie temporali associati. |
| Registra dati (attributi) | Un profilo è una rappresentazione di un soggetto, un&#39;organizzazione o un individuo, composta da molti **Attributi** (noti anche come **dati record**). Ad esempio, il profilo di un prodotto può includere uno SKU e una descrizione, mentre il profilo di una persona contiene informazioni come nome, cognome e indirizzo e-mail. **I dati del record** sono in genere di volume basso/moderato, ma sono importanti per lunghi periodi di tempo. |
| Dati delle serie temporali (Comportamento) | **I dati della serie temporale** forniscono informazioni sul comportamento di un utente. Rappresentati dalla classe di schema standard Experience Data Model (XDM) [!DNL ExperienceEvent], i dati della serie temporale possono descrivere eventi quali elementi aggiunti a un carrello, collegamenti su cui si fa clic e video visualizzati. Il valore del comportamento può diminuire nel tempo. |
| Spazio dei nomi dell’identità (identità) | Quando i dati dei clienti si uniscono, vengono uniti in un unico profilo tramite l&#39;utilizzo di **spazi dei nomi di identità** e la possibilità di unire queste identità man mano che si acquisiscono ulteriori informazioni sull&#39;utente. Per ulteriori informazioni, consulta la [panoramica sugli spazi dei nomi delle identità](../../identity-service/features/namespaces.md). |

{style="table-layout:auto"}

### Rapporti composizione archivio profili

Sono disponibili diversi rapporti per comprendere la composizione dell’archivio Profili. Questi rapporti ti aiutano a prendere decisioni informate su come e dove impostare le scadenze degli eventi esperienza per ottimizzare l’utilizzo della licenza:

* **API report di sovrapposizione set di dati**: espone i set di dati che contribuiscono maggiormente al pubblico indirizzabile. È possibile utilizzare questo report per identificare i [!DNL ExperienceEvent] set di dati per i quali impostare una scadenza. Per ulteriori informazioni, consulta l&#39;esercitazione su [generazione del report di sovrapposizione dei set di dati](../../profile/tutorials/dataset-overlap-report.md).
* **API rapporto di sovrapposizione identità**: espone gli spazi dei nomi delle identità che contribuiscono maggiormente al pubblico indirizzabile. Per ulteriori informazioni, consulta l&#39;esercitazione su [generazione del rapporto di sovrapposizione identità](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report).
<!-- * **Unknown Profiles Report API**: Exposes the impact of applying pseudonymous expirations for different time thresholds. You can use this report to identify which pseudonymous expirations threshold to apply. See the tutorial on [generating the unknown profiles report](../../profile/api/preview-sample-status.md#generate-the-unknown-profiles-report) for more information.
-->

### Scadenze dati profilo pseudonimo {#pseudonymous-profile-expirations}

Utilizza la funzionalità di scadenza dei dati dei profili pseudonimi per rimuovere automaticamente dall’archivio profili i dati che non sono più validi o utili per i tuoi casi d’uso. La scadenza dei dati del profilo pseudonimo rimuove sia i record evento che quelli del profilo. Di conseguenza, questa impostazione ridurrà i volumi del pubblico indirizzabile. Per ulteriori informazioni su questa funzione, leggere la [Panoramica sulla scadenza dei dati del profilo pseudonimo](../../profile/pseudonymous-profiles.md).

### Interfaccia utente del set di dati - Conservazione del set di dati di Experience Event {#data-retention}

Configura le impostazioni di scadenza e conservazione del set di dati per applicare un periodo di conservazione fisso per i dati nel data lake e nell’archivio profili. Al termine del periodo di conservazione, i dati vengono eliminati. La scadenza dei dati di Experience Event rimuove solo gli eventi e non i dati della classe di profilo, il che ridurrà il [volume totale di dati](total-data-volume.md) nelle metriche di utilizzo della licenza. Per ulteriori informazioni, leggere la guida all&#39;impostazione dei criteri di conservazione dei dati [](../../catalog/datasets/user-guide.md#data-retention-policy).

### Scadenze eventi esperienza profilo {#event-expirations}

Configura i tempi di scadenza per rimuovere automaticamente i dati comportamentali dal set di dati abilitati per il profilo una volta che non sono più utili per i tuoi casi d’uso. Per ulteriori informazioni, leggi la panoramica su [Scadenze evento esperienza](../../profile/event-expirations.md).

## Riepilogo delle best practice per la conformità dell’utilizzo delle licenze {#best-practices}

Di seguito è riportato un elenco di alcune best practice consigliate che è possibile seguire per garantire una migliore aderenza all’adesione all’utilizzo della licenza:

* Utilizza il [dashboard utilizzo licenze](../../dashboards/guides/license-usage.md) per monitorare e tenere traccia delle tendenze di utilizzo dei clienti. Questo ti consente di anticipare eventuali interruzioni del servizio.
* Configura [filtri di acquisizione](#ingestion-filters) identificando gli eventi necessari per i casi di utilizzo di segmentazione e personalizzazione. Questo ti consente di inviare solo gli eventi importanti necessari per i tuoi casi d’uso.
* Assicurati di disporre solo di [set di dati abilitati per il profilo](#ingestion-filters) necessari per i casi di utilizzo di segmentazione e personalizzazione.
* Configura [Scadenze evento esperienza](../../catalog/datasets/user-guide.md#data-retention-policy) e [Scadenze dati profilo pseudonimo](../../profile/pseudonymous-profiles.md) per dati ad alta frequenza come i dati Web.
* Configura i [criteri di conservazione TTL (Time-to-Live) per i set di dati Experience Event](../../catalog/datasets/experience-event-dataset-retention-ttl-guide.md) nel data lake per rimuovere automaticamente i record obsoleti e ottimizzare l&#39;utilizzo dello spazio di archiviazione in linea con i diritti alla licenza.
* Controlla periodicamente i [report sulla composizione del profilo](#profile-store-composition-reports) per conoscere la composizione dell&#39;archivio profili. Questo consente di comprendere le origini dati che contribuiscono maggiormente al consumo delle licenze.

## Caso d’uso: conformità dell’utilizzo della licenza

### Perché considerare questo caso d’uso

Garantendo la conformità alle **disposizioni sull&#39;utilizzo delle licenze** per data lake e storage dei profili, è possibile evitare interruzioni, ottimizzare i costi e allineare i criteri di conservazione dei dati ai requisiti aziendali.

### Prerequisiti e pianificazione

Considera i seguenti prerequisiti nel processo di pianificazione:

* **Accesso e autorizzazioni**:
   * Assicurati di disporre dell&#39;autorizzazione **Gestisci set di dati** per utilizzare il TTL dell&#39;evento esperienza.
   * Assicurati di avere **Gestione impostazioni profilo** per utilizzare il TTL del profilo pseudonimo.
* **Informazioni sui criteri di conservazione dei dati**:
   * Regole organizzative relative alla conservazione dei dati e alla conformità
   * Esigenze aziendali per l’analisi dei dati e intervalli di lookback della segmentazione

### Funzionalità dell’interfaccia utente, componenti di Experience Platform e prodotti Experience Cloud che utilizzerai

Per implementare correttamente questo caso d’uso, devi utilizzare più aree di Adobe Experience Platform. Assicurati di disporre delle autorizzazioni di controllo dell’accesso basate su attributi necessarie per tutte queste aree, oppure chiedi all’amministratore di sistema di concederle.

* Dashboard di utilizzo della licenza: visualizza l’utilizzo corrente dei diritti a livello sandbox.
* Gestione dei dataset: monitoraggio e gestione dei criteri di conservazione a livello di dataset.
* Tipi di pubblico (Real-Time Customer Profile): assicurati che le regole di segmentazione siano allineate alle finestre di conservazione dei dati nella finestra di lookback.
* Monitoraggio e avvisi: tieni traccia degli aggiornamenti e ricevi informazioni approfondite sulle operazioni di conservazione dei set di dati.

### Come utilizzare il caso d’uso: istruzioni dettagliate

Leggi le sezioni seguenti, che includono collegamenti a ulteriore documentazione, per completare ciascuno dei passaggi descritti nella panoramica di alto livello precedente.

**Verifica l&#39;utilizzo della licenza corrente**

Innanzitutto, passa alla **dashboard sull&#39;utilizzo delle licenze** e controlla l&#39;utilizzo dei diritti a livello di sandbox.

>[!BEGINTABS]

>[!TAB Sandbox di produzione]

Utilizzare l&#39;interfaccia [!UICONTROL Metrics] per visualizzare le metriche di utilizzo delle licenze. Per impostazione predefinita, l’interfaccia visualizza le informazioni per la sandbox di produzione.

![L&#39;interfaccia utente del dashboard utilizzo licenze visualizza le metriche di utilizzo licenze per una sandbox di produzione.](../images/data-management/prod-sandbox.png)

>[!TAB Sandbox di sviluppo]

Seleziona [!UICONTROL Development] per visualizzare le metriche di utilizzo delle licenze relative alle sandbox di sviluppo.

![L&#39;interfaccia utente del dashboard utilizzo licenze visualizza le metriche di utilizzo licenze per le sandbox di sviluppo.](../images/data-management/dev-sandbox.png)

>[!ENDTABS]

Per ulteriori informazioni, leggere la documentazione su [utilizzando il dashboard di utilizzo delle licenze](../../dashboards/guides/license-usage.md).

**Analisi dell&#39;utilizzo dell&#39;archiviazione a livello di set di dati**

Utilizza la **visualizzazione Sfoglia set di dati** per rivedere le metriche di utilizzo del set di dati sia per il data lake che per il profilo cliente in tempo reale. Selezionare le intestazioni di colonna per **[!UICONTROL Data Lake Storage]** o **[!UICONTROL Profile Storage]**, quindi selezionare **[!UICONTROL Sort Descending]** dal pannello a comparsa.

>[!BEGINTABS]

>[!TAB Archiviazione data lake]

I set di dati nel data lake sono ordinati in base alla dimensione di archiviazione. Utilizza questa funzione per identificare i maggiori consumatori di storage nel data lake.

![I set di dati nel data lake sono ordinati dal più grande al più piccolo.](../images/data-management/data-lake-storage.png)

>[!TAB Archiviazione profili]

I set di dati nel profilo sono ordinati in base alla dimensione di archiviazione. Utilizza questa funzione per identificare i principali utenti dello storage nel profilo.

![I set di dati nel profilo sono ordinati dal più grande al più piccolo.](../images/data-management/profile-storage.png)

>[!ENDTABS]

**Valuta e configura la regola di conservazione**

Quindi, verifica se i set di dati dispongono dei criteri di conservazione appropriati in base ai limiti di licenza e ai requisiti di business per Analytics e Segmentazione. Per visualizzare i criteri di conservazione di un set di dati, selezionare i puntini di sospensione (`...`) accanto al set di dati, quindi selezionare **[!UICONTROL Set data retention policy]**.

![Pannello popup con opzioni del set di dati, incluso &quot;Imposta criteri di conservazione dei dati&quot;](../images/data-management/set-retention-policy.png)

Viene visualizzata l&#39;interfaccia *[!UICONTROL Set dataset retention]*. Utilizzare questa interfaccia per configurare un criterio di conservazione per il set di dati. Puoi utilizzarlo anche per visualizzare lo spazio di archiviazione che il set di dati occupa nel data lake o nel profilo.

![Interfaccia &quot;set dataset retention&quot;.](../images/data-management/dataset-retention.png)

Puoi analizzare ulteriormente l’impatto sulla conservazione del set di dati utilizzando la funzione di previsione dell’impatto. Selezionare **[!UICONTROL View ExperienceEvent data distribution]** per visualizzare un grafico che visualizza la finestra di conservazione e la percentuale totale di archiviazione impostata per la scadenza.

Al termine, selezionare **[!UICONTROL Save]**

![Impact Forecaster dall&#39;interfaccia di conservazione dei set di dati.](../images/data-management/impact-forecaster.png)

**Convalida modifiche di conservazione**

Dopo aver applicato i criteri di conservazione, è possibile utilizzare i seguenti strumenti per convalidare le modifiche:

* [Metriche di utilizzo del set di dati](../../catalog/datasets/user-guide.md#enhanced-visibility-of-retention-periods-and-storage-metrics) nella visualizzazione Esplora set di dati.
* Il [dashboard di monitoraggio](../../dataflows/ui/monitor.md) per visualizzare e analizzare l&#39;impatto della conservazione.
* Il [dashboard utilizzo licenze](../../dashboards/guides/license-usage.md) per visualizzare snapshot giornalieri, tendenze predittive e informazioni a livello di sandbox.
