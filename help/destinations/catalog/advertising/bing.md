---
keywords: 'pubblicità; bing; '
title: Connessione Microsoft Bing
description: Con la destinazione di connessione Microsoft Bing, è possibile eseguire il retargeting e campagne digitali mirate al pubblico in Microsoft Display Advertising.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: 812688043a7da943832b5798de0f433928634998
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 2%

---

# [!DNL Microsoft Bing] connection {#bing-destination}

## Panoramica {#overview}

La [!DNL Microsoft Bing] La destinazione consente di inviare i dati del profilo a [!DNL Microsoft Display Advertising].

Per inviare i dati del profilo a [!DNL Microsoft Bing], è innanzitutto necessario connettersi alla destinazione.

## Casi d’uso {#use-cases}

In qualità di addetto al marketing, voglio essere in grado di utilizzare segmenti generati da [!DNL Microsoft Advertising IDs] per indirizzare gli utenti tramite display advertising attraverso [!DNL Microsoft Advertising] canali.

## Identità supportate {#supported-identities}

[!DNL Microsoft Bing] supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Descrizione |
|---|---|
| MAID | Microsoft Advertising ID |

{style=&quot;table-layout:auto&quot;}

## Tipo e frequenza di esportazione {#export-type-frequency}

**[!DNL Segment Export]** - stai esportando tutti i membri di un segmento (pubblico) nel [!DNL Microsoft Bing] destinazione.

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione del segmento]** | Stai esportando tutti i membri di un segmento (pubblico) nel [!DNL Microsoft Bing] destinazione. |
| Frequenza delle esportazioni | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Prerequisiti {#prerequisites}

>[!IMPORTANT]
>
>Se desideri creare la tua prima destinazione con [!DNL Microsoft Bing] e non hanno attivato il [Funzionalità di sincronizzazione ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) in Experience Cloud ID Service in passato (con Adobe Audience Manager o altre applicazioni), contatta la Consulenza Adobe o l’Assistenza clienti per abilitare la sincronizzazione degli ID. Se hai già configurato [!DNL Microsoft Bing] integrazioni in Audience Manager, le sincronizzazioni ID impostate riportano su Platform.

Durante la configurazione della destinazione, devi fornire le seguenti informazioni:

* [!UICONTROL ID account]: questo è il tuo [!DNL Bing Ads CID], in formato intero.

## Collegati alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Quando [configurazione](../../ui/connect-destination.md) questa destinazione, devi fornire le seguenti informazioni:

* **[!UICONTROL Nome]**: Nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: Una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID account]**: Le [!DNL Bing Ads CID].

### Abilitare gli avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati nella tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere le notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [iscrizione agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completati i dettagli della connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_bing_mapping_id"
>title="ID mappatura"
>abstract="Immetti l’ID del segmento Bing numerico a cui desideri mappare il segmento selezionato. Se il [!UICONTROL ID mappatura] non corrisponde a un ID segmento nella destinazione Bing, i dati del pubblico previsti non verranno visualizzati nel tuo account Bing."

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Vedi [Attivare i dati del pubblico nelle destinazioni di esportazione dei segmenti in streaming](../../ui/activate-segment-streaming-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

In [Pianificazione del segmento](../../ui/activate-segment-streaming-destinations.md#scheduling) a questo punto, devi mappare manualmente i segmenti sul loro ID segmento numerico corrispondente nella [!DNL Bing] destinazione. Compila l’ID del segmento numerico da [!DNL Bing] in [!UICONTROL ID mappatura] campo .

![Immagine dell’interfaccia utente che mostra la schermata di mappatura dei segmenti con un esempio di ID mappatura Bing](../../assets/catalog/advertising/bing/mapping-id.png)

Se il [!UICONTROL ID mappatura] non corrisponde a un ID segmento nella destinazione Bing, i dati del pubblico previsti non verranno visualizzati nel tuo account Bing.

## Dati esportati {#exported-data}

Per verificare se i dati sono stati esportati correttamente in [!DNL Microsoft Bing] destinazione, controlla il tuo [!DNL Microsoft Bing Ads] conto. Se l&#39;attivazione ha avuto successo, i tipi di pubblico vengono compilati nel tuo account.
