---
keywords: Experience Platform;home;argomenti popolari;Google PubSub;google pubsub
solution: Experience Platform
title: Creare una connessione Google PubSub Source utilizzando l’API del servizio di flusso
topic: ' - Panoramica'
type: Tutorial
description: Scopri come collegare Adobe Experience Platform a un account Google PubSub utilizzando l’API del servizio di flusso.
translation-type: tm+mt
source-git-commit: b5358ce206888c413035b46fe751520fd9aefb14
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 2%

---


# Creare una connessione sorgente [!DNL Google PubSub] utilizzando l’API del servizio di flusso

>[!NOTE]
>
>Il connettore [!DNL Google PubSub] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la [Panoramica delle sorgenti](../../../../home.md#terms-and-conditions) .

Questa esercitazione utilizza l’ [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) per guidarti nei passaggi per la connessione di [!DNL Google PubSub] (in seguito denominata &quot;[!DNL PubSub]&quot;) a Adobe Experience Platform.

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): L’Experience Platform consente di acquisire dati da varie sorgenti e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per creare correttamente una connessione sorgente [!DNL PubSub] utilizzando l&#39;API [!DNL Flow Service].

### Raccogli credenziali richieste

Affinché [!DNL Flow Service] possa connettersi a [!DNL PubSub], è necessario fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `projectId` | L&#39;ID del progetto necessario per l&#39;autenticazione [!DNL PubSub]. |
| `credentials` | Credenziale o chiave necessaria per l&#39;autenticazione [!DNL PubSub]. |

Per ulteriori informazioni su questi valori, consulta il seguente documento [PubSub authentication](https://cloud.google.com/pubsub/docs/authentication) . Se utilizzi l&#39;autenticazione basata sull&#39;account del servizio, consulta la seguente [Guida PubSub](https://cloud.google.com/docs/authentication/production#create_service_account) per i passaggi su come generare le credenziali.

>[!TIP]
>
>Se utilizzi l’autenticazione basata sull’account del servizio, assicurati di aver concesso un accesso utente sufficiente all’account del servizio e che non vi siano spazi bianchi aggiuntivi nel JSON durante la copia e l’incolla delle credenziali.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di Experience Platform.

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate alle API di Platform, devi prima completare l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in Experience Platform, incluse quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API di Platform richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

* `Content-Type: application/json`

## Creare una connessione

Una connessione specifica un&#39;origine e contiene le credenziali per tale origine. È necessaria una sola connessione per ogni account [!DNL PubSub] in quanto può essere utilizzata per creare più flussi di dati per inserire dati diversi.

**Formato API**

```http
POST /connections
```

**Richiesta**

Per creare una connessione [!DNL PubSub], è necessario fornire l’ID del provider e l’ID della specifica di connessione come parte della richiesta di POST. L&#39;ID provider è `521eee4d-8cbe-4906-bb48-fb6bd4450033` e l&#39;ID della specifica di connessione è `70116022-a743-464a-bbfe-e226a7f8210c`.

**Formato API**

```http
POST /connections
```

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google PubSub connection",
        "description": "Google PubSub connection",
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
        "auth": {
            "specName": "Google PubSub authentication credentials",
            "params": {
                "projectId": "{PROJECT_ID}",
                "credentials": "{CREDENTIALS}"
            }
        },
        "connectionSpec": {
            "id": "70116022-a743-464a-bbfe-e226a7f8210c",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.projectId` | L&#39;ID del progetto necessario per l&#39;autenticazione [!DNL PubSub]. |
| `auth.params.credentials` | Credenziale o chiave necessaria per l&#39;autenticazione [!DNL PubSub]. |
| `connectionSpec.id` | ID delle specifiche di connessione [!DNL PubSub]: `70116022-a743-464a-bbfe-e226a7f8210c`. |

**Risposta**

Una risposta corretta restituisce l&#39;ID di connessione della nuova connessione [!DNL PubSub] creata. Questo ID è necessario per esplorare i dati di archiviazione cloud nell’esercitazione successiva.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione [!DNL PubSub] utilizzando l&#39;API [!DNL Flow Service] e acquisito il relativo ID di connessione univoco. Puoi usare questo ID connessione per [raccogliere dati in streaming utilizzando l&#39;API del servizio di flusso](../../collect/streaming.md).
