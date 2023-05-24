---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Guida API del servizio criteri
description: L’API del servizio criteri consente agli sviluppatori di gestire le etichette e i criteri di utilizzo dei dati, ad Experience Platform. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
exl-id: 23c05670-7107-4b96-bc24-0a51b5d267b2
source-git-commit: 0c09db51d97bc0cf321c5d2fd57c42d194b25d5f
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 4%

---

# Guida dell’API di [!DNL Policy Service]

La governance dei dati di Adobe Experience Platform consente di gestire i dati dei clienti e di garantire la conformità alle normative, alle restrizioni e alle politiche applicabili all’utilizzo dei dati. Svolge un ruolo chiave in [!DNL Experience Platform] a vari livelli, tra cui catalogazione, derivazione dei dati, etichettatura dell’utilizzo dei dati, criteri di utilizzo dei dati e controllo dell’utilizzo dei dati per le azioni di marketing.

Il [!DNL Policy Service] API fornisce diversi endpoint che consentono di gestire in modo programmatico le etichette e i criteri di utilizzo dei dati, nonché di valutare le azioni di marketing per le violazioni dei criteri. Questi endpoint sono descritti di seguito. Per informazioni dettagliate, consulta le guide dei singoli endpoint e fai riferimento a [guida introduttiva](./getting-started.md) per informazioni importanti sulle intestazioni richieste, leggi le chiamate API di esempio e altro ancora.

Per visualizzare tutti gli endpoint disponibili e le operazioni CRUD, visitare il [[!DNL Policy Service] Swagger API](https://www.adobe.io/experience-platform-apis/references/policy-service/).

## Etichette

Applica le etichette di utilizzo dei dati agli schemi per categorizzare set di dati e campi in base ai criteri di utilizzo applicabili a tali dati. Le etichette possono essere applicate in qualsiasi momento, offrendo flessibilità nella scelta di come gestire i dati. Le best practice incoraggiano i dati di etichettatura non appena vengono acquisiti in [!DNL Experience Platform]o non appena i dati diventano disponibili per l&#39;uso in [!DNL Platform]. È possibile creare, visualizzare, modificare ed eliminare etichette utilizzando `/labels` endpoint. Per informazioni su come utilizzare questo endpoint, visita [guida dell’endpoint &quot;labels&quot;](./labels.md).

## Azioni di marketing

Le azioni di marketing (o casi di utilizzo di marketing), nel contesto del framework per la governance dei dati, sono azioni che [!DNL Experience Platform] il consumatore di dati può accettare, per il quale l’organizzazione desidera limitare l’utilizzo dei dati. Per informazioni dettagliate sull’utilizzo delle azioni di marketing, vedi [guida dell’endpoint &quot;azioni di marketing&quot;](./marketing-actions.md).

## Criteri

I criteri di governance dei dati sono regole che descrivono i tipi di azioni di marketing che possono essere eseguiti o meno sui dati in [!DNL Experience Platform].

>[!NOTE]
>
>I criteri di governance dei dati non devono essere confusi con i criteri di controllo degli accessi, che determinano gli attributi di dati specifici a cui possono accedere alcuni utenti di Platform nella tua organizzazione. Consulta la guida su [controllo degli accessi basato su attributi](../../access-control/abac/overview.md) per ulteriori informazioni.

Un criterio di governance dei dati è definito dai seguenti elementi:

1. Un’azione di marketing specifica
1. Etichette di utilizzo dati per cui l&#39;esecuzione dell&#39;azione è limitata

Per informazioni su come gestire i criteri nell’API, consulta la [guida dell’endpoint &quot;policies&quot;](./policies.md)

## Valutazione

Dopo aver applicato le etichette di utilizzo dei dati agli schemi di Platform e aver definito i criteri di utilizzo dei dati per le azioni di marketing relative a tali etichette, le funzionalità di governance dei dati consentono di applicare tali criteri e impedire operazioni sui dati che costituiscono violazioni dei criteri.

Il [!DNL Policy Service] L’API fornisce endpoint che consentono di testare azioni di marketing in base a set di dati o combinazioni arbitrarie di etichette di utilizzo dei dati per verificare se si verificano violazioni dei criteri. In base alla risposta API, puoi quindi configurare i protocolli all’interno dell’applicazione Experience per applicare in modo appropriato la conformità ai criteri di utilizzo dei dati. Consulta la [guida degli endpoint di valutazione](./evaluation.md) per ulteriori informazioni.

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando [!DNL Policy Service] API, leggi [guida introduttiva](./getting-started.md) quindi seleziona una delle guide degli endpoint per scoprire come utilizzare endpoint specifici. Per utilizzare etichette e criteri utilizzando [!DNL Experience Platform] Interfaccia utente, fare riferimento a [guida utente delle etichette](../labels/user-guide.md) e [guida utente sui criteri](../policies/user-guide.md), rispettivamente.
