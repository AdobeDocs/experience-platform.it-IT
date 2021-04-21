---
keywords: Experience Platform;home;argomenti popolari;inserimento batch;inserimento batch;inserimento parziale;inserimento parziale;acquisizione parziale;errore di recupero;errore di recupero;errore di recupero;inserimento batch parziale;inserimento batch parziale;parziale;acquisizione;
solution: Experience Platform
title: Panoramica sull’acquisizione parziale in batch
topic-legacy: overview
description: Questo documento fornisce un'esercitazione per la gestione dell'acquisizione batch parziale.
exl-id: 25a34da6-5b7c-4747-8ebd-52ba516b9dc3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---

# Acquisizione batch parziale

L’acquisizione parziale in batch è la capacità di acquisire dati contenenti errori, fino a una determinata soglia. Grazie a questa funzionalità, gli utenti possono acquisire correttamente tutti i dati corretti in Adobe Experience Platform mentre tutti i dati errati vengono inseriti in batch separatamente, insieme ai dettagli sul motivo per cui non sono validi.

Questo documento fornisce un&#39;esercitazione per la gestione dell&#39;acquisizione batch parziale.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei vari servizi Adobe Experience Platform coinvolti nell’acquisizione parziale dei batch. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti servizi:

- [Acquisizione](./overview.md) batch: Il metodo che  [!DNL Platform] acquisisce e memorizza i dati dai file di dati, come CSV e Parquet.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Platform] vengono organizzati i dati sulla customer experience.

Le sezioni seguenti forniscono informazioni aggiuntive che dovrai conoscere per effettuare correttamente le chiamate alle API [!DNL Platform] .

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform] .

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate alle API [!DNL Platform], devi prima completare l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come mostrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API [!DNL Platform] richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

- nome x-sandbox: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consulta la documentazione di panoramica [sandbox](../../sandboxes/home.md).

## Abilitare un batch per l’acquisizione parziale dei batch nell’API {#enable-api}

>[!NOTE]
>
>In questa sezione viene descritta l’abilitazione di un batch per l’acquisizione parziale dei batch utilizzando l’API. Per istruzioni sull&#39;utilizzo dell&#39;interfaccia utente, leggi il passaggio [enable a batch for parziale ingestion (abilita un batch per l&#39;acquisizione parziale) nell&#39;interfaccia utente](#enable-ui) .

Puoi creare un nuovo batch con l’acquisizione parziale abilitata.

Per creare un nuovo batch, segui i passaggi descritti nella [guida per gli sviluppatori di inserimento batch](./api-overview.md). Una volta raggiunto il passaggio **[!UICONTROL Create batch]**, aggiungi il seguente campo all’interno del corpo della richiesta:

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercentage": 5
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `enableErrorDiagnostics` | Flag che consente a [!DNL Platform] di generare messaggi di errore dettagliati sul batch. |
| `partialIngestionPercentage` | La percentuale di errori accettabili prima dell&#39;intero batch non riuscirà. Quindi, in questo esempio, un massimo del 5% del batch può essere errori, prima che fallisca. |


## Abilitare un batch per l’acquisizione parziale in batch nell’interfaccia utente {#enable-ui}

>[!NOTE]
>
>In questa sezione viene descritta l’abilitazione di un batch per l’acquisizione parziale in batch tramite l’interfaccia utente. Se hai già abilitato un batch per l’inserimento parziale dei batch utilizzando l’API, puoi passare alla sezione successiva.

Per abilitare un batch all&#39;acquisizione parziale tramite l&#39;interfaccia utente [!DNL Platform], puoi creare un nuovo batch tramite le connessioni di origine, creare un nuovo batch in un set di dati esistente o creare un nuovo batch tramite &quot;[!UICONTROL Map CSV to XDM flow]&quot;.

### Crea una nuova connessione sorgente {#new-source}

Per creare una nuova connessione sorgente, segui i passaggi elencati nella [Panoramica delle sorgenti](../../sources/home.md). Una volta raggiunto il passaggio **[!UICONTROL Dataflow detail]**, prendi nota dei campi **[!UICONTROL Partial ingestion]** e **[!UICONTROL Error diagnostics]** .

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

L’opzione **[!UICONTROL Partial ingestion]** consente di abilitare o disabilitare l’utilizzo dell’acquisizione batch parziale.

L&#39;interruttore **[!UICONTROL Error diagnostics]** viene visualizzato solo quando l&#39;interruttore **[!UICONTROL Partial ingestion]** è disattivato. Questa funzione consente a [!DNL Platform] di generare messaggi di errore dettagliati sui batch acquisiti. Se l&#39;interruttore **[!UICONTROL Partial ingestion]** è attivato, la diagnostica degli errori migliorata viene applicata automaticamente.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

Il **[!UICONTROL Error threshold]** consente di impostare la percentuale di errori accettabili prima che l&#39;intero batch non riesca. Per impostazione predefinita, questo valore è impostato su 5%.

### Utilizza un set di dati esistente {#existing-dataset}

Per utilizzare un set di dati esistente, inizia selezionando un set di dati. La barra laterale a destra si riempie di informazioni sul set di dati.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

L’opzione **[!UICONTROL Partial ingestion]** consente di abilitare o disabilitare l’utilizzo dell’acquisizione batch parziale.

L&#39;interruttore **[!UICONTROL Error diagnostics]** viene visualizzato solo quando l&#39;interruttore **[!UICONTROL Partial ingestion]** è disattivato. Questa funzione consente a [!DNL Platform] di generare messaggi di errore dettagliati sui batch acquisiti. Se l&#39;interruttore **[!UICONTROL Partial ingestion]** è attivato, la diagnostica degli errori migliorata viene applicata automaticamente.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

Il **[!UICONTROL Error threshold]** consente di impostare la percentuale di errori accettabili prima che l&#39;intero batch non riesca. Per impostazione predefinita, questo valore è impostato su 5%.

Ora è possibile caricare i dati utilizzando il pulsante **Aggiungi dati** e verranno acquisiti utilizzando l’acquisizione parziale.

### Utilizzare il flusso &quot;[!UICONTROL Map CSV to XDM schema]&quot; {#map-flow}

Per utilizzare il flusso &quot;[!UICONTROL Map CSV to XDM schema]&quot;, segui i passaggi elencati nell&#39; [Esercitazione Mappa un file CSV](../tutorials/map-a-csv-file.md). Una volta raggiunto il passaggio **[!UICONTROL Add data]**, prendi nota dei campi **[!UICONTROL Partial ingestion]** e **[!UICONTROL Error diagnostics]** .

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

L’opzione **[!UICONTROL Partial ingestion]** consente di abilitare o disabilitare l’utilizzo dell’acquisizione batch parziale.

L&#39;interruttore **[!UICONTROL Error diagnostics]** viene visualizzato solo quando l&#39;interruttore **[!UICONTROL Partial ingestion]** è disattivato. Questa funzione consente a [!DNL Platform] di generare messaggi di errore dettagliati sui batch acquisiti. Se l&#39;interruttore **[!UICONTROL Partial ingestion]** è attivato, la diagnostica degli errori migliorata viene applicata automaticamente.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

**[!UICONTROL Error threshold]** consente di impostare la percentuale di errori accettabili prima che l’intero batch non riesca. Per impostazione predefinita, questo valore è impostato su 5%.

## Passaggi successivi {#next-steps}

Questa esercitazione spiega come creare o modificare un set di dati per abilitare l’acquisizione parziale di batch. Per ulteriori informazioni sull&#39;acquisizione batch, leggere la [guida per sviluppatori per l&#39;acquisizione batch](./api-overview.md).

Per informazioni sul monitoraggio degli errori di acquisizione parziale, consulta la [guida alla diagnostica degli errori di acquisizione batch](../quality/error-diagnostics.md).
