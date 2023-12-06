---
keywords: pubblicità; bing;
title: Connessione Microsoft Bing
description: Con la destinazione di connessione di Microsoft Bing, puoi eseguire campagne digitali di retargeting e mirate al pubblico in tutta Microsoft Advertising Network, inclusi Display advertising, Search e Native.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: a7dbb5e274058a059ae1231281fd9efd509b029f
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 10%

---

# [!DNL Microsoft Bing] connessione {#bing-destination}

## Panoramica {#overview}

Utilizza il [!DNL Microsoft Bing] destinazione per inviare i dati del profilo all&#39;intero [!DNL Microsoft Advertising Network], tra cui [!DNL Display Advertising], [!DNL Search], e [!DNL Native].

Il [!DNL Microsoft Bing] creazione della destinazione *[!DNL Custom Audiences]* in Microsoft. Questi sono disponibili sia nel [!DNL Microsoft Search Network] e [!DNL Audience Network] ([!DNL Native] /[!DNL Display] /[!DNL Programmatic]) come elencato nella [Documentazione di Microsoft Advertising](https://help.ads.microsoft.com/#apex/ads/en/56892/1-500).

Per inviare i dati del profilo a [!DNL Microsoft Bing], devi prima connetterti alla destinazione.

## Casi d’uso {#use-cases}

In qualità di addetto al marketing, voglio poter utilizzare tipi di pubblico basati su [!DNL Microsoft Advertising IDs] per eseguire il targeting degli utenti tramite display o search advertising su [!DNL Microsoft Advertising] canali.

## Identità supportate {#supported-identities}

[!DNL Microsoft Bing] supporta l’attivazione di tipi di pubblico in base alle identità mostrate nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/namespaces.md).

| Identità | Descrizione |
|---|---|
| DOMESTICA | Microsoft Advertising ID |

{style="table-layout:auto"}

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive il tipo di pubblico che puoi esportare in questa destinazione.

| Origine pubblico | Supportati | Descrizione |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati dall’Experience Platform [Servizio di segmentazione](../../../segmentation/home.md). |
| Caricamenti personalizzati | ✓ | Tipi di pubblico [importato](../../../segmentation/ui/overview.md#import-audience) in Experienci Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

**[!DNL Audience Export]** : stai esportando tutti i membri di un pubblico in [!DNL Microsoft Bing] destinazione.

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione pubblico]** | Stai esportando tutti i membri di un pubblico in [!DNL Microsoft Bing] destinazione. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experienci Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni su [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Prerequisiti {#prerequisites}

>[!IMPORTANT]
>
>Se desideri creare la prima destinazione con [!DNL Microsoft Bing] e non hanno abilitato [Funzionalità di sincronizzazione ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) nel servizio ID Experience Cloud in passato (con Adobe Audience Manager o altre applicazioni), contatta la consulenza o l&#39;assistenza clienti Adobe per abilitare le sincronizzazioni ID. Se in precedenza avevi impostato [!DNL Microsoft Bing] le integrazioni in Audienci Manager, le sincronizzazioni ID configurate vengono trasferite a Platform.

Durante la configurazione della destinazione, devi fornire le seguenti informazioni:

* [!UICONTROL ID account]: questo è il tuo [!DNL Bing Ads CID], in formato numero intero.

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

### Inserire i dettagli della destinazione {#parameters}

Mentre [configurazione](../../ui/connect-destination.md) in questa destinazione, è necessario fornire le seguenti informazioni:

* **[!UICONTROL Nome]**: nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID account]**: il tuo [!DNL Bing Ads Customer ID] (CID) Il tuo CID è un numero intero, trovato nell&#39;URL quando accedi a [!DNL Microsoft Advertising].

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_bing_mapping_id"
>title="ID di mappatura"
>abstract="Immetti l’ID numerico del pubblico Bing su cui desideri mappare il segmento selezionato. Se l’[!UICONTROL ID di mappatura] fornito non corrisponde a un ID di pubblico nella destinazione Bing, i dati del pubblico previsti non verranno visualizzati nel tuo account Bing."

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Consulta [Attiva i dati del pubblico nelle destinazioni di esportazione del pubblico in streaming](../../ui/activate-segment-streaming-destinations.md) per istruzioni sull’attivazione dei tipi di pubblico in questa destinazione.

In [Pianificazione del pubblico](../../ui/activate-segment-streaming-destinations.md#scheduling) passaggio, devi mappare manualmente il nome del pubblico nel [!UICONTROL ID mappatura] campo. In questo modo i metadati del pubblico vengono trasmessi correttamente a [!DNL Bing].

![Immagine dell’interfaccia utente che mostra la schermata di pianificazione del pubblico con un esempio di come mappare il nome del pubblico sull’ID di mappatura Bing.](../../assets/catalog/advertising/bing/mapping-id.png)

## Dati esportati {#exported-data}

Per verificare se i dati sono stati esportati correttamente in [!DNL Microsoft Bing] destinazione, controlla il tuo [!DNL Microsoft Bing Ads] account. Se l&#39;attivazione ha esito positivo, i tipi di pubblico vengono popolati nel tuo account.
