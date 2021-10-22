---
title: Guida all’API di Privacy Service
description: Scopri come utilizzare l’API di Privacy Service per gestire in modo programmatico i processi relativi alla privacy per le applicazioni Adobe Experience Cloud supportate.
source-git-commit: 196147e7691010707953561c110a3934fec8ba1b
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 3%

---

# Guida dell’API di [!DNL Privacy Service]

L’API di Privacy Service fornisce diversi endpoint che ti consentono di gestire in modo programmatico i processi relativi alla privacy per la tua organizzazione. Questi endpoint sono descritti di seguito. Per informazioni dettagliate, visita le singole guide dell’endpoint e fai riferimento alla sezione [guida introduttiva](./getting-started.md) per informazioni importanti sulle intestazioni richieste, sulla lettura di chiamate API di esempio e altro ancora.

>[!NOTE]
>
>Questa guida illustra come utilizzare i [!DNL Privacy Service] API. Per informazioni dettagliate sull’utilizzo dell’interfaccia utente, consulta la [Panoramica dell’interfaccia utente di Privacy Service](../ui/overview.md).

Per visualizzare tutti gli endpoint disponibili e le operazioni CRUD, visita il [Riferimento API di Privacy Service](https://www.adobe.io/experience-platform-apis/references/privacy-service/).

## Lavori sulla privacy

Quando Privacy Service riceve una richiesta di accesso o di cancellazione dei dati personali di un soggetto, il sistema crea dei processi relativi alla privacy per soddisfare tale richiesta. Ogni processo di privacy contiene informazioni di identità relative alla persona interessata, metadati sul prodotto Adobe Experience Cloud a cui si applica il processo e lo stato di elaborazione del processo.

La `/jobs` l’endpoint ti consente di creare e recuperare processi relativi alla privacy per la tua organizzazione. Per informazioni su come utilizzare questo endpoint, consulta la sezione [guida all’endpoint per i processi di privacy](./privacy-jobs.md).

## Consenso

Alcune normative richiedono un consenso esplicito dei clienti prima che i loro dati personali possano essere raccolti. La `/consent` L’endpoint ti consente di elaborare le richieste di consenso dei clienti e di integrarle nel flusso di lavoro per la privacy. Consulta la sezione [guida all’endpoint del consenso](./consent.md) per saperne di più.

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l’API di Privacy Service, leggi la [guida introduttiva](./getting-started.md) quindi seleziona una delle guide dell’endpoint per scoprire come utilizzare endpoint specifici.
