---
keywords: ' Experience Platform;home;argomenti popolari;Segmentation Service;segmentation service;guida utente;ui guide;segmentation ui guide;Segmentation ui builder;Segmentation builder;Segmentation Builder;'
solution: Experience Platform
title: Guida all’interfaccia utente di Generatore di segmenti
topic: ui guide
description: 'Generatore di segmenti nell’interfaccia utente di Adobe Experience Platform offre un’area di lavoro completa che consente di interagire con gli elementi dei dati del profilo. L’area di lavoro offre controlli intuitivi per la creazione e la modifica di regole, come le sezioni di trascinamento utilizzate per rappresentare le proprietà dei dati. '
translation-type: tm+mt
source-git-commit: 354b756e53b360f31c1832c2b0f946b67099a87f
workflow-type: tm+mt
source-wordcount: '1839'
ht-degree: 0%

---


# [!DNL Segment Builder] Guida all&#39;interfaccia

[!DNL Segment Builder] offre un’area di lavoro completa che consente di interagire con gli elementi  [!DNL Profile] dati. L’area di lavoro offre controlli intuitivi per la creazione e la modifica di regole, come le sezioni di trascinamento utilizzate per rappresentare le proprietà dei dati.

![](../images/ui/segment-builder/segment-builder.png)

## Blocchi di generazione delle definizioni dei segmenti

Gli elementi costitutivi di base delle definizioni dei segmenti sono attributi ed eventi. Inoltre, gli attributi e gli eventi contenuti nelle audience esistenti possono essere utilizzati anche come componenti per le nuove definizioni.

Questi blocchi costitutivi sono visibili nella sezione **[!UICONTROL Fields]** a sinistra dell&#39;area di lavoro [!DNL Segment Builder]. **[!UICONTROL Fields]** contiene una scheda per ciascuno dei blocchi di generazione principali: &quot;[!UICONTROL Attributes]&quot;, &quot;[!UICONTROL Events]&quot; e &quot;[!UICONTROL Audiences]&quot;.

![](../images/ui/segment-builder/segment-fields.png)

### Attributi

La scheda **[!UICONTROL Attributes]** consente di esplorare gli attributi [!DNL Profile] appartenenti alla classe [!DNL XDM Individual Profile]. Ogni cartella può essere espansa per rivelare altri attributi, in cui ogni attributo è una sezione che può essere trascinata sul quadro del generatore di regole al centro dell’area di lavoro. Il file canvas del generatore di regole [viene descritto più dettagliatamente più avanti in questa guida.](#rule-builder-canvas)

![](../images/ui/segment-builder/attributes.png)

### Eventi

La scheda **[!UICONTROL Events]** consente di creare un&#39;audience basata su eventi o azioni che si sono verificati utilizzando gli elementi di dati [!DNL XDM ExperienceEvent]. Potete anche trovare i tipi di evento nella scheda **[!UICONTROL Events]**, una raccolta di eventi di uso comune che consente di creare i segmenti più rapidamente.

Oltre a essere in grado di individuare gli elementi [!DNL ExperienceEvent], potete anche cercare i tipi di evento. I tipi di evento utilizzano la stessa logica di codifica di [!DNL ExperienceEvents], senza che sia necessario eseguire ricerche all&#39;interno della classe [!DNL XDM ExperienceEvent] alla ricerca dell&#39;evento corretto. Ad esempio, utilizzando la barra di ricerca per cercare &quot;carrello&quot;, vengono restituiti i tipi di evento &quot;[!UICONTROL AddCart]&quot; e &quot;[!UICONTROL RemoveCart]&quot;, due azioni carrello utilizzate di frequente per la creazione delle definizioni dei segmenti.

Per cercare qualsiasi tipo di componente, digitatene il nome nella barra di ricerca, che utilizza la sintassi di ricerca di [Lucene](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). I risultati della ricerca iniziano a essere compilati man mano che vengono inserite parole intere. Ad esempio, per creare una regola basata sul campo XDM `ExperienceEvent.commerce.productViews`, iniziare a digitare &quot;product views&quot; nel campo di ricerca. Una volta digitata la parola &quot;prodotto&quot;, i risultati della ricerca iniziano a comparire. Ogni risultato include la gerarchia di oggetti alla quale appartiene.

>[!NOTE]
>
>I campi dello schema personalizzato definiti dall&#39;organizzazione possono richiedere fino a 24 ore per essere visualizzati e diventare disponibili per l&#39;uso nelle regole di creazione.

Puoi quindi trascinare [!DNL ExperienceEvents] e &quot;[!UICONTROL Event Types]&quot; facilmente nella definizione del segmento.

![](../images/ui/segment-builder/events-eventTypes.png)

Per impostazione predefinita, vengono visualizzati solo i campi dello schema compilati dall&#39;archivio dati. Ciò include &quot;[!UICONTROL Event Types]&quot;. Se l&#39;elenco &quot;[!UICONTROL Event Types]&quot; non è visibile, oppure è possibile selezionare &quot;[!UICONTROL Any]&quot; solo come &quot;[!UICONTROL Event Type]&quot;, selezionare l&#39;icona **ingranaggio** accanto a **[!UICONTROL Fields]**, quindi selezionare **[!UICONTROL Show full XDM schema]** in **[!UICONTROL Available Fields]**. Selezionare di nuovo l&#39;icona **ingranaggio** per tornare alla scheda **[!UICONTROL Fields]** e ora è possibile visualizzare più campi &quot;[!UICONTROL Event Types]&quot; e schema, indipendentemente dal fatto che contengano o meno dati.

![](../images/ui/segment-builder/show-populated.png)

### Tipi di pubblico

La scheda **[!UICONTROL Audiences]** elenca tutte le audience importate da origini esterne, come Adobe Audience Manager, nonché quelle create all&#39;interno di [!DNL Experience Platform].

Nella scheda **[!UICONTROL Audiences]** è possibile visualizzare tutte le origini disponibili come un gruppo di cartelle. Quando selezionate le cartelle, è possibile visualizzare le sottocartelle e i tipi di pubblico disponibili. Inoltre, potete selezionare l’icona della cartella (come illustrato nell’immagine all’estrema destra) per visualizzare la struttura delle cartelle (un segno di spunta indica la cartella in cui ci si trova attualmente) e navigare facilmente tra le cartelle selezionando il nome di una cartella nella struttura.

Puoi passare il cursore del mouse sul ⓘ accanto a un&#39;audience per visualizzare le informazioni relative a quest&#39;ultima, inclusi il relativo ID, la descrizione e la gerarchia di cartelle per individuare l&#39;audience.

![](../images/ui/segment-builder/audience-folder-structure.png)

È inoltre possibile cercare audience utilizzando la barra di ricerca, che utilizza la sintassi di ricerca di [Lucene](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). Nella scheda **[!UICONTROL Audiences]**, se si seleziona una cartella di livello principale viene visualizzata la barra di ricerca, che consente di effettuare ricerche all&#39;interno della cartella. I risultati della ricerca iniziano a essere compilati solo dopo l&#39;immissione di intere parole. Ad esempio, per trovare un&#39;audience denominata `Online Shoppers`, iniziate a digitare &quot;Online&quot; nella barra di ricerca. Una volta digitata la parola &quot;Online&quot;, vengono visualizzati i risultati della ricerca contenenti la parola &quot;Online&quot;.

## Area di lavoro del generatore di regole {#rule-builder-canvas}

Una definizione di segmento è una raccolta di regole utilizzate per descrivere le caratteristiche o il comportamento chiave di un&#39;audience target. Queste regole vengono create utilizzando l&#39;area di lavoro del generatore di regole, situata al centro di [!DNL Segment Builder].

Per aggiungere una nuova regola alla definizione del segmento, trascinate una sezione dalla scheda **[!UICONTROL Fields]** e rilasciatela nell’area di lavoro del generatore di regole. Verranno quindi presentate opzioni specifiche per il contesto in base al tipo di dati aggiunto. I tipi di dati disponibili includono: stringhe, date, [!DNL ExperienceEvents], &quot;[!UICONTROL Event Types]&quot; e audience.

![](../images/ui/segment-builder/rule-builder-canvas.png)

>[!IMPORTANT]
>
>Le ultime modifiche ad Adobe Experience Platform hanno aggiornato l&#39;utilizzo degli operatori logici `OR` e `AND` tra gli eventi. Questi aggiornamenti non influiranno sui segmenti esistenti. Tuttavia, tutti gli aggiornamenti successivi ai segmenti esistenti e alle nuove creazioni di segmenti saranno interessati da queste modifiche. Per ulteriori informazioni, leggere l&#39; [aggiornamento delle costanti di ora](./segment-refactoring.md).

### Aggiunta di audience

Puoi trascinare un&#39;audience dalla scheda **[!UICONTROL Audience]** nell&#39;area di lavoro del generatore di regole per fare riferimento all&#39;appartenenza all&#39;audience nella nuova definizione di segmento. Questo consente di includere o escludere l&#39;appartenenza all&#39;audience come attributo nella nuova regola del segmento.

Per i tipi di pubblico [!DNL Platform] creati utilizzando [!DNL Segment Builder], è possibile convertire l&#39;audience in un set di regole utilizzate nella definizione del segmento per tale audience. Questa conversione crea una copia della logica della regola, che può essere modificata senza influenzare la definizione del segmento originale. Prima di convertire le modifiche recenti nella definizione del segmento in logica regola, accertatevi di aver salvato le modifiche recenti.

>[!NOTE]
>
>Quando si aggiunge un&#39;audience da un&#39;origine esterna, viene fatto riferimento solo all&#39;appartenenza all&#39;audience. Non è possibile convertire l&#39;audience in regole, pertanto le regole utilizzate per creare l&#39;audience originale non possono essere modificate nella nuova definizione di segmento.

![](../images/ui/segment-builder/add-audience-to-segment.png)

Se si verificano dei conflitti durante la conversione dei tipi di pubblico in regole, [!DNL Segment Builder] tenterà di mantenere le opzioni esistenti al meglio delle proprie capacità.

### Vista Codice

In alternativa, è possibile visualizzare una versione basata su codice di una regola creata in [!DNL Segment Builder]. Dopo aver creato la regola nell&#39;area di lavoro del generatore di regole, potete selezionare **[!UICONTROL Code view]** per visualizzare il segmento come PQL.

![](../images/ui/segment-builder/code-view.png)

La vista Codice fornisce un pulsante che consente di copiare il valore del segmento da utilizzare nelle chiamate API. Per ottenere la versione più recente del segmento, accertati di aver salvato le ultime modifiche al segmento.

![](../images/ui/segment-builder/copy-code.png)

### Funzioni di aggregazione

Un&#39;aggregazione in [!DNL Segment Builder] è un calcolo su un gruppo di attributi XDM il cui tipo di dati è un numero (un doppio o un numero intero). Le quattro funzioni di aggregazione supportate in Segment Builder (Generatore di segmenti) sono SUM, AVERAGE, MIN e MAX.

Per creare una funzione di aggregazione, selezionare un evento dalla barra a sinistra, quindi inserirlo nel contenitore [!UICONTROL Events].

![](../images/ui/segment-builder/select-event.png)

Dopo aver posizionato l&#39;evento all&#39;interno del contenitore Eventi, selezionate l&#39;icona con le ellissi (...), seguita da **[!UICONTROL Aggregate]**.

![](../images/ui/segment-builder/add-aggregation.png)

L&#39;aggregazione ora viene aggiunta. È ora possibile selezionare la funzione di aggregazione, scegliere l&#39;attributo da aggregare, la funzione di uguaglianza e il valore. Per l&#39;esempio seguente, questo segmento qualificherebbe qualsiasi profilo con una somma di valori acquistati maggiore di $100, anche se ogni singolo acquisto è inferiore a $100.

![](../images/ui/segment-builder/filled-aggregation.png)

## Contenitori

Le regole del segmento vengono valutate nell&#39;ordine in cui sono elencate. I contenitori consentono il controllo dell&#39;ordine di esecuzione mediante l&#39;uso di query nidificate.

Dopo aver aggiunto almeno una sezione al quadro del generatore di regole, potete iniziare ad aggiungere contenitori. Per creare un nuovo contenitore, selezionate le ellissi (...) nell&#39;angolo superiore destro della sezione, quindi selezionate **[!UICONTROL Add container]**.

![](../images/ui/segment-builder/add-container.png)

Un nuovo contenitore viene visualizzato come secondario del primo contenitore, ma è possibile regolare la gerarchia trascinando e spostando i contenitori. Il comportamento predefinito di un contenitore è &quot;[!UICONTROL Include]&quot; l&#39;attributo, l&#39;evento o l&#39;audience forniti. Potete impostare la regola su profili &quot;[!UICONTROL Exclude]&quot; che corrispondono ai criteri del contenitore selezionando **[!UICONTROL Include]** nell&#39;angolo superiore sinistro della sezione e selezionando &quot;[!UICONTROL Exclude]&quot;.

È inoltre possibile estrarre e aggiungere un contenitore secondario al contenitore principale selezionando &quot;unwrapper contenitore&quot; nel contenitore secondario. Selezionate le ellissi (...) nell’angolo superiore destro del contenitore secondario per accedere a questa opzione.

![](../images/ui/segment-builder/include-exclude.png)

Dopo aver selezionato **[!UICONTROL Unwrap container]** il contenitore secondario viene rimosso e i criteri vengono visualizzati in linea.

>[!NOTE]
>
>Quando si estrae un contenitore, prestate attenzione affinché la logica continui a soddisfare la definizione del segmento desiderata.

![](../images/ui/segment-builder/unwrapped-container-inline.png)

## Unisci criteri

[!DNL Experience Platform] consente di unire dati provenienti da più origini e combinarli per visualizzare una visione completa di ogni singolo cliente. Quando si uniscono questi dati, i criteri di unione sono le regole utilizzate da [!DNL Platform] per determinare in che modo i dati verranno classificati come priorità e quali dati verranno combinati per creare un profilo.

È possibile selezionare un criterio di unione che corrisponda allo scopo di marketing di questo pubblico o utilizzare il criterio di unione predefinito fornito da [!DNL Platform]. È possibile creare più criteri di unione univoci per l&#39;organizzazione, inclusa la creazione di criteri di unione predefiniti. Per istruzioni dettagliate sulla creazione di criteri di unione per l&#39;organizzazione, vedere l&#39;esercitazione su [come utilizzare i criteri di unione utilizzando l&#39;interfaccia utente](../../profile/ui/merge-policies.md).

Per selezionare un criterio di unione per la definizione del segmento, selezionate l&#39;icona a forma di ingranaggio nella scheda **[!UICONTROL Fields]**, quindi utilizzate il menu a discesa **[!UICONTROL Merge Policy]** per selezionare il criterio di unione che desiderate utilizzare.

![](../images/ui/segment-builder/merge-policy-selector.png)

## Proprietà dei segmenti

Quando si crea una definizione di segmento, la sezione **[!UICONTROL Segment Properties]** sul lato destro dell&#39;area di lavoro visualizza una stima delle dimensioni del segmento risultante, consentendo di regolare la definizione del segmento come necessario prima di creare l&#39;audience stessa.

La sezione **[!UICONTROL Segment Properties]** contiene anche informazioni importanti sulla definizione del segmento, incluso nome e descrizione. I nomi delle definizioni dei segmenti vengono utilizzati per identificare il segmento tra quelli definiti dall’organizzazione e devono pertanto essere descrittivi, concisi e univoci.

Mentre continuate a generare la definizione del segmento, potete visualizzare un&#39;anteprima impaginata del pubblico selezionando **[!UICONTROL View Profiles]**.

![](../images/ui/segment-builder/segment-properties.png)

>[!NOTE]
>
>Le stime dell&#39;audience vengono generate utilizzando una dimensione di esempio dei dati di quel giorno. Se nell&#39;archivio profili sono presenti meno di 1 milione di entità, viene utilizzato l&#39;intero set di dati; per un periodo compreso tra 1 e 20 milioni di entità, sono utilizzate 1 milione di entità; e per oltre 20 milioni di entità, viene utilizzato il 5% del totale delle entità. Ulteriori informazioni sulla generazione delle stime dei segmenti sono disponibili nella sezione [generazione delle stime](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) dell&#39;esercitazione sulla creazione dei segmenti.

## Passaggi successivi {#next-steps}

Segment Builder (Generatore di segmenti) offre un flusso di lavoro avanzato che consente di isolare i tipi di pubblico commerciabili dai dati [!DNL Real-time Customer Profile]. Dopo aver letto questa guida, è ora possibile:

- Crea le definizioni dei segmenti utilizzando una combinazione di attributi, eventi e audience esistenti come elementi costitutivi.
- Utilizzate l&#39;area di lavoro e i contenitori del generatore di regole per controllare l&#39;ordine in cui vengono eseguite le regole del segmento.
- Visualizzare le stime del pubblico potenziale, per regolare le definizioni dei segmenti in base alle esigenze.
- Abilita tutte le definizioni di segmento per la segmentazione pianificata.
- Abilita le definizioni di segmento specificate per la segmentazione in streaming.

Per saperne di più su [!DNL Segmentation Service], continuate a leggere la documentazione e completate le vostre lezioni guardando i relativi video. Per ulteriori informazioni sulle altre parti dell&#39;interfaccia utente [!DNL Segmentation Service], leggere la [[!DNL Segmentation Service] guida utente](./overview.md)