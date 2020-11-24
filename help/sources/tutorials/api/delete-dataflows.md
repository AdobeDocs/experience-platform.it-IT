---
keywords: Experience Platform;home;popular topics;flow service;API;api;delete;delete dataflows
solution: Experience Platform
title: Eliminare un flusso di dati utilizzando l'API del servizio di flusso
topic: overview
type: Tutorial
description: Questa esercitazione descrive i passaggi per eliminare un flusso di dati utilizzando l'API del servizio di flusso.
translation-type: tm+mt
source-git-commit: ae3e64a5f9a82c0efe3cffeb6d4d425ae2e72bda
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 1%

---


# Eliminare un flusso di dati utilizzando l&#39;API del servizio di flusso

Questa esercitazione descrive i passaggi per eliminare i flussi di dati creati con origini batch e in streaming mediante l&#39; [[!DNL Flow Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Introduzione

Questa esercitazione richiede un ID flusso valido. Se non disponi di un ID flusso valido, seleziona il connettore desiderato dalla panoramica [delle](../../home.md) origini ed esegui i passaggi descritti prima di eseguire l&#39;esercitazione.

Questa esercitazione richiede inoltre di conoscere i seguenti componenti di Adobe Experience Platform:

* [Origini](../../home.md): [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] i servizi.
* [Sandbox](../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per eliminare correttamente un flusso di dati utilizzando l&#39; [!DNL Flow Service] API.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere chiamate](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla [!DNL Experience Platform] risoluzione dei problemi.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è prima necessario completare l&#39;esercitazione [sull&#39;](../../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate [!DNL Experience Platform] API, come illustrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], comprese quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva per il tipo di supporto:

* `Content-Type: application/json`

## Eliminare un flusso di dati

Con un ID flusso esistente, potete eliminare un flusso di dati eseguendo una richiesta di DELETE all&#39; [!DNL Flow Service] API.

**Formato API**

```http
DELETE /flows/{FLOW_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{FLOW_ID}` | Il `id` valore univoco del flusso di dati da eliminare. |

**Richiesta**

```shell
curl -X DELETE \
    'https://platform-int.adobe.io/data/foundation/flowservice/flows/20c115bc-46e3-40f3-bfe9-fb25abe4ba76' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 204 (Nessun contenuto) e un corpo vuoto. È possibile confermare l&#39;eliminazione provando una richiesta di ricerca (GET) al flusso di dati. L&#39;API restituirà un errore HTTP 404 (non trovato), a indicare che il flusso di dati è stato eliminato.

## Passaggi successivi

Seguendo questa esercitazione, l&#39; [!DNL Flow Service] API è stata utilizzata correttamente per eliminare un flusso di dati esistente.

Per informazioni su come eseguire queste operazioni utilizzando l&#39;interfaccia utente, fare riferimento all&#39;esercitazione sull&#39; [eliminazione dei flussi di dati nell&#39;interfaccia utente](../../tutorials/ui/delete.md)
