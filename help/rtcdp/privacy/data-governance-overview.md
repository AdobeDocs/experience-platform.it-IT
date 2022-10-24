---
keywords: governance dei dati rtcdp;governance dei dati rtcdp;governance dei dati dei profili dei clienti in tempo reale
title: Panoramica sulla governance dei dati
description: La governance dei dati ti consente di gestire i dati dei clienti e di garantire la conformità a normative, restrizioni e criteri applicabili all’utilizzo dei dati.
exl-id: eb501d85-cabd-4667-a1cd-2210ec83fb71
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# Governance dei dati in Real-Time CDP

[!DNL Adobe Real-Time Customer Data Platform] (Real-Time CDP) riunisce i dati di più sistemi aziendali, consentendo agli addetti al marketing di identificare, comprendere e coinvolgere meglio i propri clienti. Questi dati possono essere soggetti a restrizioni di utilizzo definite dalla tua organizzazione o da normative legali. Pertanto, è importante assicurarsi che Real-Time CDP sia conforme ai criteri di utilizzo durante la gestione dei dati.

La governance dei dati di Adobe Experience Platform ti consente di gestire i dati dei clienti e di garantire la conformità a normative, restrizioni e criteri applicabili all’utilizzo dei dati. Questo svolge un ruolo chiave all’interno di Real-Time CDP, consentendoti di definire i criteri di utilizzo, classificare i dati in base a tali criteri e verificare la presenza di violazioni dei criteri durante l’esecuzione di determinate azioni di marketing.

Real-Time CDP è basato su Adobe Experience Platform e pertanto la maggior parte delle funzionalità di governance dei dati è coperta nella [!DNL Experience Platform] documentazione. Il presente documento è inteso a completare [Panoramica sulla governance dei dati](../../data-governance/home.md) per [!DNL Experience Platform]e descrive le funzioni di governance disponibili in Real-Time CDP. Sono trattati i seguenti argomenti:

* [Applicare etichette di utilizzo ai dati](#labels)
* [Gestire i criteri di utilizzo dei dati](#policies)
* [Applica conformità all’utilizzo dei dati](#enforce)

## Applicare etichette di utilizzo ai dati {#labels}

La governance dei dati ti consente di applicare etichette di utilizzo ai dati, a livello di set di dati o di campo di set di dati. Le etichette di utilizzo dei dati ti consentono di classificare i dati in base ai criteri di utilizzo applicati a tali dati.

Per informazioni dettagliate sulle operazioni con le etichette di utilizzo dei dati, consulta la sezione [guida utente delle etichette per l’utilizzo dei dati](../../data-governance/labels/overview.md) per Adobe Experience Platform.

## Configurare le azioni di marketing per le destinazioni {#destinations}

Puoi impostare restrizioni di utilizzo dei dati su una destinazione definendo le azioni di marketing (o casi di utilizzo del marketing) per tale destinazione. Un’azione di marketing per una destinazione indica l’intento dei dati che verranno esportati in tale destinazione.

>[!NOTE]
>
>Per ulteriori informazioni sulle azioni di marketing e sul loro utilizzo nei criteri di utilizzo dei dati, consulta [panoramica dei criteri di utilizzo dei dati](../../data-governance/policies/overview.md) in [!DNL Experience Platform] documentazione.

La definizione delle azioni di marketing sulle destinazioni ti consente di garantire che tutti i profili o segmenti inviati a tali destinazioni siano conformi ai criteri di utilizzo dei dati. È pertanto necessario aggiungere alle destinazioni azioni di marketing appropriate in base alle esigenze dell’organizzazione per applicare restrizioni dei criteri sull’attivazione.

Le azioni di marketing possono essere selezionate solo quando si imposta una destinazione per la prima volta. A seconda del tipo di destinazione con cui stai lavorando, l’opportunità di configurare azioni di marketing verrà visualizzata in diversi punti del flusso di lavoro di configurazione. Consulta la sezione [documentazione sulle destinazioni](../destinations/overview.md) per informazioni su come configurare una destinazione specifica.

## Gestire i criteri di utilizzo dei dati {#policies}

Affinché le etichette per l’utilizzo dei dati supportino efficacemente la conformità dei dati, è necessario definire e abilitare i criteri per l’utilizzo dei dati. I criteri di utilizzo dei dati sono regole che descrivono i tipi di azioni di marketing che possono essere eseguite sui dati in Real-Time CDP o da cui sono previste restrizioni. Consulta la sezione &quot;Criteri di utilizzo dei dati&quot; nella sezione [!DNL Experience Platform] [Panoramica sulla governance dei dati](../../data-governance/home.md) per ulteriori informazioni.

Adobe Experience Platform fornisce diversi criteri di base per i casi d’uso più comuni della customer experience. Questi criteri possono essere visualizzati nell&#39;interfaccia utente passando alla **[!UICONTROL Criteri]** e selezionando la **[!UICONTROL Sfoglia]** scheda . Consulta la sezione [Guida utente ai criteri](../../data-governance/policies/user-guide.md) in [!DNL Experience Platform] documentazione per i passaggi più dettagliati sull&#39;utilizzo dei criteri nell&#39;interfaccia utente, tra cui come creare criteri personalizzati.

## Applica conformità all’utilizzo dei dati {#enforce}

Una volta etichettati i dati e definiti i criteri di utilizzo, puoi applicare la conformità dell’utilizzo dei dati ai criteri. Quando si attivano i segmenti di pubblico sulle destinazioni in Real-Time CDP, la governance dei dati applica automaticamente i criteri di utilizzo in caso di violazioni.

Visualizza il documento in [applicazione automatica delle politiche](../../data-governance/enforcement/auto-enforcement.md) per ulteriori informazioni.

## Passaggi successivi

Ora che sei stato introdotto nelle funzioni chiave di governance dei dati di Real-Time CDP e come [!DNL Experience Platform] consente loro di continuare con [documentazione per la governance dei dati su Adobe Experience Platform](../../data-governance/home.md). La documentazione fornisce panoramiche dei concetti fondamentali sulla governance dei dati, nonché flussi di lavoro dettagliati per la gestione delle etichette e dei criteri di utilizzo dei dati.

Il video seguente fornisce una panoramica sulla governance dei dati in Real-Time CDP, incluso l’utilizzo di casi d’uso di marketing sulle destinazioni e di flussi di lavoro di esempio per diversi scenari:

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)
