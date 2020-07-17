---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guida per lo sviluppatore di API profilo cliente in tempo reale
topic: guide
translation-type: tm+mt
source-git-commit: f910351d49de9c4a18a444b99b7f102f4ce3ed5b
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] Guida per gli sviluppatori di API

[!DNL Real-time Customer Profile] consente di visualizzare una visualizzazione olistica di ogni singolo cliente all&#39;interno  Adobe Experience Platform. [!DNL Profile] consente di consolidare dati cliente diversi da canali diversi, come online, offline, CRM e dati di terze parti, in una visualizzazione unificata che offre un account con marca temporale utilizzabile per ogni interazione con il cliente.

L&#39; [!DNL Real-time Customer Profile] API include più endpoint, descritti di seguito. Per informazioni dettagliate, consultate le singole guide degli endpoint e la guida [](getting-started.md) introduttiva per informazioni importanti sulle intestazioni richieste, sulla lettura di chiamate API di esempio e altro ancora.

Per visualizzare tutti gli endpoint disponibili e le operazioni CRUD, fare riferimento al swagger [Riferimento API profilo cliente in tempo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)reale.

## (Alfa) Attributi calcolati

>[!IMPORTANT]
>
>
>La funzionalità dell&#39;attributo calcolato è in alfa e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

Gli attributi calcolati consentono di calcolare automaticamente il valore dei campi in base ad altri valori, calcoli ed espressioni. Gli attributi calcolati operano a livello di profilo, il che significa che puoi aggregare i valori per tutti i record ed eventi. Ogni attributo calcolato contiene un&#39;espressione, o &quot;regola&quot;, che valuta i dati in arrivo e memorizza il valore risultante in un attributo di profilo o in un evento. Questi calcoli consentono di rispondere facilmente a domande relative a cose come il valore di acquisto del ciclo di vita, il tempo tra acquisti o il numero di aperture di applicazioni, senza che sia necessario eseguire manualmente calcoli complessi ogni volta che le informazioni sono necessarie. Potete creare, visualizzare, modificare ed eliminare gli attributi calcolati utilizzando l&#39; `config/computedAttributes` endpoint. Per informazioni sull&#39;utilizzo di questo endpoint, visita la guida [all&#39;endpoint degli attributi](computed-attributes.md)calcolati.

## Proiezioni Edge

 Adobe Experience Platform consente la personalizzazione in tempo reale delle esperienze dei clienti, rendendo i dati facilmente accessibili su server situati strategicamente denominati &quot;edge&quot;. L&#39; [!DNL Real-time Customer Profile] API fornisce gli endpoint per lavorare con i bordi attraverso i componenti denominati &quot;proiezioni&quot;. Ciò include configurazioni di proiezione per determinare quali dati proiettare su ciascun bordo, nonché destinazioni di proiezione per definire dove indirizzare una proiezione. Per informazioni dettagliate sull&#39;utilizzo delle proiezioni dei bordi, visitate la guida [alle configurazioni di](edge-projections.md)proiezione e agli endpoint delle destinazioni.

## Entità (accesso profilo) {#entities}

Attraverso  Adobe Experience Platform è possibile accedere [!DNL Real-time Customer Profile] ai dati utilizzando RESTful APIs o l&#39;interfaccia utente. Per informazioni su come accedere alle entità, più comunemente note come &quot;profili&quot;, mediante l&#39;API, segui i passaggi descritti nella guida [all&#39;endpoint](entities.md)entità. Per accedere ai profili utilizzando l&#39; [!DNL Platform] interfaccia utente, consulta la guida [utente relativa al](../ui/user-guide.md)profilo.

## Unisci criteri

Quando si uniscono dati da più origini in [!DNL Experience Platform], i criteri di unione sono le regole che [!DNL Platform] utilizzano per determinare in che modo i dati verranno assegnati priorità e quali dati verranno combinati per creare singoli profili cliente. Utilizzando l&#39; [!DNL Real-time Customer Profile] API, è possibile creare nuovi criteri di unione, gestire i criteri esistenti e impostare un criterio di unione predefinito per l&#39;organizzazione. Per ulteriori informazioni sull&#39;utilizzo dei criteri di unione tramite l&#39;API, consultare la guida [all&#39;endpoint dei criteri di](merge-policies.md)unione.

Per una guida all&#39;utilizzo dei criteri di unione nell&#39; [!DNL Platform] interfaccia utente, consultate la guida [utente](../ui/merge-policies.md)Unisci criteri.

## Processi del sistema di profili

I dati acquisiti [!DNL Platform] vengono memorizzati sia nell&#39;archivio [!DNL Data Lake] che nell&#39;archivio [!DNL Real-time Customer Profile] dati. Talvolta potrebbe essere necessario eliminare un set di dati o un batch dallo [!DNL Profile] store per rimuovere i dati non più richiesti o aggiunti per errore. Ciò richiede l&#39;utilizzo dell&#39;API per creare un [!DNL Profile System Job], noto come &quot;[!DNL delete request]&quot;, che può anche essere, modificato, monitorato o eliminato, se necessario. Per informazioni su come gestire le richieste di eliminazione tramite l&#39; `/system/jobs` endpoint nell&#39; [!DNL Real-time Customer Profile] API, segui i passaggi descritti nella guida [all&#39;endpoint dei processi del sistema di](profile-system-jobs.md)profilo.

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l&#39; [!DNL Real-time Customer Profile] API, leggi la guida [introduttiva e seleziona una delle guide degli endpoint per apprendere come utilizzare endpoint specifici](getting-started.md) [!DNL Profile]correlati. Per ulteriori informazioni sull’utilizzo [!DNL Profile] dei dati nell’ [!DNL Platform] interfaccia utente, consulta la guida [utente Profilo cliente](../ui/user-guide.md)in tempo reale.