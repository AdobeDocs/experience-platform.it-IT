---
keywords: Experience Platform;home;argomenti comuni;Data Landing Zone;data landing zone
title: Collegare l’area di destinazione dei dati alla piattaforma utilizzando l’interfaccia utente
description: Scopri come creare un connettore sorgente dell’area di destinazione dei dati utilizzando l’interfaccia utente di Platform.
exl-id: 653c9958-5d89-4b0c-af3d-a3e74aa47a08
source-git-commit: fb16ea940ef394a15dd24fe703239b4487fafb18
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 0%

---

# Connetti [!DNL Data Landing Zone] su Platform tramite l’interfaccia utente

[!DNL Data Landing Zone] è una struttura di archiviazione file sicura basata su cloud per l’importazione di file in Adobe Experience Platform. I dati vengono eliminati automaticamente dal [!DNL Data Landing Zone] dopo sette giorni.

Questa esercitazione fornisce i passaggi per la creazione di un [!DNL Data Landing Zone] connessione sorgente tramite l’interfaccia utente di Platform.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): L’Experience Platform consente di acquisire dati da varie sorgenti e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

## Porta i file da [!DNL Data Landing Zone] su Platform

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla navigazione a sinistra per accedere al [!UICONTROL Origini] workspace. La [!UICONTROL Catalogo] in questa schermata vengono visualizzate diverse sorgenti con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando la barra di ricerca.

Sotto la [!UICONTROL archiviazione cloud] categoria, seleziona [!DNL Data Landing Zone] quindi seleziona **[!UICONTROL Aggiungi dati]**.

![catalogo](../../../../images/tutorials/create/dlz/catalog.png)

La [!UICONTROL Aggiungi dati] viene visualizzato un passaggio che fornisce un’interfaccia per selezionare e visualizzare in anteprima i dati da portare in Platform.

* La parte sinistra dell’interfaccia è un browser delle cartelle che fornisce un elenco di file dal contenitore che puoi portare in Platform.
* La parte destra dell’interfaccia ti consente di visualizzare in anteprima fino a 100 righe di dati da un file compatibile.

Seleziona il file da portare in Platform e consenti l’aggiornamento dell’interfaccia corretta in una schermata di anteprima.

![add-data](../../../../images/tutorials/create/dlz/add-data.png)

>[!TIP]
>
>Platform rileva automaticamente le informazioni sulle proprietà del file selezionato, incluse informazioni sul formato dei dati del file, sul delimitatore di colonna designato e sul tipo di compressione.

L’interfaccia di anteprima ti consente di esaminare il contenuto e la struttura di un file. Per impostazione predefinita, l’interfaccia di anteprima visualizza il primo file nella cartella selezionata.

Per visualizzare un’anteprima di un file diverso, seleziona l’icona di anteprima accanto al nome del file da esaminare.

Al termine, seleziona **[!UICONTROL Successivo]**.

![rilevamento file](../../../../images/tutorials/create/dlz/file-detection.png)

Per una guida dettagliata e dettagliata su come creare un flusso di dati per un’origine di archiviazione cloud, consulta l’esercitazione su [creazione di un flusso di dati di archiviazione cloud per trasferire i dati a Platform](../../dataflow/batch/cloud-storage.md).

## Recupera e aggiorna il tuo [!DNL Data Landing Zone] credenziali

[!DNL Data Landing Zone] è un&#39;origine preconfigurata fornita con la licenza Adobe Experience Platform Sources. [!DNL Data Landing Zone] utilizza un’autenticazione basata su URI SAS e token SAS. Puoi recuperare e aggiornare le credenziali di autenticazione dal [!UICONTROL Catalogo origini] pagina.

In [!UICONTROL Catalogo origini], [!UICONTROL archiviazione cloud] , seleziona i puntini di sospensione (**...**) dal **[!UICONTROL Zona di destinazione dei dati]** il Card. Dal menu a discesa visualizzato, seleziona **[!UICONTROL Visualizza credenziali]**.

![options](../../../../images/tutorials/create/dlz/options.png)

Viene visualizzato un puntatore che mostra il nome del contenitore, il token SAS, il nome dell&#39;account di archiviazione e l&#39;URI SAS.

Seleziona **[!UICONTROL Aggiorna credenziali]** e consenti l&#39;elaborazione di alcune credenziali aggiornate per alcuni secondi.

>[!TIP]
>
>Le [!DNL Data Landing Zone] le credenziali sono impostate per la scadenza automatica dopo 90 giorni ed è necessario utilizzare nuove credenziali per riconnettersi a [!DNL Data Landing Zone] dopo la scadenza. I flussi di dati in Platform non sono influenzati dalla scadenza delle credenziali e puoi continuare a lavorare con flussi di dati nuovi ed esistenti con le nuove credenziali.

![view-credentials](../../../../images/tutorials/create/dlz/credentials.png)

## Passaggi successivi

Seguendo questa esercitazione, hai effettuato l’accesso al tuo [!DNL Data Landing Zone] e ha imparato a recuperare e aggiornare le credenziali. Ora puoi passare all’esercitazione successiva su [creazione di un flusso di dati per trasferire i dati da un archivio cloud a Platform](../../dataflow/batch/cloud-storage.md).
