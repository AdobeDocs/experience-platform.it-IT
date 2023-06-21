---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;profilo unificato;profilo unificato;unificato;profilo;rtcp;abilitare profilo;abilitare profilo;abilitare profilo
title: Guida all’API del profilo cliente in tempo reale
description: L’API Profilo cliente in tempo reale consente agli sviluppatori di esplorare e utilizzare i dati del profilo, tra cui la visualizzazione dei profili, la creazione e l’aggiornamento di criteri di unione, l’esportazione o l’esempio di dati del profilo e l’eliminazione dei dati del profilo che non sono più necessari o che sono stati aggiunti per errore. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
exl-id: ce39b95b-cff7-46cf-a14c-8203017c8826
source-git-commit: 3b4e1e793a610c9391b3718584a19bd11959e3be
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 1%

---

# Guida dell’API di [!DNL Real-Time Customer Profile]

[!DNL Real-Time Customer Profile] consente di visualizzare una visione olistica di ciascuno dei singoli clienti all’interno di Adobe Experience Platform. [!DNL Profile] consente di consolidare dati cliente diversi da più canali, come dati online, offline, del sistema CRM e di terze parti, in una visualizzazione unificata che offre un account actionable e con marca temporale di ogni interazione con il cliente.

Il [!DNL Real-Time Customer Profile] L’API include più endpoint, descritti di seguito. Per informazioni dettagliate, consulta le guide dei singoli endpoint e fai riferimento a [guida introduttiva](getting-started.md) per informazioni importanti sulle intestazioni richieste, leggi le chiamate API di esempio e altro ancora.

Per visualizzare tutti gli endpoint disponibili e le operazioni CRUD, visitare il [Swagger di riferimento API del profilo cliente in tempo reale](https://www.adobe.com/go/profile-apis-en).

Per una guida all’utilizzo di [!DNL Real-Time Customer Profile] dati in [!DNL Experience Platform] Interfaccia utente, fare riferimento a [Guida utente del profilo](../ui/user-guide.md).

## [!BADGE Beta]Attributi calcolati {type=Informative} {#computed-attributes}

>[!IMPORTANT]
>
>La funzionalità degli attributi calcolati è disponibile in versione beta e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

Gli attributi calcolati sono funzioni utilizzate per aggregare i dati a livello di evento negli attributi a livello di profilo. Queste funzioni vengono calcolate automaticamente in modo che possano essere utilizzate in segmentazione, attivazione e personalizzazione.

Ogni attributo calcolato contiene un’espressione, o &quot;regola&quot;, che valuta i dati in arrivo e memorizza il valore risultante in un attributo di profilo. Questi calcoli consentono di rispondere facilmente a domande relative ad aspetti quali il valore di acquisto del ciclo di vita, il tempo che intercorre tra un acquisto e l&#39;altro o il numero di aperture dell&#39;applicazione, senza dover eseguire manualmente calcoli complessi ogni volta che sono necessarie le informazioni. Questi valori di attributo calcolati possono quindi essere visualizzati in un profilo, utilizzati per creare un segmento o accessibili tramite diversi modelli di accesso.

È possibile creare, visualizzare, modificare ed eliminare attributi calcolati utilizzando `ca/attributes/` endpoint. Per informazioni su come utilizzare gli attributi calcolati, consulta [panoramica degli attributi calcolati](../computed-attributes/overview.md). Per le operazioni API, visita [guida dell’endpoint API per attributi calcolati](../computed-attributes/api.md).

## Proiezioni spigolo {#edge-projections}

Adobe Experience Platform consente la personalizzazione in tempo reale delle esperienze dei clienti rendendo i dati facilmente accessibili su server in posizione strategica denominati &quot;edge&quot;. Il [!DNL Real-Time Customer Profile] L’API fornisce endpoint per l’utilizzo degli spigoli tramite componenti denominati &quot;proiezioni&quot;. Ciò include configurazioni di proiezione per determinare quali dati devono essere proiettati a ciascun bordo, nonché destinazioni di proiezione per definire dove indirizzare una proiezione. Per informazioni dettagliate sull&#39;utilizzo delle proiezioni Edge, visitare il sito Web [guida alle configurazioni di proiezione e agli endpoint di destinazione](edge-projections.md).

## Entità ([!DNL Profile] access) {#entities}

Tramite Adobe Experience Platform è possibile accedere a [!DNL Real-Time Customer Profile] dati utilizzando le API RESTful o l’interfaccia utente di. Per scoprire come accedere alle entità, più comunemente note come &quot;profili&quot;, utilizzando l’API, segui i passaggi descritti in [guida dell’endpoint &quot;entities&quot;](entities.md). Per accedere ai profili utilizzando [!DNL Platform] interfaccia utente, fare riferimento a [Guida utente del profilo](../ui/user-guide.md).

## Processi di esportazione ([!DNL Profile] export) {#profile-export}

[!DNL Real-Time Customer Profile] i dati possono essere esportati in un set di dati per ulteriore elaborazione, ad esempio per l’esportazione di segmenti di pubblico per l’attivazione o di attributi di profilo per il reporting. I processi di esportazione per i segmenti di pubblico fanno parte del [!DNL Adobe Experience Platform Segmentation Service] API, leggi le [guida dell’endpoint &quot;segmentation export jobs&quot;](../../profile/api/export-jobs.md) per ulteriori informazioni. Per istruzioni dettagliate su come creare e gestire processi di esportazione per gli attributi del profilo, visita [guida dell’endpoint &quot;export jobs&quot;](export-jobs.md).

## Criteri di unione {#merge-policies}

Quando si uniscono dati provenienti da più origini in [!DNL Experience Platform], i criteri di unione sono le regole che [!DNL Platform] utilizza per determinare come assegnare la priorità ai dati e quali dati verranno combinati per creare singoli profili cliente. Utilizzo di [!DNL Real-Time Customer Profile] API, puoi creare nuovi criteri di unione, gestire quelli esistenti e impostare un criterio di unione predefinito per la tua organizzazione. Per utilizzare i criteri di unione tramite l’API, visita la [guida dell’endpoint &quot;merge policies&quot;](merge-policies.md).

Per ulteriori informazioni sui criteri di unione e sul loro ruolo in Platform, leggi [panoramica dei criteri di unione](../merge-policies/overview.md).

## Anteprima stato campione ([!DNL Profile] preview) {#profile-preview}

Quando i dati vengono acquisiti in Platform, viene eseguito un processo di esempio per aggiornare il conteggio dei profili e altre metriche relative ai dati del profilo cliente in tempo reale. I risultati di questo processo di esempio possono essere visualizzati utilizzando `/previewsamplestatus` endpoint, parte dell’API del profilo cliente in tempo reale. Questo endpoint può essere utilizzato anche per elencare le distribuzioni di profilo per set di dati e spazio dei nomi delle identità, nonché per generare più rapporti al fine di ottenere visibilità nella composizione dell’archivio profili della tua organizzazione.  Per iniziare a utilizzare `/profilepreviewstatus` endpoint, fare riferimento al [guida dell’endpoint &quot;preview sample status&quot;](preview-sample-status.md).

## Processi di sistema del profilo {#profile-system-jobs}

Dati abilitati per il profilo acquisiti in [!DNL Platform] è memorizzato in [!DNL Data Lake] nonché [!DNL Real-Time Customer Profile] archivio dati. A volte può essere necessario eliminare un set di dati o un batch da [!DNL Profile] archiviare per rimuovere i dati che non sono più necessari o che sono stati aggiunti per errore. A tal fine è necessario utilizzare l’API per creare un’ [!DNL Profile System Job], noto anche come &quot;[!DNL delete request]&quot;, che possono essere modificati, monitorati o eliminati se necessario. Per scoprire come lavorare con le richieste di eliminazione utilizzando `/system/jobs` endpoint nella [!DNL Real-Time Customer Profile] , segui i passaggi descritti in [guida dell’endpoint &quot;profile system jobs&quot;](profile-system-jobs.md).

## Aggiornare gli attributi dei profili {#update-profile}

A volte può essere necessario aggiornare i dati nell’archivio profili della tua organizzazione. Ad esempio, potrebbe essere necessario correggere i record o modificare un valore di attributo. Questa operazione può essere eseguita tramite l’acquisizione in batch e richiede un set di dati abilitato per il profilo configurato con un tag upsert. Per ulteriori informazioni su come configurare un set di dati per gli aggiornamenti degli attributi, consulta l’esercitazione per [abilitazione di un set di dati per Profilo e upsert](../../catalog/datasets/enable-upsert.md).

## Passaggi successivi {#next-steps}

Per iniziare a effettuare chiamate utilizzando [!DNL Real-Time Customer Profile] API, leggi [guida introduttiva](getting-started.md) quindi seleziona una delle guide degli endpoint per scoprire come utilizzare [!DNL Profile]Endpoint correlati. Per lavorare con [!DNL Profile] dati utilizzando [!DNL Experience Platform] Interfaccia utente, fare riferimento a [Guida utente di Real-Time Customer Profile](../ui/user-guide.md).
