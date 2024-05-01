---
title: Collegare Data Landing Zone a Platform tramite l’interfaccia utente
description: Scopri come creare un connettore di origine per la Data Landing Zone utilizzando l’interfaccia utente di Platform.
exl-id: 653c9958-5d89-4b0c-af3d-a3e74aa47a08
source-git-commit: 22f3b76c02e641d2f4c0dd7c0e5cc93038782836
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---

# Connetti [!DNL Data Landing Zone] a Platform tramite l’interfaccia utente

>[!IMPORTANT]
>
>Questa pagina è specifica per [!DNL Data Landing Zone] *sorgente* connettore in Experience Platform. Per informazioni sulla connessione al [!DNL Data Landing Zone] *destinazione* connettore, fare riferimento al [[!DNL Data Landing Zone] pagina della documentazione di destinazione](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] è una struttura di archiviazione dei file sicura e basata su cloud per importare i file in Adobe Experience Platform. I dati vengono eliminati automaticamente dal [!DNL Data Landing Zone] dopo sette giorni.

Questo tutorial descrive i passaggi necessari per creare [!DNL Data Landing Zone] tramite l’interfaccia utente di Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../../../home.md): un Experience Platform consente di acquisire dati da varie origini, consentendoti allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experienci Platform fornisce sandbox virtuali che permettono di suddividere una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

## Porta i file da [!DNL Data Landing Zone] alla piattaforma

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Il [!UICONTROL Catalogo] Nella schermata vengono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la fonte specifica che si desidera utilizzare utilizzando la barra di ricerca.

Sotto [!UICONTROL archiviazione cloud] categoria, seleziona [!DNL Data Landing Zone] e quindi seleziona **[!UICONTROL Aggiungi dati]**.

![Catalogo delle origini con Data Landing Zone selezionato.](../../../../images/tutorials/create/dlz/catalog.png)

Il [!UICONTROL Aggiungi dati] viene visualizzata un’interfaccia per selezionare e visualizzare in anteprima i dati da portare su Platform.

* La parte sinistra dell’interfaccia è un browser di cartelle che ti fornisce un elenco di file dal contenitore da portare su Platform.
* La parte destra dell’interfaccia consente di visualizzare in anteprima fino a 100 righe di dati da un file compatibile.

Seleziona il file da portare in Experience Platform e attendi alcuni istanti prima che l’interfaccia corretta venga aggiornata in una schermata di anteprima.

![Interfaccia per l&#39;aggiunta di dati dell&#39;area di lavoro origini.](../../../../images/tutorials/create/dlz/add-data.png)

>[!TIP]
>
>Platform rileva automaticamente le informazioni sulle proprietà del file selezionato, incluse informazioni sul formato dei dati del file, sul delimitatore di colonna designato e sul tipo di compressione.

L’interfaccia di anteprima consente di esaminare il contenuto e la struttura di un file. Per impostazione predefinita, nell&#39;interfaccia di anteprima viene visualizzato il primo file della cartella selezionata.

Per visualizzare in anteprima un file diverso, selezionate l&#39;icona di anteprima accanto al nome del file da esaminare.

Al termine, seleziona **[!UICONTROL Successivo]**.

![Pagina di anteprima dei dati dell&#39;area di lavoro origini.](../../../../images/tutorials/create/dlz/file-detection.png)

Per una guida dettagliata su come creare un flusso di dati per un’origine di archiviazione cloud, consulta l’esercitazione su [creazione di un flusso di dati di archiviazione cloud per portare i dati su Platform](../../dataflow/batch/cloud-storage.md).

## Recupera [!DNL Data Landing Zone] credenziali

[!DNL Data Landing Zone] è un’origine fornita con la licenza Adobe Experience Platform Sources. [!DNL Data Landing Zone] utilizza un URI SAS e l&#39;autenticazione basata su token SAS. Puoi recuperare le credenziali di autenticazione da [!UICONTROL Catalogo origini] pagina.

Per recuperare le credenziali, selezionare **[!UICONTROL Data Landing Zone]** e quindi copiare le credenziali dalla barra a destra visualizzata.

![Elenco delle opzioni di visualizzazione per Data Landing Zone.](../../../../images/tutorials/create/dlz/view-credentials.png)

Viene visualizzato un popover con il nome del contenitore, il token SAS, il nome dell&#39;account di archiviazione, l&#39;URI SAS e la data di scadenza.

## Aggiorna il [!DNL Data Landing Zone] credenziali

Il tuo [!DNL Data Landing Zone] le credenziali sono impostate per scadere automaticamente dopo 90 giorni ed è necessario utilizzare le nuove credenziali per riconnettersi a [!DNL Data Landing Zone] dopo la scadenza. I flussi di dati in Experienci Platform non sono interessati dalle credenziali in scadenza ed è comunque possibile continuare a lavorare con flussi di dati nuovi ed esistenti con le nuove credenziali.

Esistono due modi per aggiornare [!DNL Data Landing Zone] credenziali:

>[!BEGINTABS]

>[!TAB Utilizza la scheda sorgente]

Per aggiornare le credenziali dalla pagina del catalogo delle origini, seleziona i puntini di sospensione (**`...`**) in [!DNL Data Landing Zone] e quindi selezionare **[!UICONTROL Aggiorna credenziali]**.

![Aggiorna le credenziali utilizzando la scheda di origine.](../../../../images/tutorials/create/dlz/refresh-with-card.png)

Viene visualizzata una finestra pop-up che richiede la conferma prima di procedere. Quando sei pronto, seleziona **[!UICONTROL Aggiorna credenziali]**.

![Finestra di conferma delle credenziali di aggiornamento.](../../../../images/tutorials/create/dlz/confirm.png)

>[!TAB Utilizza la barra a destra]

Per aggiornare le credenziali utilizzando la barra a destra, seleziona la **[!UICONTROL Data Landing Zone]** scheda sorgente e quindi selezionare **[!UICONTROL Altre azioni]**. Quindi, seleziona **[!UICONTROL Aggiorna credenziali]** quindi confermare utilizzando la finestra popup visualizzata.

![Aggiorna le credenziali utilizzando la barra a destra.](../../../../images/tutorials/create/dlz/refresh-with-right-rail.png)

>[!ENDTABS]

## Passaggi successivi

Seguendo questa esercitazione, hai effettuato l’accesso a [!DNL Data Landing Zone] e ha imparato a recuperare e aggiornare le credenziali. Ora puoi passare alla prossima esercitazione su [creazione di un flusso di dati per portare i dati da un’archiviazione cloud a Platform](../../dataflow/batch/cloud-storage.md).
