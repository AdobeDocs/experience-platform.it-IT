---
title: (Beta) Esportazione di file on-demand in destinazioni batch tramite l’interfaccia utente Experience Platform
type: Tutorial
description: Scopri come esportare file on-demand in destinazioni batch utilizzando l’interfaccia utente Experience Platform.
exl-id: 0cbe5089-b73d-4584-8451-2fc34d47c357
source-git-commit: 29962e07aa50c97b6098f4c892facf48508d28cf
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 8%

---

# (Beta) Esportazione di file on-demand in destinazioni batch tramite l’interfaccia utente Experience Platform

>[!IMPORTANT]
>
>La **[!UICONTROL Esporta file ora]** in Adobe Experience Platform è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.
>Contatta il tuo rappresentante di Adobe per accedere a questa funzionalità.

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

## **[!UICONTROL Esporta file ora]** panoramica {#overview}

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_activatenow"
>title="Esporta subito i file"
>abstract="Seleziona questa opzione per fornire un’esportazione di file completa in aggiunta a eventuali esportazioni già pianificate. L’esportazione dei file viene attivata subito e raccoglie i risultati più recenti delle esecuzioni di segmentazione di Experience Platform."

Questo articolo spiega come utilizzare l’interfaccia utente di Experience Platform per esportare file on-demand in destinazioni batch come [archiviazione cloud](/help/destinations/catalog/cloud-storage/overview.md) e [marketing via e-mail](/help/destinations/catalog/email-marketing/overview.md) destinazioni.

La **[!UICONTROL Esporta file ora]** consente di esportare un file completo senza interrompere la pianificazione di esportazione corrente di un segmento pianificato in precedenza. Questa esportazione si verifica oltre alle esportazioni pianificate in precedenza e non modifica la frequenza di esportazione del segmento. L’esportazione dei file viene attivata subito e raccoglie i risultati più recenti delle esecuzioni di segmentazione di Experience Platform.

Puoi inoltre utilizzare le API di Experience Platform a questo scopo. Scopri come [attivare segmenti di pubblico su richiesta per destinazioni batch tramite l’API di attivazione ad hoc](/help/destinations/api/ad-hoc-activation-api.md).

## Prerequisiti {#prerequisites}

Per esportare i file on-demand nelle destinazioni batch, è necessario aver completato l&#39;esportazione [connesso a una destinazione](./connect-destination.md). Se non lo hai già fatto, vai alla [catalogo delle destinazioni](../catalog/overview.md), sfoglia le destinazioni supportate e configura la destinazione che desideri utilizzare.

## Come esportare i file su richiesta {#how-to-export-files-on-demand}

1. Vai a **[!UICONTROL Connessioni > Destinazioni]**, seleziona **[!UICONTROL Sfoglia]** e il simbolo del filtro per mostrare le connessioni esistenti alle destinazioni batch desiderate.

   ![Immagine che evidenzia come accedere alla scheda Sfoglia e filtrare i flussi di dati esistenti.](../assets/ui/activate-on-demand/browse-tab.png)

2. Seleziona la connessione di destinazione desiderata per controllare il flusso di dati esistente nella destinazione.

   ![Immagine che evidenzia un flusso di dati filtrato.](../assets/ui/activate-on-demand/filtered-dataflow.png)

3. Seleziona la **[!UICONTROL Dati di attivazione]** , seleziona il segmento per il quale desideri esportare un file su richiesta e seleziona il **[!UICONTROL Esporta file ora]** per attivare un&#39;esportazione una tantum che consegnerà un file alla destinazione batch.

   >[!IMPORTANT]
   >
   >La selezione di più segmenti per esportare file su richiesta in blocco non è attualmente supportata nell’interfaccia utente. Utilizza la [API di attivazione ad hoc](/help/destinations/api/ad-hoc-activation-api.md) per quello scopo.

   ![Immagine che evidenzia il pulsante Esporta file.](../assets/ui/activate-on-demand/activate-segment-on-demand.png)

4. Seleziona **[!UICONTROL Sì]** per confermare e attivare l’esportazione del file.

   ![Immagine che mostra la finestra di dialogo di conferma del file di esportazione.](../assets/ui/activate-on-demand/confirm-activation.png)

5. Viene visualizzato un messaggio di conferma che informa che l’esportazione del file è iniziata.

   ![Immagine che mostra la conferma dell’attivazione ad hoc riuscita.](../assets/ui/activate-on-demand/ad-hoc-success.png)

6. È inoltre possibile passare alla **[!UICONTROL Corse del flusso di dati]** per confermare che l’esportazione del file è stata avviata.

## Considerazioni {#considerations}

Quando si utilizza il **[!UICONTROL Esporta file ora]** controllo:

* **[!UICONTROL Esporta file ora]** funziona solo per i segmenti la cui pianificazione nel flusso di dati di attivazione batch si sovrappone alla data corrente. Sono inclusi i segmenti con pianificazioni prive di data di fine (frequenza di esportazione di **[!UICONTROL Una volta]**) o quando la data di fine non è ancora passata.
* Quando aggiungi un segmento a un flusso di dati esistente, attendi almeno 15 minuti prima di utilizzare il **[!UICONTROL Esporta file ora]** controllo.
* Se si modificano i criteri di unione di un segmento o se si crea un segmento che utilizza un nuovo criterio di unione, attendere 24 ore prima di utilizzare il **[!UICONTROL Esporta file ora]** controllo.

## Messaggi di errore interfaccia utente {#ui-error-messages}

Quando utilizzi **[!UICONTROL Esporta file ora]** controllare, potresti riscontrare uno dei messaggi di errore elencati di seguito. Rivedi la tabella per capire come affrontarle quando vengono visualizzate.

| Messaggio di errore | Risoluzione |
|---------|----------|
| Esecuzione già in corso per il segmento `segment ID` per ordine `dataflow ID` con run id `flow run ID` | Questo messaggio di errore indica che è attualmente in corso un flusso di attivazione ad hoc per un segmento. Attendere il completamento del processo prima di attivare nuovamente il processo di attivazione. |
| Segmenti `<segment name>` non fanno parte di questo flusso di dati o non rientrano nell&#39;intervallo di pianificazione! | Questo messaggio di errore indica che i segmenti selezionati per l’attivazione non sono mappati al flusso di dati o che la pianificazione di attivazione impostata per i segmenti è scaduta o non ancora iniziata. Controlla se il segmento è effettivamente mappato al flusso di dati e verifica che la pianificazione di attivazione del segmento si sovrapponga alla data attuale. |

## Informazioni correlate {#related-information}

* [Attivare i segmenti di pubblico su destinazioni in batch on-demand utilizzando le API di Experience Platform](/help/destinations/api/ad-hoc-activation-api.md)
* [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](/help/destinations/ui/activate-batch-profile-destinations.md)
