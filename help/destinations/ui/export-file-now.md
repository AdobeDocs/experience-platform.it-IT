---
title: (Beta) Esportare file on-demand in destinazioni batch utilizzando l’interfaccia utente di Experience Platform
type: Tutorial
description: Scopri come esportare file on-demand in destinazioni batch utilizzando l’interfaccia utente di Experience Platform.
exl-id: 0cbe5089-b73d-4584-8451-2fc34d47c357
source-git-commit: 64833e29d062225bc774a14ae60b102b293bb5c4
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 8%

---

# (Beta) Esportare file on-demand in destinazioni batch utilizzando l’interfaccia utente di Experience Platform

>[!IMPORTANT]
>
>L&#39;opzione **[!UICONTROL Esporta file ora]** in Adobe Experience Platform è attualmente in Beta. La documentazione e le funzionalità sono soggette a modifiche.
>Contatta il rappresentante del tuo Adobe per accedere a questa funzionalità.

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

## Panoramica su **[!UICONTROL Esporta file ora]** {#overview}

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_activatenow"
>title="Esporta subito i file"
>abstract="Seleziona questa opzione per fornire un’esportazione di file completa in aggiunta a eventuali esportazioni già pianificate. L’esportazione dei file viene attivata subito e raccoglie i risultati più recenti delle esecuzioni di segmentazione di Experience Platform."

In questo articolo viene illustrato come utilizzare l&#39;interfaccia utente di Experience Platform per esportare file su richiesta in destinazioni batch come [archiviazione cloud](/help/destinations/catalog/cloud-storage/overview.md) e [destinazioni di e-mail marketing](/help/destinations/catalog/email-marketing/overview.md).

Il controllo **[!UICONTROL Esporta file ora]** consente di esportare un file completo senza interrompere la pianificazione di esportazione corrente di un pubblico pianificato in precedenza. Questa esportazione si verifica in aggiunta alle esportazioni pianificate in precedenza e non modifica la frequenza di esportazione del pubblico. L’esportazione dei file viene attivata subito e raccoglie i risultati più recenti delle esecuzioni di segmentazione di Experience Platform.

A questo scopo, puoi anche utilizzare le API Experience Platform. Scopri come [attivare i tipi di pubblico su richiesta nelle destinazioni batch tramite l&#39;API di attivazione ad hoc](/help/destinations/api/ad-hoc-activation-api.md).

## Prerequisiti {#prerequisites}

Per esportare i file su richiesta in destinazioni batch, è necessario avere [connesso a una destinazione](./connect-destination.md). Se non lo hai già fatto, vai al [catalogo delle destinazioni](../catalog/overview.md), sfoglia le destinazioni supportate e configura la destinazione che desideri utilizzare.

## Come esportare i file on-demand {#how-to-export-files-on-demand}

1. Vai a **[!UICONTROL Connessioni > Destinazioni]**, seleziona la scheda **[!UICONTROL Sfoglia]** e il simbolo del filtro per mostrare le connessioni esistenti alle destinazioni batch desiderate.

   ![Immagine che evidenzia come accedere alla scheda Sfoglia e filtrare i flussi di dati esistenti.](../assets/ui/activate-on-demand/browse-tab.png)

2. Seleziona la connessione di destinazione desiderata per verificare il flusso di dati esistente per la destinazione.

   ![Immagine che evidenzia un flusso di dati filtrato.](../assets/ui/activate-on-demand/filtered-dataflow.png)

3. Seleziona la scheda **[!UICONTROL Dati attivazione]** e seleziona i tipi di pubblico per i quali desideri esportare i file su richiesta, quindi seleziona il controllo **[!UICONTROL Esporta file ora]** per attivare un&#39;esportazione una tantum che distribuirà un file per ogni pubblico selezionato nella destinazione batch.

   ![Immagine che evidenzia il pulsante Esporta ora file.](../assets/ui/activate-on-demand/bulk-export-file-now.png)

4. Seleziona **[!UICONTROL Sì]** per confermare e attivare l&#39;esportazione del file.

   ![Immagine che mostra la finestra di conferma Esporta file adesso.](../assets/ui/activate-on-demand/confirm-activation.png)

5. Viene visualizzato un messaggio di conferma che informa dell&#39;avvio dell&#39;esportazione del file.

   ![Immagine che mostra la conferma dell&#39;attivazione ad-hoc completata.](../assets/ui/activate-on-demand/ad-hoc-success.png)

6. Puoi anche passare alla scheda **[!UICONTROL Esecuzioni flusso di dati]** per verificare che l&#39;esportazione del file sia stata avviata.

## Considerazioni {#considerations}

Quando si utilizza il controllo **[!UICONTROL Esporta file ora]**, tenere presenti le considerazioni seguenti:

* **[!UICONTROL Il file di esportazione ora]** funziona solo per i tipi di pubblico la cui pianificazione nel flusso di dati di attivazione batch si sovrappone alla data corrente. Sono inclusi i tipi di pubblico con pianificazioni senza data di fine (frequenza di esportazione di **[!UICONTROL Una volta]**) o per i quali la data di fine non è ancora stata superata.
* Quando aggiungi un pubblico a un flusso di dati esistente, attendi almeno 15 minuti prima di utilizzare il controllo **[!UICONTROL Esporta file ora]**.
* Se modifichi il criterio di unione di un pubblico o se crei un pubblico che utilizza un nuovo criterio di unione, attendi 24 ore prima di utilizzare il controllo **[!UICONTROL Esporta file ora]**.

## Messaggi di errore dell’interfaccia utente {#ui-error-messages}

Quando si utilizza il controllo **[!UICONTROL Esporta file ora]**, è possibile che si verifichi uno dei messaggi di errore elencati di seguito. Rivedi la tabella per capire come gestirli quando vengono visualizzati.

| Messaggio di errore | Risoluzione |
|---------|----------|
| Esecuzione già in corso per il pubblico `segment ID` per l&#39;ordine `dataflow ID` con ID esecuzione `flow run ID` | Questo messaggio di errore indica che per un pubblico è attualmente in corso un flusso di attivazione ad hoc. Attendere il completamento del processo prima di riattivarlo. |
| I tipi di pubblico `<segment name>` non fanno parte di questo flusso di dati o non rientrano nell&#39;intervallo pianificato. | Questo messaggio di errore indica che i tipi di pubblico selezionati per l’attivazione non sono mappati al flusso di dati o che la pianificazione di attivazione impostata per i tipi di pubblico è scaduta o non è ancora stata avviata. Controlla se il pubblico è effettivamente mappato al flusso di dati e verifica che la pianificazione di attivazione del pubblico si sovrapponga alla data attuale. |

## Informazioni correlate {#related-information}

* [Attiva i tipi di pubblico su richiesta nelle destinazioni batch utilizzando le API Experience Platform](/help/destinations/api/ad-hoc-activation-api.md)
* [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](/help/destinations/ui/activate-batch-profile-destinations.md)
