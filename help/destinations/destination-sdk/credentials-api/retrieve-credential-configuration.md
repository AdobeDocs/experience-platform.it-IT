---
description: Questa pagina esemplifica la chiamata API utilizzata per recuperare una configurazione di credenziali tramite il Adobe Experience Platform Destination SDK.
title: Recuperare una configurazione di credenziali
exl-id: cec55073-6e2f-4412-a9dd-1aeb445279c0
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---

# Recuperare una configurazione di credenziali

>[!IMPORTANT]
>
>**Endpoint API**: `platform.adobe.io/data/core/activation/authoring/credentials`

Questa pagina illustra la richiesta API e il payload che è possibile utilizzare per recuperare una configurazione di credenziali utilizzando l&#39;endpoint API `/authoring/credentials`.

## Quando utilizzare l&#39;endpoint API `/credentials` {#when-to-use}

>[!IMPORTANT]
>
>Nella maggior parte dei casi, ***non*** deve utilizzare l&#39;endpoint API `/credentials`. È invece possibile configurare le informazioni di autenticazione per la destinazione tramite i parametri `customerAuthenticationConfigurations` dell&#39;endpoint `/destinations`.
> 
>Leggi [Configurazione autenticazione cliente](../functionality/destination-configuration/customer-authentication.md) per informazioni dettagliate sui tipi di autenticazione supportati.

Utilizzare questo endpoint API per creare una configurazione di credenziali solo se è presente un sistema di autenticazione globale tra Adobe e la piattaforma di destinazione e il cliente [!DNL Platform] non deve fornire credenziali di autenticazione per connettersi alla destinazione. In questo caso, è necessario creare una configurazione delle credenziali utilizzando l&#39;endpoint API `/credentials`.

Quando si utilizza un sistema di autenticazione globale, è necessario impostare `"authenticationRule":"PLATFORM_AUTHENTICATION"` nella configurazione [consegna di destinazione](../functionality/destination-configuration/destination-delivery.md), durante la [creazione di una nuova configurazione di destinazione](../authoring-api/destination-configuration/create-destination-configuration.md).

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **con distinzione tra maiuscole e minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Guida introduttiva alle operazioni API per le credenziali {#get-started}

Prima di continuare, consulta la [guida introduttiva](../getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente chiamate all&#39;API, tra cui come ottenere l&#39;autorizzazione di authoring della destinazione richiesta e le intestazioni richieste.

## Recuperare una configurazione di credenziali {#retrieve}

È possibile recuperare una configurazione delle credenziali [existing](create-credential-configuration.md) effettuando una richiesta `GET` all&#39;endpoint `/authoring/credentials`.

**Formato API**

Utilizza il seguente formato API per recuperare tutte le configurazioni di credenziali per il tuo account.

```http
GET /authoring/credentials
```

Utilizzare il seguente formato API per recuperare una configurazione di credenziali specifica, definita dal parametro `{INSTANCE_ID}`.

```http
GET /authoring/credentials/{INSTANCE_ID}
```

Le due richieste seguenti recuperano tutte le configurazioni di credenziali per l’organizzazione IMS o una configurazione di credenziali specifica, a seconda che si trasmetta o meno il parametro `INSTANCE_ID` nella richiesta.

Seleziona ciascuna scheda di seguito per visualizzare il payload corrispondente.

>[!BEGINTABS]

>[!TAB Recupera tutte le configurazioni di credenziali]

+++Richiesta

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Risposta

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con un elenco di configurazioni di credenziali a cui hai accesso, in base a [!DNL IMS Org ID] e al nome della sandbox utilizzato. Un `instanceId` corrisponde a una configurazione di credenziali.

```json
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"s3Authentication",
   "name":"yourdestination",
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   }
},
{
   "instanceId":"a25bffa0-3127-4030-895d-1d1236bb3680",
   "createdDate":"2022-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2022-08-07T06:41:48.641943Z",
   "type":"basic",
   "name":"yourdestination",
   "s3Authentication":{
      "url":"string",
      "username":"string",
      "password":"string"
   }
}
```

+++

>[!TAB Recuperare una configurazione di credenziali specifica]

+++Richiesta

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{INSTANCE_ID}` | ID della configurazione delle credenziali da recuperare. |

+++

+++Risposta

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della configurazione delle credenziali corrispondenti al `instanceId` fornito nella richiesta.

```json
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"s3Authentication",
   "name":"yourdestination",
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   }
}
```

+++

>[!ENDTABS]

## Gestione degli errori API {#error-handling}

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Consulta [Codici di stato API](../../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi {#next-steps}

Dopo aver letto questo documento, saprai come recuperare i dettagli sulle configurazioni delle credenziali utilizzando l&#39;endpoint API `/authoring/credentials`. Leggi [come utilizzare Destination SDK per configurare la destinazione](../guides/configure-destination-instructions.md) per capire in che modo questo passaggio si inserisce nel processo di configurazione della destinazione.
