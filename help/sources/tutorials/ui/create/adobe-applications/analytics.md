---
title: Connettere Adobe Analytics Ad Experience Platform
description: Scopri come importare i dati della suite di rapporti di Adobe Analytics in Experience Platform
exl-id: 5ddbaf63-feaa-44f5-b2f2-2d5ae507f423
source-git-commit: 086777a09eec17c94a7e0a5d2db58e4a1f6b523f
workflow-type: tm+mt
source-wordcount: '2731'
ht-degree: 3%

---

# Connettere Adobe Analytics ad Experience Platform

Leggi questa guida per scoprire come utilizzare l’origine di Adobe Analytics per acquisire in Adobe Experience Platform i dati della suite di rapporti di Analytics.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Experience Data Model (XDM) System](../../../../../xdm/home.md): framework standardizzato tramite il quale Experience Platform organizza i dati sull&#39;esperienza del cliente.
* [Profilo cliente in tempo reale](../../../../../profile/home.md): fornisce un profilo consumatore unificato in tempo reale basato su dati aggregati provenienti da più origini.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Experience Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

### Terminologia chiave

È importante comprendere i seguenti termini chiave utilizzati nel presente documento:

* **Attributo standard**: gli attributi standard sono qualsiasi attributo predefinito da Adobe. Contengono lo stesso significato per tutti i clienti e sono disponibili nei gruppi di campi Dati di origine e Schema di Analytics.
* **Attributo personalizzato**: gli attributi personalizzati sono qualsiasi attributo nella gerarchia delle variabili personalizzate in Analytics. Gli attributi personalizzati vengono utilizzati all’interno di un’implementazione di Adobe Analytics per acquisire informazioni specifiche in una suite di rapporti e possono differire nel loro utilizzo da una suite di rapporti all’altra. Gli attributi personalizzati includono eVar, prop ed elenchi. Per ulteriori informazioni sulle eVar, consulta la [documentazione di Analytics sulle variabili di conversione](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=it).
* **Qualsiasi attributo nei gruppi di campi personalizzati**: gli attributi che provengono dai gruppi di campi creati dai clienti sono tutti definiti dall&#39;utente e non sono considerati né attributi standard né personalizzati.

## Navigare nel catalogo delle origini

>[!NOTE]
>
>Quando crei un flusso di dati di origine Analytics in una sandbox di produzione, vengono creati due flussi di dati:
>
>* Un flusso di dati che esegue una retrocompilazione di 13 mesi dei dati storici della suite di rapporti nel data lake. Questo flusso di dati termina quando la retrocompilazione è completa.
>* Flusso di dati che invia dati live al data lake e a [!DNL Real-Time Customer Profile]. Questo flusso di dati viene eseguito in modo continuo.

Nell&#39;interfaccia utente di Experience Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Nella categoria *[!UICONTROL Applicazioni Adobe]*, seleziona la scheda Adobe Analytics, quindi seleziona **[!UICONTROL Aggiungi dati]**.

![Catalogo delle origini con la scheda di origine di Adobe Analytics selezionata.](../../../../images/tutorials/create/analytics/catalog.png)

## Selezionare i dati

>[!IMPORTANT]
>
>* Le suite di rapporti elencate sullo schermo possono provenire da varie aree geografiche. L’utente è responsabile della comprensione delle limitazioni e degli obblighi relativi ai suoi dati e di come utilizza tali dati in Adobe Experience Platform in aree geografiche diverse. Assicurati che ciò sia consentito dalla tua azienda.
>* I dati provenienti da più suite di rapporti possono essere abilitati per Real-Time Customer Profile solo se non sono presenti conflitti di dati, ad esempio due proprietà personalizzate (eVar, elenchi e proprietà) con un significato diverso.

Una suite di rapporti è un contenitore di dati che costituisce la base del reporting di Analytics. Un’organizzazione può avere molte suite di rapporti, ciascuna contenente set di dati diversi.

Puoi acquisire suite di rapporti da qualsiasi area geografica (Stati Uniti, Regno Unito o Singapore) purché siano mappate sulla stessa organizzazione dell’istanza sandbox di Experience Platform in cui viene creata la connessione di origine. Una suite di rapporti può essere acquisita utilizzando un solo flusso di dati attivo. Se una suite di rapporti è grigia e non può essere selezionata, significa che è già stata acquisita nella sandbox in uso o in una sandbox diversa.

È possibile effettuare più connessioni in-bound per portare più suite di rapporti nella stessa sandbox. Se le suite di rapporti hanno schemi diversi per le variabili (ad esempio eVar o eventi), è necessario mapparle su campi specifici nei gruppi di campi personalizzati ed evitare conflitti di dati utilizzando [Preparazione dati](../../../../../data-prep/ui/mapping.md). Le suite di rapporti possono essere aggiunte solo a una singola sandbox.

Seleziona la **[!UICONTROL suite di rapporti]**, quindi utilizza l&#39;interfaccia *[!UICONTROL Dati aggiunta origine di Analytics]* per spostarti nell&#39;elenco e identificare la suite di rapporti di Analytics che desideri acquisire in Experience Platform. Seleziona **[!UICONTROL Avanti]** per procedere.

![È selezionata una suite di rapporti di analisi per l&#39;acquisizione ed è evidenziato il pulsante &quot;Successivo&quot;](../../../../images/tutorials/create/analytics/add-data.png)

&lt;!- Le suite di rapporti di Analytics possono essere configurate per una sandbox alla volta. Per importare la stessa suite di rapporti in una sandbox diversa, è necessario eliminare il flusso del set di dati e crearne di nuovo un’istanza tramite la configurazione per una sandbox diversa.—>

## Mappatura {#mapping}

>[!IMPORTANT]
>
>Le trasformazioni della preparazione dati possono aggiungere latenza al flusso di dati complessivo. La latenza aggiuntiva aggiunta varia in base alla complessità della logica di trasformazione.

Prima di poter mappare i dati di Analytics sullo schema XDM di destinazione, è necessario determinare se si utilizza uno schema predefinito o personalizzato.

>[!BEGINTABS]

>[!TAB Schema predefinito]

Uno schema predefinito crea un nuovo schema per tuo conto. Questo schema appena creato contiene il gruppo di campi [!DNL Adobe Analytics ExperienceEvent Template]. Per utilizzare uno schema predefinito, selezionare **[!UICONTROL Schema predefinito]**.

![Passaggio di selezione dello schema del flusso di lavoro di origine di Analytics, con &quot;Schema predefinito&quot; selezionato.](../../../../images/tutorials/create/analytics/default-schema.png)

>[!TAB Schema personalizzato]

Con uno schema personalizzato, puoi scegliere qualsiasi schema disponibile per i dati di Analytics, purché tale schema abbia il gruppo di campi [!DNL Adobe Analytics ExperienceEvent Template]. Per utilizzare uno schema personalizzato, selezionare **[!UICONTROL Schema personalizzato]**.

![Passaggio di selezione dello schema del flusso di lavoro di origine di Analytics, con &quot;Schema personalizzato&quot; selezionato.](../../../../images/tutorials/create/analytics/custom-schema.png)

>[!ENDTABS]

Utilizza l&#39;interfaccia *[!UICONTROL Mapping]* per mappare i campi sorgente ai campi schema di destinazione appropriati. Puoi mappare le variabili personalizzate ai nuovi gruppi di campi dello schema e applicare i calcoli come supportato dalla preparazione dati. Seleziona uno schema di destinazione per avviare il processo di mappatura.

>[!TIP]
>
>Nel menu di selezione dello schema vengono visualizzati solo gli schemi con il gruppo di campi [!DNL Adobe Analytics ExperienceEvent Template]. Gli altri schemi vengono omessi. Se non sono disponibili schemi appropriati per i dati della suite di rapporti, devi creare un nuovo schema. Per i passaggi dettagliati sulla creazione di schemi, consulta la guida su [creazione e modifica di schemi nell&#39;interfaccia utente](../../../../../xdm/ui/resources/schemas.md).

![Pannello di selezione dello schema di destinazione dell&#39;interfaccia di mappatura.](../../../../images/tutorials/create/analytics/select-schema.png)

Puoi fare riferimento al pannello [!UICONTROL Mapping campi standard] per le metriche delle [!UICONTROL Mappature standard applicate]. [!UICONTROL Mappature standard con conflitti di nome descrittore] e [!DNL Custom mappings].

| Mappa campi standard | Descrizione |
| --- | --- |
| [!UICONTROL Mappature standard applicate] | Il pannello [!UICONTROL Mappature standard applicate] visualizza il numero totale di attributi mappati. Le mappature standard si riferiscono alle mappature tra tutti gli attributi nei dati Analytics di origine e gli attributi corrispondenti nel gruppo di campi Analytics. Questi sono premappati e non possono essere modificati. |
| [!UICONTROL Mappature standard con conflitti di nome descrittore] | Il pannello [!UICONTROL Mappature standard con conflitti di nome descrittore] fa riferimento al numero di attributi mappati che contengono conflitti di nome. Questi conflitti vengono visualizzati quando si riutilizza uno schema che dispone già di un set popolato di descrittori di campo di una suite di rapporti diversa. Puoi procedere con il flusso di dati di Analytics anche con conflitti di nomi. |
| [!UICONTROL Mappature personalizzate] | Il pannello [!UICONTROL Mappature personalizzate] visualizza il numero di attributi personalizzati mappati, inclusi eVar, prop ed elenchi. Le mappature personalizzate si riferiscono alla mappatura tra gli attributi personalizzati nei dati Analytics di origine e gli attributi nei gruppi di campi personalizzati inclusi nello schema selezionato. |

### Mappature standard {#standard-mappings}

Experience Platform rileva automaticamente la mappatura per eventuali conflitti di nomi. Se non ci sono conflitti con le tue mappature, seleziona **[!UICONTROL Successivo]** per continuare.

![L&#39;intestazione delle mappature standard non visualizza alcun conflitto di nomi](../../../../images/tutorials/create/analytics/standard.png)

>[!TIP]
>
>In caso di conflitti di nomi tra la suite di rapporti di origine e lo schema selezionato, puoi comunque continuare con il flusso di dati di Analytics, riconoscendo che i descrittori dei campi non verranno modificati. In alternativa, puoi scegliere di creare un nuovo schema con un set vuoto di descrittori.

## Mappature personalizzate {#custom-mappings}

È possibile utilizzare le funzioni di preparazione dati per aggiungere nuove mappature personalizzate o campi calcolati per gli attributi personalizzati. Per aggiungere mappature personalizzate, selezionare **[!UICONTROL Personalizzato]**.

![Scheda di mappatura personalizzata nel flusso di lavoro di origine di Analytics.](../../../../images/tutorials/create/analytics/custom.png)

* **[!UICONTROL Filtra campi]**: utilizza l&#39;input di testo [!UICONTROL Filtra campi] per filtrare specifici campi di mappatura nei mapping.
* **[!UICONTROL Aggiungi nuova mappatura]**: per aggiungere una nuova mappatura del campo di origine e del campo di destinazione, selezionare **[!UICONTROL Aggiungi nuova mappatura]**.
* **[!UICONTROL Aggiungi campo calcolato]**: se necessario, seleziona **[!UICONTROL Aggiungi campo calcolato]** per creare un nuovo campo calcolato per i mapping.
* **[!UICONTROL Mappatura importazione]**: puoi ridurre il tempo di configurazione manuale del processo di acquisizione dei dati e limitare gli errori utilizzando la funzionalità di mappatura importazione della preparazione dati. Selezionare **[!UICONTROL Importa mapping]** per importare i mapping da un flusso esistente o da un file esportato. Per ulteriori informazioni, leggere [la guida all&#39;importazione e all&#39;esportazione dei mapping](../../../../../data-prep/ui/mapping.md#import-mapping).
* **[!UICONTROL Scarica modello]**: puoi anche scaricare una copia CSV delle mappature e configurare le mappature nel dispositivo locale. Seleziona **[!UICONTROL Scarica modello]** per scaricare una copia CSV delle tue mappature. È necessario assicurarsi di utilizzare solo i campi forniti nel file di origine e nello schema di destinazione.

Per ulteriori informazioni sulla preparazione dati, consulta la seguente documentazione.

* [Panoramica sulla preparazione dati](../../../../../data-prep/home.md)
* [Funzioni di mappatura della preparazione dati](../../../../../data-prep/functions.md)
* [Aggiungere campi calcolati](../../../../../data-prep/ui/mapping.md#calculated-fields)

<!-- 
To use Data Prep functions and add new mapping or calculated fields for custom attributes, select **[!UICONTROL View custom mappings]**.

![view-custom-mapping](../../../../images/tutorials/create/analytics/view-custom-mapping.png)

Next, select **[!UICONTROL Add new mapping]**.

Depending on your needs, you can select either **[!UICONTROL Add new mapping]** or **[!UICONTROL Add calculated field]** from the options that appear. 

![add-new-mapping](../../../../images/tutorials/create/analytics/add-new-mapping.png)

An empty mapping set appears. Select the mapping icon to add a source field.

![select-source-field](../../../../images/tutorials/create/analytics/select-source-field.png)

You can use the interface to navigate through the source schema structure and identify the new source field that you want to use. Once you have selected the source field that you want to map, select **[!UICONTROL Select]**.

![select-mapping](../../../../images/tutorials/create/analytics/select-mapping.png)

Next, select the mapping icon under [!UICONTROL Target Field] to map your selected source field to its appropriate target field.

![select-target-field](../../../../images/tutorials/create/analytics/select-target-field.png)

Similar to the source schema, you can use the interface to navigate through the target schema structure and select the target field you want to map to. Once you have selected the appropriate target field, select **[!UICONTROL Select]**.

![select-target-mapping](../../../../images/tutorials/create/analytics/select-target-mapping.png)

With your custom mapping set completed, select **[!UICONTROL Next]** to proceed.

![complete-custom-mapping](../../../../images/tutorials/create/analytics/complete-custom-mapping.png) -->

## Filtraggio in base a profilo cliente in tempo reale {#filtering-for-profile}

>[!CONTEXTUALHELP]
>id="platform_data_prep_analytics_filtering"
>title="Creare regole di filtro"
>abstract="Quando invii dati al profilo cliente in tempo reale, puoi definire regole di filtro a livello di riga e colonna. Utilizza il filtro a livello di riga per applicare condizioni e stabilire quali dati **includere nell’acquisizione per il profilo**. Utilizza il filtro a livello di colonna per selezionare le colonne di dati da **escludere dall’acquisizione per il profilo**. Le regole di filtro non si applicano ai dati inviati al Data Lake."

Dopo aver completato le mappature per i dati della suite di rapporti di Analytics, puoi applicare regole e condizioni di filtro per includere o escludere selettivamente i dati dall’acquisizione nel Profilo cliente in tempo reale. Il supporto per il filtro è disponibile solo per i dati di Analytics e i dati vengono filtrati solo prima dell&#39;immissione di [!DNL Profile.] Tutti i dati vengono acquisiti nel data lake.

>[!BEGINSHADEBOX]

**Ulteriori informazioni sulla preparazione dei dati e sul filtraggio dei dati di Analytics per Real-Time Customer Profile**

* Puoi utilizzare la funzionalità di filtro per i dati che vanno nel profilo, ma non per i dati che vanno nel data lake.
* Puoi utilizzare il filtro per i dati live, ma non puoi filtrare i dati di retrocompilazione.
   * L’origine di Analytics non esegue il backfill dei dati nel profilo.
* Se utilizzi le configurazioni di Preparazione dati durante la configurazione iniziale di un flusso Analytics, queste modifiche vengono applicate anche alla retrocompilazione automatica di 13 mesi.
   * Tuttavia, questo non avviene per il filtro, perché il filtro è riservato solo ai dati live.
* La preparazione dati viene applicata ai percorsi di acquisizione in streaming e in batch. Se modifichi una configurazione di Preparazione dati esistente, tali modifiche vengono quindi applicate ai nuovi dati in arrivo attraverso i percorsi di acquisizione in streaming e in batch.
   * Tuttavia, eventuali configurazioni della preparazione dati non si applicano ai dati che sono già stati acquisiti in Experience Platform, indipendentemente dal fatto che si tratti di dati in streaming o batch.
* Gli attributi standard di Analytics vengono sempre mappati automaticamente. Pertanto, non è possibile applicare trasformazioni agli attributi standard.
   * Tuttavia, puoi filtrare gli attributi standard purché non siano richiesti in Identity Service o Profile.
* Non è possibile utilizzare il filtro a livello di colonna per filtrare i campi obbligatori e i campi di identità.
* Anche se è possibile filtrare le identità secondarie, in particolare AAID e AACustomID, non è possibile filtrare ECID.
* Quando si verifica un errore di trasformazione, la colonna corrispondente restituisce NULL.

>[!ENDSHADEBOX]

### Filtro a livello di riga

>[!IMPORTANT]
>
>Utilizza il filtro a livello di riga per applicare condizioni e stabilire quali dati **includere nell’acquisizione per il profilo**. Utilizza il filtro a livello di colonna per selezionare le colonne di dati da **escludere per l&#39;acquisizione del profilo**.

Puoi filtrare i dati per l’acquisizione del profilo a livello di riga e di colonna. Utilizza il filtro a livello di riga per definire criteri quali stringa contiene, è uguale a, inizia o termina con. È inoltre possibile utilizzare il filtro a livello di riga per unire le condizioni utilizzando `AND` e `OR` e negare le condizioni utilizzando `NOT`.

Per filtrare i dati di Analytics a livello di riga, seleziona **[!UICONTROL Filtro riga]** e utilizza la barra a sinistra per spostarti nella gerarchia dello schema e identificare l&#39;attributo dello schema che desideri selezionare.

![Interfaccia filtro righe per i dati di Analytics.](../../../../images/tutorials/create/analytics/row-filter.png)

Dopo aver identificato l’attributo da configurare, selezionalo e trascinalo dalla barra a sinistra al pannello di filtro.

![Attributo &quot;Manufacturer&quot; selezionato per il filtro.](../../../../images/tutorials/create/analytics/filtering-panel.png)

Per configurare condizioni diverse, selezionare **[!UICONTROL è uguale a]**, quindi selezionare una condizione dalla finestra a discesa visualizzata.

L’elenco delle condizioni configurabili include:

* [!UICONTROL è uguale a]
* [!UICONTROL è diverso da]
* [!UICONTROL inizia con]
* [!UICONTROL termina con]
* [!UICONTROL non termina con]
* [!UICONTROL contiene]
* [!UICONTROL non contiene]
* [!UICONTROL esiste]
* [!UICONTROL non esiste]

![Elenco a discesa delle condizioni con un elenco di operatori delle condizioni.](../../../../images/tutorials/create/analytics/conditions.png)

Immettere quindi i valori che si desidera includere in base all&#39;attributo selezionato. Nell&#39;esempio seguente, [!DNL Apple] e [!DNL Google] sono selezionati per l&#39;acquisizione come parte dell&#39;attributo **[!UICONTROL Manufacturer]**.

![Pannello di filtro contenente gli attributi e i valori selezionati.](../../../../images/tutorials/create/analytics/include.png)

Per specificare ulteriormente le condizioni di filtro, aggiungi un altro attributo dallo schema, quindi aggiungi i valori basati su tale attributo. Nell&#39;esempio seguente viene aggiunto l&#39;attributo **[!UICONTROL Model]** e i modelli come [!DNL iPhone 16] e [!DNL Google Pixel 9] vengono filtrati per l&#39;acquisizione.

![Attributi e valori aggiuntivi inclusi nel contenitore.](../../../../images/tutorials/create/analytics/include-model.png)

Per aggiungere un nuovo contenitore, selezionare i puntini di sospensione (`...`) in alto a destra nell&#39;interfaccia di filtro, quindi selezionare **[!UICONTROL Aggiungi contenitore]**.

![Menu a discesa &quot;Aggiungi contenitore&quot; selezionato.](../../../../images/tutorials/create/analytics/add-container.png)

Dopo aver aggiunto un nuovo contenitore, seleziona **[!UICONTROL Includi]**, quindi seleziona **[!UICONTROL Escludi]** dal menu a discesa. Aggiungere gli attributi e i valori che si desidera escludere e quindi al termine selezionare **[!UICONTROL Avanti]**.

![Attributi e valori filtrati per l&#39;esclusione.](../../../../images/tutorials/create/analytics/exclude.png)

### Filtraggio a livello di colonna

Seleziona **[!UICONTROL Filtro colonna]** dall&#39;intestazione per applicare il filtro a livello di colonna.

La pagina si aggiorna in una struttura di schema interattiva, che mostra gli attributi dello schema a livello di colonna. Da qui, puoi selezionare le colonne di dati da escludere dall’acquisizione del profilo. In alternativa, è possibile espandere una colonna e selezionare attributi specifici per l&#39;esclusione.

Per impostazione predefinita, tutte le analisi passano a Profilo e questo processo consente di escludere i rami di dati XDM dall’acquisizione del profilo.

![Interfaccia filtro colonne con struttura dello schema.](../../../../images/tutorials/create/analytics/column-filter.png)

### Filtra identità secondarie

Utilizza un filtro a colonne per escludere le identità secondarie dall’acquisizione del profilo. Per filtrare le identità secondarie, selezionare **[!UICONTROL Filtro colonna]**, quindi selezionare **[!UICONTROL _identità]**.

Il filtro si applica solo quando un’identità è contrassegnata come secondaria. Se sono selezionate identità ma arriva un evento con una delle identità contrassegnate come primarie, queste non vengono filtrate.

![Identità secondarie nell&#39;albero dello schema per il filtro delle colonne.](../../../../images/tutorials/create/analytics/secondary-identities.png)

### Fornisci i dettagli del flusso di dati

Viene visualizzato il passaggio **[!UICONTROL Dettagli flusso di dati]**, in cui è necessario fornire un nome e una descrizione facoltativa per il flusso di dati. Al termine, seleziona **[!UICONTROL Avanti]**.

![Interfaccia dettagli flusso di dati. del flusso di lavoro di acquisizione.](../../../../images/tutorials/create/analytics/dataflow-detail.png)

### Revisione

Viene visualizzato il passaggio [!UICONTROL Rivedi], che consente di rivedere il nuovo flusso di dati di Analytics prima che venga creato. I dettagli della connessione sono raggruppati per categorie, tra cui:

* [!UICONTROL Connessione]: visualizza la piattaforma di origine della connessione.
* [!UICONTROL Tipo di dati]: visualizza la suite di rapporti selezionata e il relativo ID suite di rapporti.

![Interfaccia di revisione del flusso di lavoro di acquisizione.](../../../../images/tutorials/create/analytics/review.png)

## Monitorare il flusso di dati {#monitor-your-dataflow}

Una volta completato il flusso di dati, puoi utilizzare l&#39;interfaccia *[!UICONTROL Flussi di dati]* per monitorare lo stato del flusso di dati di Analytics.

Utilizza l&#39;interfaccia dell&#39;[!UICONTROL attività set di dati] per informazioni sull&#39;avanzamento dei dati inviati da Analytics ad Experience Platform. L’interfaccia visualizza metriche quali il totale dei record del mese precedente, il totale dei record acquisiti negli ultimi sette giorni e le dimensioni dei dati nel mese precedente.

L’origine crea un’istanza di due flussi di set di dati. Un flusso rappresenta i dati di backfill e l’altro è per i dati live. I dati di backfill non sono configurati per l’acquisizione in Real-Time Customer Profile, ma vengono inviati al data lake per casi d’uso analitici e di data science.

Per ulteriori informazioni sulla retrocompilazione, sui dati live e sulle rispettive latenze, consulta la [Panoramica sull&#39;origine di Analytics](../../../../connectors/adobe-applications/analytics.md).

![Pagina attività set di dati per un set di dati di destinazione specifico per i dati di Adobe Analytics.](../../../../images/tutorials/create/analytics/dataset-activity.png)

>[!NOTE]
>
>La pagina dell’attività del set di dati non visualizza informazioni sui batch, poiché il connettore di origine di Analytics è interamente gestito da Adobe. Puoi monitorare il flusso dei dati osservando le metriche relative ai record acquisiti.

## Eliminare il flusso di dati {#delete-dataflow}

Per eliminare il flusso di dati di Analytics, seleziona **[!UICONTROL Flussi di dati]** dall&#39;intestazione superiore dell&#39;area di lavoro origini. Utilizzare la pagina Flussi dati per individuare il flusso di dati di Analytics che si desidera eliminare, quindi selezionare i puntini di sospensione (`...`) accanto ad esso. Quindi, utilizzare il menu a discesa e selezionare **[!UICONTROL Elimina]**.

* Se elimini il flusso di dati live Analytics, verrà eliminato anche il relativo set di dati sottostante.
* L’eliminazione del flusso di dati di backfill di Analytics non elimina il set di dati sottostante, ma interrompe il processo di backfill per la suite di rapporti corrispondente. Se elimini il flusso di dati di retrocompilazione, i dati acquisiti possono comunque essere visualizzati attraverso il set di dati.

## Passaggi successivi e risorse aggiuntive

Una volta creata la connessione, il flusso di dati viene creato automaticamente per contenere i dati in arrivo e popolare un set di dati con lo schema selezionato. Inoltre, avviene il recupero dei dati e acquisisce fino a 13 mesi di dati storici. Al termine dell&#39;acquisizione iniziale, i dati di Analytics e verranno utilizzati dai servizi Experience Platform a valle come [!DNL Real-Time Customer Profile] e Segmentation Service. Per ulteriori informazioni, consulta i seguenti documenti:

* [Panoramica di [!DNL Real-Time Customer Profile]](../../../../../profile/home.md)
* [Panoramica di [!DNL Segmentation Service]](../../../../../segmentation/home.md)
* [Panoramica di [!DNL Data Science Workspace]](../../../../../data-science-workspace/home.md)
* [Panoramica di [!DNL Query Service]](../../../../../query-service/home.md)

Il seguente video ha lo scopo di chiarire come acquisire dati utilizzando il connettore Source di Adobe Analytics:

>[!WARNING]
>
> L&#39;interfaccia utente [!DNL Experience Platform] mostrata nel video seguente non è aggiornata. Per le schermate e le funzionalità più recenti dell’interfaccia utente, consulta la documentazione precedente.

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)

