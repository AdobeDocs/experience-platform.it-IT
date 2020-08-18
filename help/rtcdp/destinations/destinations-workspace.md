---
keywords: RTCDP;rtcdp
title: Area di lavoro Destinazioni
seo-title: Area di lavoro Destinazioni
description: In  Adobe Piattaforma dati cliente in tempo reale, seleziona Destinazioni dalla barra di navigazione a sinistra per accedere all'area di lavoro delle destinazioni.
seo-description: In  Adobe Piattaforma dati cliente in tempo reale, seleziona Destinazioni dalla barra di navigazione a sinistra per accedere all'area di lavoro delle destinazioni.
translation-type: tm+mt
source-git-commit: ac9c629e8c83d3e056ba94b30d978edbda274923
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 1%

---


# Area di lavoro Destinazioni {#destinations-workspace}

In  Adobe Piattaforma dati cliente in tempo reale, selezionate **[!UICONTROL Destinations]** dalla barra di navigazione a sinistra per accedere all&#39; [!UICONTROL Destinations] area di lavoro.

L’ [!UICONTROL Destinations] area di lavoro è composta da quattro sezioni, **[!UICONTROL Catalog]**, **[!UICONTROL Browse]**, **[!UICONTROL Accounts]** e **[!UICONTROL System View]**, descritte nelle sezioni seguenti.

![Destinazioni-panoramica](/help/rtcdp/destinations/assets/destinations-overview.png)

## [!UICONTROL Catalog] {#catalog}

Nella **[!UICONTROL Catalog]** scheda viene visualizzato un elenco di tutte le destinazioni disponibili in CDP in tempo reale  Adobe a cui è possibile inviare i dati.

L’interfaccia utente CDP in tempo reale del Adobe  fornisce una serie di opzioni di ricerca e filtro nella pagina del catalogo delle destinazioni:

* Utilizzate la funzionalità di ricerca sulla pagina per individuare una destinazione specifica.
* Filtrare le destinazioni utilizzando il **[!UICONTROL Categories]** controllo.
* Passa da **[!UICONTROL All destinations]** a **[!UICONTROL My destinations]**. Quando **[!UICONTROL All destinations]** è selezionato, vengono visualizzate tutte le destinazioni CDP in tempo reale  Adobe disponibili. Quando **[!UICONTROL My destinations]** è selezionata, è possibile visualizzare solo le destinazioni con le quali è stata stabilita una connessione.
* Selezionare per visualizzare **[!UICONTROL Connections]** e/o **[!UICONTROL Extensions]**. Per comprendere la differenza tra le due categorie, vedere Tipi di [destinazione e categorie](/help/rtcdp/destinations/destination-types.md).

![demo di filtraggio delle destinazioni e ricerca](/help/rtcdp/destinations/assets/destinations-search-and-filter.gif)

Le schede di destinazione contengono un controllo **[!UICONTROL Configure]** o un **[!UICONTROL Activate]** controllo secondario che consente di visualizzare più opzioni. Sono descritti di seguito:

| Control | Descrizione |
---------|----------
| [!UICONTROL Configure] | Consente di creare una connessione alla destinazione. |
| [!UICONTROL Activate] | Una volta stabilita una connessione alla destinazione, puoi attivare i segmenti. |
| [!UICONTROL View account] | Visualizza gli account che hai connesso per una destinazione. |
| [!UICONTROL View dataflows] | Visualizzare i flussi di attivazione dei dati esistenti per una destinazione. |
| [!UICONTROL View documentation] | Consente di aprire un collegamento alla pagina della documentazione relativa alla destinazione specifica, per ulteriori informazioni e per facilitare la configurazione. |

![Controlli sulla scheda delle destinazioni](/help/rtcdp/destinations/assets/destination-card-options.png)

Selezionate una scheda di destinazione nel catalogo per aprire la barra laterale destra.  Qui potete vedere una descrizione della destinazione. La barra a destra fornisce gli stessi controlli descritti nella tabella precedente, nonché una descrizione della destinazione e un&#39;indicazione della categoria e del tipo di destinazione.

![Opzioni del catalogo di destinazione](/help/rtcdp/destinations/assets/destination-right-rail.png)

Per ulteriori informazioni sulle categorie di destinazione e informazioni su ciascuna destinazione, consulta Catalogo [di](/help/rtcdp/destinations/destinations-catalog.md) destinazione e Tipi e categorie [di](/help/rtcdp/destinations/destination-types.md)destinazione.

## [!UICONTROL Browse] {#browse}

Nella **[!UICONTROL Browse]** scheda vengono visualizzate le destinazioni con le quali è stata stabilita una connessione. Le destinazioni con l&#39; **[!UICONTROL enabled]** interruttore attivato impostano la destinazione su attiva e viceversa. Per visualizzare le destinazioni in cui i dati scorrono, seleziona **[!UICONTROL Segments]** > **[!UICONTROL Browse]** e seleziona un segmento da ispezionare. Per tutte le informazioni fornite per ciascuna destinazione, consultate la tabella seguente nella scheda Sfoglia:

![Scheda Sfoglia](/help/rtcdp/destinations/assets/browse-tab.png)

| Elemento | Descrizione |
---------|----------
| Nome | Nome fornito per il flusso di attivazione a questa destinazione. |
| [!UICONTROL Destination] | La piattaforma di destinazione selezionata per il flusso di attivazione. |
| [!UICONTROL Connection Type] | Rappresenta il tipo di connessione al bucket di archiviazione o alla destinazione. <ul><li>Per le destinazioni di e-mail marketing: Può essere S3 o FTP.</li><li>Per le destinazioni pubblicitarie in tempo reale: Server-to-server</li></ul> |
| [!UICONTROL Username] | Le credenziali account selezionate per il flusso di destinazione. |
| [!UICONTROL Segments] | Il numero di segmenti che vengono attivati in questa destinazione. |
| [!UICONTROL Created] | Data e ora UTC alla quale è stato creato il flusso di attivazione per la destinazione. |
| [!UICONTROL Status] | `Active` o `Inactive`. Indica se i dati sono attualmente attivati per questa destinazione. Per modificare lo stato, consultate [Disattivazione](/help/rtcdp/destinations/activate-destinations.md#disable-activation). |

Fai clic su una riga di destinazione per visualizzare ulteriori informazioni sulla destinazione nella barra a destra.

![Fare clic sulla riga di destinazione](/help/rtcdp/destinations/assets/click-destination-row.png)

Selezionate il nome di destinazione per visualizzare informazioni sui segmenti attivati per questa destinazione. Fai clic **[!UICONTROL Edit activation]** per modificare o aggiungere i segmenti che vengono inviati a questa destinazione.

## [!UICONTROL Accounts] {#accounts}

Nella **[!UICONTROL Accounts]** scheda è possibile ottenere ulteriori informazioni sulle connessioni stabilite con diverse destinazioni. Vedi la tabella seguente per tutte le informazioni che puoi ottenere su ogni destinazione:

![Scheda Account](/help/rtcdp/destinations/assets/accounts-tab.png)

| Elemento | Descrizione |
---------|----------
| [!UICONTROL Platform] | Destinazione per la quale è stata impostata la connessione. |
| [!UICONTROL Connection Type] | Rappresenta il tipo di connessione al bucket di archiviazione o alla destinazione. <ul><li>Per le destinazioni di e-mail marketing: Può essere S3 o FTP.</li><li>Per le destinazioni pubblicitarie in tempo reale: Server-to-server</li><li>Per  destinazioni di archiviazione cloud Amazon S3: Chiave di accesso </li><li>Per le destinazioni di archiviazione cloud SFTP: Autenticazione di base per SFTP</li></ul> |
| [!UICONTROL Username] | Nome utente selezionato nella procedura guidata [di destinazione di](/help/rtcdp/destinations/email-marketing-destinations.md#connect-destination)connessione. |
| [!UICONTROL Data Flows] | Rappresenta il numero di flussi di destinazione univoci con esito positivo collegati alle informazioni di base create per una destinazione. |
| [!UICONTROL Authorized] | Data in cui è stata autorizzata la connessione a questa destinazione. |
| [!UICONTROL Status] | `Active` o `Inactive`. Indica se i dati sono attualmente attivati per questa destinazione. Per modificare lo stato, consultate [Disattivazione](/help/rtcdp/destinations/activate-destinations.md#disable-activation). |

## [!UICONTROL System View] {#system-view}

Nella **[!UICONTROL System View]** scheda viene visualizzata una rappresentazione grafica dei flussi di attivazione impostati nella piattaforma dati cliente in tempo reale.

![Data-flows1](/help/rtcdp/destinations/assets/data-flows1.png)

Selezionate una delle destinazioni visualizzate sulla pagina e premete **[!UICONTROL View flows]** per visualizzare le informazioni su tutte le connessioni configurate per ciascuna destinazione.

![Data-flows2](/help/rtcdp/destinations/assets/data-flows2.png)