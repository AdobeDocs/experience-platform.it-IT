---
keywords: Experience Platform;home;argomenti popolari;controllo accessi;adobe admin console
solution: Experience Platform
title: Panoramica sul controllo degli accessi
description: Il controllo degli accessi per Adobe Experience Platform è fornito tramite Adobe Admin Console. Questa funzionalità sfrutta i profili di prodotto in Admin Console, che collegano gli utenti con autorizzazioni e sandbox.
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1540'
ht-degree: 3%

---

# Panoramica sul controllo degli accessi

Controllo di accesso per [!DNL Experience Platform] è fornito tramite [Adobe Admin Console](https://adminconsole.adobe.com). Questa funzionalità sfrutta i profili di prodotto in [!DNL Admin Console], che collega gli utenti con autorizzazioni e sandbox.

## Accedere alla gerarchia di controllo e al flusso di lavoro

Per configurare il controllo di accesso per [!DNL Experience Platform], è necessario disporre dei privilegi di amministratore per un&#39;organizzazione con un [!DNL Experience Platform] integrazione del prodotto. Il ruolo minimo che concede o revoca le autorizzazioni è un amministratore del profilo di prodotto. Altri ruoli di amministratore che possono gestire le autorizzazioni sono gli amministratori dei prodotti (possono gestire tutti i profili all’interno di un prodotto) e gli amministratori di sistema (senza restrizioni). Consulta l’articolo Adobe Help Center su [ruoli amministrativi](https://helpx.adobe.com/enterprise/using/admin-roles.html) per ulteriori informazioni.

>[!NOTE]
>
>Da questo punto in poi, qualsiasi menzione di &quot;amministratore&quot; in questo documento si riferisce a un amministratore del profilo di prodotto o a una versione successiva (come descritto sopra).

Un flusso di lavoro di alto livello per ottenere e assegnare le autorizzazioni di accesso può essere riassunto come segue:

- Dopo aver concesso la licenza a Adobe Experience Platform o a un servizio applicazione/app che utilizza Experience Platform, viene inviata un&#39;e-mail all&#39;amministratore specificato durante la concessione delle licenze.
- L’amministratore accede a [Adobe Admin Console](#adobe-admin-console) e seleziona **Adobe Experience Platform** dall’elenco dei prodotti nella pagina della panoramica.
- L&#39;amministratore può visualizzare l&#39;impostazione predefinita [profili di prodotto](#product-profiles) oppure crea nuovi profili di prodotto del cliente in base alle esigenze.
- L’amministratore può modificare le autorizzazioni e gli utenti per tutti i profili di prodotto esistenti.
- Quando crei o modifichi un profilo di prodotto, l’amministratore aggiunge gli utenti al profilo utilizzando **[!UICONTROL utenti]** e concede le autorizzazioni a questi utenti (ad esempio &quot;[!UICONTROL Leggi set di dati]&quot; o &quot;[!UICONTROL Gestire gli schemi]&quot;) accedendo al **[!UICONTROL permissions]** scheda . Analogamente, l’amministratore può assegnare l’accesso alle sandbox utilizzando la stessa scheda delle autorizzazioni.
- Quando gli utenti accedono al [!DNL Experience Platform] interfaccia utente, loro accesso [!DNL Platform] Le funzionalità sono guidate dalle autorizzazioni concesse al passaggio 2. Ad esempio, se un utente non ha la &quot;[!UICONTROL Visualizzare i set di dati]&quot; autorizzazione, **[!UICONTROL Set di dati]** nel menu laterale non sarà visibile all’utente in questione.

Per passaggi più dettagliati su come gestire il controllo degli accessi in [!DNL Experience Platform], vedi [guida utente per il controllo degli accessi](./ui/overview.md).

Tutte le chiamate a [!DNL Experience Platform] Le API vengono convalidate per le autorizzazioni e restituiranno errori se le autorizzazioni appropriate non sono trovate nel contesto utente corrente. All’interno dell’interfaccia utente, gli elementi verranno nascosti o modificati a seconda delle autorizzazioni concesse all’utente corrente.

## Adobe Admin Console

Adobe Admin Console fornisce una posizione centrale per la gestione delle adesioni ai prodotti Adobe e l’accesso per la tua organizzazione. Attraverso la console è possibile concedere a gruppi di utenti autorizzazioni di accesso per vari [!DNL Platform] , ad esempio &quot;[!UICONTROL Gestire i set di dati]&quot;, &quot;[!UICONTROL Visualizzare i set di dati]&quot;, o &quot;[!UICONTROL Gestisci profili]&quot;.

### Profili di prodotto

In [!DNL Admin Console], le autorizzazioni vengono assegnate agli utenti tramite l’utilizzo di profili di prodotto. I profili di prodotto ti consentono di concedere le autorizzazioni a uno o più utenti e contengono anche il loro accesso all’ambito delle sandbox che sono loro assegnate tramite i profili di prodotto. Gli utenti possono essere assegnati a uno o più profili di prodotto appartenenti alla tua organizzazione.

### Profili di prodotto predefiniti

[!DNL Experience Platform] viene fornito con due profili di prodotto predefiniti preconfigurati. La tabella seguente illustra ciò che viene fornito in ciascun profilo predefinito, inclusa la sandbox a cui concedono l’accesso e le autorizzazioni concesse nell’ambito di tale sandbox.

| Profilo di prodotto | Accesso sandbox | Autorizzazioni |
| --- | --- | --- |
| Accesso completo alla produzione predefinita | Produzione | Tutte le autorizzazioni applicabili a [!DNL Experience Platform], ad eccezione delle autorizzazioni Amministrazione sandbox. |
| Amministratori sandbox | N/D | Fornisce l&#39;accesso solo alle autorizzazioni di amministrazione sandbox. |

## Sandbox e autorizzazioni

Le sandbox non di produzione sono una forma di virtualizzazione dei dati che consente di isolare i dati da altre sandbox e sono generalmente utilizzate per esperimenti di sviluppo, test o test. Le autorizzazioni di un profilo di prodotto consentono agli utenti del profilo di accedere a [!DNL Platform] funzioni all’interno degli ambienti sandbox a cui è stato concesso l’accesso. Una licenza di Experience Platform predefinita concede cinque sandbox (una produzione e quattro non di produzione). Puoi aggiungere pacchetti di dieci sandbox non di produzione fino a un massimo di 75 sandbox in totale. Per ulteriori informazioni, contatta l’amministratore della tua organizzazione o il rappresentante commerciale di Adobe.

Per ulteriori informazioni sulle sandbox in [!DNL Experience Platform], si prega di fare riferimento al [panoramica sulle sandbox](../sandboxes/home.md).

### Accesso alle sandbox

L’accesso alle sandbox viene gestito tramite i profili di prodotto. Per passaggi dettagliati su come abilitare l’accesso a una sandbox per un profilo di prodotto, consulta la [guida utente per il controllo degli accessi](./ui/overview.md).

È possibile concedere agli utenti l’accesso a una o più sandbox all’interno di un profilo di prodotto. Se un utente è incluso in due o più profili di prodotto, avrà accesso a tutte le sandbox incluse in tali profili.

L’autorizzazione &quot;Gestione sandbox&quot; consente agli utenti di gestire, visualizzare o reimpostare le sandbox.

### Autorizzazioni {#permissions}

La scheda Autorizzazioni all’interno di un profilo di prodotto visualizza le sandbox e le autorizzazioni attive per tale profilo:

![permissions-overview](./images/permissions.png)

Autorizzazioni concesse tramite [!DNL Admin Console] sono ordinati per categoria, con alcune autorizzazioni che consentono l’accesso a diverse funzionalità di basso livello.

La tabella seguente illustra le autorizzazioni disponibili per [!DNL Experience Platform] in [!DNL Admin Console], con la descrizione del [!DNL Platform] alle funzionalità a cui concedono l&#39;accesso. Per passaggi dettagliati su come aggiungere autorizzazioni a un profilo di prodotto, consulta la [guida utente per il controllo degli accessi](./ui/overview.md).

| Categoria | Autorizzazione | Descrizione |
| --- | --- | --- |
| [!DNL Alerts] | [!UICONTROL Visualizza cronologia avvisi] | Accesso in sola lettura per la cronologia degli avvisi. |
| [!DNL Alerts] | [!UICONTROL Risolvere gli avvisi] | Accesso alla lettura, alla modifica e all’eliminazione degli avvisi. |
| [!DNL Alerts] | [!UICONTROL Visualizzare gli avvisi] | Accesso in sola lettura per gli avvisi. |
| [!DNL Alerts] | [!UICONTROL Gestire gli avvisi] | Accesso alla cronologia degli avvisi in lettura, creazione, modifica ed eliminazione. |
| [!DNL Data Hygiene] | [!UICONTROL Visualizza igiene dati] | Accesso in sola lettura per l&#39;igiene dei dati. |
| [!DNL Data Hygiene] | [!UICONTROL Gestire l’igiene dei dati] | Accesso per leggere, creare, modificare ed eliminare l’igiene dei dati. |
| [!DNL Data Modeling] | [!UICONTROL Gestire gli schemi] | Accesso a strumenti per la lettura, la creazione, la modifica e l’eliminazione di schemi e risorse correlate. |
| [!DNL Data Modeling] | [!UICONTROL Visualizzare gli schemi] | Accesso in sola lettura agli schemi e alle risorse correlate. |
| [!DNL Data Modeling] | [!UICONTROL Gestire le relazioni] | Accedere alla funzione di lettura, creazione, modifica ed eliminazione delle relazioni tra schemi. |
| [!DNL Data Modeling] | [!UICONTROL Gestire i metadati delle identità] | Accesso a metadati di identità per gli schemi di lettura, creazione, modifica ed eliminazione. |
| [!DNL Data Management] | [!UICONTROL Gestire i set di dati] | Accesso a set di dati di lettura, creazione, modifica ed eliminazione. Accesso in sola lettura per gli schemi. |
| [!DNL Data Management] | [!UICONTROL Visualizzare i set di dati] | Accesso in sola lettura per set di dati e schemi. |
| [!DNL Data Management] | [!UICONTROL Monitoraggio dei dati] | Accesso in sola lettura ai set di dati e ai flussi di dati di monitoraggio. |
| [!DNL Profile Management] | [!UICONTROL Gestisci profili] | Accedere alla documentazione di lettura, creazione, modifica ed eliminazione dei set di dati utilizzati per i profili cliente. Accesso in sola lettura ai profili disponibili. |
| [!DNL Profile Management] | [!UICONTROL Visualizza profili] | Accesso in sola lettura ai profili disponibili. |
| [!DNL Profile Management] | [!UICONTROL Gestire segmenti] | Accesso ai segmenti di lettura, creazione, modifica ed eliminazione. |
| [!DNL Profile Management] | [!UICONTROL Visualizzare i segmenti] | Accesso in sola lettura ai segmenti disponibili. |
| [!DNL Profile Management] | [!UICONTROL Gestisci criteri di unione] | Accesso alla lettura, alla creazione, alla modifica e all&#39;eliminazione dei criteri di unione. |
| [!DNL Profile Management] | [!UICONTROL Visualizza criteri di unione] | Accesso in sola lettura ai criteri di unione disponibili. |
| [!DNL Profile Management] | [!UICONTROL Esportare il pubblico per il segmento] | Possibilità di esportare un segmento di pubblico valutato in un set di dati. |
| [!DNL Profile Management] | [!UICONTROL Valutare un segmento in un pubblico] | Possibilità di generare profili per un pubblico valutando una definizione di segmento. |
| [!DNL Identity Management] | [!UICONTROL Manage Identity Namespaces (Gestisci spazi dei nomi di identità)] | Accesso a spazi dei nomi delle identità di lettura, creazione, modifica ed eliminazione. |
| [!DNL Identity Management] | [!UICONTROL Visualizzare gli spazi dei nomi delle identità] | Accesso in sola lettura per i namespace di identità. |
| [!DNL Identity Management] | [!UICONTROL Visualizza grafico identità] | Accesso in sola lettura per i grafici di identità. |
| [!DNL Sandbox Administration] | [!UICONTROL Gestire le sandbox] | Accesso alla lettura, alla creazione, alla modifica e all’eliminazione delle sandbox. |
| [!DNL Sandbox Administration] | [!UICONTROL View Sandboxes (Visualizza sandbox)] | Accesso in sola lettura per le sandbox appartenenti all’organizzazione. |
| [!DNL Sandbox Administration] | [!UICONTROL Reimpostare una sandbox] | Possibilità di reimpostare una sandbox. |
| [!DNL Destinations] | [!UICONTROL Gestire le destinazioni] | Accesso per leggere, creare ed eliminare i flussi di attivazione di destinazione e gli account di destinazione. |
| [!DNL Destinations] | [!UICONTROL Visualizzare le destinazioni] | Accesso in sola lettura alle destinazioni disponibili nel **[!UICONTROL Catalogo]** le destinazioni autenticate nel **[!UICONTROL Sfoglia]** scheda . |
| [!DNL Destinations] | [!UICONTROL Attivare le destinazioni] | Consente agli utenti di attivare segmenti su destinazioni esistenti. Abilita il passaggio di mappatura nel flusso di lavoro di attivazione. Questa autorizzazione richiede [!UICONTROL Visualizzare le destinazioni] o [!UICONTROL Gestire le destinazioni] da concedere all’utente che attiverà i dati nelle destinazioni. |
| [!DNL Destinations] | [!UICONTROL Attiva segmento senza mappatura] | Consente agli utenti di attivare segmenti su destinazioni esistenti, senza visualizzare il [fase di mappatura](../destinations/ui/activate-batch-profile-destinations.md#mapping). Gli utenti possono aggiungere e rimuovere segmenti nei flussi di lavoro di attivazione, ma non possono aggiungere o rimuovere attributi o identità mappati. Questa autorizzazione richiede [!UICONTROL Attivare le destinazioni] autorizzazione da concedere all’utente che attiverà i dati nelle destinazioni. |
| [!DNL Destinations] | [!UICONTROL Gestire e attivare le destinazioni del set di dati] | Possibilità di leggere, creare, modificare e disabilitare i flussi di esportazione dei set di dati. Possibilità di attivare anche i dati ai set di dati attivi creati. |
| [!DNL Destinations] | [!UICONTROL Authoring delle destinazioni] | Possibilità di creare destinazioni utilizzando [Adobe Experience Platform Destination SDK](../destinations/destination-sdk/overview.md). |
| [!DNL Data Ingestion] | [!UICONTROL Gestisci origini] | Accesso a fonti di lettura, creazione, modifica e disattivazione. |
| [!DNL Data Ingestion] | [!UICONTROL Visualizza origini] | Accesso in sola lettura alle origini disponibili nel **[!UICONTROL Catalogo]** e le origini autenticate nel **[!UICONTROL Sfoglia]** scheda . |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | Accesso ai handshakes per creare, accettare e rifiutare i partner per collegare due organizzazioni e consentire [!DNL Segment Match] flussi. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share] | Accesso a lettura, creazione, modifica e pubblicazione [!DNL Segment Match] feed con partner attivi. |
| [!DNL Data Science Workspace] | [!UICONTROL Gestione di Data Science Workspace] | Accesso a lettura, creazione, modifica ed eliminazione di [!DNL Data Science Workspace]. |
| Governance dei dati | [!UICONTROL Applicare le etichette di utilizzo dei dati] | Accesso per leggere, creare ed eliminare le etichette di utilizzo. |
| Governance dei dati | [!UICONTROL Gestire i criteri di utilizzo dei dati] | Accesso a criteri di utilizzo dei dati di lettura, creazione, modifica ed eliminazione. |
| Governance dei dati | [!UICONTROL Visualizzare i criteri di utilizzo dei dati] | Accesso in sola lettura per i criteri di utilizzo dei dati appartenenti all’organizzazione. |
| Governance dei dati | [!UICONTROL Visualizza registro attività utente] | Accesso in sola lettura alla visualizzazione registrata [registri di controllo](../landing/governance-privacy-security/audit-logs/overview.md) delle attività di Platform. |
| [!DNL Dashboards] | [!UICONTROL Visualizza dashboard di utilizzo della licenza] | Accesso in sola lettura per visualizzare il dashboard di utilizzo della licenza. |
| [!DNL Dashboards] | [!UICONTROL Gestire dashboard standard] | Aggiungi attributi personalizzati non ancora presenti nel data warehouse. |
| [!DNL Query Service] | [!UICONTROL Gestire le query] | Accesso alla lettura, alla creazione, alla modifica e all&#39;eliminazione di query SQL strutturate per i dati di Platform. |
| [!DNL Query Service] | [!UICONTROL Gestisci integrazione servizio query] | Accesso per creare, aggiornare ed eliminare le credenziali non in scadenza per l’accesso al servizio query. |

## Passaggi successivi

Leggendo questa guida, ti sono stati introdotti i principi fondamentali del controllo degli accessi in [!DNL Experience Platform]. Ora puoi continuare con la [guida utente per il controllo degli accessi](./ui/overview.md) per i passaggi dettagliati su come utilizzare [!DNL Admin Console] per creare profili di prodotto e assegnare autorizzazioni per [!DNL Platform].
