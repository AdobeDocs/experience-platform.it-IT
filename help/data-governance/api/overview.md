---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guida per gli sviluppatori API di Policy Service
topic: developer guide
translation-type: tm+mt
source-git-commit: cb3a17aa08c67c66101cbf3842bf306ebcca0305
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 1%

---


# [!DNL Policy Service] Guida per gli sviluppatori di API

Adobe Experience Platform [!DNL Data Governance] consente di gestire i dati dei clienti e garantire la conformità a normative, restrizioni e criteri applicabili all&#39;uso dei dati. Esso svolge un ruolo chiave a vari livelli, [!DNL Experience Platform] tra cui catalogazione, linea di dati, etichettatura dell&#39;utilizzo dei dati, criteri di utilizzo dei dati e controllo dell&#39;utilizzo dei dati per le azioni di marketing.

L&#39; [!DNL Policy Service] API fornisce diversi endpoint che consentono di gestire le etichette e i criteri di utilizzo dei dati a livello di programmazione, nonché di valutare le azioni di marketing per le violazioni dei criteri. Tali punti finali sono descritti di seguito. Per informazioni dettagliate, consultate le singole guide degli endpoint e la guida [](./getting-started.md) introduttiva per informazioni importanti sulle intestazioni richieste, sulla lettura di chiamate API di esempio e altro ancora.

Per visualizzare tutti gli endpoint disponibili e le operazioni CRUD, visitate lo swagger API [Policy Service](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml).

## Etichette

Le etichette di utilizzo dei dati consentono di classificare set di dati e campi in base ai criteri di utilizzo applicabili ai dati. Le etichette possono essere applicate in qualsiasi momento, fornendo la flessibilità nella modalità di gestione dei dati. Le best practice incoraggiano i dati di etichettatura non appena vengono ingeriti [!DNL Experience Platform]o non appena i dati diventano disponibili per l&#39;uso in [!DNL Platform]. È possibile creare, visualizzare, modificare ed eliminare etichette utilizzando l&#39; `/labels` endpoint. Per informazioni su come utilizzare questo endpoint, consultare la guida [all&#39;endpoint delle](./labels.md)etichette.

## Azioni di marketing

Le azioni di marketing (denominate anche casi di utilizzo del marketing), nel contesto del [!DNL Data Governance] [!DNL Experience Platform] framework, sono azioni che un consumatore di dati può intraprendere, per le quali l&#39;organizzazione intende limitare l&#39;uso dei dati. Per informazioni dettagliate sull&#39;utilizzo delle azioni di marketing, consulta la guida [all&#39;endpoint delle azioni di](./marketing-actions.md)marketing.

## Criteri

I criteri di utilizzo dei dati sono regole che descrivono i tipi di azioni di marketing consentite o con cui è consentito eseguire determinate attività sui dati all&#39;interno [!DNL Experience Platform]. Un criterio è definito come segue:

1. Un&#39;azione di marketing specifica
1. Le etichette di utilizzo dei dati a cui è stata limitata l&#39;esecuzione dell&#39;azione

Per informazioni su come gestire i criteri nell&#39;API, consulta la guida agli endpoint dei [criteri](./policies.md)

## Valutazione

Una volta applicate le etichette di utilizzo dei dati ai [!DNL Platform] set di dati e definite le policy di utilizzo dei dati per le azioni di marketing relative a tali etichette, le funzionalità di governance dei dati consentono di applicare tali criteri e di impedire le operazioni sui dati che costituiscono violazioni dei criteri.

L&#39; [!DNL Policy Service] API fornisce endpoint che consentono di sottoporre a test le azioni di marketing in base a set di dati o combinazioni arbitrarie di etichette di utilizzo dei dati per verificare se si verificano violazioni dei criteri. In base alla risposta API, potete quindi impostare protocolli all&#39;interno dell&#39;applicazione dell&#39;esperienza per applicare in modo appropriato la conformità ai criteri di utilizzo dei dati. Per ulteriori informazioni, consulta la guida [agli endpoint di](./evaluation.md) valutazione.

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l&#39; [!DNL Policy Service] API, leggi la guida [](./getting-started.md) introduttiva e seleziona una delle guide degli endpoint per apprendere come utilizzare endpoint specifici. Per utilizzare etichette e criteri utilizzando l&#39; [!DNL Experience Platform] interfaccia utente, consultare, rispettivamente, la guida [utente relativa alle](../labels/user-guide.md) etichette e la guida [utente relativa ai](../policies/user-guide.md)criteri.