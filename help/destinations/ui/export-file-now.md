---
title: Esportare file on-demand in destinazioni batch utilizzando l’interfaccia utente di Experience Platform
type: Tutorial
description: Scopri come esportare i file on-demand nelle destinazioni batch utilizzando l’interfaccia utente di Experience Platform.
exl-id: 0cbe5089-b73d-4584-8451-2fc34d47c357
source-git-commit: 111f6d5093a0b66a683745b1da8d8909eb17f7eb
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 8%

---


# Esportare file on-demand in destinazioni batch utilizzando l’interfaccia utente di Experience Platform

>[!IMPORTANT]
> 
>Per attivare i dati, sono necessarie le **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

## Panoramica di **[!UICONTROL Export file now]** {#overview}

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_activatenow"
>title="Esporta subito i file"
>abstract="Seleziona questa opzione per fornire un’esportazione di file completa in aggiunta a eventuali esportazioni pianificate in precedenza. L’esportazione dei file viene attivata subito e raccoglie i risultati più recenti delle esecuzioni di segmentazione di Experience Platform."

Questo articolo spiega come utilizzare l&#39;interfaccia utente di Experience Platform per esportare i file on-demand in destinazioni batch come [archiviazione cloud](/help/destinations/catalog/cloud-storage/overview.md) e [destinazioni e-mail marketing](/help/destinations/catalog/email-marketing/overview.md).

Il controllo **[!UICONTROL Export file now]** consente di esportare un file completo senza interrompere la pianificazione di esportazione corrente di un pubblico pianificato in precedenza. Questa esportazione si verifica in aggiunta alle esportazioni pianificate in precedenza e non modifica la frequenza di esportazione del pubblico. L’esportazione dei file viene attivata subito e raccoglie i risultati più recenti delle esecuzioni di segmentazione di Experience Platform.

A questo scopo puoi anche utilizzare le API di Experience Platform. Scopri come [attivare i tipi di pubblico su richiesta nelle destinazioni batch tramite l&#39;API di attivazione ad hoc](/help/destinations/api/ad-hoc-activation-api.md).

## Prerequisiti {#prerequisites}

Per esportare i file su richiesta in destinazioni batch, è necessario avere [connesso a una destinazione](./connect-destination.md). Se non lo hai già fatto, vai al [catalogo delle destinazioni](../catalog/overview.md), sfoglia le destinazioni supportate e configura la destinazione che desideri utilizzare.

## Come esportare i file on-demand {#how-to-export-files-on-demand}

1. Vai a **[!UICONTROL Connections > Destinations]**, seleziona la scheda **[!UICONTROL Browse]** e il simbolo del filtro per mostrare le connessioni esistenti alle destinazioni batch desiderate.

   ![Immagine che evidenzia come accedere alla scheda Sfoglia e filtrare i flussi di dati esistenti.](../assets/ui/activate-on-demand/browse-tab.png)

2. Seleziona la connessione di destinazione desiderata per verificare il flusso di dati esistente per la destinazione.

   ![Immagine che evidenzia un flusso di dati filtrato.](../assets/ui/activate-on-demand/filtered-dataflow.png)

3. Selezionare la scheda **[!UICONTROL Activation data]** e i tipi di pubblico per i quali si desidera esportare i file su richiesta, quindi selezionare il controllo **[!UICONTROL Export file now]** per attivare un&#39;esportazione una tantum che invierà un file per ogni pubblico selezionato alla destinazione batch.

   ![Immagine che evidenzia il pulsante Esporta ora file.](../assets/ui/activate-on-demand/bulk-export-file-now.png)

4. Selezionare **[!UICONTROL Yes]** per confermare e attivare l&#39;esportazione del file.

   ![Immagine che mostra la finestra di conferma Esporta file adesso.](../assets/ui/activate-on-demand/confirm-activation.png)

5. Viene visualizzato un messaggio di conferma che informa dell&#39;avvio dell&#39;esportazione del file.

   ![Immagine che mostra la conferma dell&#39;attivazione ad-hoc completata.](../assets/ui/activate-on-demand/ad-hoc-success.png)

6. È inoltre possibile passare alla scheda **[!UICONTROL Dataflow runs]** per verificare che l&#39;esportazione del file sia stata avviata.

## Considerazioni {#considerations}

Quando si utilizza il controllo **[!UICONTROL Export file now]**, tenere presenti le considerazioni seguenti:

* **[!UICONTROL Export file now]** funziona solo per i tipi di pubblico la cui pianificazione nel flusso di dati di attivazione batch si sovrappone alla data corrente. Sono inclusi i tipi di pubblico con pianificazioni senza data di fine (frequenza di esportazione di **[!UICONTROL Once]**) o per i quali la data di fine non è ancora stata superata.
* Quando aggiungi un pubblico a un flusso di dati esistente, attendi almeno **un&#39;ora** prima di utilizzare il controllo **[!UICONTROL Export file now]**.
* Se si modifica il criterio di unione di un pubblico o se si crea un pubblico che utilizza un nuovo criterio di unione, attendere 24 ore prima di utilizzare il controllo **[!UICONTROL Export file now]**.
* **[!UICONTROL Export file now]** utilizza solo i dati delle esportazioni di snapshot pianificate. Non raccoglie dati da processi di esportazione attivati da API. Per esportare i dati più recenti dopo un processo di esportazione attivato da API, attendi l’esecuzione della successiva esportazione pianificata.

## Messaggi di errore dell’interfaccia utente {#ui-error-messages}

Quando si utilizza il controllo **[!UICONTROL Export file now]**, è possibile che si verifichi uno dei messaggi di errore elencati di seguito. Rivedi la tabella per capire come gestirli quando vengono visualizzati.

| Messaggio di errore | Risoluzione |
|---------|----------|
| Esecuzione già in corso per il pubblico `segment ID` per l&#39;ordine `dataflow ID` con ID esecuzione `flow run ID` | Questo messaggio di errore indica che per un pubblico è attualmente in corso un flusso di attivazione ad hoc. Attendere il completamento del processo prima di riattivarlo. |
| I tipi di pubblico `<segment name>` non fanno parte di questo flusso di dati o non rientrano nell&#39;intervallo pianificato. | Questo messaggio di errore indica che i tipi di pubblico selezionati per l’attivazione non sono mappati al flusso di dati o che la pianificazione di attivazione impostata per i tipi di pubblico è scaduta o non è ancora stata avviata. Controlla se il pubblico è effettivamente mappato al flusso di dati e verifica che la pianificazione di attivazione del pubblico si sovrapponga alla data attuale. |

## Informazioni correlate {#related-information}

* [Attiva i tipi di pubblico su richiesta nelle destinazioni batch utilizzando le API di Experience Platform](/help/destinations/api/ad-hoc-activation-api.md)
* [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](/help/destinations/ui/activate-batch-profile-destinations.md)
