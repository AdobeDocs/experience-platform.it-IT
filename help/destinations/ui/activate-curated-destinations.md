---
title: Attiva i tipi di pubblico nelle destinazioni curate in base agli identificatori LiveRamp
type: Tutorial
description: Scopri come attivare i tipi di pubblico da Adobe Experience Platform alle destinazioni TV e audio connesse e ad altre integrazioni tramite il RampID LiveRamp.
source-git-commit: 1eb422572d95426fa8b342dc6aa79fb6125e18a1
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 0%

---


# Attiva i tipi di pubblico nelle destinazioni curate in base agli identificatori LiveRamp

Utilizzare l’integrazione di Adobe Real-Time CDP con [!DNL LiveRamp] per attivare dei tipi di pubblico in un elenco curato di destinazioni che utilizzano [!DNL [LiveRamp RampID]](https://docs.liveramp.com/connect/en/interpreting-rampid,-liveramp-s-people-based-identifier.html) per l&#39;attivazione, comprese le destinazioni TV e audio collegate, come quelle elencate di seguito.

>[!IMPORTANT]
>
>Non è necessario acquisire o utilizzare in alcun modo i RampID LiveRamp nell’interfaccia di Experienci Platform.
>
> Puoi esportare identità da Real-Time CDP, come identificatori basati su PII, identificatori noti e ID personalizzati, come descritto nella sezione [Documentazione di LiveRamp](https://docs.liveramp.com/connect/en/identity-and-identifier-terms-and-concepts.html#known-identifiers). Queste identità vengono quindi associate a [!DNL LiveRamp RampIDs] a valle del processo di attivazione.


* [[!DNL 4C Insights]](#insights)
* [[!DNL Acast]](#acast)
* [[!DNL Ampersand.tv]](#ampersand-tv)
* [[!DNL Captify]](#captify)
* [[!DNL Cardlytics]](#cardlytics)
* [[!DNL Disney (Hulu/ESPN/ABC)]](#disney)
* [[!DNL iHeartMedia]](#iheartmedia)
* [[!DNL Index Exchange]](#index-exchange)
* [[!DNL Magnite CTV Platform]](#magnite)
* [[!DNL Magnite DV+ (Rubicon Project)]](#magnite-dv)
* [[!DNL Nexxen]](#nexxen)
* [[!DNL One Fox]](#fox)
* [[!DNL Pandora]](#pandora)
* [[!DNL Reddit]](#reddit)
* [[!DNL Roku]](#roku)
* [[!DNL Spotify]](#spotify)
* [[!DNL Taboola]](#taboola)
* [[!DNL TargetSpot]](#targetspot)
* [[!DNL Teads]](#teads)
* [[!DNL WB Discovery]](#wb-discovery)

Questo articolo spiega il flusso di lavoro necessario per attivare i tipi di pubblico da Real-Time CDP alle destinazioni elencate in precedenza, direttamente dall’interfaccia utente di Real-Time CDP.

## Flusso di lavoro attivazione {#workflow}

È possibile attivare i tipi di pubblico per le destinazioni TV e audio collegate eseguendo un processo in due fasi e utilizzando [LiveRamp - Onboarding](../catalog/advertising/liveramp-onboarding.md) e [LiveRamp - Distribuzione](../catalog/advertising/liveramp-distribution.md) come illustrato nell’immagine seguente.

![Diagramma che mostra il flusso di lavoro per attivare i tipi di pubblico da Real-Time CDP alle destinazioni curate tramite LiveRamp.](../assets/ui/activate-curated-destinations-liveramp/workflow-diagram.png){width="1920" zoomable="yes"}

Innanzitutto, esporta i tipi di pubblico da Real-Time CDP a [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) come file CSV.

Dopo aver esportato i tipi di pubblico, puoi attivarli utilizzando [[!DNL LiveRamp - Distribution]](../catalog/advertising/liveramp-distribution.md) destinazione.

>[!TIP]
>
>Questo processo ti consente di attivare i tipi di pubblico in destinazioni quali [[!DNL Roku]](../catalog/advertising/liveramp-distribution.md#roku), [[!DNL Disney]](../catalog/advertising/liveramp-distribution.md#disney)e molto altro direttamente dall’interfaccia utente di Real-Time CDP, senza dover accedere al [!DNL LiveRamp] account per l&#39;attivazione.

### Esercitazione video {#video}

Guarda il video seguente per una spiegazione end-to-end del flusso di lavoro descritto in questa pagina.

>[!VIDEO](https://video.tv.adobe.com/v/3425367)

### Passaggio 1: invia i tuoi tipi di pubblico da Experienci Platform a LiveRamp, tramite [!DNL LiveRamp - Onboarding] destinazione {#onboarding}

La prima cosa da fare per attivare i tipi di pubblico in destinazioni curate basate su RampID LiveRamp è: **esportare i tipi di pubblico da Experienci Platform a[!DNL LiveRamp]**.

Per farlo, utilizza **[!DNL LiveRamp - Onboarding]** destinazione.

![Experience Platform di immagine dell’interfaccia utente che mostra la scheda LiveRamp - Onboarding destination](../assets/ui/activate-curated-destinations-liveramp/liveramp-onboarding-catalog.png)

Per scoprire come configurare [!DNL LiveRamp - Onboarding] destinazione ed esportare i tipi di pubblico da Experienci Platform, leggi la [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) documentazione di destinazione.

>[!IMPORTANT]
>
>Durante l&#39;esportazione di file in [!DNL LiveRamp - Onboarding] di destinazione, Platform genera un file CSV per ogni [ID criterio di unione](../../profile/merge-policies/overview.md). Consulta la [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) documentazione di destinazione per informazioni dettagliate su come convalidare l&#39;esportazione dei dati in LiveRamp.


Dopo aver esportato correttamente i tipi di pubblico in LiveRamp, continua con [passaggio 2](#distribution).

>[!TIP]
>
>Prima di passare a [passaggio 2](#distribution), [convalida](../catalog/advertising/liveramp-onboarding.md#exported-data) che i tipi di pubblico sono stati esportati correttamente in LiveRamp. Consulta la documentazione su [monitoraggio dei flussi di dati di destinazione](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) e informazioni sui dettagli di monitoraggio specifici per [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md#exported-data).

### Passaggio 2: attiva i tipi di pubblico onboarded sulle destinazioni TV e audio collegate, attraverso il [!DNL LiveRamp - Distribution] destinazione {#distribution}

Dopo aver [convalidato](../catalog/advertising/liveramp-onboarding.md#exported-data) che i tipi di pubblico siano stati esportati correttamente in LiveRamp, è ora di attivarli nelle destinazioni preferite, ad esempio [[!DNL Roku]](../catalog/advertising/liveramp-distribution.md#roku), [[!DNL Disney]](../catalog/advertising/liveramp-distribution.md#disney), e altro ancora.

Attivare i tipi di pubblico (esportati in [passaggio 1](#onboarding)) utilizzando **[!DNL LiveRamp - Distribution]** destinazione.

![Experience Platform di immagine dell’interfaccia utente che mostra la scheda LiveRamp - Distribution destination](../assets/ui/activate-curated-destinations-liveramp/liveramp-distribution-catalog.png)

Per scoprire come configurare **[!DNL LiveRamp - Distribution]** destinazione e attivare i tipi di pubblico esportati in [passaggio 1](#onboarding), leggi [[!DNL LiveRamp - Distribution]](../catalog/advertising/liveramp-distribution.md) documentazione di destinazione.

>[!IMPORTANT]
>
>In **selezione del pubblico** passaggio del **[!DNL LiveRamp - Distribution]** destinazione, è necessario selezionare la *stesso pubblico esatto* che hai esportato in [LiveRamp - Onboarding](../catalog/advertising/liveramp-onboarding.md) destinazione in [passaggio 1](#onboarding).

Quando si configura **[!DNL LiveRamp - Distribution]** destinazione, devi creare una connessione dedicata per ogni destinazione a valle che desideri utilizzare (Roku, Disney e così via).

>[!TIP]
>
>Per la denominazione della destinazione, Adobe consiglia di seguire questo formato: `LiveRamp - Downstream Destination Name`. Questo modello di denominazione consente di identificare rapidamente le destinazioni in [Sfoglia](../ui/destinations-workspace.md#browse) dell’area di lavoro destinazioni.
><br>
>Esempio: `LiveRamp - Roku`.

![Schermata dell’interfaccia utente di Platform che mostra più destinazioni LiveRamp.](../assets/ui/activate-curated-destinations-liveramp/liveramp-naming.png)

## Dati esportati / Convalida esportazione dati {#exported-data}

Per convalidare la corretta esportazione dei tipi di pubblico in [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) destinazione, consulta la documentazione su [monitoraggio dei flussi di dati di destinazione](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) e informazioni sui dettagli di monitoraggio specifici per [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md#exported-data).

Per convalidare la corretta attivazione dei tipi di pubblico nella piattaforma pubblicitaria scelta (ad esempio Roku, Disney e altri), accedi al tuo account della piattaforma di destinazione e controlla le metriche di attivazione.
