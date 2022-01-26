---
keywords: Experience Platform;home;argomenti comuni;streaming;connettore di archiviazione cloud;archiviazione cloud
solution: Experience Platform
title: Creare un flusso di dati in streaming per un’origine di archiviazione cloud nell’interfaccia utente
topic-legacy: overview
type: Tutorial
description: Un flusso di dati è un’attività pianificata che recupera e acquisisce dati da un’origine a un set di dati della Platform. Questa esercitazione fornisce i passaggi per configurare un nuovo flusso di dati utilizzando il connettore base di archiviazione cloud.
exl-id: 75deead6-ef3c-48be-aed2-c43d1f432178
source-git-commit: 38f64f2ba0b40a20528aac6efff0e2fd6bc12ed2
workflow-type: tm+mt
source-wordcount: '1055'
ht-degree: 0%

---

# Creare un flusso di dati in streaming per un’origine di archiviazione cloud nell’interfaccia utente

Un flusso di dati è un’attività pianificata che recupera e acquisisce dati da un’origine a un set di dati Adobe Experience Platform. Questa esercitazione fornisce i passaggi per creare un flusso di dati in streaming per un’origine di archiviazione cloud nell’interfaccia utente.

Prima di provare questa esercitazione, è necessario stabilire una connessione valida e autenticata tra l&#39;account di archiviazione cloud e Platform. Se non disponi già di una connessione autenticata, consulta una delle seguenti esercitazioni per informazioni sull’autenticazione degli account di archiviazione cloud in streaming:

- [[!DNL Amazon Kinesis]](../../../ui/create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../../../ui/create/cloud-storage/eventhub.md)
- [[!DNL Google PubSub]](../../../ui/create/cloud-storage/google-pubsub.md)

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [Flussi di dati](../../../../../dataflows/home.md): I flussi di dati sono una rappresentazione dei processi di trasferimento dei dati in Platform. I flussi di dati sono configurati su diversi servizi, dalle origini ai [!DNL Identity Service], a [!DNL Profile]e a [!DNL Destinations].
- [Preparazione dei dati](../../../../../data-prep/home.md): Data Prep consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM). La preparazione dei dati viene visualizzata come un passaggio &quot;Mappa&quot; nei processi di acquisizione dei dati, incluso il flusso di lavoro di acquisizione CSV.
- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il quadro standardizzato [!DNL Experience Platform] organizza i dati sulla customer experience.
   - [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   - [Esercitazione sull’Editor di schema](../../../../../xdm/tutorials/create-schema-ui.md): Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

## Aggiungi dati

Dopo aver creato l&#39;account di archiviazione cloud streaming autenticato, il **[!UICONTROL Seleziona dati]** viene visualizzato un passaggio che fornisce un’interfaccia per selezionare il flusso di dati che verrà portato in Platform.

- La parte sinistra dell’interfaccia è un browser che ti consente di visualizzare i flussi di dati disponibili all’interno del tuo account;
- La parte destra dell’interfaccia ti consente di visualizzare in anteprima fino a 100 righe di dati da un file JSON.

![interfaccia](../../../../images/tutorials/dataflow/cloud-storage/streaming/interface.png)

Selezionare il flusso di dati da utilizzare, quindi selezionare **[!UICONTROL Scegli file]** per caricare uno schema di esempio.

>[!TIP]
>
>Se i dati sono conformi a XDM, puoi saltare il caricamento di uno schema di esempio e selezionare **[!UICONTROL Successivo]** per procedere.

![select-stream](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-stream.png)

Una volta caricato lo schema, l&#39;interfaccia di anteprima si aggiorna per visualizzare un&#39;anteprima dello schema caricato. L’interfaccia di anteprima ti consente di esaminare il contenuto e la struttura di un file. È inoltre possibile utilizzare [!UICONTROL Campo di ricerca] utilità per accedere a elementi specifici dallo schema.

Al termine, seleziona **[!UICONTROL Successivo]**.

![schema-anteprima](../../../../images/tutorials/dataflow/cloud-storage/streaming/schema-preview.png)

## Mappatura

La **[!UICONTROL Mappatura]** viene visualizzato un passaggio che fornisce un’interfaccia per mappare i dati di origine a un set di dati di Platform.

Scegli un set di dati in entrata in cui acquisire i dati. Puoi utilizzare un set di dati esistente o crearne uno nuovo.

### Nuovo set di dati

Per acquisire dati in un nuovo set di dati, seleziona **[!UICONTROL Nuovo set di dati]** e immetti un nome e una descrizione per il set di dati nei campi forniti. Per aggiungere uno schema, è possibile immettere un nome di schema esistente nella **[!UICONTROL Seleziona schema]** finestra di dialogo. In alternativa, è possibile selezionare **[!UICONTROL Ricerca avanzata schema]** per cercare uno schema appropriato.

![nuovo set di dati](../../../../images/tutorials/dataflow/cloud-storage/streaming/new-dataset.png)

La [!UICONTROL Seleziona schema] viene visualizzata una finestra che fornisce un elenco degli schemi disponibili tra cui scegliere. Selezionare uno schema dall’elenco per aggiornare la barra a destra per visualizzare i dettagli specifici dello schema selezionato, incluse le informazioni sull’abilitazione dello schema per [!DNL Profile].

Dopo aver identificato e selezionato lo schema da utilizzare, selezionare **[!UICONTROL Fine]**.

![select-schema](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-schema.png)

La [!UICONTROL Set di dati di Target] aggiornamenti di pagina con lo schema selezionato visualizzato come parte del set di dati. Durante questo passaggio, puoi abilitare il set di dati per [!DNL Profile] e crea una visualizzazione olistica degli attributi e dei comportamenti di un&#39;entità. I dati di tutti i set di dati abilitati verranno inclusi in [!DNL Profile] e le modifiche vengono applicate al salvataggio del flusso di dati.

Attiva/disattiva la **[!UICONTROL Set di dati del profilo]** per abilitare il set di dati di destinazione per [!DNL Profile].

![nuovo profilo](../../../../images/tutorials/dataflow/cloud-storage/streaming/new-profile.png)

### Set di dati esistente

Per acquisire dati in un set di dati esistente, seleziona **[!UICONTROL Set di dati esistente]**, quindi seleziona l’icona del set di dati .

![set di dati esistente](../../../../images/tutorials/dataflow/cloud-storage/streaming/existing-dataset.png)

La **[!UICONTROL Seleziona set di dati]** viene visualizzata una finestra di dialogo che fornisce un elenco dei set di dati disponibili tra cui scegliere. Seleziona un set di dati dall’elenco per aggiornare la barra a destra in modo da visualizzare i dettagli specifici del set di dati selezionato, comprese informazioni sulla possibilità di abilitare il set di dati per [!DNL Profile].

Dopo aver identificato e selezionato il set di dati da utilizzare, seleziona **[!UICONTROL Fine]**.

![set di dati selezionati](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-dataset.png)

Dopo aver selezionato il set di dati, seleziona la [!DNL Profile] attiva/disattiva il set di dati per [!DNL Profile].

![profilo esistente](../../../../images/tutorials/dataflow/cloud-storage/streaming/existing-profile.png)

### Mappa campi standard

Con il set di dati e lo schema stabiliti, il **[!UICONTROL Mappa campi standard]** viene visualizzata un’interfaccia che consente di configurare manualmente i campi di mappatura per i dati.

>[!TIP]
>
>Platform fornisce consigli intelligenti per i campi mappati automaticamente in base allo schema o al set di dati di destinazione selezionato. Puoi regolare manualmente le regole di mappatura in base ai tuoi casi d’uso.

In base alle tue esigenze, puoi scegliere di mappare direttamente i campi oppure utilizzare le funzioni di preparazione dei dati per trasformare i dati di origine in valori calcolati o calcolati. Per i passaggi completi sull’utilizzo dell’interfaccia di mappatura e dei campi calcolati, consulta la sezione [Guida all’interfaccia utente della preparazione dei dati](../../../../../data-prep/ui/mapping.md).

Una volta mappati i dati di origine, seleziona **[!UICONTROL Successivo]**.

![mappatura](../../../../images/tutorials/dataflow/cloud-storage/streaming/mapping.png)

## Dettaglio flusso di dati

La **[!UICONTROL Dettaglio flusso di dati]** viene visualizzato un passaggio che ti consente di assegnare un nome e una breve descrizione del nuovo flusso di dati.

Immetti i valori per il flusso di dati e seleziona **[!UICONTROL Successivo]**.

![dettaglio del flusso di dati](../../../../images/tutorials/dataflow/cloud-storage/streaming/dataflow-detail.png)

### Revisione

La **[!UICONTROL Revisione]** viene visualizzato un passaggio che consente di rivedere il nuovo flusso di dati prima della creazione. I dettagli sono raggruppati nelle seguenti categorie:

- **[!UICONTROL Connessione]**: Visualizza il nome dell’account, il tipo di origine e altre informazioni varie specifiche dell’origine di archiviazione cloud in streaming che stai utilizzando.
- **[!UICONTROL Assegna set di dati e mappa campi]**: Visualizza il set di dati di destinazione e lo schema utilizzato per il flusso di dati.

Dopo aver esaminato il flusso di dati, seleziona **[!UICONTROL Fine]** e lascia un certo tempo per la creazione del flusso di dati.

![revisione](../../../../images/tutorials/dataflow/cloud-storage/streaming/review.png)

## Monitorare ed eliminare il flusso di dati

Una volta creato il flusso di dati di archiviazione cloud in streaming, puoi monitorare i dati che vengono acquisiti tramite di esso. Per ulteriori informazioni sul monitoraggio e l’eliminazione dei flussi di dati in streaming, consulta l’esercitazione su [monitoraggio dei flussi di dati in streaming](../../monitor-streaming.md).

## Passaggi successivi

Seguendo questa esercitazione, è stato creato correttamente un flusso di dati per lo streaming dei dati da un&#39;origine di archiviazione cloud. I dati in arrivo possono ora essere utilizzati dai servizi della piattaforma a valle, come [!DNL Real-time Customer Profile] e [!DNL Data Science Workspace]. Per ulteriori informazioni, consulta i seguenti documenti:

- [[!DNL Real-time Customer Profile] panoramica](../../../../../profile/home.md)
- [[!DNL Data Science Workspace] panoramica](../../../../../data-science-workspace/home.md)