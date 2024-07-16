---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;profilo unificato;profilo unificato;unificato;profilo;rtcp;abilitare profilo;abilitare profilo;abilitare profilo
title: Guida all’API del profilo cliente in tempo reale
description: L’API Profilo cliente in tempo reale consente agli sviluppatori di esplorare e utilizzare i dati del profilo, tra cui la visualizzazione dei profili, la creazione e l’aggiornamento di criteri di unione, l’esportazione o l’esempio di dati del profilo e l’eliminazione dei dati del profilo che non sono più necessari o che sono stati aggiunti per errore. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
role: Developer
exl-id: ce39b95b-cff7-46cf-a14c-8203017c8826
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 2%

---

# Guida dell’API di [!DNL Real-Time Customer Profile]

[!DNL Real-Time Customer Profile] consente di visualizzare una visualizzazione olistica di ciascuno dei singoli clienti all&#39;interno di Adobe Experience Platform. [!DNL Profile] consente di consolidare dati cliente diversi da più canali, come dati online, offline, del sistema CRM e di terze parti, in una visualizzazione unificata che offre un account utilizzabile e con marca temporale di ogni interazione con il cliente.

L&#39;API [!DNL Real-Time Customer Profile] include più endpoint, descritti di seguito. Per informazioni dettagliate, consulta le guide dei singoli endpoint e fai riferimento alla [guida introduttiva](getting-started.md) per informazioni importanti sulle intestazioni richieste, sulla lettura delle chiamate API di esempio e altro ancora.

Per visualizzare tutti gli endpoint disponibili e le operazioni CRUD, visita il [Swagger di riferimento API del profilo cliente in tempo reale](https://www.adobe.com/go/profile-apis-en).

Per una guida all&#39;utilizzo dei dati di [!DNL Real-Time Customer Profile] nell&#39;interfaccia utente di [!DNL Experience Platform], fare riferimento alla [guida utente del profilo](../ui/user-guide.md).

## Attributi calcolati di [!BADGE Beta]{type=Informative} {#computed-attributes}

>[!IMPORTANT]
>
La funzionalità degli attributi calcolati è disponibile in versione beta e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

Gli attributi calcolati sono funzioni utilizzate per aggregare i dati a livello di evento negli attributi a livello di profilo. Queste funzioni vengono calcolate automaticamente in modo che possano essere utilizzate in segmentazione, attivazione e personalizzazione.

Ogni attributo calcolato contiene un’espressione, o &quot;regola&quot;, che valuta i dati in arrivo e memorizza il valore risultante in un attributo di profilo. Questi calcoli consentono di rispondere facilmente a domande relative a fattori quali il valore di acquisto del ciclo di vita, il tempo che intercorre tra un acquisto e l&#39;altro o il numero di aperture dell&#39;applicazione, senza richiedere di eseguire manualmente calcoli complessi ogni volta che le informazioni sono necessarie. Questi valori di attributo calcolati possono quindi essere visualizzati in un profilo, utilizzati per creare un pubblico o accessibili tramite diversi modelli di accesso.

È possibile creare, visualizzare, modificare ed eliminare attributi calcolati utilizzando l&#39;endpoint `ca/attributes/`. Per informazioni sull&#39;utilizzo degli attributi calcolati, consultare la [panoramica degli attributi calcolati](../computed-attributes/overview.md). Per le operazioni API, visita la [guida dell&#39;endpoint API per attributi calcolati](../computed-attributes/api.md).

## Entità ([!DNL Profile] accesso) {#entities}

Tramite Adobe Experience Platform è possibile accedere ai dati di [!DNL Real-Time Customer Profile] utilizzando le API RESTful o l&#39;interfaccia utente. Per informazioni su come accedere alle entità, più comunemente note come &quot;profili&quot;, utilizzando l&#39;API, segui i passaggi descritti nella [guida dell&#39;endpoint entità](entities.md). Per accedere ai profili tramite l&#39;interfaccia utente [!DNL Platform], fare riferimento alla [Guida utente del profilo](../ui/user-guide.md).

## Processi di esportazione ([!DNL Profile] esportazione) {#profile-export}

I dati [!DNL Real-Time Customer Profile] possono essere esportati in un set di dati per ulteriore elaborazione, ad esempio per l&#39;esportazione di tipi di pubblico per l&#39;attivazione o per gli attributi di profilo per il reporting. I processi di esportazione per i tipi di pubblico fanno parte dell&#39;API [!DNL Adobe Experience Platform Segmentation Service]. Per ulteriori informazioni, leggere la [guida dell&#39;endpoint dei processi di esportazione segmentazione](../../profile/api/export-jobs.md). Per istruzioni dettagliate su come creare e gestire i processi di esportazione per gli attributi del profilo, consulta la [guida dell&#39;endpoint dei processi di esportazione](export-jobs.md).

## Criteri di unione {#merge-policies}

Quando si riuniscono dati provenienti da più origini in [!DNL Experience Platform], i criteri di unione sono le regole utilizzate da [!DNL Platform] per determinare la priorità dei dati e i dati che verranno combinati per creare profili cliente individuali. Utilizzando l&#39;API [!DNL Real-Time Customer Profile], è possibile creare nuovi criteri di unione, gestire i criteri esistenti e impostare un criterio di unione predefinito per l&#39;organizzazione. Per utilizzare i criteri di unione tramite l&#39;API, visita la [guida dell&#39;endpoint dei criteri di unione](merge-policies.md).

Per ulteriori informazioni sui criteri di unione e sul loro ruolo in Platform, consulta la [panoramica dei criteri di unione](../merge-policies/overview.md).

## Anteprima stato campione ([!DNL Profile] anteprima) {#profile-preview}

Quando i dati vengono acquisiti in Platform, viene eseguito un processo di esempio per aggiornare il conteggio dei profili e altre metriche relative ai dati del profilo cliente in tempo reale. I risultati di questo processo di esempio possono essere visualizzati utilizzando l&#39;endpoint `/previewsamplestatus`, parte dell&#39;API Real-Time Customer Profile. Questo endpoint può essere utilizzato anche per elencare le distribuzioni di profilo per set di dati e spazio dei nomi delle identità, nonché per generare più rapporti al fine di ottenere visibilità nella composizione dell’archivio profili della tua organizzazione.  Per iniziare a utilizzare l&#39;endpoint `/profilepreviewstatus`, fare riferimento alla [guida dell&#39;endpoint di stato di esempio di anteprima](preview-sample-status.md).

## Processi di sistema del profilo {#profile-system-jobs}

I dati abilitati per il profilo acquisiti in [!DNL Platform] sono memorizzati nell&#39;archivio dati [!DNL Data Lake] e [!DNL Real-Time Customer Profile]. Talvolta può essere necessario eliminare i dati di profilo associati a un set di dati dall’archivio Profili per rimuovere i dati non più necessari o che sono stati aggiunti per errore. È necessario utilizzare l&#39;API per creare un [!DNL Profile System Job], noto anche come &quot;[!DNL delete request]&quot;, che può essere modificato, monitorato o eliminato se necessario. Per informazioni su come gestire le richieste di eliminazione utilizzando l&#39;endpoint `/system/jobs` nell&#39;API [!DNL Real-Time Customer Profile], seguire i passaggi descritti nella [guida dell&#39;endpoint dei processi di sistema del profilo](profile-system-jobs.md).

## Aggiornare gli attributi dei profili {#update-profile}

A volte può essere necessario aggiornare i dati nell’archivio profili della tua organizzazione. Ad esempio, potrebbe essere necessario correggere i record o modificare un valore di attributo. Questa operazione può essere eseguita tramite l’acquisizione in batch e richiede un set di dati abilitato per il profilo configurato con un tag upsert. Per ulteriori informazioni su come configurare un set di dati per gli aggiornamenti degli attributi, consulta l&#39;esercitazione per [abilitare un set di dati per Profilo e upsert](../../catalog/datasets/enable-upsert.md).

## Passaggi successivi {#next-steps}

Per iniziare a effettuare chiamate utilizzando l&#39;API [!DNL Real-Time Customer Profile], leggere la [guida introduttiva](getting-started.md), quindi selezionare una delle guide degli endpoint per scoprire come utilizzare endpoint specifici correlati a [!DNL Profile]. Per utilizzare i dati di [!DNL Profile] tramite l&#39;interfaccia utente di [!DNL Experience Platform], fare riferimento alla [Guida utente del profilo cliente in tempo reale](../ui/user-guide.md).
