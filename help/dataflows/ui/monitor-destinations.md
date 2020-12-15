---
keywords: Experience Platform;home;popular topics;monitor accounts;monitor dataflows;dataflows;destinations
description: Le destinazioni consentono di attivare i dati da Adobe Experience Platform a innumerevoli partner esterni. Questa esercitazione fornisce istruzioni su come monitorare i flussi di dati per le destinazioni utilizzando l'interfaccia utente del Experience Platform .
solution: Experience Platform
title: Monitorare i flussi di dati
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 12a6682b6e28e656899aee5c38d3bb4a84bcdd2f
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 1%

---


# Monitorare i flussi di dati per le destinazioni nell’interfaccia utente

Le destinazioni consentono di attivare i dati da Adobe Experience Platform a innumerevoli partner esterni. Questa esercitazione fornisce istruzioni su come monitorare i flussi di dati per le destinazioni utilizzando l&#39;interfaccia utente del Experience Platform .

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [Destinazioni](../../destinations/home.md): Le destinazioni sono integrazioni predefinite con applicazioni comunemente utilizzate che consentono l&#39;attivazione senza soluzione di continuità dei dati dalla piattaforma per campagne di marketing multicanale, campagne e-mail, pubblicità mirata e molti altri casi di utilizzo.
- [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

## Monitorare i flussi di dati

Nell&#39; **[!UICONTROL Destinations]** area di lavoro all&#39;interno dell&#39;interfaccia utente della piattaforma, andate alla **[!UICONTROL Browse]** scheda e selezionate il nome di una destinazione che desiderate visualizzare.

![](../assets/ui/monitor-destinations/select-destination.png)

Viene visualizzato un elenco dei flussi di dati esistenti. In questa pagina è presente un elenco di flussi di dati visualizzabili, con informazioni sulla destinazione, il nome utente, il numero di flussi di dati e lo stato.

Per ulteriori informazioni sugli stati, vedere la tabella seguente:

| Stato | Descrizione |
| ------ | ----------- |
| Abilitata | Lo `Enabled` stato indica che un flusso di dati è attivo e che sta acquisendo i dati in base alla pianificazione fornita. |
| Disabilitata | Lo `Disabled` stato indica che un flusso di dati è inattivo e non sta acquisendo alcun dato. |
| Elaborazione | Lo `Processing` stato indica che un flusso di dati non è ancora attivo. Questo stato si verifica spesso subito dopo la creazione di un nuovo flusso di dati. |
| Errore | Lo `Error` stato indica che il processo di attivazione di un flusso di dati è stato interrotto. |

## [!UICONTROL Dataflow runs]

La [!UICONTROL Dataflow runs] scheda fornisce i dati delle metriche nel flusso di dati, che vengono eseguiti sulle destinazioni batch. Viene visualizzato un elenco di singole esecuzioni e delle relative metriche specifiche, insieme ai seguenti totali per i record di profilo:

- **[!UICONTROL Profile records activated]**: Totale dei record di profilo creati o aggiornati per l&#39;attivazione.
- **[!UICONTROL Profile records skipped]**:  Totale dei record di profilo saltati per l&#39;attivazione in base alle uscite di profilo o agli attributi mancanti.

![](../assets/ui/monitor-destinations/dataflow-runs.png)

>[!NOTE]
>
>Le esecuzioni dei flussi di dati vengono generate in base alla frequenza di programmazione del flusso di dati di destinazione. Per ogni criterio di unione applicato a un segmento viene eseguita un&#39;esecuzione distinta per il flusso di dati.

Per visualizzare i dettagli di una particolare esecuzione di un flusso di dati, selezionare l&#39;ora di inizio dell&#39;esecuzione dall&#39;elenco. La pagina dei dettagli per un&#39;esecuzione di un flusso di dati contiene informazioni aggiuntive, come la dimensione dei dati elaborati e un elenco degli eventuali errori che si sono verificati con i dettagli per la diagnostica degli errori.

![](../assets/ui/monitor-destinations/dataflow.png)