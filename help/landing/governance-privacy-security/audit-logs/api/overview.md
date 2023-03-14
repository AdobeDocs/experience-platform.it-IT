---
title: Guida API per query di controllo
description: Audit Query è un’API RESTful che consente agli sviluppatori di vedere chi ha eseguito determinate azioni in Adobe Experience Platform.
exl-id: 9ed291c6-ff8b-4d9b-9fed-d1e3fa8f92fb
source-git-commit: c2c5778e0a3fff7f488ad7a672123c813cca59f1
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 2%

---

# Guida dell’API di [!DNL Audit Query]

Il [!DNL Audit Query] API fornisce endpoint che consentono di recuperare e monitorare in modo programmatico i dati dell’evento per varie funzioni di Adobe Experience Platform. Gli endpoint sono descritti di seguito. Visita il sito [guida introduttiva](./getting-started.md) per informazioni importanti sulle intestazioni richieste, leggi le chiamate API di esempio e altro ancora.

Per visualizzare tutti gli endpoint disponibili e le operazioni CRUD, visitare il [[!DNL Audit Query] Swagger API](https://www.adobe.io/experience-platform-apis/references/audit-query/).

## Eventi

Gli eventi di audit forniscono informazioni approfondite sulle azioni dell’utente in Platform, tra cui il tipo di azione, la data e l’ora, l’ID e-mail dell’utente che ha eseguito l’azione e gli attributi aggiuntivi relativi al tipo di azione per varie funzioni di Adobe Experience Platform. Per informazioni su come recuperare le metriche utilizzando l’API, consulta [guida dell’endpoint &quot;events&quot;](./events.md).

## Esporta

L’esportazione dei controlli consente di recuperare i dati degli eventi specificando gli eventi da recuperare nel payload. Per informazioni su come recuperare le metriche utilizzando l’API, consulta [guida dell’endpoint di esportazione](./export.md).
