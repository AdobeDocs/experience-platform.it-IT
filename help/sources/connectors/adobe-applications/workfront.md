---
keywords: Experience Platform;home;argomenti popolari;
title: (Beta) Origine Adobe Workfront
description: Adobe Workfront è un’applicazione di marketing per la gestione dell’intero ciclo di vita del lavoro, tutto in un’unica posizione. Workfront include strumenti di reporting e analisi che puoi utilizzare per comprendere meglio e ottimizzare il flusso di lavoro nella tua organizzazione.
exl-id: ea714278-d84d-4929-9a34-81fc5fb70871
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 1%

---

# (Beta) Origine Adobe Workfront

>[!NOTE]
>
>Il codice sorgente di Adobe Workfront è in versione beta. Consulta la [Panoramica sulle origini](../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di connettori con etichetta beta.

Adobe Workfront è un’applicazione di marketing per la gestione dell’intero ciclo di vita del lavoro, tutto in un’unica posizione. Workfront include strumenti di reporting e analisi che puoi utilizzare per comprendere meglio e ottimizzare il flusso di lavoro nella tua organizzazione.

L’integrazione di Workfront con il catalogo delle origini di Adobe Experience Platform consente di inserire in Experience Platform i dati Workfront ed eseguire casi di utilizzo quali:

* Combina i record di lavoro con dati di terze parti.
* Applicare analisi cronologiche e di serie temporali ai record di lavoro.
* Accedere ai record di lavoro tramite strumenti di business intelligence di terze parti come [!DNL PowerBI].
* Eseguire query sui dati di lavoro utilizzando SQL standard.

I seguenti elementi di lavoro e i relativi attributi corrispondenti sono idonei per l’inclusione in Experience Platform tramite l’origine Workfront:

* Portfolio
* Programma
* Progetto
* Attività
* Attività operativa (problemi)
* Utente

La sorgente Workfront invia in streaming tutti i nuovi aggiornamenti a questi attributi e restituisce fino a un anno di eventi di modifica storici. Una volta inseriti i dati Workfront in un set di dati di Platform, puoi utilizzare [Servizio query](../../../query-service/home.md) e altri strumenti per analizzare ulteriormente o unire i dati relativi al lavoro con altri set di dati, in base alle esigenze.

## Connettere Workfront a Platform tramite l’interfaccia utente

Per istruzioni dettagliate su come importare i dati Workfront in Platform, consulta la guida su [creazione di una connessione sorgente per portare i dati Workfront in Platform](../../tutorials/ui/create/adobe-applications/workfront.md).
