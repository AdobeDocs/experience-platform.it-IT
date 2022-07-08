---
description: L’API di test della destinazione basata su file è una raccolta di endpoint che puoi utilizzare per convalidare la configurazione delle destinazioni basate su file generate tramite la Destination SDK.
title: API di test della destinazione basata su file
source-git-commit: d2d362f4b61e04fc2fa4d9cd9db70ed94a850642
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---


# API di test della destinazione basata su file

## Panoramica {#overview}

L’API di test della destinazione basata su file è un set di endpoint che puoi utilizzare per convalidare la configurazione delle destinazioni basate su file generate tramite la Destination SDK.

È consigliabile utilizzare questi strumenti per convalidare la configurazione prima di [invio](submit-destination.md) la destinazione da rivedere ad Adobe.

Per ottenere i migliori risultati di test, ti consigliamo di utilizzare questa API basata sul diagramma di flusso seguente.

![Diagramma che mostra il flusso di prova della destinazione consigliato](assets/file-based-testing-flow.png)

Consulta le sezioni seguenti per una breve panoramica delle operazioni eseguibili da ciascun endpoint.

## Endpoint di generazione di esempio {#sample-generation-endpoint}

Questo endpoint consente di generare profili di esempio in base allo schema di origine esistente.

I profili di esempio hanno lo scopo di aiutarti a comprendere la struttura JSON di un profilo. Inoltre, ti forniscono una spina dorsale che puoi personalizzare con i tuoi dati di profilo, per ulteriori test di destinazione.

Consulta la sezione [documentazione dedicata](file-based-sample-profile-generation-api.md) per scoprire come generare profili di esempio.

## Endpoint di test per la configurazione della destinazione {#destination-configuration-testing-endpoint}

Questo endpoint consente di verificare se la destinazione basata su file è configurata correttamente e di verificare l’integrità dei dati che fluiscono nella destinazione configurata.

È possibile inviare richieste all’endpoint di test con o senza l’aggiunta di [profili di esempio](file-based-sample-profile-generation-api.md) alla chiamata. Se non invii profili sulla richiesta, l’API genera automaticamente un profilo di esempio e lo aggiunge alla richiesta.

Consulta la sezione [documentazione dedicata](file-based-destination-testing-api.md) per scoprire come verificare la configurazione di destinazione con profili di esempio.

## Endpoint dei risultati di attivazione {#activation-results}

Questo endpoint ti aiuta a visualizzare i dettagli completi dei risultati dei test di destinazione basati su file.

Questo endpoint API restituisce lo stesso risultato ottenuto quando si utilizza il [API del servizio di flusso](../api/update-destination-dataflows.md) per monitorare i flussi di dati.

Consulta la sezione [documentazione dedicata](file-based-destination-results-api.md) per scoprire come visualizzare i risultati dettagliati dell’attivazione.

## Endpoint di rendering per campi cliente {#customer-fields-rendering-endpoint}

Questo endpoint consente di visualizzare il modello [campi dati del cliente](file-based-destination-configuration.md#customer-data-fields) come definito nella configurazione di destinazione.

L’endpoint genera valori casuali per i campi dei dati del cliente e li restituisce nella risposta. Questo consente di convalidare la struttura semantica dei campi di dati del cliente, ad esempio i nomi dei bucket o i percorsi delle cartelle.

Consulta la sezione [documentazione dedicata](file-based-render-template-api.md) per scoprire come visualizzare i risultati dettagliati dell’attivazione.