---
solution: Experience Platform
title: Guida dell’interfaccia utente di Segment Builder
description: Il Generatore di segmenti nell’interfaccia utente di Adobe Experience Platform offre un’area di lavoro avanzata che consente di interagire con gli elementi dati del profilo. L’area di lavoro fornisce controlli intuitivi per la creazione e la modifica di regole, ad esempio le tessere trascinate utilizzate per rappresentare le proprietà dei dati.
exl-id: b27516ea-8749-4b44-99d0-98d3dc2f4c65
source-git-commit: 6d33c1bd3921a754edfab227fad236caf60ac960
workflow-type: tm+mt
source-wordcount: '3308'
ht-degree: 7%

---

# [!DNL Segment Builder] Guida all’interfaccia utente

[!DNL Segment Builder] fornisce un’area di lavoro ricca che consente di interagire con [!DNL Profile] elementi dati. L’area di lavoro fornisce controlli intuitivi per la creazione e la modifica di regole, ad esempio le tessere trascinate utilizzate per rappresentare le proprietà dei dati.

![Viene visualizzata l’interfaccia utente del Generatore di segmenti.](../images/ui/segment-builder/segment-builder.png)

## Blocchi predefiniti di definizione del segmento {#building-blocks}

>[!CONTEXTUALHELP]
>id="platform_segments_createsegment_segmentbuilder_fields"
>title="Campi"
>abstract="I tre tipi di campi che compongono una definizione di segmento sono attributi, eventi e pubblico. Gli attributi consentono di utilizzare gli attributi di profilo che appartengono alla classe XDM Profilo individuale; gli eventi consentono di creare un pubblico basato su azioni o eventi che hanno luogo utilizzando gli elementi di dati XDM ExperienceEvent; i tipi di pubblico consentono di utilizzare tipi di pubblico importati da origini esterne."

Gli elementi di base per le definizioni dei segmenti sono attributi ed eventi. Inoltre, gli attributi e gli eventi contenuti nei tipi di pubblico esistenti possono essere utilizzati come componenti per nuove definizioni.

Puoi visualizzare questi blocchi predefiniti nella sezione **[!UICONTROL Campi]** sezione sul lato sinistro del [!DNL Segment Builder] Workspace. **[!UICONTROL Campi]** contiene una scheda per ciascuno dei blocchi predefiniti principali: &quot;[!UICONTROL Attributi]&quot;, &quot;[!UICONTROL Eventi]&quot;, e &quot;[!UICONTROL Tipi di pubblico]&quot;.

![Viene evidenziata la sezione dei campi del Generatore di segmenti.](../images/ui/segment-builder/segment-fields.png)

### Attributi

Il **[!UICONTROL Attributi]** consente di navigare [!DNL Profile] attributi appartenenti al [!DNL XDM Individual Profile] classe. Ogni cartella può essere espansa per visualizzare attributi aggiuntivi, dove ogni attributo è una sezione che può essere trascinata nell’area di lavoro del generatore di regole al centro dell’area di lavoro. Il [area di lavoro generatore regole](#rule-builder-canvas) viene discusso più dettagliatamente più avanti in questa guida.

![Viene evidenziata la sezione degli attributi dei campi Generatore di segmenti.](../images/ui/segment-builder/attributes.png)

### Eventi

Il **[!UICONTROL Eventi]** consente di creare un pubblico in base a eventi o azioni che hanno avuto luogo utilizzando [!DNL XDM ExperienceEvent] elementi dati. Puoi anche trovare i Tipi di evento su **[!UICONTROL Eventi]** , una raccolta di eventi di uso comune per accelerare la creazione delle definizioni dei segmenti.

Oltre a poter cercare [!DNL ExperienceEvent] , è inoltre possibile cercare Tipi di evento. I tipi di evento utilizzano la stessa logica di codifica [!DNL ExperienceEvents], senza richiedere di eseguire ricerche attraverso [!DNL XDM ExperienceEvent] classe alla ricerca dell&#39;evento corretto. Ad esempio, se si utilizza la barra di ricerca per cercare &quot;carrello&quot;, vengono restituiti i Tipi di evento &quot;[!UICONTROL AddCart]&quot; e &quot;[!UICONTROL RimuoviCarrello]&quot;, che sono due azioni del carrello molto comunemente utilizzate durante la creazione delle definizioni dei segmenti.

È possibile cercare qualsiasi tipo di componente digitandone il nome nella barra di ricerca, che utilizza [Sintassi di ricerca di Lucene](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). I risultati della ricerca iniziano a essere compilati quando vengono immesse parole intere. Ad esempio, per creare una regola basata sul campo XDM `ExperienceEvent.commerce.productViews`, inizia a digitare &quot;visualizzazioni prodotto&quot; nel campo di ricerca. Una volta digitata la parola &quot;product&quot;, i risultati della ricerca iniziano a comparire. Ogni risultato include la gerarchia di oggetti a cui appartiene.

>[!NOTE]
>
>La visualizzazione dei campi dello schema personalizzati definiti dall’organizzazione può richiedere fino a 24 ore e diventare disponibili per l’utilizzo nella creazione di regole.

Puoi quindi trascinare e rilasciare facilmente [!DNL ExperienceEvents] e &quot;[!UICONTROL Tipi di evento]&quot; nella definizione del segmento.

![Viene evidenziata la sezione degli eventi dell’interfaccia utente di Segment Builder.](../images/ui/segment-builder/events.png)

Per impostazione predefinita, vengono visualizzati solo i campi schema compilati dell’archivio dati. Ciò include &quot;[!UICONTROL Tipi di evento]&quot;. Se &quot;[!UICONTROL Tipi di evento]&quot;L’elenco non è visibile oppure puoi solo selezionare&quot;[!UICONTROL Qualsiasi]&quot; as an &quot;[!UICONTROL Tipo di evento]&quot;, seleziona la **icona ingranaggio** accanto a **[!UICONTROL Campi]**, quindi seleziona **[!UICONTROL Mostra schema XDM completo]** in **[!UICONTROL Campi disponibili]**. Seleziona la **icona ingranaggio** di nuovo per tornare al **[!UICONTROL Campi]** e ora dovresti poter visualizzare più &quot;[!UICONTROL Tipi di evento]&quot; e campi dello schema, indipendentemente dal fatto che contengano o meno dati.

![Sono evidenziati i pulsanti di scelta che consentono di scegliere se visualizzare solo i campi con dati o tutti i campi XDM.](../images/ui/segment-builder/show-populated.png)

#### Set di dati della suite di rapporti di Adobe Analytics

Puoi utilizzare i dati di una singola o più suite di rapporti di Adobe Analytics come eventi all’interno della segmentazione.

Quando si utilizzano dati da una singola suite di rapporti di Analytics, Platform aggiungerà automaticamente descrittori e nomi descrittivi alle eVar, semplificando la ricerca di tali campi in [!DNL Segment Builder].

![Un’immagine che mostra come le variabili generiche (eVar) sono mappate con un nome descrittivo.](../images/ui/segment-builder/single-report-suite.png)

Platform quando si utilizzano dati provenienti da più suite di rapporti di Analytics **non può** aggiungi automaticamente descrittori o nomi descrittivi alle eVar. Di conseguenza, prima di utilizzare i dati delle suite di rapporti di Analytics, devi eseguirne il mapping ai campi XDM. Ulteriori informazioni sulla mappatura delle variabili di Analytics su XDM sono disponibili nella sezione [guida alla connessione sorgente di Adobe Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md#mapping).

Ad esempio, considera una situazione in cui disponevi di due suite di rapporti con le seguenti variabili:

| Campo | Schema suite di rapporti A | Schema B suite di rapporti |
| ----- | --------------------- | --------------------- |
| eVar1 | Dominio di riferimento | Accesso effettuato S/N |
| eVar2 | Nome pagina | ID fedeltà membro |
| eVar3 | URL | Nome pagina |
| eVar4 | Termini di ricerca | Nome prodotto |
| event1 | Clic | Page Views |
| event2 | Page Views | Aggiunte carrello |
| event3 | Aggiunte carrello | Pagamenti |
| event4 | Acquisti | Acquisti |

In questo caso, puoi mappare le due suite di rapporti con il seguente schema:

![Un’immagine che mostra come due suite di rapporti possono essere mappate in un unico schema di unione.](../images/ui/segment-builder/union-schema.png)

>[!NOTE]
>
>Anche se i valori eVar generici vengono comunque popolati, è necessario **non** utilizzali (se possibile) nelle definizioni dei segmenti, poiché i valori potrebbero avere un significato diverso rispetto a quello originale nei loro rapporti.

Una volta mappate le suite di rapporti, puoi utilizzare questi campi appena mappati all’interno dei flussi di lavoro e della segmentazione relativi al profilo.

| Scenario | Esperienza schema di unione | Segmentazione variabile generica | Segmentazione mappata variabile |
| -------- | ----------------------- | ----------------------------- | ---------------------------- |
| Suite di rapporti singola | Il descrittore di nome descrittivo è incluso nelle variabili generiche. <br><br>**Esempio:** Nome pagina (eVar2) | <ul><li>Descrittore di nome intuitivo incluso con variabili generiche</li><li>Le query utilizzano i dati del set di dati specifico, in quanto è l’unico</li></ul> | Le query possono utilizzare dati di Adobe Analytics e potenzialmente altre origini. |
| Suite di rapporti multiple | Con le variabili generiche non sono inclusi descrittori di nomi descrittivi. <br><br>**Esempio:** EVAR 2 | <ul><li>Qualsiasi campo con più descrittori viene visualizzato come generico. Ciò significa che nell’interfaccia utente non vengono visualizzati nomi descrittivi.</li><li>Le query possono utilizzare dati di qualsiasi set di dati che contiene l’eVar, il che può causare risultati misti o errati.</li></ul> | Le query utilizzano correttamente i risultati combinati da più set di dati. |

### Tipi di pubblico

Il **[!UICONTROL Tipi di pubblico]** Questa scheda elenca tutti i tipi di pubblico importati da origini esterne, ad esempio Adobe Audience Manager, e quelli creati in [!DNL Experience Platform].

Il giorno **[!UICONTROL Tipi di pubblico]** , è possibile visualizzare tutte le origini disponibili come un gruppo di cartelle. Quando selezioni le cartelle, puoi visualizzare le sottocartelle e i tipi di pubblico disponibili. Inoltre, è possibile selezionare l&#39;icona della cartella (come mostrato nell&#39;immagine a destra) per visualizzare la struttura della cartella (un segno di spunta indica la cartella in cui ci si trova attualmente) e tornare facilmente alle cartelle selezionando il nome di una cartella nella struttura.

Puoi passare il cursore del mouse sull’ⓘ accanto a un pubblico per visualizzare informazioni su di esso, tra cui l’ID, la descrizione e la gerarchia delle cartelle per individuare il pubblico.

![Immagine che illustra il funzionamento della gerarchia di cartelle per i tipi di pubblico.](../images/ui/segment-builder/audience-folder-structure.png)

Puoi anche cercare i tipi di pubblico utilizzando la barra di ricerca, che utilizza [Sintassi di ricerca di Lucene](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). Il giorno **[!UICONTROL Tipi di pubblico]** , selezionando una cartella di livello superiore viene visualizzata la barra di ricerca, che consente di eseguire ricerche all&#39;interno di tale cartella. I risultati della ricerca iniziano a essere compilati solo dopo l&#39;immissione di parole intere. Ad esempio, per trovare un pubblico denominato `Online Shoppers`, inizia a digitare &quot;Online&quot; nella barra di ricerca. Dopo aver digitato la parola &quot;Online&quot; completamente, vengono visualizzati i risultati della ricerca contenenti la parola &quot;Online&quot;.

## Area di lavoro del generatore di regole {#rule-builder-canvas}

Una definizione di segmento è una raccolta di regole utilizzate per descrivere le caratteristiche o il comportamento chiave di un pubblico target. Queste regole vengono create utilizzando l’area di lavoro del generatore di regole, situata al centro di [!DNL Segment Builder].

Per aggiungere una nuova regola alla definizione del segmento, trascina una tessera dalla sezione **[!UICONTROL Campi]** e rilasciarlo nell’area di lavoro del generatore di regole. Verranno quindi visualizzate opzioni specifiche per il contesto in base al tipo di dati aggiunti. I tipi di dati disponibili includono: stringhe, date, [!DNL ExperienceEvents], &quot;[!UICONTROL Tipi di evento]&quot;, e tipi di pubblico.

![Area di lavoro del generatore di regole vuoto.](../images/ui/segment-builder/rule-builder-canvas.png)

>[!IMPORTANT]
>
>Le ultime modifiche apportate a Adobe Experience Platform hanno aggiornato l’utilizzo di `OR` e `AND` operatori logici tra eventi. Questi aggiornamenti non influiranno sulle definizioni dei segmenti esistenti. Tuttavia, queste modifiche interesseranno tutti gli aggiornamenti successivi alle definizioni di segmenti esistenti e alle nuove definizioni di segmenti create. Leggi le [aggiornamento costanti di tempo](./segment-refactoring.md) per ulteriori informazioni.

Quando selezioni un valore per l’attributo, visualizzerai un elenco di valori enum possibili per l’attributo.

![Immagine che mostra l&#39;elenco dei valori enum consentiti per un attributo.](../images/ui/segment-builder/enum-list.png)

Se si seleziona un valore da questo elenco di enumerazioni, il valore viene evidenziato con un bordo solido. Tuttavia, per i campi che utilizzano `meta:enum` (soft) enum, puoi anche selezionare un valore che è **non** dall&#39;elenco delle enumerazioni. Se si crea un valore personalizzato, questo verrà evidenziato con un bordo punteggiato e un&#39;avvertenza che indica che il valore non è incluso nell&#39;elenco enumerazione.

![Avviso visualizzato se si inserisce un valore che non fa parte dell&#39;elenco enumerazione.](../images/ui/segment-builder/enum-warning.png)

Se crei più valori, puoi aggiungerli tutti contemporaneamente utilizzando il caricamento in blocco. Seleziona la ![icona più](../images/ui/segment-builder/plus-icon.png) per visualizzare **[!UICONTROL Aggiungi valori in blocco]** popover.

![Viene evidenziata l’icona più, con il pulsante che puoi selezionare per accedere al popover di caricamento in blocco.](../images/ui/segment-builder/add-bulk-values.png)

Il giorno **[!UICONTROL Aggiungi valori in blocco]** Popover, puoi caricare un file CSV o TSV.

![Viene visualizzato il popover Aggiungi valori in blocco. Viene evidenziata la finestra di dialogo che puoi selezionare per caricare un file CSV o TSV.](../images/ui/segment-builder/bulk-values-popover.png)

In alternativa, puoi aggiungere manualmente valori separati da virgole.

![Viene visualizzato il popover Aggiungi valori in blocco. Vengono evidenziate sia la finestra di dialogo che è possibile utilizzare per inserire i valori, sia i valori aggiunti.](../images/ui/segment-builder/bulk-values-comma-separated.png)

È consentito un massimo di 250 valori. Se superi questo limite, rimuovi alcuni valori prima di aggiungerne altri.

![Viene visualizzato un avviso che indica che è stato raggiunto il numero massimo di valori.](../images/ui/segment-builder/maximum-values.png)

### Aggiunta di tipi di pubblico

Puoi trascinare e rilasciare un pubblico dalla sezione **[!UICONTROL Pubblico]** scheda nell’area di lavoro del generatore di regole per fare riferimento all’appartenenza al pubblico nella nuova definizione di segmento. Ciò ti consente di includere o escludere l’iscrizione al pubblico come attributo nelle nuove regole di definizione del segmento.

Per [!DNL Platform] tipi di pubblico creati con [!DNL Segment Builder], è possibile convertire il pubblico nell’insieme di regole utilizzate nella definizione del segmento per quel pubblico. Questa conversione crea una copia della logica della regola, che può quindi essere modificata senza influire sulla definizione del segmento originale. Assicurati di aver salvato le modifiche recenti alla definizione del segmento prima di convertirla nella logica della regola.

>[!NOTE]
>
>Quando si aggiunge un pubblico da un’origine esterna, viene fatto riferimento solo all’iscrizione al pubblico. Non è possibile convertire il pubblico in regole e pertanto le regole utilizzate per creare il pubblico originale non possono essere modificate nella nuova definizione del segmento.

![Questa immagine mostra come convertire un attributo di pubblico in regole.](../images/ui/segment-builder/add-audience-to-segment.png)

Se insorgono conflitti durante la conversione dei tipi di pubblico in regole, [!DNL Segment Builder] tenterà di preservare al meglio le opzioni esistenti.

### Vista Codice

In alternativa, puoi visualizzare una versione basata su codice di una regola creata in [!DNL Segment Builder]. Dopo aver creato la regola nell’area di lavoro del generatore di regole, puoi selezionare **[!UICONTROL Vista Codice]** per visualizzare la definizione del segmento come PQL.

![Viene evidenziato il pulsante di visualizzazione del codice, che consente di visualizzare la definizione del segmento come PQL.](../images/ui/segment-builder/code-view.png)

La vista Codice fornisce un pulsante che consente di copiare il valore della definizione del segmento da utilizzare nelle chiamate API. Per ottenere la versione più recente della definizione del segmento, assicurati di aver salvato le modifiche più recenti alla definizione del segmento.

![Viene evidenziato il pulsante Copia codice, che consente di: ](../images/ui/segment-builder/copy-code.png)

### Funzioni di aggregazione

Un’aggregazione in [!DNL Segment Builder] è un calcolo su un gruppo di attributi XDM il cui tipo di dati è un numero (doppio o intero). Le quattro funzioni di aggregazione supportate nel Generatore di segmenti sono SUM, AVERAGE, MIN e MAX.

Per creare una funzione di aggregazione, seleziona un evento dalla barra a sinistra e inseriscilo nella [!UICONTROL Eventi] contenitore.

![Viene evidenziata la sezione Eventi.](../images/ui/segment-builder/events.png)

Dopo aver inserito l’evento nel contenitore Eventi, seleziona l’icona con i puntini di sospensione (...), seguita da **[!UICONTROL Aggregato]**.

![Il testo aggregato viene evidenziato. Selezionando questa opzione è possibile selezionare le funzioni di aggregazione.](../images/ui/segment-builder/add-aggregation.png)

L’aggregazione viene ora aggiunta. È ora possibile selezionare la funzione di aggregazione, scegliere l&#39;attributo da aggregare, la funzione di uguaglianza e il valore. Per l’esempio seguente, questa definizione del segmento qualificherebbe qualsiasi profilo con una somma di valori acquistati superiore a $ 100, anche se ogni singolo acquisto è inferiore a $ 100.

![Le regole di evento, che visualizzano una funzione di aggregazione.](../images/ui/segment-builder/filled-aggregation.png)

### Funzioni di conteggio {#count-functions}

Le funzioni di conteggio nel Generatore di segmenti vengono utilizzate per cercare eventi specifici e contare quante volte vengono eseguite. Le funzioni di conteggio supportate nel Generatore di segmenti sono &quot;Almeno&quot;, &quot;Al massimo&quot;, &quot;Esattamente&quot;, &quot;Tra&quot; e &quot;Tutto&quot;.

Per creare una funzione di conteggio, seleziona un evento dalla barra a sinistra e inseriscilo nella [!UICONTROL Eventi] contenitore.

![I campi degli eventi sono evidenziati.](../images/ui/segment-builder/events.png)

Dopo aver inserito l’evento nel contenitore Eventi, seleziona la [!UICONTROL Almeno 1] pulsante.

![Viene evidenziato Almeno, mostrando l&#39;area da selezionare per visualizzare un elenco completo delle funzioni di conteggio.](../images/ui/segment-builder/add-count.png)

Viene aggiunta la funzione conteggio. È ora possibile selezionare la funzione count e il valore della funzione. L’esempio seguente consiste nell’includere qualsiasi evento con almeno un clic.

![Viene visualizzato ed evidenziato un elenco delle funzioni di conteggio.](../images/ui/segment-builder/select-count.png)

## Contenitori

Le regole dei segmenti vengono valutate nell’ordine in cui sono elencate. I contenitori consentono di controllare l’ordine di esecuzione tramite l’utilizzo di query nidificate.

Dopo aver aggiunto almeno una sezione all’area di lavoro del generatore di regole, puoi iniziare ad aggiungere contenitori. Per creare un nuovo contenitore, seleziona i puntini di sospensione (...) nell’angolo in alto a destra della sezione, quindi seleziona **[!UICONTROL Aggiungi contenitore]**.

![Il pulsante Aggiungi contenitore è evidenziato e consente di aggiungere un contenitore come elemento secondario del primo contenitore.](../images/ui/segment-builder/add-container.png)

Un nuovo contenitore viene visualizzato come figlio del primo contenitore, ma è possibile regolare la gerarchia trascinando e spostando i contenitori. Il comportamento predefinito di un contenitore è &quot;[!UICONTROL Includi]&quot; l’attributo, l’evento o il pubblico fornito. Puoi impostare la regola su &quot;[!UICONTROL Escludi]&quot; profili che corrispondono ai criteri del contenitore selezionando **[!UICONTROL Includi]** nell’angolo in alto a sinistra della sezione e selezionando &quot;[!UICONTROL Escludi]&quot;.

È inoltre possibile estrarre un contenitore figlio e aggiungerlo in linea al contenitore padre selezionando &quot;unwrap container&quot; (Annulla wrapping contenitore) sul contenitore figlio. Seleziona i puntini di sospensione (...) nell’angolo in alto a destra del contenitore secondario per accedere a questa opzione.

![Vengono evidenziate le opzioni che consentono di decomprimere o eliminare il contenitore.](../images/ui/segment-builder/include-exclude.png)

Dopo aver selezionato **[!UICONTROL Annulla wrapping contenitore]** il contenitore figlio viene rimosso e i criteri vengono visualizzati in linea.

>[!NOTE]
>
>Quando rimuovi il wrapping dei contenitori, fai attenzione a che la logica continui a soddisfare la definizione del segmento desiderata.

![Il contenitore viene visualizzato dopo essere stato estratto.](../images/ui/segment-builder/unwrapped-container.png)

## Criteri di unione

>[!CONTEXTUALHELP]
>id="platform_segmentation_createSegment_segmentBuilder_mergePolicies"
>title="Criteri di unione"
>abstract="Un criterio di unione consente l’unione di set di dati diversi per formare il profilo. Platform ha fornito un criterio di unione predefinito, in alternativa puoi crearne uno nuovo in Profili. Scegli un criterio di unione che corrisponda allo scopo di marketing per questo pubblico."

[!DNL Experience Platform] consente di unire dati provenienti da più origini e combinarli per ottenere una visualizzazione completa di ciascuno dei singoli clienti. Quando si riuniscono questi dati, i criteri di unione sono le regole che [!DNL Platform] utilizza per determinare come assegnare la priorità ai dati e quali dati verranno combinati per creare un profilo.

Puoi selezionare un criterio di unione corrispondente allo scopo di marketing per questo pubblico o utilizzare il criterio di unione predefinito fornito da [!DNL Platform]. È possibile creare più criteri di unione specifici per l’organizzazione, inclusa la creazione di un criterio di unione predefinito. Per istruzioni dettagliate sulla creazione di criteri di unione per l&#39;organizzazione, leggere [panoramica dei criteri di unione](../../profile/merge-policies/overview.md).

Per selezionare un criterio di unione per la definizione del segmento, seleziona l’icona a forma di ingranaggio nella **[!UICONTROL Campi]** , quindi utilizza **[!UICONTROL Criterio di unione]** menu a discesa per selezionare il criterio di unione da utilizzare.

![Il selettore dei criteri di unione viene evidenziato. Questo consente di scegliere quale criterio di unione selezionare per la definizione del segmento.](../images/ui/segment-builder/merge-policy-selector.png)

## Proprietà della definizione di segmento {#segment-properties}

>[!CONTEXTUALHELP]
>id="platform_segments_createsegment_segmentbuilder_segmentproperties"
>title="Proprietà della definizione di segmento"
>abstract="Nella sezione Proprietà della definizione di segmento viene visualizzata una stima della dimensione del segmento risultante, con il numero di profili qualificati rispetto al numero totale di profili. Questo consente di regolare la definizione del segmento in base alle tue esigenze prima di creare il pubblico stesso."

>[!CONTEXTUALHELP]
>id="platform_segments_createsegment_segmentbuilder_refreshestimate"
>title="Aggiornare le stime"
>abstract="Puoi aggiornare le stime della definizione di segmento per visualizzare subito un’anteprima del numero di profili idonei per la definizione di segmento proposta. Le stime del pubblico sono generate utilizzando una dimensione del campione dei dati di esempio del giorno in questione."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/tutorials/create-a-segment.html?lang=it#estimate-and-preview-an-audience" text="Stimare e visualizzare in anteprima un pubblico"

Durante la creazione di una definizione di segmento, il **[!UICONTROL Proprietà segmento]** nella sezione a destra dell’area di lavoro viene visualizzata una stima delle dimensioni della definizione del segmento risultante, che consente di regolare la definizione del segmento in base alle esigenze prima di creare il pubblico stesso.

Il **[!UICONTROL Proprietà segmento]** Questa sezione consente inoltre di specificare informazioni importanti sulla definizione del segmento, tra cui nome, descrizione e tipo di valutazione. I nomi delle definizioni dei segmenti vengono utilizzati per identificare la definizione del segmento tra quelle definite dall’organizzazione e devono quindi essere descrittivi, concisi e univoci.

Continuando a creare la definizione del segmento, puoi visualizzare un’anteprima impaginata del pubblico selezionando **[!UICONTROL Visualizza profili]**.

![Viene evidenziata la sezione delle proprietà di definizione del segmento. Le proprietà di definizione del segmento includono, tra l’altro, il nome, la descrizione e il metodo di valutazione della definizione del segmento.](../images/ui/segment-builder/segment-properties.png)

>[!NOTE]
>
>Le stime del pubblico sono generate utilizzando una dimensione del campione dei dati di esempio del giorno in questione. Se nell’archivio dei profili sono presenti meno di 1 milione di entità, viene utilizzato l’intero set di dati; per un numero di entità compreso tra 1 e 20 milioni, vengono utilizzate 1 milione di entità e per più di 20 milioni di entità, viene utilizzato il 5% del totale delle entità. Ulteriori informazioni sulla generazione di stime per le definizioni dei segmenti sono disponibili nella sezione [sezione generazione della stima](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) dell’esercitazione sulla creazione di definizioni di segmenti.

Puoi anche selezionare il metodo di valutazione. Se si conosce il metodo di valutazione da utilizzare, è possibile selezionare il metodo di valutazione desiderato utilizzando l&#39;elenco a discesa. Se desideri conoscere i tipi di valutazione per i quali è qualificata questa definizione di segmento, puoi selezionare l’icona Sfoglia ![icona cartella con lente di ingrandimento](../images/ui/segment-builder/segment-evaluation-select-icon.png) per visualizzare un elenco dei metodi di valutazione delle definizioni dei segmenti disponibili.

Il [!UICONTROL Idoneità al metodo di valutazione] viene visualizzato popover. In questo popover vengono visualizzati i metodi di valutazione disponibili, ovvero batch, streaming e edge. Il popover mostra quali metodi di valutazione sono idonei e non idonei. A seconda dei parametri utilizzati nella definizione del segmento, questo potrebbe non essere idoneo per alcuni metodi di valutazione. Per ulteriori informazioni sui requisiti di ciascun metodo di valutazione, consultare la [segmentazione in streaming](./streaming-segmentation.md#query-types) o [segmentazione Edge](./edge-segmentation.md#query-types) panoramiche.

![Viene visualizzata la finestra a comparsa per l’idoneità del metodo di valutazione. Questo mostra quali metodi di valutazione sono idonei e non idonei per la definizione del segmento.](../images/ui/segment-builder/select-evaluation-method.png)

Se selezioni un metodo di valutazione non valido, ti verrà richiesto di modificare le regole di definizione del segmento o il metodo di valutazione.

![Viene visualizzato il metodo di valutazione. Se viene selezionato un metodo di valutazione non idoneo, il pop-up spiega perché non è idoneo.](../images/ui/segment-builder/ineligible-evaluation-method.png)

Ulteriori informazioni sui diversi metodi di valutazione delle definizioni dei segmenti sono disponibili nella sezione [panoramica sulla segmentazione](../home.md#evaluate-segments).

## Passaggi successivi {#next-steps}

Il Generatore di segmenti offre un flusso di lavoro avanzato che consente di isolare i tipi di pubblico commerciabili da [!DNL Real-Time Customer Profile] dati. Dopo aver letto questa guida, ora dovresti essere in grado di:

- Crea definizioni di segmenti utilizzando una combinazione di attributi, eventi e tipi di pubblico esistenti come blocchi predefiniti.
- Utilizza l’area di lavoro e i contenitori del generatore di regole per controllare l’ordine in cui vengono eseguite le regole dei segmenti.
- Visualizza le stime del tuo pubblico potenziale, consentendoti di regolare le definizioni dei segmenti in base alle esigenze.
- Abilita tutte le definizioni dei segmenti per la segmentazione pianificata.
- Abilita le definizioni di segmenti specificate per la segmentazione in streaming.

Per ulteriori informazioni su [!DNL Segmentation Service], continua a leggere la documentazione e completa il tuo percorso di apprendimento guardando i video correlati. Per ulteriori informazioni sulle altre parti del [!DNL Segmentation Service] Interfaccia utente, leggi [[!DNL Segmentation Service] guida utente](./overview.md)
