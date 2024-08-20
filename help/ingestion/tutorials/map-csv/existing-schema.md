---
keywords: Experience Platform;home;argomenti popolari;mappare csv;mappare file csv;mappare file csv a xdm;mappare csv a xdm;guida interfaccia utente;
solution: Experience Platform
title: Mappare un file CSV a uno schema XDM esistente
type: Tutorial
description: Questo tutorial illustra come mappare un file CSV a uno schema XDM esistente utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 15f55562-269d-421d-ad3a-5c10fb8f109c
source-git-commit: 15de9351203f6b43653042ab73ede17781486160
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 1%

---

# Mappare un file CSV su uno schema XDM esistente

>[!NOTE]
>
>Questo documento illustra come mappare un file CSV a uno schema XDM esistente. Per informazioni su come utilizzare lo strumento di consigli per gli schemi generati dall&#39;intelligenza artificiale (attualmente in versione beta), consulta il documento su [mappatura di un file CSV utilizzando i consigli di apprendimento automatico](./recommendations.md).

Per acquisire i dati CSV in [!DNL Adobe Experience Platform], i dati devono essere mappati su uno schema [!DNL Experience Data Model] (XDM). Questo tutorial illustra come mappare un file CSV a uno schema XDM utilizzando l&#39;interfaccia utente [!DNL Platform].

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di [!DNL Platform]:

- [[!DNL Experience Data Model (XDM System)]](../../../xdm/home.md): framework standardizzato tramite il quale [!DNL Platform] organizza i dati sull&#39;esperienza del cliente.
- [Acquisizione batch](../../batch-ingestion/overview.md): metodo con cui [!DNL Platform] acquisisce i dati dai file di dati forniti dall&#39;utente.
- [Preparazione dati di Adobe Experience Platform](../../batch-ingestion/overview.md): suite di funzionalità che consente di mappare e trasformare i dati acquisiti per adeguarli agli schemi XDM. La documentazione sulle [funzioni di preparazione dati](../../../data-prep/functions.md) è particolarmente rilevante per la mappatura dello schema.

Questo tutorial richiede anche di aver già creato un set di dati in cui acquisire i dati CSV. Per i passaggi relativi alla creazione di un set di dati nell&#39;interfaccia utente, consulta l&#39;[esercitazione sull&#39;acquisizione dei dati](../ingest-batch-data.md).

## Scegli una destinazione

Accedi a [[!DNL Adobe Experience Platform]](https://platform.adobe.com) e seleziona **[!UICONTROL Flussi di lavoro]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro **[!UICONTROL Flussi di lavoro]**.

Dalla schermata **[!UICONTROL Flussi di lavoro]**, seleziona **[!UICONTROL Mappa CSV a schema XDM]** nella sezione **[!UICONTROL Acquisizione dati]**, quindi seleziona **[!UICONTROL Avvia]**.

![](../../images/tutorials/map-a-csv-file/workflows.png)

Il flusso di lavoro **[!UICONTROL Mappa CSV a schema XDM]** viene visualizzato a partire dal passaggio **[!UICONTROL Destinazione]**. Scegli un set di dati per i dati in entrata da acquisire in. Puoi utilizzare un set di dati esistente o crearne uno nuovo.

**Utilizza un set di dati esistente**

Per acquisire i dati CSV in un set di dati esistente, seleziona **[!UICONTROL Usa set di dati esistente]**. Puoi recuperare un set di dati esistente utilizzando la funzione di ricerca oppure scorrendo l’elenco dei set di dati esistenti nel pannello.

![](../../images/tutorials/map-a-csv-file/use-existing-dataset.png)

Per acquisire i dati CSV in un nuovo set di dati, seleziona **[!UICONTROL Crea nuovo set di dati]** e immetti un nome e una descrizione per il set di dati nei campi forniti. Seleziona uno schema utilizzando la funzione di ricerca o scorrendo l’elenco degli schemi forniti. Seleziona **[!UICONTROL Avanti]** per procedere.

![](../../images/tutorials/map-a-csv-file/create-new-dataset.png)

## Aggiungi dati

Viene visualizzato il passaggio **[!UICONTROL Aggiungi dati]**. Trascina il file CSV nello spazio fornito oppure seleziona **[!UICONTROL Scegli i file]** per inserire manualmente il file CSV.

![](../../images/tutorials/map-a-csv-file/add-data.png)

La sezione **[!UICONTROL Dati di esempio]** viene visualizzata dopo il caricamento del file, con le prime dieci righe di dati. Dopo aver confermato che i dati sono stati caricati come previsto, seleziona **[!UICONTROL Avanti]**.

![](../../images/tutorials/map-a-csv-file/sample-data.png)

## Mappare i campi CSV su campi schema XDM

Viene visualizzato il passaggio **[!UICONTROL Mapping]**. Le colonne del file CSV sono elencate in **[!UICONTROL Campo Source]**, con i campi dello schema XDM corrispondenti elencati in **[!UICONTROL Campo di destinazione]**.

[!DNL Platform] fornisce automaticamente consigli intelligenti per i campi mappati automaticamente in base allo schema di destinazione o al set di dati selezionato. Puoi regolare manualmente le regole di mappatura in base ai tuoi casi d’uso.

![](../../images/tutorials/map-a-csv-file/mapping-with-suggestions.png)

Per accettare tutti i valori di mapping di generazione automatica, selezionare la casella di controllo &quot;[!UICONTROL Accetta tutti i campi di destinazione]&quot;.

![](../../images/tutorials/map-a-csv-file/filled-mapping-with-suggestions.png)

A volte, per lo schema di origine sono disponibili più consigli. In questo caso, nella scheda di mappatura viene visualizzato il consiglio più importante, seguito da un cerchio blu contenente il numero di consigli aggiuntivi disponibili. Selezionando l’icona a forma di lampadina viene visualizzato un elenco dei consigli aggiuntivi. Puoi scegliere uno dei consigli alternativi selezionando la casella di controllo accanto al consiglio a cui desideri mappare.

![](../../images/tutorials/map-a-csv-file/multiple-recommendations.png)

In alternativa, puoi scegliere di mappare manualmente lo schema di origine sullo schema di destinazione. Passa il puntatore del mouse sullo schema di origine da mappare, quindi seleziona l’icona più.

![](../../images/tutorials/map-a-csv-file/mapping-with-suggestions-and-buttons.png)

Viene visualizzato il popover **[!UICONTROL Mappa origine su campo di destinazione]**. Da qui puoi selezionare il campo da mappare, seguito da **[!UICONTROL Salva]** per aggiungere la nuova mappatura.

![](../../images/tutorials/map-a-csv-file/manual-mapping.png)

Se vuoi rimuovere una delle mappature, passa il cursore su di essa, quindi seleziona l’icona meno.

### Aggiungi campo calcolato {#add-calculated-field}

I campi calcolati consentono la creazione di valori in base agli attributi nello schema di input. Questi valori possono quindi essere assegnati ad attributi nello schema di destinazione e ricevere un nome e una descrizione per consentire un riferimento più semplice.

Selezionare il pulsante **[!UICONTROL Aggiungi campo calcolato]** per continuare.

![](../../images/tutorials/map-a-csv-file/add-calculated-field.png)

Viene visualizzato il pannello **[!UICONTROL Crea campo calcolato]**. La finestra di dialogo a sinistra contiene i campi, le funzioni e gli operatori supportati nei campi calcolati. Seleziona una delle schede per iniziare ad aggiungere funzioni, campi o operatori all’editor di espressioni.

![](../../images/tutorials/map-a-csv-file/create-calculated-fields.png)

| Scheda | Descrizione |
| --------- | ----------- |
| Campi | Nella scheda Campi sono elencati i campi e gli attributi disponibili nello schema di origine. |
| Funzioni | Nella scheda Funzioni sono elencate le funzioni disponibili per la trasformazione dei dati. Per ulteriori informazioni sulle funzioni utilizzabili nei campi calcolati, leggere la guida sulle [funzioni di preparazione dati (mapper)](../../../data-prep/functions.md). |
| Operatori | Nella scheda operatori sono elencati gli operatori disponibili per la trasformazione dei dati. |

Puoi aggiungere manualmente campi, funzioni e operatori utilizzando l’editor di espressioni al centro. Seleziona l’editor per iniziare a creare un’espressione.

![](../../images/tutorials/map-a-csv-file/create-calculated-field.png)

Seleziona **[!UICONTROL Salva]** per continuare.

Viene visualizzata di nuovo la schermata di mappatura con il campo sorgente appena creato. Applica il campo di destinazione corrispondente appropriato e seleziona **[!UICONTROL Fine]** per completare la mappatura.

![](../../images/tutorials/map-a-csv-file/new-calculated-field.png)

## Monitorare l’acquisizione dei dati

Una volta mappato e creato il file CSV, puoi monitorare i dati che vengono acquisiti tramite di esso. Per ulteriori informazioni sul monitoraggio dell&#39;acquisizione dei dati, consulta l&#39;esercitazione su [monitoraggio dell&#39;acquisizione dei dati](../../../ingestion/quality/monitor-data-ingestion.md).

## Passaggi successivi

Seguendo questa esercitazione, hai mappato correttamente un file CSV flat su uno schema XDM e lo hai acquisito in [!DNL Platform]. Questi dati possono ora essere utilizzati dai servizi [!DNL Platform] downstream come [!DNL Real-Time Customer Profile]. Per ulteriori informazioni, vedere la panoramica di [[!DNL Real-Time Customer Profile]](../../../profile/home.md).

>[!TIP]
>
>È inoltre possibile utilizzare gli algoritmi di apprendimento automatico (ML) per **generare uno schema dai dati di esempio** dall&#39;area di lavoro Schema. Questo flusso di lavoro crea automaticamente un nuovo schema in base alla struttura e al contenuto del file, garantendo che lo schema corrisponda al formato dei dati. In questo modo è possibile risparmiare tempo e migliorare la precisione durante la definizione della struttura, dei campi e dei tipi di dati per set di dati complessi di grandi dimensioni. Per ulteriori informazioni su questo flusso di lavoro, consulta la [Guida alla creazione di schemi assistiti da ML](../../../xdm/ui/ml-assisted-schema-creation.md).
