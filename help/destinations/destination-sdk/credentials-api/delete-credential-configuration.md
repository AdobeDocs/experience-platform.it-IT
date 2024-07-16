---
description: Questa pagina esemplifica la chiamata API utilizzata per eliminare un Adobe Experience Platform Destination SDK di configurazione delle credenziali.
title: Eliminare una configurazione di credenziali
exl-id: a540e349-043c-4f04-8ca8-f650b9943492
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 1%

---

# Eliminare una configurazione di credenziali

>[!IMPORTANT]
>
>**Endpoint API**: `platform.adobe.io/data/core/activation/authoring/credentials`

Questa pagina illustra la richiesta API e il payload che è possibile utilizzare per eliminare una configurazione di credenziali utilizzando l&#39;endpoint API `/authoring/credentials`.

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

## Eliminare una configurazione di credenziali {#delete}

È possibile eliminare una configurazione di credenziali [esistente](create-credential-configuration.md) effettuando una richiesta `DELETE` all&#39;endpoint `/authoring/credentials` con `{INSTANCE_ID}` della configurazione di credenziali che si desidera eliminare.

Per ottenere una configurazione di destinazione esistente e i corrispondenti `{INSTANCE_ID}`, vedere l&#39;articolo relativo al [recupero di una configurazione delle credenziali](retrieve-credential-configuration.md).

**Formato API**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{INSTANCE_ID}` | `ID` della configurazione delle credenziali da eliminare. |

La richiesta seguente elimina una configurazione di credenziali definita dal parametro `{INSTANCE_ID}`.

+++Richiesta

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Risposta

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 insieme a una risposta HTTP vuota.

+++

## Gestione degli errori API {#error-handling}

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Consulta [Codici di stato API](../../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi {#next-steps}

Dopo aver letto questo documento, ora sai come eliminare una configurazione di credenziali utilizzando l&#39;endpoint API `/authoring/credentials`. Leggi [come utilizzare Destination SDK per configurare la destinazione](../guides/configure-destination-instructions.md) per capire in che modo questo passaggio si inserisce nel processo di configurazione della destinazione.
