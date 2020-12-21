---
keywords: data governance rtcdp;rtcdp data governance;real time customer data profile data governance
title: Panoramica sulla governance dei dati
seo-title: Governance dei dati in tempo reale della piattaforma dati del cliente
description: 'Data Governance consente di gestire i dati dei clienti e di garantire la conformità a normative, restrizioni e criteri applicabili all''uso dei dati. '
seo-description: 'Data Governance consente di gestire i dati dei clienti e di garantire la conformità a normative, restrizioni e criteri applicabili all''uso dei dati. '
translation-type: tm+mt
source-git-commit: e680191d495e4c33baa8242d40a15b9124eec8cd
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 0%

---


# [!DNL Data Governance] in CDP in tempo reale

[!DNL Real-time Customer Data Platform] (Real-time CDP) unisce i dati provenienti da più sistemi aziendali, consentendo agli esperti di marketing di identificare, comprendere e coinvolgere meglio i clienti. Questi dati possono essere soggetti a restrizioni d&#39;uso definite dalla tua organizzazione o dalle normative legali. Pertanto, è importante assicurarsi che la CDP in tempo reale sia conforme ai criteri di utilizzo quando si gestiscono i dati.

Adobe Experience Platform [!DNL Data Governance] consente di gestire i dati dei clienti e garantire la conformità a normative, restrizioni e criteri applicabili all&#39;uso dei dati. Questo svolge un ruolo chiave all’interno di CDP in tempo reale, consentendo di definire criteri di utilizzo, classificare i dati in base a tali criteri e verificare la presenza di violazioni dei criteri durante l’esecuzione di determinate azioni di marketing.

CDP in tempo reale è basato su Adobe Experience Platform, e pertanto la maggior parte delle funzionalità [!DNL Data Governance] sono descritte nella documentazione di [!DNL Experience Platform]. Questo documento è destinato a completare la [Panoramica sulla governance dei dati](../../data-governance/home.md) per [!DNL Experience Platform] e illustra le funzioni di governance disponibili in CDP in tempo reale. Vengono trattati i seguenti argomenti:

* [Applicazione di etichette di utilizzo ai dati](#labels)
* [Gestire i criteri di utilizzo dei dati](#policies)
* [Applica conformità all&#39;utilizzo dei dati](#enforce)

## Applica etichette di utilizzo ai dati {#labels}

[!DNL Data Governance] consente di applicare etichette di utilizzo ai dati, a livello di dataset o di campo dataset. Le etichette di utilizzo dei dati consentono di classificare i dati in base ai criteri di utilizzo applicati a tali dati.

Per informazioni dettagliate sull&#39;utilizzo delle etichette di utilizzo dei dati, vedere la [guida utente delle etichette di utilizzo dei dati](../../data-governance/labels/overview.md) per Adobe Experience Platform.

## Configurare i casi di utilizzo di marketing per le destinazioni {#destinations}

Puoi impostare le restrizioni di utilizzo dei dati su una destinazione definendo i casi di utilizzo del marketing (o azioni di marketing) per tale destinazione. Un caso di utilizzo marketing per una destinazione indica l&#39;intento dei dati che verranno esportati in quella destinazione.

>[!NOTE]
>
>Per ulteriori informazioni sulle azioni di marketing e il loro utilizzo nei criteri di utilizzo dei dati, consultare la [panoramica dei criteri di utilizzo dei dati](../../data-governance/policies/overview.md) nella [!DNL Experience Platform] documentazione.

La definizione dei casi di utilizzo del marketing sulle destinazioni consente di garantire che tutti i profili o i segmenti inviati a tali destinazioni siano conformi ai criteri di utilizzo dei dati. È pertanto necessario aggiungere alle destinazioni i casi di utilizzo del marketing appropriati in base alle esigenze aziendali per applicare restrizioni all&#39;attivazione.

I casi di utilizzo del marketing possono essere selezionati solo quando si configura una destinazione per la prima volta. A seconda del tipo di destinazione con cui state lavorando, l’opportunità di configurare i casi di utilizzo del marketing verrà visualizzata in punti diversi del flusso di lavoro di configurazione. Per informazioni su come configurare una particolare destinazione, consulta la [documentazione delle destinazioni](../destinations/overview.md).

## Gestisci criteri di utilizzo dei dati {#policies}

Affinché le etichette di utilizzo dei dati supportino efficacemente la conformità dei dati, è necessario definire e abilitare i criteri di utilizzo dei dati. I criteri di utilizzo dei dati sono regole che descrivono i tipi di azioni di marketing consentite o con cui è consentito eseguire attività sui dati all’interno di un CDP in tempo reale. Per ulteriori informazioni, vedere la sezione &quot;Criteri di utilizzo dei dati&quot; in [!DNL Experience Platform] [Panoramica sulla governance dei dati](../../data-governance/home.md).

Adobe Experience Platform fornisce diversi criteri di base per i casi di utilizzo più comuni dell&#39;esperienza cliente. Per visualizzare questi criteri nell&#39;interfaccia utente, passare all&#39;area di lavoro **[!UICONTROL Policies]** e selezionare la scheda **[!UICONTROL Browse]**. Per informazioni dettagliate sull&#39;utilizzo dei criteri nell&#39;interfaccia utente, vedere la [guida utente dei criteri](../../data-governance/policies/user-guide.md) nella [!DNL Experience Platform], inclusa la procedura per l&#39;elaborazione dei criteri personalizzati.

## Applica conformità all&#39;uso dei dati {#enforce}

Una volta etichettati i dati e definiti i criteri di utilizzo, potete applicare la conformità dell&#39;utilizzo dei dati ai criteri. Quando si attivano i segmenti di pubblico verso destinazioni in CDP in tempo reale, [!DNL Data Governance] applica automaticamente i criteri di utilizzo in caso di violazioni.

Per ulteriori informazioni, vedere il documento relativo all&#39; [imposizione automatica dei criteri](../../data-governance/enforcement/auto-enforcement.md).

## Passaggi successivi

Ora che sono state introdotte le funzionalità chiave [!DNL Data Governance] su CDP in tempo reale e come [!DNL Experience Platform] le abilita, proseguire con la [documentazione per la governance dei dati su Adobe Experience Platform](../../data-governance/home.md). La documentazione fornisce panoramiche dei concetti [!DNL Data Governance] essenziali, nonché flussi di lavoro dettagliati per la gestione delle etichette e dei criteri di utilizzo dei dati.

Il seguente video fornisce una panoramica di [!DNL Data Governance] in CDP in tempo reale, con l&#39;utilizzo di casi d&#39;uso di marketing su destinazioni e flussi di lavoro di esempio per diversi scenari:

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)