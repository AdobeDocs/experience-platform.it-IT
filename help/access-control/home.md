---
keywords: Experience Platform;home;argomenti popolari;controllo degli accessi;adobe admin console
solution: Experience Platform
title: Panoramica sul controllo degli accessi
description: Il controllo degli accessi per Adobe Experience Platform viene fornito tramite Adobe Admin Console. Questa funzionalità sfrutta i profili di prodotto di Admin Console, che collegano gli utenti con autorizzazioni e sandbox.
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: 56f1cbc622450b154e6e29a8116789b316901f66
workflow-type: tm+mt
source-wordcount: '1473'
ht-degree: 3%

---

# Panoramica sul controllo degli accessi

Controllo degli accessi per [!DNL Experience Platform] viene fornito tramite [Adobe Admin Console](https://adminconsole.adobe.com). Questa funzionalità sfrutta i profili di prodotto in [!DNL Admin Console], che collega gli utenti con autorizzazioni e sandbox.

## Gerarchia e flusso di lavoro di controllo degli accessi

Per configurare il controllo degli accessi per [!DNL Experience Platform], è necessario disporre dei privilegi di amministratore per un&#39;organizzazione con [!DNL Experience Platform] integrazione dei prodotti. Il ruolo minimo per concedere o revocare le autorizzazioni è quello di amministratore del profilo di prodotto. Altri ruoli di amministratore che possono gestire le autorizzazioni sono amministratori di prodotto (possono gestire tutti i profili all’interno di un prodotto) e amministratori di sistema (senza restrizioni). Consulta l’articolo di Adobe Help Center su [ruoli amministrativi](https://helpx.adobe.com/enterprise/using/admin-roles.html) per ulteriori informazioni.

>[!NOTE]
>
>Da questo punto in poi, qualsiasi menzione di &quot;amministratore&quot; in questo documento si riferisce a un amministratore del profilo di prodotto o a un livello superiore (come descritto sopra).

Un flusso di lavoro di alto livello per l’ottenimento e l’assegnazione delle autorizzazioni di accesso può essere riassunto come segue:

- Dopo aver concesso la licenza per Adobe Experience Platform o un servizio applicazione/app che utilizza Experience Platform, viene inviata un’e-mail all’amministratore specificato durante la gestione della licenza.
- L’amministratore accede a [Adobe Admin Console](#adobe-admin-console) e seleziona **Adobe Experience Platform** dall’elenco dei prodotti nella pagina della panoramica.
- L&#39;amministratore può visualizzare il valore predefinito [profili di prodotto](#product-profiles) o creare nuovi profili di prodotto del cliente, in base alle esigenze.
- L’amministratore può modificare le autorizzazioni e gli utenti per qualsiasi profilo di prodotto esistente.
- Quando crea o modifica un profilo di prodotto, l’amministratore lo aggiunge al profilo utilizzando **[!UICONTROL utenti]** e concede le autorizzazioni a questi utenti (ad esempio &quot;[!UICONTROL Leggi set di dati]&quot; o &quot;[!UICONTROL Gestire gli schemi]&quot;) accedendo al **[!UICONTROL autorizzazioni]** scheda. Analogamente, l’amministratore può assegnare l’accesso alle sandbox utilizzando la stessa scheda di autorizzazioni.
- Quando gli utenti accedono a [!DNL Experience Platform] dell&#39;interfaccia utente, il loro accesso a [!DNL Platform] Le funzionalità sono guidate dalle autorizzazioni concesse loro dal passaggio 2. Ad esempio, se un utente non dispone della proprietà &quot;[!UICONTROL Visualizzare i set di dati]&quot;, l&#39;autorizzazione **[!UICONTROL Set di dati]** nel menu laterale non sarà visibile a tale utente.

Per passaggi più dettagliati su come gestire il controllo degli accessi in [!DNL Experience Platform], vedere [guida utente al controllo degli accessi](./ui/overview.md).

Tutte le chiamate a [!DNL Experience Platform] Le API vengono convalidate per le autorizzazioni e restituiranno errori se le autorizzazioni appropriate non vengono trovate nel contesto utente corrente. Nell’interfaccia utente, gli elementi verranno nascosti o modificati a seconda delle autorizzazioni concesse all’utente corrente.

## Adobe Admin Console

Adobe Admin Console fornisce una posizione centrale per la gestione delle adesioni ai prodotti Adobe e dell’accesso per la tua organizzazione. Tramite la console, puoi concedere a gruppi di utenti le autorizzazioni di accesso per vari [!DNL Platform] funzionalità, ad esempio &quot;[!UICONTROL Gestione set di dati]&quot;, &quot;[!UICONTROL Visualizzare i set di dati]&quot;, o &quot;[!UICONTROL Gestisci profili]&quot;.

### Profili di prodotto

In [!DNL Admin Console], le autorizzazioni vengono assegnate agli utenti tramite l’utilizzo di profili di prodotto. I profili di prodotto consentono di concedere autorizzazioni a uno o più utenti e contengono anche il loro accesso all’ambito delle sandbox assegnate loro tramite i profili di prodotto. Gli utenti possono essere assegnati a uno o più profili di prodotto appartenenti alla tua organizzazione.

### Profili di prodotto predefiniti

[!DNL Experience Platform] viene fornito con due profili di prodotto predefiniti preconfigurati. La tabella seguente illustra cosa viene fornito in ciascun profilo predefinito, inclusa la sandbox a cui concedono l’accesso e le autorizzazioni che concedono nell’ambito di tale sandbox.

| Profilo di prodotto | Accesso alla sandbox | Autorizzazioni |
| --- | --- | --- |
| Accesso predefinito per tutti gli elementi di produzione | Produzione | Tutte le autorizzazioni applicabili a [!DNL Experience Platform], ad eccezione delle autorizzazioni di amministrazione delle sandbox. |
| Amministratori sandbox | N/D | Consente di accedere solo alle autorizzazioni di amministrazione delle sandbox. |

## Sandbox e autorizzazioni

Le sandbox non di produzione sono una forma di virtualizzazione dei dati che consente di isolare i dati da altre sandbox e sono in genere utilizzate per esperimenti di sviluppo, test o test. Le autorizzazioni di un profilo di prodotto consentono agli utenti del profilo di accedere a [!DNL Platform] funzionalità all’interno degli ambienti sandbox a cui è stato consentito l’accesso. Una licenza di Experience Platform predefinita ti concede cinque sandbox (una di produzione e quattro non di produzione). Puoi aggiungere pacchetti di dieci sandbox non di produzione per un massimo di 75 sandbox in totale. Per ulteriori informazioni, contatta l’amministratore dell’organizzazione IMS o il tuo rappresentante commerciale Adobe.

Per ulteriori informazioni sulle sandbox in [!DNL Experience Platform], fare riferimento al [panoramica sulle sandbox](../sandboxes/home.md).

### Accesso alle sandbox

L’accesso alle sandbox viene gestito tramite i profili di prodotto. Per i passaggi dettagliati su come abilitare l’accesso a una sandbox per un profilo di prodotto, consulta [guida utente al controllo degli accessi](./ui/overview.md).

Gli utenti possono essere autorizzati ad accedere a una o più sandbox all’interno di un profilo di prodotto. Se un utente è incluso in due o più profili di prodotto, avrà accesso a tutte le sandbox incluse in tali profili.

L’autorizzazione &quot;Sandbox Management&quot; (Gestione sandbox) consente agli utenti di gestire, visualizzare o ripristinare le sandbox.

### Autorizzazioni {#permissions}

Nella scheda delle autorizzazioni all’interno di un profilo di prodotto vengono visualizzate le sandbox e le autorizzazioni attive per tale profilo:

![permissions-overview](./images/permissions.png)

Autorizzazioni concesse tramite [!DNL Admin Console] sono ordinati per categoria, con alcune autorizzazioni che consentono l’accesso a diverse funzionalità di basso livello.

La tabella seguente illustra le autorizzazioni disponibili per [!DNL Experience Platform] nel [!DNL Admin Console], con descrizioni delle specifiche [!DNL Platform] le funzionalità a cui concedono l’accesso. Per i passaggi dettagliati su come aggiungere le autorizzazioni a un profilo di prodotto, consulta [guida utente al controllo degli accessi](./ui/overview.md).

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
| [!DNL Identity Management] | [!UICONTROL Manage Identity Namespaces (Gestisci spazi dei nomi di identità)] | Accesso per leggere, creare, modificare ed eliminare spazi dei nomi di identità. |
| [!DNL Identity Management] | [!UICONTROL Visualizzare gli spazi dei nomi delle identità] | Accesso in sola lettura per gli spazi dei nomi di identità. |
| [!DNL Identity Management] | [!UICONTROL Visualizza grafico delle identità] | Accesso in sola lettura per i grafici di identità. |
| [!DNL Sandbox Administration] | [!UICONTROL Gestione sandbox] | Accesso alle sandbox di lettura, creazione, modifica ed eliminazione. |
| [!DNL Sandbox Administration] | [!UICONTROL View Sandboxes (Visualizza sandbox)] | Accesso in sola lettura per le sandbox appartenenti alla tua organizzazione. |
| [!DNL Sandbox Administration] | [!UICONTROL Ripristinare una sandbox] | Possibilità di ripristinare una sandbox. |
| [!DNL Destinations] | [!UICONTROL Gestire le destinazioni] | Accesso a destinazioni di lettura, creazione, modifica e disattivazione. |
| [!DNL Destinations] | [!UICONTROL Visualizza destinazioni] | Accesso in sola lettura alle destinazioni disponibili in **[!UICONTROL Catalogo]** e le destinazioni autenticate in **[!UICONTROL Sfoglia]** scheda. |
| [!DNL Destinations] | [!UICONTROL Attivare le destinazioni] | Possibilità di attivare i dati per le destinazioni attive create. Questa autorizzazione richiede [!UICONTROL Visualizza destinazioni] o [!UICONTROL Gestire le destinazioni] da concedere all’utente che attiverà le destinazioni. |
| [!DNL Destinations] | [!UICONTROL Gestire e attivare le destinazioni dei set di dati] | Possibilità di leggere, creare, modificare e disabilitare i flussi di esportazione dei set di dati. Possibilità di attivare i dati anche per i set di dati attivi che sono stati creati. |
| [!DNL Destinations] | [!UICONTROL Authoring delle destinazioni] | Possibilità di creare destinazioni utilizzando [Adobe Experience Platform Destination SDK](../destinations/destination-sdk/overview.md). |
| [!DNL Data Ingestion] | [!UICONTROL Gestisci origini] | Accesso per leggere, creare, modificare e disabilitare le origini. |
| [!DNL Data Ingestion] | [!UICONTROL Visualizza origini] | Accesso in sola lettura alle origini disponibili in **[!UICONTROL Catalogo]** e le origini autenticate in **[!UICONTROL Sfoglia]** scheda. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | Accesso per creare, accettare e rifiutare handshake partner per connettere due organizzazioni IMS e abilitare [!DNL Segment Match] flussi. |
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

Una volta letta questa guida, potrai scoprire i principi fondamentali del controllo degli accessi in [!DNL Experience Platform]. Ora puoi passare alla sezione [guida utente al controllo degli accessi](./ui/overview.md) per i passaggi dettagliati su come utilizzare [!DNL Admin Console] per creare profili di prodotto e assegnare autorizzazioni per [!DNL Platform].
