---
title: Query con parametri
description: Scopri come utilizzare le query con parametri nell’interfaccia utente di Adobe Experience Platform.
exl-id: 5c5ac691-5e29-4262-ba53-84dcc56e744f
source-git-commit: a78f7499b55dcedbe379e917b94946948c66e6e5
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 10%

---

# Query con parametri {#parameterized-queries}

>[!CONTEXTUALHELP]
>id="platform_queryService_queryEditor_parameterizedQueries"
>title="Query con parametri"
>abstract="Utilizza le query con parametri per aggiungere valori di parametro al momento dell’esecuzione. Questo consente di lavorare con dati dinamici e riutilizzare le query per diversi casi d’uso. Utilizza la premessa `'$'` per immettere un parametro di query nella query nell’editor di testo. Quindi, aggiungi un valore per la chiave nella sezione dei parametri di query sotto l’editor."

Query Service supporta l’utilizzo di query con parametri nell’editor delle query. Con le query con parametri, ora puoi utilizzare segnaposto per i parametri e aggiungere i valori dei parametri al momento dell’esecuzione. I segnaposto consentono di lavorare con dati dinamici in cui non si sa quali saranno i valori fino all’esecuzione dell’istruzione. Puoi anche preparare le query in anticipo e riutilizzarle per scopi simili. Il riutilizzo delle query consente di risparmiare tempo evitando di creare query SQL distinte per ogni caso d’uso.

## Prerequisiti

Prima di continuare con questa guida, leggere [Guida dell’interfaccia utente di Query Editor](./user-guide.md). La guida dell’editor delle query fornisce informazioni dettagliate su come scrivere, convalidare ed eseguire query per i dati sull’esperienza del cliente nell’interfaccia utente di Experienci Platform.

>[!NOTE]
>
>Nell’interfaccia utente di Adobe Experience Platform, le query con parametri sono supportate solo a livello principale dei modelli in linea. Ciò significa che le query con parametri funzionano solo se utilizzate nel modello originale. I modelli figlio devono essere statici e non possono avere parametri dinamici. Consulta la [documentazione sui modelli in linea](../essential-concepts/inline-templates.md) per ulteriori informazioni.

## Sintassi delle query con parametri {#syntax}

Le query con parametri utilizzano il formato `'$YOUR_PARAMETER_NAME'` e possono essere concatenati utilizzando la notazione del punto. Di seguito è riportato un esempio di istruzione SQL che utilizza query con parametri.

```sql
INSERT INTO
   $Database_Name.Schema_Name.adwh_lkup_process_delta_log
   (process_name, merge_policy_id, process_status, process_date, create_ts, change_ts)
SELECT
   '$Table_Process_Name' process_name,
   hash('$Merge_PolicyID') merge_policy_id,
   '$process_status' process_status,
   to_date('$date_key') process_date,
   CURRENT_TIMESTAMP create_ts,
   CURRENT_TIMESTAMP change_ts;
```

## Creare una query con parametri {#create}

Per creare una query con parametri nell’interfaccia utente, passa all’editor delle query. Consulta la sezione su [accesso all’editor query](./user-guide.md#accessing-query-editor) per ulteriori istruzioni.

Utilizza la premessa `'$'` per immettere un parametro di query nella query nell’editor di testo. Quindi, aggiungi il valore mancante per la chiave nella [!UICONTROL Parametri di query] sotto l’editor. Impossibile eseguire la query se si omette di aggiungere un valore a una delle chiavi richieste. Un&#39;icona di avviso (![Un&#39;icona di avviso.](../images/ui/parameterized-queries/alert-icon.png)) viene visualizzato nella sezione Parametri query accanto a qualsiasi [!UICONTROL Valore] campi di input.

![Vengono evidenziati l&#39;Editor query con una query con parametri e la sezione Parametri query.](../images/ui/parameterized-queries/parameterized-query.png)

>[!TIP]
>
>Cambia schede da [!UICONTROL Parametri di query] a [!UICONTROL Console] per visualizzare l’output della console della query.

Se si rimuove un parametro e si tenta di eseguire di nuovo la query dopo che è già stata eseguita, nella viene visualizzato un messaggio di errore [!UICONTROL Parametri di query] sezione per avvisarti.

>[!NOTE]
>
>Se la query non accetta parametri, è comunque possibile immettere parametri non necessari nell&#39;editor di query. L’editor delle query ignora tutte le coppie chiave-valore non necessarie e non ha alcun effetto sull’esecuzione o sui risultati della query.

![L’editor delle query con un campo valore vuoto e l’errore Parametri query sono evidenziati.](../images/ui/parameterized-queries/query-parameter-error.png)

## Utilizzare i dettagli dei registri di query per verificare i valori dei parametri {#check-parameter-values}

Non è possibile salvare i parametri all’interno dei modelli in quanto i valori utilizzati non sono persistenti. Tuttavia, puoi controllare il [!UICONTROL Dettagli registro query] per trovare i valori dei parametri utilizzati in un&#39;esecuzione di query. In questo caso, i registri non indicano che la query era con parametri. Consulta la [documentazione dei registri di query](./query-logs.md) per istruzioni su come trovare i valori utilizzati.

![La visualizzazione dei registri della query con l’istruzione SQL di una query con parametri evidenziata nella sezione dei dettagli.](../images/ui/parameterized-queries/parameterized-query-logs.png)

<!-- improve screenshot above ^ I am waiting for a scheduled run to complete -->

## Pianificare una query con parametri {#schedule}

I valori dei parametri vengono salvati quando si pianifica una query con parametri. Per pianificare una query con parametri, seguire il processo tipico per creare una query pianificata come descritto nella guida per [creare una pianificazione di query](./query-schedules.md#create-schedule), quindi immettere i valori dei parametri da utilizzare nell&#39;esecuzione della query. Questa sezione dell’interfaccia utente viene visualizzata solo per le query con parametri. Consulta la sezione su [impostazione di parametri per una query con parametri pianificata](./query-schedules.md#set-parameters) per istruzioni specifiche.

>[!TIP]
>
>Query Service supporta le istruzioni preparate tramite l’utilizzo di query con parametri. Consulta la [guida alla sintassi delle istruzioni preparate](../sql/prepared-statements.md) per ulteriori informazioni sulla sintassi SQL interessata.

## Passaggi successivi

Dopo aver letto questo documento, hai imparato a parametrizzare le query nell’interfaccia utente di Adobe Experience Platform e a utilizzarle nelle esecuzioni pianificate delle query. Nel documento è anche evidenziato come verificare nei registri i valori dei parametri utilizzati nelle esecuzioni delle query.

Successivamente, si consiglia di leggere la guida [monitoraggio delle query pianificate](./monitor-queries.md) per comprendere meglio lo stato di tutti i processi di query tramite l’interfaccia utente di Platform.
