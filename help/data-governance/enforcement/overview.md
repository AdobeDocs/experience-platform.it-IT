---
keywords: Experience Platform;home;argomenti popolari;applicazione dei criteri;applicazione automatica;applicazione basata su API;governance dei dati
solution: Experience Platform
title: Panoramica sull’applicazione dei criteri
topic-legacy: guide
description: Una volta che le etichette di utilizzo dei dati sono state applicate ai set di dati Adobe Experience Platform e sono stati definiti i criteri di utilizzo dei dati per le azioni di marketing rispetto a tali etichette, le funzionalità di governance dei dati consentono di applicare tali criteri e di impedire le operazioni di dati che costituiscono violazioni dei criteri. Esistono due metodi di applicazione dei criteri forniti dalle funzioni di governance dei dati su Platform, applicazione basata su API e applicazione automatica.
exl-id: d19d8060-85a1-405c-856d-f59041947a33
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Panoramica sull&#39;applicazione dei criteri

Una volta applicate le etichette di utilizzo dei dati ai set di dati e definite le policy di utilizzo dei dati per le azioni di marketing rispetto a tali etichette, le funzionalità di governance dei dati di Adobe Experience Platform consentono di applicare tali criteri e di impedire le operazioni di dati che costituiscono violazioni dei criteri.

Esistono due metodi per l&#39;applicazione dei criteri forniti dalle funzionalità [!DNL Data Governance] in [!DNL Platform]: Implementazione basata su API e applicazione automatica.

## Implementazione basata su API

L’ API [!DNL Policy Service] fornisce endpoint che consentono di testare le azioni di marketing rispetto ai set di dati o a combinazioni arbitrarie di etichette di utilizzo dei dati per verificare se si verificano violazioni dei criteri. In base alla risposta API, puoi quindi impostare i protocolli all’interno dell’applicazione experience per applicare in modo appropriato la conformità ai criteri di utilizzo dei dati.

Per informazioni su come valutare i criteri utilizzando l&#39;API, consulta l&#39;esercitazione su [imposizione basata su API](./api-enforcement.md) .

## Applicazione automatica

Experience Platform sfrutta la derivazione dei dati, la classificazione dei dati e le funzionalità di gestione dei criteri per valutare automaticamente e individuare le violazioni dei criteri. Per ulteriori informazioni, consulta la panoramica sull’ [applicazione automatica dei criteri](./auto-enforcement.md) .
