---
title: Best practice per l’adesione alle licenze di gestione dati
description: Scopri le best practice da seguire e gli strumenti che puoi utilizzare per gestire al meglio i diritti alle licenze con Adobe Experience Platform.
exl-id: f23bea28-ebd2-4ed4-aeb1-f896d30d07c2
source-git-commit: 1b8fd7671146519fa66768aab3fe081adb0bd6c6
workflow-type: tm+mt
source-wordcount: '2145'
ht-degree: 2%

---

# Best practice per l’adesione alle licenze di gestione dati

Adobe Experience Platform è un sistema aperto che trasforma i tuoi dati in solidi profili cliente da aggiornare in tempo reale e utilizza informazioni basate sull’intelligenza artificiale per aiutarti a fornire le esperienze giuste su ogni canale. Puoi acquisire dati di tipi, volumi e storie diversi per Experience Platform utilizzando le origini e quindi gestire tali dati per casi d’uso che vanno dalla segmentazione e personalizzazione all’analisi e all’apprendimento automatico.

Platform offre licenze che stabiliscono il numero di profili che è possibile creare e la quantità di dati che è possibile inserire. Data la capacità di inserire qualsiasi origine, volume o cronologia di dati, è possibile superare i diritti di licenza man mano che i volumi di dati aumentano.

Questo documento illustra le best practice da seguire e gli strumenti che puoi utilizzare per gestire al meglio i diritti alle licenze con Adobe Experience Platform.

## Informazioni sull&#39;archiviazione dei dati Adobe Experience Platform

L&#39;Experience Platform è composto principalmente da due archivi di dati: l&#39;archivio [!DNL data lake] e l&#39;archivio Profilo.

**[!DNL data lake]** ha principalmente i seguenti scopi:

* funge da area di gestione temporanea per l’onboarding dei dati in Experience Platform;
* funge da archiviazione dei dati a lungo termine per tutti i dati Experience Platform;
* Abilita casi d’uso come analisi dei dati e data science.

L&#39;**archivio profili** è il luogo in cui vengono creati i profili dei clienti e ha principalmente le seguenti finalità:

* Funge da archivio dati per i profili utilizzati per supportare esperienze in tempo reale;
* Abilita casi d’uso come segmentazione, attivazione e personalizzazione.

>[!NOTE]
>
>L&#39;accesso a [!DNL data lake] può dipendere dallo SKU del prodotto acquistato. Per ulteriori informazioni sugli SKU dei prodotti, contatta il rappresentante del tuo Adobe.

## Utilizzo delle licenze {#license-usage}

Quando si riceve la licenza di Experience Platform, vengono forniti diritti di utilizzo della licenza che variano a seconda dello SKU:

**[!DNL Addressable Audience]** - numero totale di profili cliente contrattualmente consentiti in Experience Platform, inclusi i profili noti e pseudonimi.

**[!DNL Total Data Volume]** - la quantità totale di dati disponibili per Adobe Experience Platform Profile Service da utilizzare nei flussi di lavoro di coinvolgimento.

La disponibilità di queste metriche e la definizione specifica di ciascuna di esse varia a seconda delle licenze acquistate dalla tua organizzazione.

## Dashboard utilizzo licenze

L’interfaccia utente di Adobe Experience Platform fornisce un dashboard tramite il quale puoi visualizzare un’istantanea dei dati relativi alla licenza della tua organizzazione per Platform. I dati nel dashboard vengono visualizzati esattamente come appaiono nel momento specifico in cui è stata acquisita l’istantanea. L’istantanea non è né un’approssimazione né un campione di dati e il dashboard non viene aggiornato in tempo reale.

Per ulteriori informazioni, consulta la guida su [utilizzo del dashboard utilizzo licenze nell&#39;interfaccia utente di Platform](../../dashboards/guides/license-usage.md#license-usage-dashboard-data).

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

### Quali dati inserire in Platform?

I dati possono essere acquisiti in uno o più sistemi in Platform, ovvero nell’archivio [!DNL data lake] e/o Profilo. Ciò significa che in entrambi i sistemi possono esistere dati diversi per una varietà di casi d’uso diversi. Ad esempio, potrebbe essere utile conservare i dati storici in [!DNL data lake], ma non nell&#39;archivio profili. Per selezionare i dati da inviare all’archivio profili, abilita un set di dati per l’acquisizione del profilo.

>[!NOTE]
>
>L&#39;accesso a [!DNL data lake] può dipendere dallo SKU del prodotto acquistato. Per ulteriori informazioni sugli SKU dei prodotti, contatta il rappresentante del tuo Adobe.

### Quali dati conservare?

Per rimuovere i dati diventati obsoleti per i tuoi casi d’uso, puoi applicare sia i filtri di acquisizione dei dati che le regole di scadenza. In genere, i dati comportamentali (come i dati di Analytics) occupano una quantità di spazio di archiviazione significativamente maggiore rispetto ai dati dei record (come i dati CRM). Ad esempio, molti utenti di Platform hanno fino al 90% dei profili compilati dai soli dati comportamentali, rispetto a quelli dei dati dei record. Pertanto, la gestione dei dati comportamentali è fondamentale per garantire la conformità all’interno dei diritti di licenza.

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
| Filtro origine Adobe Audience Manager | Quando si crea una connessione di origine Adobe Audience Manager, è possibile scegliere i segmenti e le caratteristiche da inserire in [!DNL data lake] e nel profilo cliente in tempo reale, anziché acquisire i dati di Audience Manager nella loro interezza. Per ulteriori informazioni, vedere la guida alla [creazione di una connessione di origine Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md). |
| Preparazione dati di Adobe Analytics | È possibile utilizzare le funzionalità [!DNL Data Prep] durante la creazione di una connessione di origine Analytics per filtrare i dati non necessari per i casi d&#39;uso. Tramite [!DNL Data Prep], puoi definire quali attributi/colonne devono essere pubblicati nel profilo. È inoltre possibile fornire istruzioni condizionali per informare Platform se i dati devono essere pubblicati nel profilo o solo in [!DNL data lake]. Per ulteriori informazioni, consulta la guida sulla [creazione di una connessione di origine Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |
| Supporto per abilitare/disabilitare i set di dati per il profilo | Per acquisire dati nel Profilo cliente in tempo reale, devi abilitare un set di dati da utilizzare nell’archivio Profili. In questo modo, aggiungi alle tue [!DNL Addressable Audience] e [!DNL Total Data Volume] adesioni. Una volta che un set di dati non è più necessario per i casi di utilizzo del profilo cliente, puoi disabilitare l’integrazione del set di dati con Profilo per garantire che i dati rimangano conformi alla licenza. Per ulteriori informazioni, consulta la guida su [abilitazione e disabilitazione dei set di dati per il profilo](../../catalog/datasets/enable-for-profile.md). |
| Esclusione di dati SDK per web e SDK per dispositivi mobili | Esistono due tipi di dati raccolti da Web e Mobile SDK: dati raccolti automaticamente e dati raccolti esplicitamente dallo sviluppatore. Per gestire meglio la conformità della licenza, puoi disabilitare la raccolta automatica dei dati nella configurazione dell’SDK tramite l’impostazione contestuale. I dati personalizzati possono anche essere rimossi o non impostati dallo sviluppatore. |
| Esclusione dei dati di inoltro lato server | Se invii dati a Platform utilizzando l’inoltro lato server, puoi escludere i dati inviati rimuovendo la mappatura in un’azione della regola per escluderla in tutti gli eventi oppure aggiungendo condizioni alla regola in modo che i dati vengano attivati solo per determinati eventi. Per ulteriori informazioni, consulta la documentazione su [eventi e condizioni](/help/tags/ui/managing-resources/rules.md#events-and-conditions-if). |
| Filtrare i dati a livello di origine | Puoi utilizzare operatori logici e di confronto per filtrare i dati a livello di riga dalle origini prima di creare una connessione e acquisire i dati da Experience Platform. Per ulteriori informazioni, leggere la guida su [filtrare i dati a livello di riga per un&#39;origine utilizzando l&#39; [!DNL Flow Service] API](../../sources/tutorials/api/filter.md). |

{style="table-layout:auto"}

### Archivio profili {#profile-service}

L’archivio Profili è composto dai seguenti componenti:

| Componente archivio profili | Descrizione |
| --- | --- |
| Frammenti di profilo | Ogni profilo cliente è composto da più **frammenti di profilo** che sono stati uniti per formare un&#39;unica visualizzazione del cliente. Ad esempio, se un cliente interagisce con il tuo marchio su più canali, la tua organizzazione avrà più **frammenti di profilo** relativi a quel singolo cliente che appaiono in più set di dati. Quando questi frammenti vengono acquisiti in Platform, vengono uniti utilizzando il grafico delle identità per creare un singolo profilo per quel cliente. **I frammenti di profilo** sono costituiti da uno spazio dei nomi di identità come identificatore, con dati di record e/o dati di serie temporali associati. |
| Registra dati (attributi) | Un profilo è una rappresentazione di un soggetto, un&#39;organizzazione o un individuo, composta da molti **Attributi** (noti anche come **dati record**). Ad esempio, il profilo di un prodotto può includere uno SKU e una descrizione, mentre il profilo di una persona contiene informazioni come nome, cognome e indirizzo e-mail. **I dati del record** sono in genere di volume basso/moderato, ma sono importanti per lunghi periodi di tempo. |
| Dati delle serie temporali (Comportamento) | **I dati della serie temporale** forniscono informazioni sul comportamento di un utente. Rappresentati dalla classe di schema standard Experience Data Model (XDM) [!DNL ExperienceEvent], i dati della serie temporale possono descrivere eventi quali elementi aggiunti a un carrello, collegamenti su cui si fa clic e video visualizzati. Il valore del comportamento può diminuire nel tempo. |
| Spazio dei nomi dell’identità (identità) | Quando i dati dei clienti si uniscono, vengono uniti in un unico profilo tramite l&#39;utilizzo di **spazi dei nomi di identità** e la possibilità di unire queste identità man mano che si acquisiscono ulteriori informazioni sull&#39;utente. Per ulteriori informazioni, consulta la [panoramica sugli spazi dei nomi delle identità](../../identity-service/features/namespaces.md). |

{style="table-layout:auto"}

#### Rapporti composizione archivio profili

Sono disponibili diversi rapporti per comprendere la composizione dell’archivio Profili. Questi rapporti ti aiutano a prendere decisioni informate su come e dove impostare le scadenze degli eventi esperienza per ottimizzare l’utilizzo della licenza:

* **API report di sovrapposizione set di dati**: espone i set di dati che contribuiscono maggiormente al pubblico indirizzabile. È possibile utilizzare questo report per identificare i [!DNL ExperienceEvent] set di dati per i quali impostare una scadenza. Per ulteriori informazioni, consulta l&#39;esercitazione su [generazione del report di sovrapposizione dei set di dati](../../profile/tutorials/dataset-overlap-report.md).
* **API rapporto di sovrapposizione identità**: espone gli spazi dei nomi delle identità che contribuiscono maggiormente al pubblico indirizzabile. Per ulteriori informazioni, consulta l&#39;esercitazione su [generazione del rapporto di sovrapposizione identità](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report).
<!-- * **Unknown Profiles Report API**: Exposes the impact of applying pseudonymous expirations for different time thresholds. You can use this report to identify which pseudonymous expirations threshold to apply. See the tutorial on [generating the unknown profiles report](../../profile/api/preview-sample-status.md#generate-the-unknown-profiles-report) for more information.
-->

#### Scadenze dati profilo pseudonimo {#pseudonymous-profile-expirations}

Questa funzionalità consente di rimuovere automaticamente i profili pseudonimi non aggiornati dall’archivio profili. Per ulteriori informazioni su questa funzione, leggere la [Panoramica sulla scadenza dei dati del profilo pseudonimo](../../profile/pseudonymous-profiles.md).

#### Scadenze degli eventi esperienza {#event-expirations}

Questa funzionalità ti consente di rimuovere automaticamente i dati comportamentali da un set di dati abilitato per il profilo che non è più utile per i tuoi casi d’uso. Per informazioni dettagliate sul funzionamento di questo processo dopo che è stato abilitato per un set di dati, consulta la panoramica sulle [scadenze evento esperienza](../../profile/event-expirations.md).

## Riepilogo delle best practice per la conformità dell’utilizzo delle licenze {#best-practices}

Di seguito è riportato un elenco di alcune best practice consigliate che è possibile seguire per garantire una migliore aderenza all’adesione all’utilizzo della licenza:

* Utilizza il [dashboard utilizzo licenze](../../dashboards/guides/license-usage.md) per monitorare e tenere traccia delle tendenze di utilizzo dei clienti. Questo ti consente di anticipare eventuali interruzioni del servizio.
* Configura [filtri di acquisizione](#ingestion-filters) identificando gli eventi necessari per i casi di utilizzo di segmentazione e personalizzazione. Questo ti consente di inviare solo gli eventi importanti necessari per i tuoi casi d’uso.
* Assicurati di disporre solo di [set di dati abilitati per il profilo](#ingestion-filters) necessari per i casi di utilizzo di segmentazione e personalizzazione.
* Configura [Scadenze evento esperienza](#event-expirations) e [Scadenze dati profilo pseudonimo](#pseudonymous-profile-expirations) per dati ad alta frequenza come i dati Web.
* Controlla periodicamente i [report sulla composizione del profilo](#profile-store-composition-reports) per conoscere la composizione dell&#39;archivio profili. Questo consente di comprendere le origini dati che contribuiscono maggiormente al consumo delle licenze.

## Riepilogo delle funzioni e disponibilità {#feature-summary}

Le best practice e gli strumenti descritti in questo documento consentono di gestire meglio l’utilizzo dei diritti di licenza in Adobe Experience Platform. Questo documento verrà aggiornato con il rilascio di ulteriori funzioni che contribuiranno a fornire visibilità e controllo a tutti i clienti Experience Platform.

La tabella seguente illustra l’elenco delle funzioni attualmente disponibili per gestire al meglio il diritto all’utilizzo della licenza.

| Funzione | Descrizione |
| --- | --- |
| [Attiva/Disattiva set di dati per il profilo](../../catalog/datasets/user-guide.md) | Abilita o disabilita l’acquisizione di set di dati in Real-Time Customer Profile. |
| [Scadenze evento esperienza](../../profile/event-expirations.md) | Applica un tempo di scadenza per tutti gli eventi acquisiti in un set di dati abilitato per il profilo. Per abilitare questa funzione, contatta il team del tuo account di Adobe o l’Assistenza clienti. |
| [Filtri per la preparazione dati di Adobe Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md) | Applica i filtri [!DNL Kafka] per escludere i dati non necessari dall’acquisizione |
| [Filtri del connettore di origine di Adobe Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) | Applica i filtri di connessione di origine dell’Audience Manager per escludere i dati non necessari dall’acquisizione |
| [Filtri dati inoltro eventi](../../tags/ui/event-forwarding/overview.md) | Applica i filtri [!DNL Kafka] lato server per escludere i dati non necessari dall&#39;acquisizione.  Per ulteriori informazioni, consulta la documentazione sulle [regole tag](../../tags/ui/managing-resources/rules.md). |
| [Interfaccia utente dashboard utilizzo licenze](../../dashboards/guides/license-usage.md#license-usage-dashboard-data) | Visualizza un’istantanea dei dati relativi alla licenza della tua organizzazione, ad Experience Platform |
| [API report di sovrapposizione set di dati](../../profile/tutorials/dataset-overlap-report.md) | Restituisce i set di dati che contribuiscono maggiormente al pubblico indirizzabile |
| [API report di sovrapposizione identità](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) | Restituisce gli spazi dei nomi di identità che contribuiscono maggiormente al pubblico indirizzabile |

{style="table-layout:auto"}
