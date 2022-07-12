---
description: L’API di test della destinazione basata su file è una raccolta di endpoint che puoi utilizzare per convalidare la configurazione delle destinazioni basate su file generate tramite la Destination SDK.
title: API di test della destinazione basata su file
source-git-commit: 734d66cc881ab1b691c13ef446331d0c51851cf9
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---


# API di test della destinazione basata su file

## Panoramica {#overview}

L’API di test della destinazione basata su file è un set di endpoint che puoi utilizzare per convalidare la configurazione delle destinazioni basate su file generate tramite la Destination SDK.

È consigliabile utilizzare questi strumenti per convalidare la configurazione prima di [invio](submit-destination.md) la destinazione da rivedere ad Adobe.

Per ottenere i migliori risultati di test, ti consigliamo di utilizzare questa API basata sul diagramma di flusso seguente.

![Diagramma che mostra il flusso di prova della destinazione consigliato](assets/file-based-testing-flow.png)

Consulta le sezioni seguenti per una breve panoramica delle operazioni eseguibili da ciascun endpoint.

## Generare profili di esempio {#generate-sample-profiles}

Utilizza la `/sample-profiles` Endpoint API per generare profili di esempio basati sullo schema di origine esistente.

I profili di esempio possono aiutarti a comprendere la struttura JSON di un profilo. Inoltre, ti forniscono un valore predefinito che puoi personalizzare con i tuoi dati di profilo, per ulteriori test di destinazione.

Consulta la sezione [documentazione dedicata](file-based-sample-profile-generation-api.md) per scoprire come generare profili di esempio.

## Verificare la configurazione della destinazione {#test-destination-configuration}

Utilizza la `/testing/destinationInstance` Endpoint API per verificare se la destinazione basata su file è configurata correttamente e l’integrità dei dati scorre nella destinazione configurata.

È possibile inviare richieste all’endpoint di test con o senza l’aggiunta di [profili di esempio](file-based-sample-profile-generation-api.md) alla chiamata. Se non invii profili sulla richiesta, l’API genera automaticamente un profilo di esempio e lo aggiunge alla richiesta.

Consulta la sezione [documentazione dedicata](file-based-destination-testing-api.md) per scoprire come verificare la configurazione di destinazione con profili di esempio.

## Visualizza i risultati dettagliati dell’attivazione {#view-detailed-activation-results}

Utilizza la `/testing/destinationInstance` Endpoint API per visualizzare i dettagli completi dei risultati dei test di destinazione basati su file.

Questo endpoint API restituisce lo stesso risultato ottenuto quando si utilizza il [API del servizio di flusso](../api/update-destination-dataflows.md) per monitorare i flussi di dati.

Consulta la sezione [documentazione dedicata](file-based-destination-results-api.md) per scoprire come visualizzare i risultati dettagliati dell’attivazione.

## Campi dati del cliente di rendering {#render-customer-data-fields}

Utilizza la `/authoring/testing/template/render` Endpoint API per visualizzare il modello [campi dati del cliente](file-based-destination-configuration.md#customer-data-fields) come definito nella configurazione di destinazione.

L’endpoint API genera valori casuali per i campi dei dati del cliente e li restituisce nella risposta. Questo consente di convalidare la struttura semantica dei campi di dati del cliente, ad esempio i nomi dei bucket o i percorsi delle cartelle.

Consulta la sezione [documentazione dedicata](file-based-render-template-api.md) per scoprire come generare e visualizzare i valori per i campi dati del cliente.