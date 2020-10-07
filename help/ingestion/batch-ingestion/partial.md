---
keywords: Experience Platform;home;popular topics;batch ingestion;Batch ingestion;partial ingestion;Partial ingestion;Retrieve error;retrieve error;Partial batch ingestion;partial batch ingestion;partial;ingestion;Ingestion;
solution: Experience Platform
title: Panoramica sull’assimilazione parziale dei batch
topic: overview
description: Questo documento fornisce un’esercitazione per la gestione dell’assimilazione parziale dei batch.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 0%

---


# Iniezione parziale del batch

L&#39;assimilazione parziale dei batch è la capacità di assimilare i dati contenenti errori, fino a una determinata soglia. Grazie a questa funzionalità, gli utenti possono trasferire correttamente tutti i dati corretti in Adobe Experience Platform mentre tutti i dati errati vengono raggruppati separatamente, insieme ai dettagli sul motivo per cui non sono validi.

Questo documento fornisce un’esercitazione per la gestione dell’assimilazione parziale dei batch.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei diversi servizi Adobe Experience Platform coinvolti nell&#39;assimilazione parziale dei batch. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti servizi:

- [Caricamento](./overview.md)batch: Metodo che [!DNL Platform] raccoglie e memorizza i dati dai file di dati, come CSV e Parquet.
- [[!DNL Experience Data Model] (XDM)](../../xdm/home.md): Il framework standard con cui [!DNL Platform] organizzare i dati relativi all&#39;esperienza del cliente.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per eseguire correttamente le chiamate alle [!DNL Platform] API.

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere chiamate](../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla [!DNL Experience Platform] risoluzione dei problemi.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è prima necessario completare l&#39;esercitazione [sull&#39;](../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate [!DNL Experience Platform] API, come illustrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

## Abilitare un batch per l&#39;assimilazione parziale dei batch nell&#39;API {#enable-api}

>[!NOTE]
>
>Questa sezione descrive come abilitare un batch per l&#39;assimilazione parziale dei batch mediante l&#39;API. Per istruzioni sull’utilizzo dell’interfaccia utente, leggete il passaggio [Abilita batch per l’inserimento parziale dei batch nell’interfaccia utente](#enable-ui) .

Potete creare un nuovo batch con l’assimilazione parziale abilitata.

Per creare un nuovo batch, segui i passaggi descritti nella guida [per gli sviluppatori per l’assimilazione](./api-overview.md)batch. Una volta raggiunto il **[!UICONTROL Create batch]** passaggio, aggiungete il seguente campo all’interno del corpo della richiesta:

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercentage": 5
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `enableErrorDiagnostics` | Flag che consente [!DNL Platform] di generare messaggi di errore dettagliati sul batch. |
| `partialIngestionPercentage` | Percentuale di errori accettabili prima che l&#39;intero batch non riesca. Quindi, in questo esempio, un massimo del 5% del batch può essere costituito da errori, prima che venga meno. |


## Abilitare un batch per l’assimilazione parziale dei batch nell’interfaccia utente {#enable-ui}

>[!NOTE]
>
>Questa sezione descrive come abilitare un batch per l’assimilazione parziale dei batch utilizzando l’interfaccia utente. Se avete già attivato un batch per l&#39;assimilazione parziale dei batch utilizzando l&#39;API, potete passare alla sezione successiva.

Per abilitare un batch per l’assimilazione parziale nell’ [!DNL Platform] interfaccia utente, potete creare un nuovo batch tramite connessioni sorgente, creare un nuovo batch in un set di dati esistente o creare un nuovo batch tramite il[!UICONTROL Map CSV to XDM flow]&quot;.

### Creare una nuova connessione di origine {#new-source}

Per creare una nuova connessione di origine, segui i passaggi elencati nella panoramica [](../../sources/home.md)Origini. Una volta raggiunto il **[!UICONTROL Dataflow detail]** passaggio, prendete nota dei **[!UICONTROL Partial ingestion]** campi e **[!UICONTROL Error diagnostics]** .

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

L’ **[!UICONTROL Partial ingestion]** interruttore consente di attivare o disattivare l’inserimento parziale dei batch.

L&#39; **[!UICONTROL Error diagnostics]** interruttore viene visualizzato solo quando l&#39; **[!UICONTROL Partial ingestion]** interruttore è disattivato. Questa funzione consente [!DNL Platform] di generare messaggi di errore dettagliati sui batch acquisiti. Se l&#39; **[!UICONTROL Partial ingestion]** interruttore è attivato, la diagnostica degli errori avanzata viene applicata automaticamente.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

Consente di **[!UICONTROL Error threshold]** impostare la percentuale di errori accettabili prima che l&#39;intero batch non riesca. Per impostazione predefinita, questo valore è impostato su 5%.

### Utilizzare un dataset esistente {#existing-dataset}

Per utilizzare un set di dati esistente, iniziare selezionando un set di dati. La barra laterale a destra include informazioni sul set di dati.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

L’ **[!UICONTROL Partial ingestion]** interruttore consente di attivare o disattivare l’inserimento parziale dei batch.

L&#39; **[!UICONTROL Error diagnostics]** interruttore viene visualizzato solo quando l&#39; **[!UICONTROL Partial ingestion]** interruttore è disattivato. Questa funzione consente [!DNL Platform] di generare messaggi di errore dettagliati sui batch acquisiti. Se l&#39; **[!UICONTROL Partial ingestion]** interruttore è attivato, la diagnostica degli errori avanzata viene applicata automaticamente.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

Consente di **[!UICONTROL Error threshold]** impostare la percentuale di errori accettabili prima che l&#39;intero batch non riesca. Per impostazione predefinita, questo valore è impostato su 5%.

Ora puoi caricare i dati tramite il pulsante **Aggiungi dati** e li assimilerai parzialmente.

### Utilizzare il flusso &quot;[!UICONTROL Map CSV to XDM schema]&quot; {#map-flow}

Per usare il flusso[!UICONTROL Map CSV to XDM schema]&quot;di prova&quot;, segui i passaggi elencati nell’esercitazione [Mappa un file CSV](../tutorials/map-a-csv-file.md). Una volta raggiunto il **[!UICONTROL Add data]** passaggio, prendete nota dei **[!UICONTROL Partial ingestion]** campi e **[!UICONTROL Error diagnostics]** .

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

L’ **[!UICONTROL Partial ingestion]** interruttore consente di attivare o disattivare l’inserimento parziale dei batch.

L&#39; **[!UICONTROL Error diagnostics]** interruttore viene visualizzato solo quando l&#39; **[!UICONTROL Partial ingestion]** interruttore è disattivato. Questa funzione consente [!DNL Platform] di generare messaggi di errore dettagliati sui batch acquisiti. Se l&#39; **[!UICONTROL Partial ingestion]** interruttore è attivato, la diagnostica degli errori avanzata viene applicata automaticamente.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

**[!UICONTROL Error threshold]** consente di impostare la percentuale di errori accettabili prima che l’intero batch non riesca. Per impostazione predefinita, questo valore è impostato su 5%.

## Passaggi successivi {#next-steps}

In questa esercitazione è stato illustrato come creare o modificare un dataset per abilitare l’assimilazione parziale dei batch. Per ulteriori informazioni sull&#39;assimilazione batch, leggere la guida [per gli sviluppatori di](./api-overview.md)inserimento batch.

Per informazioni sul monitoraggio degli errori di assimilazione parziale, consultate la guida [alla diagnostica degli errori di assimilazione](../quality/error-diagnostics.md)batch.
