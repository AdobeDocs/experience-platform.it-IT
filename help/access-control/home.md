---
keywords: Experience Platform;home;argomenti popolari;controllo degli accessi;adobe admin console
solution: Experience Platform
title: Panoramica sul controllo degli accessi
description: Il controllo degli accessi per Adobe Experience Platform viene fornito tramite Adobe Admin Console. Questa funzionalità sfrutta i profili di prodotto in Admin Console, che collegano gli utenti con autorizzazioni e sandbox.
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: 6a466770495b226f890ab67b21c5cb027fd46e02
workflow-type: tm+mt
source-wordcount: '3851'
ht-degree: 0%

---

# Panoramica sul controllo degli accessi

Il controllo degli accessi per Adobe Experience Platform viene fornito tramite **[!UICONTROL Autorizzazioni]** in [Adobe Experience Cloud](https://experience.adobe.com/). Questa funzionalità sfrutta ruoli e criteri, che collegano gli utenti con autorizzazioni e sandbox.

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
- Durante la creazione o la modifica di un ruolo, l&#39;amministratore aggiunge gli utenti al ruolo utilizzando la scheda **[!UICONTROL utenti]** e concede le autorizzazioni a tali utenti (ad esempio &quot;[!UICONTROL Leggi set di dati]&quot; o &quot;[!UICONTROL Gestisci schemi]&quot;) modificando le autorizzazioni del ruolo. Analogamente, l’amministratore può assegnare l’accesso alle sandbox utilizzando la stessa opzione di modifica.
- Quando gli utenti accedono all’interfaccia utente di Experience Platform, il loro accesso alle funzionalità di Experience Platform è guidato dalle autorizzazioni concesse loro dal passaggio precedente. Ad esempio, se un utente non dispone dell&#39;autorizzazione [!UICONTROL Visualizza set di dati], la scheda **[!UICONTROL Set di dati]** nel menu laterale non sarà visibile all&#39;utente.

Per i passaggi più dettagliati su come gestire il controllo degli accessi in Experience Platform, consulta la [guida utente per il controllo degli accessi](./ui/overview.md).

Tutte le chiamate alle API di Experience Platform vengono convalidate per le autorizzazioni e restituiranno errori se le autorizzazioni appropriate non vengono trovate nel contesto utente corrente. Nell’interfaccia utente, gli elementi verranno nascosti o modificati a seconda delle autorizzazioni concesse all’utente corrente.

## Autorizzazioni {#platform-permissions}

[!UICONTROL Autorizzazioni] fornisce una posizione centrale per la gestione dell&#39;accesso ad Experience Platform per la tua organizzazione. Tramite [!UICONTROL Autorizzazioni], puoi concedere a gruppi di utenti le autorizzazioni di accesso per varie funzionalità di Experience Platform, ad esempio [!UICONTROL Gestisci set di dati], [!UICONTROL Visualizza set di dati] o [!UICONTROL Gestisci profili].

### Ruoli

Nella sezione [!UICONTROL Ruoli], le autorizzazioni vengono assegnate agli utenti tramite l&#39;utilizzo di ruoli. I ruoli consentono di concedere autorizzazioni a uno o più utenti e contengono anche il loro accesso all’ambito delle sandbox assegnate loro tramite i ruoli. Gli utenti possono essere assegnati a uno o più ruoli appartenenti alla tua organizzazione.

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

In [!UICONTROL Autorizzazioni], l&#39;area di lavoro risorse di un ruolo visualizza le sandbox e le autorizzazioni attive per tale ruolo:

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
| [!DNL Sandbox Administration] | Configura le autorizzazioni di gestione, visualizzazione e ripristino per l’amministrazione delle sandbox. |
| [!DNL Traits Configuration] | Configura la gestione e la visualizzazione delle caratteristiche tramite l’interfaccia utente degli attributi calcolati. |
| [!DNL Translation Services] | Configura le autorizzazioni di gestione e visualizzazione per i servizi di traduzione per progetti, attività, revisioni, interni, impostazioni e provider. |

La tabella seguente illustra le autorizzazioni disponibili per Experience Platform nel ruolo, con la descrizione delle funzionalità Experience Platform specifiche a cui concedono l’accesso. Per i passaggi dettagliati su come aggiungere le autorizzazioni a un ruolo, consulta la [guida dei ruoli di controllo dell&#39;accesso basati sull&#39;attributo](./abac/ui/roles.md).

| Categoria | Autorizzazione | Descrizione |
| --- | --- | --- |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Gestisci dati armonizzati di Adobe Mix Modeler] | La possibilità di visualizzare e modificare dati armonizzati. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Visualizza dati armonizzati di Adobe Mix Modeler] | Accesso in sola lettura a dati armonizzati. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Gestione configurazioni modelli Adobe Mix Modeler] | Possibilità di visualizzare e modificare le configurazioni dei modelli. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Visualizza configurazioni modelli Adobe Mix Modeler] | Accesso in sola lettura alle configurazioni dei modelli. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Gestione configurazioni piani modelli Adobe Mix Modeler] | Possibilità di visualizzare e modificare le configurazioni dei piani. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Visualizza configurazioni piani modelli Adobe Mix Modeler] | Accesso in sola lettura alle configurazioni dei piani. |
| [!DNL AI Assistant] | [!UICONTROL Abilita Assistente IA] | Possibilità di porre le domande [[!DNL [AI assistant]]](../ai-assistant/access.md). |
| [!DNL AI Assistant] | [!UICONTROL Visualizza informazioni operative] | Accesso per ottenere risposte alle [query Operational Insights](../ai-assistant/home.md##operational-insights). |
| [!DNL AI Assistant] | [!UICONTROL Genera contenuto] | Consente agli utenti di generare contenuto utilizzando [!DNL AI Assistant]. |
| [!DNL AI Assistant] | [!UICONTROL Gestire il Brand Kit] | Consente agli utenti di creare le linee guida per il marchio utilizzando [!DNL AI Assistant]. |
| [!DNL Alerts] | [!UICONTROL Visualizza cronologia avvisi] | Accesso in sola lettura per la cronologia degli avvisi. |
| [!DNL Alerts] | [!UICONTROL Risolvi avvisi] | Accesso per leggere, modificare ed eliminare gli avvisi. |
| [!DNL Alerts] | [!UICONTROL Visualizza avvisi] | Accesso in sola lettura per gli avvisi. |
| [!DNL Alerts] | [!UICONTROL Gestisci avvisi] | Accesso per leggere, creare, modificare ed eliminare gli avvisi. |
| [!DNL B2B Account Lists] | [!UICONTROL Gestione elenchi account B2B] | Possibilità di visualizzare e accedere a **[!UICONTROL Elenchi account]** nel menu di navigazione a sinistra. Gli utenti con accesso agli **[!UICONTROL elenchi account]** devono avere accesso a tutte le funzioni CRUD degli elenchi account: `/accounts-list`. |
| [!DNL B2B Admin Configurations] | [!UICONTROL Gestione configurazioni amministratore B2B] | Possibilità di visualizzare e accedere a **[!UICONTROL Configurazioni amministratore B2B]** nella barra di navigazione a sinistra. Gli utenti con accesso a **[!UICONTROL Configurazioni amministratore B2B]** devono avere accesso a tutte le funzioni CRUD delle credenziali API SMS: `/admin-configs`. |
| [!DNL B2B Assets] | [!UICONTROL Gestisci Assets B2B] | Possibilità di visualizzare e accedere a **[!UICONTROL Assets]** nella barra di navigazione a sinistra. Gli utenti con accesso a **[!UICONTROL Assets]** devono avere accesso a tutte le funzioni CRUD di Assets: `/assets-listing`. |
| [!DNL B2B Assets] | [!UICONTROL Gestisci modelli B2B] | Possibilità di visualizzare e accedere a **[!UICONTROL Modelli]** nella barra di navigazione a sinistra. Gli utenti con accesso a **[!UICONTROL Modelli]** devono avere accesso a tutte le funzioni CRUD dei modelli: `/b2b-content-templates`. |
| [!DNL B2B Assets] | [!UICONTROL Gestione frammenti B2B] | Possibilità di visualizzare e accedere a **[!UICONTROL Frammenti]** nella barra di navigazione a sinistra. Gli utenti con accesso a **[!UICONTROL Frammenti]** devono avere accesso a tutte le funzioni CRUD di Frammenti: `/fragments`. |
| [!DNL B2B Buying Groups] | [!UICONTROL Gestione gruppi di acquisto B2B] | Possibilità di visualizzare e accedere a **[!UICONTROL Gruppi di acquisto]** nel menu di navigazione a sinistra. Gli utenti con accesso a **[!UICONTROL Gruppi di acquisto]** devono avere accesso a tutte le funzioni CRUD di Gruppi di acquisto: `/buying-groups`. |
| [!DNL B2B Dashboards] | [!UICONTROL Gestione dashboard di coinvolgimento B2B] | Possibilità di visualizzare e accedere a **[!UICONTROL Dashboard]** nella barra di navigazione a sinistra. Gli utenti con accesso a **[!UICONTROL Dashboards]** devono avere accesso a tutte le funzioni CRUD delle dashboard: `/insights-dashboard`. |
| [!DNL B2B Channel Configurations] | [!UICONTROL Gestione configurazioni canali B2B] | Possibilità di visualizzare e accedere a **[!UICONTROL Canali]** nella barra di navigazione a sinistra. Gli utenti con accesso a **[!UICONTROL Canali]** devono avere accesso a tutte le funzioni CRUD dei canali: `/channels-config`. |
| [!DNL B2B Journeys] | [!UICONTROL Gestione Percorsi di account B2B] | Possibilità di visualizzare e accedere a **[!UICONTROL Percorsi di account]** nel menu di navigazione a sinistra. Gli utenti con accesso a **[!UICONTROL Percorsi di account]** devono avere accesso a tutte le funzioni CRUD dei Percorsi di account: `/account-journeys`. |
| [!DNL Campaigns] | [!UICONTROL Gestisci campagne] | Accesso a campagne di lettura, creazione, modifica ed eliminazione. |
| [!DNL Campaigns] | [!UICONTROL Approva e pubblica campagne] | Possibilità di approvare e pubblicare campagne. |
| [!DNL Campaigns] | [!UICONTROL Pubblica campagne] | Possibilità di pubblicare campagne. |
| [!DNL Campaigns] | [!UICONTROL Visualizza campagne] | Accesso in sola lettura alle campagne. |
| [!DNL Campaigns] | [!UICONTROL Visualizza report campagne] | Accesso in sola lettura ai rapporti delle campagne. |
| [!DNL Channel Configurations] | [!UICONTROL Visualizza impostazioni generali messaggi] | Accesso in sola lettura alle impostazioni generali dei messaggi. |
| [!DNL Channel Configurations] | [!UICONTROL Gestione deleghe sottodomini] | Accesso per leggere, creare, modificare ed eliminare le deleghe dei sottodomini. |
| [!DNL Channel Configurations] | [!UICONTROL Gestione pool IP] | Accesso per leggere, creare e modificare i pool IP. |
| [!DNL Channel Configurations] | [!UICONTROL Gestione impostazioni generali messaggi] | Accesso per leggere, creare, modificare ed eliminare le impostazioni generali dei messaggi. |
| [!DNL Channel Configurations] | [!UICONTROL Gestione predefiniti messaggi] | Accesso per leggere, creare, modificare ed eliminare i predefiniti per i messaggi. |
| [!DNL Channel Configurations] | [!UICONTROL Visualizza predefiniti messaggi] | Accesso in sola lettura ai predefiniti per messaggi. |
| [!DNL Channel Configurations] | [!UICONTROL Gestisci record PTR] | Accesso per la lettura e la modifica dei record PTR. |
| [!DNL Channel Configurations] | [!UICONTROL Visualizza record PTR] | Accesso in sola lettura ai record PTR. |
| [!DNL Channel Configurations] | [!UICONTROL Gestisci soppressione] | Accesso per leggere, creare, modificare ed eliminare le regole di soppressione. |
| [!DNL Channel Configurations] | [!UICONTROL Visualizza elenco di soppressione] | Accesso in sola lettura all’elenco di soppressione. |
| [!DNL Channel Configurations] | [!UICONTROL Esporta elenco di soppressione] | Accesso per esportare l’elenco di soppressione come file CSV. |
| [!DNL Channel Configurations] | [!UICONTROL Gestisci impostazioni pagina di destinazione] | Accesso per leggere, creare, modificare ed eliminare le impostazioni della pagina di destinazione. |
| [!DNL Channel Configurations] | [!UICONTROL Gestione impostazioni SMS] | Accesso per leggere, creare, modificare ed eliminare le impostazioni SMS. |
| [!DNL Channel Configurations] | [!UICONTROL Gestione sottodomini SMS] | Accesso per leggere, creare, modificare ed eliminare i sottodomini SMS. |
| [!DNL Channel Configurations] | [!UICONTROL Gestione indirizzamento file] | Accesso per la lettura, la creazione, la modifica e l&#39;eliminazione dei cicli di file. |
| [!DNL Channel Configurations] | [!UICONTROL Instradamento file visualizzazione] | Accesso in sola lettura ai cicli dei file. |
| [!DNL Channel Configurations] | [!UICONTROL Gestisci elenco seed] | Possibilità di creare e modificare l’elenco di seed. |
| [!DNL Channel Configurations] | [!UICONTROL Gestione impostazioni lingua] | Possibilità di creare e modificare le impostazioni della lingua. |
| [!DNL Channel Configurations] | [!UICONTROL Gestisci sottodomini Web] | Possibilità di creare e modificare i sottodomini web CJM. |
| [!DNL Channel Configurations] | [!UICONTROL Gestione credenziali push] | Possibilità di creare, modificare ed eliminare le credenziali push. |
| [!DNL Collaborations] | [!UICONTROL Gestisci istanze Collaboration] | Visualizzare, creare, aggiornare ed eliminare le istanze di collaborazione di un&#39;organizzazione. Scopri le istanze di collaborazione di altre organizzazioni. |
| [!DNL Collaborations] | [!UICONTROL Leggi istanze Collaboration] | Leggi le istanze di collaborazione di un’organizzazione e scopri le istanze di collaborazione di altre organizzazioni. |
| [!DNL Collaborations] | [!UICONTROL Gestisci inviti di connessione] | Visualizzare, creare ed eliminare gli inviti di connessione avviati dall&#39;organizzazione. Accetta e rifiuta l’invito alla connessione avviato da altre organizzazioni. |
| [!DNL Collaborations] | [!UICONTROL Leggi inviti di connessione] | Accesso in sola lettura agli inviti di connessione. |
| [!DNL Collaborations] | [!UICONTROL Gestione connessioni Collaboration] | Un inserzionista può visualizzare, creare e aggiornare le impostazioni, nonché inviare ed eliminare connessioni. Un editore può visualizzare, accettare o rifiutare le connessioni. |
| [!DNL Collaborations] | [!UICONTROL Leggi connessioni Collaboration] | Accesso in sola lettura alle connessioni. |
| [!DNL Collaborations] | [!UICONTROL Gestisci dati pubblico] | Eseguire l’onboarding e individuare i tipi di pubblico. Aggiorna i tipi di pubblico pubblici, privati e personalizzati e gestisci le impostazioni dei metadati di Inventario pubblico. |
| [!DNL Collaborations] | [!UICONTROL Leggi dati pubblico] | Leggi e individua i tipi di pubblico. |
| [!DNL Collaborations] | [!UICONTROL Gestisci dati di misurazione] | Integrare, aggiornare ed eliminare i dati di misurazione. |
| [!DNL Collaborations] | [!UICONTROL Leggi dati di misurazione] | Accesso in sola lettura ai dati di misurazione. |
| [!DNL Collaborations] | [!UICONTROL Gestisci progetti] | Visualizza, crea, aggiorna ed elimina progetti per qualsiasi attività di individuazione, condivisione, attivazione e misurazione. |
| [!DNL Collaborations] | [!UICONTROL Leggi progetti] | Visualizza i progetti per qualsiasi attività di individuazione, condivisione, attivazione e misurazione. |
| [!DNL Collaborations] | [!UICONTROL Attività di lettura utenti] | Accesso in sola lettura alle attività degli utenti. |
| [!DNL Collaborations] | [!UICONTROL Esporta attività utente] | Esporta attività utente. |
| [!DNL Collaborations] | [!UICONTROL Leggi monitoraggio crediti Collaboration] | Monitoraggio del credito a livello di organizzazione e istanza. |
| [!DNL Computed Attributes] | [!UICONTROL Visualizza attributi calcolati] | Accesso in sola lettura per la scheda degli attributi calcolati, l’inventario e i dettagli. |
| [!DNL Computed Attributes] | [!UICONTROL Gestisci attributi calcolati] | Accesso per leggere, creare, eliminare bozze e disattivare attributi calcolati. |
| [!DNL Customer Managed Keys] | [!UICONTROL Gestione chiavi gestite dal cliente] | Accesso per visualizzare e configurare le chiavi gestite dal cliente. |
| [!DNL Dashboards] | [!UICONTROL Visualizza dashboard utilizzo licenze] | Accesso in sola lettura per visualizzare il dashboard utilizzo licenze. |
| [!DNL Dashboards] | [!UICONTROL Gestione dashboard standard] | Aggiungi attributi personalizzati non ancora presenti nel data warehouse. |
| [!DNL Dashboards] | [!UICONTROL Visualizza dashboard standard] | Accesso in sola lettura ai dashboard Profili, Destinazioni e Segmenti. Consente inoltre di accedere alle dashboard nella barra di navigazione a sinistra e nella scheda Inventario dashboard e integrazioni. |
| [!DNL Dashboards] | [!UICONTROL Gestione dashboard personalizzati] | Accesso per creare o modificare un dashboard. |
| [!DNL Dashboards] | [!UICONTROL Visualizza dashboard personalizzati] | Accesso in sola lettura alle dashboard definite dall&#39;utente. |
| [!DNL Dashboards] | [!UICONTROL Gestione pianificazioni report] | Possibilità di creare pianificazioni. |
| [!DNL Dashboards] | [!UICONTROL Esporta dati dashboard] | Controlla la capacità di un utente di esportare dati tabulari dai dashboard in modalità query pro. |
| [!DNL Data Collection] | [!UICONTROL Gestisci flussi di dati] | Accesso per leggere, creare e modificare gli stream di dati. |
| [!DNL Data Collection] | [!UICONTROL Visualizza flussi di dati] | Accesso in sola lettura agli stream di dati. |
| [!DNL Data Governance] | [!UICONTROL Gestisci etichette di utilizzo] | Accesso per leggere, creare ed eliminare le etichette di utilizzo. |
| [!DNL Data Governance] | [!UICONTROL Gestisci criteri di utilizzo dati] | Accesso per leggere, creare, modificare ed eliminare i criteri di utilizzo dei dati. |
| [!DNL Data Governance] | [!UICONTROL Visualizza criteri di utilizzo dati] | Accesso in sola lettura per i criteri di utilizzo dei dati appartenenti alla tua organizzazione. |
| [!DNL Data Governance] | [!UICONTROL Visualizza registro attività utente] | Accesso in sola lettura per visualizzare i [registri di controllo](../landing/governance-privacy-security/audit-logs/overview.md) registrati delle attività di Experience Platform. |
| [!DNL Data Governance] | [!UICONTROL Visualizza console per la privacy] | Accesso in sola lettura alle console per la privacy. |
| [!DNL Data Ingestion] | [!UICONTROL Gestisci origini] | Accesso per leggere, creare, modificare e disabilitare le origini. |
| [!DNL Data Ingestion] | [!UICONTROL Visualizza origini] | Accesso in sola lettura alle origini disponibili nella scheda **[!UICONTROL Catalogo]** e alle origini autenticate nella scheda **[!UICONTROL Sfoglia]**. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | Accesso per creare, accettare e rifiutare la condivisione partner per connettere due organizzazioni e abilitare [!DNL Segment Match] flussi. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share] | Accesso a lettura, creazione, modifica e pubblicazione di [!DNL Segment Match] feed con partner attivi. |
| [!DNL Data Lifecycle] | [!UICONTROL Visualizza ciclo di vita dati] | Accesso in sola lettura per il ciclo di vita dei dati. |
| [!DNL Data Lifecycle] | [!UICONTROL Gestione ciclo di vita dati] | Accesso per leggere, creare, modificare ed eliminare il ciclo di vita dei dati. |
| [!DNL Data Modeling] | [!UICONTROL Gestisci schemi] | Accesso per leggere, creare, modificare ed eliminare schemi e risorse correlate. |
| [!DNL Data Modeling] | [!UICONTROL Visualizza schemi] | Accesso in sola lettura agli schemi e alle risorse correlate. |
| [!DNL Data Modeling] | [!UICONTROL Gestisci relazioni] | Accesso per leggere, creare, modificare ed eliminare le relazioni tra schemi. |
| [!DNL Data Modeling] | [!UICONTROL Gestisci metadati identità] | Accesso per leggere, creare, modificare ed eliminare i metadati di identità per gli schemi. |
| [!DNL Data Management] | [!UICONTROL Gestisci set di dati] | Accesso per leggere, creare, modificare ed eliminare i set di dati. Accesso in sola lettura per gli schemi. |
| [!DNL Data Management] | [!UICONTROL Visualizza set di dati] | Accesso in sola lettura per set di dati e schemi. |
| [!DNL Data Management] | [!UICONTROL Monitoraggio dei dati] | Accesso in sola lettura ai set di dati e ai flussi di monitoraggio. |
| [!DNL Data Science Workspace] | [!UICONTROL Gestisci Data Science Workspace] | Accesso a lettura, creazione, modifica ed eliminazione in [!DNL Data Science Workspace]. |
| [!DNL Decision Management] | [!UICONTROL Gestione di Experience Decisioning] | Possibilità di gestire le entità Experience Decisioning. |
| [!DNL Decision Management] | [!UICONTROL Visualizza Experience Decisioning] | Accesso in sola lettura alle entità Experience Decisioning. |
| [!DNL Decision Management] | [!UICONTROL Gestisci decisioni] | Accesso per leggere, creare, modificare ed eliminare entità decisionali. |
| [!DNL Decisions Management] | [!UICONTROL Visualizza decisioni] | Accesso in sola lettura alle entità decisionali. |
| [!DNL Decision Management] | [!UICONTROL Gestisci offerte] | Accesso per leggere, creare, modificare ed eliminare tutte le offerte e i componenti. Accesso in sola lettura a decisioni e raccolte. |
| [!DNL Decsion Management] | [!UICONTROL Gestione strategie di classificazione] | Accesso per leggere, creare, modificare ed eliminare rapporti personalizzati e utilizzare le funzioni di azione. |
| [!DNL Destinations] | [!UICONTROL Visualizza destinazioni] | Accesso in sola lettura per visualizzare le destinazioni disponibili nella scheda **[!UICONTROL Catalogo]** e le destinazioni autenticate nella scheda **[!UICONTROL Sfoglia]**. |
| [!DNL Destinations] | [!UICONTROL Gestione destinazioni] | Accesso per leggere, creare ed eliminare connessioni di destinazioni e account di destinazione. |
| [!DNL Destinations] | [!UICONTROL Attiva destinazioni] | Possibilità di attivare i dati per le destinazioni attive create. Questa autorizzazione richiede anche che [!UICONTROL Visualizza destinazioni] o [!UICONTROL Gestisci destinazioni] sia concesso all&#39;utente che attiverà le destinazioni. |
| [!DNL Destinations] | [!UICONTROL Attiva segmento senza mapping] | Possibilità di attivare i tipi di pubblico nelle destinazioni esistenti, senza visualizzare il [passaggio di mappatura](../destinations/ui/activate-batch-profile-destinations.md#mapping). Gli utenti possono aggiungere e rimuovere tipi di pubblico nei flussi di lavoro di attivazione, ma non possono aggiungere o rimuovere attributi o identità mappati. Questa autorizzazione richiede anche l&#39;autorizzazione [!UICONTROL Visualizza destinazioni] per essere concessa all&#39;utente che attiverà i dati nelle destinazioni. |
| [!DNL Destinations] | [!UICONTROL Gestione e attivazione delle destinazioni del set di dati] | Possibilità di leggere, creare, modificare e disabilitare i flussi di esportazione dei set di dati. Possibilità di attivare i dati anche per i set di dati attivi che sono stati creati. Questa autorizzazione richiede anche l&#39;autorizzazione [!UICONTROL Visualizza destinazioni] per essere concessa all&#39;utente che attiverà i dati nelle destinazioni. |
| [!DNL Destinations] | [!UICONTROL Authoring delle destinazioni] | Possibilità di creare destinazioni utilizzando [Adobe Experience Platform Destination SDK](../destinations/destination-sdk/overview.md). |
| [!DNL Federated Data] | [!UICONTROL Gestisci dati federati] | Possibilità di accedere a tutte le funzionalità di dati federati, ad esempio la creazione di schemi, modelli e composizioni. |
| [!DNL Identity Management] | [!UICONTROL Gestione spazi dei nomi delle identità] | Accesso per leggere, creare, modificare ed eliminare spazi dei nomi di identità. |
| [!DNL Identity Management] | [!UICONTROL Visualizza Spazi Dei Nomi Delle Identità] | Accesso in sola lettura per gli spazi dei nomi di identità. |
| [!DNL Identity Management] | [!UICONTROL Visualizza grafico identità] | Accesso in sola lettura per i grafici di identità. |
| [!DNL Identity Management] | [!UICONTROL Gestione impostazioni identità] | Accesso per leggere, creare e modificare le impostazioni di identità. |
| [!DNL Identity Management] | [!UICONTROL Visualizza impostazioni identità] | Accesso in sola lettura alle impostazioni di identità. |
| [!DNL Intelligent Services] | [!UICONTROL Visualizza IA per l&#39;attribuzione] | Accesso in sola lettura per le impostazioni e le informazioni di Attribution AI. |
| [!DNL Intelligent Services] | [!UICONTROL Gestisci IA per l&#39;attribuzione] | Accesso per leggere, creare, modificare ed eliminare modelli di IA per l’attribuzione. |
| [!DNL Intelligent Services] | [!UICONTROL Visualizza IA per l&#39;analisi dei clienti] | Accesso per leggere o visualizzare i modelli di IA per l’analisi dei clienti. |
| [!DNL Intelligent Services] | [!UICONTROL Gestisci IA per l&#39;analisi dei clienti] | Accesso per creare, aggiornare, eliminare, abilitare o disabilitare modelli di IA per l’analisi dei clienti. |
| [!DNL IP Warmup Configurations] | [!UICONTROL Visualizza piani di riscaldamento IP] | Accesso in sola lettura ai piani di riscaldamento IP. |
| [!DNL IP Warmup Configurations] | [!UICONTROL Gestisci piani di riscaldamento IP] | Possibilità di gestire i piani di riscaldamento IP. |
| [!DNL IP Warmup Configurations] | [!UICONTROL Visualizza report di riscaldamento IP] | Accesso in sola lettura ai report di riscaldamento IP. |
| [!DNL Journeys] | [!UICONTROL Gestisci Percorsi] | Accesso per leggere, creare, modificare ed eliminare percorsi. |
| [!DNL Journeys] | [!UICONTROL Visualizza Percorsi] | Accesso in sola lettura ai percorsi. |
| [!DNL Journeys] | [!UICONTROL Visualizza report Percorsi] | Rapporto Accesso in sola lettura ai percorsi. |
| [!DNL Journeys] | [!UICONTROL Gestire eventi, origini dati e azioni dei Percorsi] | Accesso per leggere, creare, modificare ed eliminare eventi, origini dati o azioni. |
| [!DNL Journeys] | [!UICONTROL Visualizza eventi Percorsi, origini dati e azioni] | Accesso in sola lettura a eventi, origini dati o azioni. |
| [!DNL Journeys] | [!UICONTROL Approva e pubblica Percorsi] | Possibilità di approvare e pubblicare percorsi quando viene applicato un criterio. |
| [!DNL Journeys] | [!UICONTROL Pubblica Percorsi] | Possibilità di pubblicare percorsi. |
| [!DNL Journey Optimizer Library] | [!UICONTROL Gestisci elementi della libreria] | Possibilità di aggiungere ed eliminare espressioni salvate. |
| [!DNL Journey Optimizer Library] | [!UICONTROL Pubblica frammenti] | Possibilità di pubblicare frammenti di contenuto. |
| [!DNL Journey Optimizer Library] | [!UICONTROL Simula contenuto] | Accesso all’opzione Simula contenuto per l’anteprima e la verifica. |
| [!DNL Journey Optimizer Rules] | [!UICONTROL Visualizza regole di frequenza] | Accesso in sola lettura alle regole di frequenza. |
| [!DNL Journey Optimizer Rules] | [!UICONTROL Gestisci regole di frequenza] | Accesso per leggere, creare, modificare o eliminare regole di frequenza. |
| [!DNL Messages] | [!UICONTROL Gestione messaggi] | Accesso per leggere, creare, modificare ed eliminare i messaggi. |
| [!DNL Messages] | [!UICONTROL Visualizza messaggi] | Accesso in sola lettura ai messaggi. |
| [!DNL Messages] | [!UICONTROL Visualizza report messaggi] | Accesso per leggere e modificare i rapporti sui messaggi. |
| [!DNL Messages] | [!UICONTROL Pubblica messaggi] | Possibilità di pubblicare messaggi. |
| [!DNL Messages] | [!UICONTROL Anteprima e prova gestione messaggi] | Possibilità di approvare e pubblicare messaggi quando viene applicato un criterio. |
| [!DNL Privacy Service] | [!UICONTROL Gestisci Privacy Service] | Accesso ai flussi di lavoro di privacy in lettura e scrittura. |
| [!DNL Privacy Service] | [!UICONTROL Visualizza Privacy Service] | Accesso in sola lettura ai flussi di lavoro sulla privacy. |
| [!DNL Profile Management] | [!UICONTROL Gestisci profili] | Accesso per leggere, creare, modificare ed eliminare i set di dati utilizzati per i profili dei clienti. Accesso in sola lettura ai profili disponibili. |
| [!DNL Profile Management] | [!UICONTROL Visualizza profili] | Accesso in sola lettura ai profili disponibili. |
| [!DNL Profile Management] | [!UICONTROL Gestisci segmenti] | Accesso per leggere, creare, modificare ed eliminare tipi di pubblico. |
| [!DNL Profile Management] | [!UICONTROL Visualizza segmenti] | Accesso in sola lettura al pubblico disponibile. |
| [!DNL Profile Management] | [!UICONTROL Gestisci criteri di unione] | Accesso per leggere, creare, modificare ed eliminare i criteri di unione. |
| [!DNL Profile Management] | [!UICONTROL Visualizza criteri di unione] | Accesso in sola lettura ai criteri di unione disponibili. |
| [!DNL Profile Management] | [!UICONTROL Importa tipi di pubblico] | Possibilità di utilizzare il flusso di lavoro di caricamento CSV per importare nuovi tipi di pubblico. |
| [!DNL Profile Management] | [!UICONTROL Esporta segmento di pubblico] | Possibilità di esportare un pubblico valutato in un set di dati. |
| [!DNL Profile Management] | [!UICONTROL Valuta un segmento in un pubblico] | Possibilità di generare profili per un pubblico valutando una definizione di segmento. |
| [!DNL Profile Management] | [!UICONTROL Visualizza IA B2B] | Accesso in sola lettura alle impostazioni e alle configurazioni per tutti i servizi di IA/ML B2B. |
| [!DNL Profile Management] | [!UICONTROL Gestione IA B2B] | Accesso per leggere, creare, modificare ed eliminare impostazioni e configurazioni per tutti i servizi di IA/ML B2B. |
| [!DNL Profile Management] | [!UICONTROL Visualizza profilo B2B] | Accesso in sola lettura a profili di entità B2B (come Account, Opportunità e così via), impostazioni e configurazioni per tutti i servizi AI/ML B2B e i widget del dashboard B2B. |
| [!DNL Profile Management] | [!UICONTROL Gestisci profilo B2B] | Accesso per leggere, creare, modificare ed eliminare profili di entità B2B (come Account, Opportunità e così via). Accesso in sola lettura per impostazioni e configurazioni per tutti i servizi AI/ML B2B e i widget del dashboard B2B. |
| [!DNL Profile Management] | [!UICONTROL Gestisci lookalike] | Possibilità di creare o eliminare tipi di pubblico simili. |
| [!DNL Profile Management] | [!UICONTROL Visualizza esperienza B2B] | Possibilità di visualizzare profili e attributi B2B. |
| [!DNL Profile Management] | [!UICONTROL Visualizza impostazioni profilo] | Accesso in sola lettura a tutte le impostazioni del profilo. |
| [!DNL Profile Management] | [!UICONTROL Gestione impostazioni profilo] | Accesso per leggere e modificare tutte le impostazioni di profilo. |
| [!DNL Prospects] | [!UICONTROL Visualizza potenziali clienti] | Accesso in sola lettura a schemi, profili, tipi di pubblico e pannello a soffietto del potenziale cliente. |
| [!DNL Prospects] | [!UICONTROL Gestisci potenziali clienti] | Possibilità di creare e gestire schemi, profili e tipi di pubblico potenziali. Accesso in sola lettura al pannello a soffietto del prospect. |
| [!DNL Query Service] | [!UICONTROL Gestisci query] | Accesso per leggere, creare, modificare ed eliminare query SQL strutturate per i dati di Experience Platform. |
| [!DNL Query Service] | [!UICONTROL Gestisci integrazione servizio query] | Accesso per creare, aggiornare ed eliminare credenziali senza scadenza per l’accesso a Query Service. |
| [!DNL Query Service] | [!UICONTROL Gestione sessioni query] | Possibilità di eliminare le sessioni esistenti. |
| [!DNL Query Service] | [!UICONTROL Gestisci Elenco consentiti] | Possibilità di gestire le restrizioni IP per la tua organizzazione. |
| [!DNL Reports] | [!UICONTROL Visualizza report canale] | Possibilità di visualizzare e modificare i rapporti sui canali. |
| [!DNL Sandbox Administration] | [!UICONTROL Gestione sandbox] | Accesso alle sandbox di lettura, creazione, modifica ed eliminazione. |
| [!DNL Sandbox Administration] | [!UICONTROL Visualizza Sandbox] | Accesso in sola lettura per le sandbox appartenenti alla tua organizzazione. |
| [!DNL Sandbox Administration] | [!UICONTROL Ripristinare una sandbox] | Possibilità di ripristinare una sandbox. |
| [!DNL Sandbox Administration] | [!UICONTROL Gestisci pacchetti] | Accesso per creare, importare o esportare pacchetti. |
| [!DNL Sandbox Administration] | [!UICONTROL Condividi pacchetti] | Accesso per la condivisione di pacchetti tra organizzazioni diverse. |
| [!DNL Traits Configurations] | [!UICONTROL Visualizza caratteristiche] | Accesso in sola lettura per le caratteristiche. |
| [!DNL Traits Configurations] | [!UICONTROL Gestione caratteristiche] | Accesso per gestire le caratteristiche. |
| [!DNL Translation Service] | [!UICONTROL Gestisci progetti di traduzione] | La capacità di gestire i progetti di traduzione. |
| [!DNL Translation Service] | [!UICONTROL Visualizza progetti di traduzione] | Accesso in sola lettura ai progetti di traduzione. |
| [!DNL Translation Service] | [!UICONTROL Gestione attività di traduzione] | La possibilità di gestire le attività di traduzione. |
| [!DNL Translation Service] | [!UICONTROL Visualizza attività di traduzione] | Accesso in sola lettura alle attività di traduzione. |
| [!DNL Translation Service] | [!UICONTROL Gestisci recensioni traduzione] | La possibilità di gestire le revisioni di traduzione. |
| [!DNL Translation Service] | [!UICONTROL Visualizza recensioni traduzione] | Accesso in sola lettura alle recensioni di traduzione. |
| [!DNL Translation Service] | [!UICONTROL Gestione traduzione interna] | La capacità di gestire la traduzione internamente. |
| [!DNL Translation Service] | [!UICONTROL Visualizza traduzione interna] | Accesso in sola lettura alla traduzione interna. |
| [!DNL Translation Service] | [!UICONTROL Gestione impostazioni di traduzione] | Possibilità per gli amministratori di gestire le impostazioni di traduzione. |
| [!DNL Translation Service] | [!UICONTROL Gestisci provider di traduzione] | La capacità di gestire i fornitori di traduzione. |

## Passaggi successivi

Una volta letta questa guida, potrai scoprire i principi fondamentali del controllo degli accessi in Experience Platform. Ora puoi passare alla [guida utente per il controllo degli accessi basato su attributi](./abac/overview.md) per i passaggi dettagliati su come utilizzare Experience Cloud per creare ruoli e assegnare autorizzazioni per Experience Platform.
