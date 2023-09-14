---
keywords: Experience Platform;home;argomenti popolari;controllo degli accessi;adobe admin console
solution: Experience Platform
title: Panoramica sul controllo degli accessi
description: Il controllo degli accessi per Adobe Experience Platform viene fornito tramite Adobe Admin Console. Questa funzionalità sfrutta i profili di prodotto di Admin Console, che collegano gli utenti con autorizzazioni e sandbox.
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: d83a5558d706e7bf059edb912f6fd43d4b66cc54
workflow-type: tm+mt
source-wordcount: '1678'
ht-degree: 3%

---

# Panoramica sul controllo degli accessi

Il controllo degli accessi per Adobe Experience Platform viene fornito tramite **[!UICONTROL Autorizzazioni]** in [Adobe Experience Cloud](https://experience.adobe.com/). Questa funzionalità sfrutta ruoli e criteri, che collegano gli utenti con autorizzazioni e sandbox.

## Gerarchia e flusso di lavoro di controllo degli accessi

Per configurare il controllo degli accessi, ad Experience Platform, è necessario disporre dei privilegi di amministratore di sistema o di prodotto per un&#39;organizzazione che dispone di un prodotto Experienci Platform. Il ruolo minimo che può concedere o revocare le autorizzazioni è quello di amministratore di prodotto. Altri ruoli di amministratore che possono gestire le autorizzazioni sono amministratori di sistema (senza restrizioni). Consulta l’articolo di Adobe Help Center su [ruoli amministrativi](https://helpx.adobe.com/it/enterprise/using/admin-roles.html) per ulteriori informazioni.

>[!NOTE]
>
>Da questo punto in poi, qualsiasi menzione di &quot;amministratore&quot; in questo documento si riferisce a un amministratore di prodotto o a un livello superiore (come descritto sopra).

Un flusso di lavoro di alto livello per l’ottenimento e l’assegnazione delle autorizzazioni di accesso può essere riassunto come segue:

- Dopo aver concesso la licenza per Adobe Experience Platform o un servizio applicazione/app che utilizza Experienci Platform, viene inviata un’e-mail all’amministratore specificato durante la gestione della licenza.
- L’amministratore accede a [Adobe Admin Console](#adobe-admin-console) e seleziona **Adobe Experience Platform** dall’elenco dei prodotti nella pagina della panoramica.
- Per concedere l’accesso a Experienci Platform, l’amministratore dovrà aggiungere gli utenti al profilo di prodotto predefinito: `AEP-Default-All-Users`.
- Nell&#39;Experience Platform Autorizzazioni, l&#39;amministratore può creare nuovi ruoli o modificare le autorizzazioni e gli utenti per qualsiasi ruolo esistente.
- Durante la creazione o la modifica di un ruolo, l&#39;amministratore aggiunge gli utenti al ruolo utilizzando **[!UICONTROL utenti]** e concede le autorizzazioni a questi utenti (ad esempio &quot;[!UICONTROL Leggi set di dati]&quot; o &quot;[!UICONTROL Gestire gli schemi]&quot;) modificando le autorizzazioni del ruolo. Analogamente, l’amministratore può assegnare l’accesso alle sandbox utilizzando la stessa opzione di modifica.
- Quando gli utenti accedono all’interfaccia utente di Experienci Platform, il loro accesso alle funzionalità di Experienci Platform è guidato dalle autorizzazioni concesse loro dal passaggio precedente. Ad esempio, se un utente non dispone di [!UICONTROL Visualizzare i set di dati] autorizzazione, **[!UICONTROL Set di dati]** nel menu laterale non sarà visibile a tale utente.

Per i passaggi più dettagliati su come gestire il controllo degli accessi in Experienci Platform, vedi [guida utente al controllo degli accessi](./ui/overview.md).

Tutte le chiamate alle API Experienci Platform vengono convalidate per le autorizzazioni e restituiranno errori se le autorizzazioni appropriate non vengono trovate nel contesto utente corrente. Nell’interfaccia utente, gli elementi verranno nascosti o modificati a seconda delle autorizzazioni concesse all’utente corrente.

## Autorizzazioni {#platform-permissions}

[!UICONTROL Autorizzazioni] fornisce una posizione centrale per la gestione dell’accesso Experienci Platform per la tua organizzazione. Da a [!UICONTROL Autorizzazioni], puoi concedere a gruppi di utenti le autorizzazioni di accesso per varie funzionalità di Experience Platform, come [!UICONTROL Gestione set di dati], [!UICONTROL Visualizzare i set di dati], o [!UICONTROL Gestisci profili].

### Ruoli

In [!UICONTROL Ruoli] sezione, le autorizzazioni vengono assegnate agli utenti tramite l’utilizzo di ruoli. I ruoli consentono di concedere autorizzazioni a uno o più utenti e contengono anche il loro accesso all’ambito delle sandbox assegnate loro tramite i ruoli. Gli utenti possono essere assegnati a uno o più ruoli appartenenti alla tua organizzazione.

### Ruoli predefiniti

Experienci Platform viene fornito con due ruoli predefiniti preconfigurati. La tabella seguente illustra cosa viene fornito in ciascun profilo predefinito, inclusa la sandbox a cui concedono l’accesso e le autorizzazioni che concedono nell’ambito di tale sandbox.

| Ruolo | Accesso alla sandbox | Autorizzazioni |
| --- | --- | --- |
| Accesso predefinito per tutti gli elementi di produzione | Produzione | Tutte le autorizzazioni applicabili ad Experienci Platform, ad eccezione delle autorizzazioni di amministrazione delle sandbox. |
| Amministratori sandbox | N/D | Consente di accedere solo alle autorizzazioni di amministrazione delle sandbox. |

## Sandbox e autorizzazioni

Le sandbox non di produzione sono una forma di virtualizzazione dei dati che consente di isolare i dati da altre sandbox e sono in genere utilizzate per esperimenti di sviluppo, test o test. Le autorizzazioni di un ruolo consentono agli utenti del ruolo di accedere alle funzioni Experienci Platform all’interno degli ambienti sandbox a cui hanno accesso. Una licenza di Experience Platform predefinita ti concede cinque sandbox (una di produzione e quattro non di produzione). Puoi aggiungere pacchetti di dieci sandbox non di produzione per un massimo di 75 sandbox in totale. Per ulteriori informazioni, contatta l’amministratore della tua organizzazione o il tuo rappresentante commerciale Adobe.

Per ulteriori informazioni sulle sandbox in Experienci Platform, consulta la sezione [panoramica sulle sandbox](../sandboxes/home.md).

### Accesso alle sandbox

L’accesso alle sandbox viene gestito tramite i ruoli. Per i passaggi dettagliati su come abilitare l’accesso a una sandbox per un ruolo, vedi [guida ai ruoli di controllo dell’accesso basato su attributi](./abac/ui/roles.md).

Gli utenti possono essere autorizzati ad accedere a una o più sandbox all’interno di un ruolo. Se un utente è incluso in due o più ruoli, avrà accesso a tutte le sandbox incluse in tali ruoli.

L’autorizzazione &quot;Sandbox Management&quot; (Gestione sandbox) consente agli utenti di gestire, visualizzare o ripristinare le sandbox.

### Autorizzazioni delle risorse {#permissions}

La risorsa [!UICONTROL Autorizzazioni] In una scheda di un ruolo vengono visualizzate le sandbox e le autorizzazioni attive per tale ruolo:

![permissions-overview](./images/permissions.png)

Le autorizzazioni concesse tramite le autorizzazioni per le risorse sono ordinate per categoria, con alcune autorizzazioni che concedono l’accesso a diverse funzionalità di basso livello.

Nella tabella seguente vengono descritte le autorizzazioni disponibili, ad Experience Platform nel ruolo, con le descrizioni delle funzionalità di Experience Platform specifiche a cui concedono l’accesso. Per i passaggi dettagliati su come aggiungere le autorizzazioni a un ruolo, vedi [guida ai ruoli di controllo dell’accesso basato su attributi](./abac/ui/roles.md).

| Categoria | Autorizzazione | Descrizione |
| --- | --- | --- |
| [!DNL Alerts] | [!UICONTROL Visualizza cronologia avvisi] | Accesso in sola lettura per la cronologia degli avvisi. |
| [!DNL Alerts] | [!UICONTROL Risolvi avvisi] | Accesso per leggere, modificare ed eliminare gli avvisi. |
| [!DNL Alerts] | [!UICONTROL Visualizza avvisi] | Accesso in sola lettura per gli avvisi. |
| [!DNL Alerts] | [!UICONTROL Gestire gli avvisi] | Accesso per leggere, creare, modificare ed eliminare la cronologia degli avvisi. |
| [!DNL Data Hygiene] | [!UICONTROL Visualizza igiene dei dati] | Accesso in sola lettura per l’igiene dei dati. |
| [!DNL Data Hygiene] | [!UICONTROL Gestire l’igiene dei dati] | Accesso per leggere, creare, modificare ed eliminare l’igiene dei dati. |
| [!DNL Data Modeling] | [!UICONTROL Gestire gli schemi] | Accesso per leggere, creare, modificare ed eliminare schemi e risorse correlate. |
| [!DNL Data Modeling] | [!UICONTROL Visualizzare gli schemi] | Accesso in sola lettura agli schemi e alle risorse correlate. |
| [!DNL Data Modeling] | [!UICONTROL Gestire le relazioni] | Accesso per leggere, creare, modificare ed eliminare le relazioni tra schemi. |
| [!DNL Data Modeling] | [!UICONTROL Gestire i metadati di identità] | Accesso per leggere, creare, modificare ed eliminare i metadati di identità per gli schemi. |
| [!DNL Data Management] | [!UICONTROL Gestione set di dati] | Accesso per leggere, creare, modificare ed eliminare i set di dati. Accesso in sola lettura per gli schemi. |
| [!DNL Data Management] | [!UICONTROL Visualizzare i set di dati] | Accesso in sola lettura per set di dati e schemi. |
| [!DNL Data Management] | [!UICONTROL Monitoraggio dei dati] | Accesso in sola lettura ai set di dati e ai flussi di monitoraggio. |
| [!DNL Profile Management] | [!UICONTROL Gestisci profili] | Accesso per leggere, creare, modificare ed eliminare i set di dati utilizzati per i profili dei clienti. Accesso in sola lettura ai profili disponibili. |
| [!DNL Profile Management] | [!UICONTROL Visualizza profili] | Accesso in sola lettura ai profili disponibili. |
| [!DNL Profile Management] | [!UICONTROL Gestire segmenti] | Accesso per leggere, creare, modificare ed eliminare segmenti. |
| [!DNL Profile Management] | [!UICONTROL Visualizzare segmenti] | Accesso in sola lettura ai segmenti disponibili. |
| [!DNL Profile Management] | [!UICONTROL Gestisci criteri di unione] | Accesso per leggere, creare, modificare ed eliminare i criteri di unione. |
| [!DNL Profile Management] | [!UICONTROL Visualizza criteri di unione] | Accesso in sola lettura ai criteri di unione disponibili. |
| [!DNL Profile Management] | [!UICONTROL Esporta pubblico per segmento] | Possibilità di esportare un segmento di pubblico valutato in un set di dati. |
| [!DNL Profile Management] | [!UICONTROL Valutare un segmento in un pubblico] | Possibilità di generare profili per un pubblico valutando una definizione di segmento. |
| [!DNL Profile Management] | [!UICONTROL Visualizza IA B2B] | Accesso in sola lettura alle impostazioni e alle configurazioni per tutti i servizi di IA/ML B2B. |
| [!DNL Profile Management] | [!UICONTROL Gestire IA B2B] | Accesso per leggere, creare, modificare ed eliminare impostazioni e configurazioni per tutti i servizi di IA/ML B2B. |
| [!DNL Profile Management] | [!UICONTROL Visualizza profilo B2B] | Accesso in sola lettura a profili di entità B2B (come Account, Opportunità e così via), impostazioni e configurazioni per tutti i servizi AI/ML B2B e i widget del dashboard B2B. |
| [!DNL Profile Management] | [!UICONTROL Gestisci profilo B2B] | Accesso per leggere, creare, modificare ed eliminare profili di entità B2B (come Account, Opportunità e così via). Accesso in sola lettura per impostazioni e configurazioni per tutti i servizi AI/ML B2B e i widget del dashboard B2B. |
| [!DNL Identity Management] | [!UICONTROL Manage Identity Namespaces (Gestisci spazi dei nomi di identità)] | Accesso per leggere, creare, modificare ed eliminare spazi dei nomi di identità. |
| [!DNL Identity Management] | [!UICONTROL Visualizzare gli spazi dei nomi delle identità] | Accesso in sola lettura per gli spazi dei nomi di identità. |
| [!DNL Identity Management] | [!UICONTROL Visualizza grafico delle identità] | Accesso in sola lettura per i grafici di identità. |
| [!DNL Sandbox Administration] | [!UICONTROL Gestione sandbox] | Accesso alle sandbox di lettura, creazione, modifica ed eliminazione. |
| [!DNL Sandbox Administration] | [!UICONTROL View Sandboxes (Visualizza sandbox)] | Accesso in sola lettura per le sandbox appartenenti alla tua organizzazione. |
| [!DNL Sandbox Administration] | [!UICONTROL Ripristinare una sandbox] | Possibilità di ripristinare una sandbox. |
| [!DNL Destinations] | [!UICONTROL Gestire le destinazioni] | Accesso per leggere, creare ed eliminare flussi di attivazione delle destinazioni e account di destinazione. |
| [!DNL Destinations] | [!UICONTROL Visualizza destinazioni] | Accesso in sola lettura alle destinazioni disponibili in **[!UICONTROL Catalogo]** e le destinazioni autenticate in **[!UICONTROL Sfoglia]** scheda. |
| [!DNL Destinations] | [!UICONTROL Attivare le destinazioni] | Consente agli utenti di attivare i segmenti nelle destinazioni esistenti. Abilita il passaggio di mappatura nel flusso di lavoro di attivazione. Questa autorizzazione richiede [!UICONTROL Visualizza destinazioni] o [!UICONTROL Gestire le destinazioni] da concedere all’utente che attiverà i dati nelle destinazioni. |
| [!DNL Destinations] | [!UICONTROL Attiva segmento senza mappatura] | Consente agli utenti di attivare i segmenti nelle destinazioni esistenti, senza visualizzare [passaggio di mappatura](../destinations/ui/activate-batch-profile-destinations.md#mapping). Gli utenti possono aggiungere e rimuovere segmenti nei flussi di lavoro di attivazione, ma non possono aggiungere o rimuovere gli attributi o le identità mappate. Questa autorizzazione richiede [!UICONTROL Attivare le destinazioni] autorizzazione da concedere all’utente che attiverà i dati nelle destinazioni. |
| [!DNL Destinations] | [!UICONTROL Gestire e attivare le destinazioni dei set di dati] | Possibilità di leggere, creare, modificare e disabilitare i flussi di esportazione dei set di dati. Possibilità di attivare i dati anche per i set di dati attivi che sono stati creati. |
| [!DNL Destinations] | [!UICONTROL Authoring delle destinazioni] | Possibilità di creare destinazioni utilizzando [Adobe Experience Platform Destination SDK](../destinations/destination-sdk/overview.md). |
| [!DNL Data Ingestion] | [!UICONTROL Gestisci origini] | Accesso per leggere, creare, modificare e disabilitare le origini. |
| [!DNL Data Ingestion] | [!UICONTROL Visualizza origini] | Accesso in sola lettura alle origini disponibili in **[!UICONTROL Catalogo]** e le origini autenticate in **[!UICONTROL Sfoglia]** scheda. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | Accesso per creare, accettare e rifiutare handshake partner per connettere due organizzazioni e abilitare [!DNL Segment Match] flussi. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share] | Accesso a lettura, creazione, modifica e pubblicazione [!DNL Segment Match] feed con partner attivi. |
| [!DNL Data Science Workspace] | [!UICONTROL Gestire Data Science Workspace] | Accesso a lettura, creazione, modifica ed eliminazione in [!DNL Data Science Workspace]. |
| Governance dei dati | [!UICONTROL Applica etichette di utilizzo dati] | Accesso per leggere, creare ed eliminare le etichette di utilizzo. |
| Governance dei dati | [!UICONTROL Gestire i criteri di utilizzo dei dati] | Accesso per leggere, creare, modificare ed eliminare i criteri di utilizzo dei dati. |
| Governance dei dati | [!UICONTROL Visualizza criteri di utilizzo dati] | Accesso in sola lettura per i criteri di utilizzo dei dati appartenenti alla tua organizzazione. |
| Governance dei dati | [!UICONTROL Visualizza registro attività utente] | Accesso in sola lettura per visualizzare i dati registrati [registri di audit](../landing/governance-privacy-security/audit-logs/overview.md) delle attività di Platform. |
| [!DNL Dashboards] | [!UICONTROL Visualizza dashboard utilizzo licenze] | Accesso in sola lettura per visualizzare il dashboard utilizzo licenze. |
| [!DNL Dashboards] | [!UICONTROL Gestione dashboard standard] | Aggiungi attributi personalizzati non ancora presenti nel data warehouse. |
| [!DNL Query Service] | [!UICONTROL Gestire le query] | Accesso per leggere, creare, modificare ed eliminare query SQL strutturate per i dati di Platform. |
| [!DNL Query Service] | [!UICONTROL Gestire l’integrazione di Query Service] | Accesso per creare, aggiornare ed eliminare credenziali senza scadenza per l’accesso a Query Service. |

## Passaggi successivi

Una volta letta questa guida, potrai scoprire i principi fondamentali del controllo degli accessi in Experienci Platform. Ora puoi passare alla sezione [guida utente per il controllo degli accessi basato su attributi](./abac/overview.md) per i passaggi dettagliati su come utilizzare Experience Cloud per creare ruoli e assegnare autorizzazioni, ad Experience Platform.
