---
description: Questa pagina esemplifica la chiamata API utilizzata per eliminare un Adobe Experience Platform Destination SDK di configurazione delle credenziali.
title: Eliminare una configurazione delle credenziali
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 2%

---


# Eliminare una configurazione delle credenziali

>[!IMPORTANT]
>
>**Endpoint API**: `platform.adobe.io/data/core/activation/authoring/credentials`

Questa pagina esemplifica la richiesta API e il payload che puoi utilizzare per eliminare una configurazione delle credenziali utilizzando `/authoring/credentials` Endpoint API.

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

## Eliminare una configurazione delle credenziali {#delete}

È possibile eliminare un [esistente](create-credential-configuration.md) configurazione delle credenziali effettuando una `DELETE` richiesta al `/authoring/credentials` punto finale con `{INSTANCE_ID}`della configurazione delle credenziali da eliminare.

Per ottenere una configurazione di destinazione esistente e i relativi `{INSTANCE_ID}`, consulta l’articolo [recupero di una configurazione delle credenziali](retrieve-credential-configuration.md).

**Formato API**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{INSTANCE_ID}` | La `ID` della configurazione delle credenziali da eliminare. |

La seguente richiesta elimina una configurazione delle credenziali definita dal `{INSTANCE_ID}` parametro .

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

Una risposta corretta restituisce lo stato HTTP 200 insieme a una risposta HTTP vuota.

+++

## Gestione degli errori API {#error-handling}

Gli endpoint API di Destination SDK seguono i principi generali dei messaggi di errore API di Experience Platform. Fai riferimento a [Codici di stato API](../../../landing/troubleshooting.md#api-status-codes) e [errori di intestazione della richiesta](../../../landing/troubleshooting.md#request-header-errors) nella guida alla risoluzione dei problemi di Platform.

## Passaggi successivi {#next-steps}

Dopo aver letto questo documento, ora sai come eliminare una configurazione delle credenziali utilizzando `/authoring/credentials` Endpoint API. Leggi [come utilizzare Destination SDK per configurare la destinazione](../guides/configure-destination-instructions.md) per capire dove si adatta questo passaggio al processo di configurazione della destinazione.
