---
title: Area di lavoro Destinazioni
seo-title: Area di lavoro Destinazioni
description: In Adobe Real-time Customer Data Platform, seleziona Destinazioni dalla barra di navigazione a sinistra per accedere all'area di lavoro delle destinazioni.
seo-description: In Adobe Real-time Customer Data Platform, seleziona Destinazioni dalla barra di navigazione a sinistra per accedere all'area di lavoro delle destinazioni.
translation-type: tm+mt
source-git-commit: 132bc9787a86045adba559c769b02927a6045b17

---


# Area di lavoro Destinazioni {#destinations-workspace}

In Adobe Real-time Customer Data Platform, seleziona **Destinazioni** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro Destinazioni.

L&#39;area di lavoro Destinazioni è composta da quattro sezioni: **Catalogo**, **Sfoglia**, **Account** e Flussi **** dati, descritte nelle sezioni seguenti.

![Destinazioni-panoramica](/help/rtcdp/destinations/assets/destinations-overview.png)

## Catalogo {#catalog}

Nella scheda **[!UICONTROL Catalogo]** è visualizzato un elenco di tutte le destinazioni offerte da Adobe, a cui potete inviare i dati. Selezionate una destinazione nel catalogo per aprire la barra laterale destra. Qui potete impostare una connessione alla destinazione (destinazione **di** Connect) o ottenere informazioni più dettagliate su ciascuna destinazione visualizzando la documentazione (documentazione **** Visualizza).

![Opzioni del catalogo di destinazione](/help/rtcdp/destinations/assets/destination-ui-catalog-options.png)

Per ulteriori informazioni sulle categorie di destinazione e informazioni su ciascuna destinazione, consulta Catalogo [](/help/rtcdp/destinations/destinations-catalog.md)di destinazione.

## Sfoglia {#browse}

Nella scheda **[!UICONTROL Sfoglia]** sono visualizzate le destinazioni con le quali è stata stabilita una connessione. Le destinazioni con l&#39;attivazione dell&#39;opzione attivata/disattivata impostano la destinazione su attiva e viceversa. Per visualizzare le destinazioni in cui i dati scorrono, seleziona **Segmenti > Sfoglia** e seleziona un segmento da esaminare. Per tutte le informazioni fornite per ciascuna destinazione, consultate la tabella seguente nella scheda Sfoglia:

![Scheda Sfoglia](/help/rtcdp/destinations/assets/browse-tab.png)

| Elemento | Descrizione |
---------|----------
| Nome destinazione | Nome fornito per il flusso di attivazione a questa destinazione. |
| Destinazione | La piattaforma di destinazione selezionata per il flusso di attivazione. |
| Creato | Data e ora UTC alla quale è stato creato il flusso di attivazione per la destinazione. |
| Tipo di connessione | *Solo* per le destinazioni di e-mail marketing. Rappresenta il tipo di connessione al bucket di archiviazione. Può essere S3 o FTP. |
| Nome utente | Le credenziali account selezionate per il flusso di destinazione. |
| Segmenti | Il numero di segmenti che vengono attivati in questa destinazione. |
| Stato | `Active` o `Inactive`. Indica se i dati sono attualmente attivati per questa destinazione. Per modificare lo stato, consultate [Disattivazione](/help/rtcdp/destinations/activate-destinations.md#disable-activation). |

Fai clic su una riga di destinazione per visualizzare ulteriori informazioni sulla destinazione nella barra a destra.

![Fare clic sulla riga di destinazione](/help/rtcdp/destinations/assets/click-destination-row.png)

Selezionate il nome di destinazione per visualizzare informazioni sui segmenti attivati per questa destinazione. Fai clic su **[!UICONTROL Modifica attivazione]** per modificare o aggiungere i segmenti che vengono inviati a questa destinazione.

## Account {#accounts}

Nella scheda **[!UICONTROL Account]** è possibile ottenere ulteriori informazioni sulle connessioni stabilite con diverse destinazioni. Vedi la tabella seguente per tutte le informazioni che puoi ottenere su ogni destinazione:

![Scheda Account](/help/rtcdp/destinations/assets/accounts-tab.png)

| Elemento | Descrizione |
---------|----------
| Piattaforma | Destinazione per la quale è stata impostata la connessione. |
| Nome utente | Nome utente selezionato nella procedura guidata [di destinazione di](/help/rtcdp/destinations/email-marketing-destinations.md#connect-destination)connessione. |
| Flussi | Rappresenta il numero di flussi di destinazione univoci con esito positivo collegati alle informazioni di base create per una destinazione. |
| Autorizzato | Data in cui è stata autorizzata la connessione a questa destinazione. |

## Flussi di dati {#data-flows}

La scheda Flussi **[!UICONTROL di]** dati mostra una rappresentazione grafica dei flussi di attivazione impostati nella piattaforma dati cliente in tempo reale.

![Data-flows1](/help/rtcdp/destinations/assets/data-flows1.png)

Seleziona una delle destinazioni visualizzate sulla pagina e premi **[!UICONTROL Visualizza flussi]** per visualizzare informazioni su tutti i flussi di dati impostati per ciascuna destinazione.

![Data-flows2](/help/rtcdp/destinations/assets/data-flows2.png)