---
keywords: Experience Platform;home;argomenti comuni;gestione dati;adesione licenze;licenze;best practice
title: Tecniche consigliate per l’abilitazione delle licenze di gestione dei dati
description: Questo documento illustra le best practice da seguire e gli strumenti che puoi utilizzare per gestire al meglio i diritti alle licenze con Adobe Experience Platform.
exl-id: f23bea28-ebd2-4ed4-aeb1-f896d30d07c2
source-git-commit: 02882957fc38058ff092938d631e290725d4bdc2
workflow-type: tm+mt
source-wordcount: '2531'
ht-degree: 2%

---

# Best practice per l’abilitazione alla licenza di gestione dati

Adobe Experience Platform è un sistema aperto che trasforma i dati in solidi profili cliente che si aggiornano in tempo reale e utilizza informazioni basate sull’intelligenza artificiale per aiutarti a fornire le esperienze giuste su ogni canale. È possibile inserire dati di tipi, volumi e cronologia diversi per Experience Platform utilizzando le origini e quindi gestire tali dati in casi d’uso che vanno dalla segmentazione e la personalizzazione all’analisi e all’apprendimento automatico.

Platform offre licenze che stabiliscono il numero di profili che puoi creare e la quantità di dati che puoi inserire. Data la capacità di inserire qualsiasi origine, volume o cronologia di dati, è possibile superare le autorizzazioni per le licenze man mano che i volumi di dati aumentano.

Questo documento illustra le best practice da seguire e gli strumenti che puoi utilizzare per gestire al meglio i diritti alle licenze con Adobe Experience Platform.

## Informazioni sull’archiviazione dati di Adobe Experience Platform

Experience Platform è composto principalmente da due archivi di dati: la [!DNL Data Lake] e dall&#39;archivio profili.

La **[!DNL Data Lake]** svolge principalmente i seguenti scopi:

* agisce come area di staging per l’inserimento dei dati nell’Experience Platform;
* agisce come archiviazione a lungo termine dei dati per tutti i dati di Experience Platform;
* Abilita casi d’uso come l’analisi dei dati e la scienza dei dati.

La **Archivio profili** è il luogo in cui vengono creati i profili dei clienti e svolge principalmente i seguenti scopi:

* agisce come archiviazione di dati per i profili utilizzati per supportare esperienze in tempo reale;
* Abilita casi d’uso come segmentazione, attivazione e personalizzazione.

>[!NOTE]
>
>Accesso al [!DNL Data Lake] può dipendere dallo SKU del prodotto acquistato. Per ulteriori informazioni sugli SKU dei prodotti, contatta il tuo rappresentante Adobe.

## Utilizzo delle licenze {#license-usage}

Quando si concede l’Experience Platform di licenza, l’utente dispone di diritti di utilizzo della licenza che variano a seconda della SKU:

**[!DNL Addressable Audience]** - il numero totale di profili cliente contrattualmente consentiti in Experience Platform, inclusi profili noti e pseudonimi.

**[!DNL Profile Richness]** - la dimensione media dei dati del profilo, ad Experience Platform. È possibile aumentare [!DNL Profile Richness] diritto acquistando un ricco pacchetto.

La [!DNL Profile Richness] varia a seconda della licenza acquistata. Sono disponibili due calcoli per [!DNL Profile Richness] disponibile:

* La somma di tutti i dati di produzione archiviati in Real-time Customer Data Platform (ad esempio, Servizio profilo e Servizio identità) in qualsiasi momento, divisa per [!DNL Addressable Audience];
* La somma di tutti i dati archiviati in Platform (compresi, tra l’altro, [!DNL Data Lake], Servizio profilo e Servizio identità) in qualsiasi momento e con tutti i dati in cui è in corso lo streaming (anziché l’archiviazione all’interno di) Platform negli ultimi 12 mesi, suddivisi per [!DNL Addressable Audience].

La disponibilità di queste metriche e la definizione specifica di ciascuna di esse variano a seconda della licenza acquistata dalla tua organizzazione.

## Dashboard di utilizzo licenze

L’interfaccia utente di Adobe Experience Platform fornisce un dashboard tramite il quale è possibile visualizzare un’istantanea dei dati relativi alla licenza dell’organizzazione per Platform. I dati nel dashboard vengono visualizzati esattamente come vengono visualizzati nel momento specifico in cui è stata scattata l&#39;istantanea. Lo snapshot non è né un&#39;approssimazione né un campione di dati e il dashboard non viene aggiornato in tempo reale.

Per ulteriori informazioni, consulta la guida su [utilizzo del dashboard di utilizzo della licenza nell’interfaccia utente di Platform](../../dashboards/guides/license-usage.md#license-usage-dashboard-data).

## Best practice per la gestione dei dati

Le sezioni seguenti descrivono le best practice da seguire per gestire meglio i dati.

### Informazioni sui dati

Non tutti i dati sono gli stessi in Adobe Experience Platform. Alcuni dati possono essere densi, ma di valore basso, mentre altri possono essere sparsi, ma di valore elevato. Alcuni dati possono perdere valore non appena generati, mentre altri possono essere preziosi per mesi, se non anni.

Ci sono tre dimensioni da considerare per comprendere il valore dei dati:

| Dimensione | Descrizione | Esempio |
| --- | --- | --- |
| Volume | Rappresenta la quantità e la totalità dei dati acquisiti. | Clic sul web: volume elevato e fedeltà moderata. Il valore può diminuire rapidamente. |
| Intervallo temporale | Rappresenta il periodo di tempo in cui i dati acquisiti rimangono preziosi. | Acquisti offline - moderati in volume e fedeltà, ma possono essere utili per lunghi periodi di tempo. |
| Fedeltà | Rappresenta il livello di ricchezza dei dati con le informazioni. | Account cliente - volume basso, ma alta fedeltà. Può essere utile oltre la durata di un cliente. |

### Strumenti di gestione dati {#data-management-tools}

Esistono due scenari centrali da considerare per garantire che l’utilizzo dei dati rimanga entro i limiti di autorizzazione della licenza:

### Quali dati inserire in Platform?

I dati possono essere acquisiti in uno o più sistemi in Platform, ovvero [!DNL Data Lake] e/o nell’archivio profili. Ciò significa che in entrambi i sistemi possono esistere dati diversi per diversi casi d’uso. Ad esempio, è possibile conservare i dati storici nel [!DNL Data Lake], ma non nell’archivio profili. Puoi selezionare i dati da inviare all’archivio profili abilitando un set di dati per l’acquisizione del profilo.

>[!NOTE]
>
>Accesso al [!DNL Data Lake] può dipendere dallo SKU del prodotto acquistato. Per ulteriori informazioni sugli SKU dei prodotti, contatta il tuo rappresentante Adobe.

### Quali dati conservare?

Puoi applicare sia i filtri di acquisizione dei dati che le regole di scadenza (noti anche come TTL Time-To-Live) per rimuovere i dati che sono diventati obsoleti per i tuoi casi d’uso. In genere, i dati comportamentali (come i dati di Analytics) consumano molto più spazio di archiviazione dei dati di record (come i dati CRM). Ad esempio, molti utenti di Platform hanno fino al 90% di profili compilati da soli con dati comportamentali, rispetto ai dati di record. Pertanto, la gestione dei dati comportamentali è fondamentale per garantire la conformità all’interno delle adesioni alla licenza.

Sono disponibili diversi strumenti che puoi sfruttare per mantenere i diritti di utilizzo della licenza:

* [Filtri di acquisizione](#ingestion-filters)
* [TTL servizio profilo](#profile-service)

### Filtri di acquisizione {#ingestion-filters}

I filtri di acquisizione ti consentono di inserire solo i dati necessari per i casi d’uso e di filtrare tutti gli eventi non richiesti.

| Filtro di acquisizione | Descrizione |
| --- | --- |
| Filtro sorgente Adobe Audience Manager | Quando crei una connessione sorgente Adobe Audience Manager, puoi scegliere i segmenti e le caratteristiche da inserire nella [!DNL Data Lake] e il servizio Profilo, anziché acquisire i dati Audienci Manager nella loro interezza. Consulta la guida su [creazione di una connessione sorgente Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) per ulteriori informazioni. |
| Preparazione dei dati di Adobe Analytics | È possibile utilizzare [!DNL Data Prep] funzionalità durante la creazione di una connessione di origine Analytics per filtrare i dati non necessari per i casi d’uso. Attraverso [!DNL Data Prep], puoi definire gli attributi/colonne da pubblicare su Profilo. Puoi anche fornire istruzioni condizionali per informare Platform se i dati devono essere pubblicati su Profilo o solo su [!DNL Data Lake]. Consulta la guida su [creazione di una connessione sorgente Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md) per ulteriori informazioni. |
| Supporto per i set di dati di attivazione/disattivazione per il profilo | Per acquisire dati nel servizio Profilo, devi abilitare un set di dati da utilizzare nell’archivio profili. In questo modo, aggiunge al tuo [!DNL Addressable Audience] e [!DNL Profile Richness] diritti. Una volta che un set di dati non è più necessario per i casi di utilizzo del profilo del cliente, puoi disattivare l’integrazione del set di dati con Profilo per garantire che i dati rimangano conformi alla licenza. Consulta la guida su [abilitazione e disabilitazione dei set di dati per il profilo](../../catalog/datasets/enable-for-profile.md) per ulteriori informazioni. |
| Esclusione di dati SDK per web e SDK per dispositivi mobili | Esistono due tipi di dati raccolti dall’SDK per web e dispositivi mobili: i dati raccolti automaticamente e quelli raccolti esplicitamente dallo sviluppatore. Per gestire meglio la conformità delle licenze, puoi disabilitare la raccolta automatica dei dati nella configurazione dell&#39;SDK tramite l&#39;impostazione del contesto. I dati personalizzati possono anche essere rimossi o non impostati dallo sviluppatore. Consulta la guida su [configurazione delle basi dell’SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en#fundamentals) per ulteriori informazioni. |
| Esclusione dei dati dell&#39;inoltro lato server | Se invii dati a Platform utilizzando l’inoltro lato server, puoi escludere quali dati vengono inviati rimuovendo la mappatura in un’azione della regola per escluderla tra tutti gli eventi, oppure aggiungendo condizioni alla regola in modo che i dati vengano attivati solo per determinati eventi. Consulta la documentazione su [eventi e condizioni](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/rules.html#events-and-conditions-(if)) per ulteriori informazioni. |

{style=&quot;table-layout:auto&quot;}

### Servizio profili {#profile-service}

La funzionalità TTL (time-to-live) del servizio profilo ti consente di applicare il TTL ai dati nell’archivio profili. In questo modo il sistema può rimuovere automaticamente i dati il cui valore è diminuito nel tempo.

L’archivio profili è composto dai seguenti componenti:

| Componente archivio profili | Descrizione |
| --- | --- |
| Frammenti di profilo | Ciascun profilo cliente è composto da più **frammenti di profilo** che sono stati uniti per formare una singola vista del cliente. Ad esempio, se un cliente interagisce con il tuo marchio su più canali, l’organizzazione avrà più canali **frammenti di profilo** relativo a quel singolo cliente che viene visualizzato in più set di dati. Quando questi frammenti vengono acquisiti in Platform, vengono uniti utilizzando il grafico delle identità per creare un singolo profilo per quel cliente. **Frammenti di profilo** sono costituiti da uno spazio dei nomi di identità come identificatore, con i dati del record associati e/o i dati delle serie temporali associati. |
| Dati record (Attributi) | Un profilo è una rappresentazione di un soggetto, un&#39;organizzazione o un individuo, composto da molti **Attributi** (noto anche come **record dati**). Ad esempio, il profilo di un prodotto può includere una SKU e una descrizione, mentre il profilo di una persona contiene informazioni come nome, cognome e indirizzo e-mail. **Registra dati** di solito è basso/moderato in volume, ma valido per lunghi periodi di tempo. |
| Dati delle serie temporali (comportamento) | **Dati della serie temporale** fornisce informazioni su un comportamento utente. Rappresentato dalla classe schema standard Experience Data Model (XDM) [!DNL ExperienceEvent], i dati delle serie temporali possono descrivere eventi quali elementi aggiunti al carrello, collegamenti su cui si fa clic e video visualizzati. Il valore dei comportamenti può diminuire nel tempo. |
| Spazio dei nomi identità (identità) | Man mano che i dati dei clienti si combinano, vengono uniti in un unico profilo utilizzando **spazi dei nomi delle identità** e la possibilità di unire queste identità man mano che più informazioni vengono note sull&#39;utente. Consulta la sezione [panoramica dei namespace delle identità](../../identity-service/namespaces.md) per ulteriori informazioni. |

{style=&quot;table-layout:auto&quot;}

#### Rapporti sulla composizione dell’archivio profili

Sono disponibili diversi rapporti per comprendere la composizione dell’archivio profili. Questi rapporti ti aiutano a prendere decisioni informate su come e dove impostare i TTL del profilo per ottimizzare meglio l’utilizzo della licenza:

* **API rapporto di sovrapposizione set di dati**: Espone i set di dati che contribuiscono maggiormente al pubblico indirizzabile. Puoi utilizzare questo rapporto per identificare quale [!DNL ExperienceEvent] set di dati per cui impostare un TTL. Guarda l’esercitazione su [generazione del rapporto di sovrapposizione set di dati](../../profile/tutorials/dataset-overlap-report.md) per ulteriori informazioni.
* **API del rapporto di sovrapposizione identità**: Espone i namespace di identità che contribuiscono maggiormente al pubblico indirizzabile. Guarda l’esercitazione su [generazione del rapporto di sovrapposizione identità](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) per ulteriori informazioni.
<!-- * **Unknown Profiles Report API**: Exposes the impact of applying pseudonymous TTL for different time thresholds. You can use this report to identify which pseudonymous TTL threshold to apply. See the tutorial on [generating the unknown profiles report](../../profile/api/preview-sample-status.md#generate-the-unknown-profiles-report) for more information.
-->

#### [!DNL ExperienceEvent] TTL set di dati {#dataset-ttl}

Puoi applicare il TTL ai set di dati abilitati per il profilo per rimuovere dall’archivio profili i dati comportamentali che non sono più utili per i casi d’uso. Una volta applicato il TTL a un set di dati abilitato per il profilo, Platform rimuove automaticamente i dati non più necessari tramite un processo in due parti:

* Tutti i nuovi dati che avanzano avranno il valore di scadenza TTL applicato al momento dell’acquisizione;
* Tutti i dati esistenti avranno il valore di scadenza TTL applicato come parte di un processo di backfill del sistema una tantum.

È possibile prevedere che il valore TTL per ogni evento sia dalla marca temporale dell’evento. Tutti gli eventi precedenti al valore di scadenza TTL vengono eliminati immediatamente durante l&#39;esecuzione del processo di sistema. Tutti gli altri eventi vengono eliminati quando si avvicinano al valore di scadenza TTL indicato nella marca temporale dell’evento.

Vedi l&#39;esempio seguente per comprendere meglio [!DNL ExperienceEvent] TTL set di dati.

Se applichi un valore TTL di 30 giorni il 15 maggio, allora:

* A tutti i nuovi eventi verrà applicato un TTL di 30 giorni al loro arrivo;
* Tutti gli eventi esistenti con una marca temporale precedente al 15 aprile vengono eliminati immediatamente da un processo di sistema.;
* Gli eventi che hanno una marca temporale dopo il 15 aprile avranno una scadenza del timestamp dell’evento + dei giorni TTL. Quindi, un evento con una marca temporale del 18 aprile terminerà tre giorni dopo il 15 maggio.

>[!IMPORTANT]
>
>Una volta applicato un TTL, tutti i dati più vecchi del numero TTL selezionato verranno **permanentemente** eliminato e non può essere ripristinato.

Prima di applicare il TTL, è necessario assicurarsi di mantenere un intervallo di lookback di qualsiasi segmento all’interno del limite TTL. In caso contrario, i risultati del segmento potrebbero diventare errati dopo l’applicazione del TTL. Ad esempio, se hai applicato un TTL di 30 giorni per i dati di Adobe Analytics e un TTL di 365 giorni per i dati delle transazioni in-store, il segmento seguente creerà risultati errati:

* Pagina prodotto visualizzata negli ultimi 60 giorni seguita da un acquisto in negozio;
* Aggiungi al carrello seguito da nessun acquisto negli ultimi 60 giorni.

Al contrario, i seguenti risultati creeranno comunque corretti:

* Pagina prodotto visualizzata negli ultimi 14 giorni seguita da un acquisto in negozio;
* È stata visualizzata una pagina di aiuto specifica online negli ultimi 30 giorni;
* ha acquistato un prodotto offline negli ultimi 120 giorni;
* Aggiunto al carrello seguito da acquisto negli ultimi 14 giorni.

>[!TIP]
>
>Per comodità, puoi mantenere lo stesso TTL per tutti i set di dati, in modo da non doverti preoccupare dell’impatto TTL tra i set di dati nella logica di segmentazione.

Per ulteriori informazioni sull’applicazione di TTL ai dati del profilo, consulta la documentazione su [TTL servizio profilo](../../profile/apply-ttl.md).

## Riepilogo delle best practice per la conformità all’utilizzo delle licenze {#best-practices}

Di seguito è riportato un elenco di alcune best practice consigliate da seguire per garantire una migliore aderenza all’adesione all’utilizzo della licenza:

* Utilizza la [dashboard di utilizzo della licenza](../../dashboards/guides/license-usage.md) per monitorare e monitorare le tendenze di utilizzo dei clienti. Questo ti consente di superare eventuali overage potenziali che potrebbero verificarsi.
* Configura [filtri di acquisizione](#ingestion-filters) identificando gli eventi necessari per i casi d’uso di segmentazione e personalizzazione. Questo consente di inviare solo gli eventi importanti richiesti per i casi d’uso.
* Assicurati di avere solo [set di dati abilitati per il profilo](#ingestion-filters) necessari per i casi d’uso di segmentazione e personalizzazione.
* Configura un [[!DNL ExperienceEvent] TTL set di dati](#dataset-ttl) per dati ad alta frequenza come i dati web.
* Controlla periodicamente il [Rapporti sulla composizione dei profili](#profile-store-composition-reports) per comprendere la composizione dell’archivio profili. Ciò ti consente di comprendere le origini dati che contribuiscono maggiormente al consumo di licenze.

## Riepilogo delle funzioni e disponibilità {#feature-summary}

Le best practice e gli strumenti descritti in questo documento ti aiuteranno a gestire meglio l’utilizzo dell’adesione alla licenza in Adobe Experience Platform. Questo documento verrà aggiornato man mano che vengono rilasciate funzioni aggiuntive per fornire visibilità e controllo a tutti i clienti di Experience Platform.

La tabella seguente illustra l’elenco delle funzionalità attualmente disponibili per gestire meglio i diritti di utilizzo della licenza.

| Funzione | Descrizione |
| --- | --- |
| [Attivare/disattivare i set di dati per il profilo](../../catalog/datasets/user-guide.md) | Abilitare o disabilitare l’acquisizione di set di dati in Profile Service |
| [!DNL ExperienceEvent] TTL set di dati | Applica una scadenza TTL per i set di dati comportamentali nell’archivio profili. Contatta il tuo rappresentante di supporto Adobe. |
| [Filtri di preparazione dei dati di Adobe Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md) | Applica [!DNL Kafka] filtri per escludere i dati non necessari dall’acquisizione |
| [Filtri del connettore sorgente Adobe Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) | Applicare filtri di connessione all’origine di Audience Manager per escludere i dati non necessari dall’acquisizione |
| [Filtri dati Alloy SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en#fundamentals) | Applicare filtri di lega per escludere i dati non necessari dall’acquisizione |
| [Filtri dati di inoltro eventi](../../tags/ui/event-forwarding/overview.md) | Applicare lato server [!DNL Kafka] filtri per escludere i dati non necessari dall’acquisizione.  Consulta la documentazione su [regole tag](../../tags/ui/managing-resources/rules.md) per ulteriori informazioni. |
| [Interfaccia utente del dashboard per l’utilizzo della licenza](../../dashboards/guides/license-usage.md#license-usage-dashboard-data) | Visualizzare un&#39;istantanea dei dati relativi alla licenza dell&#39;organizzazione, ad Experience Platform |
| [API rapporto di sovrapposizione set di dati](../../profile/tutorials/dataset-overlap-report.md) | Invia i set di dati che contribuiscono maggiormente al pubblico indirizzabile |
| [API del rapporto di sovrapposizione identità](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) | Invia i namespace di identità che contribuiscono maggiormente al pubblico indirizzabile |

{style=&quot;table-layout:auto&quot;}
