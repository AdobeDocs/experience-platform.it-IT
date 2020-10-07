---
keywords: Experience Platform;home;popular topics;Policy enforcement;Automatic enforcement;API-based enforcement;data governance
solution: Experience Platform
title: Panoramica dell'applicazione dei criteri
topic: enforcement
description: Una volta applicate le etichette di utilizzo dei dati ai set di dati Adobe Experience Platform e definite le policy di utilizzo dei dati per le azioni di marketing relative a tali etichette, le funzionalità di governance dei dati consentono di applicare tali criteri e di impedire le operazioni sui dati che costituiscono violazioni dei criteri. Esistono due metodi per l'applicazione dei criteri forniti dalle funzionalità di governance dei dati sulla piattaforma, l'applicazione basata sulle API e l'applicazione automatica.
translation-type: tm+mt
source-git-commit: 28b733a16b067f951a885c299d59e079f0074df8
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---


# Panoramica dell&#39;applicazione dei criteri

Una volta applicate le etichette di utilizzo dei dati ai [!DNL Platform] set di dati e definite le policy di utilizzo dei dati per le azioni di marketing relative a tali etichette, [!DNL Data Governance] le funzionalità consentono di applicare tali criteri e di impedire le operazioni sui dati che costituiscono violazioni dei criteri.

Esistono due metodi di applicazione delle regole forniti dalle [!DNL Data Governance] funzionalità per [!DNL Platform]: Applicazione basata su API e applicazione automatica.

## Applicazione basata sulle API

L&#39; [!DNL Policy Service] API fornisce endpoint che consentono di sottoporre a test le azioni di marketing in base a set di dati o combinazioni arbitrarie di etichette di utilizzo dei dati per verificare se si verificano violazioni dei criteri. In base alla risposta API, potete quindi impostare protocolli all&#39;interno dell&#39;applicazione dell&#39;esperienza per applicare in modo appropriato la conformità ai criteri di utilizzo dei dati.

Per istruzioni su come valutare i criteri mediante l&#39;API, vedete l&#39;esercitazione sull&#39;applicazione [dei](api-enforcement.md) criteri.

## Esecuzione automatica

Alcune applicazioni integrate [!DNL Experience Platform] (ad esempio, [!DNL Real-time Customer Data Platform]) forniscono l&#39;applicazione automatica dei criteri di utilizzo dei dati. Ogni applicazione mantiene un proprio metodo per individuare le violazioni dei criteri e per fornire le misure necessarie per risolvere i problemi.

Per ulteriori informazioni sull&#39;applicazione [!DNL Platform]basata sui criteri di utilizzo automatico dei dati, consultare la documentazione relativa all&#39;applicazione. Per informazioni sull&#39;applicazione automatica delle regole nel CDP in tempo reale, fare riferimento alla panoramica [sulla governance dei dati in tempo](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)reale del CDP.