---
keywords: Experience Platform;home;argomenti popolari;controllo accessi;adobe admin console
solution: Experience Platform
topic-legacy: overview
title: Panoramica sul controllo degli accessi
description: Il controllo degli accessi per Adobe Experience Platform è fornito tramite Adobe Admin Console. Questa funzionalità sfrutta i profili di prodotto in Admin Console, che collegano gli utenti con autorizzazioni e sandbox.
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: 13055c9b569a67b5b44a90ac2b40776e271db008
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 2%

---

# Panoramica sul controllo degli accessi

Il controllo degli accessi per [!DNL Experience Platform] è fornito tramite [Adobe Admin Console](https://adminconsole.adobe.com). Questa funzionalità sfrutta i profili di prodotto in [!DNL Admin Console], che collegano gli utenti con autorizzazioni e sandbox.

## Accedere alla gerarchia di controllo e al flusso di lavoro

Per configurare il controllo di accesso per [!DNL Experience Platform], è necessario disporre dei privilegi di amministratore per un&#39;organizzazione con un&#39;integrazione di prodotto [!DNL Experience Platform]. Il ruolo minimo che concede o revoca le autorizzazioni è un amministratore del profilo di prodotto. Altri ruoli di amministratore che possono gestire le autorizzazioni sono gli amministratori di prodotto (possono gestire tutti i profili all’interno di un prodotto) e gli amministratori di sistema (senza restrizioni). Per ulteriori informazioni, consulta l’articolo Adobe Help Center sui [ruoli amministrativi](https://helpx.adobe.com/enterprise/using/admin-roles.html) .

>[!NOTE]
>
>Da questo punto in poi, qualsiasi menzione di &quot;amministratore&quot; in questo documento si riferisce a un amministratore del profilo di prodotto o a una versione successiva (come descritto sopra).

Un flusso di lavoro di alto livello per ottenere e assegnare le autorizzazioni di accesso può essere riassunto come segue:

- Dopo aver concesso la licenza a Adobe Experience Platform o a un servizio applicazione/app che utilizza Experience Platform, viene inviata un&#39;e-mail all&#39;amministratore specificato durante la concessione delle licenze.
- L&#39;amministratore accede a [Adobe Admin Console](#adobe-admin-console) e seleziona **Adobe Experience Platform** dall&#39;elenco dei prodotti nella pagina della panoramica.
- L’amministratore può visualizzare i profili di prodotto [predefiniti](#product-profiles) o creare nuovi profili di prodotto del cliente in base alle esigenze.
- L’amministratore può modificare le autorizzazioni e gli utenti per tutti i profili di prodotto esistenti.
- Quando crei o modifichi un profilo di prodotto, l&#39;amministratore aggiunge utenti al profilo utilizzando la scheda **[!UICONTROL utenti]** e concede le autorizzazioni a tali utenti (ad esempio &quot;[!UICONTROL Leggi set di dati]&quot; o &quot;[!UICONTROL Gestisci schemi]&quot;) accedendo alla scheda **[!UICONTROL autorizzazioni]**. Analogamente, l’amministratore può assegnare l’accesso alle sandbox utilizzando la stessa scheda delle autorizzazioni.
- Quando gli utenti accedono all&#39;interfaccia utente [!DNL Experience Platform], l&#39;accesso alle funzionalità [!DNL Platform] dipende dalle autorizzazioni concesse loro dal passaggio 2. Ad esempio, se un utente non dispone dell&#39;autorizzazione &quot;[!UICONTROL Visualizza set di dati]&quot;, la scheda **[!UICONTROL Set di dati]** nel menu laterale non sarà visibile all&#39;utente.

Per passaggi più dettagliati su come gestire il controllo degli accessi in [!DNL Experience Platform], consulta la [guida utente per il controllo degli accessi](./ui/overview.md).

Tutte le chiamate alle API [!DNL Experience Platform] vengono convalidate per le autorizzazioni e restituiranno errori se le autorizzazioni appropriate non sono trovate nel contesto utente corrente. All’interno dell’interfaccia utente, gli elementi verranno nascosti o modificati a seconda delle autorizzazioni concesse all’utente corrente.

## Adobe Admin Console

Adobe Admin Console fornisce una posizione centrale per la gestione delle adesioni ai prodotti Adobe e l’accesso per la tua organizzazione. Tramite la console è possibile concedere a gruppi di utenti autorizzazioni di accesso per varie funzionalità [!DNL Platform], ad esempio &quot;[!UICONTROL Gestisci set di dati]&quot;, &quot;[!UICONTROL Visualizza set di dati]&quot; o &quot;[!UICONTROL Gestisci profili]&quot;.

### Profili di prodotto

In [!DNL Admin Console], le autorizzazioni vengono assegnate agli utenti tramite l’utilizzo di profili di prodotto. I profili di prodotto ti consentono di concedere le autorizzazioni a uno o più utenti e contengono anche il loro accesso all’ambito delle sandbox che sono loro assegnate tramite i profili di prodotto. Gli utenti possono essere assegnati a uno o più profili di prodotto appartenenti alla tua organizzazione.

### Profili di prodotto predefiniti

[!DNL Experience Platform] viene fornito con due profili di prodotto predefiniti preconfigurati. La tabella seguente illustra ciò che viene fornito in ciascun profilo predefinito, inclusa la sandbox a cui concedono l’accesso e le autorizzazioni concesse nell’ambito di tale sandbox.

| Profilo di prodotto | Accesso sandbox | Autorizzazioni |
| --- | --- | --- |
| Accesso completo alla produzione predefinita | Produzione | Tutte le autorizzazioni applicabili a [!DNL Experience Platform], ad eccezione delle autorizzazioni di amministrazione sandbox. |
| Amministratori sandbox | N/D | Fornisce l&#39;accesso solo alle autorizzazioni di amministrazione sandbox. |

## Sandbox e autorizzazioni

Le sandbox non di produzione sono una forma di virtualizzazione dei dati che consente di isolare i dati da altre sandbox e sono generalmente utilizzate per esperimenti di sviluppo, test o test. Le autorizzazioni di un profilo di prodotto consentono agli utenti del profilo di accedere alle funzioni [!DNL Platform] all’interno degli ambienti sandbox a cui sono stati concessi l’accesso. Una licenza di Experience Platform predefinita concede cinque sandbox (una produzione e quattro non di produzione). Puoi aggiungere pacchetti di dieci sandbox non di produzione fino a un massimo di 75 sandbox in totale. Per ulteriori informazioni, contatta l’amministratore dell’organizzazione IMS o il rappresentante commerciale di Adobe.

Per ulteriori informazioni sulle sandbox in [!DNL Experience Platform], consulta la [panoramica sulle sandbox](../sandboxes/home.md).

### Accesso alle sandbox

L’accesso alle sandbox viene gestito tramite i profili di prodotto. Per passaggi dettagliati su come abilitare l’accesso a una sandbox per un profilo di prodotto, consulta la [guida utente per il controllo degli accessi](./ui/overview.md).

È possibile concedere agli utenti l’accesso a una o più sandbox all’interno di un profilo di prodotto. Se un utente è incluso in due o più profili di prodotto, avrà accesso a tutte le sandbox incluse in tali profili.

L’autorizzazione &quot;Gestione sandbox&quot; consente agli utenti di gestire, visualizzare o reimpostare le sandbox.

### Autorizzazioni

La scheda Autorizzazioni all’interno di un profilo di prodotto visualizza le sandbox e le autorizzazioni attive per tale profilo:

![permissions-overview](./images/permissions-overview.png)

Le autorizzazioni concesse tramite [!DNL Admin Console] sono ordinate per categoria, con alcune autorizzazioni che consentono l&#39;accesso a diverse funzionalità di basso livello.

La tabella seguente illustra le autorizzazioni disponibili per [!DNL Experience Platform] in [!DNL Admin Console], con descrizioni delle funzionalità [!DNL Platform] specifiche a cui concedono l&#39;accesso. Per passaggi dettagliati su come aggiungere autorizzazioni a un profilo di prodotto, consulta la [guida utente per il controllo degli accessi](./ui/overview.md).

| Categoria | Autorizzazione | Descrizione |
| --- | --- | --- |
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
| [!DNL Identities] | [!UICONTROL Manage Identity Namespaces (Gestisci spazi dei nomi di identità)] | Accesso a spazi dei nomi delle identità di lettura, creazione, modifica ed eliminazione. |
| [!DNL Identities] | [!UICONTROL Visualizzare gli spazi dei nomi delle identità] | Accesso in sola lettura per i namespace di identità. |
| [!DNL Sandbox Administration] | [!UICONTROL Gestire le sandbox] | Accesso alla lettura, alla creazione, alla modifica e all’eliminazione delle sandbox. |
| [!DNL Sandbox Administration] | [!UICONTROL View Sandboxes (Visualizza sandbox)] | Accesso in sola lettura per le sandbox appartenenti all’organizzazione. |
| [!DNL Sandbox Administration] | [!UICONTROL Reimpostare una sandbox] | Possibilità di reimpostare una sandbox. |
| [!DNL Destinations] | [!UICONTROL Gestire le destinazioni] | Accesso a destinazioni in lettura, creazione, modifica e disattivazione. |
| [!DNL Destinations] | [!UICONTROL Visualizzare le destinazioni] | Accesso in sola lettura alle destinazioni disponibili nella scheda **[!UICONTROL Catalogo]** e alle destinazioni autenticate nella scheda **[!UICONTROL Sfoglia]**. |
| [!DNL Destinations] | [!UICONTROL Attivare le destinazioni] | Possibilità di attivare i dati nelle destinazioni attive create. Questa autorizzazione richiede che &quot;Visualizza destinazioni&quot; o &quot;Gestisci [!UICONTROL destinazioni&quot;] sia concessa all&#39;utente che attiverà le destinazioni. |
| [!DNL Destinations] | [!UICONTROL Authoring delle destinazioni] | Possibilità di creare destinazioni utilizzando [Adobe Experience Platform Destination SDK](../destinations/destination-sdk/overview.md). |
| [!DNL Data Ingestion] | [!UICONTROL Gestisci origini] | Accesso a fonti di lettura, creazione, modifica e disattivazione. |
| [!DNL Data Ingestion] | [!UICONTROL Visualizza origini] | Accesso in sola lettura alle origini disponibili nella scheda **[!UICONTROL Catalogo]** e alle origini autenticate nella scheda **[!UICONTROL Sfoglia]**. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | Accesso per creare, accettare e rifiutare handshake partner per collegare due organizzazioni IMS e abilitare i flussi [!DNL Segment Match]. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share] | Accesso a feed [!DNL Segment Match] in lettura, creazione, modifica e pubblicazione con partner attivi. |
| [!DNL Data Science Workspace] | [!UICONTROL Gestione di Data Science Workspace] | Accesso a lettura, creazione, modifica ed eliminazione in [!DNL Data Science Workspace]. |
| [!DNL Data Governance] | [!UICONTROL Applicare le etichette di utilizzo dei dati] | Accesso per leggere, creare ed eliminare le etichette di utilizzo. |
| [!DNL Data Governance] | [!UICONTROL Gestire i criteri di utilizzo dei dati] | Accesso a criteri di utilizzo dei dati di lettura, creazione, modifica ed eliminazione. |
| [!DNL Data Governance] | [!UICONTROL Visualizzare i criteri di utilizzo dei dati] | Accesso in sola lettura per i criteri di utilizzo dei dati appartenenti all’organizzazione. |
| [!DNL Data Governance] | [!UICONTROL Visualizza log di controllo] | Accesso in sola lettura per visualizzare i [registri di controllo ](../landing/governance-privacy-security/audit-logs/overview.md) registrati delle attività di Platform. |
| [!DNL Dashboards] | [!UICONTROL Visualizza dashboard di utilizzo della licenza] | Accesso in sola lettura per visualizzare il dashboard di utilizzo della licenza. |
| [!DNL Dashboards] | [!UICONTROL Gestire dashboard standard] | Aggiungi attributi personalizzati non ancora presenti nel data warehouse. |
| [!DNL Query Service] | [!UICONTROL Gestire le query] | Accesso alla lettura, alla creazione, alla modifica e all&#39;eliminazione di query SQL strutturate per i dati di Platform. |
| [!DNL Query Service] | [!UICONTROL Gestisci integrazione servizio query] | Accesso per creare, aggiornare ed eliminare le credenziali non in scadenza per l’accesso al servizio query. |

## Passaggi successivi

Leggendo questa guida, ti sono stati introdotti i principi principali del controllo degli accessi in [!DNL Experience Platform]. È ora possibile continuare la [guida utente per il controllo degli accessi](./ui/overview.md) per passaggi dettagliati su come utilizzare [!DNL Admin Console] per creare profili di prodotto e assegnare autorizzazioni per [!DNL Platform].
