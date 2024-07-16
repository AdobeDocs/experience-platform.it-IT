---
title: Mappare un file CSV a uno schema XDM utilizzando la funzione di Recommendations generata da IA
description: Questo tutorial illustra come mappare un file CSV a uno schema XDM utilizzando i consigli generati dall’intelligenza artificiale.
exl-id: 1daedf0b-5a25-4ca5-ae5d-e9ee1eae9e4d
source-git-commit: 6632086641004c2b788a28cbc47ac6d8bd4eace3
workflow-type: tm+mt
source-wordcount: '1100'
ht-degree: 1%

---

# Mappare un file CSV su uno schema XDM utilizzando i consigli generati dall’intelligenza artificiale

>[!NOTE]
>
>Per informazioni sulle funzionalità di mappatura CSV generalmente disponibili in Platform, consulta il documento [mappatura di un file CSV su uno schema esistente](./existing-schema.md).

Per acquisire i dati CSV in [!DNL Adobe Experience Platform], i dati devono essere mappati su uno schema [!DNL Experience Data Model] (XDM). Puoi scegliere di mappare a [uno schema esistente](./existing-schema.md), ma se non sai esattamente quale schema utilizzare o come dovrebbe essere strutturato, puoi invece utilizzare consigli dinamici basati su modelli di apprendimento automatico (ML) nell&#39;interfaccia utente di Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di [!DNL Platform]:

* [[!DNL Experience Data Model (XDM System)]](../../../xdm/home.md): framework standardizzato tramite il quale [!DNL Platform] organizza i dati sull&#39;esperienza del cliente.
   * Devi comprendere almeno il concetto di [comportamenti in XDM](../../../xdm/home.md#data-behaviors), in modo da poter decidere se mappare i dati a una classe [!UICONTROL Profile] (comportamento record) o [!UICONTROL ExperienceEvent] (comportamento serie temporale).
* [Acquisizione batch](../../batch-ingestion/overview.md): metodo con cui [!DNL Platform] acquisisce i dati dai file di dati forniti dall&#39;utente.
* [Preparazione dati di Adobe Experience Platform](../../batch-ingestion/overview.md): suite di funzionalità che consente di mappare e trasformare i dati acquisiti per adeguarli agli schemi XDM. La documentazione sulle [funzioni di preparazione dati](../../../data-prep/functions.md) è specifica per la mappatura dello schema.

## Fornisci i dettagli del flusso di dati

Nell&#39;interfaccia utente di Experience Platform, seleziona **[!UICONTROL Origini]** nell&#39;area di navigazione a sinistra. Nella visualizzazione **[!UICONTROL Catalogo]**, passare alla categoria **[!UICONTROL Sistema locale]**. In **[!UICONTROL Caricamento file locale]**, selezionare **[!UICONTROL Aggiungi dati]**.

![Il catalogo [!UICONTROL Sources] nell&#39;interfaccia utente di Platform, con [!UICONTROL Aggiungi dati] in [!UICONTROL Caricamento file locale] selezionato.](../../images/tutorials/map-csv-recommendations/local-file-upload.png)

Il flusso di lavoro **[!UICONTROL Mappa schema XDM CSV]** viene visualizzato a partire dal passaggio **[!UICONTROL Dettagli flusso di dati]**.

Seleziona **[!UICONTROL Crea un nuovo schema utilizzando ML recommendations]**, causando la visualizzazione di nuovi controlli. Scegli la classe appropriata per i dati CSV da mappare ([!UICONTROL Profilo] o [!UICONTROL ExperienceEvent]). Facoltativamente, puoi utilizzare il menu a discesa per selezionare il settore pertinente per la tua azienda, oppure lasciarlo vuoto se le categorie fornite non sono applicabili. Se l&#39;organizzazione opera con un modello [business-to-business (B2B)](../../../xdm/tutorials/relationship-b2b.md), selezionare la casella di controllo **[!UICONTROL dati B2B]**.

![Il passaggio [!UICONTROL Dettagli flusso di dati] con l&#39;opzione ML Recommendation selezionata. [!UICONTROL Profilo] selezionato per la classe e [!UICONTROL Telecomunicazioni] selezionato per il settore](../../images/tutorials/map-csv-recommendations/select-class-and-industry.png)

Da qui, fornisci un nome per lo schema che verrà creato dai dati CSV e un nome per il set di dati di output che conterrà i dati acquisiti in quello schema.

Facoltativamente, prima di procedere, puoi configurare le seguenti funzioni aggiuntive per il flusso di dati:

| Nome input | Descrizione |
| --- | --- |
| [!UICONTROL Descrizione] | Descrizione del flusso di dati. |
| [!UICONTROL Diagnostica errori] | Quando questa opzione è attivata, vengono generati messaggi di errore per i batch appena acquisiti, che possono essere visualizzati quando si recupera il batch corrispondente nell&#39;[API](../../batch-ingestion/api-overview.md). |
| [!UICONTROL Acquisizione parziale] | Quando questa opzione è attivata, i record validi per i nuovi dati batch verranno acquisiti entro una soglia di errore specificata. Questa soglia consente di configurare la percentuale di errori accettabili prima che l’intero batch abbia esito negativo. |
| [!UICONTROL Dettagli flusso di dati] | Fornisci un nome e una descrizione facoltativa per il flusso di dati che inserirà i dati CSV in Platform. All’avvio di questo flusso di lavoro, al flusso di dati viene automaticamente assegnato un nome predefinito. La modifica del nome è facoltativa. |
| [!UICONTROL Avvisi] | Seleziona da un elenco di [avvisi interni al prodotto](../../../observability/alerts/overview.md) che desideri ricevere relativi allo stato del flusso di dati una volta avviato. |

{style="table-layout:auto"}

Al termine della configurazione del flusso di dati, seleziona **[!UICONTROL Avanti]**.

![La sezione [!UICONTROL Dettagli flusso di dati] è stata completata.](../../images/tutorials/map-csv-recommendations/dataflow-detail-complete.png)

## Selezionare i dati

Nel passaggio **[!UICONTROL Seleziona dati]**, utilizza la colonna a sinistra per caricare il file CSV. È possibile selezionare **[!UICONTROL Scegli file]** per aprire una finestra di dialogo di Esplora file da cui selezionare il file oppure trascinare il file direttamente nella colonna.

![Il pulsante [!UICONTROL Scegli i file] e l&#39;area di trascinamento sono evidenziati nel passaggio [!UICONTROL Seleziona dati].](../../images/tutorials/map-csv-recommendations/upload-files.png)

Dopo aver caricato il file, viene visualizzata una sezione di dati di esempio che mostra le prime dieci righe dei dati ricevuti, in modo da verificare che siano stati caricati correttamente. Seleziona **[!UICONTROL Avanti]** per continuare.

![Le righe di dati di esempio sono popolate nell&#39;area di lavoro](../../images/tutorials/map-csv-recommendations/data-uploaded.png)

## Configurare le mappature dello schema

I modelli ML vengono eseguiti per generare un nuovo schema basato sulla configurazione del flusso di dati e sul file CSV caricato. Al termine del processo, il passaggio [!UICONTROL Mappatura] si popola per mostrare i mapping per ogni singolo campo insieme alla visualizzazione completamente navigabile della struttura dello schema generata.

![Il passaggio [!UICONTROL Mappatura] nell&#39;interfaccia utente, che mostra tutti i campi CSV mappati e la struttura dello schema risultante.](../../images/tutorials/map-csv-recommendations/schema-generated.png)

>[!NOTE]
>
>Puoi filtrare tutti i campi nello schema in base a diversi criteri durante il flusso di lavoro di mappatura dei campi da origine a destinazione. Per impostazione predefinita, vengono visualizzati tutti i campi mappati. Per modificare i campi visualizzati, selezionare l&#39;icona del filtro accanto al campo di input di ricerca e scegliere tra le opzioni del menu a discesa.<br> ![Fase di mappatura del flusso di lavoro di creazione dello schema da CSV a XDM con l&#39;icona del filtro e il menu a discesa evidenziati.](../../images/tutorials/map-csv-recommendations/source-field-to-target-mapping-filter.png "Fase di mappatura del flusso di lavoro di creazione dello schema da CSV a XDM con l&#39;icona del filtro e il menu a discesa evidenziati."){width="100" zoomable="yes"}

Da qui puoi [modificare i mapping dei campi](#edit-mappings) o [modificare i gruppi di campi a cui sono associati](#edit-schema) in base alle tue esigenze. Al termine, selezionare **[!UICONTROL Fine]** per completare la mappatura e avviare il flusso di dati configurato in precedenza. I dati CSV vengono acquisiti nel sistema e popolano un set di dati in base alla struttura dello schema generato, pronto per essere utilizzato dai servizi Platform a valle.

![Il pulsante [!UICONTROL Fine] è stato selezionato e ha completato il processo di mappatura CSV.](../../images/tutorials/map-csv-recommendations/finish-mapping.png)

### Modifica mappature campi {#edit-mappings}

Utilizza l’anteprima della mappatura dei campi per modificare o rimuovere completamente le mappature esistenti. Per ulteriori informazioni su come gestire un set di mappatura nell&#39;interfaccia utente, consulta la [guida dell&#39;interfaccia utente per la mappatura della preparazione dati](../../../data-prep/ui/mapping.md#mapping-interface).

### Modifica gruppi di campi {#edit-field-groups}

I campi CSV vengono mappati automaticamente ai gruppi di campi XDM esistenti utilizzando modelli ML. Se desideri modificare il gruppo di campi per un particolare campo CSV, seleziona **[!UICONTROL Modifica]** accanto alla struttura dello schema.

![Il pulsante [!UICONTROL Modifica] selezionato accanto alla struttura dello schema.](../../images/tutorials/map-csv-recommendations/edit-schema-structure.png)

Viene visualizzata una finestra di dialogo che consente di modificare il nome visualizzato, il tipo di dati e il gruppo di campi per qualsiasi campo della mappatura. Selezionare l&#39;icona di modifica (![icona Modifica](../../images/tutorials/map-csv-recommendations/edit-icon.png)) accanto a un campo di origine per modificarne i dettagli nella colonna di destra prima di selezionare **[!UICONTROL Applica]**.

![Gruppo di campi consigliato per un campo di origine in corso di modifica.](../../images/tutorials/map-csv-recommendations/select-schema-field.png)

Al termine della regolazione dei consigli di schema per i campi sorgente, seleziona **[!UICONTROL Salva]** per applicare le modifiche.

## Passaggi successivi

Questa guida illustra come mappare un file CSV a uno schema XDM utilizzando i consigli generati dall’intelligenza artificiale, per portare tali dati in Platform tramite l’acquisizione batch.

Per i passaggi sulla mappatura di un file CSV a uno schema esistente, consulta il [flusso di lavoro di mappatura schema esistente](./existing-schema.md). Per informazioni sullo streaming in tempo reale dei dati a Platform tramite connessioni di origine predefinite, consulta la [panoramica sulle origini](../../../sources/home.md).
