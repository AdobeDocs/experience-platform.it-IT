---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Mappare un file CSV su uno schema XDM
topic: tutorial
translation-type: tm+mt
source-git-commit: 7876e6d52815968802bd73bb5e340c99ea3387a8
workflow-type: tm+mt
source-wordcount: '1292'
ht-degree: 2%

---


# Mappare un file CSV su uno schema XDM

Per assimilare i dati CSV in [!DNL Adobe Experience Platform], i dati devono essere mappati su uno schema [!DNL Experience Data Model] (XDM). Questa esercitazione illustra come mappare un file CSV su uno schema XDM utilizzando l&#39;interfaccia [!DNL Platform] utente.

Inoltre, l&#39;appendice di questa esercitazione fornisce ulteriori informazioni sull&#39;utilizzo delle funzioni [di](#mapping-functions)mappatura.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di [!DNL Platform]:

- [!DNL Experience Data Model (XDM System)](../../xdm/home.md): Il framework standard con cui [!DNL Platform] organizzare i dati relativi all&#39;esperienza del cliente.
- [!DNL Batch ingestion](../batch-ingestion/overview.md): Metodo con cui [!DNL Platform] vengono acquisiti i dati dai file di dati forniti dall&#39;utente.

Questa esercitazione richiede anche che sia già stato creato un set di dati in cui assimilare i dati CSV. Per i passaggi sulla creazione di un dataset nell&#39;interfaccia utente, consulta l&#39;esercitazione [sull&#39;acquisizione dei](./ingest-batch-data.md)dati.

## Scegliere una destinazione

Accedete a [!DNL Adobe Experience Platform](https://platform.adobe.com) e selezionate **[!UICONTROL Workflows]** dalla barra di navigazione a sinistra per accedere all’ *[!UICONTROL Workflows]* area di lavoro.

Dalla **[!UICONTROL Workflows]** schermata, selezionate **[!UICONTROL Map CSV to XDM schema]** sotto la **[!UICONTROL Data ingestion]** sezione, quindi selezionate **[!UICONTROL Launch]**.

![](../images/tutorials/map-a-csv-file/workflows.png)

Viene *[!UICONTROL Map CSV to XDM schema]* visualizzato il flusso di lavoro, a partire dal *[!UICONTROL Destination]* passaggio. Scegliere un set di dati in entrata in cui assimilare i dati. È possibile utilizzare un set di dati esistente o crearne uno nuovo.

**Utilizzare un dataset esistente**

Per assimilare i dati CSV in un set di dati esistente, selezionate **[!UICONTROL Use existing dataset]**. È possibile recuperare un set di dati esistente utilizzando la funzione di ricerca o scorrendo l&#39;elenco dei set di dati esistenti nel pannello.

![](../images/tutorials/map-a-csv-file/use-existing-dataset.png)

Per assimilare i dati CSV in un nuovo set di dati, selezionate **[!UICONTROL Create new dataset]** e immettete un nome e una descrizione per il set di dati nei campi forniti. Selezionare uno schema utilizzando la funzione di ricerca o scorrendo l&#39;elenco degli schemi forniti. Selezionare **[!UICONTROL Next]** per continuare.

![](../images/tutorials/map-a-csv-file/create-new-dataset.png)

## Aggiungi dati

Viene *[!UICONTROL Add data]* visualizzato il passaggio. Trascinate e rilasciate il file CSV nello spazio disponibile oppure selezionate **[!UICONTROL Choose files]** per inserire manualmente il file CSV.

![](../images/tutorials/map-a-csv-file/add-data.png)

La *[!UICONTROL Sample data]* sezione viene visualizzata una volta che il file è stato caricato, mostrando le prime dieci righe di dati. Dopo aver confermato che i dati sono stati caricati come previsto, selezionate **[!UICONTROL Next]**.

![](../images/tutorials/map-a-csv-file/sample-data.png)

## Mappatura di campi CSV nei campi dello schema XDM

Viene *[!UICONTROL Mapping]* visualizzato il passaggio. Le colonne del file CSV sono elencate in *[!UICONTROL Source Field]*, con i campi dello schema XDM corrispondenti elencati in *[!UICONTROL Target Field]*. I campi di destinazione non selezionati sono evidenziati in rosso. È possibile utilizzare l&#39;opzione dei campi filtro per restringere l&#39;elenco dei campi di origine disponibili.

Per mappare una colonna CSV su un campo XDM, selezionate l&#39;icona dello schema accanto al campo di destinazione corrispondente della colonna.

![](../images/tutorials/map-a-csv-file/mapping.png)

Viene *[!UICONTROL Select schema field]* visualizzata la finestra. Qui puoi spostarti nella struttura dello schema XDM e individuare il campo a cui mappare la colonna CSV. Fate clic su un campo XDM per selezionarlo, quindi fate clic su **[!UICONTROL Select]**.

![](../images/tutorials/map-a-csv-file/select-schema-field.png)

La *[!UICONTROL Mapping]* schermata viene visualizzata nuovamente, con il campo XDM selezionato ora sotto *[!UICONTROL Target Field]*.

![](../images/tutorials/map-a-csv-file/field-mapped.png)

Se non desiderate mappare una particolare colonna CSV, potete rimuovere la mappatura facendo clic sull&#39;icona **di** rimozione accanto al campo di destinazione. È inoltre possibile rimuovere tutte le mappature selezionando la **[!UICONTROL Clear all mappings button]**.

![](../images/tutorials/map-a-csv-file/remove-mapping.png)

Per aggiungere una nuova mappatura, selezionate **[!UICONTROL Add new mapping]** nella parte superiore dell&#39; *[!UICONTROL Source Field]* elenco.

![](../images/tutorials/map-a-csv-file/add-mapping.png)

Quando mappate i campi, potete anche includere funzioni per calcolare i valori in base ai campi di origine di input. Per ulteriori informazioni, consulta la sezione delle funzioni [di](#mapping-functions) mappatura nell’appendice.

### Aggiungi campo calcolato

I campi calcolati consentono la creazione di valori in base agli attributi nello schema di input. Questi valori possono quindi essere assegnati agli attributi nello schema di destinazione e ricevere un nome e una descrizione che consentano un riferimento più semplice.

Selezionare il **[!UICONTROL Add calculated field]** pulsante per continuare.

![](../images/tutorials/map-a-csv-file/add-calculated-field.png)

Viene visualizzato il **[!UICONTROL Create calculated field]** pannello. La finestra di dialogo a sinistra contiene i campi, le funzioni e gli operatori supportati nei campi calcolati. Selezionare una delle schede per iniziare ad aggiungere funzioni, campi o operatori all&#39;editor di espressioni.

![](../images/tutorials/map-a-csv-file/create-calculated-fields.png)

| Tab | Descrizione |
| --------- | ----------- |
| Campi | La scheda Campi elenca i campi e gli attributi disponibili nello schema di origine. |
| Funzioni | La scheda Funzioni elenca le funzioni disponibili per trasformare i dati. |
| Operatori | La scheda operatori elenca gli operatori disponibili per trasformare i dati. |

È possibile aggiungere manualmente campi, funzioni e operatori utilizzando l&#39;editor di espressioni al centro. Selezionate l&#39;editor per iniziare a creare un&#39;espressione.

![](../images/tutorials/map-a-csv-file/expression-editor.png)

Selezionare **[!UICONTROL Save]** per continuare.

La schermata di mappatura viene visualizzata nuovamente con il campo di origine appena creato. Applicate il campo di destinazione corrispondente appropriato e selezionate **[!UICONTROL Finish]** per completare la mappatura.

![](../images/tutorials/map-a-csv-file/new-field.png)

## Monitorare il flusso di dati

Una volta mappato e creato il file CSV, potete monitorare i dati che vengono acquisiti tramite di esso. Per ulteriori informazioni sul monitoraggio dei flussi di dati, consulta l’esercitazione sul [monitoraggio dei flussi di dati](../../ingestion/quality/monitor-data-flows.md).

## Passaggi successivi

Seguendo questa esercitazione, avete mappato correttamente un file CSV semplice su uno schema XDM e lo avete assimilato in [!DNL Platform]. Questi dati possono ora essere utilizzati da [!DNL Platform] servizi a valle come [!DNL Real-time Customer Profile]. Per [!DNL Real-time Customer Profile](../../profile/home.md) ulteriori informazioni, consulta la panoramica.

## Appendice

La sezione seguente fornisce informazioni aggiuntive per la mappatura delle colonne CSV ai campi XDM.

### Funzioni di mappatura

Alcune funzioni di mappatura possono essere utilizzate per calcolare e calcolare i valori in base a quanto immesso nei campi di origine. Per utilizzare una funzione, digitarla in *[!UICONTROL Source Field]* base alla sintassi e agli input appropriati.

Ad esempio, per concatenare i campi CSV **città** e **paese** e assegnarli al campo XDM **città** , impostate il campo di origine come `concat(city, ", ", county)`.

![](../images/tutorials/map-a-csv-file/mapping-function.png)

Nella tabella seguente sono elencate tutte le funzioni di mappatura supportate, incluse le espressioni di esempio e i relativi output.

| Funzione | Descrizione | Espressione esempio | Output di esempio |
| -------- | ----------- | ----------------- | ------------- |
| concat | Concatenate le stringhe date. | concat(&quot;Ciao, &quot;, &quot;lì&quot;, &quot;!&quot;) | `"Hi, there!"` |
| esplodere | Divide la stringa in base a un regex e restituisce un array di parti. | esplode(&quot;Ciao, ciao!&quot;, &quot; &quot;) | `["Hi,", "there"]` |
| instr | Restituisce la posizione/indice di una sottostringa. | instr(&quot;adobe<span>.com&quot;, &quot;com&quot;) | 6 |
| sostituto | Sostituisce la stringa di ricerca, se presente nella stringa originale. | replace(&quot;Questa è una stringa ri test&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;Questo è un test di sostituzione delle stringhe&quot; |
| substr | Restituisce una sottostringa della lunghezza specificata. | substr(&quot;Questo è un test di sottostringa&quot;, 7, 8) | &quot; a subst&quot; |
| Lower /<br>lcase | Converte una stringa in caratteri minuscoli. | lower(&quot;HeLL&quot;)<br>lcase(&quot;HeLLo&quot;) | &quot;hello&quot; |
| Upper /<br>ucase | Converte una stringa in caratteri maiuscoli. | Upper(&quot;HeLL&quot;)<br>ucase(&quot;HeLLo&quot;) | &quot;HELLO&quot; |
| split | Divide una stringa di input su un separatore. | split(&quot;Hello world&quot;, &quot; &quot;) | `["Hello", "world"]` |
| join | Unisce un elenco di oggetti utilizzando il separatore. | `join(" ", ["Hello", "world"]`) | &quot;Hello world&quot; |
| fondersi | Restituisce il primo oggetto non-null in un elenco specificato. | coalesce(null, null, null, &quot;first&quot;, null, &quot;seconda&quot;) | &quot;first&quot; |
| decodificare | Data una chiave e un elenco di coppie di valori chiave appiattite come array, la funzione restituisce il valore se viene trovata una chiave o restituisce un valore predefinito se presente nell&#39;array. | decode(&quot;k2&quot;, &quot;k1&quot;, &quot;v1&quot;, &quot;k2&quot;, &quot;v2&quot;, &quot;default&quot;) | &quot;v2&quot; |
| iif | Valuta una determinata espressione booleana e restituisce il valore specificato in base al risultato. | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;True&quot; |
| min | Restituisce il minimo degli argomenti specificati. Utilizza l&#39;ordine naturale. | min(3, 1, 4) | 1 |
| max | Restituisce il massimo degli argomenti specificati. Utilizza l&#39;ordine naturale. | max(3, 1, 4) | 4 |
| first | Recupera il primo argomento specificato. | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| last | Recupera l&#39;ultimo argomento specificato. | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| uuid /<br>guid | Genera un ID pseudo-casuale. | uid()<br>guid() | {UNIQUE_ID} |
| now | Recupera l&#39;ora corrente. | now() | `2019-10-23T10:10:24.556-07:00[America/Los_Angeles]` |
| timestamp | Recupera l&#39;ora Unix corrente. | timestamp() | 1571850624571 |
| format | Formatta la data di input in base a un formato specificato. | format({DATE}, &quot;yyyy-MM-dd HH:mm:ss&quot;) | &quot;2019-10-23 11:24:35&quot; |
| dformat | Converte una marca temporale in una stringa data in base a un formato specificato. | dformat(1571829875, &quot;dd-MMM-yyyy hh:mm&quot;) | &quot;23-ott-2019 11:24&quot; |
| date | Converte una stringa data in un oggetto ZoningDateTime (formato ISO 8601). | date(&quot;23-ott-2019 11:24&quot;) | &quot;2019-10-23T11:24:00+00:00&quot; |
| date_part | Recupera le parti della data. Sono supportati i seguenti valori di componente: <br><br>&quot;anno&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;trimestre&quot;<br>&quot;qq&quot;<br>&quot;q&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;dayofyear&quot;<br><br>&quot;dy&quot;&quot;y&quot;&quot;&quot;&quot;d&quot;&quot;d&quot;&quot;settimana&quot;w&quot;&quot;giorno&quot;kolkkkolw&quot;dw&quot;<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>&quot;w&quot;&quot;h&quot;&quot;hh24&quot;&quot;hh12&quot;&quot;minuto&quot;mi&quot;&quot;n&quot;&quot;2D&quot;&quot;2D&quot;&quot;ss&quot;&quot;s&quot;&quot;millisecond&quot;ms&quot; | date_part(date(&quot;2019-10-17 11:55:12&quot;), &quot;MM&quot;) | 10 |
| set_date_part | Sostituisce un componente in una data specificata. Sono accettati i seguenti componenti: <br><br>&quot;anno&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;hour&quot;<br><br><br><br><br><br><br><br><br>&quot;hh&quot;&quot;minuti&quot;&quot;mi&quot;&quot;n&quot;&quot;2D&quot;ss&quot;&quot; | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44.797&quot;) | &quot;2016-04-09T11:44:44.797&quot; |
| make_date_time /<br>make_timestamp | Crea una data da parti. | make_date_time(2019, 10, 17, 11, 55, 12, 999, &quot;America/Los_Angeles&quot;) | `2019-10-17T11:55:12.0&#x200B;00000999-07:00[America/Los_Angeles]` |
| current_timestamp | Restituisce il timestamp corrente. | current_timestamp() | 1571850624571 |
| current_date | Restituisce la data corrente senza un componente ora. | current_date() | &quot;18-nov-2019&quot; |