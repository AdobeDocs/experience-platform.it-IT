---
title: Guida alle domande per l’Assistente AI
description: Leggi questo documento per scoprire alcune domande di esempio che puoi utilizzare quando esegui una query sull’Assistente AI.
exl-id: d16d1262-cc2d-45c9-94c4-b86132183442
source-git-commit: 0926a0e8c7ae560bf5f4f9ff6853b191af047738
workflow-type: tm+mt
source-wordcount: '1519'
ht-degree: 3%

---

# Guida alle domande per l’Assistente AI

Leggi questo documento in per una serie di domande di esempio da utilizzare quando esegui una query sull’Assistente AI.

È inoltre possibile utilizzare questo documento per apprendere suggerimenti su [come formulare le domande](#phrasing-your-questions) per ottenere risposte ottimali dall&#39;Assistente di intelligenza artificiale.

## Domande basate su obiettivi {#objectives-questions}

Le domande di esempio seguenti sono raggruppate per obiettivi che è possibile raggiungere quando si utilizza l’Assistente IA:

| Finalità | Descrizione | Esempio |
| --- | --- | --- |
| Concetti di apprendimento e flussi di lavoro continui | <ul><li>In qualità di utente principiante, puoi utilizzare l’Assistente AI per apprendere i concetti di Real-Time CDP e Adobe Journey Optimizer e integrarti in prodotti e funzionalità che non conosci.</li><li>In qualità di utente esperto, puoi utilizzare l’Assistente IA per risolvere un caso limite che potrebbe bloccare il flusso di lavoro. | <ul><li>Come si imposta una dashboard in Analytics di Percorso?</li><li>Dimmi alcuni casi d’uso per Real-Time CDP.</li></ul> |
| Risoluzione dei problemi | Utilizza l’Assistente AI per scoprire come eseguire il debug degli errori di base che potrebbero verificarsi nel flusso di lavoro. | <ul><li>Cosa significa questo errore {ERROR_MESSAGE}?</li><li>Perché non sono in grado di eliminare il pubblico denominato &quot;Luma: E-mail Audience&quot;?</li></ul> |
| Igiene delle sandbox | Utilizza l’Assistente AI per identificare eventuali oggetti duplicati o inutilizzati in modo da poter gestire la sandbox in modo efficiente. | <ul><li>Puoi mostrarmi tipi di pubblico simili?</li><li>Esistono schemi a cui non è associato un set di dati?</li></ul> |
| Analisi del valore | Utilizza l’Assistente AI per identificare gli oggetti dati più utilizzati e valutare eventuali indicatori di prestazioni o trovare gli oggetti dati più importanti. | <ul><li>Quanti profili ci sono nella definizione del segmento &quot;Luma: Pubblico e-mail&quot;?</li><li>Quando sono stati attivati i tipi di pubblico per la destinazione Tipi di pubblico di Experience Cloud?</li></ul> |
| Ricerca | Utilizza l’Assistente AI per trovare oggetti Experienci Platform supportati come tipi di pubblico, set di dati, destinazioni, schemi e origini. | <ul><li>Elencare i tipi di pubblico contenenti &quot;Luma&quot; nel nome creati nell’ultimo trimestre.</li><li>Quali attributi sono presenti nello schema XDM &quot;Luma: Azioni personalizzate&quot;?</li></ul> |
| Analisi dell&#39;impatto | Utilizza l’Assistente AI per identificare gli oggetti dati utilizzati in alcuni flussi di lavoro in modo da poter valutare l’impatto di eventuali modifiche. | <ul><li>Quali tipi di pubblico utilizzano `homeAddress.city` nello schema &quot;Luma: PersonProfiles&quot;?</li><li>Quali set di dati sono l&#39;attributo di profilo `consents.marketing.push.val` archiviato in?</li></ul> |

{style="table-layout:auto"}

## Informazioni operative per entità e domande sulla conoscenza del prodotto{#objects-questions}

Le domande seguenti sono raggruppate per oggetti dati e sono classificate come [approfondimenti operativi](./home.md#operational-insights) o [conoscenza del prodotto](./home.md#product-knowledge).

![](./images/prompt.png)

* **Tipi di pubblico - Informazioni operative**
   * Quali tipi di pubblico utilizzano altri tipi di pubblico?
   * Qual è la distribuzione del numero di profili tra i tipi di pubblico?
   * Mostra i tipi di pubblico modificati per ultimi prima di {RELATIVE_DATE}.
   * Quali tipi di pubblico hanno 0 profili?
   * {USE_AUTO_COMPLETE_TO_FILL_AUDIENCE_NAME} è utilizzato in altri tipi di pubblico?
* **Attributi - Informazioni operative**
   * Quali tipi di pubblico hanno l&#39;attributo xdm {ATTRIBUTE_PATH} nella definizione del segmento?
   * Quanti attributi dello schema XDM non vengono utilizzati in alcun pubblico?
   * Quali schemi contengono l&#39;attributo xdm {ATTRIBUTE_PATH}?
   * Quali attributi XDM vengono attivati?
   * Quali attributi XDM vengono utilizzati in tipi di pubblico con più di 10 profili?
* **Flussi dati - Informazioni operative**
   * Quali flussi di dati contribuiscono al set di dati {USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME}?
   * Quali flussi di dati di origine non vengono utilizzati o non contengono più dati in arrivo?
   * Elencare i flussi di dati di origine disponibili.
   * Quali flussi di dati sono configurati per ciascun connettore di origine?
* **Set di dati - Informazioni operative**
   * Quanti set di dati sono stati acquisiti utilizzando lo stesso schema?
   * Quale connettore di origine è associato al set di dati {USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME}?
   * Quali set di dati vengono utilizzati in ogni pubblico?
   * Quali schemi non vengono utilizzati in alcun set di dati?
   * Quanti set di dati ho?
* **Destinazioni - Informazioni operative**
   * Quali destinazioni sono in uno stato attivo?
   * Su quali account di destinazione è attivato 0 pubblico?
   * Quanti tipi di pubblico vengono attivati per ogni destinazione?
   * Quali destinazioni hanno il maggior numero di tipi di pubblico attivati?
* **Percorsi - Informazioni operative**
   * Quanti percorsi ho?
   * Quali percorsi sono stati creati in {RELATIVE_DATE} (ad esempio l&#39;ultima settimana) o {RELATIVE_DATE} (ad esempio prima/dopo/in una data specifica)?
   * Visualizzare l&#39;elenco dei percorsi modificati in {RELATIVE_DATE} (ad esempio l&#39;ultima settimana) o {RELATIVE_DATE} (ad esempio prima/dopo/in una data specifica)?
   * Elencare i percorsi live che ho.
   * Elencare i tipi di pubblico utilizzati nei percorsi live.
* **Origini - Informazioni operative**
   * Quali origini sono in uno stato attivo?
   * Quale connettore di origine è associato al set di dati {USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME}.
   * Quale connettore di origine ha il maggior numero di account associati?
   * Mostra i flussi di dati e i connettori di origine associati.
* **Apprendimento mirato - Conoscenza del prodotto (Real-Time CDP e Journey Optimizer)**
   * Cosa sono i tipi di pubblico simili?
   * In che modo i gruppi di utenti sono correlati ai ruoli?
   * Quando dovrei usare un tipo di dati rispetto a un gruppo di campi?
   * Qual è la differenza tra un&#39;identità e una chiave primaria o esterna?
* **Risoluzione dei problemi - Conoscenza del prodotto (Real-Time CDP e Journey Optimizer)**
   * Per cosa può essere utile l’Assistente IA?
   * Posso eliminare uno schema abilitato per il profilo dopo l’acquisizione dei dati?
   * Perché non posso eliminare un pubblico?
   * Quanto tempo ci vuole affinché i tipi di pubblico vengano valutati e i risultati siano disponibili per il targeting?

## Formulazione delle domande {#phrasing-your-questions}

Per ottenere una risposta il più accurata possibile, è necessario formulare le domande all’Assistente IA con chiarezza e contesto. Consulta il seguente elenco di suggerimenti per indicazioni su come porre una domanda chiara con il contesto:

* Dichiara il tuo compito e/o la tua domanda in modo conciso.
* Evita un linguaggio ambiguo o una sintassi troppo complessa per facilitare la comprensione.
* Fornisci un contesto rilevante relativo all’attività e/o alla domanda, in quanto il contesto può aiutare l’Assistente AI a generare risposte più rilevanti.

Leggi le tabelle seguenti per ulteriori indicazioni sulle best practice da seguire quando si pongono domande all’Assistente IA.

Le tabelle seguenti descrivono le best practice che è possibile seguire quando si utilizza l’Assistente IA:

| Esegui | Esempio |
| --- | --- |
| <ul><li>Specificare l&#39;oggetto o le informazioni da recuperare o analizzare.</li><li>Provare a inserire i nomi degli oggetti dati tra virgolette. Se si conosce solo una parte del nome dell&#39;oggetto, è possibile specificarlo nella domanda.</li><li>Utilizza [completamento automatico dell&#39;oggetto](./ui-guide.md#use-auto-complete) per aiutare l&#39;Assistente IA a comprendere meglio il contesto della query.</li></ul> | <ul><li>Quali set di dati utilizzano lo schema &quot;Luma - Fedeltà&quot;?</li><li>Mostrami i segmenti attivati il cui nome contiene &quot;Luma&quot;. Classificale in base al numero di profili.</li></ul> |
| <ul><li>Evita ambiguità e usa un linguaggio chiaro</li><li>Utilizza una terminologia precisa per garantire una maggiore chiarezza nella query.</li><li>Quando fai domande su Adobe Experience Platform, prova a utilizzare la terminologia specifica di Experience Platform per migliorare la pertinenza delle risposte.</li></ul> | <ul><li>Quanti profili ho in &quot;Pubblico ACME&quot;.</li><li>Mostra i primi 5 attributi XDM utilizzati nei tipi di pubblico attivati.</li></ul> |
| <ul><li>Fornisci contesto o specifica un criterio per filtrare i risultati.</li><li>Utilizza un criterio di filtro nelle domande per limitare il volume di dati nella risposta.</li></ul> | <ul><li>Mostra i tipi di pubblico che non sono stati attivati e che sono stati creati più di 6 mesi fa e che non sono mai stati modificati.</li><li>Mostra i tipi di pubblico attivati su &quot;Destinazione ACME&quot; e con più di 10000 profili.</li></ul> |

{style="table-layout:auto"}

| Non | Esempio |
| --- | --- |
| Utilizza un linguaggio vago o ambiguo. | <ul><li>Datemi informazioni sui set di dati.</li><li>Quanti utenti ho in &quot;ACME Audience&quot;?</li><li>Mostra segmenti.</li><li>Attributi elenco.</li></ul> |
| Eseguire richieste incomplete. | &quot;Luma - Set di dati fedeltà&quot; |
| Assumere conoscenze senza contesti. | <ul><li>Pubblico negli ultimi 6 mesi.</li><li>Crea una query per me.</li></ul> |
| Formulare query eccessivamente complesse. | Fornisci un’analisi completa della derivazione dei dati tra tutti gli oggetti e le loro dipendenze. |
| Omettere criteri o parametri. | Mostra i set di dati. |

{style="table-layout:auto"}

## Esempi di domande non supportate {#unsupported-questions}

Di seguito è riportato un elenco di esempi di domande non attualmente supportate da AI Assistant.

+++Seleziona per visualizzare esempi di domande non supportate

### Insight operativi

* Quanti profili in questa sandbox vivono in California? (**Nota**: per domande simili, devi fornire un criterio specifico per fornire un contesto sufficiente per la richiesta; in questo caso, il criterio specifico è &quot;live in California&quot;).
* Quali sono i segmenti in cui si trova questo profilo {PROFILE_INFO/ATTRIBUTE_VALUE}?
* Quanti profili nel set di dati hanno un messaggio e-mail?
* Quale set di dati rappresenta il numero massimo di profili in questa sandbox?
* Quale set di dati ha il numero più alto di record?
* Quanti segmenti sono stati eliminati in {RELATIVE_DATE}?
* Quale dei miei set di dati ha le dimensioni più grandi?
* Assegnami un profilo in {AUDIENCE_NAME}.
* Qual è il numero totale di profili nella sandbox
* Quanti spazi dei nomi di identità sono associati al pubblico {AUDIENCE_NAME}?
* Mostra un rapporto di tutti i segmenti di pubblico valutati oggi
* Quanti segmenti hanno profili sovrapposti?
* Quanti batch vengono caricati in {DATASET_NAME}
* Quante offerte attive ci sono?
* Quante campagne attive sono disponibili?
* Da dove provengono le mie fonti di dati?
* Qual è il set di dati o l’origine dati più grande?
* Posso ottenere l’elenco degli utenti che hanno creato questi schemi?

### Risoluzione dei problemi

* Perché il batch {BATCH_NAME/BATCH_ID} è ancora in elaborazione?
* Perché nessuno si qualifica per questo pubblico {AUDIENCE_NAME}?
* Non sono in grado di visualizzare IA per l’analisi dei clienti, perché e come posso correggerla?
* Non riesco a visualizzare l’anteprima del set di dati, perché e come posso correggerla?
* Perché non posso eliminare {SEGMENT/DATASET/SCHEMA_NAME}?
* Posso accedere a Query Service?

### Attività e automazione

* Scrivere una query che mi dia un record da {DATASET_NAME}.
* Scrivere una chiamata API di esempio in /schemas/{schemaId}/fields/{fieldPath}/values.
* Imposta un&#39;origine o una destinazione per me.
* Crea un pubblico con i criteri {USER_SPECIFIC_CRITERIA}.

+++

## Passaggi successivi

Una volta letto questo documento, sarai in grado di ottimizzare le domande per l’Assistente AI. Per informazioni su come utilizzare la funzionalità durante i flussi di lavoro, leggere la [Guida dell&#39;interfaccia utente dell&#39;Assistente AI](ui-guide.md).
