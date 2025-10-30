---
keywords: Experience Platform;home;argomenti popolari;inserimento batch;inserimento batch;inserimento parziale;inserimento parziale;inserimento parziale;recupero errore;recupero errore;inserimento batch parziale;inserimento batch parziale;inserimento parziale;inserimento;acquisizione;
solution: Experience Platform
title: Panoramica dell’acquisizione in batch parziale
description: Questo documento fornisce un’esercitazione per gestire l’acquisizione in blocco parziale.
exl-id: 25a34da6-5b7c-4747-8ebd-52ba516b9dc3
source-git-commit: bc72f77b1b4a48126be9b49c5c663ff11e9054ea
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 9%

---

# Acquisizione batch parziale

L’acquisizione in batch parziale consente di acquisire dati contenenti errori, fino a una determinata soglia. Con questa funzionalità, gli utenti possono inserire correttamente in Adobe Experience Platform tutti i dati corretti, mentre tutti i dati errati vengono raggruppati in batch separatamente, insieme ai dettagli sul motivo per cui non sono validi.

Questo documento fornisce un’esercitazione per gestire l’acquisizione in blocco parziale.

## Introduzione

Questo tutorial richiede una conoscenza operativa dei vari servizi Adobe Experience Platform coinvolti nell’acquisizione in blocco parziale. Prima di iniziare questo tutorial, consulta la documentazione dei seguenti servizi:

- [Acquisizione batch](./overview.md): metodo con cui [!DNL Experience Platform] acquisisce e memorizza dati da file di dati, ad esempio CSV e Parquet.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per effettuare correttamente chiamate alle API [!DNL Experience Platform].

### Lettura delle chiamate API di esempio

Questa guida fornisce esempi di chiamate API per illustrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere gli esempi di chiamate API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

### Raccogliere i valori per le intestazioni richieste

Per effettuare chiamate alle API di [!DNL Experience Platform], prima è necessario completare il [tutorial sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Completando il tutorial sull’autenticazione si ottengono i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di [!DNL Experience Platform], come mostrato di seguito:

- Autorizzazione: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in specifiche sandbox virtuali. Tutte le richieste alle API [!DNL Experience Platform] richiedono un&#39;intestazione che specifichi il nome della sandbox in cui verrà eseguita l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Experience Platform], consulta la [documentazione di panoramica sulle sandbox](../../sandboxes/home.md).

## Abilitare un batch per l’acquisizione in blocco parziale nell’API {#enable-api}

>[!NOTE]
>
>Questa sezione descrive come abilitare un batch per l’acquisizione in blocco parziale utilizzando l’API. Per istruzioni sull&#39;utilizzo dell&#39;interfaccia utente, leggere il passaggio [abilitare un batch per l&#39;acquisizione batch parziale nell&#39;interfaccia utente](#enable-ui).

Puoi creare un nuovo batch con l’acquisizione parziale abilitata.

Per creare un nuovo batch, segui i passaggi descritti nella [guida per gli sviluppatori sull&#39;acquisizione batch](./api-overview.md). Una volta raggiunto il passaggio **[!UICONTROL Create batch]**, aggiungi il seguente campo nel corpo della richiesta:

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercent": 5
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `enableErrorDiagnostics` | Flag che consente a [!DNL Experience Platform] di generare messaggi di errore dettagliati sul batch. |
| `partialIngestionPercent` | Percentuale di errori accettabili prima che l&#39;intero batch abbia esito negativo. Quindi, in questo esempio, un massimo del 5% del batch può essere un errore, prima che abbia esito negativo. |


## Abilitare un batch per l’acquisizione in blocco parziale nell’interfaccia utente {#enable-ui}

>[!NOTE]
>
>In questa sezione viene descritta l’abilitazione di un batch per l’acquisizione parziale tramite l’interfaccia utente di. Se hai già abilitato un batch per l’acquisizione in blocco parziale utilizzando l’API, puoi passare alla sezione successiva.

Per abilitare un batch per l&#39;acquisizione parziale tramite l&#39;interfaccia utente [!DNL Experience Platform], è possibile creare un nuovo batch tramite le connessioni di origine, creare un nuovo batch in un set di dati esistente o creare un nuovo batch tramite &quot;[!UICONTROL Map CSV to XDM flow]&quot;.

### Crea una nuova connessione sorgente {#new-source}

Per creare una nuova connessione di origine, seguire i passaggi elencati nella [Panoramica origini](../../sources/home.md). Una volta raggiunto il passaggio **[!UICONTROL Dataflow detail]**, prendere nota dei campi **[!UICONTROL Partial ingestion]** e **[!UICONTROL Error diagnostics]**.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

L&#39;interruttore **[!UICONTROL Partial ingestion]** consente di abilitare o disabilitare l&#39;utilizzo dell&#39;acquisizione batch parziale.

L&#39;interruttore **[!UICONTROL Error diagnostics]** viene visualizzato solo quando l&#39;interruttore **[!UICONTROL Partial ingestion]** è disattivato. Questa funzione consente a [!DNL Experience Platform] di generare messaggi di errore dettagliati sui batch acquisiti. Se l&#39;interruttore **[!UICONTROL Partial ingestion]** è attivato, la diagnostica avanzata degli errori viene applicata automaticamente.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

**[!UICONTROL Error threshold]** consente di impostare la percentuale di errori accettabili prima che l&#39;intero batch abbia esito negativo. Per impostazione predefinita, questo valore è impostato su 5%.

### Usa un set di dati esistente {#existing-dataset}

Per utilizzare un set di dati esistente, inizia selezionandone uno. La barra laterale a destra contiene informazioni sul set di dati.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

L&#39;interruttore **[!UICONTROL Partial ingestion]** consente di abilitare o disabilitare l&#39;utilizzo dell&#39;acquisizione batch parziale.

L&#39;interruttore **[!UICONTROL Error diagnostics]** viene visualizzato solo quando l&#39;interruttore **[!UICONTROL Partial ingestion]** è disattivato. Questa funzione consente a [!DNL Experience Platform] di generare messaggi di errore dettagliati sui batch acquisiti. Se l&#39;interruttore **[!UICONTROL Partial ingestion]** è attivato, la diagnostica avanzata degli errori viene applicata automaticamente.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

**[!UICONTROL Error threshold]** consente di impostare la percentuale di errori accettabili prima che l&#39;intero batch abbia esito negativo. Per impostazione predefinita, questo valore è impostato su 5%.

Ora puoi caricare i dati utilizzando il pulsante **Aggiungi dati**, che verrà acquisito tramite l&#39;acquisizione parziale.

### Utilizza il flusso &quot;[!UICONTROL Map CSV to XDM schema]&quot; {#map-flow}

Per utilizzare il flusso &quot;[!UICONTROL Map CSV to XDM schema]&quot;, segui i passaggi elencati nell&#39;esercitazione [Mappare un file CSV](../tutorials/map-csv/overview.md). Una volta raggiunto il passaggio **[!UICONTROL Add data]**, prendere nota dei campi **[!UICONTROL Partial ingestion]** e **[!UICONTROL Error diagnostics]**.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

L&#39;interruttore **[!UICONTROL Partial ingestion]** consente di abilitare o disabilitare l&#39;utilizzo dell&#39;acquisizione batch parziale.

L&#39;interruttore **[!UICONTROL Error diagnostics]** viene visualizzato solo quando l&#39;interruttore **[!UICONTROL Partial ingestion]** è disattivato. Questa funzione consente a [!DNL Experience Platform] di generare messaggi di errore dettagliati sui batch acquisiti. Se l&#39;interruttore **[!UICONTROL Partial ingestion]** è attivato, la diagnostica avanzata degli errori viene applicata automaticamente.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

**[!UICONTROL Error threshold]** consente di impostare la percentuale di errori accettabili prima che l&#39;intero batch abbia esito negativo. Per impostazione predefinita, questo valore è impostato su 5%.

## Abilitare l’acquisizione parziale e la diagnostica degli errori per un flusso di dati esistente

Se un flusso di dati in Experience Platform è stato creato senza abilitare l’acquisizione parziale o la diagnostica degli errori, puoi comunque abilitare queste funzioni senza ricreare il flusso. Abilitando l’acquisizione parziale e una diagnostica affidabile degli errori, puoi migliorare notevolmente l’affidabilità e la facilità di risoluzione dei problemi nei flussi di lavoro di acquisizione dei dati. Leggi le sezioni seguenti per scoprire come abilitare l&#39;acquisizione parziale e la diagnostica degli errori per un flusso di dati esistente utilizzando l&#39;API [!DNL Flow Service].

Per impostazione predefinita, nei flussi di dati potrebbe non essere abilitata l’acquisizione parziale o la diagnostica degli errori. Queste funzioni sono utili per identificare e isolare i problemi durante l’acquisizione dei dati. Utilizzando l&#39;API [!DNL Flow Service], puoi recuperare la configurazione del flusso di dati corrente e applicare le modifiche necessarie utilizzando una richiesta PATCH.

Segui i passaggi seguenti per abilitare l’acquisizione parziale e la diagnostica degli errori per un flusso di dati esistente.

### Recuperare i dettagli del flusso

Per recuperare le configurazioni del flusso di dati, effettua una richiesta GET all&#39;endpoint `/flows/{FLOW_ID}` e fornisci l&#39;ID del flusso di dati. Per ulteriori informazioni sul recupero dei dettagli del flusso di dati, consulta la [Guida all&#39;aggiornamento dei flussi di dati [!DNL Flow Service] API](../../sources/tutorials/api/update-dataflows.md).

Assicurarsi di salvare il valore del campo `etag` restituito nella risposta. Questo è necessario affinché la richiesta di aggiornamento garantisca la coerenza della versione.

### Configurazione del flusso di aggiornamento

Quindi, effettua una richiesta PATCH all&#39;endpoint `/flows/` e fornisci l&#39;ID del flusso di dati per cui desideri abilitare l&#39;acquisizione parziale e la diagnostica degli errori.

>[!IMPORTANT]
>
>- Includi il valore `etag` salvato in precedenza nell&#39;intestazione della richiesta utilizzando la chiave If-Match.
>- Puoi modificare il valore `partialIngestionPercent` in base alle tue esigenze specifiche.

**Formato API**

```http
PATCH /flows/{FLOW_ID}
```

**Richiesta**

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
        {
            "op": "add",
            "path": "/options",
            "value": {
                "partialIngestionPercent": "10"
            }
        },
        {
            "op": "add",
            "path": "/options/errorDiagnosticsEnabled",
            "value": true
        }
    ]'
```

**Risposta**

In caso di esito positivo, la risposta restituisce `id` del flusso di dati e `etag` aggiornato.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"2c000802-0000-0200-0000-613976440000\""
}
```

### Verifica l’aggiornamento

Una volta completato PATCH, effettua una richiesta GET e recupera il flusso di dati per verificare che le modifiche siano state completate correttamente.

**Formato API**

```http
GET /flows/{FLOW_ID}
```

**Richiesta**

La richiesta seguente recupera informazioni aggiornate relative all’ID flusso.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli del flusso di dati, confermando che l’acquisizione parziale e la diagnostica degli errori sono ora abilitate nella sezione `options`.

```json
"options": {
    "partialIngestionPercent": 10,
    "errorDiagnosticsEnabled": true
}
```

## Passaggi successivi {#next-steps}

Questa esercitazione illustra come creare o modificare un set di dati per abilitare l’acquisizione in blocco parziale. Per ulteriori informazioni sull&#39;acquisizione batch, consulta la [guida per gli sviluppatori sull&#39;acquisizione batch](./api-overview.md).

Per informazioni sul monitoraggio degli errori di acquisizione parziale, leggere la [guida alla diagnostica degli errori di acquisizione batch](../quality/error-diagnostics.md).
