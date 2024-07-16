---
description: Scopri come utilizzare l’API di test delle destinazioni basate su file per convalidare la configurazione delle destinazioni basate su file create tramite Destination SDK.
title: API di test di destinazione basata su file
exl-id: 2733fd00-af08-4763-a30e-a53ee56c0a19
source-git-commit: adf75720f3e13c066b5c244d6749dd0939865a6f
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---


# Panoramica dell’API di test di destinazione basato su file

L’API di test della destinazione basata su file è un set di endpoint che puoi utilizzare per convalidare la configurazione delle destinazioni basate su file generate tramite la Destination SDK.

È consigliabile utilizzare questi strumenti per convalidare la configurazione prima di [inviare](../../guides/submit-destination.md) la destinazione per la revisione ad Adobe.

Per risultati di test ottimali, consigliamo di utilizzare questa API in base al diagramma di flusso riportato di seguito.

![Diagramma che mostra il flusso di test di destinazione consigliato](../../assets/testing-api/batch-destinations/file-based-testing-flow.png)

Consulta le sezioni seguenti per una breve panoramica su ciò che può fare ogni endpoint.

## Generare profili di esempio {#generate-sample-profiles}

Utilizza l&#39;endpoint API `/sample-profiles` per generare profili di esempio in base allo schema di origine esistente.

I profili di esempio possono aiutarti a comprendere la struttura JSON di un profilo. Inoltre, ti forniscono un valore predefinito che puoi personalizzare con i tuoi dati di profilo, per ulteriori test di destinazione.

Consulta la [documentazione dedicata](file-based-sample-profile-generation-api.md) per scoprire come generare profili di esempio.

## Verifica configurazione di destinazione {#test-destination-configuration}

Utilizza l&#39;endpoint API `/testing/destinationInstance` per verificare se la destinazione basata su file è configurata correttamente e per verificare l&#39;integrità dei flussi di dati alla destinazione configurata.

Puoi effettuare richieste all&#39;endpoint di test con o senza aggiungere [profili di esempio](file-based-sample-profile-generation-api.md) alla chiamata. Se non invii profili nella richiesta, l’API genera automaticamente un profilo di esempio e lo aggiunge alla richiesta.

Consulta la [documentazione dedicata](file-based-destination-testing-api.md) per scoprire come verificare la configurazione di destinazione con i profili di esempio.

## Visualizza risultati di attivazione dettagliati {#view-detailed-activation-results}

Utilizza l&#39;endpoint API `/testing/destinationInstance` per visualizzare i dettagli completi dei risultati dei test di destinazione basati su file.

Questo endpoint API restituisce lo stesso risultato ottenuto quando si utilizza l&#39;API [Flow Service](../../../api/update-destination-dataflows.md) per monitorare i flussi di dati.

Consulta la [documentazione dedicata](file-based-destination-results-api.md) per scoprire come visualizzare i risultati dettagliati dell&#39;attivazione.

## Rendering dei campi dati del cliente {#render-customer-data-fields}

Utilizza l&#39;endpoint API `/authoring/testing/template/render` per visualizzare come si presenteranno i [campi dati cliente](../../functionality/destination-configuration/customer-data-fields.md) definiti nella configurazione di destinazione.

L’endpoint API genera valori casuali per i campi dati del cliente e li restituisce nella risposta. Questo consente di convalidare la struttura semantica dei campi dati del cliente, ad esempio i nomi dei bucket o i percorsi delle cartelle.

Consulta la [documentazione dedicata](file-based-render-template-api.md) per scoprire come generare e visualizzare i valori per i campi dei dati cliente.
