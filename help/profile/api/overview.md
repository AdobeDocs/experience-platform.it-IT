---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;profilo unificato;profilo unificato;unificato;profilo;rtcp;abilita profilo;abilita profilo
title: Guida all’API del profilo cliente in tempo reale
description: L’API Profilo cliente in tempo reale consente agli sviluppatori di esplorare e lavorare con i dati del profilo, tra cui visualizzare i profili, creare e aggiornare criteri di unione, esportare o dati del profilo di esempio ed eliminare i dati del profilo che non sono più necessari o che sono stati aggiunti per errore. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
exl-id: ce39b95b-cff7-46cf-a14c-8203017c8826
source-git-commit: 77bf6f4634987900bea1280290e8049120bb8856
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 0%

---

# [!DNL Real-time Customer Profile] Guida all’API

[!DNL Real-time Customer Profile] ti consente di visualizzare una visualizzazione olistica di ciascuno dei tuoi clienti in Adobe Experience Platform. [!DNL Profile] consente di consolidare dati cliente diversi da più canali, come online, offline, CRM e dati di terze parti, in una visualizzazione unificata che offre un account actionable e timestamp di ogni interazione con il cliente.

L’ API [!DNL Real-time Customer Profile] include più endpoint, descritti di seguito. Per informazioni dettagliate, visita le singole guide dell&#39;endpoint e fai riferimento alla [guida introduttiva](getting-started.md) per informazioni importanti sulle intestazioni richieste, sulla lettura di chiamate API di esempio e altro ancora.

Per visualizzare tutti gli endpoint disponibili e le operazioni CRUD, visita il [swagger di riferimento API del profilo cliente in tempo reale](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml).

Per una guida all&#39;utilizzo dei dati [!DNL Real-time Customer Profile] nell&#39;interfaccia utente di [!DNL Experience Platform], fai riferimento alla [Guida utente del profilo](../ui/user-guide.md).

## (Alfa) Attributi calcolati {#computed-attributes}

>[!IMPORTANT]
>
>La funzionalità dell&#39;attributo calcolato è in alfa e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

Gli attributi calcolati sono funzioni utilizzate per aggregare dati a livello di evento in attributi a livello di profilo. Queste funzioni vengono calcolate automaticamente in modo che possano essere utilizzate tra segmentazione, attivazione e personalizzazione.

Ogni attributo calcolato contiene un&#39;espressione, o &quot;regola&quot;, che valuta i dati in arrivo e memorizza il valore risultante in un attributo di profilo. Questi calcoli consentono di rispondere facilmente a domande relative a fattori quali il valore di acquisto a vita, il tempo tra gli acquisti o il numero di aperture di applicazioni, senza che sia necessario eseguire manualmente calcoli complessi ogni volta che le informazioni sono necessarie. Questi valori di attributi calcolati possono quindi essere visualizzati in un profilo, utilizzati per creare un segmento o a cui è possibile accedere tramite diversi pattern di accesso.

Puoi creare, visualizzare, modificare ed eliminare gli attributi calcolati utilizzando l’endpoint `config/computedAttributes` . Per scoprire come utilizzare gli attributi calcolati, consulta la [panoramica sugli attributi calcolati](../computed-attributes/overview.md). Per le operazioni API, visita la [guida all&#39;endpoint API degli attributi calcolati](../computed-attributes/ca-api.md).

## Proiezioni del bordo {#edge-projections}

Adobe Experience Platform consente la personalizzazione in tempo reale delle esperienze dei clienti rendendo i dati facilmente accessibili su server situati in posizioni strategiche denominati &quot;edge&quot;. L’ API [!DNL Real-time Customer Profile] fornisce gli endpoint per l’utilizzo dei bordi tramite componenti denominati &quot;proiezioni&quot;. Ciò include configurazioni di proiezione per determinare quali dati proiettare su ciascun bordo, nonché destinazioni di proiezione per definire dove indirizzare una proiezione. Per informazioni dettagliate sulle operazioni con le proiezioni dei bordi, visita la [guida alle configurazioni di proiezione e agli endpoint delle destinazioni](edge-projections.md).

## Entità ([!DNL Profile] accesso) {#entities}

Tramite Adobe Experience Platform è possibile accedere ai dati [!DNL Real-time Customer Profile] utilizzando le API RESTful o l’interfaccia utente. Per scoprire come accedere alle entità, più comunemente definite &quot;profili&quot;, utilizzando l’API, segui i passaggi descritti nella [guida all’endpoint entità](entities.md). Per accedere ai profili utilizzando l&#39;interfaccia utente [!DNL Platform], fai riferimento alla [Guida utente al profilo](../ui/user-guide.md).

## Esportare lavori ([!DNL Profile] esportare) {#profile-export}

[!DNL Real-time Customer Profile] i dati possono essere esportati in un set di dati per un’ulteriore elaborazione, ad esempio per esportare segmenti di pubblico per l’attivazione o gli attributi di profilo per il reporting. I processi di esportazione per i segmenti di pubblico fanno parte dell’ [!DNL Adobe Experience Platform Segmentation Service] API. Per ulteriori informazioni, consulta la [guida all’endpoint per i processi di esportazione della segmentazione](../../profile/api/export-jobs.md) . Per istruzioni dettagliate su come creare e gestire i processi di esportazione per gli attributi di profilo, visita la [guida all&#39;endpoint dei processi di esportazione](export-jobs.md).

## Criteri di unione {#merge-policies}

Quando si riuniscono dati provenienti da più origini in [!DNL Experience Platform], i criteri di unione sono le regole utilizzate da [!DNL Platform] per determinare come assegnare la priorità ai dati e quali dati verranno combinati per creare profili cliente individuali. Utilizzando l&#39;API [!DNL Real-time Customer Profile] è possibile creare nuovi criteri di unione, gestire i criteri esistenti e impostare un criterio di unione predefinito per la propria organizzazione. Per ulteriori informazioni sull&#39;utilizzo dei criteri di unione tramite l&#39;API, visita la [guida all&#39;endpoint dei criteri di unione](merge-policies.md).

Per una guida all&#39;utilizzo dei criteri di unione tramite l&#39;interfaccia utente [!DNL Platform], vedere la [guida utente dei criteri di unione](../ui/merge-policies.md).

## Anteprima dello stato del campione ([!DNL Profile] anteprima) {#profile-preview}

Poiché i dati abilitati per Profilo vengono acquisiti in Experience Platform, vengono memorizzati nell’archivio dati Profilo. Man mano che il numero di record nell’archivio profili aumenta o diminuisce, viene eseguito un processo di esempio che include informazioni sul numero di frammenti di profilo e profili uniti nell’archivio dati. Utilizzando l’API di profilo puoi visualizzare in anteprima l’esempio di successo più recente, oltre a elencare la distribuzione dei profili per set di dati e per namespace di identità. Per iniziare a utilizzare l&#39;endpoint `/profilepreviewstatus`, fai riferimento alla [guida all&#39;endpoint per lo stato di esempio di anteprima](preview-sample-status.md).

## Processi del sistema di profili {#profile-system-jobs}

I dati abilitati per il profilo acquisiti in [!DNL Platform] vengono memorizzati sia nell’ [!DNL Data Lake] che nell’ archivio dati [!DNL Real-time Customer Profile]. A volte può essere necessario eliminare un set di dati o un batch dall&#39; archivio [!DNL Profile] per rimuovere i dati che non sono più necessari o che sono stati aggiunti per errore. Questo richiede l&#39;utilizzo dell&#39;API per creare un [!DNL Profile System Job], noto anche come &quot;[!DNL delete request]&quot;, che può essere modificato, monitorato o eliminato se necessario. Per informazioni su come lavorare con le richieste di eliminazione utilizzando l&#39;endpoint `/system/jobs` nell&#39;API [!DNL Real-time Customer Profile], segui i passaggi descritti nella [guida all&#39;endpoint dei processi del sistema di profilo](profile-system-jobs.md).

## Passaggi successivi {#next-steps}

Per iniziare a effettuare chiamate utilizzando l&#39;API [!DNL Real-time Customer Profile], leggi la [guida introduttiva](getting-started.md) , quindi seleziona una delle guide dell&#39;endpoint per scoprire come utilizzare endpoint specifici relativi a [!DNL Profile]. Per lavorare con i dati [!DNL Profile] utilizzando l&#39;interfaccia utente [!DNL Experience Platform], fai riferimento alla [Guida utente del profilo cliente in tempo reale](../ui/user-guide.md).
