---
keywords: governance dei dati rtcdp;rtcdp governance dei dati;governance dei dati dei clienti in tempo reale
title: Panoramica sulla governance dei dati
description: La governance dei dati consente di gestire i dati dei clienti e garantire la conformità alle normative, alle restrizioni e alle politiche applicabili all’utilizzo dei dati.
exl-id: eb501d85-cabd-4667-a1cd-2210ec83fb71
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# Governance dei dati in Real-Time CDP

[!DNL Adobe Real-Time Customer Data Platform] (Real-Time CDP) riunisce dati provenienti da più sistemi aziendali, consentendo agli addetti al marketing di identificare, comprendere e coinvolgere meglio i propri clienti. Questi dati possono essere soggetti a restrizioni d’uso definite dalla tua organizzazione o da normative legali. Pertanto, è importante assicurarsi che Real-Time CDP sia conforme ai criteri di utilizzo durante la gestione dei dati.

La governance dei dati di Adobe Experience Platform consente di gestire i dati dei clienti e di garantire la conformità alle normative, alle restrizioni e alle politiche applicabili all’utilizzo dei dati. Svolge un ruolo chiave in Real-Time CDP, consentendoti di definire i criteri di utilizzo, classificare i dati in base a tali criteri e verificare la presenza di violazioni dei criteri durante l’esecuzione di determinate azioni di marketing.

Real-Time CDP è basato su Adobe Experience Platform e pertanto la maggior parte delle funzionalità di governance dei dati sono coperte nel [!DNL Experience Platform] documentazione. Il presente documento integra il [Panoramica sulla governance dei dati](../../data-governance/home.md) per [!DNL Experience Platform], e delinea le funzioni di governance disponibili in Real-Time CDP. Sono trattati i seguenti argomenti:

* [Applicare le etichette di utilizzo ai dati](#labels)
* [Gestire i criteri di utilizzo dei dati](#policies)
* [Applicazione della conformità all’utilizzo dei dati](#enforce)

## Applicare le etichette di utilizzo ai dati {#labels}

La governance dei dati consente di applicare etichette di utilizzo ai dati, a livello di set di dati o di campo set di dati. Le etichette di utilizzo dei dati consentono di categorizzare i dati in base ai criteri di utilizzo applicabili a tali dati.

Per informazioni dettagliate sull’utilizzo delle etichette di utilizzo dei dati, consulta [guida utente delle etichette di utilizzo dati](../../data-governance/labels/overview.md) per Adobe Experience Platform.

## Configurare azioni di marketing per le destinazioni {#destinations}

Puoi impostare restrizioni sull’utilizzo dei dati per una destinazione definendo azioni di marketing (dette anche casi di utilizzo di marketing) per tale destinazione. Un’azione di marketing per una destinazione indica l’intento dei dati che verranno esportati in tale destinazione.

>[!NOTE]
>
>Per ulteriori informazioni sulle azioni di marketing e sul loro utilizzo nei criteri di utilizzo dei dati, consulta [panoramica dei criteri di utilizzo dei dati](../../data-governance/policies/overview.md) nel [!DNL Experience Platform] documentazione.

La definizione delle azioni di marketing sulle destinazioni ti consente di garantire che tutti i profili o i segmenti inviati a tali destinazioni siano conformi ai criteri di utilizzo dei dati. Pertanto, devi aggiungere alle destinazioni le azioni di marketing appropriate in base alle esigenze della tua organizzazione per applicare le restrizioni dei criteri all’attivazione.

Le azioni di marketing possono essere selezionate solo al primo avvio della configurazione di una destinazione. A seconda del tipo di destinazione con cui stai lavorando, l’opportunità di configurare le azioni di marketing verrà visualizzata in punti diversi nel flusso di lavoro di configurazione. Consulta la [documentazione sulle destinazioni](../destinations/overview.md) per i passaggi su come configurare una particolare destinazione.

## Gestire i criteri di utilizzo dei dati {#policies}

Affinché le etichette di utilizzo dei dati supportino in modo efficace la conformità, è necessario definire e abilitare i criteri di utilizzo dei dati. I criteri di utilizzo dei dati sono regole che descrivono i tipi di azioni di marketing che possono essere eseguiti o meno sui dati in Real-Time CDP. Consulta la sezione &quot;Criteri di utilizzo dei dati&quot; in [!DNL Experience Platform] [Panoramica sulla governance dei dati](../../data-governance/home.md) per ulteriori informazioni.

Adobe Experience Platform fornisce diversi criteri di base per i casi d’uso comuni relativi all’esperienza del cliente. Questi criteri possono essere visualizzati nell’interfaccia utente navigando su **[!UICONTROL Criteri]** e selezionando la **[!UICONTROL Sfoglia]** scheda. Consulta la [guida utente sui criteri](../../data-governance/policies/user-guide.md) nel [!DNL Experience Platform] documentazione relativa ai passaggi più dettagliati sull’utilizzo dei criteri nell’interfaccia utente di, tra cui come creare criteri personalizzati.

## Applicazione della conformità all’utilizzo dei dati {#enforce}

Una volta etichettati i dati e definiti i criteri di utilizzo, puoi applicare la conformità dell’utilizzo dei dati ai criteri. Quando si attivano i segmenti di pubblico nelle destinazioni in Real-Time CDP, la governance dei dati applica automaticamente i criteri di utilizzo nel caso in cui si verifichino violazioni.

Vedi il documento su [applicazione automatica delle policy](../../data-governance/enforcement/auto-enforcement.md) per ulteriori informazioni.

## Passaggi successivi

Ora che hai ricevuto informazioni sulle funzioni chiave di governance dei dati in Real-Time CDP e come [!DNL Experience Platform] , continuare con il [Documentazione per la governance dei dati su Adobe Experience Platform](../../data-governance/home.md). La documentazione fornisce panoramiche dei concetti essenziali di governance dei dati, nonché flussi di lavoro dettagliati per la gestione di etichette e criteri di utilizzo dei dati.

Il video seguente offre una panoramica della governance dei dati in Real-Time CDP, incluso l’utilizzo di casi di utilizzo di marketing sulle destinazioni e flussi di lavoro di esempio per diversi scenari:

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)
