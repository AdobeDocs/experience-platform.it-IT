---
title: Mappare un file CSV su uno schema XDM utilizzando Recommendations generato dall’intelligenza artificiale
description: Questa esercitazione illustra come mappare un file CSV su uno schema XDM utilizzando i consigli generati dall’intelligenza artificiale.
exl-id: 1daedf0b-5a25-4ca5-ae5d-e9ee1eae9e4d
source-git-commit: df6f76be6beba962b1795bd33dc753ef04267734
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 1%

---

# Mappare un file CSV su uno schema XDM utilizzando i consigli generati dall’intelligenza artificiale

>[!NOTE]
>
>Per informazioni sulle funzionalità di mappatura CSV disponibili in Platform, consulta il documento su [mappatura di un file CSV su uno schema esistente](./existing-schema.md).

Per acquisire dati CSV in [!DNL Adobe Experience Platform], i dati devono essere mappati su un [!DNL Experience Data Model] Schema (XDM). Puoi scegliere di eseguire la mappatura su [uno schema esistente](./existing-schema.md), ma se non sai esattamente quale schema utilizzare o come dovrebbe essere strutturato, puoi invece utilizzare i consigli dinamici basati sui modelli di machine-learning (ML) nell’interfaccia utente di Platform.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di [!DNL Platform]:

* [[!DNL Experience Data Model (XDM System)]](../../../xdm/home.md): Il quadro standardizzato [!DNL Platform] organizza i dati sulla customer experience.
   * Come minimo, devi capire il concetto di [comportamenti in XDM](../../../xdm/home.md#data-behaviors), in modo da poter decidere se mappare i dati su un [!UICONTROL Profilo] classe (comportamento del record) o [!UICONTROL ExperienceEvent] Classe (comportamento delle serie temporali).
* [Acquisizione batch](../../batch-ingestion/overview.md): Il metodo [!DNL Platform] acquisisce i dati dai file di dati forniti dall’utente.
* [Preparazione dei dati di Adobe Experience Platform](../../batch-ingestion/overview.md): Una suite di funzionalità che ti consente di mappare e trasformare i dati acquisiti in modo che siano conformi agli schemi XDM. La documentazione su [Funzioni di preparazione dei dati](../../../data-prep/functions.md) è specifico per la mappatura dello schema.

## Fornire i dettagli del flusso di dati

Nell’interfaccia utente di Experience Platform, seleziona **[!UICONTROL Origini]** nella navigazione a sinistra. Sulla **[!UICONTROL Catalogo]** visualizzare, passare alla **[!UICONTROL Sistema locale]** categoria. Sotto **[!UICONTROL Caricamento file locale]**, seleziona **[!UICONTROL Aggiungi dati]**.

![La [!UICONTROL Origini] catalogo nell’interfaccia utente di Platform, con [!UICONTROL Aggiungi dati] sotto [!UICONTROL Caricamento file locale] selezionato.](../../images/tutorials/map-csv-recommendations/local-file-upload.png)

La **[!UICONTROL Mappa schema CSV XDM]** viene visualizzato il flusso di lavoro, a partire dal **[!UICONTROL Dettaglio flusso di dati]** passo.

Seleziona **[!UICONTROL Creare un nuovo schema utilizzando i consigli ML]**, causando la visualizzazione di nuovi controlli. Scegli la classe appropriata per i dati CSV da mappare ([!UICONTROL Profilo] o [!UICONTROL ExperienceEvent]). Facoltativamente, puoi utilizzare il menu a discesa per selezionare il settore rilevante per la tua attività, oppure lasciarlo vuoto se le categorie fornite non sono applicabili. Se l’organizzazione opera sotto una [business-to-business (B2B)](../../../xdm/tutorials/relationship-b2b.md) , seleziona il modello **[!UICONTROL Dati B2B]** casella di controllo.

![La [!UICONTROL Dettaglio flusso di dati] passo con l&#39;opzione di raccomandazione ML selezionata. [!UICONTROL Profilo] è selezionato per la classe e [!UICONTROL Telecomunicazioni] selezionato per il settore](../../images/tutorials/map-csv-recommendations/select-class-and-industry.png)

Da qui, fornisci un nome per lo schema che verrà creato dai dati CSV e un nome per il set di dati di output che conterrà i dati acquisiti in tale schema.

Facoltativamente, puoi configurare le seguenti funzionalità aggiuntive per il flusso di dati prima di procedere:

| Nome di ingresso | Descrizione |
| --- | --- |
| [!UICONTROL Descrizione] | Una descrizione del flusso di dati. |
| [!UICONTROL Diagnostica degli errori] | Quando questa opzione è attivata, vengono generati messaggi di errore per i batch appena acquisiti, che possono essere visualizzati al momento del recupero del batch corrispondente nel [API](../../batch-ingestion/api-overview.md). |
| [!UICONTROL Acquisizione parziale] | Se questa opzione è abilitata, i record validi per i nuovi dati batch verranno acquisiti entro una determinata soglia di errore. Questa soglia consente di configurare la percentuale di errori accettabili prima che l’intero batch non riesca. |
| [!UICONTROL Dettagli del flusso di dati] | Specifica un nome e una descrizione facoltative per il flusso di dati che porterà i dati CSV in Platform. Al flusso di dati viene assegnato automaticamente un nome predefinito all’avvio del flusso di lavoro. La modifica del nome è facoltativa. |
| [!UICONTROL Avvisi] | Seleziona da un elenco di [avvisi interni al prodotto](../../../observability/alerts/overview.md) che si desidera ricevere per quanto riguarda lo stato del flusso di dati una volta avviato. |

{style="table-layout:auto"}

Al termine della configurazione del flusso di dati, seleziona **[!UICONTROL Successivo]**.

![La [!UICONTROL Dettaglio flusso di dati] sezione completata.](../../images/tutorials/map-csv-recommendations/dataflow-detail-complete.png)

## Selezionare i dati

Sulla **[!UICONTROL Seleziona dati]** utilizza la colonna a sinistra per caricare il file CSV. È possibile selezionare **[!UICONTROL Scegliere i file]** per aprire una finestra di dialogo di esplorazione file da cui selezionare il file, oppure puoi trascinarlo e rilasciarlo direttamente nella colonna.

![La [!UICONTROL Scegliere i file] area con trascinamento e rilascio evidenziata all’interno della [!UICONTROL Seleziona dati] passo.](../../images/tutorials/map-csv-recommendations/upload-files.png)

Dopo aver caricato il file, viene visualizzata una sezione di dati di esempio che mostra le prime dieci righe dei dati ricevuti in modo da verificare che sia stato caricato correttamente. Seleziona **[!UICONTROL Next]** (Avanti) per continuare.

![Le righe di dati di esempio vengono compilate nell’area di lavoro](../../images/tutorials/map-csv-recommendations/data-uploaded.png)

## Configurare le mappature degli schemi

I modelli ML vengono eseguiti per generare un nuovo schema basato sulla configurazione del flusso di dati e sul file CSV caricato. Al termine del processo, la [!UICONTROL Mappatura] il passaggio si compila per mostrare le mappature per ogni singolo campo insieme alla visualizzazione completamente navigabile della struttura dello schema generata.

![La [!UICONTROL Mappatura] nell’interfaccia utente, mostra tutti i campi CSV mappati e la struttura dello schema risultante.](../../images/tutorials/map-csv-recommendations/schema-generated.png)

Da qui, è possibile [modificare le mappature dei campi](#edit-mappings) o [modificare i gruppi di campi a cui sono associati](#edit-schema) secondo le tue esigenze. Quando la risposta è soddisfacente, seleziona **[!UICONTROL Fine]** per completare la mappatura e avviare il flusso di dati configurato in precedenza. I dati CSV vengono acquisiti nel sistema e popolano un set di dati basato sulla struttura dello schema generata, pronto per essere utilizzato dai servizi Platform a valle.

![La [!UICONTROL Fine] pulsante selezionato, completamento del processo di mappatura CSV.](../../images/tutorials/map-csv-recommendations/finish-mapping.png)

### Modificare le mappature dei campi {#edit-mappings}

Utilizza l’anteprima della mappatura dei campi per modificare le mappature esistenti o rimuoverle completamente. Per ulteriori informazioni su come gestire un set di mappature nell’interfaccia utente, consulta [Guida all’interfaccia utente per la mappatura della preparazione dei dati](../../../data-prep/ui/mapping.md#mapping-interface).

### Modifica gruppi di campi {#edit-field-groups}

I campi CSV vengono mappati automaticamente ai gruppi di campi XDM esistenti utilizzando i modelli ML. Se desideri modificare il gruppo di campi per un particolare campo CSV, seleziona **[!UICONTROL Modifica]** accanto alla struttura dello schema.

![La [!UICONTROL Modifica] pulsante selezionato accanto alla struttura dello schema.](../../images/tutorials/map-csv-recommendations/edit-schema-structure.png)

Viene visualizzata una finestra di dialogo che consente di modificare il nome visualizzato, il tipo di dati e il gruppo di campi per qualsiasi campo della mappatura. Seleziona l’icona di modifica (![Icona Modifica](../../images/tutorials/map-csv-recommendations/edit-icon.png)) accanto a un campo sorgente per modificare i dettagli nella colonna di destra prima di selezionare **[!UICONTROL Applica]**.

![Gruppo di campi consigliato per un campo di origine da modificare.](../../images/tutorials/map-csv-recommendations/select-schema-field.png)

Una volta completata la regolazione delle raccomandazioni dello schema per i campi di origine, seleziona **[!UICONTROL Salva]** per applicare le modifiche.

## Passaggi successivi

Questa guida illustra come mappare un file CSV su uno schema XDM utilizzando consigli generati dall’intelligenza artificiale, per inserire tali dati in Platform tramite l’acquisizione batch.

Per i passaggi relativi alla mappatura di un file CSV su uno schema esistente, consulta [flusso di lavoro di mappatura dello schema esistente](./existing-schema.md). Per informazioni sui dati in streaming a Platform in tempo reale tramite connessioni sorgente precompilate, consulta [panoramica di origini](../../../sources/home.md).
