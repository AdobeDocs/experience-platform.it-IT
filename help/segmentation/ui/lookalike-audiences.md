---
solution: Experience Platform
title: Tipi di pubblico simili
description: Scopri come eseguire il targeting di nuovi tipi di pubblico di alto valore in Adobe Experience Platform utilizzando tipi di pubblico simili.
badgeLimitedAvailability: label="Disponibilità limitata" type=Caution
exl-id: c43dac6c-18a0-482f-803e-b75e1b211e98
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '2121'
ht-degree: 10%

---

# Guida ai tipi di pubblico simili

>[!IMPORTANT]
>
>Tieni presente che le informazioni e i tipi di pubblico simili sono in **disponibilità limitata**.

In Adobe Experience Platform, i tipi di pubblico per similarità forniscono informazioni intelligenti su ciascuno dei tipi di pubblico, sfruttando le informazioni basate sull’apprendimento automatico per identificare e indirizzare i clienti di alto valore con le campagne di marketing.

Con i tipi di pubblico simili, puoi creare tipi di pubblico espansi per rivolgerti a clienti con prestazioni simili a quelle dei tuoi tipi di pubblico con prestazioni migliori, oppure rivolgerti a clienti simili ai tipi di pubblico convertiti in precedenza.

## Terminologia {#terminology}

Prima di iniziare a utilizzare tipi di pubblico simili, assicurati di comprendere i seguenti concetti:

- **Pubblico di base**: il pubblico di base è il pubblico di cui desideri scoprire ulteriori informazioni. Questo è il pubblico del modello lookalike **basato su** su.
- **Modello lookalike**: un modello lookalike è un modello di apprendimento automatico che viene addestrato su ogni pubblico di base idoneo senza alcun input da parte del cliente. Ogni modello lookalike crea i fattori influenti e i grafici di somiglianza. Un modello lookalike **non** ottenere un punteggio.
- **Pubblico simile**: un pubblico per similarità è il pubblico che viene creato quando al pubblico di base viene applicato un modello lookalike con una soglia di similarità selezionata. Puoi creare più tipi di pubblico per similarità utilizzando lo stesso modello per similarità. Il pubblico per somiglianza è ciò che viene valutato.
- **Dimensione totale del pubblico indirizzabile**: la dimensione totale del pubblico indirizzabile corrisponde al numero totale di profili negli ultimi 30 giorni meno la popolazione del pubblico di base negli ultimi 30 giorni. Ad esempio, se un cliente ha 10 milioni di profili negli ultimi 30 giorni e il pubblico di base ha 1 milione di profili negli ultimi 30 giorni, la dimensione totale del pubblico indirizzabile è di 9 milioni di profili.

## Dettagli del modello Look-Alike {#details}

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_notEligible"
>title="Non idoneo"
>abstract="Questo pubblico non è attualmente idoneo per approfondimenti look-alike poiché potrebbe non raggiungere il numero minimo di profili richiesti per la formazione oppure l’esportazione del profilo non è stata ancora attivata."

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_processing"
>title="Elaborazione"
>abstract="Questo pubblico è attualmente in fase di elaborazione. Il modello potrebbe richiedere fino a 24 ore per completare l’elaborazione. Riprova più tardi."

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_error"
>title="Errore"
>abstract="Si è verificato un errore durante l’elaborazione del modello. Elimina e compila nuovamente questo modello o riprova più tardi."

In Adobe Experience Platform, il modello lookalike utilizza tre diversi tipi di punti dati:

- Iscrizione al pubblico negli ultimi 30 giorni
- Esperienza degli eventi degli ultimi 30 giorni acquisiti nel profilo cliente in tempo reale
- Attributi del profilo acquisiti negli ultimi 30 giorni nel profilo cliente in tempo reale

Tutti questi punti dati vengono trasformati in coppie di valori chiave che vengono inserite nel modello lookalike. Verranno mantenute solo le coppie di valori chiave con una percentuale significativa di profili corrispondenti.

In questo momento, il modello lookalike viene eseguito ogni 24 ore, creando e ricreando i fattori influenti e i grafici di somiglianza per il pubblico di base. Anche il punteggio per i tipi di pubblico simili viene eseguito frequentemente.

## Diritti {#entitlements}

I seguenti diritti si applicano all’utilizzo di tipi di pubblico simili:

- I clienti di Real-Time CDP Prime hanno diritto a **5** tipi di pubblico simili attivi nelle sandbox di produzione
- I clienti di Real-Time CDP Ultimate hanno diritto a **20** tipi di pubblico simili attivi nelle sandbox di produzione
- Le sandbox di sviluppo sono limitate a **5** Tipi di pubblico simili per tutti i clienti Real-Time CDP

I pacchetti di componenti aggiuntivi, che saranno disponibili in un secondo momento, aumentano le adesioni per le sandbox di produzione di 20 tipi di pubblico simili per pacchetto.

Per confermare se hai accesso a tipi di pubblico simili, contatta il tuo rappresentante di Adobe.

## Visualizzare informazioni simili {#view}

Le informazioni simili sono integrate nella pagina dei dettagli del pubblico. Per esaminare le informazioni simili relative a un pubblico, seleziona **[!UICONTROL Tipi di pubblico]** nella barra di navigazione a sinistra, seguito da **[!UICONTROL Sfoglia]** e il pubblico per cui desideri visualizzare le informazioni.

![Viene evidenziato il pulsante Tipi di pubblico e il pubblico di base utilizzato per la modellazione lookalike.](../images/ui/lookalike-audiences/browse.png)

Viene visualizzata la pagina dei dettagli del pubblico. Seleziona **[!UICONTROL Informazioni simili]** per visualizzare le informazioni simili del pubblico. Il **[!UICONTROL Informazioni simili]** viene visualizzata. Questa pagina presenta tre elementi principali: il grafico delle somiglianze e della portata, i tipi di pubblico simili e i fattori influenti.

![Viene evidenziata la scheda Approfondimenti simili, che mostra gli approfondimenti simili per il pubblico di base.](../images/ui/lookalike-audiences/look-alike-insights.png)

### Somiglianza e portata {#similarity-and-reach}

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_similarityAndReach"
>title="Somiglianza e portata"
>abstract="Il grafico di somiglianza e portata rappresenta la portata prevista di un pubblico Look-Alike costituito da profili al di sopra di un dato punteggio di somiglianza. Puoi passare il cursore del mouse su un punto specifico del grafico per visualizzare la percentuale di somiglianza e il numero di profili previsto per il punto attualmente evidenziato."

La sezione similarità e portata mostra un grafico che rappresenta la portata prevista di un pubblico simile costituito da profili al di sopra di un determinato punteggio di somiglianza. Il punteggio di somiglianza rappresenta **distanza** somiglianza tra il profilo del pubblico di base e il profilo di approfondimenti simili.

![Il grafico di somiglianza e portata viene evidenziato.](../images/ui/lookalike-audiences/similarity-and-reach.png)

In questo grafico, l’asse x misura la percentuale di somiglianza tra un profilo e i membri del pubblico selezionato. Il punteggio di somiglianza varia da 0% a 100%, con un punteggio di somiglianza più alto che indica che un profilo è più vicino, in termini di valori dei fattori influenti, ai membri del pubblico selezionato.

L’asse y mostra il conteggio previsto dei profili con la percentuale di similarità corrispondente al valore corrispondente dell’asse x. Il numero previsto di profili varia da 0 alla dimensione totale del pubblico indirizzabile o 25 milioni di profili, a seconda di quale valore sia inferiore. Questo asse è misurato su un **scala logaritmica** per migliorare la leggibilità del grafico.

Il grafico è **cumulativo** da destra a sinistra. Ciò significa che in qualsiasi punto del grafico, il valore dell’asse y è il numero di profili che hanno una similarità **sopra** la soglia di somiglianza. Ad esempio, se l’asse x è al 60% e l’asse y è a 10 milioni, significa che ci sono 10 milioni di profili che hanno una somiglianza pari o superiore al 60% con il pubblico di base.

Puoi passare il cursore del mouse su un punto specifico del grafico per visualizzare la percentuale di somiglianza e il numero di profili previsto per il punto attualmente evidenziato.

### Tipi di pubblico simili {#list}

La sezione Tipi di pubblico simili visualizza un elenco di tutti i tipi di pubblico simili creati in precedenza per il pubblico di base selezionato.

![Viene evidenziata la sezione Tipi di pubblico simili.](../images/ui/lookalike-audiences/select-laa.png)

### Fattori di influenza {#influential-factors}

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_influentialFactors"
>title="Fattori di influenza"
>abstract="I fattori di influenza sono attributi, eventi e appartenenze al pubblico importanti per spiegare la somiglianza di un profilo con i membri del pubblico di base. Le etichette e i criteri di utilizzo dei dati possono essere utilizzati per escludere alcuni dati dall’essere considerati fattori di influenza nei modelli Look-Alike."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/lookalike-audiences.html?lang=it#exclude" text="Escludi dati"

La sezione dei fattori influenti mostra i primi 100 fattori che influenzano il modello lookalike per il pubblico di base selezionato. Questi fattori influenti sono gli attributi del profilo, gli eventi di esperienza e le appartenenze al pubblico che sono i più importanti per spiegare le somiglianze nel pubblico di base. Comprendere i principali fattori influenti consente di personalizzare meglio i contenuti di marketing per questo pubblico e per qualsiasi pubblico simile che crei da esso. Non verranno visualizzati tutti i fattori influenti che influiscono sul modello lookalike.

Per i fattori influenti di tipo numerico, le coppie di valori chiave possono essere inserite in contenitori, a seconda del numero di valori diversi di cui dispone la chiave. Ad esempio, se disponi di una chiave `income`, è molto probabile che siano presenti molti valori univoci. Di conseguenza, le coppie chiave-valore vengono inserite in contenitori con un aspetto simile a `income=[0 -> 30000]`, `income=[30000 -> 50000]`, e `income=[50000 -> 100000]`.

Questi bucket vengono ricalcolati regolarmente per garantire che i dati siano tenuti aggiornati.

![Viene evidenziata la sezione dei fattori influenti.](../images/ui/lookalike-audiences/influential-factors.png)

>[!NOTE]
>
>I fattori influenti sono ordinati in ordine di importanza e sono indipendenti l&#39;uno dall&#39;altro.

| Campo | Descrizione |
| ----- | ----------- |
| Tipo | Il tipo di dati da cui deriva il fattore influente. Può essere un attributo di profilo, un evento esperienza o un’iscrizione a un pubblico. |
| Chiave | Nome del campo dati. Per le chiavi del tipo di appartenenza al pubblico, questo valore rappresenta **namespace** del pubblico da cui provengono i dati. I valori possibili includono `ups` (Servizio di segmentazione) e `AO` (Orchestrazione del pubblico). Per le chiavi di altri tipi, questo valore rappresenta il percorso del campo XDM. Ad esempio, se l’azienda Luma ha un campo personalizzato denominato reddito, la chiave è `_luma.income` |
| Valore | Il valore varia a seconda del fattore di influenza che rappresenta. Per gli attributi di profilo o gli eventi di esperienza, questo campo rappresenta il valore o l’intervallo di valori del campo dati che indica la somiglianza con i membri del pubblico di base. L’intervallo di valori è scritto nel modulo `[A -> B]`, dove `A` rappresenta l&#39;intervallo inferiore mentre `B` rappresenta l&#39;intervallo più alto. Per le appartenenze al pubblico, questo campo è il nome del pubblico. |
| Importanza | Livello relativo di importanza del fattore influente. Può essere alta, media o bassa. |

## Creare un pubblico simile {#create}

>[!IMPORTANT]
>
>Tu **non può** utilizza un pubblico per similarità come pubblico di base per un altro pubblico per similarità. Vale a dire, tu **non può** creare un pubblico simile concatenato.

Per creare un pubblico simile, devi selezionare il pubblico da cui vuoi basare il pubblico simile. Per accedere all’elenco dei tipi di pubblico disponibili, seleziona **[!UICONTROL Tipi di pubblico]** nella barra di navigazione a sinistra, seguito da **[!UICONTROL Sfoglia]**. Viene visualizzato l’elenco dei tipi di pubblico. In questa pagina puoi selezionare il pubblico da utilizzare come pubblico di base.

![Viene evidenziato il pulsante Tipi di pubblico e il pubblico di base utilizzato per la modellazione lookalike.](../images/ui/lookalike-audiences/browse.png)

Nella pagina dei dettagli del pubblico, seleziona **[!UICONTROL Creare un pubblico simile]** per iniziare il processo di creazione di un pubblico simile.

![Il [!UICONTROL Creare un pubblico simile] viene evidenziato.](../images/ui/lookalike-audiences/create-look-alike-audience.png)

Il **[!UICONTROL Creare un pubblico simile]** viene visualizzato popover. In questa pagina puoi impostare la percentuale di somiglianza per il pubblico simile.

![Il [!UICONTROL Creare un pubblico simile] viene visualizzato popover.](../images/ui/lookalike-audiences/create-audience.png)

Puoi impostare questa percentuale di somiglianza in tre modi diversi:

- Sposta il cursore per impostare la percentuale di somiglianza
- Immetti la percentuale di somiglianza nella casella di immissione numerica accanto al cursore
- Passa il puntatore del mouse sul grafico e seleziona la posizione desiderata per impostare la percentuale di somiglianza

Puoi anche aggiornare i dettagli sul pubblico per similarità, tra cui il nome e la descrizione. Per impostazione predefinita, il nome del pubblico simile viene generato in base al nome del pubblico di base e alla percentuale di somiglianza precedentemente specificata.

![Le informazioni di base vengono evidenziate all&#39;interno di [!UICONTROL Creare un pubblico simile] popover.](../images/ui/lookalike-audiences/basic-info.png)

Seleziona **[!UICONTROL Crea]** per completare la creazione del pubblico per similarità.

![Il pulsante Crea è evidenziato all&#39;interno di [!UICONTROL Creare un pubblico simile] popover.](../images/ui/lookalike-audiences/create-audience.png)

Il pubblico lookalike appena creato è accessibile nel **[!UICONTROL Tipi di pubblico simili]** ed è disponibile anche nel Portale dell’audience e per altri utilizzi a valle. Tieni presente che ci vorrà un po’ di tempo prima che il pubblico similare venga valutato. Finché non viene assegnato un punteggio, il conteggio dei profili apparirà pari a 0.

## Visualizzare i dettagli del pubblico per similarità {#view-details}

Per visualizzare i dettagli di un pubblico simile, seleziona il pubblico simile in **[!UICONTROL Tipi di pubblico simili]** del pubblico di base.

![Viene evidenziata la sezione Tipi di pubblico simili.](../images/ui/lookalike-audiences/select-laa.png)

Viene visualizzata la pagina dei dettagli del pubblico. Per ulteriori informazioni su questa pagina, leggere [sezione dei dettagli del pubblico nella guida dell’interfaccia utente di Segmentation Service](./overview.md#audience-details).

![Vengono visualizzati i dettagli del pubblico simile.](../images/ui/lookalike-audiences/laa-details.png)

## Escludere i campi di dati dalla modellazione lookalike {#exclude}

I tipi di pubblico simili possono essere configurati in modo da escludere i campi di dati per i quali sono impostate restrizioni per l’azione di marketing &quot;Data Science&quot;, applicando le etichette e i criteri di utilizzo dei dati pertinenti. I dati etichettati come non utilizzabili per la data science verranno rimossi dalla considerazione quando si formatta un modello di pubblico per similarità e quando si genera un pubblico per similarità dal modello addestrato. 

L’etichetta standard &quot;C9&quot; può essere utilizzata per etichettare i dati che non devono essere utilizzati per la scienza dei dati e può essere applicata abilitando la politica standard &quot;Limita scienza dei dati&quot;. Puoi anche creare criteri aggiuntivi per limitare i dati con altre etichette, comprese le etichette sensibili, dall’utilizzo per data science. Per ulteriori informazioni sulla gestione dei criteri di utilizzo dei dati, consulta [guida dell’interfaccia utente dei criteri di utilizzo dei dati](../../data-governance/policies/user-guide.md). Per ulteriori informazioni sulla gestione delle etichette di utilizzo dei dati, consulta [guida dell’interfaccia utente per le etichette di utilizzo dei dati](../../data-governance/labels/user-guide.md).

Per impostazione predefinita, il processo di modellazione per i tipi di pubblico simili escluderà **qualsiasi** campo, set di dati o pubblico in base all’informativa sulla privacy abilitata per la tua organizzazione. Se il pubblico di base non dispone di etichette di contratto, il processo di modellazione escluderà **qualsiasi** campo, set di dati o pubblico in base all’informativa sulla privacy abilitata per la tua organizzazione.

Tieni presente che **tu** sono responsabili di garantire che i dati, inclusi i dati sensibili, siano etichettati in modo appropriato e che i criteri di utilizzo dei dati siano stati definiti e abilitati in modo da rispettare gli obblighi legali e normativi in base ai quali operi. È inoltre necessario tenere presente che i campi di dati o le appartenenze a segmenti che sono **non** la correlazione diretta con i campi di dati tipicamente associati a tipi di dati sensibili o protetti può essere fonte di potenziali distorsioni. **Tu** sono responsabili dell’analisi dei dati per identificare, etichettare e applicare le policy di utilizzo dei dati appropriate ai tuoi dati, inclusi eventuali campi di dati che possono fungere da proxy per tipi di dati sensibili o protetti e che devono essere esclusi dalla modellazione.

## Passaggi successivi

Dopo aver letto questa guida, hai imparato a visualizzare informazioni similari e a creare tipi di pubblico simili in base a queste informazioni. Per ulteriori informazioni sui tipi di pubblico nell’interfaccia utente di Adobe Experience Platform, consulta [Guida dell’interfaccia utente di Segmentation Service](./overview.md).
