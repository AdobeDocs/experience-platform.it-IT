---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Guida API del servizio criteri
description: L’API del servizio criteri consente agli sviluppatori di gestire le etichette e i criteri di utilizzo dei dati, ad Experience Platform. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
role: Developer
exl-id: 23c05670-7107-4b96-bc24-0a51b5d267b2
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 4%

---

# Guida dell’API di [!DNL Policy Service]

La governance dei dati di Adobe Experience Platform consente di gestire i dati dei clienti e di garantire la conformità alle normative, alle restrizioni e alle politiche applicabili all’utilizzo dei dati. Svolge un ruolo chiave all&#39;interno di [!DNL Experience Platform] a vari livelli, tra cui catalogazione, derivazione dati, etichettatura di utilizzo dati, criteri di utilizzo dati e controllo dell&#39;utilizzo dei dati per le azioni di marketing.

L&#39;API [!DNL Policy Service] fornisce diversi endpoint che consentono di gestire programmaticamente le etichette e i criteri di utilizzo dei dati, nonché di valutare le azioni di marketing per le violazioni dei criteri. Questi endpoint sono descritti di seguito. Per informazioni dettagliate, consulta le guide dei singoli endpoint e fai riferimento alla [guida introduttiva](./getting-started.md) per informazioni importanti sulle intestazioni richieste, sulla lettura delle chiamate API di esempio e altro ancora.

Per visualizzare tutti gli endpoint disponibili e le operazioni CRUD, visita il [[!DNL Policy Service] Swagger API](https://www.adobe.io/experience-platform-apis/references/policy-service/).

## Etichette

Applica le etichette di utilizzo dei dati agli schemi per categorizzare set di dati e campi in base ai criteri di utilizzo applicabili a tali dati. Le etichette possono essere applicate in qualsiasi momento, offrendo flessibilità nella scelta di come gestire i dati. Le best practice incoraggiano l&#39;assegnazione delle etichette non appena vengono acquisite in [!DNL Experience Platform] o non appena i dati diventano disponibili per l&#39;utilizzo in [!DNL Platform]. È possibile creare, visualizzare, modificare ed eliminare etichette utilizzando l&#39;endpoint `/labels`. Per informazioni su come utilizzare questo endpoint, visita la [guida dell&#39;endpoint delle etichette](./labels.md).

## Azioni marketing

Le azioni di marketing (dette anche casi di utilizzo di marketing), nel contesto del framework di governance dei dati, sono azioni che un consumatore di dati [!DNL Experience Platform] può intraprendere, per le quali l&#39;organizzazione desidera limitare l&#39;utilizzo dei dati. Per informazioni dettagliate sull&#39;utilizzo delle azioni di marketing, consulta la [guida dell&#39;endpoint delle azioni di marketing](./marketing-actions.md).

## Criteri

I criteri di governance dei dati sono regole che descrivono i tipi di azioni di marketing che possono essere eseguiti o meno sui dati in [!DNL Experience Platform].

>[!NOTE]
>
>I criteri di governance dei dati non devono essere confusi con i criteri di controllo degli accessi, che determinano gli attributi di dati specifici a cui possono accedere alcuni utenti di Platform nella tua organizzazione. Per ulteriori informazioni, vedere la guida sul controllo degli accessi basato su [attributi](../../access-control/abac/overview.md).

Un criterio di governance dei dati è definito dai seguenti elementi:

1. Un’azione di marketing specifica
1. Etichette di utilizzo dati per cui l&#39;esecuzione dell&#39;azione è limitata

Per informazioni su come gestire i criteri nell&#39;API, consulta la [guida dell&#39;endpoint ](./policies.md)

## Valutazione

Dopo aver applicato le etichette di utilizzo dei dati agli schemi di Platform e aver definito i criteri di utilizzo dei dati per le azioni di marketing relative a tali etichette, le funzionalità di governance dei dati consentono di applicare tali criteri e impedire operazioni sui dati che costituiscono violazioni dei criteri.

L&#39;API [!DNL Policy Service] fornisce endpoint che consentono di testare azioni di marketing in base a set di dati o combinazioni arbitrarie di etichette di utilizzo dati per verificare se si verificano violazioni dei criteri. In base alla risposta API, puoi quindi configurare i protocolli all’interno dell’applicazione Experience per applicare in modo appropriato la conformità ai criteri di utilizzo dei dati. Per ulteriori informazioni, consulta la [guida degli endpoint di valutazione](./evaluation.md).

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l&#39;API [!DNL Policy Service], leggere la [guida introduttiva](./getting-started.md), quindi selezionare una delle guide degli endpoint per scoprire come utilizzare endpoint specifici. Per utilizzare etichette e criteri tramite l&#39;interfaccia utente [!DNL Experience Platform], fare riferimento rispettivamente alla [guida utente etichette](../labels/user-guide.md) e alla [guida utente criteri](../policies/user-guide.md).
