---
keywords: Experience Platform;home;argomenti popolari;inserimento batch;inserimento batch;inserimento parziale;inserimento parziale;acquisizione parziale;errore di recupero;errore di recupero;errore di recupero;inserimento batch parziale;inserimento batch parziale;parziale;acquisizione;
solution: Experience Platform
title: Panoramica sull’acquisizione parziale in batch
topic-legacy: overview
description: Questo documento fornisce un'esercitazione per la gestione dell'acquisizione batch parziale.
exl-id: 25a34da6-5b7c-4747-8ebd-52ba516b9dc3
source-git-commit: 636d6dcbe8eb73b7898fc3794f6b4567956e5618
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 0%

---

# Acquisizione batch parziale

L’acquisizione parziale in batch è la capacità di acquisire dati contenenti errori, fino a una determinata soglia. Grazie a questa funzionalità, gli utenti possono acquisire correttamente tutti i dati corretti in Adobe Experience Platform mentre tutti i dati errati vengono inseriti in batch separatamente, insieme ai dettagli sul motivo per cui non sono validi.

Questo documento fornisce un&#39;esercitazione per la gestione dell&#39;acquisizione batch parziale.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei vari servizi Adobe Experience Platform coinvolti nell’acquisizione parziale dei batch. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti servizi:

- [Acquisizione batch](./overview.md): Il metodo che [!DNL Platform] acquisisce e memorizza i dati dai file di dati, come CSV e Parquet.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il quadro standardizzato [!DNL Platform] organizza i dati sulla customer experience.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per effettuare correttamente le chiamate a [!DNL Platform] API.

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione sulle [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] guida alla risoluzione dei problemi.

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate a [!DNL Platform] API, devi prima completare l’ [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], vedi [documentazione panoramica su sandbox](../../sandboxes/home.md).

## Abilitare un batch per l’acquisizione parziale in batch nell’API {#enable-api}

>[!NOTE]
>
>In questa sezione viene descritta l’abilitazione di un batch per l’acquisizione parziale dei batch utilizzando l’API. Per istruzioni sull&#39;utilizzo dell&#39;interfaccia utente, leggere il [abilitare un batch per l’acquisizione parziale in batch nell’interfaccia utente](#enable-ui) passo.

Puoi creare un nuovo batch con l’acquisizione parziale abilitata.

Per creare un nuovo batch, segui i passaggi descritti nella sezione [guida per gli sviluppatori di batch ingestion](./api-overview.md). Una volta raggiunto il **[!UICONTROL Crea batch]** aggiungi il seguente campo nel corpo della richiesta:

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercent": 5
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `enableErrorDiagnostics` | Flag che consente [!DNL Platform] per generare messaggi di errore dettagliati sul batch. |
| `partialIngestionPercent` | La percentuale di errori accettabili prima dell&#39;intero batch non riuscirà. Quindi, in questo esempio, un massimo del 5% del batch può essere errori, prima che fallisca. |


## Abilitare un batch per l’acquisizione parziale in batch nell’interfaccia utente {#enable-ui}

>[!NOTE]
>
>In questa sezione viene descritta l’abilitazione di un batch per l’acquisizione parziale in batch tramite l’interfaccia utente. Se hai già abilitato un batch per l’inserimento parziale dei batch utilizzando l’API, puoi passare alla sezione successiva.

Per abilitare un batch all’acquisizione parziale tramite [!DNL Platform] Nell’interfaccia utente, puoi creare un nuovo batch tramite connessioni sorgente, creare un nuovo batch in un set di dati esistente o creare un nuovo batch tramite &quot;[!UICONTROL Flusso da CSV a XDM]&quot;.

### Crea una nuova connessione sorgente {#new-source}

Per creare una nuova connessione sorgente, segui i passaggi elencati nella sezione [Panoramica delle origini](../../sources/home.md). Una volta raggiunto il **[!UICONTROL Dettaglio flusso di dati]** , prendere atto del **[!UICONTROL Acquisizione parziale]** e **[!UICONTROL Diagnostica degli errori]** campi.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

La **[!UICONTROL Acquisizione parziale]** consente di abilitare o disabilitare l’utilizzo dell’acquisizione batch parziale.

La **[!UICONTROL Diagnostica degli errori]** compare solo quando **[!UICONTROL Acquisizione parziale]** l&#39;interruttore è disattivato. Questa funzione consente [!DNL Platform] per generare messaggi di errore dettagliati sui batch acquisiti. Se la **[!UICONTROL Acquisizione parziale]** l’opzione è attivata, la diagnostica degli errori migliorata viene applicata automaticamente.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

La **[!UICONTROL Soglia di errore]** consente di impostare la percentuale di errori accettabili prima che l’intero batch non riesca. Per impostazione predefinita, questo valore è impostato su 5%.

### Utilizzare un set di dati esistente {#existing-dataset}

Per utilizzare un set di dati esistente, inizia selezionando un set di dati. La barra laterale a destra si riempie di informazioni sul set di dati.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

La **[!UICONTROL Acquisizione parziale]** consente di abilitare o disabilitare l’utilizzo dell’acquisizione batch parziale.

La **[!UICONTROL Diagnostica degli errori]** compare solo quando **[!UICONTROL Acquisizione parziale]** l&#39;interruttore è disattivato. Questa funzione consente [!DNL Platform] per generare messaggi di errore dettagliati sui batch acquisiti. Se la **[!UICONTROL Acquisizione parziale]** l’opzione è attivata, la diagnostica degli errori migliorata viene applicata automaticamente.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

La **[!UICONTROL Soglia di errore]** consente di impostare la percentuale di errori accettabili prima che l’intero batch non riesca. Per impostazione predefinita, questo valore è impostato su 5%.

Ora puoi caricare i dati utilizzando la **Aggiungi dati** e verrà acquisito tramite acquisizione parziale.

### Utilizza il &quot;[!UICONTROL Mappatura di CSV su schema XDM]&quot; flusso {#map-flow}

Per utilizzare &quot;[!UICONTROL Mappatura di CSV su schema XDM]&quot; flusso, segui i passaggi elencati nel [Esercitazione sulla mappatura di un file CSV](../tutorials/map-a-csv-file.md). Una volta raggiunto il **[!UICONTROL Aggiungi dati]** , prendere atto del **[!UICONTROL Acquisizione parziale]** e **[!UICONTROL Diagnostica degli errori]** campi.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

La **[!UICONTROL Acquisizione parziale]** consente di abilitare o disabilitare l’utilizzo dell’acquisizione batch parziale.

La **[!UICONTROL Diagnostica degli errori]** compare solo quando **[!UICONTROL Acquisizione parziale]** l&#39;interruttore è disattivato. Questa funzione consente [!DNL Platform] per generare messaggi di errore dettagliati sui batch acquisiti. Se la **[!UICONTROL Acquisizione parziale]** l’opzione è attivata, la diagnostica degli errori migliorata viene applicata automaticamente.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

**[!UICONTROL Soglia di errore]** consente di impostare la percentuale di errori accettabili prima che l’intero batch non riesca. Per impostazione predefinita, questo valore è impostato su 5%.

## Passaggi successivi {#next-steps}

Questa esercitazione spiega come creare o modificare un set di dati per abilitare l’acquisizione parziale di batch. Per ulteriori informazioni sull’acquisizione in batch, leggere il [guida per gli sviluppatori di batch ingestion](./api-overview.md).

Per informazioni sul monitoraggio degli errori di acquisizione parziale, consulta la sezione [guida alla diagnostica degli errori di acquisizione in batch](../quality/error-diagnostics.md).
