---
keywords: governance dei dati rtcdp;rtcdp governance dei dati;governance dei dati dei clienti in tempo reale
title: Panoramica sulla governance dei dati
description: La governance dei dati consente di gestire i dati dei clienti e garantire la conformità alle normative, alle restrizioni e alle politiche applicabili all’utilizzo dei dati.
feature: Get Started, Data Governance
exl-id: eb501d85-cabd-4667-a1cd-2210ec83fb71
source-git-commit: 82535ec3ac2dd27e685bb591fdf661d3ab5dd2c9
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 3%

---

# Governance dei dati in Real-Time CDP

[!DNL Adobe Real-Time Customer Data Platform] (Real-Time CDP) riunisce dati provenienti da più sistemi aziendali, consentendo agli addetti al marketing di identificare, comprendere e coinvolgere meglio i propri clienti. Questi dati possono essere soggetti a restrizioni di utilizzo definite dalla tua organizzazione o da normative legali. Pertanto, è importante assicurarsi che Real-Time CDP sia conforme ai criteri di utilizzo durante la gestione dei dati.

La governance dei dati di Adobe Experience Platform consente di gestire i dati dei clienti e di garantire la conformità alle normative, alle restrizioni e alle politiche applicabili all’utilizzo dei dati. Svolge un ruolo chiave in Real-Time CDP, consentendoti di definire i criteri di utilizzo, classificare i dati in base a tali criteri e verificare la presenza di violazioni dei criteri durante l’esecuzione di determinate azioni di marketing.

Real-Time CDP è basato su Adobe Experience Platform, pertanto la maggior parte delle funzionalità di governance dei dati sono descritte nella documentazione di [!DNL Experience Platform]. Questo documento integra la [Panoramica sulla governance dei dati](../../data-governance/home.md) per [!DNL Experience Platform] e illustra le funzioni di governance disponibili in Real-Time CDP. Sono trattati i seguenti argomenti:

* [Applicare le etichette di utilizzo ai dati](#labels)
* [Gestire i criteri di utilizzo dei dati](#policies)
* [Applicazione della conformità all’utilizzo dei dati](#enforce)

## Applicare le etichette di utilizzo ai dati {#labels}

La governance dei dati consente di applicare etichette di utilizzo ai dati, a livello di set di dati o di campo set di dati. Le etichette di utilizzo dei dati consentono di categorizzare i dati in base ai criteri di utilizzo applicabili a tali dati.

Per informazioni dettagliate sull&#39;utilizzo delle etichette di utilizzo dati, vedere la [guida utente delle etichette di utilizzo dati](../../data-governance/labels/overview.md) per Adobe Experience Platform.

## Configurare azioni di marketing per le destinazioni {#destinations}

Puoi impostare restrizioni sull’utilizzo dei dati per una destinazione definendo azioni di marketing (dette anche casi di utilizzo di marketing) per tale destinazione. Un’azione di marketing per una destinazione indica l’intento dei dati che verranno esportati in tale destinazione.

>[!NOTE]
>
>Per ulteriori informazioni sulle azioni di marketing e sul loro utilizzo nei criteri di utilizzo dei dati, consulta la [panoramica dei criteri di utilizzo dei dati](../../data-governance/policies/overview.md) nella documentazione di [!DNL Experience Platform].

La definizione delle azioni di marketing sulle destinazioni ti consente di garantire che tutti i profili o i tipi di pubblico inviati a tali destinazioni siano conformi ai criteri di utilizzo dei dati. Pertanto, devi aggiungere alle destinazioni le azioni di marketing appropriate in base alle esigenze della tua organizzazione per applicare le restrizioni dei criteri all’attivazione.

Le azioni di marketing possono essere selezionate solo al primo avvio della configurazione di una destinazione. A seconda del tipo di destinazione con cui stai lavorando, l’opportunità di configurare le azioni di marketing verrà visualizzata in punti diversi nel flusso di lavoro di configurazione. Consulta la documentazione sulle [destinazioni](../destinations/overview.md) per i passaggi su come configurare una destinazione specifica.

## Gestire i criteri di utilizzo dei dati {#policies}

Affinché le etichette di utilizzo dei dati supportino in modo efficace la conformità, è necessario definire e abilitare i criteri di utilizzo dei dati. I criteri di utilizzo dei dati sono regole che descrivono i tipi di azioni di marketing che possono essere eseguiti o meno sui dati in Real-Time CDP. Per ulteriori informazioni, vedere la sezione relativa ai criteri di utilizzo dei dati nella [!DNL Experience Platform] [Panoramica sulla governance dei dati](../../data-governance/home.md).

Adobe Experience Platform fornisce diversi criteri di base per i casi d’uso comuni relativi all’esperienza del cliente. Questi criteri possono essere visualizzati nell&#39;interfaccia utente passando all&#39;area di lavoro **[!UICONTROL Criteri]** e selezionando la scheda **[!UICONTROL Sfoglia]**. Consulta la [guida utente per i criteri](../../data-governance/policies/user-guide.md) nella documentazione di [!DNL Experience Platform] per i passaggi più dettagliati sull&#39;utilizzo dei criteri nell&#39;interfaccia utente, incluso come creare criteri personalizzati.

## Applicazione della conformità all’utilizzo dei dati {#enforce}

Una volta etichettati i dati e definiti i criteri di utilizzo, puoi applicare la conformità dell’utilizzo dei dati ai criteri. Quando si attivano i tipi di pubblico nelle destinazioni in Real-Time CDP, la governance dei dati applica automaticamente i criteri di utilizzo nel caso in cui si verifichino violazioni.

Per ulteriori informazioni, consulta il documento sull&#39;[applicazione automatica dei criteri](../../data-governance/enforcement/auto-enforcement.md).

## Passaggi successivi

Dopo aver appreso le funzionalità chiave per la governance dei dati in Real-Time CDP e come [!DNL Experience Platform] le abilita, continua con la [documentazione per la governance dei dati in Adobe Experience Platform](../../data-governance/home.md). La documentazione fornisce panoramiche dei concetti essenziali di governance dei dati, nonché flussi di lavoro dettagliati per la gestione di etichette e criteri di utilizzo dei dati.

Il video seguente offre una panoramica della governance dei dati in Real-Time CDP, incluso l’utilizzo di casi di utilizzo di marketing sulle destinazioni e flussi di lavoro di esempio per diversi scenari:

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)
