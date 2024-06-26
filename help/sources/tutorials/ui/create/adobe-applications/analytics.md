---
title: Creare una connessione sorgente Adobe Analytics nell’interfaccia utente
description: Scopri come creare una connessione sorgente Adobe Analytics nell’interfaccia utente per inserire i dati dei consumatori in Adobe Experience Platform.
exl-id: 5ddbaf63-feaa-44f5-b2f2-2d5ae507f423
source-git-commit: f177a8058f6533151978bfd7b8bba4845792f5ed
workflow-type: tm+mt
source-wordcount: '2755'
ht-degree: 4%

---

# Creare una connessione sorgente Adobe Analytics nell’interfaccia utente

Questo tutorial descrive i passaggi necessari per creare una connessione di origine Adobe Analytics nell’interfaccia utente per inserire i dati della suite di rapporti Adobe Analytics in Adobe Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Sistema Experience Data Model (XDM)](../../../../../xdm/home.md): framework standardizzato tramite il quale Experienci Platform organizza i dati sull’esperienza del cliente.
* [Profilo cliente in tempo reale](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Sandbox](../../../../../sandboxes/home.md): Experienci Platform fornisce sandbox virtuali che permettono di suddividere una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

### Terminologia chiave

È importante comprendere i seguenti termini chiave utilizzati nel presente documento:

* **Attributo standard**: gli attributi standard sono qualsiasi attributo predefinito da Adobe. Contengono lo stesso significato per tutti i clienti e sono disponibili nella sezione [!DNL Analytics] dati di origine e [!DNL Analytics] gruppi di campi dello schema.
* **Attributo personalizzato**: gli attributi personalizzati sono qualsiasi attributo nella gerarchia di variabili personalizzate in [!DNL Analytics]. Gli attributi personalizzati vengono utilizzati all’interno di un’implementazione di Adobe Analytics per acquisire informazioni specifiche in una suite di rapporti e possono differire nel loro utilizzo da una suite di rapporti all’altra. Gli attributi personalizzati includono eVar, prop ed elenchi. Vedi quanto segue [[!DNL Analytics] documentazione sulle variabili di conversione](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html) per ulteriori informazioni sulle eVar.
* **Qualsiasi attributo nei gruppi di campi personalizzati**: gli attributi che provengono da gruppi di campi creati dai clienti sono tutti definiti dall’utente e non sono considerati né attributi standard né personalizzati.
* **Nomi descrittivi**: i nomi descrittivi sono etichette fornite dall’uomo per le variabili personalizzate in un [!DNL Analytics] implementazione. Vedi quanto segue [[!DNL Analytics] documentazione sulle variabili di conversione](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html) per ulteriori informazioni sui nomi descrittivi.

## Creare una connessione sorgente con Adobe Analytics

>[!NOTE]
>
>Quando crei un flusso di dati di origine Analytics in una sandbox di produzione, vengono creati due flussi di dati:
>
>* Un flusso di dati che esegue una retrocompilazione di 13 mesi dei dati storici della suite di rapporti nel data lake. Questo flusso di dati termina quando la retrocompilazione è completa.
>* Un flusso di dati che invia dati live al data lake e a [!DNL Real-Time Customer Profile]. Questo flusso di dati viene eseguito in modo continuo.

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Il [!UICONTROL Catalogo] Nella schermata vengono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. È inoltre possibile utilizzare la barra di ricerca per limitare le origini visualizzate.

Sotto **[!UICONTROL applicazioni Adobe]** categoria, seleziona **[!UICONTROL Adobe Analytics]** e quindi seleziona **[!UICONTROL Aggiungi dati]**.

![catalogo](../../../../images/tutorials/create/analytics/catalog.png)

### Selezionare i dati

>[!IMPORTANT]
>
>Le suite di rapporti elencate sullo schermo possono provenire da varie aree geografiche. L’utente è responsabile della comprensione delle limitazioni e degli obblighi relativi ai suoi dati e di come utilizza tali dati in Adobe Experience Platform in aree geografiche diverse. Assicurati che ciò sia consentito dalla tua azienda.

Il **[!UICONTROL Dati aggiunta origine di Analytics]** Il passaggio ti fornisce un elenco di [!DNL Analytics] dati della suite di rapporti con cui creare una connessione di origine.

Una suite di rapporti è un contenitore di dati che costituisce la base di [!DNL Analytics] reportistica. Un’organizzazione può avere molte suite di rapporti, ciascuna contenente set di dati diversi.

Puoi acquisire suite di rapporti da qualsiasi area geografica (Stati Uniti, Regno Unito o Singapore) purché siano mappate sulla stessa organizzazione dell’istanza sandbox Experienci Platform in cui viene creata la connessione di origine. Una suite di rapporti può essere acquisita utilizzando un solo flusso di dati attivo. Una suite di rapporti non selezionabile è già stata acquisita nella sandbox in uso o in un’altra sandbox.

È possibile effettuare più connessioni in-bound per portare più suite di rapporti nella stessa sandbox. Se le suite di rapporti hanno schemi diversi per le variabili (ad esempio eVar o eventi), questi devono essere mappati su campi specifici nei gruppi di campi personalizzati ed evitare conflitti di dati utilizzando [Preparazione dati](../../../../../data-prep/ui/mapping.md). Le suite di rapporti possono essere aggiunte solo a una singola sandbox.

![](../../../../images/tutorials/create/analytics/report-suite.png)

>[!NOTE]
>
>I dati provenienti da più suite di rapporti possono essere abilitati per Real-Time Customer Profile solo se non sono presenti conflitti di dati, ad esempio due proprietà personalizzate (eVar, elenchi e proprietà) con un significato diverso.

Per creare un [!DNL Analytics] connessione di origine, seleziona una suite di rapporti, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![](../../../../images/tutorials/create/analytics/add-data.png)

&lt;!- Le suite di rapporti di Analytics possono essere configurate per una sandbox alla volta. Per importare la stessa suite di rapporti in una sandbox diversa, è necessario eliminare il flusso del set di dati e crearne di nuovo un’istanza tramite la configurazione per una sandbox diversa.—>

### Mappatura

>[!IMPORTANT]
>
>Le trasformazioni della preparazione dati possono aggiungere latenza al flusso di dati complessivo. La latenza aggiuntiva aggiunta varia in base alla complessità della logica di trasformazione.

Prima di mappare il [!DNL Analytics] per eseguire il targeting dello schema XDM, devi prima selezionare se utilizzi uno schema predefinito o personalizzato.

Uno schema predefinito crea un nuovo schema per tuo conto, contenente [!DNL Adobe Analytics ExperienceEvent Template] gruppo di campi. Per utilizzare uno schema predefinito, seleziona **[!UICONTROL Schema predefinito]**.

![default-schema](../../../../images/tutorials/create/analytics/default-schema.png)

Con uno schema personalizzato, puoi scegliere qualsiasi schema disponibile per il [!DNL Analytics] dati, purché tale schema abbia [!DNL Adobe Analytics ExperienceEvent Template] gruppo di campi. Per utilizzare uno schema personalizzato, seleziona **[!UICONTROL Schema personalizzato]**.

![custom-schema](../../../../images/tutorials/create/analytics/custom-schema.png)

Il [!UICONTROL Mappatura] fornisce un’interfaccia per mappare i campi sorgente ai relativi campi schema di destinazione appropriati. Da qui, puoi mappare le variabili personalizzate ai nuovi gruppi di campi dello schema e applicare i calcoli come supportato dalla preparazione dati. Seleziona uno schema di destinazione per avviare il processo di mappatura.

>[!TIP]
>
>Solo gli schemi che presentano [!DNL Adobe Analytics ExperienceEvent Template] nel menu di selezione dello schema. Gli altri schemi vengono omessi. Se non sono disponibili schemi appropriati per i dati della suite di rapporti, devi creare un nuovo schema. Per la procedura di creazione degli schemi, consulta la guida su [creazione e modifica di schemi nell’interfaccia utente](../../../../../xdm/ui/resources/schemas.md).

![select-schema](../../../../images/tutorials/create/analytics/select-schema.png)

Il [!UICONTROL Mappare i campi standard] mostra i pannelli per [!UICONTROL Mappature standard applicate], [!UICONTROL Mappature standard non corrispondenti] e [!UICONTROL Mappature personalizzate]. Per informazioni specifiche su ciascuna categoria, vedere la tabella seguente:

| Mappare i campi standard | Descrizione |
| --- | --- |
| [!UICONTROL Mappature standard applicate] | Il [!UICONTROL Mappature standard applicate] nel pannello viene visualizzato il numero totale di attributi mappati. Le mappature standard si riferiscono ai set di mappatura tra tutti gli attributi nell’origine [!DNL Analytics] dati e attributi corrispondenti in [!DNL Analytics] gruppo di campi. Questi sono premappati e non possono essere modificati. |
| [!UICONTROL Mappature standard non corrispondenti] | Il [!UICONTROL Mappature standard non corrispondenti] Il pannello si riferisce al numero di attributi mappati che contengono conflitti di nomi descrittivi. Questi conflitti vengono visualizzati quando si riutilizza uno schema che dispone già di un set popolato di descrittori di campo da una suite di rapporti diversa. Puoi procedere con il tuo [!DNL Analytics] flusso di dati anche con conflitti di nomi descrittivi. |
| [!UICONTROL Mappature personalizzate] | Il [!UICONTROL Mappature personalizzate] Nel pannello viene visualizzato il numero di attributi personalizzati mappati, inclusi eVar, prop ed elenchi. Le mappature personalizzate si riferiscono ai set di mappatura tra attributi personalizzati nell’origine [!DNL Analytics] dati e attributi nei gruppi di campi personalizzati inclusi nello schema selezionato. |

![map-standard-fields](../../../../images/tutorials/create/analytics/map-standard-fields.png)

Per visualizzare in anteprima [!DNL Analytics] Gruppo di campi schema modello ExperienceEvent, seleziona **[!UICONTROL Visualizza]** nel [!UICONTROL Mappature standard applicate] pannello.

![visualizza](../../../../images/tutorials/create/analytics/view.png)

Il [!UICONTROL Gruppo di campi dello schema del modello Adobe Analytics ExperienceEvent] fornisce un’interfaccia da utilizzare per esaminare la struttura dello schema. Al termine, seleziona **[!UICONTROL Chiudi]**.

![field-group-preview](../../../../images/tutorials/create/analytics/field-group-preview.png)

Platform rileva automaticamente i set di mappatura per eventuali conflitti di nomi descrittivi. Se non ci sono conflitti con i set di mappatura, seleziona **[!UICONTROL Successivo]** per procedere.

![mappatura](../../../../images/tutorials/create/analytics/mapping.png)

>[!TIP]
>
>In caso di conflitti di nomi descrittivi tra la suite di rapporti di origine e lo schema selezionato, puoi comunque continuare con [!DNL Analytics] flusso di dati, con la conferma che i descrittori dei campi non verranno modificati. In alternativa, puoi scegliere di creare un nuovo schema con un set vuoto di descrittori.

#### Mappature personalizzate

È possibile utilizzare le funzioni di preparazione dati per aggiungere nuove mappature personalizzate o campi calcolati per gli attributi personalizzati. Per aggiungere mappature personalizzate, seleziona **[!UICONTROL Personalizzato]**.

![personalizzato](../../../../images/tutorials/create/analytics/custom.png)

A seconda delle tue esigenze, puoi selezionare: **[!UICONTROL Aggiungi nuova mappatura]** o **[!UICONTROL Aggiungi campo calcolato]** e procedi alla creazione di mappature personalizzate per gli attributi personalizzati. Per i passaggi completi su come utilizzare le funzioni di preparazione dati, leggi [Guida dell’interfaccia utente per la preparazione dati](../../../../../data-prep/ui/mapping.md).

La documentazione seguente fornisce ulteriori risorse sulla preparazione dati, sui campi calcolati e sulle funzioni di mappatura:

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

Una volta completate le mappature per [!DNL Analytics] per i dati della suite di rapporti, puoi applicare regole e condizioni di filtro per includere o escludere selettivamente i dati dall’acquisizione nel Profilo cliente in tempo reale. Il supporto per il filtro è disponibile solo per [!DNL Analytics] dati e dati vengono filtrati solo prima dell’immissione [!DNL Profile.] Tutti i dati vengono acquisiti nel data lake.

>[!BEGINSHADEBOX]

**Informazioni aggiuntive sulla preparazione dei dati e sul filtraggio dei dati di Analytics per Real-Time Customer Profile**

* Puoi utilizzare la funzionalità di filtro per i dati che vanno nel profilo, ma non per i dati che vanno nel data lake.
* Puoi utilizzare il filtro per i dati live, ma non puoi filtrare i dati di retrocompilazione.
   * Il [!DNL Analytics] La sorgente non effettua il backfill dei dati nel profilo.
* Se utilizzi le configurazioni di Preparazione dati durante la configurazione iniziale di un’ [!DNL Analytics] , queste modifiche vengono applicate anche alla retrocompilazione automatica di 13 mesi.
   * Tuttavia, questo non avviene per il filtro, perché il filtro è riservato solo ai dati live.
* La preparazione dati viene applicata ai percorsi di acquisizione in streaming e in batch. Se modifichi una configurazione di Preparazione dati esistente, tali modifiche vengono quindi applicate ai nuovi dati in arrivo attraverso i percorsi di acquisizione in streaming e in batch.
   * Tuttavia, eventuali configurazioni della preparazione dati non si applicano ai dati che sono già stati acquisiti in Experienci Platform, indipendentemente dal fatto che si tratti di dati in streaming o batch.
* Gli attributi standard di Analytics vengono sempre mappati automaticamente. Pertanto, non è possibile applicare trasformazioni agli attributi standard.
   * Tuttavia, puoi filtrare gli attributi standard purché non siano richiesti in Identity Service o Profile.
* Non è possibile utilizzare il filtro a livello di colonna per filtrare i campi obbligatori e i campi di identità.
* Anche se è possibile filtrare le identità secondarie, in particolare AAID e AACustomID, non è possibile filtrare ECID.
* Quando si verifica un errore di trasformazione, la colonna corrispondente restituisce NULL.

>[!ENDSHADEBOX]

### Filtro a livello di riga

>[!IMPORTANT]
>
>Utilizza il filtro a livello di riga per applicare condizioni e stabilire quali dati **includere nell’acquisizione per il profilo**. Utilizza il filtro a livello di colonna per selezionare le colonne di dati che desideri **escludi per l’acquisizione del profilo**.

Puoi filtrare i dati per [!DNL Profile] acquisizione a livello di riga e di colonna. Il filtro a livello di riga consente di definire criteri quali stringa contiene, è uguale a, inizia o termina con. È inoltre possibile utilizzare il filtro a livello di riga per unire le condizioni utilizzando `AND` nonché `OR`, e nega condizioni utilizzando `NOT`.

Per filtrare [!DNL Analytics] dati a livello di riga, seleziona **[!UICONTROL Filtro righe]**.

![row-filter](../../../../images/tutorials/create/analytics/row-filter.png)

Utilizza la barra a sinistra per spostarti nella gerarchia dello schema e selezionare l’attributo dello schema desiderato per approfondire ulteriormente uno schema specifico.

![barra a sinistra](../../../../images/tutorials/create/analytics/left-rail.png)

Dopo aver identificato l’attributo da configurare, selezionalo e trascinalo dalla barra a sinistra al pannello di filtro.

![filtro-pannello](../../../../images/tutorials/create/analytics/filtering-panel.png)

Per configurare diverse condizioni, seleziona **[!UICONTROL è uguale a]** quindi seleziona una condizione dalla finestra a discesa visualizzata.

L’elenco delle condizioni configurabili include:

* [!UICONTROL equals]
* [!UICONTROL non è uguale a]
* [!UICONTROL inizia con]
* [!UICONTROL termina con]
* [!UICONTROL non termina con]
* [!UICONTROL contiene]
* [!UICONTROL non contiene]
* [!UICONTROL exists]
* [!UICONTROL non esiste]

![condizioni](../../../../images/tutorials/create/analytics/conditions.png)

Immettere quindi i valori che si desidera includere in base all&#39;attributo selezionato. Nell’esempio seguente, [!DNL Apple] e [!DNL Google] sono selezionati per l’acquisizione come parte della **[!UICONTROL Produttore]** attributo.

![include-producer](../../../../images/tutorials/create/analytics/include-manufacturer.png)

Per specificare ulteriormente le condizioni di filtro, aggiungi un altro attributo dallo schema, quindi aggiungi i valori basati su tale attributo. Nell’esempio seguente, il **[!UICONTROL Modello]** viene aggiunto l&#39;attributo e modelli come [!DNL iPhone 13] e [!DNL Google Pixel 6] vengono filtrati per l’acquisizione.

![include-model](../../../../images/tutorials/create/analytics/include-model.png)

Per aggiungere un nuovo contenitore, seleziona i puntini di sospensione (`...`) in alto a destra nell’interfaccia di filtraggio, quindi seleziona **[!UICONTROL Aggiungi contenitore]**.

![add-container](../../../../images/tutorials/create/analytics/add-container.png)

Una volta aggiunto un nuovo contenitore, seleziona **[!UICONTROL Includi]** e quindi seleziona **[!UICONTROL Escludi]** dalla finestra a discesa visualizzata.

![escludi](../../../../images/tutorials/create/analytics/exclude.png)

Quindi, completa lo stesso processo trascinando gli attributi dello schema e aggiungendo i relativi valori corrispondenti che desideri escludere dal filtro. Nell’esempio seguente, il [!DNL iPhone 12], [!DNL iPhone 12 mini], e [!DNL Google Pixel 5] sono tutti filtrati dall’esclusione dal **[!UICONTROL Modello]** attributo, orizzontale è escluso dal campo **[!UICONTROL Orientamento schermo]**, e numero di modello [!DNL A1633] è escluso da **[!UICONTROL Numero modello]**.

Al termine, seleziona **[!UICONTROL Successivo]**.

![exclude-examples](../../../../images/tutorials/create/analytics/exclude-examples.png)

### Filtraggio a livello di colonna

Seleziona **[!UICONTROL Filtro colonna]** dall’intestazione per applicare il filtro a livello di colonna.

![column-filter](../../../../images/tutorials/create/analytics/column-filter.png)

La pagina si aggiorna in una struttura di schema interattiva, che mostra gli attributi dello schema a livello di colonna. Da qui puoi selezionare le colonne di dati da escludere [!DNL Profile] acquisizione. In alternativa, è possibile espandere una colonna e selezionare attributi specifici per l&#39;esclusione.

Per impostazione predefinita, tutti [!DNL Analytics] vai a [!DNL Profile] e questo processo consente di escludere i rami di dati XDM da [!DNL Profile] acquisizione.

Al termine, seleziona **[!UICONTROL Successivo]**.

![colonne selezionate](../../../../images/tutorials/create/analytics/columns-selected.png)

### Filtra identità secondarie

Utilizza un filtro a colonne per escludere le identità secondarie dall’acquisizione del profilo. Per filtrare le identità secondarie, seleziona **[!UICONTROL Filtro colonna]** e quindi seleziona **[!UICONTROL _identità]**.

Il filtro si applica solo quando un’identità è contrassegnata come secondaria. Se sono selezionate identità ma arriva un evento con una delle identità contrassegnate come primarie, queste non vengono filtrate.

![secondarie-identità](../../../../images/tutorials/create/analytics/secondary-identities.png)

### Fornisci i dettagli del flusso di dati

Il **[!UICONTROL Dettagli del flusso di dati]** viene visualizzato il passaggio, in cui è necessario fornire un nome e una descrizione facoltativa per il flusso di dati. Seleziona **[!UICONTROL Successivo]** al termine.

![dataflow-detail](../../../../images/tutorials/create/analytics/dataflow-detail.png)

### Revisione

Il [!UICONTROL Revisione] viene visualizzato un passaggio che consente di rivedere il nuovo flusso di dati di Analytics prima che venga creato. I dettagli della connessione sono raggruppati per categorie, tra cui:

* [!UICONTROL Connessione]: visualizza la piattaforma di origine della connessione.
* [!UICONTROL Tipo di dati]: visualizza la suite di rapporti selezionata e il relativo ID suite di rapporti corrispondente.

![recensione](../../../../images/tutorials/create/analytics/review.png)

## Monitorare il flusso di dati {#monitor-your-dataflow}

Una volta completato il flusso di dati, seleziona **[!UICONTROL Flussi dati]** nel catalogo sorgenti per monitorare l’attività e lo stato dei dati.

![Catalogo delle origini con la scheda Flussi dati selezionata.](../../../../images/tutorials/create/analytics/select-dataflows.png)

Viene visualizzato un elenco dei flussi di dati di Analytics esistenti nell’organizzazione. Da qui, seleziona un set di dati di destinazione per visualizzare la rispettiva attività di acquisizione.

![Elenco dei flussi di dati Adobe Analytics esistenti nell’organizzazione.](../../../../images/tutorials/create/analytics/select-target-dataset.png)

Il [!UICONTROL Attività set di dati] fornisce informazioni sull’avanzamento dei dati inviati da Analytics ad Experienci Platform. L’interfaccia visualizza metriche quali il numero di record acquisiti, il numero di batch acquisiti e il numero di batch non riusciti.

L’origine crea un’istanza di due flussi di set di dati. Un flusso rappresenta i dati di backfill e l’altro è per i dati live. I dati di backfill non sono configurati per l’acquisizione in Real-Time Customer Profile, ma vengono inviati al data lake per casi d’uso analitici e di data science.

Per ulteriori informazioni sulla retrocompilazione, sui dati live e sulle rispettive latenze, consulta [Panoramica sull’origine di Analytics](../../../../connectors/adobe-applications/analytics.md).

![Pagina dell’attività del set di dati per un determinato set di dati di destinazione per i dati di Adobe Analytics.](../../../../images/tutorials/create/analytics/dataset-activity.png)

+++Visualizzare singoli batch utilizzando l&#39;interfaccia di monitoraggio legacy

La pagina dell’attività del set di dati non visualizza un elenco di singoli batch. Per visualizzare un elenco di singoli batch, seleziona un grafico nell’interfaccia dell’attività del set di dati.

![Pagina dell’attività del set di dati con un grafico selezionato.](../../../../images/tutorials/create/analytics/select-chart.png)

Viene visualizzata la dashboard Monitoraggio. Quindi, seleziona **[!UICONTROL SOLO ERRORI DI ACQUISIZIONE: SÌ]** per cancellare il filtro e visualizzare un elenco di singoli batch.

![Dashboard di monitoraggio con il filtro errori selezionato.](../../../../images/tutorials/create/analytics/clear-filter.png)

L’interfaccia viene aggiornata a un elenco di singoli batch, incluse informazioni sulle rispettive metriche.

![Pagina di monitoraggio legacy per i dati batch.](../../../../images/tutorials/create/analytics/batch-end-to-end.png)

| Metriche | Descrizione |
| --- | --- |
| ID batch | L’ID di un determinato batch. Questo valore viene generato internamente. |
| Nome del set di dati | Nome di un dato set di dati utilizzato per i dati di Analytics. |
| Origine | L’origine dei dati acquisiti. |
| Aggiornata | Data dell&#39;iterazione dell&#39;esecuzione del flusso più recente. |
| Record nel set di dati | Numero totale di record nel set di dati. **Nota**: questo parametro mostra occasionalmente lo stato `in-progress`. Questo stato indica che il processo di acquisizione dei record non è ancora stato completato. |
| Nuovi frammenti di profilo | Numero totale di nuovi frammenti di profilo acquisiti. |
| Frammenti di profilo esistenti | Numero totale di frammenti di profilo esistenti. |
| Record di identità uniti | Numero totale di record di identità uniti dopo l’acquisizione. |
| Record nel profilo | Numero totale di record acquisiti in Real-Time Customer Profile. |

{style="table-layout:auto"}

+++

## Passaggi successivi e risorse aggiuntive

Una volta creata la connessione, il flusso di dati viene creato automaticamente per contenere i dati in arrivo e popolare un set di dati con lo schema selezionato. Inoltre, avviene il recupero dei dati e vengono acquisiti fino a 13 mesi di dati storici. Al termine dell’acquisizione iniziale, [!DNL Analytics] e possono essere utilizzati da servizi della piattaforma a valle quali [!DNL Real-Time Customer Profile] e Segmentation Service. Per ulteriori informazioni, consulta i seguenti documenti:

* [Panoramica di [!DNL Real-Time Customer Profile]](../../../../../profile/home.md)
* [Panoramica di [!DNL Segmentation Service]](../../../../../segmentation/home.md)
* [Panoramica di [!DNL Data Science Workspace]](../../../../../data-science-workspace/home.md)
* [Panoramica di [!DNL Query Service]](../../../../../query-service/home.md)

Il seguente video ha lo scopo di aiutarti a comprendere come acquisire dati utilizzando il connettore di origine di Adobe Analytics:

>[!WARNING]
>
> Il [!DNL Platform] L’interfaccia utente mostrata nel video seguente non è aggiornata. Per le schermate e le funzionalità più recenti dell’interfaccia utente, consulta la documentazione precedente.

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)
