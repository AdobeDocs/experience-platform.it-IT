---
keywords: ' Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;profilo unificato;profilo unificato;unificato;profilo;rtcp;abilita profilo;Abilita profilo'
title: Guida per sviluppatori API profilo cliente in tempo reale
topic: guide
description: L'API Profilo cliente in tempo reale include più endpoint per l'esplorazione e l'utilizzo dei dati del profilo, tra cui la visualizzazione dei profili, la creazione e l'aggiornamento di criteri di unione, l'esportazione o il campionamento dei dati del profilo e l'eliminazione dei dati del profilo non più necessari o che sono stati aggiunti per errore.
translation-type: tm+mt
source-git-commit: 823d89ab37156e775a2879e3a2c91bfd911b83bb
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] Guida per gli sviluppatori di API

[!DNL Real-time Customer Profile] consente di visualizzare una visualizzazione olistica di ogni singolo cliente all&#39;interno di Adobe Experience Platform. [!DNL Profile] consente di consolidare dati cliente diversi da canali diversi, come online, offline, CRM e dati di terze parti, in una visualizzazione unificata che offre un account con marca temporale utilizzabile per ogni interazione con il cliente.

L&#39;API [!DNL Real-time Customer Profile] include più endpoint, descritti di seguito. Per informazioni dettagliate, visitate le singole guide degli endpoint e fate riferimento alla [guida introduttiva](getting-started.md) per informazioni importanti sulle intestazioni richieste, sulla lettura di chiamate API di esempio e altro ancora.

Per visualizzare tutti gli endpoint disponibili e le operazioni CRUD, visita il [swagger di riferimento API profilo cliente in tempo reale](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml).

Per una guida sull&#39;utilizzo dei dati [!DNL Real-time Customer Profile] nell&#39;interfaccia utente [!DNL Experience Platform], fare riferimento alla [Guida utente del profilo](../ui/user-guide.md).

## (Alfa) Attributi calcolati {#computed-attributes}

>[!IMPORTANT]
>
>La funzionalità dell&#39;attributo calcolato è in alfa e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

Gli attributi calcolati consentono di calcolare automaticamente il valore dei campi in base ad altri valori, calcoli ed espressioni. Gli attributi calcolati operano a livello di profilo, il che significa che puoi aggregare i valori per tutti i record ed eventi. Ogni attributo calcolato contiene un&#39;espressione, o &quot;regola&quot;, che valuta i dati in arrivo e memorizza il valore risultante in un attributo di profilo o in un evento. Questi calcoli consentono di rispondere facilmente a domande relative a cose come il valore di acquisto del ciclo di vita, il tempo tra acquisti o il numero di aperture di applicazioni, senza che sia necessario eseguire manualmente calcoli complessi ogni volta che le informazioni sono necessarie. È possibile creare, visualizzare, modificare ed eliminare gli attributi calcolati utilizzando l&#39;endpoint `config/computedAttributes`. Per informazioni sull&#39;utilizzo di questo endpoint, visitare la [guida dell&#39;endpoint degli attributi calcolati](computed-attributes.md).

## Proiezioni Edge {#edge-projections}

Adobe Experience Platform consente di personalizzare in tempo reale le esperienze dei clienti rendendo i dati facilmente accessibili su server situati in una posizione strategica denominati &quot;edge&quot;. L&#39;API [!DNL Real-time Customer Profile] fornisce gli endpoint per l&#39;utilizzo dei bordi tramite componenti denominati &quot;proiezioni&quot;. Ciò include configurazioni di proiezione per determinare quali dati proiettare su ciascun bordo, nonché destinazioni di proiezione per definire dove indirizzare una proiezione. Per informazioni dettagliate sull&#39;utilizzo delle proiezioni dei bordi, visitare la [guida alle configurazioni di proiezione e agli endpoint delle destinazioni](edge-projections.md).

## Entità ([!DNL Profile] accesso) {#entities}

Tramite Adobe Experience Platform è possibile accedere ai dati [!DNL Real-time Customer Profile] utilizzando le API RESTful o l&#39;interfaccia utente. Per informazioni su come accedere alle entità, più comunemente note come &quot;profili&quot;, utilizzando l&#39;API, segui i passaggi descritti nella guida [endpoint entità](entities.md). Per accedere ai profili utilizzando l&#39;interfaccia [!DNL Platform], fare riferimento alla [Guida utente del profilo](../ui/user-guide.md).

## Processi di esportazione ([!DNL Profile] esportazione) {#profile-export}

[!DNL Real-time Customer Profile] i dati possono essere esportati in un set di dati per un’ulteriore elaborazione, ad esempio l’esportazione di segmenti di pubblico per l’attivazione o gli attributi di profilo per il reporting. I processi di esportazione per i segmenti di pubblico fanno parte dell&#39;API [!DNL Adobe Experience Platform Segmentation Service]. Per ulteriori informazioni, leggere la guida [all&#39;endpoint dei processi di esportazione della segmentazione](../../profile/api/export-jobs.md). Per istruzioni dettagliate su come creare e gestire i processi di esportazione per gli attributi di profilo, visitare la [guida all&#39;endpoint dei processi di esportazione](export-jobs.md).

## Unisci criteri {#merge-policies}

Quando si uniscono dati da più origini in [!DNL Experience Platform], i criteri di unione sono le regole utilizzate da [!DNL Platform] per determinare in che modo i dati verranno classificati in ordine di priorità e quali dati verranno combinati per creare singoli profili cliente. Utilizzando l&#39;API [!DNL Real-time Customer Profile] è possibile creare nuovi criteri di unione, gestire i criteri esistenti e impostare un criterio di unione predefinito per l&#39;organizzazione. Per ulteriori informazioni sull&#39;utilizzo dei criteri di unione tramite l&#39;API, visitare la [guida dell&#39;endpoint dei criteri di unione](merge-policies.md).

Per una guida all&#39;utilizzo dei criteri di unione tramite l&#39;interfaccia utente [!DNL Platform], vedere la [guida utente dei criteri di unione](../ui/merge-policies.md).

## Anteprima dello stato del campione ([!DNL Profile] anteprima) {#profile-preview}

Poiché i dati attivati per il profilo vengono trasferiti  Experience Platform, vengono memorizzati nell&#39;archivio dati del profilo. Con l’aumento o la diminuzione del numero di record nell’archivio profili, viene eseguito un processo di esempio che include informazioni sul numero di frammenti di profilo e di profili uniti presenti nell’archivio dati. Utilizzando l&#39;API Profile è possibile visualizzare in anteprima l&#39;esempio di successo più recente, nonché distribuire il profilo di elenco per set di dati e per namespace di identità. Per iniziare a utilizzare l&#39;endpoint `/profilepreviewstatus`, fare riferimento alla [guida per l&#39;endpoint dello stato dell&#39;esempio ](preview-sample-status.md).

## Processi del sistema di profili {#profile-system-jobs}

I dati abilitati per il profilo acquisiti in [!DNL Platform] vengono memorizzati sia nell&#39; [!DNL Data Lake] che nell&#39; [!DNL Real-time Customer Profile] archivio dati. Talvolta potrebbe essere necessario eliminare un set di dati o un batch dallo store [!DNL Profile] per rimuovere i dati non più richiesti o che sono stati aggiunti per errore. Ciò richiede l&#39;utilizzo dell&#39;API per creare un [!DNL Profile System Job], noto anche come &quot;[!DNL delete request]&quot;, che può essere modificato, monitorato o eliminato se necessario. Per informazioni su come gestire le richieste di eliminazione utilizzando l&#39;endpoint `/system/jobs` nell&#39;API [!DNL Real-time Customer Profile], segui i passaggi descritti nella [guida dell&#39;endpoint dei processi del sistema di profilo](profile-system-jobs.md).

## Passaggi successivi {#next-steps}

Per iniziare a effettuare chiamate utilizzando l&#39;API [!DNL Real-time Customer Profile], leggi la [guida introduttiva](getting-started.md), quindi seleziona una delle guide dell&#39;endpoint per apprendere come utilizzare endpoint [!DNL Profile] specifici. Per utilizzare i dati [!DNL Profile] utilizzando l&#39;interfaccia utente [!DNL Experience Platform], fare riferimento alla [Guida utente del profilo cliente in tempo reale](../ui/user-guide.md).