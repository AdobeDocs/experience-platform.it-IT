---
title: Guida all’API della query di audit
description: Audit Query è un’API RESTful che consente agli sviluppatori di vedere chi ha eseguito le azioni in Adobe Experience Platform.
source-git-commit: 5b3459711f41430977f9d7b06f8b35801739207c
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 2%

---

# Guida dell’API di [!DNL Audit Query]

La [!DNL Audit Query] API fornisce endpoint che consentono di recuperare e monitorare programmaticamente i dati degli eventi per varie funzioni di Adobe Experience Platform. Gli endpoint sono descritti di seguito. Visita [guida introduttiva](./getting-started.md) per informazioni importanti sulle intestazioni richieste, sulla lettura di chiamate API di esempio e altro ancora.

Per visualizzare tutti gli endpoint disponibili e le operazioni CRUD, visita il [[!DNL Audit Query] Swagger API](https://www.adobe.io/experience-platform-apis/references/audit-query/).

## Eventi

Gli eventi di controllo forniscono informazioni approfondite sulle azioni degli utenti in Platform, tra cui il tipo di azione, la data e l’ora, l’ID e-mail dell’utente che ha eseguito l’azione e gli attributi aggiuntivi relativi al tipo di azione per varie funzioni in Adobe Experience Platform. Per informazioni su come recuperare le metriche utilizzando l’API, consulta la sezione [guida endpoint eventi](./events.md).

## Esporta

L’esportazione di controllo consente di recuperare i dati degli eventi specificando gli eventi da recuperare nel payload. Per informazioni su come recuperare le metriche utilizzando l’API, consulta la sezione [guida all’endpoint per l’esportazione](./export.md).
