---
title: Panoramica sulla pubblicazione
description: Scopri come pubblicare le modifiche apportate alle librerie dei codici di gestione dei tag in Adobe Experience Platform.
exl-id: 32eaad87-d7dc-4812-b546-a136511512fe
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 97%

---

# Panoramica sulla pubblicazione

>[!NOTE]
>
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Adobe Experience Platform consente di incorporare le modifiche al codice di gestione dei tag all’interno di singole librerie. Dal momento che più librerie possono essere sviluppate in parallelo da parte di team diversi, è importante seguire uno specifico processo basato su autorizzazioni al fine di unire le modifiche prima di inviarle all’ambiente di produzione.

Al livello di base, ogni libreria è soggetta al seguente processo di pubblicazione:

1. Crea una nuova libreria (o modifica una libreria esistente) in un ambiente di sviluppo.
1. Se necessario, verifica la funzionalità della libreria in un ambiente di staging.
1. Implementa la libreria nell’ambiente di produzione.

Considera una situazione di creazione di un nuovo evento “Vai alla cassa”, crea un elemento dati sulle entrate relativo a tale evento e modifica la configurazione dell’estensione Adobe Analytics per supportare il nuovo evento e il nuovo elemento dati. Puoi includere tutte queste modifiche in una nuova libreria e utilizzare il processo di pubblicazione per testarle, approvarle e pubblicarle come una singola unità.

Per una panoramica di alto livello del flusso di lavoro di pubblicazione delle librerie, con informazioni su come queste ereditano le risorse dalle build precedenti in base al loro stato di pubblicazione, consulta la [guida al flusso di pubblicazione](./publishing-flow.md).

Oltre al flusso di pubblicazione, per sviluppare e pubblicare efficacemente le librerie è importante comprendere anche diversi componenti e relazioni. La tabella seguente presenta i concetti chiave e fornisce i collegamenti alla relativa documentazione:

| Componente | Descrizione |
| --- | --- |
| Librerie | Una libreria è un insieme di istruzioni su come estensioni, elementi dati e regole interagiscono tra loro e con il sito web. Quando una libreria viene compilata per essere implementata in un ambiente, diventa una build.<br><br>Per informazioni su come creare, gestire e attivare le librerie nell’interfaccia utente, consulta la panoramica sulle [librerie](./libraries.md). |
| Build | Una build è una libreria compilata. Quando viene implementata in un ambiente, una build fornisce il set effettivo di file contenenti il codice che viene distribuito al browser di ogni utente che visualizza il sito.<br><br>Per informazioni su contenuti e formato, consulta la panoramica sulle [build](./builds.md). |
| Ambienti | Un ambiente di tag è un insieme di istruzioni di distribuzione che indica a Platform quale formato desideri creare e dove desideri che la build venga distribuita.<br><br>Per informazioni sui diversi tipi di ambienti, su come installare e configurare quelli esistenti e su come crearne di nuovi, consulta la panoramica sugli [ambienti](./environments.md). |
| Host | Un host rappresenta i dettagli di connessione di un ambiente per distribuire una build al sito web. Puoi scegliere di consentire ad Adobe di gestire l’hosting della build oppure puoi fornire i dati dei tuoi server di host.<br><br>Per informazioni su ciascuna opzione di hosting, consulta la panoramica sugli [host](./hosts/hosts-overview.md). |
| Codice lato client | Il codice lato client è il set di script inseriti nel codice sorgente per il sito o l’applicazione che indica a ogni dispositivo client dove recuperare la build. Il codice viene allegato a un ambiente e può cambiare quando si apportano modifiche alla sua configurazione.<br><br>Per ulteriori informazioni, consulta la sezione sui [codici da incorporare](./environments.md#embed-code) nella panoramica degli ambienti. |

## Passaggi successivi

In questo documento è stata fornita una panoramica dei vari componenti coinvolti nella pubblicazione delle librerie tag in Adobe Experience Platform. Per ulteriori informazioni sul processo di pubblicazione, consulta la documentazione accessibile dai collegamenti forniti in questa guida.
