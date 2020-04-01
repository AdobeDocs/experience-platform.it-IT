---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Governance dei dati ed esercitazioni sulla privacy
topic: tutorial
translation-type: tm+mt
source-git-commit: ee08f43400fa72abce95ed52aff879f954f4b4d6

---


# Governance dei dati ed esercitazioni sulla privacy

L’etichettatura e l’applicazione dell’uso dei dati (DULE) è il meccanismo fondamentale di governance dei dati della piattaforma Adobe Experience. Le funzioni DULE consentono di applicare etichette di utilizzo dei dati a set di dati e campi, suddividendo ciascuna in categorie in base ai relativi criteri di utilizzo dei dati. Prima di iniziare a utilizzare le etichette, consulta la panoramica [sulla governance dei](../data-governance/home.md) dati per un&#39;introduzione più affidabile al framework DULE all&#39;interno della piattaforma.

Il servizio Adobe Experience Platform Privacy Service fornisce un’API RESTful e un’interfaccia utente che consentono di coordinare le richieste di privacy e conformità tra diverse soluzioni. Per saperne di più, si prega di iniziare leggendo la panoramica [del servizio](../privacy-service/home.md)sulla privacy.

## Aggiungi etichette di utilizzo dati

Le etichette di utilizzo dei dati consentono di classificare set di dati e campi in base ai criteri di utilizzo applicabili ai dati. Le etichette possono essere applicate in qualsiasi momento, fornendo la flessibilità nella modalità di gestione dei dati. Le best practice incoraggiano l’etichettatura dei dati non appena vengono trasferiti nella piattaforma Experience o non appena i dati diventano disponibili per l’uso in tale piattaforma. Le etichette di utilizzo dei dati applicate a livello di dataset vengono propagate a tutti i campi all&#39;interno del dataset. Le etichette possono anche essere applicate direttamente a singoli campi (intestazioni di colonna) di un dataset, senza propagazione. Per informazioni su come applicare le etichette di utilizzo dei dati ai dati, consultare la panoramica [delle etichette di utilizzo dei](../data-governance/labels/overview.md)dati.

## Creazione di criteri di utilizzo dei dati

DULE Policy Service API consente di creare e gestire criteri DULE per determinare quali azioni di marketing possono essere eseguite rispetto ai dati che contengono determinate etichette DULE. Per iniziare, leggi la panoramica [dei criteri di utilizzo dei](../data-governance/policies/overview.md)dati.

## Applica criteri di utilizzo dei dati

Dopo aver creato etichette DUE (Data Usage Labeling and Enforcement) per i dati, e aver creato criteri DULE per le azioni di marketing rispetto a tali etichette, potete utilizzare l&#39;API DULE Policy Service per valutare se un&#39;azione di marketing eseguita su un set di dati o un gruppo arbitrario di etichette DULE costituisce una violazione dei criteri. Potete quindi configurare i vostri protocolli interni per gestire le violazioni dei criteri in base alla risposta API. Per iniziare, consulta la panoramica [delle](../data-governance/enforcement/overview.md)attività di applicazione dei criteri.

## Applica la conformità all&#39;utilizzo dei dati per un segmento di pubblico

I segmenti abilitati per l’uso in Profilo cliente in tempo reale contengono un ID criterio di unione all’interno della definizione del segmento. Questo criterio di unione contiene informazioni sui set di dati da includere nel segmento, che a loro volta contengono eventuali etichette di utilizzo dei dati applicabili. Per passaggi specifici relativi all&#39;applicazione della conformità dell&#39;utilizzo dei dati per un segmento di pubblico, segui l&#39;esercitazione sull&#39;applicazione della conformità dell&#39;uso [dei dati per i segmenti](../segmentation/tutorials/governance.md).

## Guida introduttiva al servizio sulla privacy

Il servizio Privacy fornisce un&#39;API RESTful e un&#39;interfaccia utente che consentono di gestire i dati personali dei tuoi soggetti (clienti) nelle applicazioni Adobe Experience Cloud. Il servizio Privacy fornisce inoltre un meccanismo centrale di controllo e registrazione che consente di accedere allo stato e ai risultati dei processi che coinvolgono le applicazioni Experience Cloud. Per istruzioni su come creare e monitorare i processi relativi al servizio per la privacy, seguite i passaggi forniti nella guida [per gli sviluppatori del servizio](../privacy-service/api/getting-started.md) per la privacy o nella guida [per l&#39;utente del servizio per la](../privacy-service/ui/overview.md)privacy.