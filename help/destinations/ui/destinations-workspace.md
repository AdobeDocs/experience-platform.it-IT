---
keywords: piattaforma;destinazioni;area di lavoro destinazioni;area di lavoro;ui;interfaccia destinazioni;catalogo;catalogo destinazioni;
title: Area di lavoro Destinazioni
description: 'L''area di lavoro Destinazioni è composta da quattro sezioni: Catalogo, Sfoglia, Account e Vista sistema. Sono descritti nelle sezioni seguenti.'
seo-description: In Adobe Experience Platform, seleziona Destinazioni dalla barra di navigazione a sinistra per accedere all’area di lavoro delle destinazioni.
exl-id: 0f46f08d-0fe3-441d-933a-86bc146c0f19
source-git-commit: a619227de30513bb06a22ce7b4f2fc13847c1ab6
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 2%

---

# Area di lavoro Destinazioni {#destinations-workspace}

In Adobe Experience Platform, seleziona **[!UICONTROL Destinazioni]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Destinazioni].

L&#39;area di lavoro [!UICONTROL Destinazioni] è composta da cinque sezioni: [!UICONTROL Panoramica], [!UICONTROL Catalogo], [!UICONTROL Sfoglia], [!UICONTROL Account] e [!UICONTROL Vista di sistema], descritte nelle sezioni seguenti.

![Destinazioni - Panoramica](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL Panoramica] {#overview}

La scheda **[!UICONTROL Panoramica]** visualizza il dashboard [!UICONTROL Destinazioni], fornendo le metriche chiave relative ai dati di destinazione della tua organizzazione. Per ulteriori informazioni, visita la guida [[!UICONTROL Destinazioni] del dashboard](../../dashboards/guides/destinations.md).

>[!NOTE]
>
>Se la tua organizzazione ha poca esperienza con Experience Platform e non dispone ancora di destinazioni attive, il dashboard [!UICONTROL Destinazioni] e la scheda [!UICONTROL Panoramica] non sono visibili. Invece, selezionando [!UICONTROL Destinazioni] dalla navigazione a sinistra viene visualizzata la scheda [[!UICONTROL Catalogo]](#catalog) .

![](../../dashboards/images/destinations/dashboard-overview.png)

## [!UICONTROL Catalogo] {#catalog}

La scheda **[!UICONTROL Catalogo]** visualizza un elenco di tutte le destinazioni disponibili in [!DNL Platform] a cui è possibile inviare i dati.

L&#39;interfaccia utente [!DNL Platform] fornisce diverse opzioni di ricerca e filtro nella pagina del catalogo delle destinazioni:

* Utilizza la funzionalità di ricerca nella pagina per individuare una destinazione specifica.
* Filtrare le destinazioni utilizzando il controllo [!UICONTROL Categorie].
* Passa da [!UICONTROL Tutte le destinazioni] a [!UICONTROL Le mie destinazioni]. Quando selezioni **[!UICONTROL Tutte le destinazioni]**, vengono visualizzate tutte le destinazioni [!DNL Platform] disponibili. Quando selezioni **[!UICONTROL Le mie destinazioni]**, puoi vedere solo le destinazioni con le quali hai stabilito una connessione.
* Selezionare per visualizzare **[!UICONTROL Connessioni]** e/o **[!UICONTROL Estensioni]**. Per comprendere la differenza tra le due categorie, vedere [Tipi di destinazione e Categorie](../destination-types.md).

![demo di filtro e ricerca delle destinazioni](../assets/ui/workspace/destinations-search-and-filter.gif)

Le schede di destinazione contengono un controllo **[!UICONTROL Configure]** o **[!UICONTROL Activate]** e un controllo secondario che consente di visualizzare più opzioni. Questi controlli sono descritti di seguito:

| Controllo | Descrizione |
|---------|----------|
| [!UICONTROL Configurare gli] | Consente di creare una connessione alla destinazione. |
| [!UICONTROL Attiva] | Una volta stabilita una connessione alla destinazione, puoi attivare i segmenti. |
| [!UICONTROL Visualizza account] | Visualizzare gli account connessi a una destinazione. |
| [!UICONTROL Visualizzare i flussi di dati] | Visualizza i flussi di attivazione dei dati esistenti per una destinazione. |
| [!UICONTROL Visualizza la documentazione] | Apre un collegamento alla pagina di documentazione per la destinazione specifica, per ulteriori informazioni e per facilitarne la configurazione. |

{style=&quot;table-layout:auto&quot;}

![Controlli sulla scheda delle destinazioni](../assets/ui/workspace/destination-card-options.png)

Seleziona una scheda di destinazione nel catalogo per aprire la barra a destra. Qui puoi vedere una descrizione della destinazione. La barra a destra fornisce gli stessi controlli descritti nella tabella precedente, compresa una descrizione della destinazione e un’indicazione della categoria e del tipo di destinazione.

![Opzioni del catalogo di destinazione](../assets/ui/workspace/destination-right-rail.png)

Per ulteriori informazioni sulle categorie di destinazione e sulle relative informazioni, vedere il [Catalogo di destinazione](../catalog/overview.md) e [Tipi e categorie di destinazione](../destination-types.md).

## [!UICONTROL Account] {#accounts}

La scheda **[!UICONTROL Account]** mostra i dettagli delle connessioni stabilite con diverse destinazioni e consente di aggiornare i dettagli di connessione esistenti. Per istruzioni dettagliate, consulta [Aggiornare account](update-accounts.md) .

## [!UICONTROL Sfoglia] {#browse}

La scheda **[!UICONTROL Sfoglia]** visualizza le destinazioni con le quali hai stabilito una connessione. Le destinazioni con l&#39;opzione **[!UICONTROL Abilitato/Disabilitato]** attivata impostano la destinazione rispettivamente su attivo o inattivo. Puoi anche visualizzare le destinazioni in cui scorrono i dati selezionando **[!UICONTROL Segmenti]** > **[!UICONTROL Sfoglia]** e selezionando un segmento da esaminare. Vedi la tabella seguente per tutte le informazioni fornite per ogni destinazione nella scheda Sfoglia:

>[!TIP]
>
> * Utilizza il pulsante ![Aggiungi segmenti](../assets/ui/workspace/add-data-symbol.png) nella colonna **[!UICONTROL Nome]** per inviare i segmenti a tale destinazione.
> * Utilizza il pulsante ![Elimina destinazioni](../assets/ui/workspace/delete-destination-symbol.png) nella colonna **[!UICONTROL Nome]** per [eliminare](delete-destinations.md) una connessione esistente a una destinazione.


![Scheda Sfoglia](../assets/ui/workspace/browse-tab.png)

| Elemento | Descrizione |
|---------|----------|
| Nome | Nome fornito per il flusso di attivazione a questa destinazione. La stessa colonna include due controlli: [!UICONTROL Attiva ] e [!UICONTROL Elimina destinazione]. |
| [!UICONTROL Stato ultima esecuzione flusso] | Lo stato dell’ultima esecuzione del flusso di dati. Per ulteriori informazioni sulle esecuzioni dei flussi di dati, consulta [Visualizzare i dettagli di destinazione](destination-details-page.md) . |
| [!UICONTROL Data ultima esecuzione flusso] | Ora e data dell’ultima esecuzione del flusso di dati. Per ulteriori informazioni sulle esecuzioni dei flussi di dati, consulta [Visualizzare i dettagli di destinazione](destination-details-page.md) . |
| [!UICONTROL Destinazione] | La piattaforma di destinazione selezionata per il flusso di attivazione. |
| [!UICONTROL Tipo connessione] | Rappresenta il tipo di connessione al bucket di archiviazione o alla destinazione. <ul><li>Per le destinazioni di marketing e-mail: Può essere S3, FTP o [!DNL Azure Blob].</li><li>Per le destinazioni pubblicitarie in tempo reale: Server-to-server.</li><li>Per le destinazioni di streaming: Può essere [!DNL Azure Event Hubs] o [!DNL Amazon Kinesis].</li></ul> |
| [!UICONTROL Nome utente] | Le credenziali account selezionate per il flusso di destinazione. |
| [!UICONTROL Dati di attivazione] | Indica il numero di segmenti che vengono attivati nella destinazione. Seleziona questo controllo per ulteriori informazioni sui segmenti attivati. Per ulteriori informazioni sui segmenti attivati, consulta [Dati di attivazione](/help/destinations/ui/destination-details-page.md#activation-data) nella pagina dei dettagli della destinazione . |
| [!UICONTROL Creato] | Data e ora UTC in cui è stato creato il flusso di attivazione alla destinazione. |
| [!UICONTROL Stato] | `Active` oppure `Inactive`. Indica se i dati vengono attivati per questa destinazione. |

Fai clic su una riga di destinazione per visualizzare ulteriori informazioni sulla destinazione nella barra a destra.

![Fai clic sulla riga di destinazione](../assets/ui/workspace/click-destination-row.png)

Seleziona il nome della destinazione per visualizzare le informazioni sui segmenti attivati in questa destinazione. Fai clic su **[!UICONTROL Modifica attivazione]** per modificare o aggiungere ai segmenti che vengono inviati a questa destinazione.

## [!UICONTROL Vista di sistema] {#system-view}

La scheda **[!UICONTROL Vista sistema]** visualizza una rappresentazione grafica dei flussi di attivazione impostati in Adobe Experience Platform.

![Flussi di dati1](../assets/ui/workspace/data-flows1.png)

Seleziona una delle destinazioni visualizzate sulla pagina e fai clic su **[!UICONTROL Visualizza flussi]** per visualizzare informazioni su tutte le connessioni impostate per ciascuna destinazione.

![Flussi di dati2](../assets/ui/workspace/data-flows2.png)
