---
keywords: Experience Platform;home;argomenti popolari;servizio di segmentazione;segmentazione;servizio di segmentazione;guida utente;guida utente;guida utente;guida utente di segmentazione;generatore di segmenti;generatore di segmenti;
solution: Experience Platform
title: Guida all’interfaccia utente di Generatore di segmenti
topic-legacy: ui guide
description: Il Generatore di segmenti nell’interfaccia utente di Adobe Experience Platform offre un’area di lavoro ricca che consente di interagire con gli elementi dati di profilo. L’area di lavoro fornisce controlli intuitivi per la creazione e la modifica di regole, ad esempio riquadri drag-and-drop utilizzati per rappresentare le proprietà dei dati.
exl-id: b27516ea-8749-4b44-99d0-98d3dc2f4c65
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1940'
ht-degree: 0%

---

# [!DNL Segment Builder] Guida all’interfaccia utente

[!DNL Segment Builder] offre un’area di lavoro ricca che consente di interagire con gli elementi  [!DNL Profile] dati. L’area di lavoro fornisce controlli intuitivi per la creazione e la modifica di regole, ad esempio riquadri drag-and-drop utilizzati per rappresentare le proprietà dei dati.

![](../images/ui/segment-builder/segment-builder.png)

## Blocchi di generazione della definizione del segmento

Gli elementi di base delle definizioni dei segmenti sono attributi ed eventi. Inoltre, gli attributi e gli eventi contenuti nei tipi di pubblico esistenti possono essere utilizzati come componenti per nuove definizioni.

Puoi visualizzare questi blocchi predefiniti nella sezione **[!UICONTROL Fields]** sul lato sinistro dell’ area di lavoro [!DNL Segment Builder] . **[!UICONTROL Fields]** contiene una scheda per ciascuno dei blocchi predefiniti principali: &quot;[!UICONTROL Attributes]&quot;, &quot;[!UICONTROL Events]&quot; e &quot;[!UICONTROL Audiences]&quot;.

![](../images/ui/segment-builder/segment-fields.png)

### Attributi

La scheda **[!UICONTROL Attributes]** ti consente di sfogliare gli attributi [!DNL Profile] appartenenti alla classe [!DNL XDM Individual Profile] . Ogni cartella può essere espansa per visualizzare attributi aggiuntivi, in cui ogni attributo è un riquadro che può essere trascinato sull’area di lavoro del generatore di regole al centro dell’area di lavoro. La sezione [canvas](#rule-builder-canvas) del generatore di regole viene discussa più avanti in questa guida.

![](../images/ui/segment-builder/attributes.png)

### Eventi

La scheda **[!UICONTROL Events]** ti consente di creare un pubblico in base a eventi o azioni che hanno avuto luogo utilizzando gli elementi dati [!DNL XDM ExperienceEvent] . Puoi anche trovare Tipi di eventi nella scheda **[!UICONTROL Events]** , che è una raccolta di eventi comunemente utilizzati per consentire di creare i segmenti più rapidamente.

Oltre a essere in grado di cercare gli elementi [!DNL ExperienceEvent], puoi anche cercare i tipi di evento. I tipi di evento utilizzano la stessa logica di codifica di [!DNL ExperienceEvents], senza che sia necessario cercare l’evento corretto nella classe [!DNL XDM ExperienceEvent]. Ad esempio, utilizzando la barra di ricerca per cercare &quot;carrello&quot; vengono restituiti i Tipi di evento &quot;[!UICONTROL AddCart]&quot; e &quot;[!UICONTROL RemoveCart]&quot;, due azioni carrello molto comunemente utilizzate durante la creazione delle definizioni dei segmenti.

È possibile cercare qualsiasi tipo di componente digitandone il nome nella barra di ricerca, che utilizza la [sintassi di ricerca di Lucene](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). I risultati della ricerca iniziano a popolarsi man mano che vengono inserite parole intere. Ad esempio, per creare una regola basata sul campo XDM `ExperienceEvent.commerce.productViews`, inizia a digitare &quot;product views&quot; nel campo di ricerca. Una volta digitata la parola &quot;prodotto&quot;, iniziano ad apparire i risultati della ricerca. Ogni risultato include la gerarchia di oggetti a cui appartiene.

>[!NOTE]
>
>I campi dello schema personalizzato definiti dall&#39;organizzazione possono richiedere fino a 24 ore per essere visualizzati e diventare disponibili per l&#39;utilizzo nella creazione delle regole.

Puoi quindi trascinare facilmente [!DNL ExperienceEvents] e &quot;[!UICONTROL Event Types]&quot; nella definizione del segmento.

![](../images/ui/segment-builder/events-eventTypes.png)

Per impostazione predefinita, vengono visualizzati solo i campi dello schema compilati dall’archivio dati. Ciò include &quot;[!UICONTROL Event Types]&quot;. Se l&#39;elenco &quot;[!UICONTROL Event Types]&quot; non è visibile o se è possibile selezionare &quot;[!UICONTROL Any]&quot; solo come &quot;[!UICONTROL Event Type]&quot;, selezionare l&#39;icona **ingranaggio** accanto a **[!UICONTROL Fields]**, quindi selezionare **[!UICONTROL Show full XDM schema]** in **[!UICONTROL Available Fields]**. Seleziona nuovamente l&#39; **icona a forma di ingranaggio** per tornare alla scheda **[!UICONTROL Fields]** e ora dovresti essere in grado di visualizzare più campi &quot;[!UICONTROL Event Types]&quot; e schema, indipendentemente dal fatto che contengano o meno dati.

![](../images/ui/segment-builder/show-populated.png)

### Tipi di pubblico

La scheda **[!UICONTROL Audiences]** elenca tutti i tipi di pubblico importati da origini esterne, ad esempio Adobe Audience Manager, e quelli creati in [!DNL Experience Platform].

Nella scheda **[!UICONTROL Audiences]** è possibile visualizzare tutte le origini disponibili come gruppo di cartelle. Quando selezioni le cartelle, puoi vedere le sottocartelle e i tipi di pubblico disponibili. Inoltre, è possibile selezionare l’icona della cartella (come mostrato nell’immagine all’estrema destra) per visualizzare la struttura della cartella (un segno di spunta indica la cartella in cui ci si trova attualmente) e navigare facilmente tra le cartelle selezionando il nome di una cartella nella struttura.

Puoi passare il cursore sul ⓘ accanto a un pubblico per visualizzare informazioni sul pubblico, tra cui il suo ID, la sua descrizione e la gerarchia delle cartelle per individuare il pubblico.

![](../images/ui/segment-builder/audience-folder-structure.png)

Puoi anche cercare il pubblico utilizzando la barra di ricerca, che utilizza la sintassi di ricerca di [Lucene](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). Nella scheda **[!UICONTROL Audiences]** , se si seleziona una cartella di livello superiore viene visualizzata la barra di ricerca, che consente di eseguire ricerche all’interno della cartella. I risultati della ricerca iniziano a compilarsi solo una volta inserite intere parole. Ad esempio, per trovare un pubblico denominato `Online Shoppers`, inizia a digitare &quot;Online&quot; nella barra di ricerca. Una volta digitata la parola &quot;Online&quot;, vengono visualizzati i risultati della ricerca contenenti la parola &quot;Online&quot;.

## Area di lavoro del generatore di regole {#rule-builder-canvas}

Una definizione di segmento è una raccolta di regole utilizzate per descrivere le caratteristiche o il comportamento chiave di un pubblico target. Queste regole vengono create utilizzando l&#39;area di lavoro del generatore di regole, situata al centro di [!DNL Segment Builder].

Per aggiungere una nuova regola alla definizione del segmento, trascina un riquadro dalla scheda **[!UICONTROL Fields]** e rilascialo nell’area di lavoro del generatore di regole. Verranno quindi presentate opzioni specifiche per il contesto in base al tipo di dati aggiunti. I tipi di dati disponibili includono: stringhe, date, [!DNL ExperienceEvents], &quot;[!UICONTROL Event Types]&quot; e tipi di pubblico.

![](../images/ui/segment-builder/rule-builder-canvas.png)

>[!IMPORTANT]
>
>Le ultime modifiche apportate a Adobe Experience Platform hanno aggiornato l’utilizzo degli operatori logici `OR` e `AND` tra gli eventi. Questi aggiornamenti non avranno alcun impatto sui segmenti esistenti. Tuttavia, questi cambiamenti interesseranno tutti gli aggiornamenti successivi ai segmenti esistenti e alle nuove creazioni di segmenti. Per ulteriori informazioni, leggere l&#39; [aggiornamento delle costanti di tempo](./segment-refactoring.md) .

### Aggiunta di tipi di pubblico

Puoi trascinare un pubblico dalla scheda **[!UICONTROL Audience]** nell’area di lavoro del generatore di regole per fare riferimento all’appartenenza al pubblico nella nuova definizione del segmento. Questo ti consente di includere o escludere l’appartenenza al pubblico come attributo nella nuova regola del segmento.

Per i tipi di pubblico [!DNL Platform] creati utilizzando [!DNL Segment Builder], puoi convertire il pubblico nel set di regole utilizzate nella definizione del segmento per quel pubblico. Questa conversione crea una copia della logica della regola, che può quindi essere modificata senza influire sulla definizione originale del segmento. Assicurati di aver salvato le modifiche recenti alla definizione del segmento prima di convertirlo in logica di regola.

>[!NOTE]
>
>Quando si aggiunge un pubblico da un’origine esterna, viene fatto riferimento solo all’appartenenza al pubblico. Non è possibile convertire il pubblico in regole e pertanto le regole utilizzate per creare il pubblico originale non possono essere modificate nella nuova definizione del segmento.

![](../images/ui/segment-builder/add-audience-to-segment.png)

In caso di conflitti durante la conversione di tipi di pubblico in regole, [!DNL Segment Builder] tenterà di mantenere al meglio le opzioni esistenti.

### Vista Codice

In alternativa, puoi visualizzare una versione basata su codice di una regola creata in [!DNL Segment Builder]. Dopo aver creato la regola nell&#39;area di lavoro del generatore di regole, puoi selezionare **[!UICONTROL Code view]** per visualizzare il segmento come PQL.

![](../images/ui/segment-builder/code-view.png)

La vista Codice fornisce un pulsante che consente di copiare il valore del segmento da utilizzare nelle chiamate API. Per ottenere la versione più recente del segmento, accertati di aver salvato le modifiche più recenti al segmento.

![](../images/ui/segment-builder/copy-code.png)

### Funzioni di aggregazione

Un&#39;aggregazione in [!DNL Segment Builder] è un calcolo su un gruppo di attributi XDM il cui tipo di dati è un numero (doppio o intero). Le quattro funzioni di aggregazione supportate nel Generatore di segmenti sono SOMMA, MEDIA, MIN e MAX.

Per creare una funzione di aggregazione, seleziona un evento dalla barra a sinistra e inseriscilo nel contenitore [!UICONTROL Events] .

![](../images/ui/segment-builder/select-event.png)

Dopo aver posizionato l’evento all’interno del contenitore Eventi, seleziona l’icona dei puntini di sospensione (...), seguita da **[!UICONTROL Aggregate]**.

![](../images/ui/segment-builder/add-aggregation.png)

L’aggregazione viene ora aggiunta. Ora puoi selezionare la funzione di aggregazione, scegliere l&#39;attributo da aggregare, la funzione di uguaglianza e il valore. Per l’esempio seguente, questo segmento qualificherebbe qualsiasi profilo con una somma di valori acquistati maggiore di $100, anche se ogni singolo acquisto è inferiore a $100.

![](../images/ui/segment-builder/filled-aggregation.png)

### Funzioni di conteggio

Le funzioni di conteggio nel Generatore di segmenti vengono utilizzate per cercare eventi specifici e contare il numero di volte in cui vengono eseguiti. Le funzioni di conteggio supportate nel Generatore di segmenti sono &quot;Almeno&quot;, &quot;Al massimo&quot;, &quot;Esattamente&quot;, &quot;Tra&quot; e &quot;Tutto&quot;.

Per creare una funzione di conteggio, seleziona un evento dalla barra a sinistra e inseriscilo nel contenitore [!UICONTROL Events] .

![](../images/ui/segment-builder/add-event.png)

Dopo aver posizionato l’evento all’interno del contenitore Eventi, seleziona il pulsante [!UICONTROL At least 1] .

![](../images/ui/segment-builder/add-count.png)

La funzione di conteggio viene ora aggiunta. Ora puoi selezionare la funzione di conteggio e il valore della funzione. L’esempio seguente includerebbe qualsiasi evento con almeno un clic.

![](../images/ui/segment-builder/select-count.png)

## Contenitori

Le regole dei segmenti vengono valutate nell’ordine in cui sono elencate. I contenitori consentono il controllo dell’ordine di esecuzione tramite l’utilizzo di query nidificate.

Dopo aver aggiunto almeno un riquadro all’area di lavoro del generatore di regole, puoi iniziare ad aggiungere contenitori. Per creare un nuovo contenitore, seleziona i puntini di sospensione (...) nell’angolo in alto a destra del riquadro, quindi seleziona **[!UICONTROL Add container]**.

![](../images/ui/segment-builder/add-container.png)

Un nuovo contenitore viene visualizzato come secondario del primo contenitore, ma è possibile regolare la gerarchia trascinando e spostando i contenitori. Il comportamento predefinito di un contenitore è &quot;[!UICONTROL Include]&quot; l&#39;attributo, l&#39;evento o il pubblico fornito. Puoi impostare la regola sui profili &quot;[!UICONTROL Exclude]&quot; che corrispondono ai criteri del contenitore selezionando **[!UICONTROL Include]** nell’angolo in alto a sinistra del riquadro e selezionando &quot;[!UICONTROL Exclude]&quot;.

È inoltre possibile estrarre un contenitore secondario e aggiungerlo in linea al contenitore principale selezionando &quot;estrae il contenitore&quot; dal contenitore secondario. Seleziona i puntini di sospensione (...) nell’angolo in alto a destra del contenitore secondario per accedere a questa opzione.

![](../images/ui/segment-builder/include-exclude.png)

Dopo aver selezionato **[!UICONTROL Unwrap container]** il contenitore secondario viene rimosso e i criteri vengono visualizzati in linea.

>[!NOTE]
>
>Quando scompili i contenitori, fai attenzione a che la logica continui a soddisfare la definizione del segmento desiderata.

![](../images/ui/segment-builder/unwrapped-container-inline.png)

## Unisci criteri

[!DNL Experience Platform] consente di unire dati provenienti da più sorgenti e combinarli per visualizzare una visualizzazione completa di ciascuno dei singoli clienti. Quando si riuniscono questi dati, i criteri di unione sono le regole utilizzate da [!DNL Platform] per determinare in che modo i dati avranno priorità e quali saranno combinati per creare un profilo.

Puoi selezionare un criterio di unione che corrisponda allo scopo di marketing per questo pubblico o utilizzare il criterio di unione predefinito fornito da [!DNL Platform]. È possibile creare più criteri di unione univoci per l&#39;organizzazione, inclusa la creazione di un criterio di unione predefinito. Per istruzioni dettagliate sulla creazione di criteri di unione per l&#39;organizzazione, vedere l&#39;esercitazione su [come utilizzare i criteri di unione utilizzando l&#39;interfaccia utente](../../profile/ui/merge-policies.md).

Per selezionare un criterio di unione per la definizione del segmento, seleziona l’icona a forma di ingranaggio nella scheda **[!UICONTROL Fields]** , quindi utilizza il menu a discesa **[!UICONTROL Merge Policy]** per selezionare il criterio di unione che desideri utilizzare.

![](../images/ui/segment-builder/merge-policy-selector.png)

## Proprietà del segmento

Quando si crea una definizione di segmento, la sezione **[!UICONTROL Segment Properties]** sul lato destro dell’area di lavoro visualizza una stima delle dimensioni del segmento risultante, che consente di regolare la definizione del segmento in base alle esigenze prima di creare il pubblico stesso.

La sezione **[!UICONTROL Segment Properties]** contiene inoltre informazioni importanti sulla definizione del segmento, compreso il nome e la descrizione. I nomi delle definizioni dei segmenti vengono utilizzati per identificare il segmento tra quelli definiti dall’organizzazione e devono quindi essere descrittivi, concisi e univoci.

Continuando a generare la definizione del segmento, puoi visualizzare un’anteprima impaginata del pubblico selezionando **[!UICONTROL View Profiles]**.

![](../images/ui/segment-builder/segment-properties.png)

>[!NOTE]
>
>Le stime del pubblico sono generate utilizzando una dimensione del campione dei dati del giorno in questione. Se nell’archivio dei profili sono presenti meno di 1 milione di entità, viene utilizzato l’intero set di dati; tra 1 e 20 milioni di entità sono utilizzate 1 milione di entità; e per più di 20 milioni di entità viene utilizzato il 5% del totale delle entità. Ulteriori informazioni sulla generazione delle stime dei segmenti sono disponibili nella sezione [generazione delle stime](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) dell’esercitazione sulla creazione dei segmenti.

## Passaggi successivi {#next-steps}

Il Generatore di segmenti offre un flusso di lavoro avanzato che consente di isolare i tipi di pubblico negoziabili dai dati [!DNL Real-time Customer Profile]. Dopo aver letto questa guida, ora dovresti essere in grado di:

- Crea definizioni di segmenti utilizzando una combinazione di attributi, eventi e tipi di pubblico esistenti come blocchi predefiniti.
- Utilizza l’area di lavoro e i contenitori del generatore di regole per controllare l’ordine in cui vengono eseguite le regole del segmento.
- Visualizza le stime del pubblico potenziale, che consentono di regolare le definizioni dei segmenti in base alle esigenze.
- Abilita tutte le definizioni dei segmenti per la segmentazione pianificata.
- Abilita definizioni di segmenti specifiche per la segmentazione in streaming.

Per saperne di più su [!DNL Segmentation Service], continua a leggere la documentazione e completa il tuo apprendimento guardando i relativi video. Per ulteriori informazioni sulle altre parti dell&#39;interfaccia utente di [!DNL Segmentation Service], consulta la [[!DNL Segmentation Service] guida utente](./overview.md)
