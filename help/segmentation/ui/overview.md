---
keywords: ' Experience Platform;home;argomenti popolari;Segmentation Service;segmentation service;guida utente;ui guide;segmentation ui guide;Segmentation ui builder;Segment builder;realizza;esistente;exting;'
solution: Experience Platform
title: Guida all’interfaccia utente del servizio di segmentazione
topic: ui guide
description: Adobe Experience Platform Segmentation Service fornisce un'interfaccia utente per la creazione e la gestione delle definizioni dei segmenti.
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 0%

---


# Guida all’interfaccia utente del servizio di segmentazione

[!DNL Adobe Experience Platform Segmentation Service] fornisce un&#39;interfaccia utente per la creazione e la gestione delle definizioni dei segmenti.

## Introduzione

Per utilizzare le definizioni dei segmenti è necessario conoscere i vari servizi [!DNL Experience Platform] coinvolti nella segmentazione. Prima di leggere questa guida utente, consulta la documentazione relativa ai seguenti servizi:

- [[!DNL Segmentation Service]](../home.md):  [!DNL Segmentation Service] consente di dividere in gruppi più piccoli i dati memorizzati in  [!DNL Experience Platform] relazione a individui (come clienti, potenziali, utenti o organizzazioni).
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Consente la creazione di profili cliente collegando le identità di origini dati diverse in cui viene eseguito il caricamento  [!DNL Platform].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il framework standard con cui  [!DNL Platform] organizzare i dati relativi all&#39;esperienza dei clienti.

È inoltre importante conoscere due termini chiave utilizzati in questo documento e comprendere la differenza tra questi:
- **Definizione** segmento: Set di regole utilizzato per descrivere le caratteristiche o i comportamenti chiave di un&#39;audience di destinazione.
- **Pubblico**: Set di profili risultante che soddisfano i criteri di una definizione di segmento.

## Panoramica

Nell&#39; [[!DNL Experience Platform] interfaccia utente](http://platform.adobe.com/), selezionare **[!UICONTROL Segments]** nel menu di navigazione a sinistra per aprire la scheda **[!UICONTROL Overview]**. Questa scheda fornisce collegamenti alla documentazione e ai video per agevolare la comprensione e l&#39;utilizzo dei segmenti.

![](../images/ui/overview/segment-overview.png)

## Sfoglia

Selezionate la scheda **[!UICONTROL Browse]** per visualizzare un elenco di tutte le definizioni di segmento per l&#39;organizzazione IMS.

![](../images/ui/overview/segment-browse-all.png)

Questa visualizzazione elenca le informazioni sulla definizione del segmento, tra cui la suddivisione, il churn, il conteggio del profilo, il metodo di valutazione, la data di creazione e l’ultima data di modifica.

La suddivisione mostra un grafico a barre che mostra la percentuale di profili appartenenti a ciascuno dei seguenti stati: [!UICONTROL Entered], [!UICONTROL Realized] e [!UICONTROL Exiting].

![](../images/ui/overview/segment-browse-breakdown.png)

| Stato | Descrizione |
| ------ | ----------- |
| Inserito | Un nuovo profilo all’interno del segmento. |
| Realizzato | Un profilo esistente che è rimasto all&#39;interno del segmento. |
| Uscita | Un profilo esistente che sta uscendo dal segmento. |

Il churn rappresenta la percentuale di profili che si modificano all&#39;interno di una definizione di segmento rispetto all&#39;ultima esecuzione del processo di segmento, mentre il conteggio dei profili rappresenta il numero totale di profili idonei per il segmento.

Il metodo di valutazione può essere in streaming o batch. I segmenti di streaming vengono valutati costantemente quando i dati entrano nel sistema. I segmenti batch vengono valutati in base a una pianificazione prestabilita.

![](../images/ui/overview/segment-browse-segments.png)

Nella parte superiore della pagina sono disponibili opzioni per aggiungere tutti i segmenti a una pianificazione e per creare un nuovo segmento.

Attivando **[!UICONTROL Add all segments to schedule]** la segmentazione pianificata verrà abilitata. Ulteriori informazioni sulla segmentazione pianificata sono disponibili nella sezione [segmentazione pianificata di questa guida utente](#scheduled-segmentation).

Se si seleziona **[!UICONTROL Create segment]** si passa al Generatore di segmenti. Per ulteriori informazioni sulla creazione di segmenti, consultare la sezione sulla [creazione di un segmento nella guida utente](#create-segment).

![](../images/ui/overview/segment-browse-top.png)

La barra laterale destra contiene informazioni su tutti i segmenti all’interno dell’organizzazione IMS, in cui sono elencati il numero totale di segmenti, l’ultima data di valutazione, la data di valutazione successiva e una suddivisione dei segmenti per metodo di valutazione.

![](../images/ui/overview/segment-browse-segment-info.png)

La selezione della riga della definizione del segmento fornisce un riepilogo della definizione del segmento, con le opzioni per modificare o eliminare il segmento, l&#39;audience qualificata per il segmento, la dimensione totale dell&#39;audience, oltre al nome del segmento, alla descrizione, al metodo di valutazione, alla data di creazione e all&#39;ultima data modificata.

![](../images/ui/overview/segment-browse-details.png)

## Dettagli definizione segmento {#segment-details}

Per visualizzare ulteriori dettagli su una definizione di segmento specifica, seleziona il nome di un segmento nella scheda **[!UICONTROL Browse]**.

Viene visualizzata la pagina dei dettagli del segmento. In alto, è disponibile un riepilogo della definizione del segmento, delle informazioni sulla dimensione del pubblico qualificata e delle destinazioni per le quali il segmento è attivato.

![](../images/ui/overview/segment-details-summary.png)

### Riepilogo segmento

La sezione **[!UICONTROL Segment summary]** contiene informazioni quali l&#39;ID, il nome, la descrizione e i dettagli degli attributi.

Inoltre, potete modificare il segmento. Se si seleziona **[!UICONTROL Edit segment]** si passa alla [!DNL Segment Builder]. Per informazioni più dettagliate sull&#39;utilizzo dell&#39;area di lavoro [!DNL Segment Builder], leggere la [[!DNL Segment Builder] guida utente](./segment-builder.md).

### Totale pubblico nel segmento

La sezione **[!UICONTROL Total audience in segment]** mostra il numero totale di profili idonei per il segmento.

Le stime vengono generate utilizzando una dimensione di esempio dei dati di quel giorno. Se nell&#39;archivio profili sono presenti meno di 1 milione di entità, viene utilizzato l&#39;intero set di dati; per un periodo compreso tra 1 e 20 milioni di entità, sono utilizzate 1 milione di entità; e per oltre 20 milioni di entità, viene utilizzato il 5% del totale delle entità. Ulteriori informazioni sulla generazione delle stime dei segmenti sono disponibili nella sezione [generazione delle stime](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) dell&#39;esercitazione sulla creazione dei segmenti.

### Destinazioni attivate

La sezione **[!UICONTROL Activated destinations]** mostra le destinazioni per le quali questo segmento è attivato.

>[!NOTE]
>
> Le destinazioni sono una funzionalità disponibile con [!DNL Real-time Customer Data Platform] e consentono di esportare i dati su piattaforme esterne. Per ulteriori informazioni sulle destinazioni, leggere la [panoramica delle destinazioni](../../destinations/home.md). Per informazioni su come attivare un segmento in una destinazione, leggere la guida [sull&#39;attivazione dei segmenti in una destinazione](../../destinations/ui/activate-destinations.md).

### Esempi di profilo

Sotto c&#39;è un esempio di profili idonei per il segmento, con informazioni dettagliate che includono l&#39;ID [!DNL Profile], il nome, il cognome e l&#39;e-mail personale.

Il modo in cui viene attivato il campionamento dei dati dipende dal metodo di assimilazione.

Per l’assimilazione batch, lo store del profilo viene analizzato automaticamente ogni quindici minuti per verificare se un nuovo batch è stato correttamente assimilato dall’ultima esecuzione del processo di campionamento. In tal caso, lo store del profilo viene successivamente analizzato per verificare se il numero di record è stato modificato almeno del 5%. Se tali condizioni sono soddisfatte, viene attivato un nuovo processo di campionamento.

Per l&#39;assimilazione in streaming, lo store del profilo viene automaticamente analizzato ogni ora per verificare se il numero di record è cambiato almeno del 5%. Se questa condizione viene soddisfatta, viene attivato un nuovo processo di campionamento.

La dimensione del campione della scansione dipende dal numero complessivo di entità nell&#39;archivio profili. Queste dimensioni di campione sono rappresentate nella seguente tabella:

| Entità nell&#39;archivio profili | Dimensione del campione |
| ------------------------- | ----------- |
| Meno di 1 milione | Set di dati completo |
| Da 1 a 20 milioni | 1 milione |
| Oltre 20 milioni | 5% del totale |

Per informazioni più dettagliate su ciascun [!DNL Profile], selezionare l&#39;ID [!DNL Profile]. Per ulteriori informazioni sui dettagli di un profilo, leggere la [[!DNL Real-time Customer Profile] guida utente](../../profile/ui/user-guide.md#profile-detail).

![](../images/ui/overview/segment-details-profiles.png)

## Creazione di un segmento {#create-segment}

Se si seleziona **[!UICONTROL Create segment]** nell&#39;angolo superiore destro, si apre l&#39;area di lavoro [!DNL Segment Builder], dove è possibile iniziare a creare una definizione di segmento.

![](../images/ui/overview/segment-browse-create.png)

### [!DNL Segment Builder] workspace

[!DNL Segment Builder] offre un’area di lavoro completa che consente di interagire con gli elementi  [!DNL Profile] dati. L’area di lavoro offre controlli intuitivi per la creazione e la modifica di regole, come le sezioni di trascinamento utilizzate per rappresentare le proprietà dei dati.

Per informazioni più dettagliate sull&#39;utilizzo dell&#39;area di lavoro [!DNL Segment Builder], leggere la [[!DNL Segment Builder] guida utente](./segment-builder.md).

![](../images/ui/overview/segment-builder.png)

## Segmentazione pianificata {#scheduled-segmentation}

Una volta create le definizioni dei segmenti, potete valutarle tramite una valutazione su richiesta o pianificata (continua). Valutazione significa spostare i dati [!DNL Real-time Customer Profile] attraverso le definizioni dei segmenti al fine di produrre le audience corrispondenti. Una volta creati, i tipi di pubblico vengono salvati e memorizzati in modo che possano essere esportati utilizzando le [!DNL Experience Platform] API.

La valutazione su richiesta prevede l&#39;utilizzo dell&#39;API per eseguire la valutazione e generare audience in base alle esigenze, mentre la valutazione programmata (nota anche come &quot;segmentazione pianificata&quot;) consente di creare una pianificazione periodica per valutare le definizioni dei segmenti in un momento specifico (al massimo, una volta al giorno).

### Abilita segmentazione pianificata {#enable-scheduled-segmentation}

Per abilitare le definizioni dei segmenti per la valutazione pianificata, puoi utilizzare l’interfaccia utente o l’API. Nell&#39;interfaccia utente, tornare alla scheda **[!UICONTROL Browse]** all&#39;interno di **[!UICONTROL Segments]** e attivare **[!UICONTROL Add all segments to schedule]**. In questo modo tutti i segmenti verranno valutati in base alla pianificazione impostata dall&#39;organizzazione.

>[!NOTE]
>
>La valutazione pianificata può essere abilitata per le sandbox con un massimo di cinque (5) criteri di unione per [!DNL XDM Individual Profile]. Se l&#39;organizzazione dispone di più di cinque criteri di unione per [!DNL XDM Individual Profile] all&#39;interno di un unico ambiente sandbox, non sarà possibile utilizzare la valutazione pianificata.

Le pianificazioni al momento possono essere create solo tramite l&#39;API. Per informazioni dettagliate sulla creazione, la modifica e l&#39;utilizzo delle pianificazioni tramite l&#39;API, seguite l&#39;esercitazione per valutare e accedere ai risultati dei segmenti, in particolare la sezione sulla [valutazione pianificata utilizzando l&#39;API](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![](../images/ui/overview/segment-browse-scheduled.png)

## Segmentazione streaming {#streaming-segmentation}

La segmentazione in streaming è la capacità di eseguire la segmentazione su [!DNL Platform] in tempo quasi reale, concentrandosi sulla ricchezza dei dati. Con la segmentazione in streaming, la qualifica del segmento ora avviene quando i dati entrano in [!DNL Platform], eliminando la necessità di pianificare ed eseguire i processi di segmentazione.

Ulteriori informazioni sulla segmentazione in streaming sono disponibili nella [guida utente della segmentazione in streaming](./streaming-segmentation.md).

>[!NOTE]
>
>Per consentire il funzionamento della segmentazione in streaming, è necessario abilitare la segmentazione pianificata per l&#39;organizzazione. Per informazioni dettagliate sull&#39;abilitazione della segmentazione pianificata, consultate [la sezione sulla segmentazione in streaming in questa guida utente](#scheduled-segmentation).

## Violazioni dei criteri

>[!NOTE]
>
>Le violazioni dei criteri si applicano solo se stai creando un segmento che è stato assegnato a una destinazione.

Dopo aver creato il segmento, il segmento verrà analizzato da Adobe Experience Platform Data Governance per assicurarsi che non ci siano violazioni dei criteri all&#39;interno del segmento. Per ulteriori informazioni, vedere la [[!DNL Data Governance] panoramica](../../data-governance/home.md).

![](../images/ui/overview/segment-dule-policy-violations.png)

## Passaggi successivi e risorse aggiuntive {#next-steps}

L&#39;interfaccia [!DNL Segmentation Service] offre un flusso di lavoro avanzato che consente di isolare i tipi di pubblico commerciabili dai dati [!DNL Real-time Customer Profile].

Per ulteriori informazioni su [!DNL Segmentation Service], continuare a leggere la documentazione. Per informazioni sull&#39;utilizzo dell&#39;API [!DNL Segmentation Service], leggere la guida [[!DNL Segmentation Service] per gli sviluppatori](../api/overview.md).
