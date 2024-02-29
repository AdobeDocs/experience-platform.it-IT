---
title: Guida all’API di Privacy Service
description: Scopri come utilizzare l’API Privacy Service per gestire in modo programmatico i processi relativi alla privacy per le applicazioni Adobe Experience Cloud supportate.
role: Developer
exl-id: 665466ac-2447-4a9d-a8cf-62092c09e431
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 4%

---

# Guida dell’API di [!DNL Privacy Service]

L’API Privacy Service fornisce diversi endpoint che consentono di gestire in modo programmatico i processi relativi alla privacy per l’organizzazione. Questi endpoint sono descritti di seguito. Per informazioni dettagliate, consulta le guide dei singoli endpoint e fai riferimento a [guida introduttiva](./getting-started.md) per informazioni importanti sulle intestazioni richieste, leggi le chiamate API di esempio e altro ancora.

>[!NOTE]
>
>Questa guida illustra come utilizzare [!DNL Privacy Service] API. Per informazioni dettagliate su come utilizzare l’interfaccia utente, consulta [Panoramica dell’interfaccia utente di Privacy Service](../ui/overview.md).

Per visualizzare tutti gli endpoint disponibili e le operazioni CRUD, visitare il [Riferimento API di Privacy Service](https://www.adobe.io/experience-platform-apis/references/privacy-service/).

## Processi di privacy

Quando Privacy Service riceve una richiesta di accesso o di cancellazione dei dati personali di un soggetto, crea dei lavori sulla privacy per soddisfare tale richiesta. Ogni processo di privacy contiene informazioni di identità relative all’interessato, metadati sul prodotto Adobe Experience Cloud a cui si applica il processo e lo stato di elaborazione del processo.

Il `/jobs` l’endpoint ti consente di creare e recuperare processi sulla privacy per la tua organizzazione. Per informazioni su come utilizzare questo endpoint, consulta [guida dell’endpoint &quot;privacy jobs&quot;](./privacy-jobs.md).

## Consenso

Alcune normative richiedono il consenso esplicito del cliente prima che i suoi dati personali possano essere raccolti. Il `/consent` L’endpoint ti consente di elaborare le richieste di consenso dei clienti e di integrarle nel flusso di lavoro sulla privacy. Consulta la [guida dell’endpoint di consenso](./consent.md) per ulteriori informazioni.

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l’API Privacy Service, leggi la sezione [guida introduttiva](./getting-started.md) quindi seleziona una delle guide degli endpoint per scoprire come utilizzare endpoint specifici.
