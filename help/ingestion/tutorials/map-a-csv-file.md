---
keywords: Experience Platform;home;argomenti popolari;mappa csv;mappa file csv;mappa file csv su xdm;mappa csv su xdm;guida ui;
solution: Experience Platform
title: Mappare un file CSV su uno schema XDM
topic-legacy: tutorial
type: Tutorial
description: Questa esercitazione illustra come mappare un file CSV su uno schema XDM utilizzando l'interfaccia utente di Adobe Experience Platform.
exl-id: 15f55562-269d-421d-ad3a-5c10fb8f109c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 1%

---

# Mappare un file CSV su uno schema XDM

Per acquisire dati CSV in [!DNL Adobe Experience Platform], è necessario mappare i dati su uno schema [!DNL Experience Data Model] (XDM). Questa esercitazione illustra come mappare un file CSV su uno schema XDM utilizzando l’ interfaccia utente [!DNL Platform] .

Inoltre, l&#39;appendice di questa esercitazione fornisce ulteriori informazioni sull&#39;utilizzo di [funzioni di mappatura](#mapping-functions).

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di [!DNL Platform]:

- [[!DNL Experience Data Model (XDM System)]](../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Platform] vengono organizzati i dati sulla customer experience.
- [[!DNL Batch ingestion]](../batch-ingestion/overview.md): Il metodo con cui  [!DNL Platform] vengono acquisiti i dati dai file di dati forniti dall’utente.

Questa esercitazione richiede anche di aver già creato un set di dati per acquisire i dati CSV in . Per i passaggi necessari per creare un set di dati nell’interfaccia utente, consulta l’ [esercitazione sull’acquisizione dei dati](./ingest-batch-data.md).

## Scegliere una destinazione

Accedi a [[!DNL Adobe Experience Platform]](https://platform.adobe.com) e seleziona **[!UICONTROL Workflows]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro **[!UICONTROL Workflows]**.

Dalla schermata **[!UICONTROL Workflows]**, seleziona **[!UICONTROL Map CSV to XDM schema]** sotto la sezione **[!UICONTROL Data ingestion]** , quindi seleziona **[!UICONTROL Launch]**.

![](../images/tutorials/map-a-csv-file/workflows.png)

Viene visualizzato il flusso di lavoro **[!UICONTROL Map CSV to XDM schema]** a partire dal passaggio **[!UICONTROL Destination]** . Scegli un set di dati in entrata in cui acquisire i dati. Puoi utilizzare un set di dati esistente o crearne uno nuovo.

**Utilizzare un set di dati esistente**

Per acquisire i dati CSV in un set di dati esistente, seleziona **[!UICONTROL Use existing dataset]**. Puoi recuperare un set di dati esistente utilizzando la funzione di ricerca o scorrendo l’elenco dei set di dati esistenti nel pannello.

![](../images/tutorials/map-a-csv-file/use-existing-dataset.png)

Per acquisire i dati CSV in un nuovo set di dati, seleziona **[!UICONTROL Create new dataset]** e immetti un nome e una descrizione per il set di dati nei campi forniti. Selezionare uno schema utilizzando la funzione di ricerca o scorrendo l’elenco degli schemi forniti. Selezionare **[!UICONTROL Next]** per continuare.

![](../images/tutorials/map-a-csv-file/create-new-dataset.png)

## Aggiungi dati

Viene visualizzato il passaggio **[!UICONTROL Add data]** . Trascina e rilascia il file CSV nello spazio disponibile oppure seleziona **[!UICONTROL Choose files]** per inserire manualmente il file CSV.

![](../images/tutorials/map-a-csv-file/add-data.png)

La sezione **[!UICONTROL Sample data]** viene visualizzata una volta caricato il file, mostrando le prime dieci righe di dati. Dopo aver confermato che i dati sono stati caricati come previsto, seleziona **[!UICONTROL Next]**.

![](../images/tutorials/map-a-csv-file/sample-data.png)

## Mappatura di campi CSV nei campi dello schema XDM

Viene visualizzato il passaggio **[!UICONTROL Mapping]** . Le colonne del file CSV sono elencate in **[!UICONTROL Source Field]**, con i relativi campi dello schema XDM elencati in **[!UICONTROL Target Field]**.

[!DNL Platform] fornisce automaticamente raccomandazioni intelligenti per i campi mappati automaticamente in base allo schema o al set di dati di destinazione selezionato. Puoi regolare manualmente le regole di mappatura in base ai tuoi casi d’uso.

![](../images/tutorials/map-a-csv-file/mapping-with-suggestions.png)

Per accettare tutti i valori di mappatura di generazione automatica, seleziona la casella di controllo &quot;[!UICONTROL Accept all target fields]&quot;.

![](../images/tutorials/map-a-csv-file/filled-mapping-with-suggestions.png)

A volte, per lo schema di origine sono disponibili più consigli. In questo caso, la scheda di mappatura visualizza la raccomandazione più importante, seguita da un cerchio blu che contiene il numero di raccomandazioni aggiuntive disponibili. Selezionando l’icona della lampadina viene visualizzato un elenco dei consigli aggiuntivi. Potete scegliere una delle raccomandazioni alternative selezionando la casella di controllo accanto alla raccomandazione a cui desiderate eseguire la mappatura.

![](../images/tutorials/map-a-csv-file/multiple-recommendations.png)

In alternativa, puoi scegliere di mappare manualmente lo schema di origine sullo schema di destinazione. Passa il puntatore del mouse sullo schema di origine da mappare, quindi seleziona l’icona più .

![](../images/tutorials/map-a-csv-file/mapping-with-suggestions-and-buttons.png)

Viene visualizzato il puntatore **[!UICONTROL Map source to target field]** . Da qui puoi selezionare il campo da mappare, seguito da **[!UICONTROL Save]** per aggiungere la nuova mappatura.

![](../images/tutorials/map-a-csv-file/manual-mapping.png)

Per rimuovere una delle mappature, posiziona il cursore del mouse su tale mappatura, quindi seleziona l’icona meno .

### Aggiungi campo calcolato

I campi calcolati consentono la creazione di valori in base agli attributi nello schema di input. Questi valori possono quindi essere assegnati agli attributi nello schema di destinazione e ricevere un nome e una descrizione per facilitarne il riferimento.

Selezionare il pulsante **[!UICONTROL Add calculated field]** per continuare.

![](../images/tutorials/map-a-csv-file/add-calculated-field.png)

Viene visualizzato il pannello **[!UICONTROL Create calculated field]** . La finestra di dialogo a sinistra contiene i campi, le funzioni e gli operatori supportati nei campi calcolati. Seleziona una delle schede per iniziare ad aggiungere funzioni, campi o operatori all’editor di espressioni.

![](../images/tutorials/map-a-csv-file/create-calculated-fields.png)

| Scheda | Descrizione |
| --------- | ----------- |
| Campi | Nella scheda Campi sono elencati i campi e gli attributi disponibili nello schema di origine. |
| Funzioni | Nella scheda Funzioni sono elencate le funzioni disponibili per la trasformazione dei dati. Per ulteriori informazioni sulle funzioni che è possibile utilizzare all&#39;interno dei campi calcolati, leggere la guida sulle funzioni [Preparazione dati (mappatore)](../../data-prep/functions.md). |
| Operatori | La scheda operatori elenca gli operatori disponibili per la trasformazione dei dati. |

Puoi aggiungere manualmente campi, funzioni e operatori utilizzando l’editor espressioni al centro. Seleziona l’editor per iniziare a creare un’espressione.

![](../images/tutorials/map-a-csv-file/create-calculated-field.png)

Selezionare **[!UICONTROL Save]** per continuare.

La schermata di mappatura viene visualizzata nuovamente con il campo sorgente appena creato. Applica il campo di destinazione corrispondente appropriato e seleziona **[!UICONTROL Finish]** per completare la mappatura.

![](../images/tutorials/map-a-csv-file/new-calculated-field.png)

## Monitorare l’acquisizione di dati

Una volta mappato e creato il file CSV, puoi monitorare i dati che vengono acquisiti tramite di esso. Per ulteriori informazioni sul monitoraggio dell’inserimento dei dati, consulta l’esercitazione sul [monitoraggio dell’inserimento dei dati](../../ingestion/quality/monitor-data-ingestion.md).

## Passaggi successivi

Seguendo questa esercitazione, hai mappato correttamente un file CSV semplice su uno schema XDM e lo hai acquisito in [!DNL Platform]. Questi dati possono ora essere utilizzati dai servizi a valle [!DNL Platform] come [!DNL Real-time Customer Profile]. Per ulteriori informazioni, consulta la panoramica di [[!DNL Real-time Customer Profile]](../../profile/home.md) .
