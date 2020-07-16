---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Governance dei dati ed esercitazioni sulla privacy
topic: tutorial
translation-type: tm+mt
source-git-commit: 5c5f6c4868e195aef76bacc0a1e5df3857647bde
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---


# [!DNL Data Governance] e [!DNL Privacy] esercitazioni

[!DNL Data Usage Labeling and Enforcement] (DULE) è il meccanismo principale del Adobe Experience Platform  [!DNL Data Governanc]e. Le funzioni DULE consentono di applicare etichette di utilizzo dei dati a set di dati e campi, suddividendo ciascuna in categorie in base ai relativi criteri di utilizzo dei dati. Prima di iniziare con le etichette, consulta la panoramica [sulla governance dei](../data-governance/home.md) dati per un&#39;introduzione più efficace al framework DULE all&#39;interno [!DNL Platform].

 Adobe Experience Platform [!DNL Privacy Service] fornisce un&#39;API RESTful e un&#39;interfaccia utente che consentono di coordinare le richieste di privacy e conformità tra le varie soluzioni. Per saperne di più, si prega di iniziare leggendo la panoramica [di](../privacy-service/home.md)Privacy Service.

## Aggiungi etichette di utilizzo dati

Le etichette di utilizzo dei dati consentono di classificare set di dati e campi in base ai criteri di utilizzo applicabili ai dati. Le etichette possono essere applicate in qualsiasi momento, fornendo la flessibilità nella modalità di gestione dei dati. Le best practice incoraggiano i dati di etichettatura non appena vengono ingeriti [!DNL Experience Platform]o non appena i dati diventano disponibili per l&#39;uso in [!DNL Platform]. Le etichette di utilizzo dei dati applicate a livello di dataset vengono propagate a tutti i campi all&#39;interno del dataset. Le etichette possono anche essere applicate direttamente a singoli campi (intestazioni di colonna) di un dataset, senza propagazione. Per informazioni su come applicare le etichette di utilizzo dei dati ai dati, consultare la panoramica [delle etichette di utilizzo dei](../data-governance/labels/overview.md)dati.

## Creazione di criteri di utilizzo dei dati

L&#39; [!DNL Policy Service] API DULE consente di creare e gestire criteri DULE per determinare quali azioni di marketing possono essere eseguite rispetto ai dati che contengono determinate etichette DULE. Per iniziare, leggi la panoramica [dei criteri di utilizzo dei](../data-governance/policies/overview.md)dati.

## Applica criteri di utilizzo dei dati

Dopo aver creato etichette DUE (Data Usage Labeling and Enforcement) per i dati, e aver creato criteri DULE per le azioni di marketing rispetto a tali etichette, potete utilizzare l&#39; [!DNL Policy Service] API DULE per valutare se un&#39;azione di marketing eseguita su un set di dati o un gruppo arbitrario di etichette DULE costituisce una violazione dei criteri. Potete quindi configurare i vostri protocolli interni per gestire le violazioni dei criteri in base alla risposta API. Per iniziare, consulta la panoramica [delle](../data-governance/enforcement/overview.md)attività di applicazione dei criteri.

## Applica la conformità all&#39;utilizzo dei dati per un segmento di pubblico

I segmenti abilitati per l’uso in [!DNL Real-time Customer Profile] contengono un ID criterio di unione all’interno della definizione del segmento. Questo criterio di unione contiene informazioni sui set di dati da includere nel segmento, che a loro volta contengono eventuali etichette di utilizzo dei dati applicabili. Per passaggi specifici relativi all&#39;applicazione della conformità dell&#39;utilizzo dei dati per un segmento di pubblico, segui l&#39;esercitazione sull&#39;applicazione della conformità dell&#39;uso [dei dati per i segmenti](../segmentation/tutorials/governance.md).

## Get started with [!DNL Privacy Service]

[!DNL Privacy Service] fornisce un&#39;API RESTful e un&#39;interfaccia utente che consentono di gestire i dati personali degli interessati (clienti) nelle applicazioni Adobe Experience Cloud. [!DNL Privacy Service] fornisce inoltre un meccanismo centrale di controllo e registrazione che consente di accedere allo stato e ai risultati dei processi che coinvolgono [!DNL Experience Cloud] le applicazioni. Per istruzioni su come creare e monitorare [!DNL Privacy Service] i processi, seguite i passaggi forniti nella guida [per gli sviluppatori di](../privacy-service/api/getting-started.md) Privacy Service o nella guida [per gli utenti di](../privacy-service/ui/overview.md)Privacy Service.