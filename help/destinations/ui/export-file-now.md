---
title: (Beta) Esportare file on-demand in destinazioni batch utilizzando l’interfaccia utente di Experienci Platform
type: Tutorial
description: Scopri come esportare file on-demand in destinazioni batch utilizzando l’interfaccia utente di Experienci Platform.
exl-id: 0cbe5089-b73d-4584-8451-2fc34d47c357
source-git-commit: 165793619437f403045b9301ca6fa5389d55db31
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 8%

---

# (Beta) Esportare file on-demand in destinazioni batch utilizzando l’interfaccia utente di Experienci Platform

>[!IMPORTANT]
>
>Il **[!UICONTROL Esporta subito il file]** in Adobe Experience Platform è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.
>Contatta il rappresentante del tuo Adobe per accedere a questa funzionalità.

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

## Panoramica su **[!UICONTROL Esporta file ora]** {#overview}

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_activatenow"
>title="Esporta subito i file"
>abstract="Seleziona questa opzione per fornire un’esportazione di file completa in aggiunta a eventuali esportazioni già pianificate. L’esportazione dei file viene attivata subito e raccoglie i risultati più recenti delle esecuzioni di segmentazione di Experience Platform."

Questo articolo spiega come utilizzare l’interfaccia utente di Experienci Platform per esportare i file on-demand in destinazioni batch come [archiviazione cloud](/help/destinations/catalog/cloud-storage/overview.md) e [e-mail marketing](/help/destinations/catalog/email-marketing/overview.md) destinazioni.

Il **[!UICONTROL Esporta subito il file]** control ti consente di esportare un file completo senza interrompere la pianificazione di esportazione corrente di un pubblico pianificato in precedenza. Questa esportazione si verifica in aggiunta alle esportazioni pianificate in precedenza e non modifica la frequenza di esportazione del pubblico. L’esportazione dei file viene attivata subito e raccoglie i risultati più recenti delle esecuzioni di segmentazione di Experience Platform.

A questo scopo, puoi anche utilizzare le API Experienci Platform. Scopri come [attivare i tipi di pubblico on-demand nelle destinazioni batch tramite l’API di attivazione ad hoc](/help/destinations/api/ad-hoc-activation-api.md).

## Prerequisiti {#prerequisites}

Per esportare i file on-demand nelle destinazioni batch, è necessario avere [connesso a una destinazione](./connect-destination.md). Se non lo hai già fatto, accedi al [catalogo delle destinazioni](../catalog/overview.md), sfoglia le destinazioni supportate e configura la destinazione che desideri utilizzare.

## Come esportare i file on-demand {#how-to-export-files-on-demand}

1. Vai a **[!UICONTROL Connessioni > Destinazioni]**, seleziona la **[!UICONTROL Sfoglia]** e il simbolo del filtro per mostrare le connessioni esistenti alle destinazioni batch desiderate.

   ![Immagine che evidenzia come accedere alla scheda Sfoglia e filtrare i flussi di dati esistenti.](../assets/ui/activate-on-demand/browse-tab.png)

2. Seleziona la connessione di destinazione desiderata per verificare il flusso di dati esistente per la destinazione.

   ![Immagine che evidenzia un flusso di dati filtrato.](../assets/ui/activate-on-demand/filtered-dataflow.png)

3. Seleziona la **[!UICONTROL Dati di attivazione]** e selezionare il pubblico per il quale si desidera esportare un file su richiesta e selezionare **[!UICONTROL Esporta subito il file]** controllo per attivare un&#39;esportazione una tantum che invierà un file alla destinazione batch.

   >[!IMPORTANT]
   >
   >La selezione di più tipi di pubblico per esportare i file in blocco su richiesta non è attualmente supportata nell’interfaccia utente di. Utilizza il [API di attivazione ad hoc](/help/destinations/api/ad-hoc-activation-api.md) a tal fine.

   ![Immagine che evidenzia il pulsante Export file now (Esporta file ora).](../assets/ui/activate-on-demand/activate-segment-on-demand.png)

4. Seleziona **[!UICONTROL Sì]** per confermare e attivare l&#39;esportazione dei file.

   ![Immagine che mostra la finestra di conferma Esporta file ora.](../assets/ui/activate-on-demand/confirm-activation.png)

5. Viene visualizzato un messaggio di conferma che informa dell&#39;avvio dell&#39;esportazione del file.

   ![Immagine che mostra la conferma dell’attivazione ad-hoc riuscita.](../assets/ui/activate-on-demand/ad-hoc-success.png)

6. È inoltre possibile passare alla **[!UICONTROL Il flusso di dati viene eseguito]** per confermare che l’esportazione del file è iniziata.

## Considerazioni {#considerations}

Quando utilizzi la proprietà, tieni presente quanto segue **[!UICONTROL Esporta subito il file]** controllo:

* **[!UICONTROL Esporta subito il file]** funziona solo per i tipi di pubblico la cui pianificazione nel flusso di dati di attivazione batch si sovrappone alla data corrente. Sono inclusi i tipi di pubblico con pianificazioni senza data di fine (frequenza di esportazione di **[!UICONTROL Una volta]**) o se la data di fine non è ancora passata.
* Quando aggiungi un pubblico a un flusso di dati esistente, attendi almeno 15 minuti prima di utilizzare il **[!UICONTROL Esporta subito il file]** controllo.
* Se modifichi il criterio di unione di un pubblico o se crei un pubblico che utilizza un nuovo criterio di unione, attendi 24 ore prima di utilizzare il **[!UICONTROL Esporta subito il file]** controllo.

## Messaggi di errore dell’interfaccia utente {#ui-error-messages}

Quando si utilizza **[!UICONTROL Esporta subito il file]** , è possibile che si verifichi uno dei messaggi di errore elencati di seguito. Rivedi la tabella per capire come gestirli quando vengono visualizzati.

| Messaggio di errore | Risoluzione |
|---------|----------|
| Esecuzione già in corso per il pubblico `segment ID` per ordine `dataflow ID` con id esecuzione `flow run ID` | Questo messaggio di errore indica che per un pubblico è attualmente in corso un flusso di attivazione ad hoc. Attendere il completamento del processo prima di riattivarlo. |
| Tipi di pubblico `<segment name>` non fanno parte di questo flusso di dati o non rientrano nell’intervallo di pianificazione. | Questo messaggio di errore indica che i tipi di pubblico selezionati per l’attivazione non sono mappati al flusso di dati o che la pianificazione di attivazione impostata per i tipi di pubblico è scaduta o non è ancora stata avviata. Controlla se il pubblico è effettivamente mappato al flusso di dati e verifica che la pianificazione di attivazione del pubblico si sovrapponga alla data attuale. |

## Informazioni correlate {#related-information}

* [Attiva i tipi di pubblico su richiesta nelle destinazioni batch utilizzando le API Experienci Platform](/help/destinations/api/ad-hoc-activation-api.md)
* [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](/help/destinations/ui/activate-batch-profile-destinations.md)
