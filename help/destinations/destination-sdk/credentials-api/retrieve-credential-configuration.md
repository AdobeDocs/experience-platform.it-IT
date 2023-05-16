---
description: Questa pagina esemplifica la chiamata API utilizzata per recuperare una configurazione delle credenziali tramite Adobe Experience Platform Destination SDK.
title: Recuperare una configurazione delle credenziali
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 2%

---


# Recuperare una configurazione delle credenziali

>[!IMPORTANT]
>
>**Endpoint API**: `platform.adobe.io/data/core/activation/authoring/credentials`

Questa pagina esemplifica la richiesta API e il payload che puoi utilizzare per recuperare una configurazione delle credenziali utilizzando `/authoring/credentials` Endpoint API.

## Quando utilizzare il `/credentials` Endpoint API {#when-to-use}

>[!IMPORTANT]
>
>Nella maggior parte dei casi, ***non*** devono utilizzare `/credentials` Endpoint API. È invece possibile configurare le informazioni di autenticazione per la destinazione tramite la `customerAuthenticationConfigurations` dei parametri `/destinations` punto finale.
> 
>Leggi [Configurazione dell’autenticazione cliente](../functionality/destination-configuration/customer-authentication.md) per informazioni dettagliate sui tipi di autenticazione supportati.

Utilizza questo endpoint API per creare una configurazione delle credenziali solo se è presente un sistema di autenticazione globale tra Adobe e la piattaforma di destinazione e [!DNL Platform] il cliente non deve fornire credenziali di autenticazione per connettersi alla destinazione. In questo caso, devi creare una configurazione delle credenziali utilizzando `/credentials` Endpoint API.

Quando utilizzi un sistema di autenticazione globale, devi impostare `"authenticationRule":"PLATFORM_AUTHENTICATION"` in [consegna a destinazione](../functionality/destination-configuration/destination-delivery.md) configurazione, quando [creazione di una nuova configurazione di destinazione](../authoring-api/destination-configuration/create-destination-configuration.md).

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **distinzione tra maiuscole e minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Guida introduttiva alle operazioni API con le credenziali {#get-started}

Prima di continuare, controlla la [guida introduttiva](../getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente le chiamate all’API, tra cui come ottenere l’autorizzazione di authoring di destinazione richiesta e le intestazioni richieste.

## Recuperare una configurazione delle credenziali {#retrieve}

Puoi recuperare un [esistente](create-credential-configuration.md) configurazione delle credenziali effettuando una `GET` richiesta al `/authoring/credentials` punto finale.

**Formato API**

Utilizza il seguente formato API per recuperare tutte le configurazioni delle credenziali per il tuo account.

```http
GET /authoring/credentials
```

Utilizza il seguente formato API per recuperare una configurazione specifica delle credenziali, definita dalla `{INSTANCE_ID}` parametro .

```http
GET /authoring/credentials/{INSTANCE_ID}
```

Le due richieste seguenti recuperano tutte le configurazioni di credenziali per la tua organizzazione IMS o una configurazione di credenziali specifica, a seconda che tu passi o meno la `INSTANCE_ID` nella richiesta.

Seleziona ciascuna scheda qui sotto per visualizzare il payload corrispondente.

>[!BEGINTABS]

>[!TAB Recupera tutte le configurazioni delle credenziali]

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

Una risposta corretta restituisce lo stato HTTP 200 con un elenco di configurazioni di credenziali a cui hai accesso, in base al [!DNL IMS Org ID] e nome della sandbox utilizzata. Uno `instanceId` corrisponde a una configurazione delle credenziali.

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

>[!TAB Recupera una configurazione specifica delle credenziali]

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

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli della configurazione delle credenziali corrispondente al `instanceId` fornito su richiesta.

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

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](../../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi {#next-steps}

Dopo aver letto questo documento, ora sai come recuperare i dettagli sulle configurazioni delle credenziali utilizzando `/authoring/credentials` Endpoint API. Leggi [come utilizzare Destination SDK per configurare la destinazione](../guides/configure-destination-instructions.md) per capire dove si adatta questo passaggio al processo di configurazione della destinazione.
