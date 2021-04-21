---
keywords: Experience Platform;home;argomenti popolari;servizio di segmentazione;segmentazione;servizio di segmentazione;guida utente;guida utente;guida utente;guida utente di segmentazione;generatore segmenti;generatore segmenti;realizzato;esistente;esistente; uscita;
solution: Experience Platform
title: Guida all’interfaccia utente del servizio di segmentazione
topic-legacy: ui guide
description: Il servizio di segmentazione di Adobe Experience Platform fornisce un’interfaccia utente per la creazione e la gestione delle definizioni dei segmenti.
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1479'
ht-degree: 0%

---

# Guida all’interfaccia utente del servizio di segmentazione

[!DNL Adobe Experience Platform Segmentation Service] fornisce un’interfaccia utente per la creazione e la gestione delle definizioni dei segmenti.

## Introduzione

Per lavorare con le definizioni dei segmenti è necessario conoscere i vari servizi [!DNL Experience Platform] coinvolti nella segmentazione. Prima di leggere questa guida utente, consulta la documentazione relativa ai seguenti servizi:

- [[!DNL Segmentation Service]](../home.md):  [!DNL Segmentation Service] ti consente di suddividere in gruppi più piccoli i dati archiviati in  [!DNL Experience Platform] relativi a singoli utenti (ad esempio clienti, potenziali clienti, utenti o organizzazioni).
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Consente la creazione di profili cliente tramite il collegamento di identità provenienti da diverse origini dati che vengono acquisite in  [!DNL Platform].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Platform] vengono organizzati i dati sulla customer experience.

È inoltre importante conoscere due termini chiave utilizzati nel presente documento e comprendere la differenza tra questi:
- **Definizione** del segmento: Il set di regole utilizzato per descrivere le caratteristiche o i comportamenti chiave di un pubblico target.
- **Pubblico**: Il set risultante di profili che soddisfano i criteri di una definizione di segmento.

## Panoramica

Nel menu di navigazione [[!DNL Experience Platform] UI](http://platform.adobe.com/), seleziona **[!UICONTROL Segments]** nel menu di navigazione a sinistra per aprire la scheda **[!UICONTROL Overview]** . Questa scheda fornisce collegamenti alla documentazione e ai video per comprendere e iniziare a lavorare con i segmenti.

![](../images/ui/overview/segment-overview.png)

## Sfoglia

Seleziona la scheda **[!UICONTROL Browse]** per visualizzare un elenco di tutte le definizioni di segmenti per la tua organizzazione IMS.

![](../images/ui/overview/segment-browse-all.png)

Questa visualizzazione elenca informazioni sulla definizione del segmento, tra cui suddivisione, abbandono, conteggio dei profili, metodo di valutazione, data di creazione e data dell’ultima modifica.

La suddivisione mostra un grafico a barre che mostra la percentuale di profili che appartengono a ciascuno dei seguenti stati: [!UICONTROL Entered], [!UICONTROL Realized] e [!UICONTROL Exiting].

![](../images/ui/overview/segment-browse-breakdown.png)

| Stato | Descrizione |
| ------ | ----------- |
| Inserito | Un nuovo profilo all’interno del segmento. |
| Realizzato | Un profilo esistente rimasto all’interno del segmento. |
| Uscita | Un profilo esistente che sta lasciando il segmento. |

L’abbandono rappresenta la percentuale di profili che cambiano all’interno di una definizione di segmento rispetto all’ultima esecuzione del processo di segmento, mentre il conteggio del profilo rappresenta il numero totale di profili idonei per il segmento.

Il metodo di valutazione può essere in streaming o batch. I segmenti in streaming vengono valutati costantemente man mano che i dati entrano nel sistema. I segmenti batch vengono valutati in base a una pianificazione impostata.

![](../images/ui/overview/segment-browse-segments.png)

Nella parte superiore della pagina sono disponibili le opzioni per aggiungere tutti i segmenti a una pianificazione e per creare un nuovo segmento.

Attivando **[!UICONTROL Add all segments to schedule]** la segmentazione programmata verrà attivata. Ulteriori informazioni sulla segmentazione pianificata sono disponibili nella sezione [segmentazione pianificata di questa guida utente](#scheduled-segmentation).

Selezionando **[!UICONTROL Create segment]** verrai indirizzato al Generatore di segmenti. Per ulteriori informazioni sulla creazione di segmenti, consulta la sezione su [creazione di un segmento nella guida utente](#create-segment).

![](../images/ui/overview/segment-browse-top.png)

La barra laterale destra contiene informazioni su tutti i segmenti all’interno dell’organizzazione IMS, elencando il numero totale di segmenti, la data dell’ultima valutazione, la data della valutazione successiva e una suddivisione dei segmenti in base al metodo di valutazione.

![](../images/ui/overview/segment-browse-segment-info.png)

Selezionando la riga della definizione del segmento viene fornito un riepilogo della definizione del segmento, incluse le opzioni per modificare o eliminare il segmento, il pubblico qualificato per il segmento, la dimensione totale del pubblico, oltre al nome, alla descrizione, al metodo di valutazione, alla data di creazione e all’ultima data di modifica del segmento.

![](../images/ui/overview/segment-browse-details.png)

## Dettagli della definizione del segmento {#segment-details}

Per visualizzare ulteriori dettagli su una definizione di segmento specifica, seleziona il nome di un segmento nella scheda **[!UICONTROL Browse]** .

Viene visualizzata la pagina dei dettagli del segmento. Nella parte superiore, è presente un riepilogo della definizione del segmento, delle informazioni sulla dimensione del pubblico qualificato e delle destinazioni per le quali il segmento viene attivato.

![](../images/ui/overview/segment-details-summary.png)

### Riepilogo del segmento

La sezione **[!UICONTROL Segment summary]** fornisce informazioni quali ID, nome, descrizione e dettagli degli attributi.

Inoltre, puoi modificare il segmento. Selezionando **[!UICONTROL Edit segment]** potrai accedere al percorso [!DNL Segment Builder]. Per informazioni più dettagliate sull&#39;utilizzo dell&#39;area di lavoro [!DNL Segment Builder], leggere la [[!DNL Segment Builder] guida utente](./segment-builder.md).

### Pubblico totale nel segmento

La sezione **[!UICONTROL Total audience in segment]** mostra il numero totale di profili idonei per il segmento.

Le stime vengono generate utilizzando una dimensione del campione dei dati di esempio del giorno in questione. Se nell’archivio dei profili sono presenti meno di 1 milione di entità, viene utilizzato l’intero set di dati; tra 1 e 20 milioni di entità sono utilizzate 1 milione di entità; e per più di 20 milioni di entità viene utilizzato il 5% del totale delle entità. Ulteriori informazioni sulla generazione delle stime dei segmenti sono disponibili nella sezione [generazione delle stime](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) dell’esercitazione sulla creazione dei segmenti.

### Destinazioni attivate

La sezione **[!UICONTROL Activated destinations]** mostra le destinazioni per le quali questo segmento è attivato.

>[!NOTE]
>
> Le destinazioni sono una funzionalità disponibile con [!DNL Real-time Customer Data Platform] e ti consentono di esportare dati su piattaforme esterne. Per ulteriori informazioni sulle destinazioni, consulta la [panoramica delle destinazioni](../../destinations/home.md). Per scoprire come attivare un segmento a una destinazione, leggi la [guida sull&#39;attivazione dei segmenti a una destinazione](../../destinations/ui/activate-destinations.md).

### Esempi di profilo

Di seguito è riportato un esempio di profili idonei per il segmento, con informazioni dettagliate quali [!DNL Profile] ID, nome, cognome ed e-mail personali.

Il modo in cui viene attivato il campionamento dei dati dipende dal metodo di acquisizione.

Per l’acquisizione batch, l’archivio dei profili viene analizzato automaticamente ogni quindici minuti per verificare se un nuovo batch è stato acquisito correttamente dall’ultima esecuzione del processo di campionamento. In questo caso, l’archivio dei profili viene successivamente analizzato per verificare se vi è stato almeno un cambiamento del 5% nel numero di record. Se queste condizioni vengono soddisfatte, viene attivato un nuovo processo di campionamento.

Per l’acquisizione in streaming, l’archivio dei profili viene analizzato automaticamente ogni ora per verificare se vi è stato almeno un cambiamento del 5% nel numero di record. Se questa condizione viene soddisfatta, viene attivato un nuovo processo di campionamento.

La dimensione del campione della scansione dipende dal numero complessivo di entità nell’archivio dei profili. Le dimensioni dei campioni sono rappresentate nella tabella seguente:

| Entità nell’archivio profili | Dimensione del campione |
| ------------------------- | ----------- |
| Meno di 1 milione | Set di dati completo |
| Da 1 a 20 milioni | 1 milione |
| Oltre 20 milioni | 5% del totale |

Per informazioni più dettagliate su ciascun [!DNL Profile], seleziona l’ID [!DNL Profile] . Per ulteriori informazioni sui dettagli di un profilo, consulta la [[!DNL Real-time Customer Profile] guida utente](../../profile/ui/user-guide.md#profile-detail).

![](../images/ui/overview/segment-details-profiles.png)

## Creazione di un segmento {#create-segment}

Selezionando **[!UICONTROL Create segment]** nell’angolo in alto a destra, si apre l’area di lavoro [!DNL Segment Builder] in cui puoi iniziare a creare una definizione di segmento.

![](../images/ui/overview/segment-browse-create.png)

### [!DNL Segment Builder] workspace

[!DNL Segment Builder] offre un’area di lavoro ricca che consente di interagire con gli elementi  [!DNL Profile] dati. L’area di lavoro fornisce controlli intuitivi per la creazione e la modifica di regole, ad esempio riquadri drag-and-drop utilizzati per rappresentare le proprietà dei dati.

Per informazioni più dettagliate sull&#39;utilizzo dell&#39;area di lavoro [!DNL Segment Builder], leggere la [[!DNL Segment Builder] guida utente](./segment-builder.md).

![](../images/ui/overview/segment-builder.png)

## Segmentazione pianificata {#scheduled-segmentation}

Una volta create le definizioni dei segmenti, puoi valutarle tramite valutazione on-demand o pianificata (continua). Valutazione significa spostare i dati [!DNL Real-time Customer Profile] attraverso le definizioni dei segmenti per produrre i tipi di pubblico corrispondenti. Una volta creati, i tipi di pubblico vengono salvati e memorizzati in modo che possano essere esportati utilizzando le API [!DNL Experience Platform] .

La valutazione su richiesta comporta l’utilizzo dell’API per eseguire valutazioni e generare tipi di pubblico in base alle esigenze, mentre la valutazione pianificata (nota anche come &quot;segmentazione pianificata&quot;) consente di creare una pianificazione periodica per valutare le definizioni dei segmenti in un momento specifico (al massimo una volta al giorno).

### Abilita segmentazione pianificata {#enable-scheduled-segmentation}

Puoi abilitare le definizioni dei segmenti per la valutazione pianificata utilizzando l’interfaccia utente o l’API. Nell’interfaccia utente, torna alla scheda **[!UICONTROL Browse]** in **[!UICONTROL Segments]** e attiva **[!UICONTROL Add all segments to schedule]**. In questo modo tutti i segmenti verranno valutati in base alla pianificazione impostata dall’organizzazione.

>[!NOTE]
>
>La valutazione pianificata può essere abilitata per le sandbox con un massimo di cinque (5) criteri di unione per [!DNL XDM Individual Profile]. Se la tua organizzazione dispone di più di cinque criteri di unione per [!DNL XDM Individual Profile] all’interno di un singolo ambiente sandbox, non potrai utilizzare la valutazione pianificata.

Attualmente le pianificazioni possono essere create solo utilizzando l’API . Per passaggi dettagliati sulla creazione, la modifica e l’utilizzo delle pianificazioni tramite l’API, segui l’esercitazione per valutare e accedere ai risultati dei segmenti, in particolare la sezione sulla [valutazione pianificata utilizzando l’API](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![](../images/ui/overview/segment-browse-scheduled.png)

## Segmentazione streaming {#streaming-segmentation}

La segmentazione in streaming è la capacità di eseguire segmentazione su [!DNL Platform] in tempo quasi reale, concentrandosi sulla ricchezza di dati. Con la segmentazione in streaming, la qualificazione dei segmenti ora avviene quando i dati arrivano in [!DNL Platform], alleviando la necessità di pianificare ed eseguire processi di segmentazione.

Ulteriori informazioni sulla segmentazione in streaming sono disponibili nella [guida utente per la segmentazione in streaming](./streaming-segmentation.md).

>[!NOTE]
>
>Affinché la segmentazione in streaming funzioni, è necessario abilitare la segmentazione pianificata per l’organizzazione. Per informazioni dettagliate sull&#39;abilitazione della segmentazione pianificata, fai riferimento alla sezione [segmentazione in streaming in questa guida utente](#scheduled-segmentation).

## Segmentazione dei bordi {#edge-segmentation}

La segmentazione dei bordi è la capacità di valutare istantaneamente i segmenti in Platform sul bordo, abilitando casi d’uso di personalizzazione della pagina e della stessa pagina.

Ulteriori informazioni sulla segmentazione dei bordi sono disponibili nella [guida dell&#39;interfaccia utente per la segmentazione dei bordi](./edge-segmentation.md)

## Violazioni dei criteri

>[!NOTE]
>
>Le violazioni dei criteri si applicano solo se si crea un segmento assegnato a una destinazione.

Dopo aver creato il segmento, questo viene analizzato dalla governance dei dati di Adobe Experience Platform per garantire che non vi siano violazioni dei criteri all’interno del segmento. Per ulteriori informazioni, consulta la sezione [[!DNL Data Governance] panoramica](../../data-governance/home.md) .

![](../images/ui/overview/segment-dule-policy-violations.png)

## Passaggi successivi e risorse aggiuntive {#next-steps}

L’ [!DNL Segmentation Service] interfaccia utente offre un flusso di lavoro avanzato che consente di isolare i tipi di pubblico commerciabili dai dati [!DNL Real-time Customer Profile] .

Per ulteriori informazioni su [!DNL Segmentation Service], continua a leggere la documentazione. Per informazioni su come utilizzare l&#39;API [!DNL Segmentation Service], leggi la [[!DNL Segmentation Service] guida per gli sviluppatori](../api/overview.md).
