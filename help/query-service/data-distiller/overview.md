---
title: Panoramica di Data Distiller
description: Riepilogo dei limiti di utilizzo di Data Distiller per i dati di Query Service in relazione all’adesione alla licenza.
source-git-commit: b3003cc62e8d3555b887a23f0614020bd2c5e81e
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---

# Panoramica di Data Distiller

Data Distiller è un pacchetto che include un sottoinsieme delle funzionalità di Adobe Experience Platform. Con Data Distiller è possibile eseguire la preparazione dei dati post-acquisizione (ad esempio la pulizia, la modellazione e la manipolazione) per casi d’uso in tempo reale del profilo del cliente o analitici eseguendo query batch in Query Service. L’utilizzo di Data Distiller dipende dall’adesione alle applicazioni basate su Platform.

## Utilizzo delle licenze {#license-usage}

La  [Dashboard dell&#39;utilizzo della licenza di Distiller dati](./license-usage.md) è disponibile dopo l’acquisto delle ore di elaborazione di Data Distiller. Il dashboard di utilizzo della licenza consente di monitorare il consumo di ore di calcolo autorizzate. Consulta la sezione [Documento sull&#39;utilizzo della licenza di Distiller dati](./license-usage.md) per visualizzare informazioni importanti sull’utilizzo della licenza Query Service della tua organizzazione.

## Parametri di ambito {#scoping-parameters}

I parametri di ambito sono limiti di utilizzo relativi all&#39;ambito della configurazione richiesta e sono definiti dalla capacità della licenza. Senza componenti aggiuntivi, i parametri di ambito di Data Distiller sono i seguenti:

* **Orari di calcolo**: È possibile utilizzare PSQL o l’API del servizio query per eseguire query batch eseguite in qualsiasi sandbox (pianificato o di altro tipo) per eseguire la scansione e la scrittura di dati. Questo utilizza le ore di calcolo assegnate all&#39;anno come determinato nel processo di ambito del contratto di licenza. Il totale delle ore di elaborazione viene accumulato in tutte le sandbox.
* **Dati inseriti**: I dati acquisiti in Adobe Experience Platform che possono essere sottoposti a query tramite Data Distiller sono soggetti alle limitazioni descritte nella licenza corrente in uso per Adobe Real-time Customer Data Platform, Customer Journey Analytics e/o Adobe Journey Optimizer.
* **Archiviazione Data Lake**: L’archiviazione data lake fornita nella licenza in uso per Adobe Real-time Customer Data Platform, Customer Journey Analytics e/o Adobe Journey Optimizer può essere utilizzata anche con Data Distiller. Data Lake Storage è una funzionalità condivisa.
* **Utenti del servizio query**: È inoltre possibile utilizzare con Data Distiller il numero di utenti del servizio Query, descritti nella licenza corrente per Adobe Real-time Customer Data Platform, Customer Journey Analytics e/o Adobe Journey Optimizer. Utenti del servizio query è una funzionalità condivisa.

## Guardrail

Consulta la sezione [Garanzie del servizio query](../guardrails.md) documento relativo ai limiti di utilizzo predefiniti per i dati del servizio query in relazione al diritto di licenza.

## Limiti statici

Un limite statico è il limite di utilizzo relativo ai limiti funzionali di Adobe Experience Platform Activation. [Ulteriori informazioni su Adobe Experience Platform Activation](https://helpx.adobe.com/ca/legal/product-descriptions/adobe-experience-platform0.html) si trova nei documenti della guida di Adobe. Di seguito è riportato un riepilogo dei limiti statici di Data Distiller. Per informazioni più complete, consulta il documento di garanzia del servizio query .

* **Query batch**: Le query batch pianificate scadono dopo 24 ore.
* **Servizio query**: È possibile utilizzare Query Service per i seguenti scopi:
   * Per eseguire query SQL per l’analisi dei dati e la preparazione dei dati post-acquisizione (pulizia, modellazione e manipolazione).
   * Per eseguire query SQL per creare metriche di rollup da visualizzare direttamente in uno strumento BI.
   * Per ispezionare rapidamente i dati in Adobe Experience Platform.
   * Per generare informazioni significative dai tuoi dati.
* **Chiamata API per reporting**: Per garantire che le query eseguite sui dati aggregati utilizzando l’API di reporting dispongano di risorse sufficienti per essere eseguite in modo efficiente. Ciò include query che migliorano i modelli di dati esistenti, come quelli forniti da Real-time Customer Data Platform. L’API di reporting tiene traccia dell’utilizzo delle risorse assegnando gli slot di concorrenza a ogni query. Sono disponibili simultaneamente fino a 4 chiamate API per la generazione di rapporti. Se si accede all&#39;API di reporting tramite uno strumento BI e si richiedono più slot di concorrenza, è necessario un server BI.


