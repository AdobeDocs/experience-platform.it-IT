---
title: Collegare i profili utente di Algolia ad Experience Platform tramite l’interfaccia utente
description: Scopri come collegare gli utenti dell’Algolia interessati ad Experience Platform
exl-id: d4c936a7-4983-4a12-a813-03b672116e44
source-git-commit: 9bc7d372eba9ffcfe64f90d2d58a532411e5f1ce
workflow-type: tm+mt
source-wordcount: '1136'
ht-degree: 1%

---

# Acquisire dati [!DNL Algolia User Profiles] in Experience Platform utilizzando l&#39;interfaccia utente

Leggi questo tutorial per scoprire come acquisire dati dall&#39;account [!DNL Algolia User Profiles] a Adobe Experience Platform utilizzando l&#39;interfaccia utente.

## Introduzione

>[!IMPORTANT]
>
>Prima di iniziare, assicurati di completare i passaggi preliminari descritti nella [[!DNL Algolia User Profiles] panoramica](../../../../connectors/data-partners/algolia-user-profiles.md#prerequisites).

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale Experience Platform organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Experience Platform.

### Raccogli le credenziali richieste

Per connettere [!DNL Algolia] ad Experience Platform, è necessario fornire i valori per le credenziali seguenti:

| Credenziali | Descrizione |
| --- | --- |
| ID applicazione | L&#39;ID applicazione [!DNL Algolia] è un identificatore univoco assegnato al tuo account [!DNL Algolia]. |
| Chiave API | La chiave API [!DNL Algolia] è una credenziale utilizzata per autenticare e autorizzare richieste API ai servizi di ricerca e indicizzazione di [!DNL Algolia]. |

Per ulteriori informazioni su queste credenziali, vedere la [!DNL Algolia] [documentazione sull&#39;autenticazione](https://www.algolia.com/doc/tools/cli/get-started/authentication/).

## Connetti il tuo account [!DNL Algolia]

Nell&#39;interfaccia utente di Experience Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro *[!UICONTROL Origini]*. Puoi selezionare la categoria appropriata nel pannello *[!UICONTROL Categorie]*. In alternativa, è possibile utilizzare la barra di ricerca per passare all&#39;origine specifica che si desidera utilizzare.

Per utilizzare [!DNL Algolia], seleziona la scheda di origine **[!UICONTROL Algolia]** in *[!UICONTROL Partner dati e identità]*, quindi seleziona **[!UICONTROL Configurazione]**.

>[!TIP]
>
>Le origini nel catalogo delle origini visualizzano l&#39;opzione **[!UICONTROL Configura]** quando un&#39;origine specificata non dispone ancora di un account autenticato. Quando esiste un account autenticato, questa opzione diventa **[!UICONTROL Aggiungi dati]**.

![Catalogo delle origini con l&#39;origine Profili utente Algolia selezionata.](../../../../images/tutorials/create/algolia/user-profiles/catalog.png)

## Autenticazione

### Usa un account esistente

Per utilizzare un account esistente, selezionare **[!UICONTROL Account esistente]**, quindi selezionare l&#39;account [!DNL Algolia User Profiles] che si desidera utilizzare. Per continuare, selezionare **[!UICONTROL Avanti]**.

![Interfaccia account esistente.](../../../../images/tutorials/create/algolia/user-profiles/existing-account.png)

### Crea un nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci un nome, una descrizione facoltativa e [!DNL Algolia] credenziali. Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![Nuova interfaccia account.](../../../../images/tutorials/create/algolia/user-profiles/new-account.png)

## Aggiungi dati

Dopo aver creato l&#39;account [!DNL Algolia User Profiles], viene visualizzato il passaggio **[!UICONTROL Aggiungi dati]**, che fornisce un&#39;interfaccia per esplorare i profili utente [!DNL Algolia] che desideri portare in Experience Platform.

* La parte sinistra dell&#39;interfaccia consente di immettere i campi facoltativi **[!UICONTROL Indici]** e **[!UICONTROL Affinità]**.
* La parte destra dell’interfaccia consente di visualizzare in anteprima fino a 100 righe di profili utente.

Dopo aver selezionato e visualizzato in anteprima i dati per l&#39;acquisizione, seleziona **[!UICONTROL Avanti]**.

![Passaggio di dati selezionato del flusso di lavoro.](../../../../images/tutorials/create/algolia/user-profiles/select-data.png)

## Fornisci i dettagli del flusso di dati

Se utilizzi un set di dati esistente, seleziona un set di dati associato a uno schema che utilizza il gruppo di campi [!DNL Algolia Profile].

![Passaggio del set di dati esistente del flusso di lavoro origini.](../../../../images/tutorials/create/algolia/user-profiles/dataflow-detail-existing-dataset.png)

Se stai creando un nuovo set di dati, seleziona uno schema che utilizza il gruppo di campi [!DNL Algolia Profile] richiesto nel passaggio di mappatura.

![Il nuovo passaggio del set di dati del flusso di lavoro origini.](../../../../images/tutorials/create/algolia/user-profiles/dataflow-detail-new-dataset.png)

## Mappare i campi dati su uno schema XDM

Utilizza l’interfaccia di mappatura per mappare i dati di origine sui campi dello schema appropriati prima di acquisire i dati in Experience Platform.  Per ulteriori informazioni, leggere la [guida alla mappatura nell&#39;interfaccia utente](../../../../../data-prep/ui/mapping.md).

![Passaggio di mappatura del flusso di lavoro di origine.](../../../../images/tutorials/create/algolia/user-profiles/mapping.png)

## Pianificazione esecuzioni dell’acquisizione

Quindi, utilizza l’interfaccia di pianificazione per definire la pianificazione dell’acquisizione del flusso di dati.

<!-- The Scheduling step allows for configuration of the data/time to execute the [!DNL Algolia Uer Profiles] Source connector. There is configuration to backfill the data from [!DNL Algolia] which will pull all the profiles from the source system.  If the source is scheduled, then it will retrieve modified profiles from the [!DNL Algolia] based on the configured time interval. -->

![Passaggio di pianificazione del flusso di lavoro di origine.](../../../../images/tutorials/create/algolia/user-profiles/scheduling.png)

| Configurazione pianificazione | Descrizione |
| --- | --- |
| Frequenza | Configura la frequenza per indicare la frequenza con cui deve essere eseguito il flusso di dati. Puoi impostare la frequenza su: <ul><li>**Una volta**: imposta la frequenza su `once` per creare un&#39;acquisizione unica. Le configurazioni di intervallo e backfill non sono disponibili quando crei un flusso di dati di acquisizione una tantum. Per impostazione predefinita, la frequenza di pianificazione è impostata su una volta.</li><li>**Minuti**: imposta la frequenza su `minute` per pianificare il flusso di dati in modo da acquisire i dati al minuto.</li><li>**Ora**: imposta la frequenza su `hour` per pianificare il flusso di dati per acquisire i dati su base oraria.</li><li>**Giorno**: imposta la frequenza su `day` per pianificare il flusso di dati in modo da acquisire i dati su base giornaliera.</li><li>**Settimana**: imposta la frequenza su `week` per pianificare il flusso di dati in modo da acquisire i dati su base settimanale.</li></ul> |
| Intervallo | Dopo aver selezionato una frequenza, puoi configurare l’impostazione dell’intervallo per stabilire l’intervallo di tempo tra ogni acquisizione. Ad esempio, se imposti la frequenza su giorno e configuri l’intervallo su 15, il flusso di dati verrà eseguito ogni 15 giorni. Impossibile impostare l&#39;intervallo su zero. Il valore dell&#39;intervallo minimo accettato per ciascuna frequenza è il seguente:<ul><li>**Una volta**: n/d</li><li>**Minuto**: 15</li><li>**Ora**: 1</li><li>**Giorno**: 1</li><li>**Settimana**: 1</li></ul> |
| Ora di inizio | La marca temporale per l’esecuzione prevista, presentata in fuso orario UTC. |
| Retrocompilazione | La retrocompilazione determina quali dati vengono inizialmente acquisiti. Se la retrocompilazione è abilitata, tutti i file correnti nel percorso specificato verranno acquisiti durante la prima acquisizione pianificata. Se la retrocompilazione è disattivata, verranno acquisiti solo i file caricati tra la prima esecuzione dell’acquisizione e l’ora di inizio. I file caricati prima dell’ora di inizio non verranno acquisiti. |

## Verifica il flusso di dati

Utilizza la pagina di revisione per un riepilogo del flusso di dati prima dell’acquisizione. I dettagli sono raggruppati nelle seguenti categorie:

* **Connessione** - Mostra il tipo di origine, il percorso pertinente del file di origine scelto e il numero di colonne all&#39;interno di tale file di origine.
* **Assegna set di dati e mappa campi**: mostra in quale set di dati vengono acquisiti i dati di origine, incluso lo schema a cui il set di dati è conforme.
* **Pianificazione** - Mostra il periodo attivo, la frequenza e l&#39;intervallo della pianificazione di acquisizione.

Dopo aver rivisto il flusso di dati, seleziona **[!UICONTROL Fine]** e attendi che venga creato un po&#39; di tempo.

![Passaggio di revisione del flusso di lavoro origini.](../../../../images/tutorials/create/algolia/user-profiles/review.png)

## Passaggi successivi

Seguendo questa esercitazione, è stato creato un flusso di dati per portare dati intento dall&#39;origine [!DNL Algolia] ad Experience Platform. Per ulteriori risorse, consulta la documentazione descritta di seguito.

### Monitorare il flusso di dati

Una volta creato il flusso di dati, puoi monitorare i dati che vengono acquisiti tramite di esso per visualizzare informazioni su tassi di acquisizione, successo ed errori. Per ulteriori informazioni su come monitorare il flusso di dati, visita l&#39;esercitazione su [account di monitoraggio e flussi di dati nell&#39;interfaccia utente](../../../../../dataflows/ui/monitor-sources.md).

### Aggiornare il flusso di dati

Per aggiornare le configurazioni per la pianificazione, la mappatura e le informazioni generali dei flussi di dati, visita il tutorial su [aggiornamento dei flussi di dati di origine nell&#39;interfaccia utente](../../update-dataflows.md).

### Eliminare il flusso di dati

È possibile eliminare i flussi di dati non più necessari o creati in modo errato utilizzando la funzione **[!UICONTROL Elimina]** disponibile nell&#39;area di lavoro **[!UICONTROL Flussi di dati]**. Per ulteriori informazioni su come eliminare i flussi di dati, consulta l&#39;esercitazione su [eliminazione dei flussi di dati nell&#39;interfaccia utente](../../delete.md).
