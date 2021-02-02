---
keywords: ' Experience Platform;home;argomenti popolari;ingestione batch;ingestione parziale;assimilazione parziale;errore di recupero;errore di recupero;errore di recupero;inserimento batch parziale;assimilazione parziale;parziale;inserimento;inserimento;'
solution: Experience Platform
title: Panoramica sull’assimilazione parziale dei batch
topic: overview
description: Questo documento fornisce un’esercitazione per la gestione dell’assimilazione parziale dei batch.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---


# Iniezione parziale del batch

L&#39;assimilazione parziale dei batch è la capacità di assimilare i dati contenenti errori, fino a una determinata soglia. Grazie a questa funzionalità, gli utenti possono trasferire correttamente tutti i dati corretti in Adobe Experience Platform mentre tutti i dati errati vengono raggruppati separatamente, insieme ai dettagli sul motivo per cui non sono validi.

Questo documento fornisce un’esercitazione per la gestione dell’assimilazione parziale dei batch.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei diversi servizi Adobe Experience Platform coinvolti nell&#39;assimilazione parziale dei batch. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti servizi:

- [Caricamento](./overview.md) batch: Metodo che  [!DNL Platform] raccoglie e memorizza i dati dai file di dati, come CSV e Parquet.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il framework standard con cui  [!DNL Platform] organizzare i dati relativi all&#39;esperienza dei clienti.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per eseguire correttamente le chiamate alle [!DNL Platform] API.

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consultate la sezione relativa a [come leggere chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è innanzitutto necessario completare l&#39;esercitazione sull&#39;autenticazione [a2/>. ](https://www.adobe.com/go/platform-api-authentication-en) Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come illustrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui verrà eseguita l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consultate la documentazione di [panoramica sulla sandbox](../../sandboxes/home.md).

## Abilitare un batch per l&#39;inserimento parziale dei batch nell&#39;API {#enable-api}

>[!NOTE]
>
>Questa sezione descrive come abilitare un batch per l&#39;assimilazione parziale dei batch mediante l&#39;API. Per istruzioni sull&#39;utilizzo dell&#39;interfaccia utente, leggere il passaggio [abilita un batch per l&#39;inserimento parziale dei batch nell&#39;interfaccia utente](#enable-ui).

Potete creare un nuovo batch con l’assimilazione parziale abilitata.

Per creare un nuovo batch, seguire i passaggi descritti nella [guida per gli sviluppatori di assimilazione batch](./api-overview.md). Una volta raggiunto il passaggio **[!UICONTROL Create batch]**, aggiungete il seguente campo all&#39;interno del corpo della richiesta:

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercentage": 5
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `enableErrorDiagnostics` | Flag che consente a [!DNL Platform] di generare messaggi di errore dettagliati sul batch. |
| `partialIngestionPercentage` | Percentuale di errori accettabili prima che l&#39;intero batch non riesca. Quindi, in questo esempio, un massimo del 5% del batch può essere costituito da errori, prima che venga meno. |


## Abilitare un batch per l&#39;inserimento parziale dei batch nell&#39;interfaccia utente {#enable-ui}

>[!NOTE]
>
>Questa sezione descrive come abilitare un batch per l’assimilazione parziale dei batch utilizzando l’interfaccia utente. Se avete già attivato un batch per l&#39;assimilazione parziale dei batch utilizzando l&#39;API, potete passare alla sezione successiva.

Per abilitare un batch per l&#39;assimilazione parziale tramite l&#39;interfaccia utente di [!DNL Platform], è possibile creare un nuovo batch mediante connessioni di origine, creare un nuovo batch in un dataset esistente o creare un nuovo batch tramite &quot;[!UICONTROL Map CSV to XDM flow]&quot;.

### Creare una nuova connessione di origine {#new-source}

Per creare una nuova connessione di origine, segui i passaggi elencati nella [Panoramica delle origini](../../sources/home.md). Una volta raggiunto il passaggio **[!UICONTROL Dataflow detail]**, prendere nota dei campi **[!UICONTROL Partial ingestion]** e **[!UICONTROL Error diagnostics]**.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

L&#39;interruttore **[!UICONTROL Partial ingestion]** consente di abilitare o disabilitare l&#39;inserimento parziale dei batch.

L&#39;interruttore **[!UICONTROL Error diagnostics]** viene visualizzato solo quando l&#39;interruttore **[!UICONTROL Partial ingestion]** è disattivato. Questa funzione consente a [!DNL Platform] di generare messaggi di errore dettagliati sui batch da inserire. Se l&#39;interruttore **[!UICONTROL Partial ingestion]** è attivato, la diagnostica degli errori avanzata viene applicata automaticamente.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

**[!UICONTROL Error threshold]** consente di impostare la percentuale di errori accettabili prima che l&#39;intero batch non riesca. Per impostazione predefinita, questo valore è impostato su 5%.

### Utilizza un set di dati esistente {#existing-dataset}

Per utilizzare un set di dati esistente, iniziare selezionando un set di dati. La barra laterale a destra include informazioni sul set di dati.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

L&#39;interruttore **[!UICONTROL Partial ingestion]** consente di abilitare o disabilitare l&#39;inserimento parziale dei batch.

L&#39;interruttore **[!UICONTROL Error diagnostics]** viene visualizzato solo quando l&#39;interruttore **[!UICONTROL Partial ingestion]** è disattivato. Questa funzione consente a [!DNL Platform] di generare messaggi di errore dettagliati sui batch da inserire. Se l&#39;interruttore **[!UICONTROL Partial ingestion]** è attivato, la diagnostica degli errori avanzata viene applicata automaticamente.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

**[!UICONTROL Error threshold]** consente di impostare la percentuale di errori accettabili prima che l&#39;intero batch non riesca. Per impostazione predefinita, questo valore è impostato su 5%.

Ora puoi caricare i dati utilizzando il pulsante **Aggiungi dati**, che verrà assimilato parzialmente.

### Utilizzare il flusso &quot;[!UICONTROL Map CSV to XDM schema]&quot; {#map-flow}

Per utilizzare il flusso &quot;[!UICONTROL Map CSV to XDM schema]&quot;, segui i passaggi elencati in [Mappa un&#39;esercitazione file CSV](../tutorials/map-a-csv-file.md). Una volta raggiunto il passaggio **[!UICONTROL Add data]**, prendere nota dei campi **[!UICONTROL Partial ingestion]** e **[!UICONTROL Error diagnostics]**.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

L&#39;interruttore **[!UICONTROL Partial ingestion]** consente di abilitare o disabilitare l&#39;inserimento parziale dei batch.

L&#39;interruttore **[!UICONTROL Error diagnostics]** viene visualizzato solo quando l&#39;interruttore **[!UICONTROL Partial ingestion]** è disattivato. Questa funzione consente a [!DNL Platform] di generare messaggi di errore dettagliati sui batch da inserire. Se l&#39;interruttore **[!UICONTROL Partial ingestion]** è attivato, la diagnostica degli errori avanzata viene applicata automaticamente.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

**[!UICONTROL Error threshold]** consente di impostare la percentuale di errori accettabili prima che l’intero batch non riesca. Per impostazione predefinita, questo valore è impostato su 5%.

## Passaggi successivi {#next-steps}

In questa esercitazione è stato illustrato come creare o modificare un dataset per abilitare l’assimilazione parziale dei batch. Per ulteriori informazioni sull&#39;assimilazione batch, leggere la [guida per gli sviluppatori di assimilazione batch](./api-overview.md).

Per informazioni sul monitoraggio degli errori di assimilazione parziale, leggere la [guida per la diagnostica degli errori di caricamento batch](../quality/error-diagnostics.md).
