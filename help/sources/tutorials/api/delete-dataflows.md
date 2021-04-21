---
keywords: Experience Platform;home;argomenti popolari;servizio di flusso;API;api;elimina;elimina flussi di dati
solution: Experience Platform
title: Eliminare un flusso di dati utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come eliminare i flussi di dati in batch e in streaming utilizzando l’API del servizio di flusso.
exl-id: ea9040b1-3a40-493d-86f0-27deef09df07
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 1%

---

# Eliminare un flusso di dati utilizzando l’API del servizio di flusso

Puoi eliminare i flussi di dati in batch e in streaming che contengono errori o che sono diventati obsoleti utilizzando l&#39; [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

Questa esercitazione descrive i passaggi per eliminare i flussi di dati creati con origini in batch e in streaming utilizzando [!DNL Flow Service].

## Introduzione

Questa esercitazione richiede un ID di flusso valido. Se non disponi di un ID di flusso valido, seleziona il connettore desiderato dalla [panoramica origini](../../home.md) e segui i passaggi descritti prima di provare questa esercitazione.

Questa esercitazione richiede anche di avere una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../home.md):  [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite  [!DNL Platform] i servizi.
* [Sandbox](../../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che dovrai conoscere per eliminare correttamente un flusso di dati utilizzando l’ [!DNL Flow Service] API .

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform] .

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate alle API [!DNL Platform], devi prima completare l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], comprese quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API [!DNL Platform] richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

* `Content-Type: application/json`

## Eliminare un flusso di dati

Con un ID flusso esistente, puoi eliminare un flusso di dati eseguendo una richiesta DELETE all’ API [!DNL Flow Service] .

**Formato API**

```http
DELETE /flows/{FLOW_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{FLOW_ID}` | Il valore univoco `id` per il flusso di dati da eliminare. |

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

Una risposta corretta restituisce lo stato HTTP 204 (Nessun contenuto) e un corpo vuoto. Puoi confermare l’eliminazione tentando una richiesta di ricerca (GET) al flusso di dati. L’API restituirà un errore HTTP 404 (Non trovato) che indica che il flusso di dati è stato eliminato.

## Passaggi successivi

Seguendo questa esercitazione, hai utilizzato correttamente l’ API [!DNL Flow Service] per eliminare un flusso di dati esistente.

Per i passaggi su come eseguire queste operazioni utilizzando l&#39;interfaccia utente, fai riferimento all&#39;esercitazione su [eliminazione dei flussi di dati nell&#39;interfaccia utente](../../tutorials/ui/delete.md)
