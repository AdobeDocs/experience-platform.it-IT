---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guida per lo sviluppatore di API profilo cliente in tempo reale
topic: guide
translation-type: tm+mt
source-git-commit: c0b059d6654a98b74be5bc6a55f360c4dc2f216b
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 0%

---


# Guida per lo sviluppatore di API profilo cliente in tempo reale

Il profilo cliente in tempo reale consente di visualizzare una visione olistica di ogni singolo cliente all&#39;interno  Adobe Experience Platform. Il profilo consente di consolidare diversi dati dei clienti da più canali, come online, offline, CRM e dati di terze parti, in una visualizzazione unificata che offre un account con marca temporale utilizzabile per ogni interazione con il cliente.

L&#39;API del profilo cliente in tempo reale include più endpoint, descritti di seguito. Per informazioni dettagliate, consultate le singole guide degli endpoint e la guida [](getting-started.md) introduttiva per informazioni importanti sulle intestazioni richieste, sulla lettura di chiamate API di esempio e altro ancora.

Per visualizzare tutti gli endpoint disponibili e le operazioni CRUD, fare riferimento al swagger [Riferimento API profilo cliente in tempo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)reale.

## (Alfa) Attributi calcolati

>[!IMPORTANT]
>
>
>La funzionalità dell&#39;attributo calcolato è in alfa e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

Gli attributi calcolati consentono di calcolare automaticamente il valore dei campi in base ad altri valori, calcoli ed espressioni. Gli attributi calcolati operano a livello di profilo, il che significa che puoi aggregare i valori per tutti i record ed eventi. Ogni attributo calcolato contiene un&#39;espressione, o &quot;regola&quot;, che valuta i dati in arrivo e memorizza il valore risultante in un attributo di profilo o in un evento. Questi calcoli consentono di rispondere facilmente a domande relative a cose come il valore di acquisto del ciclo di vita, il tempo tra acquisti o il numero di aperture di applicazioni, senza che sia necessario eseguire manualmente calcoli complessi ogni volta che le informazioni sono necessarie. Potete creare, visualizzare, modificare ed eliminare gli attributi calcolati utilizzando l&#39; `config/computedAttributes` endpoint. Per informazioni sull&#39;utilizzo di questo endpoint, visita la guida [all&#39;endpoint degli attributi](computed-attributes.md)calcolati.

## Proiezioni Edge

 Adobe Experience Platform consente la personalizzazione in tempo reale delle esperienze dei clienti, rendendo i dati facilmente accessibili su server situati strategicamente denominati &quot;edge&quot;. L&#39;API del profilo cliente in tempo reale fornisce gli endpoint per l&#39;utilizzo dei bordi tramite componenti denominati &quot;proiezioni&quot;. Ciò include configurazioni di proiezione per determinare quali dati proiettare su ciascun bordo, nonché destinazioni di proiezione per definire dove indirizzare una proiezione. Per informazioni dettagliate sull&#39;utilizzo delle proiezioni dei bordi, visitate la guida [alle configurazioni di](edge-projections.md)proiezione e agli endpoint delle destinazioni.

## Entità (accesso profilo) {#entities}

Attraverso  Adobe Experience Platform puoi accedere ai dati del profilo cliente in tempo reale utilizzando le API RESTful o l&#39;interfaccia utente. Per informazioni su come accedere alle entità, più comunemente note come &quot;profili&quot;, mediante l&#39;API, segui i passaggi descritti nella guida [all&#39;endpoint](entities.md)entità. Per accedere ai profili utilizzando l’interfaccia utente di Platform, consulta la guida [utente relativa al](../ui/user-guide.md)profilo.

## Unisci criteri

Quando si uniscono dati da più origini in  Experience Platform, i criteri di unione sono le regole utilizzate da Platform per determinare in che modo i dati verranno classificati in ordine di priorità e quali dati verranno combinati per creare singoli profili cliente. Utilizzando l&#39;API Profilo cliente in tempo reale, puoi creare nuovi criteri di unione, gestire i criteri esistenti e impostare un criterio di unione predefinito per la tua organizzazione. Per ulteriori informazioni sull&#39;utilizzo dei criteri di unione tramite l&#39;API, consultare la guida [all&#39;endpoint dei criteri di](merge-policies.md)unione.

Per una guida all&#39;utilizzo dei criteri di unione nell&#39;interfaccia utente di Platform, consultate la guida [utente](../ui/merge-policies.md)Unisci criteri.

## Processi del sistema di profili

I dati acquisiti in Platform sono memorizzati nel Data Lake e nell&#39;archivio dati del profilo cliente in tempo reale. Talvolta potrebbe essere necessario eliminare un set di dati o un batch dall&#39;archivio dei profili per rimuovere i dati che non sono più necessari o che sono stati aggiunti per errore. Ciò richiede l’utilizzo dell’API per creare un processo di sistema dei profili, noto come &quot;richiesta di eliminazione&quot;, che può anche essere, modificato, monitorato o eliminato se necessario. Per informazioni su come gestire le richieste di eliminazione tramite l&#39; `/system/jobs` endpoint nell&#39;API Profilo cliente in tempo reale, segui i passaggi descritti nella guida [all&#39;endpoint dei processi del sistema di](profile-system-jobs.md)profilo.

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l&#39;API Profilo cliente in tempo reale, leggi la guida [](getting-started.md) introduttiva e seleziona una delle guide dell&#39;endpoint per scoprire come utilizzare endpoint specifici correlati al profilo. Per ulteriori informazioni sull’utilizzo dei dati di profilo nell’interfaccia utente di Platform, consulta la guida [utente Profilo cliente](../ui/user-guide.md)in tempo reale.