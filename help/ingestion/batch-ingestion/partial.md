---
keywords: Experience Platform;home;argomenti popolari;inserimento batch;inserimento batch;inserimento batch;inserimento parziale;inserimento parziale;recupero errore;recupero errore;inserimento batch parziale;inserimento batch parziale;inserimento parziale;inserimento;acquisizione;
solution: Experience Platform
title: Panoramica dell’acquisizione in batch parziale
description: Questo documento fornisce un’esercitazione per gestire l’acquisizione in blocco parziale.
exl-id: 25a34da6-5b7c-4747-8ebd-52ba516b9dc3
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 7%

---

# Acquisizione batch parziale

L’acquisizione in batch parziale consente di acquisire dati contenenti errori, fino a una determinata soglia. Con questa funzionalità, gli utenti possono inserire correttamente in Adobe Experience Platform tutti i dati corretti, mentre tutti i dati errati vengono raggruppati in batch separatamente, insieme ai dettagli sul motivo per cui non sono validi.

Questo documento fornisce un’esercitazione per gestire l’acquisizione in blocco parziale.

## Introduzione

Questo tutorial richiede una conoscenza operativa dei vari servizi Adobe Experience Platform coinvolti nell’acquisizione in blocco parziale. Prima di iniziare questo tutorial, consulta la documentazione dei seguenti servizi:

- [Acquisizione batch](./overview.md): metodo con cui [!DNL Platform] acquisisce e memorizza dati da file di dati, ad esempio CSV e Parquet.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): framework standardizzato tramite il quale [!DNL Platform] organizza i dati sull&#39;esperienza del cliente.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per effettuare correttamente chiamate alle API [!DNL Platform].

### Lettura delle chiamate API di esempio

Questa guida fornisce esempi di chiamate API per illustrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

### Raccogliere i valori per le intestazioni richieste

Per effettuare chiamate alle API [!DNL Platform], devi prima completare l&#39;[esercitazione di autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Completando il tutorial sull’autenticazione si ottengono i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di [!DNL Experience Platform], come mostrato di seguito:

- Autorizzazione: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in specifiche sandbox virtuali. Tutte le richieste alle API [!DNL Platform] richiedono un&#39;intestazione che specifichi il nome della sandbox in cui verrà eseguita l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consulta la [documentazione di panoramica sulle sandbox](../../sandboxes/home.md).

## Abilitare un batch per l’acquisizione in blocco parziale nell’API {#enable-api}

>[!NOTE]
>
>Questa sezione descrive come abilitare un batch per l’acquisizione in blocco parziale utilizzando l’API. Per istruzioni sull&#39;utilizzo dell&#39;interfaccia utente, leggere il passaggio [abilitare un batch per l&#39;acquisizione batch parziale nell&#39;interfaccia utente](#enable-ui).

Puoi creare un nuovo batch con l’acquisizione parziale abilitata.

Per creare un nuovo batch, segui i passaggi descritti nella [guida per gli sviluppatori sull&#39;acquisizione batch](./api-overview.md). Una volta raggiunto il passaggio **[!UICONTROL Crea batch]**, aggiungi il seguente campo nel corpo della richiesta:

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercent": 5
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `enableErrorDiagnostics` | Flag che consente a [!DNL Platform] di generare messaggi di errore dettagliati sul batch. |
| `partialIngestionPercent` | Percentuale di errori accettabili prima che l&#39;intero batch abbia esito negativo. Quindi, in questo esempio, un massimo del 5% del batch può essere un errore, prima che abbia esito negativo. |


## Abilitare un batch per l’acquisizione in blocco parziale nell’interfaccia utente {#enable-ui}

>[!NOTE]
>
>In questa sezione viene descritta l’abilitazione di un batch per l’acquisizione parziale tramite l’interfaccia utente di. Se hai già abilitato un batch per l’acquisizione in blocco parziale utilizzando l’API, puoi passare alla sezione successiva.

Per abilitare un batch per l&#39;acquisizione parziale tramite l&#39;interfaccia utente [!DNL Platform], è possibile creare un nuovo batch tramite le connessioni di origine, creare un nuovo batch in un set di dati esistente o creare un nuovo batch tramite il &quot;[!UICONTROL Flusso CSV-XDM]&quot;.

### Crea una nuova connessione sorgente {#new-source}

Per creare una nuova connessione di origine, seguire i passaggi elencati nella [Panoramica origini](../../sources/home.md). Una volta raggiunto il passaggio **[!UICONTROL Dettagli flusso di dati]**, prendi nota dei campi **[!UICONTROL Acquisizione parziale]** e **[!UICONTROL Diagnostica errori]**.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

L&#39;opzione **[!UICONTROL Acquisizione parziale]** consente di abilitare o disabilitare l&#39;utilizzo dell&#39;acquisizione batch parziale.

L&#39;interruttore **[!UICONTROL Diagnostica errori]** viene visualizzato solo quando l&#39;interruttore **[!UICONTROL Acquisizione parziale]** è disattivato. Questa funzione consente a [!DNL Platform] di generare messaggi di errore dettagliati sui batch acquisiti. Se l&#39;opzione **[!UICONTROL Acquisizione parziale]** è attivata, la diagnostica avanzata degli errori viene applicata automaticamente.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

La **[!UICONTROL soglia di errore]** consente di impostare la percentuale di errori accettabili prima che l&#39;intero batch abbia esito negativo. Per impostazione predefinita, questo valore è impostato su 5%.

### Usa un set di dati esistente {#existing-dataset}

Per utilizzare un set di dati esistente, inizia selezionandone uno. La barra laterale a destra contiene informazioni sul set di dati.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

L&#39;opzione **[!UICONTROL Acquisizione parziale]** consente di abilitare o disabilitare l&#39;utilizzo dell&#39;acquisizione batch parziale.

L&#39;interruttore **[!UICONTROL Diagnostica errori]** viene visualizzato solo quando l&#39;interruttore **[!UICONTROL Acquisizione parziale]** è disattivato. Questa funzione consente a [!DNL Platform] di generare messaggi di errore dettagliati sui batch acquisiti. Se l&#39;opzione **[!UICONTROL Acquisizione parziale]** è attivata, la diagnostica avanzata degli errori viene applicata automaticamente.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

La **[!UICONTROL soglia di errore]** consente di impostare la percentuale di errori accettabili prima che l&#39;intero batch abbia esito negativo. Per impostazione predefinita, questo valore è impostato su 5%.

Ora puoi caricare i dati utilizzando il pulsante **Aggiungi dati**, che verrà acquisito tramite l&#39;acquisizione parziale.

### Utilizza il flusso &quot;[!UICONTROL Mappatura di CSV a schema XDM]&quot; {#map-flow}

Per utilizzare il flusso &quot;[!UICONTROL Mappare il file CSV su schema XDM]&quot;, segui i passaggi elencati nell&#39;esercitazione [Mappare un file CSV](../tutorials/map-csv/overview.md). Una volta raggiunto il passaggio **[!UICONTROL Aggiungi dati]**, prendi nota dei campi **[!UICONTROL Acquisizione parziale]** e **[!UICONTROL Diagnostica errori]**.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

L&#39;opzione **[!UICONTROL Acquisizione parziale]** consente di abilitare o disabilitare l&#39;utilizzo dell&#39;acquisizione batch parziale.

L&#39;interruttore **[!UICONTROL Diagnostica errori]** viene visualizzato solo quando l&#39;interruttore **[!UICONTROL Acquisizione parziale]** è disattivato. Questa funzione consente a [!DNL Platform] di generare messaggi di errore dettagliati sui batch acquisiti. Se l&#39;opzione **[!UICONTROL Acquisizione parziale]** è attivata, la diagnostica avanzata degli errori viene applicata automaticamente.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

**[!UICONTROL Soglia di errore]** consente di impostare la percentuale di errori accettabili prima che l&#39;intero batch abbia esito negativo. Per impostazione predefinita, questo valore è impostato su 5%.

## Passaggi successivi {#next-steps}

Questa esercitazione illustra come creare o modificare un set di dati per abilitare l’acquisizione in blocco parziale. Per ulteriori informazioni sull&#39;acquisizione batch, consulta la [guida per gli sviluppatori sull&#39;acquisizione batch](./api-overview.md).

Per informazioni sul monitoraggio degli errori di acquisizione parziale, leggere la [guida alla diagnostica degli errori di acquisizione batch](../quality/error-diagnostics.md).
