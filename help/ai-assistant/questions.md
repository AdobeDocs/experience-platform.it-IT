---
title: Guida alle domande per l’Assistente AI
description: Leggi questo documento per scoprire alcune domande di esempio che puoi utilizzare quando esegui una query sull’Assistente AI.
source-git-commit: a1092e21940c5e4ba9b598bc51ba1243b57a0051
workflow-type: tm+mt
source-wordcount: '1224'
ht-degree: 0%

---

# Guida alle domande per l’Assistente AI

Leggi questo documento in per una serie di domande di esempio da utilizzare quando esegui una query sull’Assistente AI.

È inoltre possibile utilizzare questo documento per apprendere suggerimenti su [come formulare le domande](#phrasing-your-questions) per ottenere risposte ottimali dall’Assistente AI.

## Domande basate su obiettivi {#objectives-questions}

Le domande di esempio seguenti sono raggruppate per obiettivi che è possibile raggiungere quando si utilizza l’Assistente IA:

| Finalità | Descrizione | Esempio |
| --- | --- | --- |
| Concetti di apprendimento e flussi di lavoro continui | <ul><li>In qualità di utente principiante, puoi utilizzare l’Assistente AI per apprendere i concetti di Real-Time CDP e Adobe Journey Optimizer e integrarti in prodotti e funzionalità che non conosci.</li><li>In qualità di utente esperto, puoi utilizzare l’Assistente IA per risolvere un caso limite che potrebbe bloccare il flusso di lavoro. | <ul><li>Come si imposta una dashboard in Analytics di Percorso?</li><li>Dimmi alcuni casi d’uso per Real-Time CDP.</li></ul> |
| Risoluzione dei problemi | Utilizza l’Assistente AI per scoprire come eseguire il debug degli errori di base che potrebbero verificarsi nel flusso di lavoro. | <ul><li>Cos’è questo errore {ERROR_MESSAGE} Cioè?</li><li>Perché non sono in grado di eliminare il pubblico denominato &quot;Luma: E-mail Audience&quot;?</li></ul> |
| Igiene delle sandbox | Utilizza l’Assistente AI per identificare eventuali oggetti duplicati o inutilizzati in modo da poter gestire la sandbox in modo efficiente. | <ul><li>Puoi mostrarmi tipi di pubblico simili?</li><li>Esistono schemi a cui non è associato un set di dati?</li></ul> |
| Analisi del valore | Utilizza l’Assistente AI per identificare gli oggetti dati più utilizzati e valutare eventuali indicatori di prestazioni o trovare gli oggetti dati più importanti. | <ul><li>Quanti profili ci sono nella definizione del segmento &quot;Luma: Pubblico e-mail&quot;?</li><li>Quando sono stati attivati i tipi di pubblico per la destinazione Tipi di pubblico di Experience Cloud?</li></ul> |
| Ricerca | Utilizza l’Assistente AI per trovare oggetti Experienci Platform supportati come tipi di pubblico, set di dati, destinazioni, schemi e origini. | <ul><li>Elencare i tipi di pubblico contenenti &quot;Luma&quot; nel nome creati nell’ultimo trimestre.</li><li>Quali attributi sono presenti nello schema XDM &quot;Luma: Azioni personalizzate&quot;?</li></ul> |
| Analisi dell&#39;impatto | Utilizza l’Assistente AI per identificare gli oggetti dati utilizzati in alcuni flussi di lavoro in modo da poter valutare l’impatto di eventuali modifiche. | <ul><li>Quali tipi di pubblico utilizzano `homeAddress.city` nello schema &quot;Luma: PersonProfiles&quot;?</li><li>Quali set di dati sono `consents.marketing.push.val` attributo profilo memorizzato in?</li></ul> |

{style="table-layout:auto"}

## Informazioni operative per entità e domande sulla conoscenza del prodotto{#objects-questions}

Le domande seguenti sono raggruppate per oggetti dati e sono classificate come [approfondimenti operativi](./home.md#operational-insights) o [conoscenza del prodotto](./home.md#product-knowledge).

| Oggetto | Descrizione |
| --- | --- |
| Tipi di pubblico - Informazioni operative | <ul><li>Quali tipi di pubblico utilizzano altri tipi di pubblico?</li><li>Qual è la distribuzione del numero di profili tra i tipi di pubblico?</li><li>Mostra i tipi di pubblico modificati per ultimi prima di {RELATIVE_DATE}.</li><li>Quali tipi di pubblico hanno 0 profili?</li><li>È {USE_AUTOCOMPLETE_TO_FILL_AUDIENCE_NAME} utilizzato in altri tipi di pubblico?</li></ul> |
| Attributi - Informazioni operative | <ul><li>Quali tipi di pubblico hanno l’attributo XDM {ATTRIBUTE_PATH} nella loro definizione del segmento?</li><li>Quanti attributi dello schema XDM non vengono utilizzati in alcun pubblico?</li><li>Quali schemi hanno l’attributo XDM {ATTRIBUTE_PATH} in loro?</li><li>Quali attributi XDM vengono attivati?</li><li>Quali attributi XDM vengono utilizzati in tipi di pubblico con più di 10 profili</li></ul> |
| Flussi di dati - Informazioni operative | <ul><li>A quali flussi di dati contribuisce {DATASET_NAME} set di dati?</li><li>Quali flussi di dati di origine non vengono utilizzati o non contengono più dati in arrivo?</li><li> |
| Set di dati: informazioni operative | <ul><li>Quanti set di dati sono stati acquisiti utilizzando lo stesso schema?</li><li>Quale connettore di origine è associato a {DATASET_NAME} set di dati></li><li>Quali set di dati vengono utilizzati in ogni pubblico?</li><li>Quali schemi non vengono utilizzati in alcun set di dati?</li><li>Quanti set di dati ho?</li></ul> |
| Destinazioni: approfondimenti operativi | <ul><li>Quali destinazioni sono in uno stato attivo?</li><li>Su quali account di destinazione è attivato 0 pubblico?</li><li> |
| Percorsi - Informazioni operative | <ul><li>Quanti percorsi ho?</li><li>Percorsi creati in {RELATIVE_DATE} (ad esempio, ultima settimana) oppure {RELATIVE_DATE} (ad esempio prima/dopo/in una data specifica)?</li><li>Mostra l&#39;elenco dei percorsi modificati in {RELATIVE_DATE} (ad esempio, ultima settimana) oppure {RELATIVE_DATE} (ad esempio prima/dopo/in una data specifica)?</li><li>Elencare i percorsi che ho.</li><li>Elencare i tipi di pubblico utilizzati nei percorsi live.</li></ul> |
| Schemi - Informazioni operative | <ul><li>Quali campi dello schema hanno contribuito più al pubblico?</li><li>Quanti schemi sono abilitati per i profili?</li><li>Elenca tutti gli schemi modificati nell&#39;ultima settimana.</li><li>Quali schemi non vengono utilizzati in alcun set di dati?</li><li>Elenca tutti gli schemi creati nell&#39;ultima settimana.</li></ul> |
| Sorgenti: approfondimenti operativi | <ul><li>Quali origini sono in uno stato attivo?</li><li>Quale connettore di origine è associato al set di dati {DATASET_NAME}?</li><li>Quale connettore di origine ha il maggior numero di account associati?</li><li>Mostra i flussi di dati e i connettori di origine associati.</li></ul> |
| Apprendimento mirato - Conoscenza del prodotto (Real-Time CDP e Journey Optimizer) | <ul><li>Cosa può aiutare l’Assistente AI con?</li><li>Cosa sono i tipi di pubblico simili?</li><li>In che modo i gruppi di utenti sono correlati ai ruoli?</li><li>Quando dovrei usare un tipo di dati rispetto a un gruppo di campi?</li><li>Qual è la differenza tra un&#39;identità e una chiave primaria o esterna?</li><li>Come viene calcolata la ricchezza del profilo?</li></ul> |
| Risoluzione dei problemi - Conoscenza del prodotto (Real-Time CDP e Journey Optimizer) | <ul><li>Cosa può aiutare l’Assistente AI con?</li><li>Posso eliminare uno schema abilitato per il profilo dopo l’acquisizione dei dati?</li><li>Perché non posso eliminare un pubblico?</li><li>Quanto tempo ci vuole per valutare i tipi di pubblico e per rendere disponibili i risultati per il targeting?</li></ul> |

{style="table-layout:auto"}

## Formulazione delle domande {#phrasing-your-questions}

Per ottenere una risposta il più accurata possibile, è necessario formulare le domande all’Assistente IA con chiarezza e contesto. Consulta il seguente elenco di suggerimenti per indicazioni su come porre una domanda chiara con il contesto:

* Dichiara il tuo compito e/o la tua domanda in modo conciso.
* Evita un linguaggio ambiguo o una sintassi troppo complessa per facilitare la comprensione.
* Fornisci un contesto rilevante relativo all’attività e/o alla domanda, in quanto il contesto può aiutare l’Assistente AI a generare risposte più rilevanti.

Leggi le tabelle seguenti per ulteriori indicazioni sulle best practice da seguire quando si pongono domande all’Assistente IA.

Le tabelle seguenti descrivono le best practice che è possibile seguire quando si utilizza l’Assistente IA:

| Esegui | Esempio |
| --- | --- |
| <ul><li>Specificare l&#39;oggetto o le informazioni da recuperare o analizzare.</li><li>Provare a inserire i nomi degli oggetti dati tra virgolette. Se si conosce solo una parte del nome dell&#39;oggetto, è possibile specificarlo nella domanda.</li><li>Utilizzare [completamento automatico dell&#39;oggetto](./ui-guide.md#use-auto-complete) per aiutare l’Assistente AI a comprendere meglio il contesto della query.</li></ul> | <ul><li>Quali set di dati utilizzano lo schema &quot;Luma - Fedeltà&quot;?</li><li>Mostrami i segmenti attivati il cui nome contiene &quot;Luma&quot;. Classificale in base al numero di profili.</li></ul> |
| <ul><li>Evita ambiguità e usa un linguaggio chiaro</li><li>Utilizza una terminologia precisa per garantire una maggiore chiarezza nella query.</li><li>Quando fai domande su Adobe Experience Platform, prova a utilizzare la terminologia specifica di Experienci Platform per migliorare la pertinenza delle risposte.</li></ul> | <ul><li>Quanti profili ho in &quot;Pubblico ACME&quot;.</li><li>Mostra i primi 5 attributi XDM utilizzati nei tipi di pubblico attivati.</li></ul> |
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

## Passaggi successivi

Una volta letto questo documento, sarai in grado di ottimizzare le domande per l’Assistente AI. Per informazioni su come utilizzare la funzione durante i flussi di lavoro, leggi [Guida all’interfaccia utente di Assistente IA](ui-guide.md).
