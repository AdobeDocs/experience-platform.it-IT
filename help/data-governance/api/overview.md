---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Guida all’API di Policy Service
topic-legacy: developer guide
description: L’API del servizio criteri consente agli sviluppatori di gestire le etichette di utilizzo dei dati e i criteri in Experience Platform. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
exl-id: 23c05670-7107-4b96-bc24-0a51b5d267b2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 0%

---

# [!DNL Policy Service] Guida all’API

Adobe Experience Platform [!DNL Data Governance] ti consente di gestire i dati dei clienti e di garantire la conformità a normative, restrizioni e criteri applicabili all’utilizzo dei dati. svolge un ruolo chiave all’interno di [!DNL Experience Platform] a vari livelli, tra cui catalogazione, derivazione dei dati, etichettatura dell’utilizzo dei dati, criteri di utilizzo dei dati e controllo dell’utilizzo dei dati per le azioni di marketing.

L’ API [!DNL Policy Service] fornisce diversi endpoint che ti consentono di gestire in modo programmatico le etichette e i criteri di utilizzo dei dati, nonché di valutare le azioni di marketing per le violazioni dei criteri. Questi punti finali sono descritti di seguito. Per informazioni dettagliate, visita le singole guide dell&#39;endpoint e fai riferimento alla [guida introduttiva](./getting-started.md) per informazioni importanti sulle intestazioni richieste, sulla lettura di chiamate API di esempio e altro ancora.

Per visualizzare tutti gli endpoint disponibili e le operazioni CRUD, visita il [[!DNL Policy Service] Swagger API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml).

## Etichette

Le etichette di utilizzo dei dati ti consentono di classificare set di dati e campi in base ai criteri di utilizzo applicati a tali dati. Le etichette possono essere applicate in qualsiasi momento, fornendo flessibilità nella scelta della modalità di gestione dei dati. Le best practice incoraggiano l’etichettatura dei dati non appena vengono acquisiti in [!DNL Experience Platform] o non appena i dati diventano disponibili per l’uso in [!DNL Platform]. Puoi creare, visualizzare, modificare ed eliminare le etichette utilizzando l’endpoint `/labels`. Per scoprire come utilizzare questo endpoint, visita la [guida all&#39;endpoint delle etichette](./labels.md).

## Azioni di marketing

Le azioni di marketing (o casi d’uso di marketing), nel contesto del framework [!DNL Data Governance], sono azioni che un consumatore di dati [!DNL Experience Platform] può intraprendere, per le quali la tua organizzazione desidera limitare l’utilizzo dei dati. Per informazioni dettagliate sull&#39;utilizzo delle azioni di marketing, consulta la [guida dell&#39;endpoint per le azioni di marketing](./marketing-actions.md).

## Criteri

I criteri di utilizzo dei dati sono regole che descrivono i tipi di azioni di marketing consentite o a cui è stata limitata l’esecuzione di dati all’interno di [!DNL Experience Platform]. Un criterio è definito come segue:

1. Un’azione di marketing specifica
1. Le etichette di utilizzo dei dati su cui è limitata l’esecuzione dell’azione

Per informazioni su come gestire i criteri nell&#39;API, consulta la [guida all&#39;endpoint dei criteri](./policies.md)

## Valutazione

Una volta applicate le etichette di utilizzo dei dati ai set di dati [!DNL Platform] e definite le policy di utilizzo dei dati per le azioni di marketing basate su tali etichette, le funzionalità di governance dei dati consentono di applicare tali criteri e impedire le operazioni relative ai dati che costituiscono violazioni dei criteri.

L’ API [!DNL Policy Service] fornisce endpoint che consentono di testare le azioni di marketing rispetto ai set di dati o a combinazioni arbitrarie di etichette di utilizzo dei dati per verificare se si verificano violazioni dei criteri. In base alla risposta API, puoi quindi impostare i protocolli all’interno dell’applicazione experience per applicare in modo appropriato la conformità ai criteri di utilizzo dei dati. Per ulteriori informazioni, consulta la [guida agli endpoint di valutazione](./evaluation.md) .

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l&#39;API [!DNL Policy Service], leggi la [guida introduttiva](./getting-started.md) , quindi seleziona una delle guide dell&#39;endpoint per scoprire come utilizzare endpoint specifici. Per utilizzare le etichette e i criteri utilizzando l&#39;interfaccia utente [!DNL Experience Platform], fare riferimento rispettivamente alla [guida utente delle etichette](../labels/user-guide.md) e alla [guida utente dei criteri](../policies/user-guide.md).
