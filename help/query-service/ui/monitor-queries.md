---
title: Monitorare le query pianificate
description: Scopri come monitorare le query tramite l’interfaccia utente di Query Service.
exl-id: 4640afdd-b012-4768-8586-32f1b8232879
source-git-commit: 41c069ef1c0a19f34631e77afd7a80b8967c5060
workflow-type: tm+mt
source-wordcount: '2454'
ht-degree: 0%

---

# Monitorare le query pianificate

Adobe Experience Platform fornisce una migliore visibilità dello stato di tutti i processi di query tramite l’interfaccia utente. Dalla sezione [!UICONTROL Query pianificate] , è ora possibile trovare informazioni importanti sulle esecuzioni delle query, tra cui lo stato, i dettagli della pianificazione e i messaggi/codici di errore in caso di esito negativo. È inoltre possibile abbonarsi agli avvisi per le query basate sul loro stato tramite l’interfaccia utente per una di queste query tramite [!UICONTROL Query pianificate] scheda.

## [!UICONTROL Query pianificate]

Il [!UICONTROL Query pianificate] fornisce una panoramica di tutte le query CTAS e ITAS pianificate. È possibile trovare i dettagli di esecuzione per tutte le query pianificate, nonché i codici di errore e i messaggi per eventuali query non riuscite.

Per passare al [!UICONTROL Query pianificate] , seleziona **[!UICONTROL Query]** dalla barra di navigazione a sinistra seguita da **[!UICONTROL Query pianificate]**

![La scheda Query pianificate nell’area di lavoro Query con Query pianificate ed evidenziate.](../images/ui/monitor-queries/scheduled-queries.png)

La tabella seguente descrive ogni colonna disponibile.

>[!NOTE]
>
>Icona di notifica delle sottoscrizioni (![Icona di notifica delle sottoscrizioni.](../images/ui/monitor-queries/alert-subscription-icon.png)) è contenuto in ogni riga di una colonna senza titolo. Consulta la [avvisi abbonamenti](#alert-subscription) per ulteriori informazioni.

| Colonna | Descrizione |
|---|---|
| **[!UICONTROL Nome]** | Il campo del nome corrisponde al nome del modello o ai primi caratteri della query SQL. Tutte le query create tramite l’interfaccia utente con l’editor delle query sono denominate all’inizio. Se la query è stata creata tramite l’API, il nome diventa un frammento dell’istruzione SQL iniziale utilizzata per creare la query. Per visualizzare un elenco di tutte le esecuzioni associate alla query, selezionare un elemento dal [!UICONTROL Nome] colonna. Per ulteriori informazioni, vedere [la query esegue i dettagli della pianificazione](#query-runs) sezione. |
| **[!UICONTROL Modello]** | Nome del modello della query. Selezionate un nome di modello per passare all&#39;editor di query. Il modello di query viene visualizzato nell’editor delle query per comodità. Se non è presente alcun nome di modello, la riga viene contrassegnata con un trattino e non è possibile reindirizzare all’editor delle query per visualizzare la query. |
| **[!UICONTROL SQL]** | Frammento della query SQL. |
| **[!UICONTROL Frequenza di esecuzione]** | La frequenza con cui la query è impostata per l&#39;esecuzione. I valori disponibili sono `Run once` e `Scheduled`. |
| **[!UICONTROL Creato da]** | Nome dell&#39;utente che ha creato la query. |
| **[!UICONTROL Creato]** | La marca temporale in formato UTC in cui è stata creata la query. |
| **[!UICONTROL Timestamp dell’ultima esecuzione]** | Il timestamp più recente in cui è stata eseguita la query. In questa colonna viene evidenziato se una query è stata eseguita in base alla pianificazione corrente. |
| **[!UICONTROL Stato ultima esecuzione]** | Stato dell’esecuzione della query più recente. I valori dello stato sono: `Success`, `Failed`, `In progress`, e `No runs`. |
| **[!UICONTROL Stato pianificazione]** | Stato corrente della query pianificata. Esistono sei valori potenziali, [!UICONTROL Registrazione], [!UICONTROL Attivo], [!UICONTROL Inattivo], [!UICONTROL Eliminato], un trattino e [!UICONTROL In quarantena].<ul><li>Il **[!UICONTROL Registrazione]** Lo stato indica che il sistema sta ancora elaborando la creazione della nuova pianificazione per la query. Non è possibile disattivare o eliminare una query pianificata durante la registrazione.</li><li>Il **[!UICONTROL Attivo]** lo stato indica che la query pianificata ha **non ancora passato** la data e l’ora di completamento.</li><li>Il **[!UICONTROL Inattivo]** lo stato indica che la query pianificata ha **passato** la data e l’ora di completamento o è stato contrassegnato da un utente come inattivo.</li><li>Il **[!UICONTROL Eliminato]** lo stato indica che la pianificazione della query è stata eliminata.</li><li>Il trattino indica che la query pianificata è una query occasionale non ricorrente.</li><li>Il **[!UICONTROL In quarantena]** Lo stato indica che la query non è riuscita per dieci esecuzioni consecutive e richiede l’intervento dell’utente prima di poter eseguire ulteriori esecuzioni.</li></ul> |

>[!TIP]
>
>Se si passa all&#39;editor delle query, è possibile selezionare **[!UICONTROL Query]** per tornare al [!UICONTROL Modelli] scheda.

## Personalizzare le impostazioni della tabella per le query pianificate {#customize-table}

È possibile regolare le colonne nel [!UICONTROL Query pianificate] in base alle tue esigenze. Per aprire [!UICONTROL Personalizza tabella] impostazioni e modificare le colonne disponibili, seleziona l’icona impostazioni (![Un&#39;icona delle impostazioni.](../images/ui/monitor-queries/settings-icon.png)) in alto a destra.

>[!NOTE]
>
>Il [!UICONTROL Creato] La colonna che fa riferimento alla data di creazione della pianificazione è nascosta per impostazione predefinita.

![Scheda Query pianificate con l’icona Personalizza impostazioni tabella evidenziata.](../images/ui/monitor-queries/customze-table-settings-icon.png)

Per rimuovere o aggiungere una colonna di tabella, attiva o disattiva le caselle di controllo corrispondenti. Quindi, seleziona **[!UICONTROL Applica]** per confermare le scelte effettuate.

>[!NOTE]
>
>Qualsiasi query creata tramite l’interfaccia utente diventa un modello denominato come parte del processo di creazione. Il nome del modello viene visualizzato nella colonna del modello. Se la query è stata creata tramite l’API, la colonna del modello è vuota.

![Finestra di dialogo Personalizza impostazioni tabella.](../images/ui/monitor-queries/customize-table-dialog.png)

## Gestire le query pianificate con azioni in linea {#inline-actions}

Il [!UICONTROL Query pianificate] visualizza offre diverse azioni in linea per gestire tutte le query pianificate da un’unica posizione. Le azioni in linea sono indicate con puntini di sospensione in ogni riga. Selezionare i puntini di sospensione di una query pianificata che si desidera gestire per visualizzare le opzioni disponibili in un menu a comparsa. Le opzioni disponibili includono [[!UICONTROL Disattiva pianificazione]](#disable) o [!UICONTROL Abilita pianificazione], [[!UICONTROL Elimina pianificazione]](#delete), [[!UICONTROL Abbonati]](#alert-subscription) per eseguire query sugli avvisi e [Abilita o [!UICONTROL Disattiva quarantena]](#quarantined-queries).

![Scheda Query pianificate con i puntini di sospensione delle azioni in linea e il menu a comparsa evidenziati.](../images/ui/monitor-queries/inline-actions.png)

### Disattivare o attivare una query pianificata {#disable}

Per disabilitare una query pianificata, seleziona i puntini di sospensione per la query pianificata da gestire, quindi fai clic su **[!UICONTROL Disattiva pianificazione]** dalle opzioni del menu a comparsa. Viene visualizzata una finestra di dialogo per confermare l’azione. Seleziona **[!UICONTROL Disattiva]** per confermare l&#39;impostazione.

Dopo aver disabilitato una query pianificata, puoi abilitare la pianificazione attraverso lo stesso processo. Seleziona i puntini di sospensione, quindi seleziona **[!UICONTROL Abilita pianificazione]** dalle opzioni disponibili.

>[!NOTE]
>
>Se una query è stata messa in quarantena, è necessario esaminare l&#39;istruzione SQL del modello prima di abilitarne la pianificazione. In questo modo si evita lo spreco di ore di calcolo se la query del modello presenta ancora problemi.

### Eliminare una query pianificata {#delete}

Per eliminare una query pianificata, seleziona i puntini di sospensione per la query pianificata da gestire, quindi fai clic su **[!UICONTROL Elimina pianificazione]** dalle opzioni del menu a comparsa. Viene visualizzata una finestra di dialogo per confermare l’azione. Seleziona **[!UICONTROL Elimina]** per confermare l&#39;impostazione.

Una volta eliminata, la query pianificata **non** è stato rimosso dall’elenco delle query pianificate. Le azioni in linea fornite dai puntini di sospensione vengono rimosse e sostituite dall’icona di aggiunta avviso disattivata. Non è possibile sottoscrivere avvisi per la pianificazione eliminata. La riga rimane nell’interfaccia utente per fornire informazioni sulle esecuzioni eseguite come parte della query pianificata.

![La scheda Query pianificate presenta una query pianificata eliminata ed è evidenziata l’icona di abbonamento agli avvisi disattivata.](../images/ui/monitor-queries/post-delete.png)

Se si desidera pianificare le esecuzioni per tale modello di query, selezionare il nome del modello dalla riga appropriata per passare all&#39;editor di query, quindi seguire la [istruzioni per aggiungere una pianificazione a una query](./query-schedules.md#create-schedule) come descritto nella documentazione.

### Abbonati agli avvisi {#alert-subscription}

Per abbonarsi agli avvisi relativi alle esecuzioni pianificate delle query, selezionare `...` (puntini di sospensione) o icona di avviso (![Icona di sottoscrizione di un avviso.](../images/ui/monitor-queries/alert-subscription-icon.png)) per la query pianificata che desideri gestire. Viene visualizzato il menu a discesa delle azioni in linea. Quindi, seleziona **[!UICONTROL Abbonati]** dalle opzioni disponibili.

![Nell’area di lavoro delle query pianificate sono evidenziati i puntini di sospensione, l’icona di sottoscrizione dell’avviso e il menu a discesa delle azioni in linea.](../images/ui/monitor-queries/subscribe.png)

Il [!UICONTROL Avvisi] viene visualizzata una finestra di dialogo. Il [!UICONTROL Avvisi] La finestra di dialogo ti consente di ricevere notifiche tramite interfaccia utente e avvisi e-mail. Sono disponibili diverse opzioni di abbonamento agli avvisi: `start`, `success`, `failure`, `quarantine`, e `delay`. Seleziona la casella o le caselle appropriate e seleziona **[!UICONTROL Salva]** per iscriversi.

![Finestra di dialogo Sottoscrizioni avvisi.](../images/ui/monitor-queries/alert-subscription-dialog.png)

La tabella seguente spiega i tipi di avviso per le query supportati:

| Tipo di avviso | Descrizione |
|---|---|
| `start` | Questo avviso avvisa quando viene avviata o avviata l&#39;elaborazione di una query pianificata. |
| `success` | Questo avviso informa l&#39;utente quando una query pianificata viene eseguita correttamente, indicando che la query è stata eseguita senza errori. |
| `failed` | Questo avviso viene attivato quando una query pianificata viene eseguita con un errore o non viene eseguita correttamente. Consente di identificare e risolvere tempestivamente i problemi. |
| `quarantine` | Questo avviso viene attivato quando un’esecuzione di query pianificata viene messa in quarantena. Quando le query vengono registrate in [funzione di quarantena](#quarantined-queries), qualsiasi query pianificata che non supera dieci esecuzioni consecutive viene automaticamente inserita in una [!UICONTROL In quarantena] stato. Quindi richiedono il tuo intervento prima che possano aver luogo ulteriori esecuzioni. |
| `delay` | Questo avviso ti avvisa se è presente [ritardo nell’esito di un’esecuzione di una query](#query-run-delay) oltre una soglia specificata. È possibile impostare un&#39;ora personalizzata che attivi l&#39;avviso quando la query viene eseguita per tale durata senza completare o non riuscire. |

>[!NOTE]
>
>Per ricevere notifiche sulle esecuzioni delle query messe in quarantena, devi prima registrare le esecuzioni delle query pianificate in [funzione di quarantena](#quarantined-queries).

Consulta la [documentazione API per le sottoscrizioni di avvisi](../api/alert-subscriptions.md) per ulteriori informazioni.

### Visualizzare i dettagli della query {#query-details}

Seleziona l’icona delle informazioni (![Icona delle informazioni.](../images/ui/monitor-queries/information-icon.png)) per visualizzare il pannello dei dettagli della query. Il pannello dei dettagli contiene tutte le informazioni rilevanti sulla query oltre ai fatti inclusi nella tabella delle query pianificate. Le informazioni aggiuntive includono l’ID della query, la data dell’ultima modifica, l’SQL della query, l’ID della pianificazione e la pianificazione del set corrente.

![La scheda Query pianificate con l’icona delle informazioni ed evidenziato il pannello dei dettagli.](../images/ui/monitor-queries/details-panel.png)

## Query in quarantena {#quarantined-queries}

>[!NOTE]
>
>L’avviso di quarantena non è disponibile per le query ad hoc &quot;run-once&quot;. L’avviso di quarantena è applicabile solo per le query batch pianificate (CTAS e ITAS).

Quando si registra nella funzione di quarantena, tutte le query pianificate che non superano dieci esecuzioni consecutive vengono automaticamente inserite in una [!UICONTROL In quarantena] stato. Una query con questo stato diventa inattiva e non viene eseguita alla frequenza pianificata. Quindi richiede il tuo intervento prima che possano aver luogo ulteriori esecuzioni. In questo modo vengono salvaguardate le risorse di sistema in quanto è necessario esaminare e correggere i problemi con l’SQL prima di eseguire ulteriori esecuzioni.

Per attivare una query pianificata per la funzione di quarantena, selezionare i puntini di sospensione (`...`) seguito da [!UICONTROL Abilita quarantena] dal menu a discesa visualizzato.

![La scheda Query pianificate con i puntini di sospensione e Abilita quarantena evidenziati dal menu a discesa delle azioni in linea.](../images/ui/monitor-queries/inline-enable.png)

È inoltre possibile registrare le query nella funzione di quarantena durante il processo di creazione della pianificazione. Consulta la [documentazione pianificazioni query](./query-schedules.md#quarantine) per ulteriori informazioni.

## Ritardo esecuzione query {#query-run-delay}

Tieni sotto controllo le ore di calcolo impostando avvisi per i ritardi nelle query. Puoi monitorare le prestazioni delle query e ricevere notifiche se lo stato di una query rimane invariato dopo un determinato periodo. Utilizza il carattere &#39;[!UICONTROL Ritardo esecuzione query]&#39; avviso da notificare se una query continua a essere elaborata dopo un periodo di tempo specifico senza completamento.

Quando [abbonati agli avvisi](#alert-subscription) per le esecuzioni di query pianificate, uno degli avvisi disponibili è [!UICONTROL Ritardo esecuzione query]. Questo avviso richiede di impostare una soglia per il tempo di esecuzione, nel qual caso viene inviata una notifica del ritardo nell’elaborazione.

Per scegliere una durata di soglia che attivi la notifica, immettere un numero nel campo di immissione testo o utilizzare le frecce su e giù per aumentare di un minuto. Poiché la soglia è impostata in minuti, la durata massima per osservare un ritardo di esecuzione di una query è di 1440 minuti (24 ore). Il periodo di tempo predefinito per un ritardo di esecuzione è di 150 minuti.

>[!NOTE]
>
>Un&#39;esecuzione di una query può avere un solo ritardo. Se modifichi la soglia di ritardo, questa viene modificata per l’utente abbonato all’avviso e per l’intera organizzazione.

![La finestra di dialogo Avvisi della scheda Query pianificate con il campo di input Ritardo esecuzione query evidenziato.](../images/ui/monitor-queries/query-run-delay-input.png)

Consulta la sezione abbonamento agli avvisi per scoprire come [abbonati a [!UICONTROL Ritardo esecuzione query] avvisi](#alert-subscription).

## Filtrare le query {#filter}

Puoi filtrare le query in base alla frequenza di esecuzione. Dalla sezione [!UICONTROL Query pianificate] , seleziona l’icona del filtro (![Icona filtro](../images/ui/monitor-queries/filter-icon.png)) per aprire la barra laterale del filtro.

![Scheda Query pianificate con l’icona del filtro evidenziata.](../images/ui/monitor-queries/filter-queries.png)

Per filtrare l’elenco delle query in base alla loro frequenza di esecuzione, seleziona la **[!UICONTROL Pianificato]** o **[!UICONTROL Esegui una volta]** caselle di controllo filtro.

>[!NOTE]
>
>Qualsiasi query eseguita ma non pianificata può essere considerata [!UICONTROL Esegui una volta].

![Scheda Query pianificate con la barra laterale dei filtri evidenziata.](../images/ui/monitor-queries/filter-sidebar.png)

Dopo aver abilitato i criteri di filtro, seleziona **[!UICONTROL Nascondi filtri]** per chiudere il pannello dei filtri.

## La query esegue i dettagli della pianificazione {#query-runs}

Per aprire la pagina dei dettagli della pianificazione, selezionare un nome di query dal [!UICONTROL Query pianificate] scheda. Questa vista fornisce un elenco di tutte le esecuzioni eseguite come parte della query pianificata. Le informazioni fornite includono l’ora di inizio e di fine, lo stato e il set di dati utilizzati.

![La pagina dei dettagli della pianificazione.](../images/ui/monitor-queries/schedule-details.png)

Queste informazioni sono fornite in una tabella a cinque colonne. Ogni riga indica un’esecuzione di query.

| Nome colonna | Descrizione |
|---|---|
| **[!UICONTROL ID esecuzione query]** | ID esecuzione query per l’esecuzione giornaliera. Seleziona la **[!UICONTROL ID esecuzione query]** per passare al [!UICONTROL Panoramica sull’esecuzione delle query]. |
| **[!UICONTROL Inizio esecuzione query]** | Il timestamp in cui è stata eseguita la query. Il timestamp è in formato UTC. |
| **[!UICONTROL Esecuzione query completata]** | La marca temporale in cui è stata completata la query. Il timestamp è in formato UTC. |
| **[!UICONTROL Stato]** | Stato dell’esecuzione della query più recente. I valori dello stato sono: `Success`, `Failed`, `In progress`, o `Quarantined`. |
| **[!UICONTROL Set di dati]** | Il set di dati coinvolto nell’esecuzione. |

I dettagli della query pianificata sono disponibili nella sezione [!UICONTROL Proprietà] pannello. Questo pannello include l’ID della query iniziale, il tipo di client, il nome del modello, l’SQL della query e la frequenza della pianificazione.

![La pagina dei dettagli della pianificazione con il pannello delle proprietà evidenziato.](../images/ui/monitor-queries/properties-panel.png)

Selezionare un ID esecuzione query per passare alla pagina dei dettagli esecuzione e visualizzare le informazioni sulla query.

![La schermata dei dettagli della pianificazione con un ID esecuzione evidenziato.](../images/ui/monitor-queries/navigate-to-run-details.png)

## Panoramica dell’esecuzione delle query {#query-run-overview}

Il [!UICONTROL Panoramica sull’esecuzione delle query] fornisce informazioni sulle singole esecuzioni per questa query pianificata e un raggruppamento più dettagliato dello stato di esecuzione. Questa pagina include anche le informazioni sul client e i dettagli di eventuali errori che potrebbero aver causato l’esito negativo della query.

![La schermata dei dettagli dell’esecuzione con la sezione panoramica evidenziata.](../images/ui/monitor-queries/query-run-details.png)

La sezione sullo stato della query fornisce il codice di errore e il messaggio di errore in caso di errore della query.

![La schermata dei dettagli dell’esecuzione con la sezione errori evidenziata.](../images/ui/monitor-queries/failed-query.png)

Da questa vista è possibile copiare l&#39;istruzione SQL per query negli Appunti. Per copiare la query, selezionare l&#39;icona Copia in alto a destra del frammento SQL. Un messaggio a comparsa conferma che il codice è stato copiato.

![La schermata dei dettagli dell&#39;esecuzione con l&#39;icona Copia SQL evidenziata.](../images/ui/monitor-queries/copy-sql.png)

### Eseguire i dettagli per le query con blocco anonimo {#anonymous-block-queries}

Le query che utilizzano blocchi anonimi per comporre le istruzioni SQL vengono separate nelle singole sottoquery. La separazione in sottoquery consente di esaminare singolarmente i dettagli di esecuzione per ogni blocco di query.

>[!NOTE]
>
>I dettagli di esecuzione di un blocco anonimo che utilizza il comando DROP **non** essere segnalato come sottoquery separata. Sono disponibili dettagli di esecuzione separati per le query CTAS, le query ITAS e le istruzioni COPY utilizzate come sottoquery di blocco anonime. I dettagli di esecuzione del comando DROP non sono attualmente supportati.

I blocchi anonimi sono identificati mediante l’uso di un `$$` prima della query. Per ulteriori informazioni sui blocchi anonimi nel servizio di query, consulta [documento blocco anonimo](../key-concepts/anonymous-block.md).

Le sottoquery di blocco anonime dispongono di schede a sinistra dello stato di esecuzione. Selezionare una scheda per visualizzare i dettagli dell&#39;esecuzione.

![Panoramica dell’esecuzione della query con una query di blocco anonima. Vengono evidenziate più schede di query.](../images/ui/monitor-queries/anonymous-block-overview.png)

Nel caso in cui una query di blocco anonimo non riesca, puoi trovare il codice di errore per quel particolare blocco tramite questa interfaccia utente.

![Nella panoramica dell’esecuzione della query viene visualizzata una query di blocco anonima con il codice di errore per un singolo blocco evidenziato.](../images/ui/monitor-queries/anonymous-block-failed-query.png)

Seleziona **[!UICONTROL Query]** per tornare alla schermata dettagli pianificazione, oppure **[!UICONTROL Query pianificate]** per tornare al [!UICONTROL Query pianificate] scheda.

![La schermata dei dettagli dell’esecuzione con Query evidenziata.](../images/ui/monitor-queries/return-navigation.png)
