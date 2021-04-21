---
keywords: Experience Platform;home;argomenti popolari;controllo accessi;adobe admin console
solution: Experience Platform
topic-legacy: overview
title: Panoramica sul controllo degli accessi
description: Il controllo degli accessi per Adobe Experience Platform è fornito tramite Adobe Admin Console. Questa funzionalità sfrutta i profili di prodotto in Admin Console, che collegano gli utenti con autorizzazioni e sandbox.
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1181'
ht-degree: 1%

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
- Quando crei o modifichi un profilo di prodotto, l’amministratore aggiunge utenti al profilo utilizzando la scheda **[!UICONTROL users]** e concede le autorizzazioni a tali utenti (ad esempio &quot;[!UICONTROL Read Datasets]&quot; o &quot;[!UICONTROL Manage Schemas]&quot;) accedendo alla scheda **[!UICONTROL permissions]**. Analogamente, l’amministratore può assegnare l’accesso alle sandbox utilizzando la stessa scheda delle autorizzazioni.
- Quando gli utenti accedono all&#39;interfaccia utente [!DNL Experience Platform], l&#39;accesso alle funzionalità [!DNL Platform] dipende dalle autorizzazioni concesse loro dal passaggio 2. Ad esempio, se un utente non dispone dell&#39;autorizzazione &quot;[!UICONTROL View Datasets]&quot;, la scheda **[!UICONTROL Datasets]** nel menu laterale non sarà visibile all&#39;utente.

Per passaggi più dettagliati su come gestire il controllo degli accessi in [!DNL Experience Platform], consulta la [guida utente per il controllo degli accessi](./ui/overview.md).

Tutte le chiamate alle API [!DNL Experience Platform] vengono convalidate per le autorizzazioni e restituiranno errori se le autorizzazioni appropriate non sono trovate nel contesto utente corrente. All’interno dell’interfaccia utente, gli elementi verranno nascosti o modificati a seconda delle autorizzazioni concesse all’utente corrente.

## Adobe Admin Console

Adobe Admin Console fornisce una posizione centrale per la gestione delle adesioni ai prodotti Adobe e l’accesso per la tua organizzazione. Tramite la console è possibile concedere a gruppi di utenti autorizzazioni di accesso per varie funzionalità [!DNL Platform], come &quot;[!UICONTROL Manage Datasets]&quot;, &quot;[!UICONTROL View Datasets]&quot; o &quot;[!UICONTROL Manage Profiles]&quot;.

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
| [!DNL Data Modeling] | [!UICONTROL Manage Schemas] | Accesso a strumenti per la lettura, la creazione, la modifica e l’eliminazione di schemi e risorse correlate. |
| [!DNL Data Modeling] | [!UICONTROL View Schemas] | Accesso in sola lettura agli schemi e alle risorse correlate. |
| [!DNL Data Modeling] | [!UICONTROL Manage Relationships] | Accedere alla funzione di lettura, creazione, modifica ed eliminazione delle relazioni tra schemi. |
| [!DNL Data Modeling] | [!UICONTROL Manage Identity Metadata] | Accesso a metadati di identità per gli schemi di lettura, creazione, modifica ed eliminazione. |
| [!DNL Data Management] | [!UICONTROL Manage Datasets] | Accesso a set di dati di lettura, creazione, modifica ed eliminazione. Accesso in sola lettura per gli schemi. |
| [!DNL Data Management] | [!UICONTROL View Datasets] | Accesso in sola lettura per set di dati e schemi. |
| [!DNL Data Management] | [!UICONTROL Data Monitoring] | Accesso in sola lettura ai set di dati e ai flussi di dati di monitoraggio. |
| [!DNL Profile Management] | [!UICONTROL Manage Profiles] | Accedere alla documentazione di lettura, creazione, modifica ed eliminazione dei set di dati utilizzati per i profili cliente. Accesso in sola lettura ai profili disponibili. |
| [!DNL Profile Management] | [!UICONTROL View Profiles] | Accesso in sola lettura ai profili disponibili. |
| [!DNL Profile Management] | [!UICONTROL Manage Segments] | Accesso ai segmenti di lettura, creazione, modifica ed eliminazione. |
| [!DNL Profile Management] | [!UICONTROL View Segments] | Accesso in sola lettura ai segmenti disponibili. |
| [!DNL Profile Management] | [!UICONTROL Manage Merge Policies] | Accesso alla lettura, alla creazione, alla modifica e all&#39;eliminazione dei criteri di unione. |
| [!DNL Profile Management] | [!UICONTROL View Merge Policies] | Accesso in sola lettura ai criteri di unione disponibili. |
| [!DNL Profile Management] | [!UICONTROL Export Audience for Segment] | Possibilità di esportare un segmento di pubblico valutato in un set di dati. |
| [!DNL Profile Management] | [!UICONTROL Evaluate a Segment to an Audience] | Possibilità di generare profili per un pubblico valutando una definizione di segmento. |
| [!DNL Identities] | [!UICONTROL Manage Identity Namespaces] | Accesso a spazi dei nomi delle identità di lettura, creazione, modifica ed eliminazione. |
| [!DNL Identities] | [!UICONTROL View Identity Namespaces] | Accesso in sola lettura per i namespace di identità. |
| [!DNL Sandbox Administration] | [!UICONTROL Manage Sandboxes] | Accesso alla lettura, alla creazione, alla modifica e all’eliminazione delle sandbox. |
| [!DNL Sandbox Administration] | [!UICONTROL View Sandboxes] | Accesso in sola lettura per le sandbox appartenenti all’organizzazione. |
| [!DNL Sandbox Administration] | [!UICONTROL Reset a Sandbox] | Possibilità di reimpostare una sandbox. |
| [!DNL Destinations] | [!UICONTROL Manage Destinations] | Accesso a destinazioni in lettura, creazione, modifica e disattivazione. |
| [!DNL Destinations] | [!UICONTROL View Destinations] | Accesso in sola lettura alle destinazioni disponibili nella scheda **[!UICONTROL Catalog]** e alle destinazioni autenticate nella scheda **[!UICONTROL Browse]** . |
| [!DNL Destinations] | [!UICONTROL Activate Destinations] | Possibilità di attivare i dati nelle destinazioni attive create. Questa autorizzazione richiede che &quot;View Destinations&quot; (Visualizza destinazioni) o &quot;Manage [!UICONTROL Destinations”] (Gestisci) sia concesso all&#39;utente che attiva le destinazioni. |
| [!DNL Data Ingestion] | [!UICONTROL Manage Sources] | Accesso a fonti di lettura, creazione, modifica e disattivazione. |
| [!DNL Data Ingestion] | [!UICONTROL View Sources] | Accesso in sola lettura alle origini disponibili nella scheda **[!UICONTROL Catalog]** e alle origini autenticate nella scheda **[!UICONTROL Browse]** . |
| [!DNL Data Science Workspace] | [!UICONTROL Manage Data Science Workspace] | Accesso a lettura, creazione, modifica ed eliminazione in [!DNL Data Science Workspace]. |
| [!DNL Data Governance] | [!UICONTROL Apply Data Usage Labels] | Accesso per leggere, creare ed eliminare le etichette di utilizzo. |
| [!DNL Data Governance] | [!UICONTROL Manage Data Usage Policies] | Accesso a criteri di utilizzo dei dati di lettura, creazione, modifica ed eliminazione. |
| [!DNL Data Governance] | [!UICONTROL View Data Usage Policies] | Accesso in sola lettura per i criteri di utilizzo dei dati appartenenti all’organizzazione. |
| [!DNL Query Service] | [!UICONTROL Manage Queries] | Accesso alla lettura, alla creazione, alla modifica e all&#39;eliminazione di query SQL strutturate per i dati di Platform. |

## Passaggi successivi

Leggendo questa guida, ti sono stati introdotti i principi principali del controllo degli accessi in [!DNL Experience Platform]. È ora possibile continuare la [guida utente per il controllo degli accessi](./ui/overview.md) per passaggi dettagliati su come utilizzare [!DNL Admin Console] per creare profili di prodotto e assegnare autorizzazioni per [!DNL Platform].
