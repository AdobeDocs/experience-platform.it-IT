---
title: Guida all’API per gli strumenti sandbox
description: Gli strumenti sandbox in Adobe Experience Platform consentono di esportare e importare un’istantanea delle configurazioni sandbox tra le sandbox.
exl-id: 4bcc095b-5db1-4824-8b7c-c2ea5a393b98
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 3%

---

# Guida API agli strumenti di [!DNL Sandbox]

L&#39;API per gli strumenti [!DNL Sandbox] fornisce diversi endpoint che consentono di esportare e importare snapshot tra le sandbox disponibili all&#39;interno dell&#39;organizzazione. Tutte le interazioni si verificano tramite endpoint HTTP. Prima di esportare un&#39;istantanea, nella sandbox di origine vengono verificati gli artefatti, ovvero gli oggetti contenuti in un pacchetto. Quando viene effettuata una richiesta di importazione, viene ottenuta e utilizzata come modello uno snapshot [!DNL Azure Blob] per produrre artefatti quasi simili per la sandbox di destinazione. Per un elenco degli oggetti e delle limitazioni supportati, consulta la documentazione [sandbox tooling](../ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling).

Questi endpoint sono descritti di seguito. Per informazioni dettagliate, consulta le guide dei singoli endpoint e fai riferimento alla [guida introduttiva](./getting-started.md) per informazioni importanti sulle intestazioni richieste, sulla lettura delle chiamate API di esempio e altro ancora.

## Pacchetti {#packages}

L’endpoint &quot;sandbox tooling packages&quot; consente di gestire i pacchetti. Il pacchetto di strumenti sandbox è una raccolta di definizioni di artefatti che includono ID pacchetto, nome, descrizione, ID organizzazione e ID creatore. Per ulteriori informazioni sull&#39;utilizzo dei pacchetti nell&#39;API, consulta la guida dell&#39;endpoint [packages](./packages.md).

## Strumenti {#tools}

L’endpoint &quot;sandbox tooling tools&quot; consente di recuperare in modo indipendente i dati JSON del processo. Per ulteriori informazioni sul recupero dei dati JSON del processo nell&#39;API, consulta la [guida dell&#39;endpoint &quot;tools&quot;](./tools.md).

## Passaggi successivi {#next-steps}

Per iniziare a effettuare chiamate utilizzando l&#39;API degli strumenti sandbox, leggi la [guida introduttiva](./getting-started.md), quindi seleziona una delle guide degli endpoint per scoprire come utilizzare endpoint specifici.
