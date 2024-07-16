---
keywords: Experience Platform;home;argomenti popolari;servizio di flusso;API;api;eliminare;eliminare i flussi di dati di destinazione
solution: Experience Platform
title: Eliminare un flusso di dati di destinazione utilizzando l’API del servizio Flusso
type: Tutorial
description: Scopri come eliminare i flussi di dati nelle destinazioni batch e di streaming utilizzando l’API del servizio Flusso.
exl-id: fa40cf97-46c6-4a10-b53c-30bed2dd1b2d
source-git-commit: c35a29d4e9791b566d9633b651aecd2c16f88507
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 14%

---

# Eliminare un flusso di dati di destinazione utilizzando l’API del servizio Flusso

È possibile eliminare i flussi di dati che contengono errori o che sono diventati obsoleti utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Questa esercitazione descrive i passaggi per eliminare i flussi di dati sia per le destinazioni batch che per quelle in streaming utilizzando [!DNL Flow Service].

## Introduzione {#get-started}

Questo tutorial richiede un ID di flusso valido. Se non disponi di un ID di flusso valido, seleziona la destinazione desiderata dal [catalogo delle destinazioni](../catalog/overview.md) e segui i passaggi descritti per [connettersi alla destinazione](../ui/connect-destination.md) e [attivare i dati](../ui/activation-overview.md) prima di provare questa esercitazione.

Questo tutorial richiede anche una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Destinazioni](../home.md): [!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l&#39;attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.
* [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza di [!DNL Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per eliminare correttamente un flusso di dati utilizzando l&#39;API [!DNL Flow Service].

### Lettura delle chiamate API di esempio {#reading-sample-api-calls}

Questo tutorial fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

### Raccogliere i valori per le intestazioni richieste {#gather-values-for-required-headers}

Per effettuare chiamate alle API [!DNL Platform], devi prima completare l&#39;[esercitazione di autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Completando il tutorial sull’autenticazione si ottengono i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di [!DNL Experience Platform], come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Tutte le risorse in [!DNL Experience Platform], incluse quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API [!DNL Platform] richiedono un&#39;intestazione che specifichi il nome della sandbox in cui verrà eseguita l&#39;operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Se l&#39;intestazione `x-sandbox-name` non è specificata, le richieste vengono risolte nella sandbox `prod`.

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

* `Content-Type: application/json`

## Eliminare un flusso di dati di destinazione {#delete-destination-dataflow}

Con un ID di flusso esistente, puoi eliminare un flusso di dati di destinazione eseguendo una richiesta DELETE all&#39;API [!DNL Flow Service].

**Formato API**

```http
DELETE /flows/{FLOW_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{FLOW_ID}` | Valore `id` univoco per il flusso di dati di destinazione da eliminare. |

**Richiesta**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/flows/455fa81b-f290-4222-94b6-540a73e3fbc2' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 202 (nessun contenuto) e un corpo vuoto. Puoi confermare l’eliminazione tentando una richiesta di ricerca (GET) nel flusso di dati. L’API restituirà un errore HTTP 404 (Non trovato), che indica che il flusso di dati è stato eliminato.

## Gestione degli errori API {#api-error-handling}

Gli endpoint API in questa esercitazione seguono i principi generali dei messaggi di errore API di Experience Platform. Per ulteriori informazioni sull&#39;interpretazione delle risposte di errore, consultare [codici di stato API](/help/landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](/help/landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione, hai usato correttamente l&#39;API [!DNL Flow Service] per eliminare un flusso di dati esistente in una destinazione.

Per i passaggi su come eseguire queste operazioni utilizzando l&#39;interfaccia utente, fare riferimento al tutorial su [eliminazione dei flussi di dati nell&#39;interfaccia utente](../ui/delete-destinations.md).

Ora puoi continuare ed eliminare [gli account di destinazione](/help/destinations/api/delete-destination-account.md) utilizzando l&#39;API [!DNL Flow Service].
