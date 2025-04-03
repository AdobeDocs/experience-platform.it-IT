---
solution: Experience Platform
title: Tipi di pubblico simili
description: Scopri come eseguire il targeting di nuovi tipi di pubblico di alto valore in Adobe Experience Platform utilizzando tipi di pubblico simili.
exl-id: c43dac6c-18a0-482f-803e-b75e1b211e98
source-git-commit: f6d700087241fb3a467934ae8e64d04f5c1d98fa
workflow-type: tm+mt
source-wordcount: '2193'
ht-degree: 9%

---

# Guida ai tipi di pubblico simili

>[!IMPORTANT]
>
>Informazioni e tipi di pubblico simili sono disponibili solo nella **edizione B2C**.

In Adobe Experience Platform, i tipi di pubblico per similarità forniscono informazioni intelligenti su ciascuno dei tipi di pubblico, sfruttando le informazioni basate sull’apprendimento automatico per identificare e indirizzare i clienti di alto valore con le campagne di marketing.

Con i tipi di pubblico simili, puoi creare tipi di pubblico espansi per rivolgerti a clienti con prestazioni simili a quelle dei tuoi tipi di pubblico con prestazioni migliori, oppure rivolgerti a clienti simili ai tipi di pubblico convertiti in precedenza.

## Terminologia {#terminology}

Prima di iniziare a utilizzare tipi di pubblico simili, assicurati di comprendere i seguenti concetti:

- **Pubblico di base**: il pubblico di base è il pubblico di cui desideri ottenere ulteriori informazioni. Questo è il pubblico su cui si basa il modello lookalike **based**.
- **Modello lookalike**: un modello lookalike è un modello di apprendimento automatico addestrato per ogni pubblico di base idoneo senza alcun input da parte del cliente. Ogni modello lookalike crea i fattori influenti e i grafici di somiglianza. Un modello lookalike **non** riceve un punteggio.
- **Pubblico per similarità**: un pubblico per similarità è il pubblico che viene creato quando al pubblico di base viene applicato un modello per similarità con una soglia di similarità selezionata. Puoi creare più tipi di pubblico per similarità utilizzando lo stesso modello per similarità. Il pubblico per somiglianza è ciò che viene valutato.
- **Dimensione totale pubblico indirizzabile**: la dimensione totale del pubblico indirizzabile corrisponde al numero totale di profili negli ultimi 30 giorni meno la popolazione del pubblico di base negli ultimi 30 giorni. Ad esempio, se un cliente ha 10 milioni di profili negli ultimi 30 giorni e il pubblico di base ha 1 milione di profili negli ultimi 30 giorni, la dimensione totale del pubblico indirizzabile è di 9 milioni di profili.

## Idoneità {#eligibility}

Per utilizzare informazioni simili, il pubblico di base **deve** soddisfare i seguenti criteri di idoneità:

- Il pubblico di base **deve** essere creato in Experience Platform.
   - I tipi di pubblico generati esternamente sono **non** idonei per approfondimenti simili.
- Il pubblico di base **deve** essere nel criterio di unione predefinito.
- Il pubblico di base **deve** non utilizzare campi limitati dalla governance dei dati.

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

- I clienti Real-Time CDP Prime hanno diritto a **5** tipi di pubblico lookalike attivi nelle sandbox di produzione
- I clienti Real-Time CDP Ultimate hanno diritto a **20** tipi di pubblico lookalike attivi nelle sandbox di produzione
- Le sandbox di sviluppo sono limitate a **5** tipi di pubblico simili per tutti i clienti Real-Time CDP

I pacchetti di componenti aggiuntivi, che saranno disponibili in un secondo momento, aumentano le adesioni per le sandbox di produzione di 20 tipi di pubblico simili per pacchetto.

Per confermare se hai accesso a tipi di pubblico simili, contatta il tuo rappresentante Adobe.

## Visualizzare informazioni simili {#view}

Le informazioni simili sono integrate nella pagina dei dettagli del pubblico. Per esaminare gli approfondimenti simili relativi a un pubblico, seleziona **[!UICONTROL Tipi di pubblico]** nella barra di navigazione a sinistra, seguito da **[!UICONTROL Sfoglia]** e dal pubblico per il quale desideri visualizzare gli approfondimenti.

![Il pulsante Tipi di pubblico è evidenziato, così come il pubblico di base utilizzato per la modellazione lookalike.](../images/types/lookalike/browse.png)

Viene visualizzata la pagina dei dettagli del pubblico. Seleziona la scheda **[!UICONTROL Approfondimenti simili]** per visualizzare gli approfondimenti simili del pubblico. Viene visualizzata la pagina **[!UICONTROL Informazioni simili]**. Questa pagina presenta tre elementi principali: il grafico delle somiglianze e della portata, i tipi di pubblico simili e i fattori influenti.

![Viene evidenziata la scheda Approfondimenti simili, che mostra gli approfondimenti simili per il pubblico di base.](../images/types/lookalike/look-alike-insights.png)

### Somiglianza e portata {#similarity-and-reach}

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_similarityAndReach"
>title="Somiglianza e portata"
>abstract="Il grafico di somiglianza e portata rappresenta la portata prevista di un pubblico Look-Alike costituito da profili al di sopra di un dato punteggio di somiglianza. Puoi passare il cursore del mouse su un punto specifico del grafico per visualizzare la percentuale di somiglianza e il numero di profili previsto per il punto attualmente evidenziato."

La sezione similarità e portata mostra un grafico che rappresenta la portata prevista di un pubblico simile costituito da profili al di sopra di un determinato punteggio di somiglianza. Il punteggio di somiglianza rappresenta la **distanza** di somiglianza tra il profilo del pubblico di base e il profilo dell&#39;approfondimento similare.

![Il grafico similarità e portata è evidenziato.](../images/types/lookalike/similarity-and-reach.png)

In questo grafico, l’asse x misura la percentuale di somiglianza tra un profilo e i membri del pubblico selezionato. Il punteggio di somiglianza varia da 0% a 100%, con un punteggio di somiglianza più alto che indica che un profilo è più vicino, in termini di valori dei fattori influenti, ai membri del pubblico selezionato.

L’asse y mostra il conteggio previsto dei profili con la percentuale di similarità corrispondente al valore corrispondente dell’asse x. Il numero previsto di profili varia da 0 alla dimensione totale del pubblico indirizzabile o 25 milioni di profili, a seconda di quale valore sia inferiore. Questo asse viene misurato su una **scala logaritmica** per migliorare la leggibilità del grafico.

Il grafico è **cumulativo** da destra a sinistra. Ciò significa che in qualsiasi punto del grafico, il valore dell&#39;asse y è il numero di profili con una somiglianza **superiore** alla soglia di somiglianza. Ad esempio, se l’asse x è al 60% e l’asse y è a 10 milioni, significa che ci sono 10 milioni di profili che hanno una somiglianza pari o superiore al 60% con il pubblico di base.

Puoi passare il cursore del mouse su un punto specifico del grafico per visualizzare la percentuale di somiglianza e il numero di profili previsto per il punto attualmente evidenziato.

### Tipi di pubblico per similarità {#list}

La sezione Tipi di pubblico simili visualizza un elenco di tutti i tipi di pubblico simili creati in precedenza per il pubblico di base selezionato.

![La sezione dei tipi di pubblico simili è evidenziata.](../images/types/lookalike/select-laa.png)

### Fattori di influenza {#influential-factors}

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_influentialFactors"
>title="Fattori di influenza"
>abstract="I fattori di influenza sono attributi, eventi e appartenenze al pubblico importanti per spiegare la somiglianza di un profilo con i membri del pubblico di base. Le etichette e i criteri di utilizzo dei dati possono essere utilizzati per escludere alcuni dati dall’essere considerati fattori di influenza nei modelli Look-Alike."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/types/lookalike-audiences.html?lang=it#exclude" text="Escludi dati"

La sezione dei fattori influenti mostra i primi 100 fattori che influenzano il modello lookalike per il pubblico di base selezionato. Questi fattori influenti sono gli attributi del profilo, gli eventi di esperienza e le appartenenze al pubblico che sono i più importanti per spiegare le somiglianze nel pubblico di base. Comprendere i principali fattori influenti consente di personalizzare meglio i contenuti di marketing per questo pubblico e per qualsiasi pubblico simile che crei da esso. Non verranno visualizzati tutti i fattori influenti che influiscono sul modello lookalike.

Per i fattori influenti di tipo numerico, le coppie di valori chiave possono essere inserite in contenitori, a seconda del numero di valori diversi di cui dispone la chiave. Ad esempio, se la chiave è `income`, è probabile che siano presenti molti valori univoci. Di conseguenza, le coppie chiave-valore verranno inserite in contenitori simili a `income=[0 -> 30000]`, `income=[30000 -> 50000]` e `income=[50000 -> 100000]`.

Questi bucket vengono ricalcolati regolarmente per garantire che i dati siano tenuti aggiornati.

![La sezione dei fattori influenti è evidenziata.](../images/types/lookalike/influential-factors.png)

>[!NOTE]
>
>I fattori influenti sono ordinati in ordine di importanza e sono indipendenti l&#39;uno dall&#39;altro.

| Campo | Descrizione |
| ----- | ----------- |
| Tipo | Il tipo di dati da cui deriva il fattore influente. Può essere un attributo di profilo, un evento esperienza o un’iscrizione a un pubblico. |
| Chiave | Nome del campo dati. Per le chiavi del tipo di appartenenza al pubblico, questo valore rappresenta lo **spazio dei nomi** del pubblico da cui provengono i dati. I valori possibili includono `ups` (servizio di segmentazione) e `AO` (orchestrazione del pubblico). Per le chiavi di altri tipi, questo valore rappresenta il percorso del campo XDM. Ad esempio, se la società Luma ha un campo personalizzato denominato reddito, la chiave sarà `_luma.income` |
| Valore | Il valore varia a seconda del fattore di influenza che rappresenta. Per gli attributi di profilo o gli eventi di esperienza, questo campo rappresenta il valore o l’intervallo di valori del campo dati che indica la somiglianza con i membri del pubblico di base. L&#39;intervallo di valori è scritto nel formato `[A -> B]`, dove `A` rappresenta l&#39;intervallo inferiore mentre `B` rappresenta l&#39;intervallo superiore. Per le appartenenze al pubblico, questo campo è il nome del pubblico. |
| Importanza | Livello relativo di importanza del fattore influente. Può essere alta, media o bassa. |

## Creare un pubblico simile {#create}

>[!IMPORTANT]
>
>**impossibile** utilizzare un pubblico simile come pubblico di base per un altro pubblico simile. In altre parole, **non puoi** creare tipi di pubblico simili concatenati.

Per creare un pubblico simile, devi selezionare il pubblico da cui vuoi basare il pubblico simile. Per accedere all&#39;elenco dei tipi di pubblico disponibili, seleziona **[!UICONTROL Tipi di pubblico]** nella barra di navigazione a sinistra, seguito da **[!UICONTROL Sfoglia]**. Viene visualizzato l’elenco dei tipi di pubblico. In questa pagina puoi selezionare il pubblico da utilizzare come pubblico di base.

![Il pulsante Tipi di pubblico è evidenziato, così come il pubblico di base utilizzato per la modellazione lookalike.](../images/types/lookalike/browse.png)

Nella pagina dei dettagli del pubblico, seleziona **[!UICONTROL Crea pubblico simile]** per iniziare il processo di creazione di un pubblico simile.

![Il pulsante [!UICONTROL Crea pubblico simile] è evidenziato.](../images/types/lookalike/create-look-alike-audience.png)

Viene visualizzata la finestra a comparsa **[!UICONTROL Crea un pubblico simile]**. In questa pagina puoi impostare la percentuale di somiglianza per il pubblico simile.

![Viene visualizzato il messaggio a comparsa [!UICONTROL Crea un pubblico simile].](../images/types/lookalike/create-audience.png)

Puoi impostare questa percentuale di somiglianza in tre modi diversi:

- Sposta il cursore per impostare la percentuale di somiglianza
- Immetti la percentuale di somiglianza nella casella di immissione numerica accanto al cursore
- Passa il puntatore del mouse sul grafico e seleziona la posizione desiderata per impostare la percentuale di somiglianza

Puoi anche aggiornare i dettagli sul pubblico per similarità, tra cui il nome e la descrizione. Per impostazione predefinita, il nome del pubblico simile viene generato in base al nome del pubblico di base e alla percentuale di somiglianza precedentemente specificata.

![Le informazioni di base sono evidenziate nella finestra a comparsa [!UICONTROL Crea un pubblico simile].](../images/types/lookalike/basic-info.png)

Seleziona **[!UICONTROL Crea]** per completare la creazione del pubblico per similarità.

![Il pulsante Crea è evidenziato nella finestra a comparsa [!UICONTROL Crea un pubblico simile].](../images/types/lookalike/create-audience.png)

Il pubblico lookalike appena creato è accessibile nella sezione **[!UICONTROL Tipi di pubblico lookalike]** della pagina dei dettagli del pubblico ed è disponibile anche nel Portale pubblico e per altri utilizzi a valle. Tieni presente che ci vorrà un po’ di tempo prima che il pubblico similare venga valutato. Finché non viene assegnato un punteggio, il conteggio dei profili apparirà pari a 0.

## Visualizzare i dettagli del pubblico per similarità {#view-details}

Per visualizzare i dettagli di un pubblico simile, seleziona il pubblico simile nella sezione **[!UICONTROL Tipi di pubblico simili]** del pubblico di base.

![La sezione dei tipi di pubblico simili è evidenziata.](../images/types/lookalike/select-laa.png)

Viene visualizzata la pagina dei dettagli del pubblico. Per ulteriori informazioni su questa pagina, consulta la sezione [Dettagli pubblico della panoramica di Audience Portal](../ui/audience-portal.md#audience-details).

![Vengono visualizzati i dettagli del pubblico per similarità.](../images/types/lookalike/laa-details.png)

## Escludere i campi di dati dalla modellazione lookalike {#exclude}

>[!IMPORTANT]
>
> **L&#39;utente** ha la responsabilità di garantire che i dati, inclusi i dati sensibili, siano etichettati in modo appropriato e che i criteri di utilizzo dei dati siano stati definiti e abilitati per rispettare gli obblighi legali e normativi in base ai quali l&#39;utente opera. È inoltre necessario tenere presente che i campi di dati o le appartenenze a segmenti **non** direttamente correlati con i campi di dati in genere associati a tipi di dati sensibili o protetti possono essere fonte di potenziali distorsioni. **L&#39;utente** è responsabile dell&#39;analisi dei dati per identificare, etichettare e applicare i criteri di utilizzo dei dati appropriati ai dati, inclusi eventuali campi di dati che possono fungere da proxy per tipi di dati sensibili o protetti e che devono essere esclusi dalla modellazione.

I tipi di pubblico simili possono essere configurati in modo da escludere i campi di dati per i quali sono impostate restrizioni per l’azione di marketing &quot;Data Science&quot;, applicando le etichette e i criteri di utilizzo dei dati pertinenti. I dati etichettati come non utilizzabili per la data science verranno rimossi dalla considerazione quando si formatta un modello di pubblico per similarità e quando si genera un pubblico per similarità dal modello addestrato. 

>[!NOTE]
>
>L’entrata in vigore delle modifiche alle etichette di utilizzo dei dati sul pubblico di base può richiedere fino a 48 ore.

L’etichetta standard &quot;C9&quot; può essere utilizzata per etichettare i dati che non devono essere utilizzati per la scienza dei dati e può essere applicata abilitando la politica standard &quot;Limita scienza dei dati&quot;. Puoi anche creare criteri aggiuntivi per limitare i dati con altre etichette, comprese le etichette sensibili, dall’utilizzo per data science. Per ulteriori informazioni sulla gestione dei criteri di utilizzo dei dati, leggere la [guida dell&#39;interfaccia utente dei criteri di utilizzo dei dati](../../data-governance/policies/user-guide.md). Per ulteriori informazioni sulla gestione delle etichette di utilizzo dei dati, leggere la [guida all&#39;interfaccia utente delle etichette di utilizzo dei dati](../../data-governance/labels/user-guide.md).

Per impostazione predefinita, se un pubblico di base non ha etichette di contratto, il processo di modellazione per i tipi di pubblico simili escluderà **qualsiasi** campo, set di dati o pubblico in base all&#39;informativa sulla privacy abilitata per la tua organizzazione.

## Passaggi successivi

Dopo aver letto questa guida, hai imparato a visualizzare informazioni similari e a creare tipi di pubblico simili in base a queste informazioni. Per ulteriori informazioni sui tipi di pubblico nell&#39;interfaccia utente di Adobe Experience Platform, consulta la [Guida dell&#39;interfaccia utente del servizio di segmentazione](./overview.md).
