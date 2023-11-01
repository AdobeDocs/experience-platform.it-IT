---
title: Best practice per l’adesione alle licenze di gestione dati
description: Scopri le best practice da seguire e gli strumenti che puoi utilizzare per gestire al meglio i diritti alle licenze con Adobe Experience Platform.
exl-id: f23bea28-ebd2-4ed4-aeb1-f896d30d07c2
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '2283'
ht-degree: 2%

---

# Best practice per l’adesione alle licenze di gestione dati

Adobe Experience Platform è un sistema aperto che trasforma i tuoi dati in solidi profili cliente da aggiornare in tempo reale e utilizza informazioni basate sull’intelligenza artificiale per aiutarti a fornire le esperienze giuste su ogni canale. Puoi acquisire dati di tipi, volumi e storie diversi per Experience Platform utilizzando le origini e quindi gestire tali dati per casi d’uso che vanno dalla segmentazione e personalizzazione all’analisi e all’apprendimento automatico.

Platform offre licenze che stabiliscono il numero di profili che è possibile creare e la quantità di dati che è possibile inserire. Data la capacità di inserire qualsiasi origine, volume o cronologia di dati, è possibile superare i diritti di licenza man mano che i volumi di dati aumentano.

Questo documento illustra le best practice da seguire e gli strumenti che puoi utilizzare per gestire al meglio i diritti alle licenze con Adobe Experience Platform.

## Informazioni sull&#39;archiviazione dei dati Adobe Experience Platform

Experience Platform è composto principalmente da due archivi di dati: [!DNL data lake] e nell’archivio Profili.

Il **[!DNL data lake]** ha principalmente i seguenti scopi:

* funge da area di gestione temporanea per l’onboarding dei dati in Experienci Platform;
* funge da archiviazione dei dati a lungo termine per tutti i dati Experienci Platform;
* Abilita casi d’uso come analisi dei dati e data science.

Il **Archivio profili** è dove vengono creati i profili dei clienti e serve principalmente per i seguenti scopi:

* Funge da archivio dati per i profili utilizzati per supportare esperienze in tempo reale;
* Abilita casi d’uso come segmentazione, attivazione e personalizzazione.

>[!NOTE]
>
>L&#39;accesso a [!DNL data lake] può dipendere dallo SKU del prodotto acquistato. Per ulteriori informazioni sugli SKU dei prodotti, contatta il rappresentante del tuo Adobe.

## Utilizzo delle licenze {#license-usage}

Quando si riceve la licenza di Experience Platform, vengono forniti diritti di utilizzo della licenza che variano a seconda dello SKU:

**[!DNL Addressable Audience]** - il numero totale di profili cliente consentiti contrattualmente in Experienci Platform, inclusi i profili noti e pseudonimi.

**[!DNL Profile Richness]** : la dimensione media dei dati del profilo in Experienci Platform. Puoi aumentare il tuo [!DNL Profile Richness] acquistando un pacchetto richness.

Il [!DNL Profile Richness] La metrica varia a seconda della licenza acquistata. Esistono due calcoli per [!DNL Profile Richness] disponibile:

* La somma di tutti i dati di produzione memorizzati in Adobe Real-time Customer Data Platform (ovvero Profilo cliente in tempo reale e Servizio identità) in qualsiasi momento, divisa per [!DNL Addressable Audience];
* La somma di tutti i dati memorizzati in Platform (inclusi, ma non limitati a [!DNL data lake], Real-Time Customer Profile e Identity Service) in qualsiasi momento e tutti i dati trasmessi tramite (anziché archiviati all’interno di) Platform negli ultimi 12 mesi, divisi per [!DNL Addressable Audience].

La disponibilità di queste metriche e la definizione specifica di ciascuna di esse varia a seconda delle licenze acquistate dalla tua organizzazione.

## Dashboard utilizzo licenze

L’interfaccia utente di Adobe Experience Platform fornisce un dashboard tramite il quale puoi visualizzare un’istantanea dei dati relativi alla licenza della tua organizzazione per Platform. I dati nel dashboard vengono visualizzati esattamente come appaiono nel momento specifico in cui è stata acquisita l’istantanea. L’istantanea non è né un’approssimazione né un campione di dati e il dashboard non viene aggiornato in tempo reale.

Per ulteriori informazioni, consulta la guida su [utilizzo del dashboard utilizzo licenze nell’interfaccia utente di Platform](../../dashboards/guides/license-usage.md#license-usage-dashboard-data).

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

I dati possono essere acquisiti in uno o più sistemi in Platform, ovvero [!DNL data lake] e/o nell’archivio Profili. Ciò significa che in entrambi i sistemi possono esistere dati diversi per una varietà di casi d’uso diversi. Ad esempio, potrebbe essere utile conservare i dati storici nel [!DNL data lake], ma non nell’archivio Profili. Per selezionare i dati da inviare all’archivio profili, abilita un set di dati per l’acquisizione del profilo.

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

Tuttavia, i limiti del grafo delle identità possono influenzare il pubblico indirizzabile a causa della suddivisione delle identità. Ad esempio, se l’ECID più vecchio viene rimosso dal grafico, ECID continuerà a esistere in Real-Time Customer Profile come profilo pseudonimo. È possibile impostare [Scadenze dati profilo pseudonimo](../../profile/pseudonymous-profiles.md) per aggirare questo comportamento. Per ulteriori informazioni, leggere [guardrail per i dati del servizio Identity](../../identity-service/guardrails.md).

### Filtri di acquisizione {#ingestion-filters}

I filtri di acquisizione consentono di inserire solo i dati necessari per i casi d’uso e di escludere tutti gli eventi non necessari.

| Filtro di acquisizione | Descrizione |
| --- | --- |
| Filtro origine Adobe Audience Manager | Quando crei una connessione sorgente Adobe Audience Manager, puoi scegliere quali segmenti e caratteristiche inserire nella [!DNL data lake] e Real-Time Customer Profile, anziché acquisire i dati Audienci Manager nella loro interezza. Consulta la guida su [creazione di una connessione sorgente Audienci Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) per ulteriori informazioni. |
| Preparazione dati di Adobe Analytics | È possibile utilizzare [!DNL Data Prep] funzionalità durante la creazione di una connessione di origine Analytics per filtrare i dati non necessari per i casi d’uso. Da a [!DNL Data Prep], puoi definire gli attributi o le colonne da pubblicare nel profilo. Puoi anche fornire istruzioni condizionali per informare Platform se i dati devono essere pubblicati nel profilo o solo nel [!DNL data lake]. Consulta la guida su [creazione di una connessione sorgente Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md) per ulteriori informazioni. |
| Supporto per abilitare/disabilitare i set di dati per il profilo | Per acquisire dati nel Profilo cliente in tempo reale, devi abilitare un set di dati da utilizzare nell’archivio Profili. In questo modo, aggiunge al tuo [!DNL Addressable Audience] e [!DNL Profile Richness] diritti. Una volta che un set di dati non è più necessario per i casi di utilizzo del profilo cliente, puoi disabilitare l’integrazione del set di dati con Profilo per garantire che i dati rimangano conformi alla licenza. Consulta la guida su [abilitazione e disabilitazione dei set di dati per il profilo](../../catalog/datasets/enable-for-profile.md) per ulteriori informazioni. |
| Esclusione di dati SDK per web e SDK per dispositivi mobili | Esistono due tipi di dati raccolti da Web e Mobile SDK: dati raccolti automaticamente e dati raccolti esplicitamente dallo sviluppatore. Per gestire meglio la conformità della licenza, puoi disabilitare la raccolta automatica dei dati nella configurazione dell’SDK tramite l’impostazione contestuale. I dati personalizzati possono anche essere rimossi o non impostati dallo sviluppatore. Consulta la guida su [configurazione delle nozioni di base dell’SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#fundamentals) per ulteriori informazioni. |
| Esclusione dei dati di inoltro lato server | Se invii dati a Platform utilizzando l’inoltro lato server, puoi escludere i dati inviati rimuovendo la mappatura in un’azione della regola per escluderla in tutti gli eventi oppure aggiungendo condizioni alla regola in modo che i dati vengano attivati solo per determinati eventi. Consulta la documentazione su [eventi e condizioni](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/rules.html#events-and-conditions-(if) per ulteriori informazioni. |
| Filtrare i dati a livello di origine | Puoi utilizzare operatori logici e di confronto per filtrare i dati a livello di riga dalle origini prima di creare una connessione e acquisire i dati da Experienci Platform. Per ulteriori informazioni, consulta la guida su [filtrare i dati a livello di riga per un&#39;origine utilizzando [!DNL Flow Service] API](../../sources/tutorials/api/filter.md). |

{style="table-layout:auto"}

### Archivio profili {#profile-service}

L’archivio Profili è composto dai seguenti componenti:

| Componente archivio profili | Descrizione |
| --- | --- |
| Frammenti di profilo | Ogni profilo cliente è composto da più **frammenti di profilo** che sono stati uniti per formare un’unica vista del cliente. Ad esempio, se un cliente interagisce con il tuo marchio attraverso diversi canali, la tua organizzazione avrà più **frammenti di profilo** relativo al singolo cliente visualizzato in più set di dati. Quando questi frammenti vengono acquisiti in Platform, vengono uniti utilizzando il grafico delle identità per creare un singolo profilo per quel cliente. **Frammenti di profilo** consistere in uno spazio dei nomi di identità come identificatore, con dati di record e/o dati di serie temporali associati. |
| Registra dati (attributi) | Un profilo è una rappresentazione di un soggetto, un’organizzazione o un individuo, composta da molti **Attributi** (noto anche come **registrare dati**). Ad esempio, il profilo di un prodotto può includere uno SKU e una descrizione, mentre il profilo di una persona contiene informazioni come nome, cognome e indirizzo e-mail. **Registra dati** di solito ha un volume basso/moderato, ma è utile per lunghi periodi di tempo. |
| Dati delle serie temporali (Comportamento) | **Dati delle serie temporali** fornisce informazioni sul comportamento di un utente. Rappresentata dalla classe di schema standard Experience Data Model (XDM) [!DNL ExperienceEvent], i dati delle serie temporali possono descrivere eventi quali elementi aggiunti al carrello, collegamenti su cui viene fatto clic e video visualizzati. Il valore del comportamento può diminuire nel tempo. |
| Spazio dei nomi dell’identità (identità) | Quando i dati del cliente si uniscono, vengono uniti in un unico profilo tramite l’utilizzo di **spazi dei nomi di identità** e la possibilità di unire queste identità man mano che si acquisiscono maggiori informazioni sull’utente. Consulta la [panoramica degli spazi dei nomi delle identità](../../identity-service/namespaces.md) per ulteriori informazioni. |

{style="table-layout:auto"}

#### Rapporti composizione archivio profili

Sono disponibili diversi rapporti per comprendere la composizione dell’archivio Profili. Questi rapporti ti aiutano a prendere decisioni informate su come e dove impostare le scadenze degli eventi esperienza per ottimizzare l’utilizzo della licenza:

* **API del rapporto di sovrapposizione dei set di dati**: espone i set di dati che contribuiscono maggiormente al pubblico di riferimento. Puoi utilizzare questo rapporto per identificare quale [!DNL ExperienceEvent] set di dati per cui impostare una scadenza. Guarda il tutorial su [generazione del rapporto di sovrapposizione dei set di dati](../../profile/tutorials/dataset-overlap-report.md) per ulteriori informazioni.
* **API rapporto di sovrapposizione identità**: espone gli spazi dei nomi delle identità che contribuiscono maggiormente al pubblico indirizzabile. Guarda il tutorial su [generazione del rapporto di sovrapposizione identità](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) per ulteriori informazioni.
<!-- * **Unknown Profiles Report API**: Exposes the impact of applying pseudonymous expirations for different time thresholds. You can use this report to identify which pseudonymous expirations threshold to apply. See the tutorial on [generating the unknown profiles report](../../profile/api/preview-sample-status.md#generate-the-unknown-profiles-report) for more information.
-->

#### Scadenze dati profilo pseudonimo {#pseudonymous-profile-expirations}

Questa funzionalità consente di rimuovere automaticamente i profili pseudonimi non aggiornati dall’archivio profili. Per ulteriori informazioni su questa funzione, leggere [Panoramica sulla scadenza dei dati del profilo pseudonimo](../../profile/pseudonymous-profiles.md).

#### Scadenze degli eventi esperienza {#event-expirations}

Questa funzionalità ti consente di rimuovere automaticamente i dati comportamentali da un set di dati abilitato per il profilo che non è più utile per i tuoi casi d’uso. Consulta la panoramica su [Scadenze degli eventi esperienza](../../profile/event-expirations.md) per informazioni dettagliate sul funzionamento di questo processo dopo che è stato abilitato per un set di dati.

## Riepilogo delle best practice per la conformità dell’utilizzo delle licenze {#best-practices}

Di seguito è riportato un elenco di alcune best practice consigliate che è possibile seguire per garantire una migliore aderenza all’adesione all’utilizzo della licenza:

* Utilizza il [dashboard utilizzo licenze](../../dashboards/guides/license-usage.md) per monitorare e tenere traccia delle tendenze di utilizzo dei clienti. Questo ti consente di anticipare eventuali interruzioni del servizio.
* Configura [filtri di acquisizione](#ingestion-filters) identificando gli eventi necessari per i casi di utilizzo di segmentazione e personalizzazione. Questo ti consente di inviare solo gli eventi importanti necessari per i tuoi casi d’uso.
* Assicurati di avere solo [set di dati abilitati per il profilo](#ingestion-filters) necessari per i casi di utilizzo di segmentazione e personalizzazione.
* Configura [Scadenze degli eventi esperienza](#event-expirations) e [Scadenze dati profilo pseudonimo](#pseudonymous-profile-expirations) per dati ad alta frequenza come i dati web.
* Controlla periodicamente [Report composizione profilo](#profile-store-composition-reports) per comprendere la composizione dell’archivio profili. Questo consente di comprendere le origini dati che contribuiscono maggiormente al consumo delle licenze.

## Riepilogo delle funzioni e disponibilità {#feature-summary}

Le best practice e gli strumenti descritti in questo documento consentono di gestire meglio l’utilizzo dei diritti di licenza in Adobe Experience Platform. Questo documento verrà aggiornato con il rilascio di ulteriori funzioni che contribuiranno a fornire visibilità e controllo a tutti i clienti Experienci Platform.

La tabella seguente illustra l’elenco delle funzioni attualmente disponibili per gestire al meglio il diritto all’utilizzo della licenza.

| Funzione | Descrizione |
| --- | --- |
| [Abilitare/disabilitare i set di dati per il profilo](../../catalog/datasets/user-guide.md) | Abilita o disabilita l’acquisizione di set di dati in Real-Time Customer Profile. |
| [Scadenze degli eventi esperienza](../../profile/event-expirations.md) | Applica un tempo di scadenza per tutti gli eventi acquisiti in un set di dati abilitato per il profilo. Per abilitare questa funzione, contatta il team del tuo account di Adobe o l’Assistenza clienti. |
| [Filtri per la preparazione dati di Adobe Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md) | Applica [!DNL Kafka] filtri per escludere i dati non necessari dall’acquisizione |
| [Filtri del connettore di origine di Adobe Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) | Applica i filtri di connessione di origine dell’Audience Manager per escludere i dati non necessari dall’acquisizione |
| [Filtri dati di Alloy SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#fundamentals) | Applicare i filtri di lega per escludere i dati non necessari dall’acquisizione |
| [Filtri dati inoltro eventi](../../tags/ui/event-forwarding/overview.md) | Applica lato server [!DNL Kafka] filtri per escludere i dati non necessari dall’acquisizione.  Consulta la documentazione su [regole di tag](../../tags/ui/managing-resources/rules.md) per ulteriori informazioni. |
| [Interfaccia utente dashboard utilizzo licenze](../../dashboards/guides/license-usage.md#license-usage-dashboard-data) | Visualizza un’istantanea dei dati relativi alla licenza della tua organizzazione, ad Experience Platform |
| [API del rapporto di sovrapposizione dei set di dati](../../profile/tutorials/dataset-overlap-report.md) | Restituisce i set di dati che contribuiscono maggiormente al pubblico indirizzabile |
| [API rapporto di sovrapposizione identità](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) | Restituisce gli spazi dei nomi di identità che contribuiscono maggiormente al pubblico indirizzabile |

{style="table-layout:auto"}
