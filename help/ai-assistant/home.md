---
title: Panoramica dell’Assistente AI in Adobe Experience Platform
description: Scopri l’Assistente IA, le sue sfumature e i casi di utilizzo, e come utilizzarlo per accelerare il flusso di lavoro con Adobe Experience Platform e Real-time Customer Data Platform.
source-git-commit: dd3a7d07c0c78d76c552affef892d5e5c0f0bfb5
workflow-type: tm+mt
source-wordcount: '2371'
ht-degree: 0%

---

# Assistente AI in Adobe Experience Platform

Leggi questo documento per scoprire di più sull’Assistente AI in Adobe Experience Platform.

L’Assistente AI in Adobe Experience Platform è un’esperienza di conversazione che puoi utilizzare per accelerare i flussi di lavoro nelle applicazioni Adobe. È possibile utilizzare l’Assistente AI per comprendere meglio la conoscenza del prodotto, risolvere i problemi o eseguire ricerche attraverso le informazioni e trovare informazioni operative. L’Assistente AI supporta Experienci Platform, Real-time Customer Data Platform, Adobe Journey Optimizer e Customer Journey Analytics.

>[!IMPORTANT]
>
>* Devi accettare [un contratto utente](https://adobe.sharepoint.com/:w:/s/ExCUserExperience/EVzJv1jFBiZGnaFEufsfIqwBC_9ehv3KaXTkEMTGpQFRpg?e=qzwOo8) prima di poter utilizzare l’Assistente AI. Il contratto utente contiene anche il contratto beta pubblico. In questo modo è possibile utilizzare funzioni dell’Assistente AI aggiuntive durante il rollout in una capacità beta.

![L’interfaccia di AI Assistant con la prima esperienza utente attivata.](./images/blank.png)

## Informazioni sull’Assistente AI {#understanding-ai-assistant}

L&#39;Assistente AI risponde alle domande inviate eseguendo una query su un database e quindi traducendo i dati dal database in una risposta leggibile.

Questa rappresentazione interna dei dati sottostanti è nota anche come **[!DNL Knowledge Graph]** - un web completo di concetti, dati e metadati per una determinata risposta.

Il [!DNL Knowledge Graph] è costituito da sottografi a cui viene fatto riferimento ogni volta che vengono inviate query:

* Informazioni operative sul cliente.
* Informazioni operative sui clienti nei vari meta-store.
* Documentazione di Experience League.

Prima di eseguire una query su Assistente IA, è necessario considerare due classi di domande:

### Conoscenza del prodotto {#product-knowledge}

Per conoscenza del prodotto si intendono i concetti e gli argomenti basati sulla documentazione di Experience League. Le domande relative alla conoscenza del prodotto possono essere ulteriormente specificate nei seguenti sottogruppi:

| Conoscenza del prodotto | Esempi |
| --- | --- |
| Apprendimento puntato | <ul><li>Qual è la differenza tra un&#39;identità e una chiave primaria o esterna?</li><li>Come viene calcolata la ricchezza del profilo?</li></ul> |
| Rilevamento aperto | <ul><li>Come posso esportare questo set di dati?</li><li>Esistono schemi per i clienti del settore sanitario?</li></ul> |
| Risoluzione dei problemi | <ul><li>Perché non posso attivare uno schema di proprietà di Adobe per il profilo?</li><li>Perché non posso eliminare un segmento?</li></ul> |

{style="table-layout:auto"}

### Informazioni operative {#operational-insights}

>[!IMPORTANT]
>
>Le risposte di Operational Insights sono in versione beta. Chiunque abbia accesso a **Visualizza informazioni operative** L’autorizzazione avrà accesso alle risposte di Operational Insights.

Le informazioni operative si riferiscono alle risposte che l’Assistente AI genera sugli oggetti di metadati (attributi, tipi di pubblico, flussi di dati, set di dati, destinazioni, percorsi, schemi e origini), inclusi i conteggi, le ricerche e l’impatto sulla derivazione. Non esamina alcun dato all’interno della sandbox.

* Quanti set di dati ho?
* Quanti attributi dello schema non sono mai stati utilizzati?
* Quale pubblico è stato attivato?

Puoi porre domande all’Assistente AI sulle informazioni operative nei seguenti domini:

* Attributi
* Tipi di pubblico
* Flussi di dati
* Set di dati
* Destinazioni _Al momento non è possibile rispondere ad alcune domande relative agli account e al flusso di dati._
* Percorsi
* Schemi _Al momento non è possibile rispondere alle domande relative ai gruppi di campi._
* Sorgenti _(Al momento non è possibile rispondere alle domande relative ai conti)._

Per le domande sulle informazioni operative, le risposte potrebbero non riflettere lo stato corrente dell’interfaccia utente. I dati che supportano queste domande vengono aggiornati una volta ogni 24 ore. Ad esempio, le modifiche apportate dagli utenti in Real-Time CDP durante il giorno vengono sincronizzate con gli archivi dati di notte e quindi diventano disponibili per le domande degli utenti di mattina. Dovrai accedere a una sandbox per informazioni su dati specifici relativi agli oggetti.

### Ambito della funzione {#feature-scope}

Attualmente, l’ambito di AI Assistant è il seguente:

* [Conoscenza del prodotto](./home.md#product-knowledge): AI Assistant può rispondere a domande sulla conoscenza del prodotto, ad Experience Platform, Real-time Customer Data Platform e Adobe Journey Optimizer. Puoi anche approfondire gli argomenti della conoscenza del prodotto per il Customer Journey Analytics, ma solo tramite l’interfaccia utente del Customer Journey Analytics.
* [Informazioni operative](./home.md#operational-insights): puoi chiedere all’Assistente AI informazioni approfondite operative sui seguenti oggetti dati: attributi, tipi di pubblico, flussi di dati, set di dati, destinazioni, percorsi, schemi e origini.

## Accesso alle funzioni {#feature-access}

L’accesso all’Assistente IA è disciplinato dai seguenti parametri:

* **Accedere all’applicazione:** È possibile accedere all’Assistente IA in Adobe Experience Platform, Adobe Real-Time CDP, Adobe Journey Optimizer e [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/ai-assistant).
* **Accesso contrattuale:** La tua azienda deve accettare alcune [!DNL GenAI]- termini legali relativi prima che la tua organizzazione possa utilizzare l’Assistente all’intelligenza artificiale. Se non riesci ad accedere all’Assistente AI, contatta l’amministratore della tua organizzazione o il team dell’account Adobe.
* **Autorizzazioni:** Utilizza il [Interfaccia utente autorizzazioni](../access-control/abac/ui/permissions.md) per concedere o revocare l’accesso a AI Assistant nell’organizzazione. Per utilizzare l’Assistente IA, un determinato utente deve appartenere a un ruolo fornito con il **Abilita Assistente IA** e **Visualizza informazioni operative** autorizzazioni.
   * Come amministratore, puoi aggiungere **Abilita Assistente IA** a un determinato ruolo e aggiungere un utente a tale ruolo, per consentire loro di accedere all’Assistente AI nella tua organizzazione.
   * Come amministratore, puoi aggiungere **Visualizza informazioni operative** a un determinato ruolo e aggiungere un utente a tale ruolo, per consentire loro di utilizzare le funzionalità di approfondimenti operativi di AI Assistant. Le informazioni operative sono attualmente in versione beta.

![La pagina dell’interfaccia utente delle autorizzazioni con le autorizzazioni Abilita Assistente AI e Visualizza informazioni operative incluse in un determinato ruolo.](./images/permissions.png)

## Domande di esempio {#example-questions}

Questa sezione illustra alcune domande di esempio a cui puoi fare riferimento durante i flussi di lavoro. Le domande sono raggruppate in tre sezioni: approfondimenti operativi, obiettivi e oggetti.

### Domande di esempio raggruppate per approfondimenti operativi {#operational-insights-questions}

+++Seleziona per visualizzare esempi di domande di approfondimento operativo e i rispettivi casi d’uso:

| Tipo di domanda | Caso d’uso | Esempi |
| --- | --- | --- | 
| Derivazione dei dati | Tracciare l&#39;utilizzo di uno o più oggetti tra altri oggetti Experienci Platform | <ul><li>Quali set di dati utilizzano lo schema &quot;schema ACME&quot;?</li><li>Quanti set di dati sono stati acquisiti utilizzando lo stesso schema?</li><li>Quali set di dati sono stati utilizzati nei tipi di pubblico attivati?</li><li>Elencare gli schemi con attributi utilizzati nei tipi di pubblico attivati.</li><li>Mostra i tipi di pubblico attivati su &quot;Destinazioni ACME&quot; e con più di 1000 profili.</li><li>Mostra gli attributi utilizzati nei tipi di pubblico attivati che sono stati modificati dopo gennaio 2023.</li><li>Quali sono i set di dati acquisiti tramite l’origine &quot;ACME Amazon S3&quot;?</li><li>Quali flussi di dati sono associati a &quot;Flusso di dati sulla fedeltà ACME&quot;?</li><li>Elencare gli schemi relativi ai tipi di pubblico attivati e creati nell’ultimo anno.</li></ul> |
| Distribuzione e aggregazioni | Domande basate su riepilogo sull&#39;utilizzo degli oggetti di Experience Platform | <ul><li>Qual è la percentuale di pubblico attivato?</li><li>Quanti campi vengono utilizzati nella segmentazione?</li><li>Quali tipi di pubblico vengono attivati nel maggior numero di destinazioni?</li><li>Elencare tipi di pubblico duplicati.</li><li>Mostra i tipi di pubblico attivati in &quot;Destinazioni ACME&quot; e classificali in base alla dimensione del profilo.</li><li>Qual è la percentuale di tipi di pubblico che non sono stati attivati ma hanno più di 100 profili. Mostratemi i loro nomi.</li><li>Elenca i 3 connettori di origine che acquisiscono i dati nei miei set di dati.</li><li>Elencami i primi 5 attributi utilizzati nei tipi di pubblico attivati in base alla loro occorrenza.</li></ul> |
| Ricerca oggetto | Recuperare o accedere a un oggetto Experience Platform o alle relative proprietà. | <ul><li>A quali set di dati non è associato alcuno schema</li><li>Elencare gli attributi utilizzati per &quot;Pubblico ACME&quot;?</li><li>Dammi l’elenco degli schemi abilitati per il profilo ma non modificati dalla loro creazione.</li><li>Quali tipi di pubblico sono stati modificati nell&#39;ultima settimana?</li><li>Elencami i tipi di pubblico che hanno le stesse definizioni di segmenti insieme alla loro data di creazione.</li><li>Quali set di dati sono abilitati per il profilo e includono anche quanti tipi di pubblico sono stati creati da ciascun set di dati.</li><li>Quali account di origine sono associati al set di dati XYZ?</li><li>Visualizza la definizione del segmento e la data di modifica di &quot;Pubblico ACME&quot;.</li></ul> |
| Confronto degli oggetti | Identifica tipi di pubblico duplicati. | <ul><li>In base alla definizione del segmento, elenca i tipi di pubblico che sono duplicati.</li><li>Quali tipi di pubblico duplicati vengono attivati nelle &quot;Destinazioni ACME&quot;.</li></ul> |

{style="table-layout:auto"}

+++

### Domande di esempio raggruppate per obiettivi {#objectives-questions}

+++Seleziona per visualizzare un elenco di obiettivi che puoi raggiungere con l’Assistente AI

| Finalità | Descrizione | Esempio |
| --- | --- | --- |
| Concetti di apprendimento e flussi di lavoro continui | <ul><li>In qualità di utente principiante, puoi utilizzare l’Assistente AI per apprendere i concetti di Real-Time CDP e Adobe Journey Optimizer e integrarti in prodotti e funzionalità che non conosci.</li><li>In qualità di utente esperto, puoi utilizzare l’Assistente IA per risolvere un caso limite che potrebbe bloccare il flusso di lavoro. | <ul><li>Come si imposta una dashboard in Analytics di Percorso?</li><li>Dimmi alcuni casi d’uso per Real-Time CDP.</li></ul> |
| Risoluzione dei problemi | Utilizza l’Assistente AI per scoprire come eseguire il debug degli errori di base che potrebbero verificarsi nel flusso di lavoro. | <ul><li>Cos’è questo errore {ERROR_MESSAGE} Cioè?</li><li>Perché non sono in grado di eliminare il pubblico denominato &quot;Luma: E-mail Audience&quot;?</li></ul> |
| Igiene delle sandbox | Utilizza l’Assistente AI per identificare eventuali oggetti duplicati o inutilizzati in modo da poter gestire la sandbox in modo efficiente. | <ul><li>Puoi mostrarmi tipi di pubblico simili?</li><li>Esistono schemi a cui non è associato un set di dati?</li></ul> |
| Analisi del valore | Utilizza l’Assistente AI per identificare gli oggetti dati più utilizzati e valutare eventuali indicatori di prestazioni o trovare gli oggetti dati più importanti. | <ul><li>Quanti profili ci sono nella definizione del segmento &quot;Luma: Pubblico e-mail&quot;?</li><li>Quando sono stati attivati i tipi di pubblico per la destinazione Tipi di pubblico di Experience Cloud?</li></ul> |
| Ricerca | Utilizza l’Assistente AI per trovare oggetti Experienci Platform supportati come tipi di pubblico, set di dati, destinazioni, schemi e origini. | <ul><li>Elencare i tipi di pubblico contenenti &quot;Luma&quot; nel nome creati nell’ultimo trimestre.</li><li>Quali attributi sono presenti nello schema XDM &quot;Luma: Azioni personalizzate&quot;?</li></ul> |
| Analisi dell&#39;impatto | Utilizza l’Assistente AI per identificare gli oggetti dati utilizzati in alcuni flussi di lavoro in modo da poter valutare l’impatto di eventuali modifiche. | <ul><li>Quali tipi di pubblico utilizzano `homeAddress.city` nello schema &quot;Luma: PersonProfiles&quot;?</li><li>Quali set di dati sono `consents.marketing.push.val` attributo profilo memorizzato in?</li></ul> |

{style="table-layout:auto"}

+++

### Domande di esempio raggruppate per oggetti {#objects-questions}

+++Seleziona questa opzione per visualizzare un elenco di esempi di domande che l’Assistente AI può aiutarti con:

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

+++

## Formulazione delle domande {#phrasing-your-questions}

Per ottenere una risposta il più accurata possibile, è necessario formulare le domande all’Assistente IA con chiarezza e contesto. Consulta il seguente elenco di suggerimenti per indicazioni su come porre una domanda chiara con il contesto:

* Dichiara il tuo compito e/o la tua domanda in modo conciso.
* Evita un linguaggio ambiguo o una sintassi troppo complessa per facilitare la comprensione.
* Fornisci un contesto rilevante relativo all’attività e/o alla domanda, in quanto il contesto può aiutare l’Assistente AI a generare risposte più rilevanti.

Leggi le tabelle seguenti per ulteriori indicazioni sulle best practice da seguire quando si pongono domande all’Assistente IA.

+++Selezionare questa opzione per visualizzare gli esempi di best practice da seguire per la formulazione delle domande

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

+++

## Passaggi successivi

Ora che hai una conoscenza generale di AI Assistant, puoi procedere e utilizzare AI Assistant durante i flussi di lavoro. Per ulteriori informazioni, consulta la seguente documentazione:

* [Guida all’interfaccia utente di Assistente IA](./ui-guide.md)
* [Privacy, sicurezza e governance nell’Assistente di IA](./privacy.md)
* [Domande frequenti](./faq.md)