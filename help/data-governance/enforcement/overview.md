---
keywords: Experience Platform;home;popular topics;Policy enforcement;Automatic enforcement;API-based enforcement;data governance
solution: Experience Platform
title: Panoramica dell'applicazione dei criteri
topic: enforcement
description: Una volta applicate le etichette di utilizzo dei dati ai set di dati Adobe Experience Platform e definite le policy di utilizzo dei dati per le azioni di marketing relative a tali etichette, le funzionalità di governance dei dati consentono di applicare tali criteri e di impedire le operazioni sui dati che costituiscono violazioni dei criteri. Esistono due metodi per l'applicazione dei criteri forniti dalle funzionalità di governance dei dati sulla piattaforma, l'applicazione basata sulle API e l'applicazione automatica.
translation-type: tm+mt
source-git-commit: 30733f2274ff8cb9ae73cf2b9f7f0219fefbd393
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# Panoramica dell&#39;applicazione dei criteri

Una volta applicate le etichette di utilizzo dei dati ai set di dati [!DNL Platform] e definite le policy di utilizzo dei dati per le azioni di marketing relative a tali etichette, le funzionalità [!DNL Data Governance] consentono di applicare tali criteri e di impedire le operazioni sui dati che costituiscono violazioni dei criteri.

Esistono due metodi di imposizione dei criteri forniti dalle funzionalità [!DNL Data Governance] in [!DNL Platform]: Applicazione basata su API e applicazione automatica.

## Applicazione basata sulle API

L&#39;API [!DNL Policy Service] fornisce endpoint che consentono di sottoporre a test le azioni di marketing in base a set di dati o combinazioni arbitrarie di etichette di utilizzo dei dati per verificare se si verificano violazioni dei criteri. In base alla risposta API, potete quindi impostare protocolli all&#39;interno dell&#39;applicazione dell&#39;esperienza per applicare in modo appropriato la conformità ai criteri di utilizzo dei dati.

Per informazioni su come valutare i criteri mediante l&#39;API, vedete l&#39;esercitazione su [imposizione basata sulle API](./api-enforcement.md).

## Esecuzione automatica

 Experience Platform sfrutta il line-up di dati, la classificazione dei dati e le funzionalità di gestione dei criteri per valutare e monitorare automaticamente le violazioni dei criteri. Per ulteriori informazioni, vedere la panoramica sull&#39; [applicazione automatica dei criteri](./auto-enforcement.md).