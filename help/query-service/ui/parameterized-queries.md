---
title: Query con parametri
description: Scopri come utilizzare le query con parametri nel interfaccia Adobe Experience Platform.
exl-id: 5c5ac691-5e29-4262-ba53-84dcc56e744f
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 11%

---

# Query con parametri {#parameterized-queries}

>[!CONTEXTUALHELP]
>id="platform_queryService_queryEditor_parameterizedQueries"
>title="Query con parametri"
>abstract="Utilizza le query con parametri per aggiungere valori di parametro al momento dell’esecuzione. Questo consente di lavorare con dati dinamici e riutilizzare le query per diversi casi d’uso. Utilizza la premessa `'$'` per immettere un parametro di query nella query nell’editor di testo. Quindi, aggiungi un valore per la chiave nella sezione dei parametri di query sotto l’editor."

Query Service supporta l&#39;utilizzo di query con parametri nell&#39;editor di query. Con le query con parametri, è ora possibile utilizzare segnaposto per i parametri e aggiungere i valori dei parametri in fase di esecuzione. I segnaposto consentono di lavorare con dati dinamici in cui non si conoscono i valori fino all&#39;esecuzione dell&#39;istruzione. Puoi anche preparare le tue query in anticipo e riutilizzarle per scopi simili. Il riutilizzo delle query consente di risparmiare molto tempo in quanto si evita di creare query SQL distinte per ogni caso d&#39;uso.

## Prerequisiti

Prima di continuare con questa guida, leggere la guida[&#128279;](./user-guide.md) all&#39;interfaccia dell&#39;editor di query. La guida dell&#39;editor di query fornisce informazioni dettagliate su come scrivere, convalidare ed eseguire query per esperienza del cliente dati all&#39;interno dell&#39;interfaccia utente Experience Platform.

>[!NOTE]
>
>Nell&#39;ambito della Adobe Experience Platform interfaccia, le query con parametri sono supportate solo al livello padre dei modelli in linea. Ciò significa che le query con parametri funzionano solo se utilizzate nel modello originale. I modelli secondari devono essere statici e non possono avere parametri dinamici. Per ulteriori informazioni, consulta la documentazione[&#128279;](../key-concepts/inline-templates.md) relativa ai modelli in linea.

## Sintassi di query con parametri {#syntax}

Le query con parametri utilizzano questo formato `'$YOUR_PARAMETER_NAME'` e possono essere concatenate utilizzando la notazione a punti. Di seguito è riportato un esempio di istruzione SQL che utilizza query con parametri.

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

## Crea una query con parametri {#create}

Per creare la query con parametri nella interfaccia, passare all&#39;editor di query. Per ulteriori istruzioni, vedere la sezione sull&#39;accesso [all&#39;editor di](./user-guide.md#accessing-query-editor) query.

Utilizza la premessa `'$'` per immettere un parametro di query nella query nell’editor di testo. Successivo, seleziona i parametri **della**&#x200B; query scheda aggiungi il valore mancante per la chiave accanto alla [!UICONTROL console]. La query non può essere eseguita se si trascura di aggiungere un valore a una delle chiavi richieste. Un&#39;icona di avviso (![Icona di avviso.](/help/images/icons/alert.png)) viene visualizzato nella sezione Parametri di query accanto a qualsiasi campo di immissione del Valore vuoto.

>[!NOTE]
>
>Se la query non accetta parametri, è comunque possibile immettere parametri non necessari all&#39;interno dell&#39;editor di query. L&#39;editor di query ignora tutte le coppie chiave-valore non necessarie e non hanno alcun effetto sull&#39;esecuzione o sui risultati della query.

![Editor di query con una query con parametri e la sezione Parametri di query evidenziata.](../images/ui/parameterized-queries/parameterized-query.png)

>[!TIP]
>
>Per visualizzare l&#39;output della query, modificate le schede da [!UICONTROL Parametri] di query a [!UICONTROL Console] .

## Utilizzare i dettagli dei log di query per controllare i valori dei parametri {#check-parameter-values}

Non è possibile salvare parametri all&#39;interno dei modelli poiché i valori utilizzati non sono persistenti. Tuttavia, è possibile controllare la pagina dei dettagli del registro delle query per trovare i valori dei parametri utilizzati in un&#39;esecuzione di query. In questo caso, i log non indicano che si tratta di una query con parametri. Vedere la [documentazione](./query-logs.md) dei log delle query per istruzioni su come trovare i valori utilizzati.

![La visualizzazione dei log di query con l&#39;SQL di una query con parametri evidenziato nella sezione dettagli.](../images/ui/parameterized-queries/parameterized-query-logs.png)

<!-- improve screenshot above ^ I am waiting for a scheduled run to complete -->

## Pianificare una query con parametri {#schedule}

I valori dei parametri vengono salvati quando si programmare una query con parametri. Per programmare una query con parametri, seguire il processo tipico per creare una query pianificata come descritto nella guida per [creare un programmare](./query-schedules.md#create-schedule) di query, quindi immettere i valori dei parametri da utilizzare nell&#39;esecuzione della query. Questa sezione interfaccia è disponibile solo per le query con parametri. Vedere la sezione sull&#39;impostazione [dei parametri per una query](./query-schedules.md#set-parameters) parametrizzata pianificata per istruzioni specifiche.

>[!TIP]
>
>Query Service supporta le istruzioni preparate mediante l&#39;utilizzo di query con parametri. Per ulteriori informazioni sulla sintassi SQL coinvolta, vedere la [guida](../sql/prepared-statements.md) alla sintassi delle istruzioni preparata.

## Passaggi successivi

Leggendo questo documento, si è appreso come parametrizzare le query nel interfaccia Adobe Experience Platform e utilizzarle nelle esecuzioni di query pianificate. Il documento ha anche evidenziato come controllare i log per i valori dei parametri utilizzati nelle esecuzioni delle query.

Successivo, si consiglia di leggere la guida al [monitoraggio delle query pianificate](./monitor-queries.md) per comprendere meglio lo stato di tutti i processi di query tramite il interfaccia Experience Platform.
