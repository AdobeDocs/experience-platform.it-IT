---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Tutorial sulla governance dei dati e sulla privacy
topic-legacy: tutorial
type: Tutorial
description: Questo documento fornisce una panoramica delle diverse esercitazioni disponibili relative alla governance dei dati di Adobe Experience Platform e ad Adobe Experience Platform Privacy Service.
exl-id: c3cef447-b343-445b-a3ed-54f873f6dfb9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# [!DNL Data Governance] e  [!DNL Privacy] Tutorials

La governance dei dati di Adobe Experience Platform consente di applicare etichette di utilizzo dei dati ai set di dati e ai campi, suddividerle in categorie in base ai criteri di utilizzo dei dati correlati e di valutare le violazioni dei criteri quando vengono eseguite determinate azioni su tali set di dati e/o campi. Prima di iniziare le esercitazioni elencate in questo documento, consulta la sezione [[!DNL Data Governance] panoramica](../data-governance/home.md) per un’introduzione più affidabile al framework.

Adobe Experience Platform [!DNL Privacy Service] fornisce un’API RESTful e un’interfaccia utente che ti consentono di coordinare le richieste di privacy e conformità tra diverse soluzioni. Per ulteriori informazioni, inizia leggendo la [panoramica Privacy Service](../privacy-service/home.md).

## Aggiungi etichette di utilizzo dati

Le etichette di utilizzo dei dati ti consentono di classificare set di dati e campi in base ai criteri di utilizzo applicati a tali dati. Le etichette possono essere applicate in qualsiasi momento, fornendo flessibilità nella scelta della modalità di gestione dei dati. Le best practice incoraggiano l’etichettatura dei dati non appena vengono acquisiti in [!DNL Experience Platform] o non appena i dati diventano disponibili per l’uso in [!DNL Platform]. Le etichette di utilizzo dei dati applicate a livello di set di dati vengono propagate a tutti i campi all’interno del set di dati. Le etichette possono anche essere applicate direttamente ai singoli campi (intestazioni di colonna) di un set di dati, senza propagazione. Per informazioni su come applicare le etichette di utilizzo dei dati ai dati, visita la [panoramica delle etichette di utilizzo dei dati](../data-governance/labels/overview.md).

## Creare criteri di utilizzo dei dati

L’ [!DNL Policy Service] API ti consente di creare e gestire i criteri di utilizzo dei dati per determinare quali azioni di marketing possono essere intraprese rispetto ai dati che contengono determinate etichette di utilizzo. Per iniziare, leggi la [panoramica dei criteri di utilizzo dei dati](../data-governance/policies/overview.md).

## Applica criteri di utilizzo dati

Dopo aver aggiunto le etichette di utilizzo per i dati e aver creato i criteri per le azioni di marketing in base a tali etichette, puoi utilizzare [!DNL Policy Service API] per valutare se un&#39;azione di marketing costituisca una violazione dei criteri quando viene eseguita su un set di dati o su un gruppo arbitrario di etichette di utilizzo. Puoi quindi impostare i tuoi protocolli interni per gestire le violazioni dei criteri in base alla risposta API. Per iniziare, visita la [panoramica sull&#39;applicazione dei criteri](../data-governance/enforcement/overview.md).

## Applicare la conformità in materia di utilizzo dei dati per un segmento di pubblico

I segmenti abilitati per l’uso in [!DNL Real-time Customer Profile] contengono un ID criterio di unione all’interno della relativa definizione del segmento. Questo criterio di unione contiene informazioni sui set di dati da includere nel segmento, che a loro volta contengono eventuali etichette di utilizzo dei dati applicabili. Per passaggi specifici sull&#39;applicazione della conformità per l&#39;utilizzo dei dati per un segmento di pubblico, segui il [tutorial sull&#39;applicazione della conformità per l&#39;utilizzo dei dati per i segmenti](../segmentation/tutorials/governance.md).

## Guida introduttiva di [!DNL Privacy Service]

[!DNL Privacy Service] fornisce un’API RESTful e un’interfaccia utente che consentono di gestire i dati personali delle persone interessate (clienti) nelle applicazioni Adobe Experience Cloud. [!DNL Privacy Service] fornisce inoltre un meccanismo centrale di audit e registrazione che consente di accedere allo stato e ai risultati dei processi che coinvolgono  [!DNL Experience Cloud] le applicazioni. Per istruzioni su come creare e monitorare i processi [!DNL Privacy Service], segui i passaggi descritti nella [guida per gli sviluppatori di Privacy Service](../privacy-service/api/getting-started.md) o nella [guida utente di Privacy Service](../privacy-service/ui/overview.md).
