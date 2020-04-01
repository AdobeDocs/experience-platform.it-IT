---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Panoramica sul controllo degli accessi
topic: overview
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


# Panoramica sul controllo degli accessi

Il controllo degli accessi per Experience Platform è fornito tramite [Adobe Admin Console](https://adminconsole.adobe.com). Questa funzionalità sfrutta i profili di prodotto in Admin Console, che collegano gli utenti con autorizzazioni e sandbox.

## Gerarchia e flusso di lavoro del controllo degli accessi

Per configurare il controllo di accesso per Experience Platform, devi disporre dei privilegi di amministratore per un&#39;organizzazione che dispone di un&#39;integrazione con un prodotto Experience Platform. Il ruolo minimo che concede o revoca le autorizzazioni è un amministratore **del profilo di** prodotto. Altri ruoli di amministratore che possono gestire le autorizzazioni sono gli amministratori **di** prodotto (in grado di gestire tutti i profili all&#39;interno di un prodotto) e gli amministratori **di** sistema (senza restrizioni). Per ulteriori informazioni, consultate l&#39;articolo Adobe Help Center sui ruoli [](https://helpx.adobe.com/enterprise/using/admin-roles.html) amministrativi.

>[!NOTE] Da questo punto in poi, qualsiasi menzione di &quot;amministratore&quot; in questo documento fa riferimento a un amministratore del profilo di prodotto o a una versione successiva (come indicato sopra).

Un flusso di lavoro di alto livello per ottenere e assegnare le autorizzazioni di accesso può essere riassunto come segue:

- Dopo l&#39;iscrizione ad Adobe Experience Platform, viene inviato un messaggio e-mail all&#39;amministratore specificato nel modulo di registrazione.
- L’amministratore accede ad [Adobe Admin Console](#adobe-admin-console) e seleziona **Adobe Experience Platform** dall’elenco dei prodotti nella pagina della panoramica.
- L&#39;amministratore può visualizzare i profili [di](#product-profiles) prodotto predefiniti o creare nuovi profili di prodotto cliente, a seconda delle necessità.
- L&#39;amministratore può modificare le autorizzazioni e gli utenti per qualsiasi profilo di prodotto esistente.
- Durante la creazione o la modifica di un profilo di prodotto, l&#39;amministratore aggiunge gli utenti al profilo utilizzando la scheda **utenti** e concede le autorizzazioni a tali utenti (ad esempio &quot;Leggi i dati&quot; o &quot;Gestisci schemi&quot;) accedendo alla scheda delle **autorizzazioni** . Analogamente, l&#39;amministratore può assegnare l&#39;accesso alle sandbox utilizzando la stessa scheda delle autorizzazioni.
- Quando gli utenti accedono all&#39;interfaccia utente della piattaforma Experience, il loro accesso alle funzionalità della piattaforma è determinato dalle autorizzazioni concesse loro dal Passaggio 2. Ad esempio, se un utente non dispone dell&#39;autorizzazione &quot;Visualizza set di dati&quot;, la scheda *Set* di dati del menu laterale non sarà visibile all&#39;utente.

Per informazioni dettagliate su come gestire il controllo degli accessi in Experience Platform, consultate la guida [utente per il controllo degli](./ui/overview.md)accessi.

Tutte le chiamate alle API della piattaforma Experience vengono convalidate per le autorizzazioni e restituiranno errori se le autorizzazioni appropriate non vengono trovate nel contesto utente corrente. Nell’interfaccia utente, gli elementi verranno nascosti o modificati in base alle autorizzazioni concesse all’utente corrente.

## Adobe Admin Console

Adobe Admin Console fornisce una posizione centrale per la gestione delle adesioni ai prodotti Adobe e l&#39;accesso per la tua organizzazione. Tramite la console, potete concedere a gruppi di utenti autorizzazioni di accesso per diverse funzionalità della piattaforma, come &quot;Gestisci set di dati&quot;, &quot;Visualizza set di dati&quot; o &quot;Gestisci profili&quot;.

### Profili di prodotto

In Admin Console, le autorizzazioni vengono assegnate agli utenti tramite l&#39;uso dei profili **di** prodotto. I profili di prodotto consentono di concedere le autorizzazioni a uno o più utenti e contengono anche il loro accesso all&#39;ambito delle sandbox che sono loro assegnate tramite i profili di prodotto. Gli utenti possono essere assegnati a uno o più profili di prodotto appartenenti alla tua organizzazione.

### Profili di prodotto predefiniti

Experience Platform viene fornito con due profili di prodotto predefiniti preconfigurati. La tabella seguente riassume i dati forniti in ciascun profilo predefinito, inclusa la sandbox a cui concedono l&#39;accesso, nonché le autorizzazioni concesse all&#39;interno dell&#39;ambito di tale sandbox.

| Profilo di prodotto | Accesso sandbox | Autorizzazioni |
| --- | --- | --- |
| Produzione predefinita - Accesso completo | Produzione | Tutte le autorizzazioni applicabili a Experience Platform, tranne quelle per l&#39;amministrazione sandbox. |
| Amministrazione sandbox predefinita | N/D | Fornisce l&#39;accesso solo alle autorizzazioni Amministrazione sandbox. |

## Sandbox e autorizzazioni

Experience Platform consente di accedere a una sandbox di produzione e di creare **sandbox** non di produzione. Le sandbox non di produzione sono una forma di virtualizzazione dei dati che consente di isolare i dati da altre sandbox e sono generalmente utilizzate per esperimenti di sviluppo, test o test. Le **autorizzazioni** di un profilo di prodotto forniscono agli utenti del profilo l&#39;accesso alle funzionalità della piattaforma all&#39;interno degli ambienti sandbox a cui gli è stato concesso l&#39;accesso.

Per ulteriori informazioni sulle sandbox in Experience Platform, consultate la panoramica [sulle](../sandboxes/home.md)sandbox.

### Accesso alle sandbox

L&#39;accesso alle sandbox è gestito tramite i profili di prodotto. Per istruzioni dettagliate su come abilitare l&#39;accesso a una sandbox per un profilo di prodotto, consultate la guida [utente per il controllo](./ui/overview.md)degli accessi.

Agli utenti può essere concesso l&#39;accesso a una o più sandbox all&#39;interno di un profilo di prodotto. Se un utente è incluso in due o più profili di prodotto, avrà accesso a tutte le sandbox incluse in tali profili.

L&#39;autorizzazione &quot;Gestione sandbox&quot; consente agli utenti di gestire, visualizzare o ripristinare le sandbox.

### Autorizzazioni

La scheda **Autorizzazioni** all&#39;interno di un profilo di prodotto visualizza le sandbox e le autorizzazioni attive per tale profilo:

![](./images/permissions-overview.png)

Le autorizzazioni concesse tramite Admin Console sono ordinate per categoria, con alcune autorizzazioni che concedono l&#39;accesso a diverse funzionalità di basso livello.

La tabella seguente riassume le autorizzazioni disponibili per Experience Platform nell’Admin Console e descrive le funzionalità specifiche della piattaforma a cui concedono l’accesso. Per i passaggi dettagliati su come aggiungere le autorizzazioni a un profilo di prodotto, consulta la guida [utente per il controllo](./ui/overview.md)degli accessi.

| Categoria | Autorizzazione | Descrizione |
| --- | --- | --- |
| Modellazione dati | Gestione schemi | Accesso per leggere, creare, modificare ed eliminare schemi e risorse correlate. |
| Modellazione dati | Visualizza schemi | Accesso in sola lettura agli schemi e alle risorse correlate. |
| Gestione dei dati | Gestisci set di dati | Accesso per la lettura, la creazione, la modifica e l&#39;eliminazione dei set di dati. Accesso in sola lettura per gli schemi. |
| Gestione dei dati | Visualizza set di dati | Accesso in sola lettura per set di dati e schemi. |
| Gestione dei dati | Monitoraggio dei dati | Accesso in sola lettura ai set di dati e ai flussi di monitoraggio. |
| Gestione profili | Gestisci profili | Accesso per leggere, creare, modificare ed eliminare i set di dati utilizzati per i profili cliente. Accesso in sola lettura ai profili disponibili. |
| Gestione profili | Visualizza profili | Accesso in sola lettura ai profili disponibili. |
| Gestione profili | Esporta pubblico per segmento | Possibilità di esportare un segmento di pubblico valutato in un dataset. |
| Identità | Gestisci spazi dei nomi identità | Accesso agli spazi dei nomi delle identità di lettura, creazione, modifica ed eliminazione. |
| Identità | Visualizza spazi dei nomi identità | Accesso in sola lettura per gli spazi dei nomi di identità. |
| Amministrazione sandbox | Gestisci sandbox | Accesso alle sandbox di lettura, creazione, modifica ed eliminazione. |
| Amministrazione sandbox | Visualizza sandbox | Accesso in sola lettura per le sandbox appartenenti alla vostra organizzazione. |
| Amministrazione sandbox | Reimpostare una sandbox | Possibilità di ripristinare una sandbox. |
| Destinazioni | Gestione destinazioni | Accesso alle destinazioni di lettura, creazione, modifica e disattivazione.* |
| Destinazioni | Visualizza destinazioni | Accesso in sola lettura alle destinazioni disponibili nella scheda *Catalogo* e alle destinazioni autenticate nella scheda *Sfoglia* .* |
| Destinazioni | Attiva destinazioni | Possibilità di attivare i dati nelle destinazioni attive create. Questa autorizzazione richiede che all&#39;utente che attiverà le destinazioni sia concesso &quot;Visualizza destinazioni&quot; o &quot;Gestisci destinazioni&quot;.* |
| Ingestione dati | Gestisci origini | Accesso alle origini di lettura, creazione, modifica e disattivazione. |
| Ingestione dati | Visualizza origini | Accesso in sola lettura alle origini disponibili nella scheda *Catalogo* e alle origini autenticate nella scheda *Sfoglia* . |
| Area di lavoro Data Science | Gestisci area di lavoro Data Science | Accesso a lettura, creazione, modifica ed eliminazione in Data Science Workspace. |

_(*) Questa autorizzazione richiede disposizioni per la piattaforma dati cliente in tempo reale. Per ulteriori informazioni sulla CDP in tempo reale, consultare la panoramica[CDP in tempo](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/overview.html)reale._

## Passaggi successivi

Leggendo questa guida, hai introdotto i principi principali del controllo degli accessi in Experience Platform. Ora puoi continuare a seguire la guida [utente per il controllo degli](./ui/overview.md) accessi per i passaggi dettagliati su come utilizzare Admin Console per creare profili di prodotto e assegnare le autorizzazioni per la piattaforma.