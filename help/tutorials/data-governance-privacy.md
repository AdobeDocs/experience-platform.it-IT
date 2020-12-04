---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Governance dei dati ed esercitazioni sulla privacy
topic: tutorial
type: Tutorial
description: Questo documento fornisce una panoramica delle diverse esercitazioni disponibili relative a Adobe Experience Platform Data Governance e  Adobe Experience Platform Privacy Service.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---


# [!DNL Data Governance] e [!DNL Privacy] Tutorials

Adobe Experience Platform Data Governance consente di applicare etichette di utilizzo dei dati a set di dati e campi, suddividere in categorie ciascuna in base ai relativi criteri di utilizzo dei dati e valutare la presenza di violazioni dei criteri quando vengono eseguite determinate azioni su tali set di dati e/o campi. Prima di iniziare con le esercitazioni elencate in questo documento, consultate la [[!DNL Data Governance] panoramica](../data-governance/home.md) per un&#39;introduzione più affidabile al framework.

Adobe Experience Platform [!DNL Privacy Service] fornisce un&#39;API RESTful e un&#39;interfaccia utente che consentono di coordinare le richieste di privacy e conformità tra le varie soluzioni. Per saperne di più, si prega di iniziare leggendo la panoramica [](../privacy-service/home.md)Privacy Service.

## Aggiungi etichette di utilizzo dati

Le etichette di utilizzo dei dati consentono di classificare set di dati e campi in base ai criteri di utilizzo applicabili ai dati. Le etichette possono essere applicate in qualsiasi momento, fornendo la flessibilità nella modalità di gestione dei dati. Le best practice incoraggiano i dati di etichettatura non appena vengono ingeriti [!DNL Experience Platform]o non appena i dati diventano disponibili per l&#39;uso in [!DNL Platform]. Le etichette di utilizzo dei dati applicate a livello di dataset vengono propagate a tutti i campi all&#39;interno del dataset. Le etichette possono anche essere applicate direttamente a singoli campi (intestazioni di colonna) di un dataset, senza propagazione. Per informazioni su come applicare le etichette di utilizzo dei dati ai dati, consultare la panoramica [delle etichette di utilizzo dei](../data-governance/labels/overview.md)dati.

## Creazione di criteri di utilizzo dei dati

L&#39; [!DNL Policy Service] API consente di creare e gestire i criteri di utilizzo dei dati per determinare quali azioni di marketing possono essere eseguite rispetto ai dati che contengono determinate etichette di utilizzo. Per iniziare, leggi la panoramica [dei criteri di utilizzo dei](../data-governance/policies/overview.md)dati.

## Applica criteri di utilizzo dei dati

Dopo aver aggiunto le etichette di utilizzo per i dati e aver creato criteri per le azioni di marketing in base a tali etichette, puoi utilizzare il metodo [!DNL Policy Service API] per valutare se un&#39;azione di marketing costituisca una violazione dei criteri quando viene eseguita su un set di dati o su un gruppo arbitrario di etichette di utilizzo. Potete quindi configurare i vostri protocolli interni per gestire le violazioni dei criteri in base alla risposta API. Per iniziare, consulta la panoramica [delle](../data-governance/enforcement/overview.md)attività di applicazione dei criteri.

## Applica la conformità all&#39;utilizzo dei dati per un segmento di pubblico

I segmenti abilitati per l’uso in [!DNL Real-time Customer Profile] contengono un ID criterio di unione all’interno della definizione del segmento. Questo criterio di unione contiene informazioni sui set di dati da includere nel segmento, che a loro volta contengono eventuali etichette di utilizzo dei dati applicabili. Per passaggi specifici relativi all&#39;applicazione della conformità dell&#39;utilizzo dei dati per un segmento di pubblico, segui l&#39;esercitazione sull&#39;applicazione della conformità dell&#39;uso [dei dati per i segmenti](../segmentation/tutorials/governance.md).

## Guida introduttiva a [!DNL Privacy Service]

[!DNL Privacy Service] fornisce un&#39;API RESTful e un&#39;interfaccia utente che consentono di gestire i dati personali degli interessati (clienti) nelle applicazioni Adobe Experience Cloud. [!DNL Privacy Service] fornisce inoltre un meccanismo centrale di controllo e registrazione che consente di accedere allo stato e ai risultati dei processi che coinvolgono [!DNL Experience Cloud] le applicazioni. Per istruzioni su come creare e monitorare [!DNL Privacy Service] i processi, seguite i passaggi forniti nella guida [per gli sviluppatori di](../privacy-service/api/getting-started.md) Privacy Service o nella guida [per gli utenti di](../privacy-service/ui/overview.md)Privacy Service.