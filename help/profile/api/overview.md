---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;unified profile;Unified Profile;unified;Profile;rtcp;enable profile;Enable profile
solution: Adobe Experience Platform
title: Guida per lo sviluppatore di API profilo cliente in tempo reale
topic: guide
description: L'API del profilo cliente in tempo reale include più endpoint, descritti di seguito.
translation-type: tm+mt
source-git-commit: 04efbf63741ef39bbf0b22795be74087f1f7c595
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] Guida per gli sviluppatori di API

[!DNL Real-time Customer Profile] consente di visualizzare una visualizzazione olistica di ogni singolo cliente all&#39;interno di Adobe Experience Platform. [!DNL Profile] consente di consolidare dati cliente diversi da canali diversi, come online, offline, CRM e dati di terze parti, in una visualizzazione unificata che offre un account con marca temporale utilizzabile per ogni interazione con il cliente.

L&#39; [!DNL Real-time Customer Profile] API include più endpoint, descritti di seguito. Per informazioni dettagliate, consultate le singole guide degli endpoint e la guida [](getting-started.md) introduttiva per informazioni importanti sulle intestazioni richieste, sulla lettura di chiamate API di esempio e altro ancora.

Per visualizzare tutti gli endpoint disponibili e le operazioni CRUD, visita lo swagger [Riferimento API profilo cliente in tempo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)reale.

Per una guida all’utilizzo [!DNL Real-time Customer Profile] dei dati nell’ [!DNL Experience Platform] interfaccia utente, consulta la guida [utente](../ui/user-guide.md)Profilo.

## (Alfa) Attributi calcolati {#computed-attributes}

>[!IMPORTANT]
>
>La funzionalità dell&#39;attributo calcolato è in alfa e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

Gli attributi calcolati consentono di calcolare automaticamente il valore dei campi in base ad altri valori, calcoli ed espressioni. Gli attributi calcolati operano a livello di profilo, il che significa che puoi aggregare i valori per tutti i record ed eventi. Ogni attributo calcolato contiene un&#39;espressione, o &quot;regola&quot;, che valuta i dati in arrivo e memorizza il valore risultante in un attributo di profilo o in un evento. Questi calcoli consentono di rispondere facilmente a domande relative a cose come il valore di acquisto del ciclo di vita, il tempo tra acquisti o il numero di aperture di applicazioni, senza che sia necessario eseguire manualmente calcoli complessi ogni volta che le informazioni sono necessarie. Potete creare, visualizzare, modificare ed eliminare gli attributi calcolati utilizzando l&#39; `config/computedAttributes` endpoint. Per informazioni sull&#39;utilizzo di questo endpoint, visita la guida [all&#39;endpoint degli attributi](computed-attributes.md)calcolati.

## Proiezioni Edge {#edge-projections}

Adobe Experience Platform consente di personalizzare in tempo reale le esperienze dei clienti rendendo i dati facilmente accessibili su server situati in una posizione strategica denominati &quot;edge&quot;. L&#39; [!DNL Real-time Customer Profile] API fornisce gli endpoint per lavorare con i bordi attraverso i componenti denominati &quot;proiezioni&quot;. Ciò include configurazioni di proiezione per determinare quali dati proiettare su ciascun bordo, nonché destinazioni di proiezione per definire dove indirizzare una proiezione. Per informazioni dettagliate sull&#39;utilizzo delle proiezioni dei bordi, visitate la guida [alle configurazioni di](edge-projections.md)proiezione e agli endpoint delle destinazioni.

## Entità ([!DNL Profile] accesso) {#entities}

Tramite Adobe Experience Platform è possibile accedere [!DNL Real-time Customer Profile] ai dati utilizzando le RESTful API o l&#39;interfaccia utente. Per informazioni su come accedere alle entità, più comunemente note come &quot;profili&quot;, mediante l&#39;API, segui i passaggi descritti nella guida [all&#39;endpoint](entities.md)entità. Per accedere ai profili utilizzando l&#39; [!DNL Platform] interfaccia utente, consulta la guida [utente relativa al](../ui/user-guide.md)profilo.

## Processi di esportazione ([!DNL Profile] esportazione) {#profile-export}

[!DNL Real-time Customer Profile] i dati possono essere esportati in un set di dati per un’ulteriore elaborazione, ad esempio l’esportazione di segmenti di pubblico per l’attivazione o gli attributi di profilo per il reporting. I processi di esportazione per i segmenti di pubblico fanno parte dell&#39; [!DNL Adobe Experience Platform Segmentation Service] API. Per ulteriori informazioni, consultate la guida [all&#39;endpoint dei processi di esportazione della](../../profile/api/export-jobs.md) segmentazione. Per istruzioni dettagliate su come creare e gestire i processi di esportazione per gli attributi di profilo, consultate la guida [all’endpoint dei processi di](export-jobs.md)esportazione.

## Unisci criteri {#merge-policies}

Quando si uniscono dati da più origini in [!DNL Experience Platform], i criteri di unione sono le regole che [!DNL Platform] utilizzano per determinare in che modo i dati verranno assegnati priorità e quali dati verranno combinati per creare singoli profili cliente. Utilizzando l&#39; [!DNL Real-time Customer Profile] API, è possibile creare nuovi criteri di unione, gestire i criteri esistenti e impostare un criterio di unione predefinito per l&#39;organizzazione. Per ulteriori informazioni sull&#39;utilizzo dei criteri di unione tramite l&#39;API, consultare la guida [all&#39;endpoint dei criteri di](merge-policies.md)unione.

Per una guida all&#39;utilizzo dei criteri di unione tramite l&#39; [!DNL Platform] interfaccia utente, vedere la guida [utente dei criteri di](../ui/merge-policies.md)unione.

## Stato dell’anteprima del campione ([!DNL Profile] anteprima) {#profile-preview}

Poiché i dati attivati per il profilo vengono trasferiti  Experience Platform, vengono memorizzati nell&#39;archivio dati del profilo. Con l’aumento o la diminuzione del numero di record nell’archivio profili, viene eseguito un processo di esempio che include informazioni sul numero di frammenti di profilo e di profili uniti presenti nell’archivio dati. Utilizzando l&#39;API Profile è possibile visualizzare in anteprima l&#39;esempio di successo più recente, nonché distribuire il profilo di elenco per set di dati e per namespace di identità. Per iniziare a utilizzare l’ `/profilepreviewstatus` endpoint, consultate la guida [all’endpoint di stato dell’esempio di](preview-sample-status.md)anteprima.

## Processi del sistema di profili {#profile-system-jobs}

I dati acquisiti [!DNL Platform] vengono memorizzati sia nell&#39;archivio [!DNL Data Lake] che nell&#39;archivio [!DNL Real-time Customer Profile] dati. Talvolta potrebbe essere necessario eliminare un set di dati o un batch dallo [!DNL Profile] store per rimuovere i dati non più richiesti o aggiunti per errore. Ciò richiede l&#39;utilizzo dell&#39;API per creare un [!DNL Profile System Job], noto come &quot;[!DNL delete request]&quot;, che può anche essere, modificato, monitorato o eliminato, se necessario. Per informazioni su come gestire le richieste di eliminazione tramite l&#39; `/system/jobs` endpoint nell&#39; [!DNL Real-time Customer Profile] API, segui i passaggi descritti nella guida [all&#39;endpoint dei processi del sistema di](profile-system-jobs.md)profilo.

## Passaggi successivi {#next-steps}

Per iniziare a effettuare chiamate utilizzando l&#39; [!DNL Real-time Customer Profile] API, leggi la guida [introduttiva e seleziona una delle guide degli endpoint per apprendere come utilizzare endpoint specifici](getting-started.md) [!DNL Profile]correlati. Per utilizzare [!DNL Profile] i dati nell&#39; [!DNL Experience Platform] interfaccia utente, fare riferimento alla guida [utente Profilo cliente](../ui/user-guide.md)in tempo reale.