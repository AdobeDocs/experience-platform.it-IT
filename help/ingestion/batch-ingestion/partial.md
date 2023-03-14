---
keywords: Experience Platform;home;argomenti popolari;inserimento batch;inserimento batch;inserimento batch;inserimento parziale;inserimento parziale;recupero errore;recupero errore;inserimento batch parziale;inserimento batch parziale;inserimento parziale;inserimento;acquisizione;
solution: Experience Platform
title: Panoramica dell’acquisizione in batch parziale
description: Questo documento fornisce un’esercitazione per gestire l’acquisizione in blocco parziale.
exl-id: 25a34da6-5b7c-4747-8ebd-52ba516b9dc3
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 0%

---

# Acquisizione batch parziale

L’acquisizione in batch parziale consente di acquisire dati contenenti errori, fino a una determinata soglia. Con questa funzionalità, gli utenti possono inserire correttamente in Adobe Experience Platform tutti i dati corretti, mentre tutti i dati errati vengono raggruppati in batch separatamente, insieme ai dettagli sul motivo per cui non sono validi.

Questo documento fornisce un’esercitazione per gestire l’acquisizione in blocco parziale.

## Introduzione

Questo tutorial richiede una conoscenza operativa dei vari servizi Adobe Experience Platform coinvolti nell’acquisizione in blocco parziale. Prima di iniziare questo tutorial, consulta la documentazione dei seguenti servizi:

- [Acquisizione in batch](./overview.md): il metodo che [!DNL Platform] acquisisce e memorizza dati da file di dati, come CSV e Parquet.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Platform] organizza i dati sull’esperienza del cliente.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per effettuare correttamente le chiamate a [!DNL Platform] API.

### Lettura delle chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito il codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere esempi di chiamate API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nel [!DNL Experience Platform] guida alla risoluzione dei problemi.

### Raccogli i valori per le intestazioni richieste

Per effettuare chiamate a [!DNL Platform] , devi prima completare le [tutorial sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento del tutorial sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

- Autorizzazione: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolati in specifiche sandbox virtuali. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui verrà eseguita l’operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], vedere [documentazione di panoramica sulla sandbox](../../sandboxes/home.md).

## Abilitare un batch per l’acquisizione in blocco parziale nell’API {#enable-api}

>[!NOTE]
>
>Questa sezione descrive come abilitare un batch per l’acquisizione in blocco parziale utilizzando l’API. Per istruzioni sull’utilizzo dell’interfaccia utente, leggi la sezione [abilitare un batch per l’acquisizione in blocco parziale nell’interfaccia utente](#enable-ui) passaggio.

Puoi creare un nuovo batch con l’acquisizione parziale abilitata.

Per creare un nuovo batch, segui i passaggi descritti in [guida per gli sviluppatori sull’acquisizione batch](./api-overview.md). Una volta raggiunto il **[!UICONTROL Crea batch]** , aggiungi il seguente campo nel corpo della richiesta:

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercent": 5
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `enableErrorDiagnostics` | Un flag che consente [!DNL Platform] per generare messaggi di errore dettagliati sul batch. |
| `partialIngestionPercent` | Percentuale di errori accettabili prima che l&#39;intero batch abbia esito negativo. Quindi, in questo esempio, un massimo del 5% del batch può essere un errore, prima che abbia esito negativo. |


## Abilitare un batch per l’acquisizione in blocco parziale nell’interfaccia utente {#enable-ui}

>[!NOTE]
>
>Questa sezione descrive come abilitare un batch per l’acquisizione in blocco parziale tramite l’interfaccia utente di. Se hai già abilitato un batch per l’acquisizione in blocco parziale utilizzando l’API, puoi passare alla sezione successiva.

Per abilitare un batch per l’acquisizione parziale tramite [!DNL Platform] interfaccia utente, puoi creare un nuovo batch tramite le connessioni di origine, creare un nuovo batch in un set di dati esistente o creare un nuovo batch tramite il &quot;[!UICONTROL Mappare il flusso CSV a XDM]&quot;.

### Crea una nuova connessione sorgente {#new-source}

Per creare una nuova connessione sorgente, segui i passaggi elencati in [Panoramica sulle origini](../../sources/home.md). Una volta raggiunto il **[!UICONTROL Dettagli del flusso di dati]** , prendi nota della **[!UICONTROL Acquisizione parziale]** e **[!UICONTROL Diagnostica degli errori]** campi.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

Il **[!UICONTROL Acquisizione parziale]** consente di abilitare o disabilitare l’utilizzo dell’acquisizione in blocco parziale.

Il **[!UICONTROL Diagnostica degli errori]** viene visualizzato solo quando **[!UICONTROL Acquisizione parziale]** l&#39;interruttore è disattivato. Questa funzione consente [!DNL Platform] per generare messaggi di errore dettagliati sui batch acquisiti. Se il **[!UICONTROL Acquisizione parziale]** l&#39;interruttore è attivato, la diagnostica avanzata degli errori viene applicata automaticamente.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

Il **[!UICONTROL Soglia di errore]** consente di impostare la percentuale di errori accettabili prima che l’intero batch abbia esito negativo. Per impostazione predefinita, questo valore è impostato su 5%.

### Usa un set di dati esistente {#existing-dataset}

Per utilizzare un set di dati esistente, inizia selezionandone uno. La barra laterale a destra contiene informazioni sul set di dati.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

Il **[!UICONTROL Acquisizione parziale]** consente di abilitare o disabilitare l’utilizzo dell’acquisizione in blocco parziale.

Il **[!UICONTROL Diagnostica degli errori]** viene visualizzato solo quando **[!UICONTROL Acquisizione parziale]** l&#39;interruttore è disattivato. Questa funzione consente [!DNL Platform] per generare messaggi di errore dettagliati sui batch acquisiti. Se il **[!UICONTROL Acquisizione parziale]** l&#39;interruttore è attivato, la diagnostica avanzata degli errori viene applicata automaticamente.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

Il **[!UICONTROL Soglia di errore]** consente di impostare la percentuale di errori accettabili prima che l’intero batch abbia esito negativo. Per impostazione predefinita, questo valore è impostato su 5%.

Ora è possibile caricare i dati utilizzando **Aggiungi dati** e verrà acquisito tramite l’acquisizione parziale.

### Utilizza la &quot;[!UICONTROL Mappa lo schema CSV a XDM]Flusso &quot; {#map-flow}

Per utilizzare la funzione &quot;[!UICONTROL Mappa lo schema CSV a XDM]&quot;, segui i passaggi elencati in [Tutorial su come mappare un file CSV](../tutorials/map-csv/overview.md). Una volta raggiunto il **[!UICONTROL Aggiungi dati]** , prendi nota della **[!UICONTROL Acquisizione parziale]** e **[!UICONTROL Diagnostica degli errori]** campi.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

Il **[!UICONTROL Acquisizione parziale]** consente di abilitare o disabilitare l’utilizzo dell’acquisizione in blocco parziale.

Il **[!UICONTROL Diagnostica degli errori]** viene visualizzato solo quando **[!UICONTROL Acquisizione parziale]** l&#39;interruttore è disattivato. Questa funzione consente [!DNL Platform] per generare messaggi di errore dettagliati sui batch acquisiti. Se il **[!UICONTROL Acquisizione parziale]** l&#39;interruttore è attivato, la diagnostica avanzata degli errori viene applicata automaticamente.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

**[!UICONTROL Soglia di errore]** consente di impostare la percentuale di errori accettabili prima che l’intero batch abbia esito negativo. Per impostazione predefinita, questo valore è impostato su 5%.

## Passaggi successivi {#next-steps}

Questa esercitazione illustra come creare o modificare un set di dati per abilitare l’acquisizione in blocco parziale. Per ulteriori informazioni sull’acquisizione batch, consulta [guida per gli sviluppatori sull’acquisizione batch](./api-overview.md).

Per informazioni sul monitoraggio degli errori di acquisizione parziale, leggi la sezione [guida alla diagnostica degli errori di acquisizione batch](../quality/error-diagnostics.md).
