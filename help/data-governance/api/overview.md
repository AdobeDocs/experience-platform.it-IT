---
keywords: ' Experience Platform;home;argomenti popolari'
solution: Experience Platform
title: Guida per gli sviluppatori API di Policy Service
topic: developer guide
description: Scoprite come utilizzare l'API Policy Service per gestire le etichette e i criteri di utilizzo dei dati in  Experience Platform.
translation-type: tm+mt
source-git-commit: 5dad1fcc82707f6ee1bf75af6c10d34ff78ac311
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 1%

---


# [!DNL Policy Service] Guida per gli sviluppatori di API

Adobe Experience Platform [!DNL Data Governance] consente di gestire i dati dei clienti e garantire la conformità a normative, restrizioni e criteri applicabili all&#39;uso dei dati. Essa svolge un ruolo chiave all&#39;interno di [!DNL Experience Platform] a vari livelli, tra cui catalogazione, linea di dati, etichettatura dell&#39;utilizzo dei dati, criteri di utilizzo dei dati e controllo dell&#39;utilizzo dei dati per le azioni di marketing.

L&#39;API [!DNL Policy Service] fornisce diversi endpoint che consentono di gestire etichette e criteri di utilizzo dei dati a livello di programmazione, nonché di valutare le azioni di marketing per le violazioni dei criteri. Tali punti finali sono descritti di seguito. Per informazioni dettagliate, visitate le singole guide degli endpoint e fate riferimento alla [guida introduttiva](./getting-started.md) per informazioni importanti sulle intestazioni richieste, sulla lettura di chiamate API di esempio e altro ancora.

Per visualizzare tutti gli endpoint disponibili e le operazioni CRUD, visitare il [[!DNL Policy Service] swagger API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml).

## Etichette

Le etichette di utilizzo dei dati consentono di classificare set di dati e campi in base ai criteri di utilizzo applicabili ai dati. Le etichette possono essere applicate in qualsiasi momento, fornendo la flessibilità nella modalità di gestione dei dati. Le best practice incoraggiano i dati di etichettatura non appena vengono trasferiti in [!DNL Experience Platform] o non appena i dati diventano disponibili per l&#39;uso in [!DNL Platform]. È possibile creare, visualizzare, modificare ed eliminare le etichette utilizzando l&#39;endpoint `/labels`. Per informazioni su come utilizzare questo endpoint, visitare la [guida dell&#39;endpoint etichette](./labels.md).

## Azioni di marketing

Le azioni di marketing (o casi di utilizzo marketing), nel contesto del framework [!DNL Data Governance], sono azioni che un consumatore di dati [!DNL Experience Platform] può intraprendere, per le quali l&#39;organizzazione desidera limitare l&#39;uso dei dati. Per informazioni dettagliate sull&#39;utilizzo delle azioni di marketing, consulta la [guida dell&#39;endpoint delle azioni di marketing](./marketing-actions.md).

## Criteri

I criteri di utilizzo dei dati sono regole che descrivono i tipi di azioni di marketing consentite o con cui è consentito eseguire attività sui dati all&#39;interno di [!DNL Experience Platform]. Un criterio è definito come segue:

1. Un&#39;azione di marketing specifica
1. Le etichette di utilizzo dei dati a cui è stata limitata l&#39;esecuzione dell&#39;azione

Per informazioni su come gestire i criteri nell&#39;API, consulta la [guida dell&#39;endpoint dei criteri](./policies.md)

## Valutazione

Una volta applicate le etichette di utilizzo dei dati ai set di dati [!DNL Platform] e definite le policy di utilizzo dei dati per le azioni di marketing relative a tali etichette, le funzionalità di governance dei dati consentono di applicare tali criteri e di impedire le operazioni sui dati che costituiscono violazioni dei criteri.

L&#39;API [!DNL Policy Service] fornisce endpoint che consentono di sottoporre a test le azioni di marketing in base a set di dati o combinazioni arbitrarie di etichette di utilizzo dei dati per verificare se si verificano violazioni dei criteri. In base alla risposta API, potete quindi impostare protocolli all&#39;interno dell&#39;applicazione dell&#39;esperienza per applicare in modo appropriato la conformità ai criteri di utilizzo dei dati. Per ulteriori informazioni, vedere la [guida agli endpoint di valutazione](./evaluation.md).

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l&#39;API [!DNL Policy Service], leggi la [guida introduttiva](./getting-started.md), quindi seleziona una delle guide dell&#39;endpoint per scoprire come utilizzare endpoint specifici. Per utilizzare etichette e criteri utilizzando l&#39;interfaccia utente [!DNL Experience Platform], fare riferimento rispettivamente alla guida utente delle etichette [guide utente](../labels/user-guide.md) e alla guida utente [alle regole](../policies/user-guide.md).