---
title: Panoramica di Data Distiller
description: Riepilogo dei limiti di utilizzo di Data Distiller per i dati di Query Service in relazione ai diritti di licenza.
source-git-commit: b3003cc62e8d3555b887a23f0614020bd2c5e81e
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---

# Panoramica di Data Distiller

Data Distiller è un pacchetto che include un sottoinsieme delle funzionalità di Adobe Experience Platform. Con Data Distiller puoi eseguire la preparazione dei dati di post-acquisizione (ad esempio la pulizia, la modellazione e la manipolazione) per i casi d’uso analitici o di profilo cliente in tempo reale, eseguendo query batch in Query Service. L’utilizzo di Data Distiller dipende dalla licenza di per le applicazioni basate su Platform.

## Utilizzo delle licenze {#license-usage}

Il  [Dashboard utilizzo licenze di Data Distiller](./license-usage.md) è disponibile dopo l’acquisto delle ore di elaborazione di Data Distiller. La dashboard utilizzo licenze consente di monitorare il consumo delle ore di calcolo consentite. Consulta la [Documento sull’utilizzo delle licenze di Data Distiller](./license-usage.md) per visualizzare informazioni importanti sull’utilizzo delle licenze di Query Service da parte dell’organizzazione.

## Parametri di ambito {#scoping-parameters}

I parametri di ambito sono limiti di utilizzo correlati all’ambito della configurazione richiesta e sono definiti in base alla capacità della licenza. Senza componenti aggiuntivi, i parametri di ambito di Data Distiller sono i seguenti:

* **Calcola ore**: puoi utilizzare PSQL o l’API Query Service per eseguire query batch eseguite in qualsiasi sandbox (pianificata o meno) per analizzare e scrivere dati. Questo utilizza le ore di calcolo assegnate all’anno come determinato nel processo di valutazione del contratto di licenza. Le ore totali calcolate vengono accumulate in tutte le sandbox.
* **Dati acquisiti**: i dati acquisiti in Adobe Experience Platform che possono essere interrogati utilizzando Data Distiller sono soggetti alle limitazioni descritte nella licenza corrente di Adobe Real-time Customer Data Platform, Customer Journey Analytics e/o Adobe Journey Optimizer.
* **Archiviazione Data Lake**: l’archiviazione del data lake fornita nella licenza corrente di Adobe Real-time Customer Data Platform, Customer Journey Analytics e/o Adobe Journey Optimizer può essere utilizzata anche con Data Distiller. Archiviazione Data Lake è una funzione condivisa.
* **Utenti di Query Service**: con Data Distiller è possibile utilizzare anche il numero di utenti Query Service descritto nella licenza corrente di Adobe Real-time Customer Data Platform, Customer Journey Analytics e/o Adobe Journey Optimizer. Utenti di Query Service è una funzione condivisa.

## Guardrail

Consulta la [Guardrail di Query Service](../guardrails.md) documento relativo ai limiti di utilizzo predefiniti per i dati di Query Service in relazione al diritto di licenza.

## Limiti statici

Un limite statico è il limite di utilizzo relativo ai limiti funzionali di Attivazione Adobe Experience Platform. [Ulteriori informazioni su Adobe Experience Platform Activation](https://helpx.adobe.com/ca/legal/product-descriptions/adobe-experience-platform0.html) sono disponibili nella guida di Adobe. Di seguito è riportato un riepilogo dei limiti statici di Data Distiller. Per informazioni più complete, consulta il documento del guardrail di Query Service.

* **Query batch**: le query batch pianificate scadono dopo 24 ore.
* **Servizio query**: puoi utilizzare Query Service per i seguenti scopi:
   * Eseguire query SQL per l’analisi dei dati e la preparazione dei dati di post-acquisizione (pulizia, modellazione e manipolazione).
   * Eseguire query SQL per creare metriche di rollup da visualizzare direttamente in uno strumento BI.
   * Esaminare rapidamente i dati in Adobe Experience Platform.
   * Per generare informazioni significative dai dati.
* **Chiamata API di reporting**: per garantire che le query vengano eseguite sui dati aggregati utilizzando l’API di reporting con risorse sufficienti per essere eseguite in modo efficiente. Sono incluse le query che migliorano i modelli di dati esistenti, come quelli forniti da Real-time Customer Data Platform. L’API di reporting tiene traccia dell’utilizzo delle risorse assegnando slot di concorrenza a ciascuna query. Sono disponibili contemporaneamente fino a 4 chiamate API per la generazione di rapporti. Se accedi all’API di reporting tramite uno strumento BI e richiedi più slot di concorrenza, è necessario un server BI.


