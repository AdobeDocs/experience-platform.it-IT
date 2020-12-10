---
keywords: Experience Platform;home;popular topics;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;
solution: Experience Platform
title: Mappare un file CSV su uno schema XDM
topic: tutorial
type: Tutorial
description: Questa esercitazione illustra come mappare un file CSV su uno schema XDM utilizzando l'interfaccia utente di Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: c19360450d7b1f11063683b796774a04f3dbe16c
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 1%

---


# Mappare un file CSV su uno schema XDM

Per assimilare i dati CSV in [!DNL Adobe Experience Platform], i dati devono essere mappati su uno schema [!DNL Experience Data Model] (XDM). Questa esercitazione illustra come mappare un file CSV su uno schema XDM utilizzando l&#39;interfaccia [!DNL Platform] utente.

Inoltre, l&#39;appendice di questa esercitazione fornisce ulteriori informazioni sull&#39;utilizzo delle funzioni [di](#mapping-functions)mappatura.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di [!DNL Platform]:

- [[!DNL Experience Data Model (XDM System)]](../../xdm/home.md): Il framework standard con cui [!DNL Platform] organizzare i dati relativi all&#39;esperienza del cliente.
- [[!DNL Batch ingestion]](../batch-ingestion/overview.md): Metodo con cui [!DNL Platform] vengono acquisiti i dati dai file di dati forniti dall&#39;utente.

Questa esercitazione richiede anche che sia già stato creato un set di dati in cui assimilare i dati CSV. Per i passaggi sulla creazione di un dataset nell&#39;interfaccia utente, consulta l&#39;esercitazione [sull&#39;acquisizione dei](./ingest-batch-data.md)dati.

## Scegliere una destinazione

Accedete a [[!DNL Adobe Experience Platform]](https://platform.adobe.com) e selezionate **[!UICONTROL Workflows]** dalla barra di navigazione a sinistra per accedere all’ **[!UICONTROL Workflows]** area di lavoro.

Dalla **[!UICONTROL Workflows]** schermata, selezionate **[!UICONTROL Map CSV to XDM schema]** sotto la **[!UICONTROL Data ingestion]** sezione, quindi selezionate **[!UICONTROL Launch]**.

![](../images/tutorials/map-a-csv-file/workflows.png)

Viene **[!UICONTROL Map CSV to XDM schema]** visualizzato il flusso di lavoro, a partire dal **[!UICONTROL Destination]** passaggio. Scegliere un set di dati in entrata in cui assimilare i dati. È possibile utilizzare un set di dati esistente o crearne uno nuovo.

**Utilizzare un dataset esistente**

Per assimilare i dati CSV in un set di dati esistente, selezionate **[!UICONTROL Use existing dataset]**. È possibile recuperare un set di dati esistente utilizzando la funzione di ricerca o scorrendo l&#39;elenco dei set di dati esistenti nel pannello.

![](../images/tutorials/map-a-csv-file/use-existing-dataset.png)

Per assimilare i dati CSV in un nuovo set di dati, selezionate **[!UICONTROL Create new dataset]** e immettete un nome e una descrizione per il set di dati nei campi forniti. Selezionare uno schema utilizzando la funzione di ricerca o scorrendo l&#39;elenco degli schemi forniti. Selezionare **[!UICONTROL Next]** per continuare.

![](../images/tutorials/map-a-csv-file/create-new-dataset.png)

## Aggiungi dati

Viene **[!UICONTROL Add data]** visualizzato il passaggio. Trascinate e rilasciate il file CSV nello spazio disponibile oppure selezionate **[!UICONTROL Choose files]** per inserire manualmente il file CSV.

![](../images/tutorials/map-a-csv-file/add-data.png)

La **[!UICONTROL Sample data]** sezione viene visualizzata una volta che il file è stato caricato, mostrando le prime dieci righe di dati. Dopo aver confermato che i dati sono stati caricati come previsto, selezionate **[!UICONTROL Next]**.

![](../images/tutorials/map-a-csv-file/sample-data.png)

## Mappatura di campi CSV nei campi dello schema XDM

Viene **[!UICONTROL Mapping]** visualizzato il passaggio. Le colonne del file CSV sono elencate in **[!UICONTROL Source Field]**, con i campi dello schema XDM corrispondenti elencati in **[!UICONTROL Target Field]**.

[!DNL Platform] fornisce automaticamente raccomandazioni intelligenti per i campi mappati automaticamente in base allo schema di destinazione o al dataset selezionato. Puoi regolare manualmente le regole di mappatura in base ai tuoi casi di utilizzo.

![](../images/tutorials/map-a-csv-file/mapping-with-suggestions.png)

Per accettare tutti i valori di mappatura della generazione automatica, selezionate la casella di controllo &quot;[!UICONTROL Accept all target fields]&quot;.

![](../images/tutorials/map-a-csv-file/filled-mapping-with-suggestions.png)

A volte, per lo schema di origine è disponibile più di una raccomandazione. In questo caso, la scheda di mappatura visualizza la raccomandazione più importante, seguita da un cerchio blu che contiene il numero di raccomandazioni aggiuntive disponibili. Selezionando l&#39;icona della lampadina, verrà visualizzato un elenco delle raccomandazioni aggiuntive. Potete scegliere una delle raccomandazioni alternative selezionando la casella di controllo accanto alla raccomandazione alla quale desiderate eseguire la mappatura.

![](../images/tutorials/map-a-csv-file/multiple-recommendations.png)

In alternativa, è possibile scegliere di mappare manualmente lo schema di origine sullo schema di destinazione. Passa il cursore del mouse sullo schema di origine da mappare, quindi seleziona l&#39;icona più.

![](../images/tutorials/map-a-csv-file/mapping-with-suggestions-and-buttons.png)

Viene **[!UICONTROL Map source to target field]** visualizzato il puntatore. Da qui è possibile selezionare il campo da mappare, seguito **[!UICONTROL Save]** da aggiungere la nuova mappatura.

![](../images/tutorials/map-a-csv-file/manual-mapping.png)

Se si desidera rimuovere una delle mappature, passare il mouse su tale mappatura, quindi selezionare l&#39;icona meno.

### Aggiungi campo calcolato

I campi calcolati consentono la creazione di valori in base agli attributi nello schema di input. Questi valori possono quindi essere assegnati agli attributi nello schema di destinazione e ricevere un nome e una descrizione che consentano un riferimento più semplice.

Selezionare il **[!UICONTROL Add calculated field]** pulsante per continuare.

![](../images/tutorials/map-a-csv-file/add-calculated-field.png)

Viene visualizzato il **[!UICONTROL Create calculated field]** pannello. La finestra di dialogo a sinistra contiene i campi, le funzioni e gli operatori supportati nei campi calcolati. Selezionare una delle schede per iniziare ad aggiungere funzioni, campi o operatori all&#39;editor di espressioni.

![](../images/tutorials/map-a-csv-file/create-calculated-fields.png)

| Scheda | Descrizione |
| --------- | ----------- |
| Campi | La scheda Campi elenca i campi e gli attributi disponibili nello schema di origine. |
| Funzioni | La scheda Funzioni elenca le funzioni disponibili per trasformare i dati. Per ulteriori informazioni sulle funzioni che è possibile utilizzare all&#39;interno dei campi calcolati, consultare la guida sull&#39; [utilizzo delle funzioni](../../data-prep/functions.md)di mappatura dei dati. |
| Operatori | La scheda operatori elenca gli operatori disponibili per trasformare i dati. |

È possibile aggiungere manualmente campi, funzioni e operatori utilizzando l&#39;editor di espressioni al centro. Selezionate l&#39;editor per iniziare a creare un&#39;espressione.

![](../images/tutorials/map-a-csv-file/create-calculated-field.png)

Selezionare **[!UICONTROL Save]** per continuare.

La schermata di mappatura viene visualizzata nuovamente con il campo di origine appena creato. Applicate il campo di destinazione corrispondente appropriato e selezionate **[!UICONTROL Finish]** per completare la mappatura.

![](../images/tutorials/map-a-csv-file/new-calculated-field.png)

## Caricamento dei dati del monitor

Una volta mappato e creato il file CSV, potete monitorare i dati che vengono acquisiti tramite di esso. Per ulteriori informazioni sul monitoraggio dell’inserimento dei dati, consulta l’esercitazione sul [monitoraggio dell’inserimento](../../ingestion/quality/monitor-data-ingestion.md)dei dati.

## Passaggi successivi

Seguendo questa esercitazione, avete mappato correttamente un file CSV semplice su uno schema XDM e lo avete assimilato in [!DNL Platform]. Questi dati possono ora essere utilizzati da [!DNL Platform] servizi a valle come [!DNL Real-time Customer Profile]. Per [[!DNL Real-time Customer Profile]](../../profile/home.md) ulteriori informazioni, consulta la panoramica.
