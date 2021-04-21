---
keywords: Experience Platform;home;argomenti comuni;monitorare account;monitorare flussi di dati;flussi di dati;destinazioni
description: Le destinazioni ti consentono di attivare i tuoi dati da Adobe Experience Platform a innumerevoli partner esterni. Questa esercitazione fornisce istruzioni su come monitorare i flussi di dati per le destinazioni utilizzando l’interfaccia utente di Experience Platform.
solution: Experience Platform
title: Monitorare i flussi di dati per le destinazioni nell’interfaccia utente
topic-legacy: overview
type: Tutorial
exl-id: 8eb7bb3c-f2dc-4dbc-9cf5-3d5d3224f5f1
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 1%

---

# Monitorare i flussi di dati per le destinazioni nell’interfaccia utente

Le destinazioni ti consentono di attivare i tuoi dati da Adobe Experience Platform a innumerevoli partner esterni. Questa esercitazione fornisce istruzioni su come monitorare i flussi di dati per le destinazioni utilizzando l’interfaccia utente di Experience Platform.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [Destinazioni](../../destinations/home.md): Le destinazioni sono integrazioni predefinite con applicazioni comunemente utilizzate che consentono l’attivazione senza soluzione di continuità dei dati da Platform per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.
- [Sandbox](../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

## Monitorare i flussi di dati

Nell’area di lavoro **[!UICONTROL Destinations]** all’interno dell’interfaccia utente di Platform, passa alla scheda **[!UICONTROL Browse]** e seleziona il nome di una destinazione da visualizzare.

![](../assets/ui/monitor-destinations/select-destination.png)

Viene visualizzato un elenco dei flussi di dati esistenti. In questa pagina è riportato un elenco di flussi di dati visualizzabili, con informazioni sulla loro destinazione, nome utente, numero di flussi di dati e stato.

Per ulteriori informazioni sugli stati, consulta la tabella seguente:

| Stato | Descrizione |
| ------ | ----------- |
| Abilitata | Lo stato `Enabled` indica che un flusso di dati è attivo e acquisisce i dati in base alla pianificazione fornita. |
| Disabilitata | Lo stato `Disabled` indica che un flusso di dati è inattivo e non acquisisce alcun dato. |
| Elaborazione | Lo stato `Processing` indica che un flusso di dati non è ancora attivo. Questo stato viene spesso rilevato immediatamente dopo la creazione di un nuovo flusso di dati. |
| Errore | Lo stato `Error` indica che il processo di attivazione di un flusso di dati è stato interrotto. |

## [!UICONTROL Dataflow runs]

La scheda [!UICONTROL Dataflow runs] fornisce dati metrici sul flusso di dati da eseguire su destinazioni batch. Viene visualizzato un elenco di singole esecuzioni e delle relative metriche specifiche, insieme ai seguenti totali per i record di profilo:

- **[!UICONTROL Profile records activated]**: Numero totale di record di profilo creati o aggiornati per l’attivazione.
- **[!UICONTROL Profile records skipped]**: Numero totale di record di profilo saltati per l’attivazione in base alle uscite di profilo o agli attributi mancanti.

![](../assets/ui/monitor-destinations/dataflow-runs.png)

>[!NOTE]
>
>Le esecuzioni dei flussi di dati vengono generate in base alla frequenza di pianificazione del flusso di dati di destinazione. Viene eseguita un&#39;esecuzione separata del flusso di dati per ogni criterio di unione applicato a un segmento.

Per visualizzare i dettagli di una particolare esecuzione di un flusso di dati, selezionare l’ora di inizio dell’esecuzione dall’elenco. La pagina dei dettagli di un&#39;esecuzione del flusso di dati contiene informazioni aggiuntive, come la dimensione dei dati elaborati e un elenco degli eventuali errori che si sono verificati con i dettagli relativi alla diagnostica degli errori.

![](../assets/ui/monitor-destinations/dataflow.png)
