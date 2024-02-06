---
solution: Experience Platform
title: Guida dell’interfaccia utente del servizio di segmentazione
description: Scopri come creare e gestire tipi di pubblico e definizioni di segmenti nell’interfaccia utente di Adobe Experience Platform.
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
source-git-commit: c6d471d7bb8cb9d5e376cc49c9c89c39e663d7f9
workflow-type: tm+mt
source-wordcount: '3933'
ht-degree: 3%

---

# Guida dell’interfaccia utente di Segmentation Service

[!DNL Adobe Experience Platform Segmentation Service] fornisce un’interfaccia utente per la creazione e la gestione dei tipi di pubblico e delle definizioni dei segmenti.

## Introduzione

L’utilizzo dei tipi di pubblico e delle definizioni dei segmenti richiede una comprensione dei vari [!DNL Experience Platform] servizi coinvolti nella segmentazione. Prima di leggere questa guida utente, consulta la documentazione dei seguenti servizi:

- [[!DNL Segmentation Service]](../home.md): [!DNL Segmentation Service] consente di segmentare i dati memorizzati in [!DNL Experience Platform] che si riferisce a singoli utenti (come clienti, potenziali clienti, utenti o organizzazioni) in gruppi più piccoli.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): consente la creazione di profili cliente collegando le identità da diverse origini dati acquisite in [!DNL Platform].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Platform] organizza i dati sull’esperienza del cliente. Per utilizzare al meglio la segmentazione, assicurati che i dati vengano acquisiti come profili ed eventi in base alla [best practice per la modellazione dei dati](../../xdm/schema/best-practices.md).

Devi inoltre comprendere due termini chiave utilizzati in questo documento e la loro differenza:

- **Pubblico**: un insieme di persone che condividono comportamenti e/o caratteristiche simili. Questa raccolta di persone può essere generata da Adobe Experience Platform utilizzando le definizioni dei segmenti o la composizione del pubblico (pubblico generato da Platform) oppure da fonti esterne, come caricamenti personalizzati (pubblico generato esternamente).
- **Definizione del segmento**: regole utilizzate da Adobe Experience Platform per descrivere le caratteristiche o il comportamento chiave di un pubblico target.
- **Segmento**: atto di separazione dei profili in tipi di pubblico.

## Panoramica

Nell’interfaccia utente di Experienci Platform, seleziona **[!UICONTROL Tipi di pubblico]** nel menu di navigazione a sinistra per aprire **[!UICONTROL Panoramica]** scheda che visualizza [!UICONTROL Tipi di pubblico] dashboard.

>[!NOTE]
>
>Se la tua organizzazione non utilizza ancora Platform e non dispone ancora di set di dati di profilo attivi o criteri di unione creati, il [!UICONTROL Tipi di pubblico] dashboard non visibile. Al contrario, [!UICONTROL Panoramica] Nella scheda vengono visualizzati collegamenti e documentazione per aiutarti a iniziare a utilizzare i tipi di pubblico.

### [!UICONTROL Tipi di pubblico] dashboard {#segments-dashboard}

Il **[!UICONTROL Tipi di pubblico]** la dashboard illustra le metriche chiave relative ai dati sul pubblico della tua organizzazione.

Per ulteriori informazioni, visita [guida della dashboard di audiences](../../dashboards/guides/audiences.md).

![Viene visualizzato il dashboard del pubblico. Mostra vari widget, tra cui la dimensione del pubblico, i profili per identità, la sovrapposizione delle identità e la tendenza di modifica della dimensione del pubblico.](../../dashboards/images/segments/dashboard-overview.png)

## Sfogliare {#browse}

>[!CONTEXTUALHELP]
>id="platform_segments_browse_churncolumnname"
>title="Abbandono"
>abstract="L’abbandono rappresenta la percentuale di profili che cambiano all’interno di un pubblico rispetto all’ultima esecuzione del processo di segmentazione."

>[!CONTEXTUALHELP]
>id="platform_segments_browse_evaluationmethodcolumnname"
>title="Metodo di valutazione"
>abstract="I metodi di valutazione per i tipi di pubblico includono batch, streaming e Edge."

>[!CONTEXTUALHELP]
>id="platform_segments_browse_addallsegmentstoschedule"
>title="Aggiungi tutti i tipi di pubblico alla pianificazione"
>abstract="Abilita questa opzione per includere tutti i tipi di pubblico valutati utilizzando la segmentazione in batch nell’aggiornamento pianificato giornaliero. Disabilita questa opzione per rimuovere tutti i tipi di pubblico dall’aggiornamento pianificato."

Seleziona la **[!UICONTROL Sfoglia]** per visualizzare un elenco di tutti i tipi di pubblico per la tua organizzazione. Questa vista elenca informazioni sui tipi di pubblico, tra cui il conteggio dei profili, l’origine, la data di creazione, la data dell’ultima modifica, i tag e il raggruppamento.

![Viene visualizzata la schermata Sfoglia. Viene visualizzato un elenco di tutti i tipi di pubblico appartenenti all’organizzazione.](../images/ui/overview/audience-browse.png)

Accanto a ogni pubblico è presente un’icona con i puntini di sospensione. Selezionando questa opzione viene visualizzato un elenco delle azioni rapide disponibili per il pubblico. Questo elenco di azioni è diverso in base all’origine del pubblico.

![Viene visualizzato l’elenco delle azioni rapide per i tipi di pubblico con origine [!UICONTROL Composizione del pubblico].](../images/ui/overview/browse-audience-composition-details.png)

| Azione | Origini | Descrizione |
| ------ | ------- | ----------- |
| [!UICONTROL Modifica] | Servizio di segmentazione | Apre Segment Builder (Generatore di segmenti) per modificare il pubblico. Tieni presente che se il pubblico è stato creato tramite l’API, **non** essere in grado di modificarlo utilizzando Segment Builder (Generatore di segmenti). Per ulteriori informazioni sull’utilizzo del Generatore di segmenti, consulta la sezione [Guida dell’interfaccia utente di Segment Builder](./segment-builder.md). |
| [!UICONTROL Apri composizione] | Composizione del pubblico | Apre la composizione Pubblico per visualizzare il pubblico. Per ulteriori informazioni sulla composizione del pubblico, leggi [guida dell’interfaccia utente per la composizione del pubblico](./audience-composition.md). |
| [!UICONTROL Attiva nella destinazione] | Servizio di segmentazione | Attiva il pubblico in una destinazione. Per informazioni più dettagliate sull’attivazione di un pubblico in una destinazione, consulta la sezione [panoramica sull’attivazione](../../destinations/ui/activation-overview.md). |
| [!UICONTROL Condividi con i partner] | Composizione del pubblico, caricamento personalizzato, servizio di segmentazione | Condivide il pubblico con altri utenti di Platform. Per ulteriori informazioni su questa funzione, leggere [Panoramica di Segment Match](./segment-match/overview.md). |
| [!UICONTROL Gestione tag] | Composizione del pubblico, caricamento personalizzato, servizio di segmentazione | Gestisce i tag definiti dall’utente che appartengono al pubblico. Per ulteriori informazioni su questa funzione, consulta la sezione su [filtraggio e assegnazione di tag](#manage-audiences). |
| [!UICONTROL Sposta nella cartella] | Composizione del pubblico, caricamento personalizzato, servizio di segmentazione | Gestisce la cartella a cui appartiene il pubblico. Per ulteriori informazioni su questa funzione, consulta la sezione su [filtraggio e assegnazione di tag](#manage-audiences). |
| [!UICONTROL Copia] | Composizione del pubblico, caricamento personalizzato, servizio di segmentazione | Duplica il pubblico selezionato. |
| [!UICONTROL Applica etichette di accesso] | Composizione del pubblico, caricamento personalizzato, servizio di segmentazione | Gestisce le etichette di accesso che appartengono al pubblico. Per ulteriori informazioni sulle etichette di accesso, consulta la documentazione su [gestione delle etichette](../../access-control/abac/ui/labels.md). |
| [!UICONTROL Archivia] | Caricamento personalizzato | Archivia il pubblico selezionato. |
| [!UICONTROL Elimina] | Composizione del pubblico, caricamento personalizzato, servizio di segmentazione | Elimina il pubblico selezionato. |
| [!UICONTROL Aggiungi al pacchetto] | Composizione del pubblico, caricamento personalizzato, servizio di segmentazione | Sposta il pubblico da una sandbox all’altra. Per ulteriori informazioni su questa funzione, leggere [guida agli strumenti sandbox](../../sandboxes/ui/sandbox-tooling.md). |

>[!NOTE]
>
> Lo farai **non** essere in grado di eliminare un pubblico utilizzato in un’attivazione di destinazione.

Nella parte superiore della pagina sono presenti opzioni per aggiungere tutti i tipi di pubblico a una pianificazione, importare un pubblico, creare un nuovo pubblico e visualizzare un raggruppamento della frequenza di aggiornamento.

Attivazione/disattivazione **[!UICONTROL Pianifica tutti i tipi di pubblico]** abiliterà la segmentazione pianificata. Ulteriori informazioni sulla segmentazione pianificata sono disponibili nella sezione [sezione segmentazione pianificata di questa guida utente](#scheduled-segmentation).

Selezione **[!UICONTROL Importa pubblico]** consente di importare un pubblico generato esternamente. Per ulteriori informazioni sull’importazione di tipi di pubblico, consulta la sezione su [importazione di un pubblico nella guida utente](#import-audience).

Selezione **[!UICONTROL Creare un pubblico]** ti consente di creare un pubblico. Per ulteriori informazioni sulla creazione di tipi di pubblico, consulta la sezione su [creazione di un pubblico nella guida utente](#create-audience).

![Viene evidenziata la barra di navigazione superiore nella pagina di navigazione del pubblico. Questa barra contiene un pulsante per creare un pubblico e un pulsante per importare un pubblico.](../images/ui/overview/browse-audiences-top.png)

Puoi selezionare **[!UICONTROL Aggiorna riepilogo frequenza]** per visualizzare un grafico a torta che mostra la frequenza di aggiornamento.

![Viene evidenziato il pulsante Aggiorna riepilogo frequenza.](../images/ui/overview/browse-audience-update-frequency-summary.png)

Viene visualizzato il grafico a torta, con una suddivisione dei tipi di pubblico in base alla frequenza di aggiornamento. Il grafico mostra il numero totale di tipi di pubblico al centro. Se passi il cursore del mouse sulle diverse parti del pubblico, viene visualizzato il numero di tipi di pubblico che appartengono a ciascun tipo di frequenza di aggiornamento.

![Viene visualizzato il grafico a torta della frequenza di aggiornamento.](../images/ui/overview/update-frequency-chart.png)

### Personalizza {#customize}

È possibile aggiungere ulteriori campi al [!UICONTROL Sfoglia] pagina selezionando ![icona attributo filtro](../images/ui/overview/filter-attribute.png). Questi campi aggiuntivi includono lo stato del ciclo di vita, la frequenza di aggiornamento, l’ultimo aggiornamento di, la descrizione, creato da ed etichette di accesso.

| Campo | Descrizione |
| ----- | ----------- |
| [!UICONTROL Nome] | Il nome del pubblico. |
| [!UICONTROL Conteggio dei profili] | Il numero totale di profili idonei per il pubblico. |
| [!UICONTROL Origin] | L’origine del pubblico. Indica da dove proviene il pubblico. I valori possibili includono Servizio di segmentazione, Caricamento personalizzato, Composizione del pubblico e Audience Manager. |
| [!UICONTROL Stato del ciclo di vita] | Stato del pubblico. I valori possibili per questo campo includono `Draft`, `Published`, e `Archived`. |
| [!UICONTROL Frequenza di aggiornamento] | Valore che indica la frequenza con cui vengono aggiornati i dati del pubblico. I valori possibili per questo campo includono [!UICONTROL Batch], [!UICONTROL Streaming], [!UICONTROL Bordo], e [!UICONTROL Non pianificato]. |
| [!UICONTROL Ultimo aggiornamento eseguito da] | Nome dell’ultima persona che ha aggiornato il pubblico. |
| [!UICONTROL Creato] | La data e l’ora in UTC in cui è stato creato il pubblico. |
| [!UICONTROL Ultimo aggiornamento] | La data e l’ora, in UTC, in cui il pubblico è stato aggiornato l’ultima volta. |
| [!UICONTROL Tag] | I tag definiti dall’utente che appartengono al pubblico. Ulteriori informazioni su questi tag sono disponibili nella sezione [sezione sui tag](#tags). |
| [!UICONTROL Descrizione] | Descrizione del pubblico. |
| [!UICONTROL Creato da] | Nome della persona che ha creato il pubblico. |
| [!UICONTROL Etichette di accesso] | Le etichette di accesso per il pubblico. Le etichette di accesso consentono di categorizzare set di dati e campi in base ai criteri di utilizzo applicabili a tali dati. Queste etichette possono essere applicate in qualsiasi momento, fornendo flessibilità nella scelta di come gestire i dati. Per ulteriori informazioni sulle etichette di accesso, consulta la documentazione su [gestione delle etichette](../../access-control/abac/ui/labels.md). |
| [!UICONTROL Suddividi] | Il raggruppamento dello stato del profilo per il pubblico. Di seguito è riportata una descrizione più dettagliata del raggruppamento dello stato del profilo. |

Se è selezionato il raggruppamento, la visualizzazione mostra un grafico a barre che illustra la percentuale di profili che appartengono a ciascuno dei seguenti stati di profilo calcolati: [!UICONTROL Realizzato], [!UICONTROL Esistente], e [!UICONTROL Uscita]. Inoltre, la suddivisione mostrata nella [!UICONTROL Sfoglia] Questa è la suddivisione più accurata dello stato di definizione del segmento. Se questo numero è diverso da quello riportato sulla [!UICONTROL Panoramica] , è necessario utilizzare i numeri della scheda [!UICONTROL Sfoglia] come fonte corretta di informazioni, poiché il [!UICONTROL Panoramica] i numeri di tabulazione vengono aggiornati solo una volta al giorno.

| Stato | Descrizione |
| ------ | ----------- |
| [!UICONTROL Realizzato] | Numero di profili che **qualificato** per il segmento nelle ultime 24 ore dall’esecuzione dell’ultimo processo di segmentazione batch. |
| [!UICONTROL Esistente] | Numero di profili che **rimasto** nel segmento nelle ultime 24 ore dall’esecuzione dell’ultimo processo di segmentazione batch. |
| [!UICONTROL Uscita] | Numero di profili che **uscita** il segmento nelle ultime 24 ore dall’ultima esecuzione del processo di segmentazione batch. |

Dopo aver selezionato i campi da visualizzare, è possibile ridimensionare anche la larghezza delle colonne visualizzate. Per eseguire questa operazione, trascina l’area tra le colonne oppure seleziona la ![icona freccia](../images/ui/overview/arrow-icon.png) della colonna da ridimensionare, seguita da **[!UICONTROL Ridimensiona colonna]**.

![Viene evidenziato il pulsante Ridimensiona colonna.](../images/ui/overview/browse-audience-resize-column.png)

### Filtraggio, cartelle e assegnazione tag {#manage-audiences}

Per migliorare l’efficienza del lavoro, puoi cercare i tipi di pubblico esistenti, aggiungere tag definiti dall’utente ai tipi di pubblico, inserire i tipi di pubblico nelle cartelle e filtrare quelli visualizzati.

**Ricerca** {#search}

Puoi cercare i tipi di pubblico esistenti in fino a 9 lingue diverse con [!DNL Unified Search].

Da utilizzare [!DNL Unified Search], aggiungi il termine che desideri cercare nella barra di ricerca evidenziata.

![La barra di ricerca viene evidenziata.](../images/ui/overview/browse-audience-search.png)

Per ulteriori informazioni su [!DNL Unified Search], incluse le funzionalità supportate, leggere [Documentazione di Unified Search](https://experienceleague.adobe.com/docs/core-services/interface/services/search-experience-cloud.html).

**Tag** {#tags}

Puoi aggiungere tag definiti dall’utente per descrivere, trovare e gestire meglio i tipi di pubblico.

Per aggiungere un tag, seleziona **[!UICONTROL Gestione tag]** sul pubblico a cui desideri assegnare il tag.

![Il [!UICONTROL Gestione tag] viene selezionato per un pubblico specificato.](../images/ui/overview/browse-manage-tags.png)

Il **[!UICONTROL Gestione tag]** viene visualizzato popover. In questo popover è possibile selezionare un tag categorizzato o un tag non categorizzato.

| Tipo di tag | Descrizione |
| -------- | ----------- |
| Categorizzato | Tag creato e gestito dagli amministratori dell’organizzazione. |
| Non categorizzato | Un tag creato all’interno del [!UICONTROL Gestione tag] popover. Chiunque può creare o gestire questi tipi di tag. |

![Il [!UICONTROL Gestione tag] viene visualizzato popover. Vengono evidenziate le opzioni per scegliere una categoria o una non categorizzata.](../images/ui/overview/create-tag.png)

Dopo aver aggiunto al pubblico tutti i tag che desideri allegare, seleziona **[!UICONTROL Salva]**.

![Il giorno [!UICONTROL Gestione tag] a comparsa, i tag aggiunti vengono evidenziati.](../images/ui/overview/created-tags.png)

Per ulteriori informazioni sulla creazione e la gestione dei tag, consulta [Guida alla gestione dei tag](../../administrative-tags/ui/managing-tags.md).

**Cartelle** {#folders}

Puoi inserire i tipi di pubblico all’interno delle cartelle per una migliore gestione dell’audience.

Per spostare un pubblico in una cartella, seleziona **[!UICONTROL Sposta nella cartella]** sul pubblico che desideri spostare.

![Il [!UICONTROL Sposta nella cartella] viene selezionato per un pubblico specifico.](../images/ui/overview/browse-move-to-folder.png)

Il **Sposta pubblico in cartella** viene visualizzato popover. Seleziona la cartella in cui desideri spostare il pubblico, quindi fai clic su **[!UICONTROL Salva]**.

![Viene visualizzato il popover Sposta pubblico in cartella. Viene evidenziata la cartella in cui verrà spostato il pubblico.](../images/ui/overview/move-to-folder.png)

Una volta che il pubblico si trova in una cartella, puoi scegliere di visualizzare solo i tipi di pubblico che appartengono a una cartella specifica.

![Vengono visualizzati i tipi di pubblico che appartengono a una cartella specifica.](../images/ui/overview/browse-folders.png)

**Filtro** {#filter}

Puoi anche filtrare i tipi di pubblico, in base a diverse impostazioni.

Per filtrare i tipi di pubblico disponibili, seleziona ![icona filtro](../images/ui/overview/filter-icon.png).

![Viene visualizzata la pagina Sfoglia pubblico, con l’icona del filtro evidenziata.](../images/ui/overview/browse-select-filter.png)

Viene visualizzato l’elenco dei filtri disponibili.

| Filtro | Descrizione |
| ------ | ----------- |
| [!UICONTROL Origin] | Consente di filtrare in base all’origine del pubblico. Le opzioni disponibili includono Segmentation Service (Servizio di segmentazione), Custom upload (Caricamento personalizzato), Audience composition (Composizione pubblico) e Audienci Manager. |
| [!UICONTROL Ha qualsiasi tag] | Consente di filtrare per tag. Puoi scegliere tra **[!UICONTROL Ha qualsiasi tag]** e **[!UICONTROL Ha tutti i tag]**. Quando **[!UICONTROL Ha qualsiasi tag]** è selezionato, i tipi di pubblico filtrati includeranno **qualsiasi** dei tag aggiunti. Quando **[!UICONTROL Ha tutti i tag]** è selezionato, i tipi di pubblico filtrati devono includere **tutto** dei tag aggiunti. |
| [!UICONTROL Stato del ciclo di vita] | Consente di filtrare in base allo stato del ciclo di vita del pubblico. Le opzioni disponibili includono [!UICONTROL Attivo], [!UICONTROL Archiviato], [!UICONTROL Eliminato], [!UICONTROL Bozza], [!UICONTROL Inattivo], e [!UICONTROL Pubblicato]. |
| [!UICONTROL Frequenza di aggiornamento] | Consente di filtrare in base alla frequenza di aggiornamento del pubblico. Le opzioni disponibili includono [!UICONTROL Pianificato], [!UICONTROL Continuo], e [!UICONTROL On-demand]. |
| [!UICONTROL Creato da] | Consente di filtrare in base alla persona che ha creato il pubblico. |
| [!UICONTROL Data di creazione] | Consente di filtrare in base alla data di creazione del pubblico. Puoi scegliere un intervallo di date da filtrare al momento della creazione del pubblico. |
| [!UICONTROL Data di modifica] | Consente di filtrare in base all’ultima data modificata del pubblico. Puoi scegliere un intervallo di date per filtrare quando il pubblico è stato modificato l’ultima volta. |

![I filtri disponibili vengono visualizzati ed evidenziati nella pagina Sfoglia pubblico.](../images/ui/overview/filter-audiences.png)

### Dettagli del pubblico {#audience-details}

Per visualizzare ulteriori dettagli su un pubblico specifico, seleziona il nome di un pubblico in **[!UICONTROL Sfoglia]** scheda.

Viene visualizzata la pagina dei dettagli del pubblico. In alto è riportato un riepilogo del pubblico, informazioni sulle dimensioni del pubblico qualificato e le destinazioni per le quali il segmento viene attivato.

![Viene visualizzata la pagina dei dettagli del pubblico. Vengono evidenziate le schede Riepilogo pubblico, Totale pubblico e Destinazioni attivate.](../images/ui/overview/audience-details-summary.png)

**Riepilogo del pubblico** {#segment-summary}

Il **[!UICONTROL Riepilogo del pubblico]** fornisce informazioni quali ID, nome, descrizione, origine e dettagli degli attributi.

Inoltre, puoi attivare il pubblico su una destinazione, applicare etichette di accesso o modificare/aggiornare il pubblico.

Selezione **[!UICONTROL Attiva nella destinazione]** consente di attivare il pubblico in una destinazione. Per informazioni più dettagliate sull’attivazione di un pubblico in una destinazione, consulta la sezione [panoramica sull’attivazione](../../destinations/ui/activation-overview.md).

![Viene evidenziato il pulsante Attiva nella destinazione.](../images/ui/overview/audience-details-activate.png)

Selezione **[!UICONTROL Applica etichette di accesso]** consente di gestire le etichette di accesso che appartengono al pubblico. Per ulteriori informazioni sulle etichette di accesso, consulta la documentazione su [gestione delle etichette](../../access-control/abac/ui/labels.md).

![Viene evidenziato il pulsante Applica etichette di accesso.](../images/ui/overview/audience-details-access-labels.png)

>[!BEGINTABS]

>[!TAB Composizione del pubblico]

![Viene visualizzata la pagina dei dettagli del pubblico, con [!UICONTROL Apri composizione] pulsante evidenziato.](../images/ui/overview/audience-details-open-composition.png)

Selezione **[!UICONTROL Apri composizione]** consente di visualizzare il pubblico in Composizione pubblico. Per ulteriori informazioni sulla composizione del pubblico, leggi [Guida dell’interfaccia utente di Audience Composition](./audience-composition.md).

>[!TAB Caricamento personalizzato]

![Viene visualizzata la pagina dei dettagli del pubblico, con [!UICONTROL Aggiorna pubblico] pulsante evidenziato.](../images/ui/overview/audience-details-update-audience.png)

Selezione **[!UICONTROL Aggiorna pubblico]** consente di ricaricare un pubblico generato esternamente. Per ulteriori informazioni sull’importazione di un pubblico generato esternamente, consulta la sezione su [importazione di un pubblico](#import-audience).

>[!TAB Servizio di segmentazione]

![Viene visualizzata la pagina dei dettagli del pubblico, con [!UICONTROL Modifica pubblico] pulsante evidenziato.](../images/ui/overview/audience-details-edit-audience.png)

Selezione **[!UICONTROL Modifica pubblico]** consente di modificare il pubblico nel Generatore di segmenti. Per informazioni più dettagliate sull&#39;utilizzo di [!DNL Segment Builder] Workspace, leggi il [[!DNL Segment Builder] guida utente](./segment-builder.md).

>[!ENDTABS]

Selezione **[!UICONTROL Modifica proprietà]** consente di modificare i dettagli di base del pubblico, come il nome, la descrizione e i tag.

![](../images/ui/overview/audience-details-edit-properties.png)

**Totale pubblico** {#audience-total}

Il **[!UICONTROL Totale pubblico]** mostra il numero totale di profili idonei per il pubblico.

Le stime vengono generate utilizzando una dimensione campione dei dati di campionamento di quel giorno. Se nell’archivio dei profili sono presenti meno di 1 milione di entità, viene utilizzato l’intero set di dati; per un numero di entità compreso tra 1 e 20 milioni, vengono utilizzate 1 milione di entità e per più di 20 milioni di entità, viene utilizzato il 5% del totale delle entità. Ulteriori informazioni sulla generazione delle stime sono disponibili nella sezione [sezione generazione della stima](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) dell’esercitazione sulla creazione di tipi di pubblico.

**Destinazioni attivate** {#activated-destinations}

Il **[!UICONTROL Destinazioni attivate]** mostra le destinazioni per le quali è attivato questo pubblico.

>[!NOTE]
>
> Le destinazioni sono una funzione disponibile con [!DNL Adobe Real-Time Customer Data Platform]e ti consentono di esportare dati su piattaforme esterne. Per ulteriori informazioni sulle destinazioni, consulta [panoramica sulle destinazioni](../../destinations/home.md). Per informazioni su come attivare un segmento in una destinazione, consulta [panoramica sull’attivazione](../../destinations/ui/activation-overview.md).

**Esempi di profilo** {#profile-samples}

Di seguito è riportato un campionamento dei profili idonei per il segmento, con informazioni dettagliate che includono [!DNL Profile] ID, nome, cognome e indirizzo e-mail personale.

Il modo in cui viene attivato il campionamento dei dati dipende dal metodo di acquisizione.

Per l’acquisizione batch, l’archivio profili viene analizzato automaticamente ogni quindici minuti per verificare se un nuovo batch è stato correttamente acquisito dall’ultima esecuzione del processo di campionamento. In questo caso, l’archivio profili viene successivamente analizzato per verificare se è stata registrata una modifica di almeno il 5% nel numero di record. Se queste condizioni vengono soddisfatte, viene attivato un nuovo processo di campionamento.

Per l’acquisizione in streaming, l’archivio profili viene analizzato automaticamente ogni ora per verificare se si è verificata una modifica di almeno il 5% nel numero di record. Se questa condizione viene soddisfatta, viene attivato un nuovo processo di campionamento.

La dimensione del campione della scansione dipende dal numero complessivo di entità nell’archivio profili. Queste dimensioni di esempio sono rappresentate nella tabella seguente:

| Entità nell’archivio profili | Dimensione campione |
| ------------------------- | ----------- |
| Meno di 1 milione | Set di dati completo |
| Da 1 a 20 milioni | 1 milione |
| Oltre 20 milioni | 5% del totale |

Informazioni più dettagliate su ciascuno [!DNL Profile] può essere visualizzato selezionando la [!DNL Profile] ID Per ulteriori informazioni sui dettagli di un profilo, consulta [[!DNL Real-Time Customer Profile] guida utente](../../profile/ui/user-guide.md#profile-detail).

![Vengono evidenziati i profili di esempio per il pubblico. Le informazioni di profilo di esempio includono l’ID profilo, il nome, il cognome e l’e-mail della persona.](../images/ui/overview/audience-details-profiles.png)

### Creazione di un pubblico {#create-audience}

Puoi selezionare **[!UICONTROL Creare un pubblico]** per creare un pubblico.

![Nella pagina di navigazione del pubblico, viene evidenziato il pulsante Crea pubblico.](../images/ui/overview/browse-create-audience.png)

Viene visualizzato un popover che consente di scegliere se comporre un pubblico o creare regole.

![Un popover che visualizza i due tipi di pubblico che puoi creare.](../images/ui/overview/create-audience-type.png)

**Composizione del pubblico** {#audience-composition}

Selezione **[!UICONTROL Componi tipi di pubblico]** ti porta a Composizione del pubblico. Questa area di lavoro offre controlli intuitivi per la creazione e la modifica di tipi di pubblico, ad esempio il trascinamento della selezione utilizzato per rappresentare azioni diverse. Per ulteriori informazioni sulla creazione di tipi di pubblico, consulta [Guida alla composizione del pubblico](./audience-composition.md).

![Viene visualizzata l’area di lavoro Composizione pubblico.](../images/ui/overview/audience-composition.png)

**Generatore di segmenti** {#segment-builder}

Selezione **[!UICONTROL Genera regola]** ti porta al Generatore di segmenti. Questa area di lavoro fornisce controlli intuitivi per la creazione e la modifica delle definizioni dei segmenti, ad esempio le tessere trascinate utilizzate per rappresentare le proprietà dei dati. Per ulteriori informazioni sulla creazione delle definizioni dei segmenti, consulta [Guida al Generatore di segmenti](./segment-builder.md)

![Viene visualizzata l’area di lavoro del Generatore di segmenti.](../images/ui/overview/segment-builder.png)

### Importazione di un pubblico {#import-audience}

Puoi selezionare **[!UICONTROL Importa pubblico]** per importare un pubblico generato esternamente.

![Nella pagina di navigazione del pubblico, il pulsante Importa pubblico è evidenziato.](../images/ui/overview/browse-import-audience.png)

Il **[!UICONTROL Importa CSV pubblico]** viene visualizzato workflow. Puoi selezionare un file CSV da importare come pubblico generato esternamente.

![In [!UICONTROL Importa CSV pubblico] flusso di lavoro, [!UICONTROL Trascinare i file] viene evidenziata, mostrando dove puoi caricare il pubblico generato esternamente.](../images/ui/overview/import-audience-csv.png)

>[!NOTE]
>
>Il pubblico generato esterno **deve** essere in formato CSV, avere **massimo** di 25 colonne e deve essere inferiore a 1 GB.

Dopo aver selezionato il file CSV da importare, viene visualizzato un elenco di dati di esempio per questo pubblico generato esternamente. Dopo aver verificato la correttezza dei dati di esempio, seleziona **[!UICONTROL Successivo]**.

![Vengono visualizzati dati di esempio per il pubblico generato esternamente.](../images/ui/overview/import-audience-sample-data.png)

Il **[!UICONTROL Dettagli del pubblico]** viene visualizzata. Puoi aggiungere informazioni sul pubblico, tra cui nome, descrizione, identità primaria e valore dello spazio dei nomi dell’identità.

Quando importi il pubblico generato esternamente, devi selezionare una delle colonne da usare come campo di identità principale e specificare il valore dello spazio dei nomi. Si prega di notare che tutti i campi rimanenti verranno considerati **attributi payload**. Questi attributi vengono considerati **non durevole**, poiché saranno associate a questo pubblico solo a scopo di personalizzazione e sono **non** connesso al profilo.

![Il [!UICONTROL Dettagli del pubblico] viene visualizzata.](../images/ui/overview/import-audience-audience-details.png)

Dopo aver inserito i dettagli del pubblico, seleziona **[!UICONTROL Successivo]**.

![Il [!UICONTROL Successivo] viene evidenziato sulla [!UICONTROL Dettagli del pubblico] pagina.](../images/ui/overview/import-audience-filled-details.png)

Il **[!UICONTROL Revisione]** viene visualizzata. Puoi rivedere i dettagli del pubblico appena importato generato esternamente.

![Il [!UICONTROL Revisione] viene visualizzata una pagina che mostra i dettagli del pubblico generato esternamente appena importato.](../images/ui/overview/import-audience-review-details.png)

Dopo aver confermato la correttezza dei dettagli, seleziona **[!UICONTROL Fine]** per importare in Adobe Experience Platform il pubblico generato esternamente.

>[!IMPORTANT]
>
>Per impostazione predefinita, i tipi di pubblico generati esternamente hanno una scadenza dei dati di 30 giorni. La scadenza dei dati viene reimpostata se il pubblico viene aggiornato o modificato in qualsiasi modo.
>
>Inoltre, se il pubblico generato esternamente contiene informazioni sensibili e/o relative all’assistenza sanitaria, **deve** applica le etichette di utilizzo dei dati necessarie prima di attivarla in qualsiasi destinazione. Per ulteriori informazioni sull’applicazione delle etichette di utilizzo dei dati, consulta la documentazione su [gestione delle etichette](../../access-control/abac/ui/labels.md).

## Segmentazione pianificata {#scheduled-segmentation}

Una volta creati i tipi di pubblico, puoi valutarli tramite valutazione on-demand o pianificata (continua). Valutazione significa spostamento [!DNL Real-Time Customer Profile] dati attraverso processi di segmentazione per produrre tipi di pubblico corrispondenti. Una volta creati, i tipi di pubblico vengono salvati e memorizzati in modo che possano essere esportati utilizzando [!DNL Experience Platform] API.

La valutazione on-demand comporta l’utilizzo dell’API per eseguire valutazioni e generare tipi di pubblico in base alle esigenze, mentre la valutazione pianificata (nota anche come &quot;segmentazione pianificata&quot;) consente di creare una pianificazione ricorrente per valutare i tipi di pubblico in un momento specifico (al massimo, una volta al giorno).

### Abilita segmentazione pianificata {#enable-scheduled-segmentation}

Abilitare i tipi di pubblico per la valutazione pianificata può essere fatto utilizzando l’interfaccia utente o l’API. Nell’interfaccia utente, torna a **[!UICONTROL Sfoglia]** scheda in **[!UICONTROL Tipi di pubblico]** e attivare **[!UICONTROL Pianifica tutti i tipi di pubblico]**. In questo modo tutti i tipi di pubblico verranno valutati in base alla pianificazione impostata dall’organizzazione.

>[!NOTE]
>
>La valutazione pianificata può essere abilitata per le sandbox con un massimo di cinque (5) criteri di unione per [!DNL XDM Individual Profile]. Se nell’organizzazione sono presenti più di cinque criteri di unione per [!DNL XDM Individual Profile] in un singolo ambiente sandbox non puoi utilizzare la valutazione pianificata.

Al momento è possibile creare pianificazioni solo utilizzando l’API. Per i passaggi dettagliati sulla creazione, la modifica e l’utilizzo delle pianificazioni utilizzando l’API, segui il tutorial per valutare e accedere ai risultati della segmentazione, in particolare la sezione su [valutazione pianificata tramite l’API](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![L’opzione Pianifica tutti i tipi di pubblico è evidenziata nella pagina Sfoglia pubblico.](../images/ui/overview/browse-audiences-scheduled.png)

## Composizioni {#compositions}

Seleziona la **[!UICONTROL Composizioni]** per visualizzare un elenco di tutti i tipi di pubblico generati tramite la Composizione del pubblico per la tua organizzazione.

![Un elenco di tipi di pubblico creati in Composizione pubblico per la tua organizzazione.](../images/ui/overview/compositions.png)

Per impostazione predefinita, questa visualizzazione elenca informazioni sui tipi di pubblico, tra cui nome, stato, data di creazione, data di creazione, data dell’ultimo aggiornamento e data dell’ultimo aggiornamento di.

È possibile selezionare ![Personalizza tabella](../images/ui/overview/customize-table.png) per modificare i campi visualizzati.

![Viene evidenziato il pulsante Personalizza tabella. Selezionando questo pulsante puoi personalizzare i campi visualizzati nella pagina Composizioni pubblico.](../images/ui/overview/compositions-select-customize-table.png)

Viene visualizzato un popover che elenca tutti i campi che possono essere visualizzati nella tabella.

![Attributi che possono essere visualizzati per la sezione Composizione.](../images/ui/overview/compositions-customize-table.png)

| Campo | Descrizione |
| ----- | ----------- | 
| [!UICONTROL Nome] | Il nome del pubblico. |
| [!UICONTROL Stato] | Stato del pubblico. I valori possibili per questo campo includono `Draft`, `Published`, e `Archived`. |
| [!UICONTROL Creato] | L’ora e la data di creazione del pubblico. |
| [!UICONTROL Creato da] | Nome della persona che ha creato il pubblico. |
| [!UICONTROL Aggiornato] | Ora e data dell’ultimo aggiornamento del pubblico. |
| [!UICONTROL Aggiornato da] | Nome dell’ultima persona che ha aggiornato il pubblico. |

Per visualizzare la modalità di composizione del pubblico, seleziona il nome di un pubblico all’interno del [!UICONTROL Tipi di pubblico] scheda.

Viene visualizzata la pagina Composizione pubblico con i blocchi predefiniti che compongono il pubblico. Per ulteriori dettagli su come utilizzare Composizione del pubblico, leggi [Guida dell’interfaccia utente di Audience Composition](./audience-composition.md).

## Segmentazione in streaming {#streaming-segmentation}

La segmentazione in streaming è la capacità di eseguire la segmentazione su [!DNL Platform] quasi in tempo reale, concentrandosi sulla ricchezza dei dati. Con la segmentazione in streaming, la qualificazione per la segmentazione ora avviene quando i dati arrivano in [!DNL Platform], riducendo la necessità di pianificare ed eseguire processi di segmentazione.

Ulteriori informazioni sulla segmentazione dello streaming sono disponibili nella sezione [guida utente sulla segmentazione in streaming](./streaming-segmentation.md).

>[!NOTE]
>
>Affinché la segmentazione in streaming funzioni, devi abilitare la segmentazione pianificata per l’organizzazione. Per informazioni dettagliate sull’abilitazione della segmentazione pianificata, consulta [la sezione segmentazione streaming in questa guida utente](#scheduled-segmentation).

## Segmentazione Edge {#edge-segmentation}

La segmentazione Edge consente di valutare i tipi di pubblico in Platform istantaneamente al limite, abilitando casi di utilizzo di personalizzazione della pagina stessa e successiva.

Ulteriori informazioni sulla segmentazione Edge sono disponibili nella sezione [guida dell’interfaccia utente per la segmentazione Edge](./edge-segmentation.md)

## Violazioni dei criteri

>[!NOTE]
>
>Le violazioni dei criteri si applicano solo se stai creando un pubblico assegnato a una destinazione.

Una volta completata la creazione del pubblico, questo verrà analizzato da Governance dei dati di Adobe Experience Platform per garantire che non vi siano violazioni dei criteri all’interno del pubblico. Consulta la [Panoramica sulla governance dei dati](../../data-governance/home.md) per ulteriori informazioni.

![Vengono visualizzate le violazioni dei criteri per il pubblico.](../images/ui/overview/audience-dule-policy-violations.png)

## Passaggi successivi e risorse aggiuntive {#next-steps}

Il [!DNL Segmentation Service] L’interfaccia utente offre un flusso di lavoro avanzato che consente di creare tipi di pubblico commerciabili da [!DNL Real-Time Customer Profile] dati.

Per ulteriori informazioni su [!DNL Segmentation Service], continua a leggere la documentazione. Per scoprire come utilizzare il [!DNL Segmentation Service] API, leggi le [[!DNL Segmentation Service] guida per sviluppatori](../api/overview.md).
