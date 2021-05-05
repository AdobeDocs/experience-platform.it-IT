---
keywords: piattaforma;destinazioni;area di lavoro destinazioni;area di lavoro;ui;interfaccia destinazioni;catalogo;catalogo destinazioni;
title: Area di lavoro Destinazioni
description: 'L''area di lavoro Destinazioni è composta da quattro sezioni: Catalogo, Sfoglia, Account e Vista sistema. Sono descritti nelle sezioni seguenti.'
seo-description: In Adobe Experience Platform, seleziona Destinazioni dalla barra di navigazione a sinistra per accedere all’area di lavoro delle destinazioni.
exl-id: 0f46f08d-0fe3-441d-933a-86bc146c0f19
translation-type: tm+mt
source-git-commit: eaa4a7efc248104d823267eca574f2eca16edc3f
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 1%

---

# Area di lavoro Destinazioni {#destinations-workspace}

## Panoramica {#overview}

In Adobe Experience Platform, seleziona **[!UICONTROL Destinations]** dalla barra di navigazione a sinistra per accedere all’area di lavoro [!UICONTROL Destinations].

L’area di lavoro [!UICONTROL Destinations] è costituita da quattro sezioni, [!UICONTROL Catalog], [!UICONTROL Browse], [!UICONTROL Accounts] e [!UICONTROL System View], descritte nelle sezioni seguenti.

![Destinazioni - Panoramica](../assets/ui/workspace/destinations-workspace.png)

## [!UICONTROL Catalog] {#catalog}

La scheda **[!UICONTROL Catalog]** visualizza un elenco di tutte le destinazioni disponibili in [!DNL Platform] a cui è possibile inviare i dati.

L&#39;interfaccia utente [!DNL Platform] fornisce diverse opzioni di ricerca e filtro nella pagina del catalogo delle destinazioni:

* Utilizza la funzionalità di ricerca nella pagina per individuare una destinazione specifica.
* Filtrare le destinazioni utilizzando il controllo [!UICONTROL Categories].
* Passa da [!UICONTROL All destinations] a [!UICONTROL My destinations]. Quando selezioni **[!UICONTROL All destinations]**, vengono visualizzate tutte le destinazioni [!DNL Platform] disponibili. Quando selezioni **[!UICONTROL My destinations]**, puoi visualizzare solo le destinazioni con le quali hai stabilito una connessione.
* Selezionare per visualizzare **[!UICONTROL Connections]** e/o **[!UICONTROL Extensions]**. Per comprendere la differenza tra le due categorie, vedere [Tipi di destinazione e Categorie](../destination-types.md).

![demo di filtro e ricerca delle destinazioni](../assets/ui/workspace/destinations-search-and-filter.gif)

Le schede di destinazione contengono un controllo **[!UICONTROL Configure]** o **[!UICONTROL Activate]** e un controllo secondario che offre più opzioni. Questi controlli sono descritti di seguito:

| Controllo | Descrizione |
|---------|----------|
| [!UICONTROL Configure] | Consente di creare una connessione alla destinazione. |
| [!UICONTROL Activate] | Una volta stabilita una connessione alla destinazione, puoi attivare i segmenti. |
| [!UICONTROL View account] | Visualizzare gli account connessi a una destinazione. |
| [!UICONTROL View dataflows] | Visualizza i flussi di attivazione dei dati esistenti per una destinazione. |
| [!UICONTROL View documentation] | Apre un collegamento alla pagina di documentazione per la destinazione specifica, per ulteriori informazioni e per facilitarne la configurazione. |

{style=&quot;table-layout:auto&quot;}

![Controlli sulla scheda delle destinazioni](../assets/ui/workspace/destination-card-options.png)

Seleziona una scheda di destinazione nel catalogo per aprire la barra a destra. Qui puoi vedere una descrizione della destinazione. La barra a destra fornisce gli stessi controlli descritti nella tabella precedente, compresa una descrizione della destinazione e un’indicazione della categoria e del tipo di destinazione.

![Opzioni del catalogo di destinazione](../assets/ui/workspace/destination-right-rail.png)

Per ulteriori informazioni sulle categorie di destinazione e sulle relative informazioni, vedere il [Catalogo di destinazione](../catalog/overview.md) e [Tipi e categorie di destinazione](../destination-types.md).

## [!UICONTROL Accounts] {#accounts}

La scheda **[!UICONTROL Accounts]** mostra i dettagli delle connessioni stabilite con diverse destinazioni e consente di aggiornare i dettagli di connessione esistenti. Per istruzioni dettagliate, consulta [Aggiornare account](update-accounts.md) .

## [!UICONTROL Browse] {#browse}

La scheda **[!UICONTROL Browse]** visualizza le destinazioni con le quali hai stabilito una connessione. Le destinazioni con l&#39;opzione **[!UICONTROL Enabled/Disabled]** attivata impostano la destinazione rispettivamente su attiva o inattiva. Puoi anche visualizzare le destinazioni in cui scorrono i dati selezionando **[!UICONTROL Segments]** > **[!UICONTROL Browse]** e selezionando un segmento da esaminare. Vedi la tabella seguente per tutte le informazioni fornite per ogni destinazione nella scheda Sfoglia:

>[!TIP]
>
> * Utilizza il pulsante ![Aggiungi segmenti](../assets/ui/workspace/add-data-symbol.png) nella colonna **[!UICONTROL Name]** per [attivare](activate-destinations.md) altri segmenti in quella destinazione.
> * Utilizza il pulsante ![Elimina destinazioni](../assets/ui/workspace/delete-destination-symbol.png) nella colonna **[!UICONTROL Name]** per [eliminare](delete-destinations.md) una connessione esistente a una destinazione.


![Scheda Sfoglia](../assets/ui/workspace/browse-tab.png)

| Elemento | Descrizione |
|---------|----------|
| Nome | Nome fornito per il flusso di attivazione a questa destinazione. La stessa colonna include due controlli: [!UICONTROL Activate ] e [!UICONTROL Delete destination]. |
| [!UICONTROL Last Flow Run Status] | Lo stato dell’ultima esecuzione del flusso di dati. Per ulteriori informazioni sulle esecuzioni dei flussi di dati, consulta [Visualizzare i dettagli di destinazione](destination-details-page.md) . |
| [!UICONTROL Last Flow Run Date] | Ora e data dell’ultima esecuzione del flusso di dati. Per ulteriori informazioni sulle esecuzioni dei flussi di dati, consulta [Visualizzare i dettagli di destinazione](destination-details-page.md) . |
| [!UICONTROL Destination] | La piattaforma di destinazione selezionata per il flusso di attivazione. |
| [!UICONTROL Connection Type] | Rappresenta il tipo di connessione al bucket di archiviazione o alla destinazione. <ul><li>Per le destinazioni di marketing e-mail: Può essere S3, FTP o [!DNL Azure Blob].</li><li>Per le destinazioni pubblicitarie in tempo reale: Server-to-server.</li><li>Per le destinazioni di streaming: Può essere [!DNL Azure Event Hubs] o [!DNL Amazon Kinesis].</li></ul> |
| [!UICONTROL Username] | Le credenziali account selezionate per il flusso di destinazione. |
| [!UICONTROL Activation Data] | Indica il numero di segmenti che vengono attivati nella destinazione. Seleziona questo controllo per ulteriori informazioni sui segmenti attivati. Per ulteriori informazioni sui segmenti attivati, consulta [Dati di attivazione](/help/destinations/ui/destination-details-page.md#activation-data) nella pagina dei dettagli della destinazione . |
| [!UICONTROL Created] | Data e ora UTC in cui è stato creato il flusso di attivazione alla destinazione. |
| [!UICONTROL Status] | `Active` oppure `Inactive`. Indica se i dati vengono attivati per questa destinazione. Per modificare lo stato, consulta [Disabilita attivazione](./activate-destinations.md#disable-activation). |

Fai clic su una riga di destinazione per visualizzare ulteriori informazioni sulla destinazione nella barra a destra.

![Fai clic sulla riga di destinazione](../assets/ui/workspace/click-destination-row.png)

Seleziona il nome della destinazione per visualizzare le informazioni sui segmenti attivati in questa destinazione. Fai clic su **[!UICONTROL Edit activation]** per modificare o aggiungere ai segmenti che vengono inviati a questa destinazione.

## [!UICONTROL System View] {#system-view}

La scheda **[!UICONTROL System View]** visualizza una rappresentazione grafica dei flussi di attivazione impostati in Adobe Experience Platform.

![Flussi di dati1](../assets/ui/workspace/data-flows1.png)

Seleziona una delle destinazioni visualizzate sulla pagina e fai clic su **[!UICONTROL View flows]** per visualizzare informazioni su tutte le connessioni configurate per ciascuna destinazione.

![Flussi di dati2](../assets/ui/workspace/data-flows2.png)
