---
keywords: Experience Platform;home;argomenti popolari;schema crm;CRM;flusso di dati;flusso di dati
solution: Experience Platform
title: Configurare un flusso di dati per una connessione sorgente di gestione delle relazioni con i clienti nell’interfaccia utente
topic-legacy: overview
type: Tutorial
description: Un flusso di dati è un’attività pianificata che recupera e acquisisce dati da un’origine a un set di dati della Platform. Questa esercitazione fornisce i passaggi per configurare un nuovo flusso di dati utilizzando il tuo account CRM.
exl-id: e14eafa7-6594-48e6-ab7a-f6c928d1e5fb
source-git-commit: 38f64f2ba0b40a20528aac6efff0e2fd6bc12ed2
workflow-type: tm+mt
source-wordcount: '1415'
ht-degree: 0%

---

# Configurare un flusso di dati per una connessione CRM nell’interfaccia utente

Un flusso di dati è un’attività pianificata che recupera e acquisisce dati da un’origine a un set di dati della Platform. Questa esercitazione fornisce i passaggi per configurare un nuovo flusso di dati utilizzando il tuo account CRM.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../xdm/home.md): Il quadro standardizzato [!DNL Experience Platform] organizza i dati sulla customer experience.
   * [Nozioni di base sulla composizione dello schema](../../../../xdm/schema/composition.md): Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’Editor di schema](../../../../xdm/tutorials/create-schema-ui.md): Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-time Customer Profile]](../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Inoltre, questa esercitazione richiede che tu abbia già creato un account CRM. Un elenco di esercitazioni per la creazione di diversi connettori di gestione delle relazioni con i clienti nell’interfaccia utente è disponibile nella sezione [panoramica dei connettori sorgente](../../../home.md).

## Seleziona dati

Dopo aver creato il tuo account CRM, [!UICONTROL Seleziona dati] viene visualizzato un passaggio che fornisce un’interfaccia per l’esplorazione della gerarchia dei file.

* La metà sinistra dell&#39;interfaccia è un browser di directory che visualizza i file e le directory del CRM.
* La metà destra dell’interfaccia consente di visualizzare in anteprima fino a 100 righe di dati da un file compatibile.

È possibile utilizzare **[!UICONTROL Ricerca]** nella parte superiore della pagina per identificare rapidamente i dati di origine che intendi utilizzare.

>[!NOTE]
>
>L’opzione per i dati dell’origine di ricerca è disponibile per tutti i connettori sorgente basati su tabelle, esclusi i connettori Analytics, Classificazioni, Hubs evento e Kinesis.

Una volta trovati i dati di origine, seleziona la directory, quindi seleziona **[!UICONTROL Successivo]**.

![select-data](../../../images/tutorials/dataflow/all-tabular/select-data.png)

## Mappatura di campi dati su uno schema XDM

La **[!UICONTROL Mappatura]** viene visualizzato un passaggio che fornisce un’interfaccia per mappare i dati di origine a un set di dati di Platform.

Scegli un set di dati in entrata in cui acquisire i dati. Puoi utilizzare un set di dati esistente o crearne uno nuovo.

### Utilizzare un set di dati esistente

Per acquisire dati in un set di dati esistente, seleziona **[!UICONTROL Set di dati esistente]**, quindi seleziona l’icona dei dati ![dati](../../../images/tutorials/dataflow/crm/data.png) accanto alla barra di ingresso.

![set di dati esistente](../../../images/tutorials/dataflow/crm/existing-dataset.png)

La **[!UICONTROL Seleziona set di dati]** viene visualizzata la finestra di dialogo . Trova il set di dati che desideri utilizzare, selezionalo, quindi fai clic su **[!UICONTROL Continua]**.

![set di dati selezionati](../../../images/tutorials/dataflow/crm/select-dataset.png)

### Utilizzare un nuovo set di dati

Per acquisire dati in un nuovo set di dati, seleziona **[!UICONTROL Nuovo set di dati]** e immetti un nome e una descrizione per il set di dati nei campi forniti.

È possibile allegare un campo schema immettendo un nome schema nel **[!UICONTROL Seleziona schema]** barra di ricerca. Puoi anche selezionare l’icona a discesa per visualizzare un elenco degli schemi esistenti. In alternativa, è possibile selezionare **[!UICONTROL Ricerca avanzata]** accedere alla schermata degli schemi esistenti, compresi i rispettivi dettagli.

Durante questo passaggio, puoi abilitare il set di dati per [!DNL Real-time Customer Profile] e crea una visualizzazione olistica degli attributi e dei comportamenti di un&#39;entità. I dati di tutti i set di dati abilitati verranno inclusi in [!DNL Profile] e le modifiche vengono applicate al salvataggio del flusso di dati.

Attiva/disattiva la **[!UICONTROL Set di dati del profilo]** per abilitare il set di dati di destinazione per [!DNL Profile].

![create-new-dataset](../../../images/tutorials/dataflow/crm/new-dataset.png)

La **[!UICONTROL Seleziona schema]** viene visualizzata la finestra di dialogo . Seleziona lo schema da applicare al nuovo set di dati, quindi fai clic su **[!UICONTROL Fine]**.

![select-schema](../../../images/tutorials/dataflow/crm/select-schema.png)

In base alle tue esigenze, puoi scegliere di mappare direttamente i campi oppure utilizzare le funzioni di preparazione dei dati per trasformare i dati di origine in valori calcolati o calcolati. Per i passaggi completi sull’utilizzo dell’interfaccia di mappatura e dei campi calcolati, consulta la sezione [Guida all’interfaccia utente della preparazione dei dati](../../../../data-prep/ui/mapping.md)

>[!TIP]
>
>Se utilizzi [!DNL Salesforce] come parte del CDP B2B, fare riferimento al [[!DNL Salesforce] tabelle di mappatura dei campi](../../../connectors/adobe-applications/mapping/salesforce.md) per una guida sui set di mappature appropriati tra [!DNL Salesforce] campi di origine e campi di destinazione XDM.

Platform fornisce consigli intelligenti per i campi mappati automaticamente in base allo schema o al set di dati di destinazione selezionato. Puoi regolare manualmente le regole di mappatura in base ai tuoi casi d’uso.

Seleziona **[!UICONTROL Anteprima dati]** per visualizzare i risultati della mappatura di fino a 100 righe di dati di esempio dal set di dati selezionato.

![](../../../images/tutorials/dataflow/crm/preview-data.png)

Durante l’anteprima, la colonna Identity ha la priorità come primo campo, in quanto rappresenta le informazioni chiave necessarie per la convalida dei risultati della mappatura.

Una volta mappati i dati di origine, seleziona **[!UICONTROL Chiudi]**.

![](../../../images/tutorials/dataflow/crm/preview.png)

Successivo, dal [!UICONTROL Mappatura] schermata, seleziona **[!UICONTROL Successivo]** per procedere.

![](../../../images/tutorials/dataflow/crm/mapping.png)

## Pianifica esecuzioni di acquisizione

La **[!UICONTROL Pianificazione]** viene visualizzato un passaggio che consente di configurare una pianificazione dell’acquisizione per l’acquisizione automatica dei dati di origine selezionati utilizzando le mappature configurate. La tabella seguente illustra i diversi campi configurabili per la pianificazione:

| Campo | Descrizione |
| --- | --- |
| Frequenza | Le frequenze selezionabili includono `Once`, `Minute`, `Hour`, `Day`e `Week`. |
| Intervallo | Un numero intero che imposta l&#39;intervallo per la frequenza selezionata. |
| Ora di inizio | Una marca temporale UTC che indica quando è impostata la prima acquisizione. |
| Backfill | Un valore booleano che determina i dati inizialmente acquisiti. Se **[!UICONTROL Backfill]** è attivato, tutti i file correnti nel percorso specificato verranno acquisiti durante la prima acquisizione pianificata. Se **[!UICONTROL Backfill]** è disabilitato, solo i file caricati tra la prima esecuzione dell’acquisizione e il **[!UICONTROL Ora di inizio]** verranno acquisiti. File caricati prima di **[!UICONTROL Ora di inizio]** non vengono acquisiti. |
| Colonna Delta | Opzione con un set filtrato di campi dello schema di origine di tipo, data o ora. Questo campo viene utilizzato per distinguere tra dati nuovi ed esistenti. I dati incrementali verranno acquisiti in base al timestamp della colonna selezionata. |

I flussi di dati sono progettati per acquisire automaticamente i dati su base pianificata. Inizia selezionando la frequenza di acquisizione. Quindi, impostare l&#39;intervallo per indicare il periodo tra due esecuzioni di flusso. Il valore dell&#39;intervallo deve essere un numero intero diverso da zero e deve essere impostato su maggiore o uguale a 15.

Per impostare l’ora di inizio per l’acquisizione, regola la data e l’ora visualizzate nella casella dell’ora di inizio. In alternativa, puoi selezionare l’icona del calendario per modificare il valore dell’ora di inizio. L’ora di inizio deve essere maggiore o uguale all’ora UTC corrente.

Seleziona **[!UICONTROL Carica dati incrementali per]** per assegnare la colonna delta. Questo campo distingue tra dati nuovi ed esistenti.

![](../../../images/tutorials/dataflow/crm/scheduling.png)

### Configurare un flusso di dati di acquisizione una tantum

Per impostare l’acquisizione una tantum, seleziona la freccia a discesa della frequenza e seleziona **[!UICONTROL Una volta]**.

>[!TIP]
>
>**[!UICONTROL Intervallo]** e **[!UICONTROL Backfill]** non sono visibili durante un’acquisizione una tantum.

Dopo aver fornito i valori appropriati alla pianificazione, seleziona **[!UICONTROL Successivo]**.

![pianificazione](../../../images/tutorials/dataflow/crm/one-time-ingestion.png)

## Fornire i dettagli del flusso di dati

La **[!UICONTROL Dettaglio flusso di dati]** viene visualizzato un passaggio che ti consente di assegnare un nome e una breve descrizione del nuovo flusso di dati.

Durante questo processo, puoi anche abilitare **[!UICONTROL Acquisizione parziale]** e **[!UICONTROL Diagnostica degli errori]**. Abilitazione **[!UICONTROL Acquisizione parziale]** consente di acquisire dati contenenti errori fino a una determinata soglia. Una volta **[!UICONTROL Acquisizione parziale]** è abilitato, trascina **[!UICONTROL Soglia errore %]** per regolare la soglia di errore del batch. In alternativa, è possibile regolare manualmente la soglia selezionando la casella di input. Per ulteriori informazioni, consulta la sezione [panoramica dell’acquisizione parziale in batch](../../../../ingestion/batch-ingestion/partial.md).

Immetti i valori per il flusso di dati e seleziona **[!UICONTROL Successivo]**.

![dataflow-details](../../../images/tutorials/dataflow/crm/dataflow-detail.png)

## Controlla il tuo flusso di dati

La *Revisione* viene visualizzato un passaggio che consente di rivedere il nuovo flusso di dati prima della creazione. I dettagli sono raggruppati nelle seguenti categorie:

* **[!UICONTROL Connessione]**: Visualizza il nome dell&#39;account di origine, la piattaforma di origine, il percorso pertinente del file di origine scelto e la quantità di colonne all&#39;interno del file di origine.
* **[!UICONTROL Assegna set di dati e mappa campi]**: Visualizza il set di dati di destinazione in cui vengono acquisiti i dati di origine, incluso lo schema a cui il set di dati aderisce.
* **[!UICONTROL Pianificazione]**: Visualizza l&#39;ora di inizio e la frequenza del flusso di dati.

Dopo aver esaminato il flusso di dati, fai clic su **[!UICONTROL Fine]** e lascia un certo tempo per la creazione del flusso di dati.

![revisione](../../../images/tutorials/dataflow/crm/review.png)

## Monitorare il flusso di dati

Una volta creato il flusso di dati, puoi monitorare i dati che vengono acquisiti tramite di esso per visualizzare informazioni sui tassi di acquisizione, sul successo e sugli errori. Per ulteriori informazioni su come monitorare il flusso di dati, consulta l’esercitazione su [monitoraggio di account e flussi di dati nell’interfaccia utente](../monitor.md).

## Elimina il flusso di dati

È possibile eliminare i flussi di dati che non sono più necessari o che sono stati creati in modo errato utilizzando **[!UICONTROL Elimina]** funzione disponibile nella **[!UICONTROL Flussi di dati]** workspace. Per ulteriori informazioni su come eliminare i flussi di dati, consulta l’esercitazione su [eliminazione dei flussi di dati nell’interfaccia utente](../delete.md).

## Passaggi successivi

Seguendo questa esercitazione, hai creato correttamente un flusso di dati per inserire i dati da un CRM e hai acquisito informazioni sul monitoraggio dei set di dati. Per ulteriori informazioni sulla creazione di flussi di dati, è possibile completare l&#39;apprendimento guardando il video sottostante. Inoltre, i dati in arrivo possono ora essere utilizzati dai servizi della piattaforma a valle, come [!DNL Real-time Customer Profile] e [!DNL Data Science Workspace]. Per ulteriori informazioni, consulta i seguenti documenti:

* [Panoramica del profilo cliente in tempo reale](../../../../profile/home.md)
* [Panoramica di Data Science Workspace](../../../../data-science-workspace/home.md)

>[!WARNING]
>
> L’interfaccia utente della piattaforma mostrata nel video seguente è obsoleta. Fai riferimento alla documentazione precedente per le ultime schermate e funzionalità dell’interfaccia utente.
>
>[!VIDEO](https://video.tv.adobe.com/v/29711?quality=12&learn=on)
