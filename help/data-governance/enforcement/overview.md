---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Panoramica dell'applicazione dei criteri
topic: enforcement
translation-type: tm+mt
source-git-commit: d1659bbdd40cf1e598713f1fe1a6eeae8e8249cc

---


# Panoramica dell&#39;applicazione dei criteri

Una volta applicate le etichette di utilizzo dei dati ai set di dati della piattaforma e definite le policy di utilizzo dei dati per le azioni di marketing relative a tali etichette, le funzionalità di governance dei dati consentono di applicare tali criteri e di impedire le operazioni sui dati che costituiscono violazioni dei criteri.

Esistono due metodi di applicazione dei criteri forniti dalle funzionalità di governance dei dati sulla piattaforma: Applicazione **basata su** API e applicazione **automatica**.

## Applicazione basata sulle API

L&#39;API Policy Service fornisce endpoint che consentono di sottoporre a test le azioni di marketing in base a set di dati o combinazioni arbitrarie di etichette di utilizzo dei dati per verificare se si verificano violazioni dei criteri. In base alla risposta API, potete quindi impostare protocolli all&#39;interno dell&#39;applicazione dell&#39;esperienza per applicare in modo appropriato la conformità ai criteri di utilizzo dei dati.

Per istruzioni su come valutare i criteri mediante l&#39;API, vedete l&#39;esercitazione sull&#39;applicazione [dei](api-enforcement.md) criteri.

## Esecuzione automatica

Alcune applicazioni integrate nella piattaforma Experience (ad esempio la piattaforma dati cliente in tempo reale) forniscono l&#39;applicazione automatica dei criteri di utilizzo dei dati. Ogni applicazione mantiene un proprio metodo per individuare le violazioni dei criteri e per fornire le misure necessarie per risolvere i problemi.

Per ulteriori informazioni sull&#39;implementazione automatica dei criteri di utilizzo dei dati, consultare la documentazione relativa all&#39;applicazione basata sulla piattaforma in uso. Per informazioni sull&#39;applicazione automatica delle regole nel CDP in tempo reale, fare riferimento alla panoramica [sulla governance dei dati in tempo](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)reale del CDP.