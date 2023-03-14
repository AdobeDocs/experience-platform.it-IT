---
keywords: Experience Platform;home;argomenti popolari;connettore di origine Audience Manager;Audience Manager;connettore audience manager
title: Creare una connessione sorgente Adobe Audience Manager nell’interfaccia utente
description: Questo tutorial illustra i passaggi necessari per creare una connessione di origine per Adobe Audience Manager al fine di inserire i dati di Consumer Experience Event in Platform utilizzando l’interfaccia utente.
exl-id: 90c4a719-aaad-4687-afd8-7a1c0c56f744
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---

# Creare una connessione sorgente Adobe Audience Manager nell’interfaccia utente

Questo tutorial illustra i passaggi necessari per creare un connettore di origine per Adobe Audience Manager al fine di inserire i dati di Consumer Experience Event in Platform utilizzando l’interfaccia utente.

## Creare una connessione sorgente con Adobe Audience Manager

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Il [!UICONTROL Catalogo] Nella schermata vengono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la fonte specifica che si desidera utilizzare utilizzando la barra di ricerca.

Sotto [!UICONTROL Applicazione Adobe], seleziona **[!UICONTROL Adobe Audience Manager]** e quindi seleziona **[!UICONTROL Configurazione]**.

![catalogo](../../../../images/tutorials/create/aam/catalog.png)

### Seleziona caratteristiche e segmenti

>[!NOTE]
>
>Non è possibile acquisire dati regionali dall’origine dell’Audience Manager all’Experience Platform. In presenza di casi di utilizzo di Analytics che richiedono dati regionali, utilizza [Connettore di origine di Analytics](../adobe-applications/analytics.md).

Il [!UICONTROL Seleziona caratteristiche e segmenti] viene visualizzato un passaggio che offre un’interfaccia interattiva per esplorare e selezionare caratteristiche, segmenti e dati.

* Il pannello a sinistra dell’interfaccia contiene [!UICONTROL Seleziona caratteristiche e segmenti] nonché una directory gerarchica di tutti i segmenti disponibili.
* La metà destra dell’interfaccia ti consente di interagire con i segmenti selezionati e di selezionare i dati specifici che desideri utilizzare.

![add-data](../../../../images/tutorials/create/aam/add-data.png)

Per spostarti tra i segmenti disponibili, seleziona la cartella a cui desideri accedere da [!UICONTROL Tutti i segmenti] pannello. Selezionando una cartella puoi scorrere la gerarchia di una cartella e ottenere un elenco dei segmenti da filtrare.

![segment-folder](../../../../images/tutorials/create/aam/segment-folder.png)

Dopo aver identificato e selezionato i segmenti che desideri utilizzare, a destra viene visualizzato un nuovo pannello che mostra l’elenco degli elementi selezionati. Puoi continuare ad accedere a diverse cartelle e selezionare diversi segmenti per la connessione. Selezionando altri segmenti si aggiorna il pannello a destra.

![select-data](../../../../images/tutorials/create/aam/select-data.png)

In alternativa, è possibile selezionare **[!UICONTROL Seleziona tutti i segmenti]** e **[!UICONTROL Seleziona tutte le caratteristiche]** scatole. La selezione di tutti i segmenti porterà i segmenti Audience Manager in Platform, mentre la selezione di tutte le caratteristiche abilita tutte le caratteristiche di prime parti da Audience Manager.

>[!WARNING]
>
>L’acquisizione di popolazioni di segmenti Audience Manager di dimensioni considerevoli ha un impatto diretto sul conteggio totale dei profili quando invii un segmento di Audience Manager a Platform per la prima volta utilizzando l’origine di Audience Manager. Ciò significa che la selezione di tutti i segmenti può potenzialmente causare un conteggio dei profili superiore al limite di utilizzo della licenza consentito. Rivedi il [quota di utilizzo licenza](../../../../../dashboards/guides/license-usage.md) prima di procedere.

Al termine, seleziona **[!UICONTROL Successivo]**

![tutti i segmenti](../../../../images/tutorials/create/aam/all-segments.png)

Il [!UICONTROL Revisione] viene visualizzato un passaggio che consente di esaminare le caratteristiche e i segmenti selezionati prima che siano connessi a Platform. I dettagli sono raggruppati nelle seguenti categorie:

* **[!UICONTROL Connessione]**: mostra la piattaforma di origine e lo stato della connessione.
* **[!UICONTROL Dati selezionati]**: mostra il numero di segmenti selezionati e le caratteristiche abilitate.

![recensione](../../../../images/tutorials/create/aam/review.png)

Dopo aver rivisto il flusso di dati, seleziona **[!UICONTROL Fine]** e lascia un po’ di tempo per creare il flusso di dati.

## Passaggi successivi

Quando un flusso di dati di Audience Manager è attivo, i dati in arrivo vengono acquisiti automaticamente nei Profili cliente in tempo reale. Ora puoi utilizzare i dati in arrivo e creare segmenti di pubblico utilizzando il servizio di segmentazione di Platform. Per ulteriori informazioni, consulta i seguenti documenti:

* [Panoramica del profilo cliente in tempo reale](../../../../../profile/home.md)
* [Panoramica del servizio di segmentazione](../../../../../segmentation/home.md)
