---
keywords: Experience Platform;home;argomenti popolari;controllo degli accessi;adobe admin console
solution: Experience Platform
title: Panoramica sul controllo degli accessi
description: Il controllo degli accessi per Adobe Experience Platform viene fornito tramite Adobe Admin Console. Questa funzionalità sfrutta i profili di prodotto in Admin Console, che collegano gli utenti con autorizzazioni e sandbox.
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: da3328e58b9009d80fea1c84e79fb14c9cc1ecf2
workflow-type: tm+mt
source-wordcount: '3279'
ht-degree: 0%

---

# Panoramica sul controllo degli accessi

Il controllo degli accessi per Adobe Experience Platform viene fornito tramite **[!UICONTROL Permissions]** in [Adobe Experience Cloud](https://experience.adobe.com/). Questa funzionalità sfrutta ruoli e criteri, che collegano gli utenti con autorizzazioni e sandbox.

## Gerarchia e flusso di lavoro di controllo degli accessi

Per configurare il controllo degli accessi per Experience Platform, è necessario disporre dei privilegi di amministratore di sistema o di prodotto per un’organizzazione che dispone di un prodotto Experience Platform. Il ruolo minimo che può concedere o revocare le autorizzazioni è quello di amministratore di prodotto. Altri ruoli di amministratore che possono gestire le autorizzazioni sono amministratori di sistema (senza restrizioni). Per ulteriori informazioni, consulta l&#39;articolo del Centro assistenza Adobe su [ruoli amministrativi](https://helpx.adobe.com/it/enterprise/using/admin-roles.html).

>[!NOTE]
>
>Da questo punto in poi, qualsiasi menzione di &quot;amministratore&quot; in questo documento si riferisce a un amministratore di prodotto o a un livello superiore (come descritto sopra).

Un flusso di lavoro di alto livello per l’ottenimento e l’assegnazione delle autorizzazioni di accesso può essere riassunto come segue:

- Dopo aver concesso la licenza per Adobe Experience Platform o un servizio applicazioni/app che utilizza Experience Platform, viene inviata un’e-mail all’amministratore specificato durante la gestione della licenza.
- L&#39;amministratore accede a [Adobe Admin Console](#adobe-admin-console) e seleziona **Adobe Experience Platform** dall&#39;elenco dei prodotti nella pagina della panoramica.
- Per concedere l&#39;accesso ad Experience Platform, si consiglia all&#39;amministratore di aggiungere utenti al profilo di prodotto predefinito: `AEP-Default-All-Users`.
- In Autorizzazioni di Experience Platform, l’amministratore può creare nuovi ruoli o modificare le autorizzazioni e gli utenti per qualsiasi ruolo esistente.
- Durante la creazione o la modifica di un ruolo, l&#39;amministratore aggiunge gli utenti al ruolo utilizzando la scheda **[!UICONTROL users]** e concede le autorizzazioni a tali utenti (ad esempio &quot;[!UICONTROL Read Datasets]&quot; o &quot;[!UICONTROL Manage Schemas]&quot;) modificando le autorizzazioni del ruolo. Analogamente, l’amministratore può assegnare l’accesso alle sandbox utilizzando la stessa opzione di modifica.
- Quando gli utenti accedono all’interfaccia utente di Experience Platform, il loro accesso alle funzionalità di Experience Platform è guidato dalle autorizzazioni concesse loro dal passaggio precedente. Se ad esempio un utente non dispone dell&#39;autorizzazione [!UICONTROL View Datasets], la scheda **[!UICONTROL Datasets]** nel menu laterale non sarà visibile all&#39;utente.

Per i passaggi più dettagliati su come gestire il controllo degli accessi in Experience Platform, consulta la [guida utente per il controllo degli accessi](./ui/overview.md).

Tutte le chiamate alle API di Experience Platform vengono convalidate per le autorizzazioni e restituiranno errori se le autorizzazioni appropriate non vengono trovate nel contesto utente corrente. Nell’interfaccia utente, gli elementi verranno nascosti o modificati a seconda delle autorizzazioni concesse all’utente corrente.

## Autorizzazioni {#platform-permissions}

[!UICONTROL Permissions] fornisce una posizione centrale per la gestione dell&#39;accesso ad Experience Platform per la tua organizzazione. Tramite [!UICONTROL Permissions] è possibile concedere a gruppi di utenti le autorizzazioni di accesso per varie funzionalità di Experience Platform, ad esempio [!UICONTROL Manage Datasets], [!UICONTROL View Datasets] o [!UICONTROL Manage Profiles].

### Ruoli

Nella sezione [!UICONTROL Roles], le autorizzazioni vengono assegnate agli utenti tramite l&#39;utilizzo di ruoli. I ruoli consentono di concedere autorizzazioni a uno o più utenti e contengono anche il loro accesso all’ambito delle sandbox assegnate loro tramite i ruoli. Gli utenti possono essere assegnati a uno o più ruoli appartenenti alla tua organizzazione.

### Ruoli predefiniti

Experience Platform viene fornito con due ruoli predefiniti preconfigurati. La tabella seguente illustra cosa viene fornito in ciascun profilo predefinito, inclusa la sandbox a cui concedono l’accesso e le autorizzazioni che concedono nell’ambito di tale sandbox.

| Ruolo | Accesso alla sandbox | Autorizzazioni |
| --- | --- | --- |
| Accesso predefinito per tutti gli elementi di produzione | Prod | Tutte le autorizzazioni applicabili ad Experience Platform, eccetto quelle per l’amministrazione delle sandbox. |
| Amministratori sandbox | N/D | Consente di accedere alla sandbox `Prod` e alle autorizzazioni di amministrazione della sandbox. |

## Sandbox e autorizzazioni

Le sandbox non di produzione sono una forma di virtualizzazione dei dati che consente di isolare i dati da altre sandbox e sono in genere utilizzate per esperimenti di sviluppo, test o test. Le autorizzazioni di un ruolo consentono agli utenti del ruolo di accedere alle funzioni di Experience Platform all’interno degli ambienti sandbox a cui hanno accesso. Una licenza Experience Platform predefinita ti offre cinque sandbox (una di produzione e quattro non di produzione). Puoi aggiungere pacchetti di dieci sandbox non di produzione per un massimo di 75 sandbox in totale. Per ulteriori informazioni, contatta l’amministratore della tua organizzazione o il tuo rappresentante commerciale Adobe.

Per ulteriori informazioni sulle sandbox in Experience Platform, consulta la [panoramica sulle sandbox](../sandboxes/home.md).

### Accesso alle sandbox

L’accesso alle sandbox viene gestito tramite i ruoli. Per i passaggi dettagliati su come abilitare l&#39;accesso a una sandbox per un ruolo, consulta la [guida ai ruoli di controllo dell&#39;accesso basati sull&#39;attributo](./abac/ui/roles.md).

Gli utenti possono essere autorizzati ad accedere a una o più sandbox all’interno di un ruolo. Se un utente è incluso in due o più ruoli, avrà accesso a tutte le sandbox incluse in tali ruoli.

L’autorizzazione &quot;Sandbox Management&quot; (Gestione sandbox) consente agli utenti di gestire, visualizzare o ripristinare le sandbox.

### Autorizzazioni delle risorse {#permissions}

Le autorizzazioni per le risorse consentono di accedere a funzionalità specifiche di Experience Platform. Le risorse sono suddivise in categorie che contengono un set di autorizzazioni rilevanti, che possono essere assegnate singolarmente ai ruoli.

In [!UICONTROL Permissions], l&#39;area di lavoro risorse di un ruolo visualizza le sandbox e le autorizzazioni attive per tale ruolo:

![Area di lavoro risorse di un ruolo con un elenco di categorie e autorizzazioni selezionate.](./images/permissions.png)

La tabella seguente illustra le categorie di risorse disponibili sia per Experience Platform che per le applicazioni gestite tramite Autorizzazioni:

| Categoria | Descrizione |
| --- | --- |
| [!DNL Adobe Mix Modeler] | Configurare, gestire e visualizzare le autorizzazioni per [!DNL Adobe Mix Modeler]. |
| [!DNL AI Assistant] | Configurare le autorizzazioni per [!DNL AI Assistant]. |
| [!DNL Alerts] | Configurare le autorizzazioni di gestione, risoluzione e visualizzazione per gli avvisi e la cronologia degli avvisi. |
| [!DNL B2B Account Lists] | Configurare le autorizzazioni di gestione, visualizzazione e pubblicazione per gli elenchi di account B2B, incluse le azioni di aggiunta, rimozione, importazione ed eliminazione di account dagli elenchi di account. |
| [!DNL B2B Admin Configurations] | Configura le autorizzazioni di gestione e visualizzazione per le configurazioni dell’amministratore B2B, tra cui connessioni per la gestione delle risorse digitali, archivi di risorse ed eventi. |
| [!DNL B2B Assets] | Configura le autorizzazioni di gestione e visualizzazione per le risorse B2B, tra cui e-mail, SMS, pagine di destinazione, frammenti, modelli e immagini. |
| [!DNL B2B Buying Groups] | Configura le autorizzazioni di gestione e visualizzazione per i gruppi di acquisto B2B, incluse funzioni quali interessi della soluzione, modelli di ruoli e stato del gruppo di acquisto. |
| [!DNL B2B Channel Configurations] | Configura le autorizzazioni di gestione e visualizzazione per le configurazioni del canale B2B, tra cui impostazioni quali limiti di comunicazione, credenziali API e impostazioni di sicurezza. |
| [!DNL B2B Dashboards] | Configurare le autorizzazioni di visualizzazione per le dashboard B2B, incluse funzionalità quali coinvolgimento dell’account, fasi di acquisto del gruppo, account in crescita e copertura dei contatti. |
| [!DNL B2B Journeys] | Configurare le autorizzazioni di gestione, visualizzazione e pubblicazione per i percorsi B2B, incluse funzioni quali azioni per account e persone, listener di eventi e percorsi suddivisi. |
| [!DNL Campaigns] | Configura le autorizzazioni di gestione, pubblicazione e visualizzazione per le campagne in Journey Optimizer. |
| [!DNL Channel Configurations] | Configura le funzioni di gestione, visualizzazione ed esportazione delle configurazioni dei canali, ad esempio sottodomini, pool IP, predefiniti per messaggi, record PTR, elenchi di soppressione, impostazioni della pagina di destinazione, impostazioni SMS e indirizzamento dei file. |
| [!DNL Collaborations] | Configura le autorizzazioni di gestione e visualizzazione per le funzioni di Real-Time Customer Data Profile Collaboration. |
| [!DNL Computed Attributes] | Configura le autorizzazioni di gestione e visualizzazione per gli attributi calcolati bozza o pubblicati. |
| [!DNL Customer Managed Keys] | Configura le autorizzazioni di gestione per le chiavi gestite dal cliente. |
| [!DNL Dashboards] | Configura le autorizzazioni di gestione e visualizzazione per dashboard standard, personalizzati e con licenza. |
| [!DNL Data Collection] | Configurare le autorizzazioni di gestione e visualizzazione per gli stream di dati. |
| [!DNL Data Governance] | Configura le autorizzazioni di gestione, applicazione e visualizzazione per le funzioni di governance dei dati come etichette, criteri e registri di attività. |
| [!DNL Data Ingestion] | Configura le autorizzazioni di gestione e visualizzazione per le funzioni di acquisizione dei dati, come origini e condivisione di pubblico. |
| [!DNL Data Lifecycle] | Configura le autorizzazioni di gestione e visualizzazione per le funzioni di igiene dei dati. |
| [!DNL Data Management] | Configura le autorizzazioni di gestione e visualizzazione per le funzioni di gestione dei dati, come i set di dati e i set di dati e i flussi di monitoraggio. |
| [!DNL Data Modeling] | Configura le autorizzazioni di gestione e visualizzazione per le funzionalità di modellazione dati come schemi, relazioni e metadati di identità. |
| [!DNL Data Science Workspace] | Configurare le autorizzazioni di gestione per [!DNL Data Science Workspace]. |
| [!DNL Decision Management] | Configura le autorizzazioni di gestione e visualizzazione per le funzioni di decisioni, offerte e strategie di classificazione nella gestione delle decisioni. |
| [!DNL Destinations] | Configura le autorizzazioni di gestione e visualizzazione per le destinazioni, incluse funzioni quali l’attivazione e l’authoring con Destinations SDK. |
| [!DNL Federated Data] | Configurare le autorizzazioni di gestione e visualizzazione per le funzionalità di dati federati. |
| [!DNL Identity Management] | Configura le autorizzazioni di gestione e visualizzazione per le funzioni di Identity Service, ad esempio gli spazi dei nomi delle identità e il grafo delle identità. |
| [!DNL Intelligent Service] | Configura le autorizzazioni di gestione e visualizzazione per IA per l’attribuzione e IA per l’analisi dei clienti in Intelligent Service. |
| [!DNL IP Warmup Configurations] | Configurare le autorizzazioni di gestione e visualizzazione per i piani di riscaldamento IP e visualizzare le autorizzazioni per visualizzare i rapporti di riscaldamento IP. |
| [!DNL Journey Optimizer Library] | Configura le autorizzazioni di gestione per gli elementi della libreria in Adobe Journey Optimizer. |
| [!DNL Journey Optimizer Rules] | Configura le autorizzazioni di gestione e visualizzazione per le regole di frequenza in Adobe Journey Optimizer. |
| [!DNL Journeys] | Configura le autorizzazioni di gestione, pubblicazione e visualizzazione per i percorsi, incluse funzioni quali report sui percorsi, eventi, origini dati e azioni. |
| [!DNL Messages] | Configura le autorizzazioni di gestione, pubblicazione e visualizzazione per i messaggi, incluse funzionalità quali anteprima e test dei messaggi. |
| [!DNL Privacy Service] | Configura le autorizzazioni di gestione e visualizzazione per le funzioni di Privacy Service. |
| [!DNL Profile Management] | Configura le autorizzazioni di gestione, visualizzazione, esportazione e valutazione per le funzioni dei servizi di profilo, quali tipi di pubblico, profili e criteri di unione. |
| [!DNL Prospects] | Configura le autorizzazioni di gestione e visualizzazione per schemi, profili e tipi di pubblico di potenziali clienti, incluse funzionalità quali la visualizzazione del pannello a soffietto del prospect. |
| [!DNL Query Service] | Configurare le autorizzazioni di gestione per le funzionalità del servizio di query, ad esempio credenziali senza scadenza e query SQL strutturate. |
| [!DNL Reports] | Configurare le autorizzazioni di visualizzazione per canalizzare i rapporti. |
| [!DNL Run and Operate] | Configurare le autorizzazioni di visualizzazione per le funzionalità di esecuzione e funzionamento, ad esempio i controlli di integrità e le pianificazioni dei job. |
| [!DNL Sandbox Administration] | Configura le autorizzazioni di gestione, visualizzazione e ripristino per l’amministrazione delle sandbox. |
| [!DNL Traits Configuration] | Configura la gestione e la visualizzazione delle caratteristiche tramite l’interfaccia utente degli attributi calcolati. |
| [!DNL Translation Services] | Configura le autorizzazioni di gestione e visualizzazione per i servizi di traduzione per progetti, attività, revisioni, interni, impostazioni e provider. |

La tabella seguente illustra le autorizzazioni disponibili per Experience Platform nel ruolo, con la descrizione delle funzionalità Experience Platform specifiche a cui concedono l’accesso. Per i passaggi dettagliati su come aggiungere le autorizzazioni a un ruolo, consulta la [guida dei ruoli di controllo dell&#39;accesso basati sull&#39;attributo](./abac/ui/roles.md).

| Categoria | Autorizzazione | Descrizione |
| --- | --- | --- |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Manage Adobe Mix Modeler Harmonized Data] | La possibilità di visualizzare e modificare dati armonizzati. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL View Adobe Mix Modeler Harmonized Data] | Accesso in sola lettura a dati armonizzati. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Manage Adobe Mix Modeler Models Configurations] | Possibilità di visualizzare e modificare le configurazioni dei modelli. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL View Adobe Mix Modeler Models Configurations] | Accesso in sola lettura alle configurazioni dei modelli. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Manage Adobe Mix Modeler Models Plans Configurations] | Possibilità di visualizzare e modificare le configurazioni dei piani. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL View Adobe Mix Modeler Models Plans Configurations] | Accesso in sola lettura alle configurazioni dei piani. |
| [!DNL AI Assistant] | [!UICONTROL Enable AI Assistant] | Possibilità di porre le domande [!DNL [AI assistant]](../ai-assistant/access.md). |
| [!DNL AI Assistant] | [!UICONTROL View Operational Insights] | Accesso per ottenere risposte alle [query Operational Insights](../ai-assistant/home.md##operational-insights). |
| [!DNL AI Assistant] | [!UICONTROL Generate Content] | Consente agli utenti di generare contenuto utilizzando [!DNL AI Assistant]. |
| [!DNL AI Assistant] | [!UICONTROL Manage Brand Kit] | Consente agli utenti di creare le linee guida per il marchio utilizzando [!DNL AI Assistant]. |
| [!DNL Alerts] | [!UICONTROL View Alerts History] | Accesso in sola lettura per la cronologia degli avvisi. |
| [!DNL Alerts] | [!UICONTROL Resolve Alerts] | Accesso per leggere, modificare ed eliminare gli avvisi. |
| [!DNL Alerts] | [!UICONTROL View Alerts] | Accesso in sola lettura per gli avvisi. |
| [!DNL Alerts] | [!UICONTROL Manage Alerts] | Accesso per leggere, creare, modificare ed eliminare gli avvisi. |
| [!DNL B2B Account Lists] | [!UICONTROL Manage B2B Account Lists] | Possibilità di visualizzare e accedere a **[!UICONTROL Account Lists]** nel menu di navigazione a sinistra. Gli utenti con accesso a **[!UICONTROL Account Lists]** devono avere accesso a tutte le funzioni CRUD degli elenchi account: `/accounts-list`. |
| [!DNL B2B Admin Configurations] | [!UICONTROL Manage B2B Admin Configurations] | Possibilità di visualizzare e accedere a **[!UICONTROL B2B Admin Configurations]** nel menu di navigazione a sinistra. Gli utenti con accesso a **[!UICONTROL B2B Admin Configurations]** devono avere accesso a tutte le funzioni CRUD delle credenziali API SMS: `/admin-configs`. |
| [!DNL B2B Assets] | [!UICONTROL Manage B2B Assets] | Possibilità di visualizzare e accedere a **[!UICONTROL Assets]** nel menu di navigazione a sinistra. Gli utenti con accesso a **[!UICONTROL Assets]** devono avere accesso a tutte le funzioni CRUD di Assets: `/assets-listing`. |
| [!DNL B2B Assets] | [!UICONTROL Manage B2B Templates] | Possibilità di visualizzare e accedere a **[!UICONTROL Templates]** nel menu di navigazione a sinistra. Gli utenti con accesso a **[!UICONTROL Templates]** devono avere accesso a tutte le funzioni CRUD dei modelli: `/b2b-content-templates`. |
| [!DNL B2B Assets] | [!UICONTROL Manage B2B Fragments] | Possibilità di visualizzare e accedere a **[!UICONTROL Fragments]** nel menu di navigazione a sinistra. Gli utenti con accesso a **[!UICONTROL Fragments]** devono avere accesso a tutte le funzioni CRUD dei frammenti: `/fragments`. |
| [!DNL B2B Buying Groups] | [!UICONTROL Manage B2B Buying Groups] | Possibilità di visualizzare e accedere a **[!UICONTROL Buying Groups]** nel menu di navigazione a sinistra. Gli utenti con accesso a **[!UICONTROL Buying Groups]** devono avere accesso a tutte le funzioni CRUD dei gruppi di acquisto: `/buying-groups`. |
| [!DNL B2B Dashboards] | [!UICONTROL Manage B2B Engagement Dashboards] | Possibilità di visualizzare e accedere a **[!UICONTROL Dashboard]** nel menu di navigazione a sinistra. Gli utenti con accesso a **[!UICONTROL Dashboards]** devono avere accesso a tutte le funzioni CRUD delle dashboard: `/insights-dashboard`. |
| [!DNL B2B Channel Configurations] | [!UICONTROL Manage B2B Channels Configurations] | Possibilità di visualizzare e accedere a **[!UICONTROL Channels]** nel menu di navigazione a sinistra. Gli utenti con accesso a **[!UICONTROL Channels]** devono avere accesso a tutte le funzioni CRUD dei canali: `/channels-config`. |
| [!DNL B2B Journeys] | [!UICONTROL Manage B2B Account Journeys] | Possibilità di visualizzare e accedere a **[!UICONTROL Account Journeys]** nel menu di navigazione a sinistra. Gli utenti con accesso a **[!UICONTROL Account Journeys]** devono avere accesso a tutte le funzioni CRUD dei Percorsi di account: `/account-journeys`. |
| [!DNL Campaigns] | [!UICONTROL Manage Campaigns] | Accesso a campagne di lettura, creazione, modifica ed eliminazione. |
| [!DNL Campaigns] | [!UICONTROL Approve and Publish Campaigns] | Possibilità di approvare e pubblicare campagne. |
| [!DNL Campaigns] | [!UICONTROL Publish Campaigns] | Possibilità di pubblicare campagne. |
| [!DNL Campaigns] | [!UICONTROL View Campaigns] | Accesso in sola lettura alle campagne. |
| [!DNL Campaigns] | [!UICONTROL View Campaigns Report] | Accesso in sola lettura ai rapporti delle campagne. |
| [!DNL Channel Configurations] | [!UICONTROL View Messages General Settings] | Accesso in sola lettura alle impostazioni generali dei messaggi. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Subdomains Delegations] | Accesso per leggere, creare, modificare ed eliminare le deleghe dei sottodomini. |
| [!DNL Channel Configurations] | [!UICONTROL Manage IP Pools] | Accesso per leggere, creare e modificare i pool IP. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Messages General Settings] | Accesso per leggere, creare, modificare ed eliminare le impostazioni generali dei messaggi. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Messages Presets] | Accesso per leggere, creare, modificare ed eliminare i predefiniti per i messaggi. |
| [!DNL Channel Configurations] | [!UICONTROL View Messages Presets] | Accesso in sola lettura ai predefiniti per messaggi. |
| [!DNL Channel Configurations] | [!UICONTROL Manage PTR Records] | Accesso per la lettura e la modifica dei record PTR. |
| [!DNL Channel Configurations] | [!UICONTROL View PTR Records] | Accesso in sola lettura ai record PTR. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Suppression] | Accesso per leggere, creare, modificare ed eliminare le regole di soppressione. |
| [!DNL Channel Configurations] | [!UICONTROL View Suppression List] | Accesso in sola lettura all’elenco di soppressione. |
| [!DNL Channel Configurations] | [!UICONTROL Export Suppression List] | Accesso per esportare l’elenco di soppressione come file CSV. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Landing Page Settings] | Accesso per leggere, creare, modificare ed eliminare le impostazioni della pagina di destinazione. |
| [!DNL Channel Configurations] | [!UICONTROL Manage SMS Settings] | Accesso per leggere, creare, modificare ed eliminare le impostazioni SMS. |
| [!DNL Channel Configurations] | [!UICONTROL Manage SMS Subdomains] | Accesso per leggere, creare, modificare ed eliminare i sottodomini SMS. |
| [!DNL Channel Configurations] | [!UICONTROL Manage File Routing] | Accesso per la lettura, la creazione, la modifica e l&#39;eliminazione dei cicli di file. |
| [!DNL Channel Configurations] | [!UICONTROL View File Routing] | Accesso in sola lettura ai cicli dei file. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Seedlist] | Possibilità di creare e modificare l’elenco di seed. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Language Settings] | Possibilità di creare e modificare le impostazioni della lingua. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Web Subdomains] | Possibilità di creare e modificare i sottodomini web CJM. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Push Credentials] | Possibilità di creare, modificare ed eliminare le credenziali push. |
| [!DNL Collaborations] | [!UICONTROL Manage Collaboration Instances] | Visualizzare, creare, aggiornare ed eliminare le istanze di collaborazione di un&#39;organizzazione. Scopri le istanze di collaborazione di altre organizzazioni. |
| [!DNL Collaborations] | [!UICONTROL Read Collaboration Instances] | Leggi le istanze di collaborazione di un’organizzazione e scopri le istanze di collaborazione di altre organizzazioni. |
| [!DNL Collaborations] | [!UICONTROL Manage Connection Invites] | Visualizzare, creare ed eliminare gli inviti di connessione avviati dall&#39;organizzazione. Accetta e rifiuta l’invito alla connessione avviato da altre organizzazioni. |
| [!DNL Collaborations] | [!UICONTROL Read Connection Invites] | Accesso in sola lettura agli inviti di connessione. |
| [!DNL Collaborations] | [!UICONTROL Manage Collaboration Connections] | Un inserzionista può visualizzare, creare e aggiornare le impostazioni, nonché inviare ed eliminare connessioni. Un editore può visualizzare, accettare o rifiutare le connessioni. |
| [!DNL Collaborations] | [!UICONTROL Read Collaboration Connections] | Accesso in sola lettura alle connessioni. |
| [!DNL Collaborations] | [!UICONTROL Manage Audience Data] | Eseguire l’onboarding e individuare i tipi di pubblico. Aggiorna i tipi di pubblico pubblici, privati e personalizzati e gestisci le impostazioni dei metadati di Inventario pubblico. |
| [!DNL Collaborations] | [!UICONTROL Read Audience Data] | Leggi e individua i tipi di pubblico. |
| [!DNL Collaborations] | [!UICONTROL Manage Measurement Data] | Integrare, aggiornare ed eliminare i dati di misurazione. |
| [!DNL Collaborations] | [!UICONTROL Read Measurement Data] | Accesso in sola lettura ai dati di misurazione. |
| [!DNL Collaborations] | [!UICONTROL Manage Projects] | Visualizza, crea, aggiorna ed elimina progetti per qualsiasi attività di individuazione, condivisione, attivazione e misurazione. |
| [!DNL Collaborations] | [!UICONTROL Read Projects] | Visualizza i progetti per qualsiasi attività di individuazione, condivisione, attivazione e misurazione. |
| [!DNL Collaborations] | [!UICONTROL Read User Activities] | Accesso in sola lettura alle attività degli utenti. |
| [!DNL Collaborations] | [!UICONTROL Export User Activities] | Esporta attività utente. |
| [!DNL Collaborations] | [!UICONTROL Read Collaboration Credit Monitoring] | Monitoraggio del credito a livello di organizzazione e istanza. |
| [!DNL Computed Attributes] | [!UICONTROL View Computed attributes] | Accesso in sola lettura per la scheda degli attributi calcolati, l’inventario e i dettagli. |
| [!DNL Computed Attributes] | [!UICONTROL Manage Computed attributes] | Accesso per leggere, creare, eliminare bozze e disattivare attributi calcolati. |
| [!DNL Customer Managed Keys] | [!UICONTROL Manage Customer Managed Keys] | Accesso per visualizzare e configurare le chiavi gestite dal cliente. |
| [!DNL Dashboards] | [!UICONTROL View License Usage Dashboard] | Accesso in sola lettura per visualizzare il dashboard utilizzo licenze. |
| [!DNL Dashboards] | [!UICONTROL Manage Standard Dashboards] | Aggiungi attributi personalizzati non ancora presenti nel data warehouse. |
| [!DNL Dashboards] | [!UICONTROL View Standard Dashboards] | Accesso in sola lettura ai dashboard Profili, Destinazioni e Segmenti. Consente inoltre di accedere alle dashboard nella barra di navigazione a sinistra e nella scheda Inventario dashboard e integrazioni. |
| [!DNL Dashboards] | [!UICONTROL Manage Custom Dashboards] | Accesso per creare o modificare un dashboard. |
| [!DNL Dashboards] | [!UICONTROL View Custom Dashboards] | Accesso in sola lettura alle dashboard definite dall&#39;utente. |
| [!DNL Dashboards] | [!UICONTROL Manage Report Schedules] | Possibilità di creare pianificazioni. |
| [!DNL Dashboards] | [!UICONTROL Export Dashboard Data] | Controlla la capacità di un utente di esportare dati tabulari dai dashboard in modalità query pro. |
| [!DNL Data Collection] | [!UICONTROL Manage Datastreams] | Accesso per leggere, creare e modificare gli stream di dati. |
| [!DNL Data Collection] | [!UICONTROL View Datastreams] | Accesso in sola lettura agli stream di dati. |
| [!DNL Data Governance] | [!UICONTROL Manage Usage Labels] | Accesso per leggere, creare ed eliminare le etichette di utilizzo. |
| [!DNL Data Governance] | [!UICONTROL Manage Data Usage Policies] | Accesso per leggere, creare, modificare ed eliminare i criteri di utilizzo dei dati. |
| [!DNL Data Governance] | [!UICONTROL View Data Usage Policies] | Accesso in sola lettura per i criteri di utilizzo dei dati appartenenti alla tua organizzazione. |
| [!DNL Data Governance] | [!UICONTROL View User Activity Log] | Accesso in sola lettura per visualizzare i [registri di controllo](../landing/governance-privacy-security/audit-logs/overview.md) registrati delle attività di Experience Platform. |
| [!DNL Data Governance] | [!UICONTROL View Privacy Console] | Accesso in sola lettura alle console per la privacy. |
| [!DNL Data Ingestion] | [!UICONTROL Manage Sources] | Accesso per leggere, creare, modificare e disabilitare le origini. |
| [!DNL Data Ingestion] | [!UICONTROL View Sources] | Accesso in sola lettura alle origini disponibili nella scheda **[!UICONTROL Catalog]** e alle origini autenticate nella scheda **[!UICONTROL Browse]**. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | Accesso per creare, accettare e rifiutare la condivisione partner per connettere due organizzazioni e abilitare [!DNL Segment Match] flussi. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share] | Accesso a lettura, creazione, modifica e pubblicazione di [!DNL Segment Match] feed con partner attivi. |
| [!DNL Data Lifecycle] | [!UICONTROL View Data Lifecycle] | Accesso in sola lettura per il ciclo di vita dei dati. |
| [!DNL Data Lifecycle] | [!UICONTROL Manage Data Lifecycle] | Accesso per leggere, creare, modificare ed eliminare il ciclo di vita dei dati. |
| [!DNL Data Modeling] | [!UICONTROL Manage Schemas] | Accesso per leggere, creare, modificare ed eliminare schemi e risorse correlate. |
| [!DNL Data Modeling] | [!UICONTROL View Schemas] | Accesso in sola lettura agli schemi e alle risorse correlate. |
| [!DNL Data Modeling] | [!UICONTROL Manage Relationships] | Accesso per leggere, creare, modificare ed eliminare le relazioni tra schemi. |
| [!DNL Data Modeling] | [!UICONTROL Manage Identity Metadata] | Accesso per leggere, creare, modificare ed eliminare i metadati di identità per gli schemi. |
| [!DNL Data Management] | [!UICONTROL Manage Datasets] | Accesso per leggere, creare, modificare ed eliminare i set di dati. Accesso in sola lettura per gli schemi. |
| [!DNL Data Management] | [!UICONTROL View Datasets] | Accesso in sola lettura per set di dati e schemi. |
| [!DNL Data Management] | [!UICONTROL Data Monitoring] | Accesso in sola lettura ai set di dati e ai flussi di monitoraggio. |
| [!DNL Data Science Workspace] | [!UICONTROL Manage Data Science Workspace] | Accesso a lettura, creazione, modifica ed eliminazione in [!DNL Data Science Workspace]. |
| [!DNL Decision Management] | [!UICONTROL Manage Experience Decisioning] | Possibilità di gestire le entità Experience Decisioning. |
| [!DNL Decision Management] | [!UICONTROL View Experience Decisioning] | Accesso in sola lettura alle entità Experience Decisioning. |
| [!DNL Decision Management] | [!UICONTROL Manage Decisions] | Accesso per leggere, creare, modificare ed eliminare entità decisionali. |
| [!DNL Decisions Management] | [!UICONTROL View Decisions] | Accesso in sola lettura alle entità decisionali. |
| [!DNL Decision Management] | [!UICONTROL Manage Offers] | Accesso per leggere, creare, modificare ed eliminare tutte le offerte e i componenti. Accesso in sola lettura a decisioni e raccolte. |
| [!DNL Decsion Management] | [!UICONTROL Manage Ranking Strategies] | Accesso per leggere, creare, modificare ed eliminare rapporti personalizzati e utilizzare le funzioni di azione. |
| [!DNL Destinations] | [!UICONTROL View Destinations] | Accesso in sola lettura per visualizzare le destinazioni disponibili nella scheda **[!UICONTROL Catalog]** e le destinazioni autenticate nella scheda **[!UICONTROL Browse]**. |
| [!DNL Destinations] | [!UICONTROL Manage Destinations] | Accesso per leggere, creare ed eliminare connessioni di destinazioni e account di destinazione. |
| [!DNL Destinations] | [!UICONTROL Activate Destinations] | Possibilità di attivare i dati per le destinazioni attive create. Questa autorizzazione richiede anche che [!UICONTROL View Destinations] o [!UICONTROL Manage Destinations] siano concessi all&#39;utente che attiverà le destinazioni. |
| [!DNL Destinations] | [!UICONTROL Activate Segment without Mapping] | Possibilità di attivare i tipi di pubblico nelle destinazioni esistenti, senza visualizzare il [passaggio di mappatura](../destinations/ui/activate-batch-profile-destinations.md#mapping). Gli utenti possono aggiungere e rimuovere tipi di pubblico nei flussi di lavoro di attivazione, ma non possono aggiungere o rimuovere attributi o identità mappati. Questa autorizzazione richiede anche l&#39;autorizzazione [!UICONTROL View Destinations] per essere concessa all&#39;utente che attiverà i dati nelle destinazioni. |
| [!DNL Destinations] | [!UICONTROL Manage and Activate Dataset Destinations] | Possibilità di leggere, creare, modificare e disabilitare i flussi di esportazione dei set di dati. Possibilità di attivare i dati anche per i set di dati attivi che sono stati creati. Questa autorizzazione richiede anche l&#39;autorizzazione [!UICONTROL View Destinations] per essere concessa all&#39;utente che attiverà i dati nelle destinazioni. |
| [!DNL Destinations] | [!UICONTROL Destination Authoring] | Possibilità di creare destinazioni utilizzando [Adobe Experience Platform Destination SDK](../destinations/destination-sdk/overview.md). |
| [!DNL Federated Data] | [!UICONTROL Manage Federated Data] | Possibilità di accedere a tutte le funzionalità di dati federati, ad esempio la creazione di schemi, modelli e composizioni. |
| [!DNL Identity Management] | [!UICONTROL Manage Identity Namespaces] | Accesso per leggere, creare, modificare ed eliminare spazi dei nomi di identità. |
| [!DNL Identity Management] | [!UICONTROL View Identity Namespaces] | Accesso in sola lettura per gli spazi dei nomi di identità. |
| [!DNL Identity Management] | [!UICONTROL View Identity Graph] | Accesso in sola lettura per i grafici di identità. |
| [!DNL Identity Management] | [!UICONTROL Manage Identity Settings] | Accesso per leggere, creare e modificare le impostazioni di identità. |
| [!DNL Identity Management] | [!UICONTROL View Identity Settings] | Accesso in sola lettura alle impostazioni di identità. |
| [!DNL Intelligent Services] | [!UICONTROL View Attribution AI] | Accesso in sola lettura per le impostazioni e le informazioni di Attribution AI. |
| [!DNL Intelligent Services] | [!UICONTROL Manage Attribution AI] | Accesso per leggere, creare, modificare ed eliminare modelli di IA per l’attribuzione. |
| [!DNL Intelligent Services] | [!UICONTROL View Customer AI] | Accesso per leggere o visualizzare i modelli di IA per l’analisi dei clienti. |
| [!DNL Intelligent Services] | [!UICONTROL Manage Customer AI] | Accesso per creare, aggiornare, eliminare, abilitare o disabilitare modelli di IA per l’analisi dei clienti. |
| [!DNL IP Warmup Configurations] | [!UICONTROL View IP Warmup Plans] | Accesso in sola lettura ai piani di riscaldamento IP. |
| [!DNL IP Warmup Configurations] | [!UICONTROL Manage IP Warmup Plans] | Possibilità di gestire i piani di riscaldamento IP. |
| [!DNL IP Warmup Configurations] | [!UICONTROL View IP Warmup Reports] | Accesso in sola lettura ai report di riscaldamento IP. |
| [!DNL Journeys] | [!UICONTROL Manage Journeys] | Accesso per leggere, creare, modificare ed eliminare percorsi. |
| [!DNL Journeys] | [!UICONTROL View Journeys] | Accesso in sola lettura ai percorsi. |
| [!DNL Journeys] | [!UICONTROL View Journeys Report] | Rapporto Accesso in sola lettura ai percorsi. |
| [!DNL Journeys] | [!UICONTROL Manage Journeys Events, Data Sources and Actions] | Accesso per leggere, creare, modificare ed eliminare eventi, origini dati o azioni. |
| [!DNL Journeys] | [!UICONTROL View Journeys Events, Data Sources and Actions] | Accesso in sola lettura a eventi, origini dati o azioni. |
| [!DNL Journeys] | [!UICONTROL Approve and Publish Journeys] | Possibilità di approvare e pubblicare percorsi quando viene applicato un criterio. |
| [!DNL Journeys] | [!UICONTROL Publish Journeys] | Possibilità di pubblicare percorsi. |
| [!DNL Journey Optimizer Library] | [!UICONTROL Manage Library Items] | Possibilità di aggiungere ed eliminare espressioni salvate. |
| [!DNL Journey Optimizer Library] | [!UICONTROL Publish Fragments] | Possibilità di pubblicare frammenti di contenuto. |
| [!DNL Journey Optimizer Library] | [!UICONTROL Simulate Content] | Accesso all’opzione Simula contenuto per l’anteprima e la verifica. |
| [!DNL Journey Optimizer Rules] | [!UICONTROL View Frequency Rules] | Accesso in sola lettura alle regole di frequenza. |
| [!DNL Journey Optimizer Rules] | [!UICONTROL Manage Frequency Rules] | Accesso per leggere, creare, modificare o eliminare regole di frequenza. |
| [!DNL Messages] | [!UICONTROL Manage Messages] | Accesso per leggere, creare, modificare ed eliminare i messaggi. |
| [!DNL Messages] | [!UICONTROL View Messages] | Accesso in sola lettura ai messaggi. |
| [!DNL Messages] | [!UICONTROL View Messages Report] | Accesso per leggere e modificare i rapporti sui messaggi. |
| [!DNL Messages] | [!UICONTROL Publish Messages] | Possibilità di pubblicare messaggi. |
| [!DNL Messages] | [!UICONTROL Manage Messages Preview and Test] | Possibilità di approvare e pubblicare messaggi quando viene applicato un criterio. |
| [!DNL Privacy Service] | [!UICONTROL Manage Privacy Service] | Accesso ai flussi di lavoro di privacy in lettura e scrittura. |
| [!DNL Privacy Service] | [!UICONTROL View Privacy Service] | Accesso in sola lettura ai flussi di lavoro sulla privacy. |
| [!DNL Profile Management] | [!UICONTROL Manage Profiles] | Accesso per leggere, creare, modificare ed eliminare i set di dati utilizzati per i profili dei clienti. Accesso in sola lettura ai profili disponibili. |
| [!DNL Profile Management] | [!UICONTROL View Profiles] | Accesso in sola lettura ai profili disponibili. |
| [!DNL Profile Management] | [!UICONTROL Manage Segments] | Accesso per leggere, creare, modificare ed eliminare tipi di pubblico. |
| [!DNL Profile Management] | [!UICONTROL View Segments] | Accesso in sola lettura al pubblico disponibile. |
| [!DNL Profile Management] | [!UICONTROL Manage Merge Policies] | Accesso per leggere, creare, modificare ed eliminare i criteri di unione. |
| [!DNL Profile Management] | [!UICONTROL View Merge Policies] | Accesso in sola lettura ai criteri di unione disponibili. |
| [!DNL Profile Management] | [!UICONTROL Import Audiences] | Possibilità di utilizzare il flusso di lavoro di caricamento CSV per importare nuovi tipi di pubblico. |
| [!DNL Profile Management] | [!UICONTROL Export Audience Segment] | Possibilità di esportare un pubblico valutato in un set di dati. |
| [!DNL Profile Management] | [!UICONTROL Evaluate a Segment to an Audience] | Possibilità di generare profili per un pubblico valutando una definizione di segmento. |
| [!DNL Profile Management] | [!UICONTROL View B2B AI] | Accesso in sola lettura alle impostazioni e alle configurazioni per tutti i servizi di IA/ML B2B. |
| [!DNL Profile Management] | [!UICONTROL Manage B2B AI] | Accesso per leggere, creare, modificare ed eliminare impostazioni e configurazioni per tutti i servizi di IA/ML B2B. |
| [!DNL Profile Management] | [!UICONTROL View B2B Profile] | Accesso in sola lettura a profili di entità B2B (come Account, Opportunità e così via), impostazioni e configurazioni per tutti i servizi AI/ML B2B e i widget del dashboard B2B. |
| [!DNL Profile Management] | [!UICONTROL Manage B2B Profile] | Accesso per leggere, creare, modificare ed eliminare profili di entità B2B (come Account, Opportunità e così via). Accesso in sola lettura per impostazioni e configurazioni per tutti i servizi AI/ML B2B e i widget del dashboard B2B. |
| [!DNL Profile Management] | [!UICONTROL Manage Lookalikes] | Possibilità di creare o eliminare tipi di pubblico simili. |
| [!DNL Profile Management] | [!UICONTROL View B2B Experience] | Possibilità di visualizzare profili e attributi B2B. |
| [!DNL Profile Management] | [!UICONTROL View Profile Settings] | Accesso in sola lettura a tutte le impostazioni del profilo. |
| [!DNL Profile Management] | [!UICONTROL Manage Profile Settings] | Accesso per leggere e modificare tutte le impostazioni di profilo. |
| [!DNL Prospects] | [!UICONTROL View Prospects] | Accesso in sola lettura a schemi, profili, tipi di pubblico e pannello a soffietto del potenziale cliente. |
| [!DNL Prospects] | [!UICONTROL Manage Prospects] | Possibilità di creare e gestire schemi, profili e tipi di pubblico potenziali. Accesso in sola lettura al pannello a soffietto del prospect. |
| [!DNL Query Service] | [!UICONTROL Manage Queries] | Accesso per leggere, creare, modificare ed eliminare query SQL strutturate per i dati di Experience Platform. |
| [!DNL Query Service] | [!UICONTROL Manage Query Service Integration] | Accesso per creare, aggiornare ed eliminare credenziali senza scadenza per l’accesso a Query Service. |
| [!DNL Query Service] | [!UICONTROL Manage Query Sessions] | Possibilità di eliminare le sessioni esistenti. |
| [!DNL Query Service] | [!UICONTROL Manage Allow List] | Possibilità di gestire le restrizioni IP per la tua organizzazione. |
| [!DNL Reports] | [!UICONTROL View Channel Reports] | Possibilità di visualizzare e modificare i rapporti sui canali. |
| [!DNL Run and Operate] | [!UICONTROL View Health Checks] | Accesso in sola lettura ai controlli di integrità. |
| [!DNL Run and Operate] | [!UICONTROL View Job Schedules] | Accesso in sola lettura alle pianificazioni dei processi. |
| [!DNL Sandbox Administration] | [!UICONTROL Manage Sandboxes] | Accesso alle sandbox di lettura, creazione, modifica ed eliminazione. |
| [!DNL Sandbox Administration] | [!UICONTROL View Sandboxes] | Accesso in sola lettura per le sandbox appartenenti alla tua organizzazione. |
| [!DNL Sandbox Administration] | [!UICONTROL Reset a Sandbox] | Possibilità di ripristinare una sandbox. |
| [!DNL Sandbox Administration] | [!UICONTROL Manage Packages] | Accesso per creare, importare o esportare pacchetti. |
| [!DNL Sandbox Administration] | [!UICONTROL Share Packages] | Accesso per la condivisione di pacchetti tra organizzazioni diverse. |
| [!DNL Traits Configurations] | [!UICONTROL View Traits] | Accesso in sola lettura per le caratteristiche. |
| [!DNL Traits Configurations] | [!UICONTROL Manage Traits] | Accesso per gestire le caratteristiche. |
| [!DNL Translation Service] | [!UICONTROL Manage Translation Projects] | La capacità di gestire i progetti di traduzione. |
| [!DNL Translation Service] | [!UICONTROL View Translation Projects] | Accesso in sola lettura ai progetti di traduzione. |
| [!DNL Translation Service] | [!UICONTROL Manage Translation Tasks] | La possibilità di gestire le attività di traduzione. |
| [!DNL Translation Service] | [!UICONTROL View Translation Tasks] | Accesso in sola lettura alle attività di traduzione. |
| [!DNL Translation Service] | [!UICONTROL Manage Translation Reviews] | La possibilità di gestire le revisioni di traduzione. |
| [!DNL Translation Service] | [!UICONTROL View Translation Reviews] | Accesso in sola lettura alle recensioni di traduzione. |
| [!DNL Translation Service] | [!UICONTROL Manage Translation In-house] | La capacità di gestire la traduzione internamente. |
| [!DNL Translation Service] | [!UICONTROL View Translation In-house] | Accesso in sola lettura alla traduzione interna. |
| [!DNL Translation Service] | [!UICONTROL Manage Translation Settings] | Possibilità per gli amministratori di gestire le impostazioni di traduzione. |
| [!DNL Translation Service] | [!UICONTROL Manage Translation Providers] | La capacità di gestire i fornitori di traduzione. |

## Passaggi successivi

Una volta letta questa guida, potrai scoprire i principi fondamentali del controllo degli accessi in Experience Platform. Ora puoi passare alla [guida utente per il controllo degli accessi basato su attributi](./abac/overview.md) per i passaggi dettagliati su come utilizzare Experience Cloud per creare ruoli e assegnare autorizzazioni per Experience Platform.
