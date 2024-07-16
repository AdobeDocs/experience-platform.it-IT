---
title: Attiva i tipi di pubblico nelle destinazioni curate in base agli identificatori LiveRamp
type: Tutorial
description: Scopri come attivare i tipi di pubblico da Adobe Experience Platform alle destinazioni TV e audio connesse e ad altre integrazioni tramite il RampID LiveRamp.
exl-id: 37e5bab9-588f-40b3-b65b-68f1a4b868f1
source-git-commit: c2e308b5e743f07062be9a34e23c4bc700b27463
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---

# Attiva i tipi di pubblico nelle destinazioni curate in base agli identificatori LiveRamp

Utilizza l&#39;integrazione di Adobe Real-Time CDP con [!DNL LiveRamp] per attivare i tipi di pubblico in un elenco curato di destinazioni che utilizzano [!DNL [LiveRamp RampID]](https://docs.liveramp.com/connect/en/interpreting-rampid,-liveramp-s-people-based-identifier.html) per l&#39;attivazione, incluse le destinazioni TV e audio connesse, come quelle elencate di seguito.

>[!IMPORTANT]
>
>Non è necessario acquisire o utilizzare in alcun modo i RampID LiveRamp nell’interfaccia di Experience Platform.
>
> Puoi esportare le identità da Real-Time CDP, ad esempio identificatori basati su PII, identificatori noti e ID personalizzati, come descritto nella [documentazione LiveRamp](https://docs.liveramp.com/connect/en/identity-and-identifier-terms-and-concepts.html#known-identifiers) ufficiale. Queste identità vengono quindi associate a [!DNL LiveRamp RampIDs] più a valle nel processo di attivazione.


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

Puoi attivare i tipi di pubblico per le destinazioni TV e audio connesse seguendo un processo in due fasi e utilizzando le destinazioni [LiveRamp - Onboarding](../catalog/advertising/liveramp-onboarding.md) e [LiveRamp - Distribuzione](../catalog/advertising/liveramp-distribution.md), come illustrato nell&#39;immagine seguente.

![Diagramma che mostra il flusso di lavoro per attivare i tipi di pubblico da Real-Time CDP alle destinazioni curate tramite LiveRamp.](../assets/ui/activate-curated-destinations-liveramp/workflow-diagram.png){width="1920" zoomable="yes"}

Esportare innanzitutto i tipi di pubblico da Real-Time CDP nella destinazione [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) come file CSV.

Dopo aver esportato i tipi di pubblico, attivarli utilizzando la destinazione [[!DNL LiveRamp - Distribution]](../catalog/advertising/liveramp-distribution.md).

>[!TIP]
>
>Questo processo consente di attivare i tipi di pubblico in destinazioni quali [[!DNL Roku]](../catalog/advertising/liveramp-distribution.md#roku), [[!DNL Disney]](../catalog/advertising/liveramp-distribution.md#disney) e altre direttamente dall&#39;interfaccia utente di Real-Time CDP, senza dover accedere all&#39;account [!DNL LiveRamp] per l&#39;attivazione.

### Esercitazione video {#video}

Guarda il video seguente per una spiegazione end-to-end del flusso di lavoro descritto in questa pagina.

>[!VIDEO](https://video.tv.adobe.com/v/3425367)

### Passaggio 1: invia i tuoi tipi di pubblico da Experience Platform a LiveRamp, tramite la destinazione [!DNL LiveRamp - Onboarding] {#onboarding}

Per attivare i tipi di pubblico in destinazioni curate basate su RampID LiveRamp, devi innanzitutto **esportare i tipi di pubblico da Experience Platform a[!DNL LiveRamp]**.

A tale scopo, utilizzare la destinazione **[!DNL LiveRamp - Onboarding]**.

![Experience Platform di immagine dell&#39;interfaccia utente che mostra la scheda LiveRamp - Onboarding destinazione](../assets/ui/activate-curated-destinations-liveramp/liveramp-onboarding-catalog.png)

Per informazioni su come configurare la destinazione [!DNL LiveRamp - Onboarding] ed esportare i tipi di pubblico da Experience Platform, consulta la documentazione della destinazione [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md).

>[!IMPORTANT]
>
>Durante l&#39;esportazione dei file nella destinazione [!DNL LiveRamp - Onboarding], Platform genera un file CSV per ogni [ID del criterio di unione](../../profile/merge-policies/overview.md). Per informazioni dettagliate su come convalidare l&#39;esportazione dei dati in LiveRamp, consulta la documentazione della destinazione [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md).


Dopo aver esportato correttamente i tipi di pubblico in LiveRamp, continua con il [passaggio 2](#distribution).

>[!TIP]
>
>Prima di passare al [passaggio 2](#distribution), [verifica](../catalog/advertising/liveramp-onboarding.md#exported-data) che i tipi di pubblico siano stati esportati correttamente in LiveRamp. Consulta la documentazione sui [flussi di dati di destinazione di monitoraggio](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) e leggi i dettagli di monitoraggio specifici per [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md#exported-data).

### Passaggio 2: attiva i tipi di pubblico onboarded nelle destinazioni TV e audio connesse, tramite la destinazione [!DNL LiveRamp - Distribution] {#distribution}

Dopo aver [convalidato](../catalog/advertising/liveramp-onboarding.md#exported-data) che i tipi di pubblico sono stati esportati correttamente in LiveRamp, è ora di attivare i tipi di pubblico nelle destinazioni preferite, ad esempio [[!DNL Roku]](../catalog/advertising/liveramp-distribution.md#roku), [[!DNL Disney]](../catalog/advertising/liveramp-distribution.md#disney) e altro ancora.

È possibile attivare i tipi di pubblico (esportati nel [passaggio 1](#onboarding)) utilizzando la destinazione **[!DNL LiveRamp - Distribution]**.

![Immagine dell&#39;interfaccia utente di Experience Platform che mostra la scheda LiveRamp - Distribution destination](../assets/ui/activate-curated-destinations-liveramp/liveramp-distribution-catalog.png)

Per informazioni su come configurare la destinazione **[!DNL LiveRamp - Distribution]** e attivare i tipi di pubblico esportati nel [passaggio 1](#onboarding), leggere la documentazione della destinazione [[!DNL LiveRamp - Distribution]](../catalog/advertising/liveramp-distribution.md).

>[!IMPORTANT]
>
>Nel passaggio **selezione pubblico** della destinazione **[!DNL LiveRamp - Distribution]**, devi selezionare i *tipi di pubblico identici* che hai esportato nella destinazione [LiveRamp - Onboarding](../catalog/advertising/liveramp-onboarding.md) in [passaggio 1](#onboarding).

Quando configuri la destinazione **[!DNL LiveRamp - Distribution]**, devi creare una connessione dedicata per ogni destinazione a valle che desideri utilizzare (Roku, Disney e così via).

>[!TIP]
>
>Per la denominazione della destinazione, l&#39;Adobe consiglia di usare questo formato: `LiveRamp - Downstream Destination Name`. Questo modello di denominazione consente di identificare rapidamente le destinazioni nella scheda [Sfoglia](../ui/destinations-workspace.md#browse) dell&#39;area di lavoro delle destinazioni.
><br>
>Esempio: `LiveRamp - Roku`.

![Schermata dell&#39;interfaccia utente di Platform che mostra più destinazioni LiveRamp.](../assets/ui/activate-curated-destinations-liveramp/liveramp-naming.png)

## Dati esportati / Convalida esportazione dati {#exported-data}

Per convalidare la corretta esportazione dei tipi di pubblico nella destinazione [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md), consulta la documentazione sui [flussi di dati di destinazione di monitoraggio](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) e leggi i dettagli di monitoraggio specifici per [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md#exported-data).

Per convalidare la corretta attivazione dei tipi di pubblico nella piattaforma pubblicitaria scelta (ad esempio Roku, Disney e altri), accedi al tuo account della piattaforma di destinazione e controlla le metriche di attivazione.
