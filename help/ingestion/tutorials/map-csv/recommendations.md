---
title: Mappare un file CSV a uno schema XDM utilizzando la funzione di Recommendations generata da IA
description: Questo tutorial illustra come mappare un file CSV a uno schema XDM utilizzando i consigli generati dall’intelligenza artificiale.
exl-id: 1daedf0b-5a25-4ca5-ae5d-e9ee1eae9e4d
source-git-commit: df6f76be6beba962b1795bd33dc753ef04267734
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 1%

---

# Mappare un file CSV su uno schema XDM utilizzando i consigli generati dall’intelligenza artificiale

>[!NOTE]
>
>Per informazioni sulle funzionalità di mappatura CSV generalmente disponibili in Platform, consulta il documento su [mappatura di un file CSV a uno schema esistente](./existing-schema.md).

Per acquisire i dati CSV in [!DNL Adobe Experience Platform], i dati devono essere mappati su un [!DNL Experience Data Model] (XDM). Puoi scegliere di eseguire il mapping a [uno schema esistente](./existing-schema.md), ma se non sai esattamente quale schema utilizzare o come dovrebbe essere strutturato, puoi invece utilizzare consigli dinamici basati su modelli di apprendimento automatico (ML) nell’interfaccia utente di Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di [!DNL Platform]:

* [[!DNL Experience Data Model (XDM System)]](../../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Platform] organizza i dati sull’esperienza del cliente.
   * Devi comprendere almeno il concetto di [comportamenti in XDM](../../../xdm/home.md#data-behaviors), in modo da poter decidere se mappare i dati su [!UICONTROL Profilo] classe (comportamento record) o [!UICONTROL ExperienceEvent] classe (comportamento delle serie temporali).
* [Acquisizione in batch](../../batch-ingestion/overview.md): il metodo con cui [!DNL Platform] acquisisce i dati dai file di dati forniti dall’utente.
* [Preparazione dati di Adobe Experience Platform](../../batch-ingestion/overview.md): suite di funzionalità che consente di mappare e trasformare i dati acquisiti per renderli conformi agli schemi XDM. La documentazione su [Funzioni di preparazione dati](../../../data-prep/functions.md) è particolarmente rilevante per la mappatura dello schema.

## Fornisci i dettagli del flusso di dati

Nell’interfaccia utente di Experience Platform, seleziona **[!UICONTROL Sorgenti]** nel menu di navigazione a sinistra. Il giorno **[!UICONTROL Catalogo]** visualizzare, passare alla **[!UICONTROL Sistema locale]** categoria. Sotto **[!UICONTROL Caricamento di file locali]**, seleziona **[!UICONTROL Aggiungi dati]**.

![Il [!UICONTROL Sorgenti] nell’interfaccia utente di Platform, con [!UICONTROL Aggiungi dati] in [!UICONTROL Caricamento di file locali] in fase di selezione.](../../images/tutorials/map-csv-recommendations/local-file-upload.png)

Il **[!UICONTROL Mappa lo schema XDM CSV]** viene visualizzato il flusso di lavoro, a partire dal **[!UICONTROL Dettagli del flusso di dati]** passaggio.

Seleziona **[!UICONTROL Creare un nuovo schema utilizzando ML recommendations]**, causando la visualizzazione di nuovi controlli. Scegli la classe appropriata per i dati CSV da mappare ([!UICONTROL Profilo] o [!UICONTROL ExperienceEvent]). Facoltativamente, puoi utilizzare il menu a discesa per selezionare il settore pertinente per la tua azienda, oppure lasciarlo vuoto se le categorie fornite non sono applicabili. Se l’organizzazione opera in un [business-to-business (B2B)](../../../xdm/tutorials/relationship-b2b.md) modello, seleziona la **[!UICONTROL Dati B2B]** casella di controllo.

![Il [!UICONTROL Dettagli del flusso di dati] passo con l&#39;opzione ML Recommendation selezionata. [!UICONTROL Profilo] è selezionato per la classe e [!UICONTROL Telecomunicazioni] selezionato per il settore](../../images/tutorials/map-csv-recommendations/select-class-and-industry.png)

Da qui, fornisci un nome per lo schema che verrà creato dai dati CSV e un nome per il set di dati di output che conterrà i dati acquisiti in quello schema.

Facoltativamente, prima di procedere, puoi configurare le seguenti funzioni aggiuntive per il flusso di dati:

| Nome input | Descrizione |
| --- | --- |
| [!UICONTROL Descrizione] | Descrizione del flusso di dati. |
| [!UICONTROL Diagnostica degli errori] | Quando questa opzione è abilitata, vengono generati messaggi di errore per i batch appena acquisiti, che possono essere visualizzati quando si recupera il batch corrispondente in [API](../../batch-ingestion/api-overview.md). |
| [!UICONTROL Acquisizione parziale] | Quando questa opzione è attivata, i record validi per i nuovi dati batch verranno acquisiti entro una soglia di errore specificata. Questa soglia consente di configurare la percentuale di errori accettabili prima che l’intero batch abbia esito negativo. |
| [!UICONTROL Dettagli del flusso di dati] | Fornisci un nome e una descrizione facoltativa per il flusso di dati che inserirà i dati CSV in Platform. All’avvio di questo flusso di lavoro, al flusso di dati viene automaticamente assegnato un nome predefinito. La modifica del nome è facoltativa. |
| [!UICONTROL Avvisi] | Seleziona da un elenco di [avvisi interni al prodotto](../../../observability/alerts/overview.md) che desideri ricevere relativamente allo stato del flusso di dati una volta avviato. |

{style="table-layout:auto"}

Al termine della configurazione del flusso di dati, seleziona **[!UICONTROL Successivo]**.

![Il [!UICONTROL Dettagli del flusso di dati] sezione è stata completata.](../../images/tutorials/map-csv-recommendations/dataflow-detail-complete.png)

## Selezionare i dati

Il giorno **[!UICONTROL Seleziona dati]** , utilizza la colonna sinistra per caricare il file CSV. Puoi selezionare **[!UICONTROL Scegli i file]** per aprire una finestra di dialogo esplora file in cui selezionare il file oppure trascinare il file direttamente nella colonna.

![Il [!UICONTROL Scegli i file] e l&#39;area di trascinamento evidenziata all&#39;interno del [!UICONTROL Seleziona dati] passaggio.](../../images/tutorials/map-csv-recommendations/upload-files.png)

Dopo aver caricato il file, viene visualizzata una sezione di dati di esempio che mostra le prime dieci righe dei dati ricevuti, in modo da verificare che siano stati caricati correttamente. Seleziona **[!UICONTROL Next]** (Avanti) per continuare.

![Le righe di dati di esempio vengono popolate all’interno dell’area di lavoro](../../images/tutorials/map-csv-recommendations/data-uploaded.png)

## Configurare le mappature dello schema

I modelli ML vengono eseguiti per generare un nuovo schema basato sulla configurazione del flusso di dati e sul file CSV caricato. Al termine del processo, il [!UICONTROL Mappatura] step compila per mostrare le mappature per ogni singolo campo, insieme alla vista completamente navigabile della struttura dello schema generata.

![Il [!UICONTROL Mappatura] nell’interfaccia utente, mostrando tutti i campi CSV mappati e la struttura dello schema risultante.](../../images/tutorials/map-csv-recommendations/schema-generated.png)

Da qui, puoi opzionalmente [modificare le mappature dei campi](#edit-mappings) o [modificare i gruppi di campi a cui sono associati](#edit-schema) in base alle tue esigenze. Quando sei soddisfatto, seleziona **[!UICONTROL Fine]** per completare la mappatura e avviare il flusso di dati configurato in precedenza. I dati CSV vengono acquisiti nel sistema e popolano un set di dati in base alla struttura dello schema generato, pronto per essere utilizzato dai servizi Platform a valle.

![Il [!UICONTROL Fine] pulsante selezionato, completando il processo di mappatura CSV.](../../images/tutorials/map-csv-recommendations/finish-mapping.png)

### Modifica mappature campi {#edit-mappings}

Utilizza l’anteprima della mappatura dei campi per modificare o rimuovere completamente le mappature esistenti. Per ulteriori informazioni su come gestire un set di mappatura nell’interfaccia utente, consulta [Guida all’interfaccia utente per la mappatura della preparazione dati](../../../data-prep/ui/mapping.md#mapping-interface).

### Modifica gruppi di campi {#edit-field-groups}

I campi CSV vengono mappati automaticamente ai gruppi di campi XDM esistenti utilizzando modelli ML. Se desideri modificare il gruppo di campi per un particolare campo CSV, seleziona **[!UICONTROL Modifica]** accanto alla struttura dello schema.

![Il [!UICONTROL Modifica] accanto alla struttura dello schema.](../../images/tutorials/map-csv-recommendations/edit-schema-structure.png)

Viene visualizzata una finestra di dialogo che consente di modificare il nome visualizzato, il tipo di dati e il gruppo di campi per qualsiasi campo della mappatura. Seleziona l’icona Modifica (![Icona Modifica](../../images/tutorials/map-csv-recommendations/edit-icon.png)) accanto a un campo di origine per modificarne i dettagli nella colonna di destra prima di selezionare **[!UICONTROL Applica]**.

![Gruppo di campi consigliato per un campo di origine che viene modificato.](../../images/tutorials/map-csv-recommendations/select-schema-field.png)

Al termine della regolazione dei consigli di schema per i campi sorgente, seleziona **[!UICONTROL Salva]** per applicare le modifiche.

## Passaggi successivi

Questa guida illustra come mappare un file CSV a uno schema XDM utilizzando i consigli generati dall’intelligenza artificiale, per portare tali dati in Platform tramite l’acquisizione batch.

Per i passaggi sulla mappatura di un file CSV a uno schema esistente, consulta [flusso di lavoro di mappatura schema esistente](./existing-schema.md). Per informazioni sullo streaming dei dati in Platform in tempo reale tramite connessioni sorgente predefinite, consulta [panoramica sulle origini](../../../sources/home.md).
