---
keywords: Experience Platform;home;argomenti popolari;applicazione dei criteri;applicazione automatica;applicazione basata su API;governance dei dati
solution: Experience Platform
title: Panoramica sull’applicazione dei criteri
topic-legacy: guide
description: Una volta che le etichette di utilizzo dei dati sono state applicate ai set di dati Adobe Experience Platform e sono stati definiti i criteri di utilizzo dei dati per le azioni di marketing rispetto a tali etichette, le funzionalità di governance dei dati consentono di applicare tali criteri e di impedire le operazioni di dati che costituiscono violazioni dei criteri. Esistono due metodi di applicazione dei criteri forniti dalle funzioni di governance dei dati su Platform, applicazione basata su API e applicazione automatica.
exl-id: d19d8060-85a1-405c-856d-f59041947a33
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# Panoramica sull&#39;applicazione dei criteri

Una volta applicate le etichette di utilizzo dei dati ai set di dati e definite le policy di utilizzo dei dati per le azioni di marketing rispetto a tali etichette, le funzionalità di governance dei dati di Adobe Experience Platform consentono di applicare tali criteri e di impedire le operazioni di dati che costituiscono violazioni dei criteri.

Esistono due metodi di applicazione dei criteri forniti dalle funzioni di governance dei dati su [!DNL Platform]: Implementazione basata su API e applicazione automatica.

## Implementazione basata su API

La [!DNL Policy Service] L’API fornisce endpoint che consentono di testare le azioni di marketing rispetto ai set di dati o a combinazioni arbitrarie di etichette di utilizzo dei dati per verificare se si verificano violazioni dei criteri. In base alla risposta API, puoi quindi impostare i protocolli all’interno dell’applicazione experience per applicare in modo appropriato la conformità ai criteri di utilizzo dei dati.

Guarda l’esercitazione su [Implementazione basata su API](./api-enforcement.md) per informazioni su come valutare i criteri utilizzando l’API .

## Applicazione automatica

Experience Platform sfrutta la derivazione dei dati, la classificazione dei dati e le funzionalità di gestione dei criteri per valutare automaticamente e individuare le violazioni dei criteri. Vedi la panoramica su [applicazione automatica delle politiche](./auto-enforcement.md) per ulteriori informazioni.
