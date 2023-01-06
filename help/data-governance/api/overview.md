---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Guida all’API di Policy Service
description: L’API del servizio criteri consente agli sviluppatori di gestire le etichette di utilizzo dei dati e i criteri in Experience Platform. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
exl-id: 23c05670-7107-4b96-bc24-0a51b5d267b2
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 4%

---

# Guida dell’API di [!DNL Policy Service]

La governance dei dati di Adobe Experience Platform ti consente di gestire i dati dei clienti e di garantire la conformità a normative, restrizioni e criteri applicabili all’utilizzo dei dati. svolge un ruolo chiave all&#39;interno di [!DNL Experience Platform] a vari livelli, compresi catalogazione, derivazione dati, etichettatura dell’utilizzo dei dati, criteri di utilizzo dei dati e controllo dell’utilizzo dei dati per le azioni di marketing.

La [!DNL Policy Service] API fornisce diversi endpoint che ti consentono di gestire in modo programmatico le etichette e i criteri di utilizzo dei dati, nonché di valutare le azioni di marketing per le violazioni dei criteri. Questi endpoint sono descritti di seguito. Per informazioni dettagliate, visita le singole guide dell’endpoint e fai riferimento alla sezione [guida introduttiva](./getting-started.md) per informazioni importanti sulle intestazioni richieste, sulla lettura di chiamate API di esempio e altro ancora.

Per visualizzare tutti gli endpoint disponibili e le operazioni CRUD, visita il [[!DNL Policy Service] Swagger API](https://www.adobe.io/experience-platform-apis/references/policy-service/).

## Etichette

Le etichette di utilizzo dei dati ti consentono di classificare set di dati e campi in base ai criteri di utilizzo applicati a tali dati. Le etichette possono essere applicate in qualsiasi momento, fornendo flessibilità nella scelta della modalità di gestione dei dati. Le best practice incoraggiano l’etichettatura dei dati non appena vengono acquisiti in [!DNL Experience Platform], o non appena i dati diventano disponibili per l&#39;utilizzo in [!DNL Platform]. È possibile creare, visualizzare, modificare ed eliminare le etichette utilizzando `/labels` punto finale. Per scoprire come utilizzare questo endpoint, visita la [guida all’endpoint delle etichette](./labels.md).

## Azioni di marketing

Le azioni di marketing (o casi di utilizzo del marketing), nel contesto del framework di governance dei dati, sono azioni che [!DNL Experience Platform] il consumatore di dati può utilizzare, per i quali la tua organizzazione desidera limitare l’utilizzo dei dati. Per informazioni dettagliate sull’utilizzo delle azioni di marketing, consulta la sezione [guida endpoint per le azioni di marketing](./marketing-actions.md).

## Criteri

I criteri di governance dei dati sono regole che descrivono i tipi di azioni di marketing che ti sono consentite o a cui ti è consentito eseguire sui dati all’interno di [!DNL Experience Platform].

>[!NOTE]
>
>I criteri di governance dei dati non devono essere confusi con i criteri di controllo degli accessi, che determinano gli attributi di dati specifici a cui possono accedere alcuni utenti Platform della tua organizzazione. Consulta la guida su [controllo dell&#39;accesso basato sugli attributi](../../access-control/abac/overview.md) per ulteriori informazioni.

I criteri di governance dei dati sono definiti nel modo seguente:

1. Un’azione di marketing specifica
1. Le etichette di utilizzo dei dati su cui è limitata l’esecuzione dell’azione

Per informazioni su come gestire i criteri nell’API, consulta [guida all’endpoint dei criteri](./policies.md)

## Valutazione

Una volta applicate le etichette di utilizzo dei dati a [!DNL Platform] i set di dati e i criteri di utilizzo dei dati sono stati definiti per le azioni di marketing rispetto a tali etichette, le funzionalità di governance dei dati consentono di applicare tali criteri e di impedire le operazioni di dati che costituiscono violazioni dei criteri.

La [!DNL Policy Service] L’API fornisce endpoint che consentono di testare le azioni di marketing rispetto ai set di dati o a combinazioni arbitrarie di etichette di utilizzo dei dati per verificare se si verificano violazioni dei criteri. In base alla risposta API, puoi quindi impostare i protocolli all’interno dell’applicazione experience per applicare in modo appropriato la conformità ai criteri di utilizzo dei dati. Consulta la sezione [guida agli endpoint di valutazione](./evaluation.md) per ulteriori informazioni.

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando [!DNL Policy Service] API, leggi [guida introduttiva](./getting-started.md) quindi seleziona una delle guide dell’endpoint per scoprire come utilizzare endpoint specifici. Per lavorare con etichette e criteri utilizzando la variabile [!DNL Experience Platform] Interfaccia utente, fai riferimento al [guida utente sulle etichette](../labels/user-guide.md) e [Guida utente ai criteri](../policies/user-guide.md), rispettivamente.
