---
keywords: Experience Platform;home;popular topics;access control;adobe admin console
solution: Experience Platform
topic: overview
title: Panoramica sul controllo degli accessi
description: Il controllo degli accessi per Adobe Experience Platform è fornito tramite Adobe Admin Console. Questa funzionalità sfrutta i profili di prodotto in  Admin Console, che collegano gli utenti con autorizzazioni e sandbox.
translation-type: tm+mt
source-git-commit: ccb7286e47aa4cf6356d22f84111b0c0fb30dfa8
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 2%

---


# Panoramica sul controllo degli accessi

Il controllo di accesso per [!DNL Experience Platform] è fornito tramite [Adobe Admin Console](https://adminconsole.adobe.com). Questa funzionalità sfrutta i profili di prodotto in [!DNL Admin Console], che collegano gli utenti con autorizzazioni e sandbox.

## Gerarchia e flusso di lavoro del controllo degli accessi

Per configurare il controllo di accesso per [!DNL Experience Platform], è necessario disporre dei privilegi di amministratore per un&#39;organizzazione che dispone di un&#39;integrazione con un [!DNL Experience Platform] prodotto. Il ruolo minimo che concede o revoca le autorizzazioni è un amministratore del profilo di prodotto. Altri ruoli di amministratore che possono gestire le autorizzazioni sono gli amministratori dei prodotti (che possono gestire tutti i profili all&#39;interno di un prodotto) e gli amministratori di sistema (senza restrizioni). Per ulteriori informazioni, consultate l&#39;articolo Adobe Help Center sui ruoli [](https://helpx.adobe.com/enterprise/using/admin-roles.html) amministrativi.

>[!NOTE]
>
>Da questo punto in poi, qualsiasi menzione di &quot;amministratore&quot; in questo documento fa riferimento a un amministratore del profilo di prodotto o a una versione successiva (come indicato sopra).

Un flusso di lavoro di alto livello per ottenere e assegnare le autorizzazioni di accesso può essere riassunto come segue:

- Dopo aver concesso la licenza ad Adobe Experience Platform o a un servizio applicazione/app che utilizza  Experience Platform, viene inviato un messaggio e-mail all&#39;amministratore specificato durante la licenza.
- L’amministratore accede ad [Adobe Admin Console](#adobe-admin-console) e seleziona **Adobe Experience Platform** dall’elenco dei prodotti nella pagina della panoramica.
- L&#39;amministratore può visualizzare i profili [di](#product-profiles) prodotto predefiniti o creare nuovi profili di prodotto cliente, a seconda delle necessità.
- L&#39;amministratore può modificare le autorizzazioni e gli utenti per qualsiasi profilo di prodotto esistente.
- Durante la creazione o la modifica di un profilo di prodotto, l&#39;amministratore aggiunge gli utenti al profilo utilizzando la **[!UICONTROL users]** scheda e concede le autorizzazioni a tali utenti (come &quot;[!UICONTROL Read Datasets]&quot; o &quot;[!UICONTROL Manage Schemas]&quot;) accedendo alla **[!UICONTROL permissions]** scheda. Analogamente, l&#39;amministratore può assegnare l&#39;accesso alle sandbox utilizzando la stessa scheda delle autorizzazioni.
- Quando gli utenti accedono all&#39;interfaccia [!DNL Experience Platform] utente, il loro accesso alle [!DNL Platform] funzionalità è determinato dalle autorizzazioni concesse loro dal Passaggio 2. Ad esempio, se un utente non dispone dell&#39;autorizzazione &quot;[!UICONTROL View Datasets]&quot;, la **[!UICONTROL Datasets]** scheda nel menu laterale non sarà visibile all&#39;utente.

Per ulteriori dettagli su come gestire il controllo degli accessi in [!DNL Experience Platform], consultate la guida [utente per il controllo degli](./ui/overview.md)accessi.

Tutte le chiamate alle [!DNL Experience Platform] API vengono convalidate per le autorizzazioni e restituiranno errori se le autorizzazioni appropriate non vengono trovate nel contesto utente corrente. Nell’interfaccia utente, gli elementi verranno nascosti o modificati in base alle autorizzazioni concesse all’utente corrente.

## Adobe Admin Console

Adobe Admin Console fornisce una posizione centrale per la gestione delle adesioni  prodotto Adobe e l&#39;accesso per la vostra organizzazione. Tramite la console potete concedere a gruppi di utenti autorizzazioni di accesso per varie [!DNL Platform] funzionalità, ad esempio &quot;[!UICONTROL Manage Datasets]&quot;, &quot;[!UICONTROL View Datasets]&quot; o &quot;[!UICONTROL Manage Profiles]&quot;.

### Profili di prodotto

Nel pannello [!DNL Admin Console], le autorizzazioni vengono assegnate agli utenti tramite l&#39;uso di profili di prodotto. I profili di prodotto consentono di concedere le autorizzazioni a uno o più utenti e contengono anche il loro accesso all&#39;ambito delle sandbox che sono loro assegnate tramite i profili di prodotto. Gli utenti possono essere assegnati a uno o più profili di prodotto appartenenti alla tua organizzazione.

### Profili di prodotto predefiniti

[!DNL Experience Platform] viene fornito con due profili di prodotto predefiniti preconfigurati. La tabella seguente riassume i dati forniti in ciascun profilo predefinito, inclusa la sandbox a cui concedono l&#39;accesso, nonché le autorizzazioni concesse all&#39;interno dell&#39;ambito di tale sandbox.

| Profilo di prodotto | Accesso sandbox | Autorizzazioni |
| --- | --- | --- |
| Produzione predefinita - Accesso completo | Produzione | Tutte le autorizzazioni applicabili a [!DNL Experience Platform], tranne quelle per l&#39;amministrazione sandbox. |
| Amministrazione sandbox predefinita | N/D | Fornisce l&#39;accesso solo alle autorizzazioni Amministrazione sandbox. |

## Sandbox e autorizzazioni

Le sandbox non di produzione sono una forma di virtualizzazione dei dati che consente di isolare i dati da altre sandbox e sono generalmente utilizzate per esperimenti di sviluppo, test o test. Le autorizzazioni del profilo di prodotto consentono agli utenti del profilo di accedere alle [!DNL Platform] funzionalità all&#39;interno degli ambienti sandbox a cui gli è stato concesso l&#39;accesso. Una licenza di Experience Platform  predefinita concede cinque sandbox (una produzione e quattro non di produzione). Potete aggiungere pacchetti di dieci sandbox non di produzione fino a un massimo di 75 sandbox in totale. Per maggiori informazioni, contattate l&#39;amministratore dell&#39;organizzazione IMS o il rappresentante commerciale  Adobe.

Per ulteriori informazioni sulle sandbox in [!DNL Experience Platform], consultate la panoramica sulle [sandbox](../sandboxes/home.md).

### Accesso alle sandbox

L&#39;accesso alle sandbox viene gestito tramite i profili di prodotto. Per istruzioni dettagliate su come abilitare l&#39;accesso a una sandbox per un profilo di prodotto, consultate la guida [utente per il controllo](./ui/overview.md)degli accessi.

Agli utenti può essere concesso l&#39;accesso a una o più sandbox all&#39;interno di un profilo di prodotto. Se un utente è incluso in due o più profili di prodotto, avrà accesso a tutte le sandbox incluse in tali profili.

L&#39;autorizzazione &quot;Gestione sandbox&quot; consente agli utenti di gestire, visualizzare o ripristinare le sandbox.

### Autorizzazioni

La scheda Autorizzazioni all&#39;interno di un profilo di prodotto visualizza le sandbox e le autorizzazioni attive per tale profilo:

![permissions-overview](./images/permissions-overview.png)

Le autorizzazioni concesse tramite l&#39; [!DNL Admin Console] opzione sono ordinate per categoria, con alcune autorizzazioni che concedono l&#39;accesso a diverse funzionalità di basso livello.

La tabella seguente delinea le autorizzazioni disponibili per [!DNL Experience Platform] in [!DNL Admin Console], con una descrizione delle [!DNL Platform] funzionalità specifiche a cui concedono l&#39;accesso. Per i passaggi dettagliati su come aggiungere le autorizzazioni a un profilo di prodotto, consulta la guida [utente per il controllo](./ui/overview.md)degli accessi.

| Categoria | Autorizzazione | Descrizione |
| --- | --- | --- |
| [!DNL Data Modeling] | [!UICONTROL Manage Schemas] | Accesso per leggere, creare, modificare ed eliminare schemi e risorse correlate. |
| [!DNL Data Modeling] | [!UICONTROL View Schemas] | Accesso in sola lettura agli schemi e alle risorse correlate. |
| [!DNL Data Modeling] | [!UICONTROL Manage Relationships] | Accesso per leggere, creare, modificare ed eliminare le relazioni tra schemi. |
| [!DNL Data Modeling] | [!UICONTROL Manage Identity Metadata] | Accesso per leggere, creare, modificare ed eliminare i metadati di identità per gli schemi. |
| [!DNL Data Management] | [!UICONTROL Manage Datasets] | Accesso per la lettura, la creazione, la modifica e l&#39;eliminazione dei set di dati. Accesso in sola lettura per gli schemi. |
| [!DNL Data Management] | [!UICONTROL View Datasets] | Accesso in sola lettura per set di dati e schemi. |
| [!DNL Data Management] | [!UICONTROL Data Monitoring] | Accesso in sola lettura ai set di dati e ai flussi di monitoraggio. |
| [!DNL Profile Management] | [!UICONTROL Manage Profiles] | Accesso per leggere, creare, modificare ed eliminare i set di dati utilizzati per i profili cliente. Accesso in sola lettura ai profili disponibili. |
| [!DNL Profile Management] | [!UICONTROL View Profiles] | Accesso in sola lettura ai profili disponibili. |
| [!DNL Profile Management] | [!UICONTROL Manage Segments] | Accesso ai segmenti di lettura, creazione, modifica ed eliminazione. |
| [!DNL Profile Management] | [!UICONTROL View Segments] | Accesso in sola lettura ai segmenti disponibili. |
| [!DNL Profile Management] | [!UICONTROL Manage Merge Policies] | Accesso per la lettura, la creazione, la modifica e l&#39;eliminazione dei criteri di unione. |
| [!DNL Profile Management] | [!UICONTROL View Merge Policies] | Accesso in sola lettura ai criteri di unione disponibili. |
| [!DNL Profile Management] | [!UICONTROL Export Audience for Segment] | Possibilità di esportare un segmento di pubblico valutato in un dataset. |
| [!DNL Profile Management] | [!UICONTROL Evaluate a Segment to an Audience] | Possibilità di generare profili per un&#39;audience valutando la definizione di un segmento. |
| [!DNL Identities] | [!UICONTROL Manage Identity Namespaces] | Accesso agli spazi dei nomi delle identità di lettura, creazione, modifica ed eliminazione. |
| [!DNL Identities] | [!UICONTROL View Identity Namespaces] | Accesso in sola lettura per gli spazi dei nomi di identità. |
| [!DNL Sandbox Administration] | [!UICONTROL Manage Sandboxes] | Accesso alle sandbox di lettura, creazione, modifica ed eliminazione. |
| [!DNL Sandbox Administration] | [!UICONTROL View Sandboxes] | Accesso in sola lettura per le sandbox appartenenti alla vostra organizzazione. |
| [!DNL Sandbox Administration] | [!UICONTROL Reset a Sandbox] | Possibilità di ripristinare una sandbox. |
| [!DNL Destinations] | [!UICONTROL Manage Destinations] | Accesso alle destinazioni di lettura, creazione, modifica e disattivazione.* |
| [!DNL Destinations] | [!UICONTROL View Destinations] | Accesso in sola lettura alle destinazioni disponibili nella **[!UICONTROL Catalog]** scheda e alle destinazioni autenticate nella **[!UICONTROL Browse]** scheda.* |
| [!DNL Destinations] | [!UICONTROL Activate Destinations] | Possibilità di attivare i dati nelle destinazioni attive create. Questa autorizzazione richiede che &quot;Visualizza destinazioni&quot; o &quot;Gestisci [!UICONTROL Destinations”] venga concesso all&#39;utente che attiverà le destinazioni.* |
| [!DNL Data Ingestion] | [!UICONTROL Manage Sources] | Accesso alle origini di lettura, creazione, modifica e disattivazione. |
| [!DNL Data Ingestion] | [!UICONTROL View Sources] | Accesso in sola lettura alle origini disponibili nella **[!UICONTROL Catalog]** scheda e alle origini autenticate nella **[!UICONTROL Browse]** scheda. |
| [!DNL Data Science Workspace] | [!UICONTROL Manage Data Science Workspace] | Accesso a lettura, creazione, modifica ed eliminazione in [!DNL Data Science Workspace]. |
| [!DNL Data Governance] | [!UICONTROL Apply Data Usage Labels] | Accesso per la lettura, la creazione e l&#39;eliminazione delle etichette di utilizzo. |
| [!DNL Data Governance] | [!UICONTROL Manage Data Usage Policies] | Accesso a criteri di utilizzo dei dati di lettura, creazione, modifica ed eliminazione. |
| [!DNL Data Governance] | [!UICONTROL View Data Usage Policies] | Accesso in sola lettura per i criteri di utilizzo dei dati appartenenti alla tua organizzazione. |
| [!DNL Query Service] | [!UICONTROL Manage Queries] | Accesso per leggere, creare, modificare ed eliminare query SQL strutturate per i dati della piattaforma. |

_(*) Questa autorizzazione richiede disposizioni per [!DNL Real-time Customer Data Platform]. Per ulteriori informazioni sulla CDP in tempo reale, consultare la panoramica [CDP in tempo](https://docs.adobe.com/content/help/it-IT/experience-platform/rtcdp/overview.html)reale._

## Passaggi successivi

Leggendo questa guida, sono stati introdotti i principi principali del controllo degli accessi in [!DNL Experience Platform]. È ora possibile continuare a seguire la guida [utente per il controllo](./ui/overview.md) degli accessi per i passaggi dettagliati su come utilizzare l&#39;app per [!DNL Admin Console] creare profili di prodotto e assegnare le autorizzazioni per [!DNL Platform].