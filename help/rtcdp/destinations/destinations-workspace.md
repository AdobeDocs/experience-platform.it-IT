---
title: Area di lavoro Destinazioni
seo-title: Area di lavoro Destinazioni
description: In  Adobe Platform Dati cliente in tempo reale, seleziona Destinazioni dalla barra di navigazione a sinistra per accedere all'area di lavoro delle destinazioni.
seo-description: In  Adobe Platform Dati cliente in tempo reale, seleziona Destinazioni dalla barra di navigazione a sinistra per accedere all'area di lavoro delle destinazioni.
translation-type: tm+mt
source-git-commit: 570c627672439a5ee0f4215b7bf7915ec3dd2bb3
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 1%

---


# Area di lavoro Destinazioni {#destinations-workspace}

In  Adobe Platform Dati cliente in tempo reale, selezionate **[!UICONTROL Destinations]** dalla barra di navigazione a sinistra per accedere all&#39; [!UICONTROL Destinations] area di lavoro.

L’ [!UICONTROL Destinations] area di lavoro è composta da quattro sezioni, **[!UICONTROL Catalog]**, **[!UICONTROL Browse]**, **[!UICONTROL Accounts]** e **[!UICONTROL System View]**, descritte nelle sezioni seguenti.

![Destinazioni-panoramica](/help/rtcdp/destinations/assets/destinations-overview.png)

## [!UICONTROL Catalog] {#catalog}

Nella **[!UICONTROL Catalog]** scheda viene visualizzato un elenco di tutte le destinazioni offerte  Adobe, a cui è possibile inviare i dati.

Utilizzate la funzionalità di ricerca nella pagina per individuare una destinazione o destinazioni di filtro specifiche utilizzando il **[!UICONTROL Categories]** controllo.

Selezionate una destinazione nel catalogo per aprire la barra laterale destra. In questa scheda è possibile impostare una connessione alla destinazione (**[!UICONTROL Connect destination]**), visualizzare le connessioni di destinazione esistenti (**[!UICONTROL Browse destinations]**) o ottenere informazioni più dettagliate su ciascuna destinazione visualizzando la documentazione (**[!UICONTROL View documentation]**).

![Opzioni del catalogo di destinazione](/help/rtcdp/destinations/assets/destination-ui-catalog-options.png)

Per ulteriori informazioni sulle categorie di destinazione e informazioni su ciascuna destinazione, consulta Catalogo [](/help/rtcdp/destinations/destinations-catalog.md)di destinazione.

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

Nella **[!UICONTROL System View]** scheda viene visualizzata una rappresentazione grafica dei flussi di attivazione impostati nell&#39;Platform dati cliente in tempo reale.

![Data-flows1](/help/rtcdp/destinations/assets/data-flows1.png)

Selezionate una delle destinazioni visualizzate sulla pagina e premete **[!UICONTROL View flows]** per visualizzare le informazioni su tutte le connessioni configurate per ciascuna destinazione.

![Data-flows2](/help/rtcdp/destinations/assets/data-flows2.png)