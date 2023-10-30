---
title: Guida all’API per gli strumenti sandbox
description: Gli strumenti sandbox in Adobe Experience Platform consentono di esportare e importare un’istantanea delle configurazioni sandbox tra le sandbox.
exl-id: 4bcc095b-5db1-4824-8b7c-c2ea5a393b98
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 3%

---

# [!DNL Sandbox] guida all’API per strumenti

Il [!DNL Sandbox] L’API per strumenti fornisce diversi endpoint che consentono di esportare e importare snapshot tra le sandbox disponibili all’interno dell’organizzazione. Tutte le interazioni si verificano tramite endpoint HTTP. Prima di esportare un&#39;istantanea, nella sandbox di origine vengono verificati gli artefatti, ovvero gli oggetti contenuti in un pacchetto. Quando viene effettuata una richiesta di importazione, viene [!DNL Azure Blob] l’istantanea viene ottenuta e utilizzata come modello per produrre artefatti quasi simili per la sandbox di destinazione. Consulta la [strumenti sandbox](../ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling) per un elenco di oggetti e limitazioni supportati.

Questi endpoint sono descritti di seguito. Per informazioni dettagliate, consulta le guide dei singoli endpoint e fai riferimento a [guida introduttiva](./getting-started.md) per informazioni importanti sulle intestazioni richieste, leggi le chiamate API di esempio e altro ancora.

## Pacchetti {#packages}

L’endpoint &quot;sandbox tooling packages&quot; consente di gestire i pacchetti. Il pacchetto di strumenti sandbox è una raccolta di definizioni di artefatti che includono ID pacchetto, nome, descrizione, ID organizzazione e ID creatore. Consulta la [guida dell’endpoint &quot;packages&quot;](./packages.md) per ulteriori informazioni sull’utilizzo dei pacchetti nell’API.

## Strumenti {#tools}

L’endpoint &quot;sandbox tooling tools&quot; consente di recuperare in modo indipendente i dati JSON del processo. Consulta la [guida dell’endpoint &quot;tools&quot;](./tools.md) per ulteriori informazioni sul recupero dei dati JSON del processo nell’API.

## Passaggi successivi {#next-steps}

Per iniziare a effettuare chiamate utilizzando l’API degli strumenti sandbox, leggi la [guida introduttiva](./getting-started.md) quindi seleziona una delle guide degli endpoint per scoprire come utilizzare endpoint specifici.
