---
keywords: Experience Platform;guida utente;ia clienti;argomenti comuni;configurare istanza;creare istanza;
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Configurare un’istanza di Customer AI
description: I servizi AI/ML forniscono IA per l’analisi dei clienti come servizio Adobe Sensei semplice da utilizzare che può essere configurato per diversi casi d’uso. Le sezioni seguenti illustrano i passaggi per la configurazione di un’istanza di Customer AI.
exl-id: 78353dab-ccb5-4692-81f6-3fb3f6eca886
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '2827'
ht-degree: 0%

---


# Configurare un’istanza di Customer AI

IA per l’analisi dei clienti, parte dei servizi di IA/ML, consente di generare punteggi di propensione personalizzati senza doversi preoccupare dell’apprendimento automatico.

I servizi AI/ML forniscono IA per l’analisi dei clienti come servizio Adobe Sensei semplice da utilizzare che può essere configurato per diversi casi d’uso. Le sezioni seguenti illustrano i passaggi per la configurazione di un’istanza di Customer AI.

## Creare un’istanza {#set-up-your-instance}

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Servizi]** nel menu di navigazione a sinistra. Il **[!UICONTROL Servizi]** viene visualizzato il browser e vengono visualizzati tutti i servizi disponibili. Nel contenitore di IA per l’analisi dei clienti, seleziona **[!UICONTROL Apri]**.

![](../images/user-guide/navigate-to-service.png)

Il **IA per l’analisi dei clienti** Viene visualizzata l’interfaccia utente di e tutte le istanze del servizio.

- È possibile trovare **[!UICONTROL Profili totali valutati]** metrica situata nella parte inferiore destra del **[!UICONTROL Crea istanza]** contenitore. Questa metrica tiene traccia del numero totale di profili valutati da IA per l’analisi dei clienti per l’anno civile corrente, inclusi tutti gli ambienti sandbox ed eventuali istanze di servizio eliminate.

![](../images/user-guide/total-profiles.png)

Le istanze del servizio possono essere modificate, clonate ed eliminate utilizzando i controlli presenti sul lato destro dell’interfaccia utente. Per visualizzare questi controlli, seleziona un’istanza dal tuo **[!UICONTROL Istanze del servizio]**. I controlli contengono quanto segue:

- **[!UICONTROL Modifica]**: selezione **[!UICONTROL Modifica]** consente di modificare un’istanza di servizio esistente. Puoi modificare il nome, la descrizione e la frequenza di punteggio dell’istanza.
- **[!UICONTROL Clona]**: selezione **[!UICONTROL Clona]** copia la configurazione dell&#39;istanza del servizio attualmente selezionata. Puoi quindi modificare il flusso di lavoro per apportare modifiche minori e rinominarlo come nuova istanza.
- **[!UICONTROL Elimina]**: puoi eliminare un’istanza del servizio, comprese le esecuzioni storiche. Il set di dati di output corrispondente verrà eliminato da Platform. Tuttavia, i punteggi sincronizzati con Real-Time Customer Profile non vengono eliminati.
- **[!UICONTROL Origine dati]**: collegamento al set di dati utilizzato da questa istanza. Se vengono utilizzati più set di dati, quando si seleziona il testo del collegamento ipertestuale viene aperto il popover di anteprima del set di dati.
- **[!UICONTROL Dettagli ultima esecuzione]**: viene visualizzato solo quando un’esecuzione non riesce. Qui vengono visualizzate le informazioni sul motivo per cui l’esecuzione non è riuscita, ad esempio i codici di errore.
- **[!UICONTROL Definizione punteggio]**: panoramica rapida dell’obiettivo configurato per questa istanza.

![](../images/user-guide/service-instance-panel.png)

Per creare una nuova istanza, seleziona **[!UICONTROL Crea istanza]**.

![](../images/user-guide/dashboard.png)

## Configurazione

Viene visualizzato il flusso di lavoro per la creazione dell’istanza, che inizia con **[!UICONTROL Configurazione]** passaggio.

Di seguito sono riportate informazioni importanti sui valori che è necessario fornire all’istanza:

- **[!UICONTROL Nome]:** Il nome dell’istanza viene utilizzato in tutte le posizioni in cui vengono visualizzati i punteggi di Customer AI. Pertanto, i nomi devono descrivere cosa rappresentano i punteggi di previsione. Ad esempio, &quot;Probabilità di annullare l’abbonamento alla rivista&quot;.

- **[!UICONTROL Descrizione]:** Una descrizione che indica cosa stai cercando di prevedere.

- **[!UICONTROL Tipo tendenza]:** Il tipo di propensione determina l’intento del punteggio e della polarità della metrica. Puoi scegliere **[!UICONTROL Abbandono]** o **[!UICONTROL Conversione]**. Consulta la nota sotto [riepilogo punteggio](./discover-insights.md#scoring-summary) per ulteriori informazioni su come il tipo di propensione influisce sull’istanza, consulta il documento individuazione di insights.

![Schermata di configurazione](../images/user-guide/create-instance.png)

Immetti i valori richiesti, quindi seleziona **[!UICONTROL Successivo]** per continuare.

## Selezionare i dati {#select-data}

Per impostazione predefinita, IA per l’analisi dei clienti utilizza Adobe Analytics, Adobe Audience Manager, gli eventi esperienza in generale e i dati degli eventi esperienza del consumatore per calcolare i punteggi di tendenza. Quando selezioni un set di dati, vengono elencati solo quelli compatibili con IA per l’analisi dei clienti. Per selezionare un set di dati, seleziona la voce (**+**) accanto al nome del set di dati o seleziona la casella di controllo per aggiungere più set di dati contemporaneamente. Utilizza l’opzione di ricerca per trovare rapidamente i set di dati che ti interessano.

![Seleziona e cerca set di dati](../images/user-guide/configure-dataset-page-save-and-exit-cai.png)

Dopo aver selezionato i set di dati da utilizzare, seleziona la **[!UICONTROL Aggiungi]** per aggiungere i set di dati al riquadro di anteprima dei set di dati.

![Seleziona set di dati](../images/user-guide/select-datasets.png)

Selezione dell&#39;icona Info ![icona info](../images/user-guide/info-icon.png) accanto al set di dati apre il popover anteprima set di dati.

![Seleziona e cerca set di dati](../images/user-guide/dataset-info.png)

L’anteprima del set di dati contiene dati quali l’ora dell’ultimo aggiornamento, lo schema di origine e un’anteprima delle prime dieci colonne.

Seleziona **[!UICONTROL Salva]** per salvare le bozze durante lo spostamento lungo il flusso di lavoro. Puoi anche salvare le configurazioni del modello di bozza e passare al passaggio successivo nel flusso di lavoro. Utilizzare **[!UICONTROL Salva e continua]** per creare e salvare le bozze durante le configurazioni del modello. La funzione consente di creare e salvare le bozze della configurazione del modello ed è particolarmente utile quando è necessario definire molti campi nel flusso di lavoro di configurazione.

![Il flusso di lavoro Crea della scheda IA per l’analisi dei clienti di Data Science Services con Salva e salva e continua evidenziato.](../images/user-guide/cai-save-and-exit.png)

### Completezza del set di dati {#dataset-completeness}

Nell’anteprima del set di dati è presente un valore percentuale di completezza. Questo valore fornisce un’istantanea rapida del numero di colonne vuote o nulle nel set di dati. Se un set di dati contiene molti valori mancanti e questi valori vengono acquisiti altrove, è consigliabile includere il set di dati contenente i valori mancanti. In questo esempio l’ID persona è vuoto, tuttavia, l’ID persona viene acquisito in un set di dati separato che può essere incluso.

>[!NOTE]
>
>La completezza del set di dati viene calcolata utilizzando la finestra di formazione massima per IA per l’analisi dei clienti (un anno). Ciò significa che i dati che hanno più di un anno non vengono presi in considerazione durante la visualizzazione del valore di completezza del set di dati.

![Completezza del set di dati](../images/user-guide/dataset-info-2.png)

### Seleziona un’identità {#identity}

Ora puoi unire più set di dati in base alla mappa di identità (campo). Devi selezionare un tipo di identità (noto anche come &quot;spazio dei nomi delle identità&quot;) e un valore di identità all’interno di tale spazio dei nomi. Se hai assegnato più di un campo come identità all’interno dello schema nello stesso spazio dei nomi, tutti i valori di identità assegnati vengono visualizzati nel menu a discesa delle identità anteposto dallo spazio dei nomi, ad esempio `EMAIL (personalEmail.address)` o `EMAIL (workEmail.address)`.

[seleziona lo stesso spazio dei nomi](../images/user-guide/cai-identity-map.png)

>[!IMPORTANT]
>
>Per ogni set di dati selezionato deve essere utilizzato lo stesso tipo di identità (spazio dei nomi). Accanto al tipo di identità nella colonna Identity viene visualizzato un segno di spunta verde per indicare che i set di dati sono compatibili. Ad esempio, quando utilizzi lo spazio dei nomi del telefono e `mobilePhone.number` come identificatore, tutti gli identificatori per i set di dati rimanenti devono contenere e utilizzare lo spazio dei nomi Telefono.

Per selezionare un’identità, seleziona il valore sottolineato che si trova nella colonna Identità. Viene visualizzato il popover seleziona un’identità.

<!-- ![select same namespace](../images/user-guide/identity-type.png) -->
[seleziona lo stesso spazio dei nomi](../images/user-guide/cai-identity-namespace.png)

Se in uno spazio dei nomi sono disponibili più identità, assicurati di selezionare il campo di identità corretto per il caso d’uso. Ad esempio, nello spazio dei nomi dell’e-mail sono disponibili due identità e-mail: un’e-mail aziendale e personale. A seconda del caso d’uso, un’e-mail personale ha più probabilità di essere compilata ed è più utile nelle previsioni individuali. Ciò significa che `EMAIL (personalEmail.address)` come identità.

![Chiave set di dati non selezionata](../images/user-guide/select-identity.png)

>[!NOTE]
>
> Se non esiste un tipo di identità (spazio dei nomi) valido per un set di dati, è necessario impostare un’identità primaria e assegnarla a uno spazio dei nomi di identità utilizzando [editor schema](../../../xdm/schema/composition.md#identity). Per ulteriori informazioni sugli spazi dei nomi e sulle identità, visita [Spazi dei nomi di Identity Service](../../../identity-service/namespaces.md) documentazione.

## Definisci l’obiettivo {#define-a-goal}

<!-- https://www.adobe.com/go/cai-define-a-goal -->

Il **[!UICONTROL Definisci l’obiettivo]** Questo passaggio fornisce un ambiente interattivo che consente di definire visivamente un obiettivo di previsione. Un obiettivo è composto da uno o più eventi, in cui l’occorrenza di ogni evento è basata sulla condizione che contiene. L’obiettivo di un’istanza di IA per l’analisi dei clienti è determinare la probabilità di raggiungere il proprio obiettivo entro un determinato intervallo di tempo.

Per creare un obiettivo, seleziona **[!UICONTROL Inserisci il nome del campo]** e seguito da un campo dall’elenco a discesa. Selezionare il secondo input, una clausola per la condizione dell&#39;evento, quindi facoltativamente specificare il valore di destinazione per completare l&#39;evento. È possibile configurare altri eventi selezionando **[!UICONTROL Aggiungi evento]**. Infine, completa l’obiettivo applicando un intervallo di tempo di previsione in numero di giorni, quindi seleziona **[!UICONTROL Successivo]**.

<!-- ![](../images/user-guide/define-a-goal.png) -->
![](../images/user-guide/cai-define-a-goal.png)

### Si verifica e non si verifica

Quando definisci l’obiettivo, puoi selezionare **[!UICONTROL Si verificherà]** o **[!UICONTROL Non si verificherà]**. Selezione **[!UICONTROL Si verificherà]** significa che le condizioni evento definite devono essere soddisfatte affinché i dati dell’evento di un cliente possano essere inclusi nell’interfaccia utente di Insights.

Ad esempio, se desideri configurare un’app per prevedere se un cliente effettuerà un acquisto, puoi selezionare **[!UICONTROL Si verificherà]** seguito da **[!UICONTROL Tutti]** e quindi immetti **commerce.purchases.id** (o un campo analogo) e **[!UICONTROL esiste]** come operatore.

<!-- ![will occur](../images/user-guide/occur.png) -->
![si verificherà](../images/user-guide/cai-will-occur.png)

Tuttavia, ci possono essere casi in cui sei interessato a prevedere se un evento non si verificherà in un determinato arco temporale. Per configurare un obiettivo con questa opzione, seleziona **[!UICONTROL Non si verificherà]** dal menu a discesa di livello principale.

Ad esempio, se sei interessato a prevedere quali clienti saranno meno coinvolti e non visiti la pagina di accesso del tuo account nel mese successivo. Seleziona **[!UICONTROL Non si verificherà]** seguito da **[!UICONTROL Tutti]** e quindi immetti **web.webInteraction.URL** (o un campo analogo) e **[!UICONTROL è uguale a]** come operatore con **account-login** come valore.

![non si verificherà](../images/user-guide/not-occur.png)

### Tutti e uno di

In alcuni casi, può essere utile prevedere se si verificherà una combinazione di eventi e in altri casi, può essere utile prevedere il verificarsi di qualsiasi evento da un set predefinito. Per prevedere se un cliente avrà una combinazione di eventi, seleziona la **[!UICONTROL Tutti]** dall’elenco a discesa di secondo livello nella **[!UICONTROL Definisci obiettivo]** pagina.

Ad esempio, è possibile prevedere se un cliente acquista un particolare prodotto. Questo obiettivo predittivo è definito da due condizioni: `commerce.order.purchaseID` **esiste** e `productListItems.SKU` **è uguale a** un valore specifico.

![Tutti gli esempi](../images/user-guide/all-of.png)

Per prevedere se un cliente avrà un evento da un determinato set, puoi utilizzare **[!UICONTROL Qualsiasi di]** opzione.

Ad esempio, puoi prevedere se un cliente visita un determinato URL o una pagina web con un nome particolare. Questo obiettivo predittivo è definito da due condizioni: `web.webPageDetails.URL` **inizia con** un valore particolare e `web.webPageDetails.name` **inizia con** un valore particolare.

![Qualsiasi esempio](../images/user-guide/any-of.png)

### Popolazione ammissibile *(facoltativo)*

Per impostazione predefinita, i punteggi di tendenza vengono generati per tutti i profili, a meno che non sia specificata una popolazione idonea. Puoi specificare una popolazione idonea definendo le condizioni per includere o escludere i profili in base agli eventi.

![popolazione ammissibile](../images/user-guide/eligible-population.png)

### Eventi personalizzati (*facoltativo*) {#custom-events}

Se disponi di informazioni aggiuntive oltre a [campi evento standard](../data-requirements.md#standard-events) utilizzato da IA per l’analisi dei clienti per generare punteggi di tendenza, viene fornita un’opzione di eventi personalizzata. L’utilizzo di questa opzione consente di aggiungere altri eventi che ritieni influenti, il che può migliorare la qualità del modello e contribuire a fornire risultati più precisi. Se il set di dati selezionato include eventi personalizzati definiti nello schema, puoi aggiungerli all’istanza.

>[!NOTE]
>
> Per una spiegazione dettagliata di come gli eventi personalizzati influiscono sui risultati del punteggio di Customer AI, visita il [Esempio di evento personalizzato](#custom-event) sezione.

![funzione evento](../images/user-guide/event-feature.png)

Per aggiungere un evento personalizzato, seleziona **[!UICONTROL Aggiungi evento personalizzato]**. Quindi, inserisci un nome evento personalizzato da mappare al campo evento nello schema. I nomi degli eventi personalizzati vengono visualizzati al posto del valore dei campi quando si esaminano i fattori influenti e altre informazioni. Ciò significa che verrà utilizzato il nome dell’evento personalizzato invece dell’ID/valore dell’evento. Per ulteriori informazioni sulla modalità di visualizzazione degli eventi personalizzati, vedi [sezione di esempio di evento personalizzato](#custom-event). Questi eventi personalizzati aggiuntivi vengono utilizzati da IA per l’analisi dei clienti per migliorare la qualità del modello e fornire risultati più precisi.

![Campo Evento personalizzato](../images/user-guide/custom-event.png)

Quindi, seleziona l’operatore che desideri utilizzare dal menu a discesa degli operatori disponibili. Vengono elencati solo gli operatori compatibili con l’evento.

![Operatore evento personalizzato](../images/user-guide/custom-operator.png)

Infine, immetti i valori del campo se l’operatore selezionato ne richiede uno. In questo esempio, dobbiamo solo verificare se esiste una prenotazione di un hotel o ristorante. Tuttavia, se vogliamo essere più precisi, possiamo utilizzare l’operatore è uguale a e immettere un valore esatto nel prompt dei valori.

![Valore campo Evento personalizzato](../images/user-guide/custom-value.png)

Al termine, seleziona **[!UICONTROL Successivo]** in alto a destra per continuare.

### Attributi di profilo personalizzati (*facoltativo*)

Puoi definire importanti campi del set di dati profilo (con marche temporali) nei dati, oltre a [campi evento standard](../data-requirements.md#standard-events) utilizzato da IA per l’analisi dei clienti per generare punteggi di tendenza. L’utilizzo di questa opzione consente di aggiungere attributi di profilo aggiuntivi che ritieni influenti, il che può migliorare la qualità del modello e fornire risultati più precisi. Inoltre, l’aggiunta di attributi di profilo personalizzati consente ad IA per l’analisi dei clienti di mostrare meglio come determinati profili sono finiti in un bucket di propensione.

>[!NOTE]
>
>L’aggiunta di un attributo di profilo personalizzato segue lo stesso flusso di lavoro dell’aggiunta di un evento personalizzato. Analogamente agli eventi personalizzati, gli attributi di profilo personalizzati influiscono sul punteggio del modello nello stesso modo. Per una spiegazione dettagliata, visita [Esempio di evento personalizzato](#custom-event) sezione.

![aggiungere un attributo di profilo personalizzato](../images/user-guide/profile-attributes.png)

#### Seleziona gli attributi del profilo dall’esportazione dello snapshot del profilo

Puoi anche scegliere di includere gli attributi del profilo dall’esportazione giornaliera dello snapshot del profilo. Questi attributi vengono sincronizzati con l’esportazione dello snapshot del profilo e visualizzano l’ultimo valore disponibile.

>[!WARNING]
>
> Fai attenzione a non selezionare un attributo di profilo aggiornato in seguito all’obiettivo di previsione o altamente correlato con l’obiettivo di previsione. Questo causa la perdita di dati e il sovraadattamento del modello. Un esempio di tale attributo è `total_purchases_in_the_last_3_months` che prevede la conversione degli acquisti.

>[!NOTE]
>
>Il supporto per l’utilizzo degli attributi del profilo dall’esportazione delle istantanee UPS è disponibile nell’interfaccia utente su richiesta.

### Aggiunta di un esempio di evento personalizzato {#custom-event}

Nell’esempio seguente, un evento personalizzato e un attributo di profilo vengono aggiunti a un’istanza di Customer AI. L’obiettivo dell’istanza di IA per l’analisi dei clienti è prevedere la probabilità che un cliente acquisti un altro prodotto Luma nei successivi 60 giorni. Normalmente, i dati del prodotto sono collegati a uno SKU del prodotto. In questo caso, lo SKU è `prd1013`. Dopo aver addestrato/valutato il modello di IA per l’analisi dei clienti, questa SKU può essere collegata a un evento e visualizzata come fattore influente per un bucket di propensione.

IA per l’analisi dei clienti applica automaticamente la generazione di funzioni come &quot;Giorni da&quot; o &quot;Conteggi di&quot; a fronte di eventi personalizzati come **Guarda l’acquisto**. Se questo evento è stato considerato un fattore influente sul motivo per cui i clienti sono ad alta, media o bassa propensione, IA per l’analisi dei clienti lo visualizza come `Days since prd1013 purchase` o `Count of prd1013 purchase`. Creando questo evento come Custom, puoi assegnare all’evento un nuovo nome che ne faciliti la lettura. Ad esempio, `Days since Watch purchase`. Inoltre, IA per l’analisi dei clienti utilizza questo evento per la formazione e il punteggio, anche se non è un evento standard. Ciò significa che puoi aggiungere più eventi che pensi possano essere influenti e personalizzare ulteriormente il modello includendo dati come prenotazioni, registri di visitatori e altri eventi. L’aggiunta di questi punti dati aumenta ulteriormente l’accuratezza e la precisione del modello di IA per l’analisi dei clienti.

![esempio di evento personalizzato](../images/user-guide/custom-event-name.png)

## Impostare le opzioni

Il passaggio Imposta opzioni consente di configurare una pianificazione per automatizzare le esecuzioni delle previsioni, definire esclusioni di previsione per filtrare determinati eventi e attivare **[!UICONTROL Profilo]** on/off.

### Configurare una pianificazione *(facoltativo)* {#configure-a-schedule}

Per impostare una pianificazione del punteggio, inizia configurando il **[!UICONTROL Frequenza punteggio]**. È possibile pianificare l’esecuzione di esecuzioni automatizzate di previsioni su base settimanale o mensile.

![](../images/user-guide/schedule.png)

### Previsioni esclusioni *(facoltativo)*

Se il set di dati conteneva colonne aggiunte come dati di test, puoi aggiungere tale colonna o evento a un elenco di esclusione selezionando **[!UICONTROL Aggiungi esclusione]** quindi immetti il campo da escludere. Questo impedisce la valutazione degli eventi che soddisfano determinate condizioni durante la generazione dei punteggi. Questa funzione può essere utilizzata per filtrare gli input di dati o le promozioni irrilevanti.

Per escludere un evento, seleziona **[!UICONTROL Aggiungi esclusione]** e definisci l’evento. Per rimuovere un’esclusione, seleziona i puntini di sospensione (**[!UICONTROL ...]**) in alto a destra nel contenitore degli eventi, quindi seleziona **[!UICONTROL Rimuovi contenitore]**.

![](../images/user-guide/exclusion.png)

### Attiva/disattiva profilo

L’interruttore Profilo consente ad IA per l’analisi dei clienti di esportare i risultati del punteggio in Profilo cliente in tempo reale. La disattivazione di questa opzione impedisce l’aggiunta dei risultati del punteggio dei modelli al profilo. I risultati del punteggio di IA per l’analisi dei clienti sono ancora disponibili con questa funzione disabilitata.

Quando utilizzi Customer AI per la prima volta, puoi disattivare questa funzione fino a quando non sei soddisfatto dei risultati di output del modello. Questo impedisce di caricare più set di dati di punteggio nei profili cliente mentre ottimizzi il modello. Una volta completata la calibrazione del modello, potete clonarlo utilizzando [opzione clone](#set-up-your-instance) dal **Istanze del servizio** pagina. Questo consente di creare una copia del modello e attivare/disattivare il profilo.

![Attiva/disattiva profilo](../images/user-guide/advanced-workflow-save.png)

Una volta impostata la pianificazione del punteggio, incluse le esclusioni di previsione e l’interruttore di profilo in cui desideri che si trovi, seleziona **[!UICONTROL Fine]** in alto a destra per creare l’istanza di Customer AI.

Se l’istanza viene creata correttamente, viene immediatamente attivata un’esecuzione di previsione e le esecuzioni successive vengono eseguite in base alla pianificazione definita.

>[!NOTE]
>
>A seconda delle dimensioni dei dati di input, il completamento delle esecuzioni delle previsioni può richiedere fino a 24 ore.

Seguendo questa sezione, hai configurato un’istanza di Customer AI ed eseguito un’esecuzione di previsione. Al completamento dell’esecuzione, le informazioni con punteggio popolano automaticamente i profili con punteggi previsti se l’opzione di profilo è abilitata. Attendi fino a 24 ore prima di continuare con la sezione successiva di questa esercitazione.

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione, hai configurato correttamente un’istanza di IA per l’analisi dei clienti e generato punteggi di tendenza. Ora puoi scegliere di utilizzare il Generatore di segmenti per [creare segmenti di clienti con punteggi previsti](./create-segment.md) o [scoprire informazioni con Customer AI](./discover-insights.md).

## Risorse aggiuntive

Il seguente video è progettato per comprendere il flusso di lavoro di configurazione per Customer AI. Inoltre, vengono forniti esempi di best practice e casi d’uso.

>[!IMPORTANT]
>
> Il seguente video non è aggiornato. Per informazioni aggiornate, consulta la documentazione.

>[!VIDEO](https://video.tv.adobe.com/v/32665?learn=on&quality=12)
