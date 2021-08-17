---
keywords: Experience Platform;home;argomenti comuni;connettore origine Analytics;connettore Analytics;origine Analytics;Analytics
solution: Experience Platform
title: Creare una connessione sorgente Adobe Analytics nell’interfaccia utente
topic-legacy: overview
type: Tutorial
description: Scopri come creare una connessione sorgente Adobe Analytics nell’interfaccia utente per inserire i dati dei consumatori in Adobe Experience Platform.
exl-id: 5ddbaf63-feaa-44f5-b2f2-2d5ae507f423
source-git-commit: 0af9290a3143b85311fbbd8d194f4799b0c9a873
workflow-type: tm+mt
source-wordcount: '1441'
ht-degree: 1%

---

# Creare una connessione sorgente Adobe Analytics nell’interfaccia utente

Questa esercitazione fornisce passaggi per creare una connessione sorgente Adobe Analytics nell’interfaccia utente per inserire i dati [!DNL Analytics] della suite di rapporti in Adobe Experience Platform.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md) Experience Data Model (XDM): Il framework standardizzato in base al quale l’Experience Platform organizza i dati sulla customer experience.
* [Profilo](../../../../../profile/home.md) cliente in tempo reale: Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

### Terminologia chiave

È importante comprendere i seguenti termini chiave utilizzati in questo documento:

* **Attributo** standard: Gli attributi standard sono tutti gli attributi predefiniti di Adobe. Contengono lo stesso significato per tutti i clienti e sono disponibili nei gruppi di campi [!DNL Analytics] di origine e [!DNL Analytics] dello schema.
* **Attributo** personalizzato: Gli attributi personalizzati sono qualsiasi attributo nella gerarchia delle dimensioni personalizzate in  [!DNL Analytics]. Sono anche uno degli schemi definiti dall’Adobe, ma possono essere interpretati in modo diverso da clienti diversi. Gli attributi personalizzati includono eVar, prop ed elenchi. Per ulteriori informazioni sulle eVar, consulta la seguente [[!DNL Analytics] documentazione sulle variabili di conversione](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) .
* **Qualsiasi attributo nei gruppi** di campi personalizzati: Gli attributi che provengono da gruppi di campi creati dai clienti sono tutti definiti dall’utente e non sono considerati attributi standard o personalizzati.
* **Nomi** descrittivi: I nomi descrittivi sono etichette fornite dall&#39;utente per le variabili personalizzate in un&#39; [!DNL Analytics] implementazione. Per ulteriori informazioni sui nomi descrittivi, consulta la seguente [[!DNL Analytics] documentazione sulle variabili di conversione](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) .

## Creare una connessione sorgente con Adobe Analytics

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all’area di lavoro [!UICONTROL Origini]. La schermata [!UICONTROL Catalogo] visualizza una varietà di sorgenti con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. Puoi anche usare la barra di ricerca per limitare le sorgenti visualizzate.

Sotto la categoria **[!UICONTROL Applicazioni di Adobe]**, selezionare **[!UICONTROL Adobe Analytics]**, quindi selezionare **[!UICONTROL Aggiungi dati]**.

![catalogo](../../../../images/tutorials/create/analytics/catalog.png)

### Seleziona dati

Viene visualizzato il passaggio **[!UICONTROL Aggiungi dati origine Analytics]** . Seleziona **[!UICONTROL Suite di rapporti]** per iniziare a creare una connessione sorgente per i dati della suite di rapporti di Analytics, quindi seleziona la suite di rapporti da acquisire. Selezionare **[!UICONTROL Avanti]** per continuare.

>[!NOTE]
>
>È possibile effettuare più connessioni in-bound a un’origine per l’inserimento di dati diversi.

![](../../../../images/tutorials/create/analytics/add-data.png)

<!---Analytics report suites can be configured for one sandbox at a time. To import the same report suite into a different sandbox, the dataset flow will have to be deleted and instantiated again via configuration for a different sandbox.--->

### Mappatura

>[!IMPORTANT]
>
>La funzione di supporto di Data Prep per la sorgente [!DNL Analytics] è in versione beta.

La pagina [!UICONTROL Mapping] fornisce un&#39;interfaccia per mappare i campi di origine ai campi dello schema di destinazione appropriati. Da qui puoi mappare variabili personalizzate a nuovi gruppi di campi dello schema e applicare calcoli supportati da Data Prep. Seleziona uno schema di destinazione per avviare il processo di mappatura.

>[!TIP]
>
>Nel menu di selezione dello schema vengono visualizzati solo gli schemi che hanno il gruppo di campi modello [!DNL Analytics] . Gli altri schemi vengono omessi. Se non sono disponibili schemi appropriati per i dati della suite di rapporti, devi creare un nuovo schema. Per passaggi dettagliati sulla creazione degli schemi, consulta la guida alla [creazione e modifica degli schemi nell’interfaccia utente](../../../../../xdm/ui/resources/schemas.md).

![select-schema](../../../../images/tutorials/create/analytics/select-schema.png)

La sezione [!UICONTROL Mappa campi standard] visualizza i pannelli per le mappature [!UICONTROL Standard applicate], [!UICONTROL Mappature standard non corrispondenti] e [!UICONTROL Mappature personalizzate]. Per informazioni specifiche relative a ciascuna categoria, consultare la tabella seguente:

| Mappa campi standard | Descrizione |
| --- | --- |
| [!UICONTROL Mappature standard applicate] | Il pannello [!UICONTROL Mappature standard applicate] visualizza il numero totale di attributi standard mappati. Le mappature standard si riferiscono ai set di mappatura tra gli attributi standard nei dati di origine [!DNL Analytics] e gli attributi standard nel gruppo di campi [!DNL Analytics]. Questi sono pre-mappati e non possono essere modificati. |
| [!UICONTROL Mappature standard non corrispondenti] | Il pannello [!UICONTROL Mappature standard non corrispondenti] fa riferimento al numero di attributi standard mappati che contengono conflitti di nomi descrittivi. Questi conflitti vengono visualizzati quando si riutilizza uno schema che dispone già di un set popolato di descrittori di campo. Puoi procedere con il flusso di dati [!DNL Analytics] anche con conflitti di nomi descrittivi. |
| [!UICONTROL Mappature personalizzate] | Il pannello [!UICONTROL Mappature personalizzate] visualizza il numero di attributi personalizzati mappati, tra cui eVar, prop ed elenchi. Le mappature personalizzate fanno riferimento ai set di mappature tra gli attributi personalizzati nei dati [!DNL Analytics] di origine e gli attributi personalizzati nel gruppo di campi [!DNL Analytics]. Gli attributi personalizzati possono essere mappati ad altri attributi personalizzati, nonché agli attributi standard. |

![map-standard-fields](../../../../images/tutorials/create/analytics/map-standard-fields.png)

Per visualizzare in anteprima il gruppo di campi dello schema del modello di esperienza [!DNL Analytics], seleziona **[!UICONTROL Visualizza]** nel pannello [!UICONTROL Mappature standard applicate].

![visualizzare](../../../../images/tutorials/create/analytics/view.png)

La pagina [!UICONTROL Gruppo di campi schema modello di Adobe Analytics ExperienceEvent] offre un&#39;interfaccia da utilizzare per controllare la struttura dello schema. Al termine, selezionare **[!UICONTROL Chiudi]**.

![field-group-preview](../../../../images/tutorials/create/analytics/field-group-preview.png)

Platform rileva automaticamente i set di mappatura per eventuali conflitti di nomi descrittivi. Se non ci sono conflitti con i set di mappatura, selezionare **[!UICONTROL Avanti]** per continuare.

![mappatura](../../../../images/tutorials/create/analytics/mapping.png)

Se nei set di mappatura sono presenti conflitti di nomi descrittivi, puoi comunque continuare con il flusso di dati [!DNL Analytics], riconoscendo che i descrittori dei campi saranno gli stessi. In alternativa, puoi scegliere di creare un nuovo schema con un set vuoto di descrittori.

Selezionare **[!UICONTROL Avanti]** per continuare.

![cautela](../../../../images/tutorials/create/analytics/caution.png)

#### Mappature personalizzate

Per utilizzare le funzioni di preparazione dei dati e aggiungere nuovi campi di mappatura o calcolati per gli attributi personalizzati, seleziona **[!UICONTROL Visualizza mappature personalizzate]**.

![view-custom-mapping](../../../../images/tutorials/create/analytics/view-custom-mapping.png)

Quindi, seleziona **[!UICONTROL Aggiungi nuova mappatura]**.

A seconda delle tue esigenze, puoi selezionare **[!UICONTROL Aggiungi nuova mappatura]** o **[!UICONTROL Aggiungi campo calcolato]** dalle opzioni visualizzate.

![add-new-mapping](../../../../images/tutorials/create/analytics/add-new-mapping.png)

Viene visualizzato un set di mappature vuoto. Seleziona l’icona di mappatura per aggiungere un campo sorgente.

![select-source-field](../../../../images/tutorials/create/analytics/select-source-field.png)

È possibile utilizzare l&#39;interfaccia per navigare nella struttura dello schema di origine e identificare il nuovo campo di origine che si desidera utilizzare. Dopo aver selezionato il campo di origine da mappare, selezionare **[!UICONTROL Seleziona]**.

![select-mapping](../../../../images/tutorials/create/analytics/select-mapping.png)

Quindi, seleziona l’icona di mappatura in [!UICONTROL Campo di destinazione] per mappare il campo di origine selezionato al relativo campo di destinazione appropriato.

![select-target-field](../../../../images/tutorials/create/analytics/select-target-field.png)

Analogamente allo schema di origine, è possibile utilizzare l’interfaccia per navigare nella struttura dello schema di destinazione e selezionare il campo di destinazione a cui si desidera eseguire la mappatura. Dopo aver selezionato il campo di destinazione appropriato, seleziona **[!UICONTROL Seleziona]**.

![select-target-mapping](../../../../images/tutorials/create/analytics/select-target-mapping.png)

Una volta completato il set di mappatura personalizzato, seleziona **[!UICONTROL Avanti]** per continuare.

![complete-custom-mapping](../../../../images/tutorials/create/analytics/complete-custom-mapping.png)

La seguente documentazione fornisce ulteriori risorse sulla preparazione dei dati, sui campi calcolati e sulle funzioni di mappatura:

* [Panoramica sulla preparazione dei dati](../../../../../data-prep/home.md)
* [Funzioni di mappatura della preparazione dei dati](../../../../../data-prep/functions.md)
* [Aggiungi campi calcolati](../../../../../data-prep/calculated-fields.md)

### Fornire i dettagli del flusso di dati

Viene visualizzato il passaggio **[!UICONTROL Dettaglio flusso di dati]** in cui è necessario specificare un nome e una descrizione facoltativa per il flusso di dati. Al termine, seleziona **[!UICONTROL Avanti]**.

![dettaglio del flusso di dati](../../../../images/tutorials/create/analytics/dataflow-detail.png)

### Revisione

Viene visualizzato il passaggio [!UICONTROL Rivedi], che consente di rivedere il nuovo flusso di dati di Analytics prima della creazione. I dettagli della connessione sono raggruppati per categorie, tra cui:

* [!UICONTROL Connessione]: Visualizza la piattaforma sorgente della connessione.
* [!UICONTROL Tipo] di dati: Visualizza la suite di rapporti selezionata e il relativo ID suite di rapporti.

![revisione](../../../../images/tutorials/create/analytics/review.png)

### Monitorare il flusso di dati

Una volta creato il flusso di dati, puoi monitorare i dati che vengono acquisiti tramite di esso. Dalla schermata [!UICONTROL Catalogo], seleziona **[!UICONTROL Flussi di dati]** per visualizzare un elenco dei flussi stabiliti associati al tuo account Analytics.

![select-dataflows](../../../../images/tutorials/create/analytics/select-dataflows.png)

Viene visualizzata la schermata **Dataflows**. In questa pagina è presente una coppia di flussi di set di dati, che include informazioni su nome, dati di origine, tempo di creazione e stato.

Il connettore crea un&#39;istanza di due flussi di set di dati. Un flusso rappresenta i dati di backfill e l’altro è per i dati live. I dati di backfill non sono configurati per il profilo, ma vengono inviati al data lake per casi d’uso analitici e per la scienza dei dati.

Per ulteriori informazioni sul backfill, i dati live e le rispettive latenze, consulta la [panoramica di Analytics Data Connector](../../../../connectors/adobe-applications/analytics.md).

Seleziona il flusso di set di dati da visualizzare dall’elenco.

![select-target-dataset](../../../../images/tutorials/create/analytics/select-target-dataset.png)

Viene visualizzata la pagina **[!UICONTROL Attività set di dati]** . In questa pagina viene visualizzata la frequenza dei messaggi visualizzati sotto forma di grafico. Seleziona **[!UICONTROL Data governance]** dall&#39;intestazione superiore per accedere ai campi di etichettatura.

![dataset-activity](../../../../images/tutorials/create/analytics/dataset-activity.png)

Puoi visualizzare le etichette ereditate di un flusso di dati dalla schermata [!UICONTROL governance dei dati] . Per ulteriori informazioni su come etichettare i dati provenienti da Analytics, visita la [guida alle etichette per l&#39;uso dei dati](../../../../../data-governance/labels/user-guide.md).

![data-gov](../../../../images/tutorials/create/analytics/data-gov.png)

Per eliminare un flusso di dati, passare alla pagina [!UICONTROL Dataflows], quindi selezionare i puntini di sospensione (`...`) accanto al nome del flusso di dati, quindi selezionare [!UICONTROL Delete].

![delete](../../../../images/tutorials/create/analytics/delete.png)

## Passaggi successivi e risorse aggiuntive

Una volta creata la connessione, viene creato automaticamente uno schema e un flusso di dati di destinazione per contenere i dati in arrivo. Inoltre, avviene il recupero dei dati e vengono acquisiti fino a 13 mesi di dati storici. Al termine dell’acquisizione iniziale, i dati [!DNL Analytics] vengono utilizzati dai servizi della piattaforma a valle, come [!DNL Real-time Customer Profile] e il servizio di segmentazione. Per ulteriori informazioni, consulta i seguenti documenti:

* [[!DNL Real-time Customer Profile] panoramica](../../../../../profile/home.md)
* [[!DNL Segmentation Service] panoramica](../../../../../segmentation/home.md)
* [[!DNL Data Science Workspace] panoramica](../../../../../data-science-workspace/home.md)
* [[!DNL Query Service] panoramica](../../../../../query-service/home.md)

Il seguente video è pensato per comprendere come acquisire i dati utilizzando il connettore Adobe Analytics Source:

>[!WARNING]
>
> L’ [!DNL Platform] interfaccia utente mostrata nel video seguente è obsoleta. Fai riferimento alla documentazione precedente per le ultime schermate e funzionalità dell’interfaccia utente.

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)
