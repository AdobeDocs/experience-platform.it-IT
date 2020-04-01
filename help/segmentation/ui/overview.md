---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guida all'interfaccia utente di Generatore di segmenti
topic: ui guide
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc

---


# Guida utente di Segment Builder

Adobe Experience Platform Segmentation Service offre un&#39;API RESTful e un&#39;interfaccia utente per la creazione di definizioni di segmenti dai dati del profilo cliente in tempo reale.

## Introduzione

Per utilizzare le definizioni dei segmenti è necessario conoscere i diversi servizi della piattaforma Experience Manager relativi alla segmentazione. Prima di leggere questa guida utente, consulta la documentazione relativa ai seguenti servizi:

- [Servizio](../home.md)segmentazione: Il servizio di segmentazione consente di dividere i dati memorizzati in Experience Platform che riguardano individui (come clienti, potenziali, utenti o organizzazioni) in gruppi più piccoli che condividono caratteristiche simili e risponderanno in modo simile alle strategie di marketing.
- [Profilo](../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.
- [Servizio](../../identity-service/home.md)identità: Abilita il profilo cliente in tempo reale collegando identità da origini dati diverse che vengono caricate nella piattaforma.
- [Experience Data Model (XDM)](../../xdm/home.md): Il framework standardizzato tramite il quale la piattaforma organizza i dati sull&#39;esperienza cliente.

È inoltre importante conoscere due termini chiave utilizzati in questo documento e comprendere la differenza tra questi:
- **Definizione** segmento: Set di regole utilizzato per descrivere le caratteristiche o i comportamenti chiave di un&#39;audience di destinazione.
- **Pubblico**: Set di profili risultante che soddisfano i criteri di una definizione di segmento.

## Accesso alle definizioni dei segmenti

Per iniziare a lavorare con le definizioni dei segmenti in Adobe Experience Platform, fai clic su **Segmenti** nella barra di navigazione a sinistra. Per visualizzare tutte le definizioni di segmento per la tua organizzazione, fai clic sulla scheda *Sfoglia* . Questa visualizzazione elenca informazioni sulla definizione del segmento, incluso il metodo di valutazione, la data di creazione e l’ultima data di modifica.

Il metodo di valutazione può essere in streaming o batch. I segmenti di streaming vengono valutati costantemente quando i dati entrano nel sistema. I segmenti batch vengono valutati in base a una pianificazione prestabilita.

I segmenti batch presentano informazioni aggiuntive, che mostrano sia la data dell&#39;ultima valutazione, sia la data della valutazione successiva per il batch.

Facendo clic su **Crea segmento** nell’angolo in alto a destra si apre l’area di lavoro Generatore di segmenti, in cui potete iniziare a creare una definizione di segmento.

![](../images/segment-builder/segment-browse.png)

## Area di lavoro Generatore di segmenti

Segment Builder (Generatore di segmenti) fornisce un’area di lavoro completa che consente di interagire con gli elementi dati del profilo. L’area di lavoro offre controlli intuitivi per la creazione e la modifica di regole, come le sezioni di trascinamento utilizzate per rappresentare le proprietà dei dati.

![](../images/segment-builder/segment-builder.png)

## Blocchi di generazione delle definizioni dei segmenti

I mattoni base delle definizioni dei segmenti sono **Attributi** ed **Eventi**. Inoltre, gli attributi e gli eventi contenuti in **Audience** esistenti possono essere utilizzati anche come componenti per le nuove definizioni.

Puoi vedere questi blocchi costitutivi nella sezione *Campi* sul lato sinistro dell’area di lavoro Generatore di segmenti. *I campi* contengono una scheda per ciascuno dei blocchi predefiniti principali: **Attributi**, **Eventi** e **Audience**.

![](../images/segment-builder/segment-fields.png)

### Attributi

La scheda **Attributi** consente di sfogliare gli attributi Profilo appartenenti alla classe Profilo singolo XDM. Ogni cartella può essere espansa per rivelare altri attributi, in cui ogni attributo è una sezione che può essere trascinata sul quadro del generatore di regole al centro dell’area di lavoro. Il quadro del generatore di [regole](#rule-builder-canvas) viene discusso più dettagliatamente più avanti in questa guida.

![](../images/segment-builder/attributes.png)

### Eventi

La scheda **Eventi** consente di creare un pubblico basato su eventi o azioni che si sono verificati utilizzando gli elementi dati XDM ExperienceEvent. Potete anche trovare i tipi di evento nella scheda **Eventi** , una raccolta di eventi di uso comune che consente di creare i segmenti più rapidamente.

Oltre a essere in grado di cercare gli elementi ExperienceEvent, potete anche cercare i tipi di evento. I tipi di evento utilizzano la stessa logica di codifica di ExperienceEvents, senza che sia necessario cercare l&#39;evento corretto nella classe ExperienceEvent XDM. Ad esempio, utilizzando la barra di ricerca per cercare &quot;carrello&quot;, vengono restituiti i tipi di evento &quot;AddCart&quot; e &quot;RemoveCart&quot;, due azioni carrello utilizzate di frequente durante la creazione delle definizioni dei segmenti.

Per cercare qualsiasi tipo di componente, digitatene il nome nella barra di ricerca, che utilizza la sintassi [di ricerca di](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)Lucene. I risultati della ricerca iniziano a essere compilati man mano che vengono inserite parole intere. Ad esempio, per creare una regola basata sul campo XDM `ExperienceEvent.commerce.productViews`, iniziate a digitare &quot;product views&quot; nel campo di ricerca. Una volta digitata la parola &quot;prodotto&quot;, i risultati della ricerca iniziano a comparire. Ogni risultato include la gerarchia di oggetti alla quale appartiene.

>[!NOTE] I campi dello schema personalizzato definiti dall&#39;organizzazione possono richiedere fino a 24 ore per essere visualizzati e diventare disponibili per l&#39;uso nelle regole di creazione.

Puoi quindi trascinare facilmente ExperienceEvents e Event Types nella definizione del segmento.

![](../images/segment-builder/events-eventTypes.png)

Per impostazione predefinita, vengono visualizzati solo i campi dello schema compilati dall&#39;archivio dati. Ciò include i tipi di evento. Se l&#39;elenco Tipi evento non è visibile, oppure è possibile selezionare &quot;Qualsiasi&quot; solo come tipo di evento, fare clic sull&#39;icona a forma di ingranaggio accanto a *Campi*, quindi selezionare **Mostra schema** XDM completo sotto Campi ** disponibili. Fate di nuovo clic sull&#39;icona a forma di ingranaggio per tornare alla scheda *Campi* e dovreste essere in grado di visualizzare più tipi di evento e campi dello schema, indipendentemente dal fatto che contengano o meno dati.

![](../images/segment-builder/show-populated.png)

### Audiences

La scheda **Audiences** elenca tutte le audience importate da origini esterne, come Adobe Audience Manager, nonché quelle create all&#39;interno di Experience Platform.

Nella scheda Audiences (Audience) puoi vedere tutte le origini disponibili come un gruppo di cartelle. Facendo clic su queste cartelle, è possibile visualizzare le sottocartelle e le audience disponibili. Inoltre, potete fare clic sull’icona della cartella (come illustrato nell’immagine all’estrema destra) per visualizzare la struttura delle cartelle (un segno di spunta indica la cartella in cui ci si trova attualmente) e navigare facilmente tra le cartelle facendo clic sul nome di una cartella nella struttura.

Puoi passare il cursore del mouse sul ⓘ accanto a un&#39;audience per visualizzare le informazioni relative a quest&#39;ultima, inclusi il relativo ID, la descrizione e la gerarchia di cartelle per individuare l&#39;audience.

![](../images/segment-builder/audience-folder-structure.png)

Potete anche cercare Audiences utilizzando la barra di ricerca, che utilizza la sintassi [di ricerca di](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)Lucene. Nella scheda *Audiences* , quando si seleziona una cartella di livello superiore viene visualizzata la barra di ricerca, che consente di effettuare ricerche all&#39;interno di tale cartella. I risultati della ricerca iniziano a essere compilati solo dopo l&#39;immissione di intere parole. Ad esempio, per trovare un pubblico con nome `Online Shoppers`, iniziate a digitare &quot;Online&quot; nella barra di ricerca. Una volta digitata la parola &quot;Online&quot;, vengono visualizzati i risultati della ricerca contenenti la parola &quot;Online&quot;.

## Area di lavoro del generatore di regole

Una definizione di segmento è una raccolta di regole utilizzate per descrivere le caratteristiche o il comportamento chiave di un&#39;audience target. Queste regole vengono create utilizzando l&#39;area di lavoro del generatore di *regole*, situata al centro di Segment Builder (Generatore di segmenti).

Per aggiungere una nuova regola alla definizione del segmento, trascinate una sezione dalla scheda *Campi* e rilasciatela nell’area di lavoro del generatore di regole. Verranno quindi presentate opzioni specifiche per il contesto in base al tipo di dati aggiunto. I tipi di dati disponibili includono: stringhe, date, ExperienceEvents, tipi di eventi e audience.

![](../images/segment-builder/rule-builder-canvas.png)

### Aggiunta di audience

Puoi trascinare un&#39;audience dalla scheda *Audience* nell&#39;area di lavoro del generatore di regole per fare riferimento all&#39;appartenenza all&#39;audience nella nuova definizione di segmento. Questo consente di includere o escludere l&#39;appartenenza all&#39;audience come attributo nella nuova regola del segmento.

Per i tipi di pubblico della piattaforma creati con Segment Builder (Generatore di segmenti), potete scegliere di convertire l&#39;audience in un set di regole utilizzate nella definizione del segmento per quel tipo di pubblico. Questa conversione crea una copia della logica della regola, che può essere modificata senza influenzare la definizione del segmento originale.

>[!NOTE] Quando si aggiunge un&#39;audience da un&#39;origine esterna, viene fatto riferimento solo all&#39;appartenenza all&#39;audience. Non è possibile convertire l&#39;audience in regole, pertanto le regole utilizzate per creare l&#39;audience originale non possono essere modificate nella nuova definizione di segmento.

![](../images/segment-builder/add-audience-to-segment.png)

## Contenitori

Le regole del segmento vengono valutate nell&#39;ordine in cui sono elencate. I contenitori consentono il controllo dell&#39;ordine di esecuzione mediante l&#39;uso di query nidificate.

Dopo aver aggiunto almeno una sezione al quadro del generatore di regole, potete iniziare ad aggiungere contenitori. Per creare un nuovo contenitore, fate clic sulle ellissi (...) nell’angolo superiore destro della sezione, quindi fate clic su **Aggiungi contenitore**.

![](../images/segment-builder/add-container.png)

Un nuovo contenitore viene visualizzato come secondario del primo contenitore, ma è possibile regolare la gerarchia trascinando e spostando i contenitori. Il comportamento predefinito di un contenitore è &quot;Includi&quot; l&#39;attributo, l&#39;evento o l&#39;audience forniti. Per impostare la regola su &quot;Escludi&quot; profili che corrispondono ai criteri del contenitore, fate clic su **Includi** nell’angolo superiore sinistro della sezione e selezionate &quot;Escludi&quot;.

È inoltre possibile estrarre e aggiungere un contenitore secondario al contenitore principale facendo clic su &quot;unwrapper contenitore&quot; nel contenitore secondario. Fate clic sulle ellissi (...) nell’angolo superiore destro del contenitore secondario per accedere a questa opzione.

![](../images/segment-builder/include-exclude.png)

Dopo aver fatto clic su **Annulla racchiudi in un contenitore** , il contenitore secondario viene rimosso e i criteri vengono visualizzati in linea.

>[!NOTE] Quando si estrae un contenitore, prestate attenzione affinché la logica continui a soddisfare la definizione del segmento desiderata.

![](../images/segment-builder/unwrapped-container-inline.png)

## Unisci criteri

Experience Platform consente di unire dati provenienti da più fonti e combinarli per visualizzare una visione completa di ogni singolo cliente. Quando si uniscono questi dati, i criteri di unione sono le regole utilizzate dalla piattaforma per determinare in che modo i dati verranno classificati come priorità e quali dati verranno combinati per creare un profilo.

È possibile selezionare un criterio di unione che corrisponda allo scopo di marketing per questo pubblico o utilizzare il criterio di unione predefinito fornito da Piattaforma. È possibile creare più criteri di unione univoci per l&#39;organizzazione, inclusa la creazione di criteri di unione predefiniti. Per istruzioni dettagliate sulla creazione di criteri di unione per l&#39;organizzazione, vedere l&#39;esercitazione sull&#39; [utilizzo dei criteri di unione nell&#39;interfaccia utente](../../profile/ui/merge-policies.md).

Per selezionare un criterio di unione per la definizione del segmento, fare clic sull&#39;icona a forma di ingranaggio nella scheda *Campi* , quindi utilizzare il menu *a discesa* Unisci criteri per selezionare il criterio di unione che si desidera utilizzare.

![](../images/segment-builder/merge-policy-selector.png)

## Proprietà dei segmenti

Quando si crea una definizione di segmento, la sezione Proprietà ** segmento sul lato destro dell&#39;area di lavoro mostra una stima delle dimensioni del segmento risultante, consentendo di regolare la definizione del segmento come necessario prima di creare il pubblico stesso.

La sezione Proprietà ** segmento consente inoltre di specificare informazioni importanti sulla definizione del segmento, inclusi *Nome* e *Descrizione*. I nomi delle definizioni dei segmenti vengono utilizzati per identificare il segmento tra quelli definiti dall’organizzazione e devono pertanto essere descrittivi, concisi e univoci.

Mentre continuate a generare la definizione del segmento, potete visualizzare un&#39;anteprima impaginata del pubblico selezionando **Visualizza profili**.

![](../images/segment-builder/segment-properties.png)

>[!NOTE] Le stime dell&#39;audience vengono generate utilizzando una dimensione di esempio dei dati di quel giorno. Se nell&#39;archivio profili sono presenti meno di 1 milione di entità, viene utilizzato l&#39;intero set di dati; per un periodo compreso tra 1 e 20 milioni di entità, sono utilizzate 1 milione di entità; e per oltre 20 milioni di entità, viene utilizzato il 5% del totale delle entità. Ulteriori informazioni sulla generazione delle stime dei segmenti sono disponibili nella sezione [Generazione delle](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) stime dell’esercitazione sulla creazione dei segmenti.

## Abilita segmentazione pianificata

Una volta create le definizioni dei segmenti, potete valutarle tramite una valutazione su richiesta o pianificata (continua). Valutazione significa spostare i dati del profilo cliente in tempo reale attraverso le definizioni del segmento per produrre audience corrispondenti. Una volta creati, i tipi di pubblico vengono salvati e memorizzati in modo che possano essere esportati tramite le API di Experience Platform.

La valutazione su richiesta prevede l&#39;utilizzo dell&#39;API per eseguire la valutazione e generare audience in base alle esigenze, mentre la valutazione programmata (nota anche come &quot;segmentazione pianificata&quot;) consente di creare una pianificazione periodica per valutare le definizioni dei segmenti in un momento specifico (al massimo, una volta al giorno).

Per abilitare le definizioni dei segmenti per la valutazione pianificata, puoi utilizzare l’interfaccia utente o l’API. Nell’interfaccia utente, tornate alla scheda *Sfoglia* all’interno di **Segmenti** e selezionate **Valuta tutti i segmenti**. In questo modo tutti i segmenti verranno valutati in base alla pianificazione impostata dall&#39;organizzazione.

>[!NOTE] La valutazione pianificata può essere abilitata per le sandbox con un massimo di cinque (5) criteri di unione per il profilo individuale XDM. Se l&#39;organizzazione dispone di più di cinque criteri di unione per il profilo individuale XDM all&#39;interno di un unico ambiente sandbox, non sarà possibile utilizzare la valutazione pianificata.

Le pianificazioni al momento possono essere create solo tramite l&#39;API. Per informazioni dettagliate sulla creazione, la modifica e l&#39;utilizzo delle pianificazioni tramite l&#39;API, seguite l&#39;esercitazione per valutare e accedere ai risultati dei segmenti, in particolare la sezione sulla valutazione [pianificata tramite l&#39;API](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![](../images/segment-builder/scheduled-segmentation.png)

## Abilita segmentazione in streaming

>[!NOTE] La segmentazione in streaming è una funzione beta ed è disponibile su richiesta.

Inoltre, una definizione di segmento può essere abilitata per la segmentazione in streaming prima o dopo la creazione. La segmentazione in streaming valuta istantaneamente un cliente non appena un evento entra in un particolare gruppo di segmenti. Grazie a questa funzionalità, ora è possibile valutare la maggior parte delle regole del segmento quando i dati vengono passati in Piattaforma, il che significa che l&#39;appartenenza al segmento verrà mantenuta aggiornata senza eseguire processi di segmentazione pianificati. Per informazioni più dettagliate sulla segmentazione in streaming, consulta la documentazione [sulla segmentazione in](../api/streaming-segmentation.md)streaming.

Per abilitare le definizioni dei segmenti per lo streaming, puoi utilizzare l’interfaccia utente o l’API. Per abilitare una definizione di segmento nuova o esistente per lo streaming nell&#39;interfaccia utente, è necessario attivare l&#39;opzione *Streaming* su **ON**.

![](../images/segment-builder/enable-streaming-segmentation.png)

Una volta attivata la segmentazione in streaming, è necessario stabilire una linea di base (si tratta dell’esecuzione iniziale dopo la quale il segmento sarà sempre aggiornato). Il sistema gestisce automaticamente la gestione della base, tuttavia ciò è possibile solo se è stata abilitata la segmentazione pianificata. Per informazioni dettagliate sull&#39;abilitazione della segmentazione pianificata, consultate [la sezione precedente in questa guida](#enable-scheduled-segmentation)utente.

## Passaggi successivi

Segment Builder (Generatore di segmenti) offre un flusso di lavoro avanzato che consente di isolare i tipi di pubblico commerciabili dai dati del profilo cliente in tempo reale. Dopo aver letto questa guida, è ora possibile:

- Crea le definizioni dei segmenti utilizzando una combinazione di attributi, eventi e audience esistenti come elementi costitutivi.
- Utilizzate l&#39;area di lavoro e i contenitori del generatore di regole per controllare l&#39;ordine in cui vengono eseguite le regole del segmento.
- Visualizzare le stime del pubblico potenziale, per regolare le definizioni dei segmenti in base alle esigenze.
- Abilita tutte le definizioni di segmento per la segmentazione pianificata.
- Abilita le definizioni di segmento specificate per la segmentazione in streaming.

Per istruzioni dettagliate sull&#39;utilizzo del servizio di segmentazione tramite l&#39;API del profilo cliente in tempo reale, consulta l&#39;esercitazione sulla [creazione di segmenti di pubblico tramite API](../tutorials/create-a-segment.md) .