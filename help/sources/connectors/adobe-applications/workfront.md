---
keywords: Experience Platform;home;argomenti popolari;
title: Origine Adobe Workfront
description: Adobe Workfront è un’applicazione di marketing work management che consente di gestire l’intero ciclo di vita del lavoro in un’unica posizione. Workfront include strumenti di reporting e analisi che puoi utilizzare per comprendere e ottimizzare meglio il flusso di lavoro all’interno della tua organizzazione.
source-git-commit: 99741a3be4d50d1a812e945483c9ed1577a0a999
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 1%

---

# Origine Adobe Workfront

Adobe Workfront è un’applicazione di marketing work management che consente di gestire l’intero ciclo di vita del lavoro in un’unica posizione. Workfront include strumenti di reporting e analisi che puoi utilizzare per comprendere e ottimizzare meglio il flusso di lavoro all’interno della tua organizzazione.

L’integrazione di Workfront con il catalogo sorgenti Adobe Experience Platform consente di inserire i dati Workfront in un Experience Platform ed eseguire casi d’uso come:

* Combinare i record di lavoro con dati di terze parti.
* Applicare analisi storiche e serie temporali ai record di lavoro.
* Accedere ai record di lavoro tramite strumenti di business intelligence di terze parti come [!DNL PowerBI].
* Eseguire query sui dati di lavoro utilizzando SQL standard.

I seguenti elementi di lavoro e i relativi attributi possono essere inclusi nell’Experience Platform tramite l’origine Workfront:

* Portfolio
* Programma
* Progetto
* Attività
* Attività operativa (problemi)
* Utente

La sorgente Workfront invia in streaming tutti i nuovi aggiornamenti a questi attributi e in modo da eseguire il backfill fino a un anno di eventi di cambiamento storico. Una volta che i dati di Workfront si trovano in un set di dati di Platform, puoi utilizzare [Servizio query](../../../query-service/home.md) e altri strumenti per analizzare ulteriormente o unire i dati relativi al lavoro con altri set di dati, se necessario.

## Collegare Workfront a Platform tramite l’interfaccia utente

Per istruzioni dettagliate su come trasferire i dati di Workfront a Platform, consulta la guida su [creazione di una connessione sorgente per trasferire i dati Workfront a Platform](../../tutorials/ui/create/adobe-applications/workfront.md).