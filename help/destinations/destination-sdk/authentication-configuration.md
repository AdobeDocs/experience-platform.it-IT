---
description: Utilizza le configurazioni di autenticazione supportate nell’SDK di destinazione di Adobe Experience Platform per autenticare gli utenti e attivare i dati nell’endpoint di destinazione.
title: Configurazione dell’autenticazione
exl-id: 33eaab24-f867-4744-b424-4ba71727373c
source-git-commit: e6d922800c17312df8529061c56d8a2deac46662
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# Configurazione dell’autenticazione {#credentials}

## Tipi di autenticazione supportati {#supported-authentication-types}

L’SDK di destinazione di Adobe Experience Platform supporta diversi tipi di autenticazione:

* Autenticazione portatore
* OAuth 2 con codice di autorizzazione
* OUAth 2 con password
* Assegnazione di credenziali client a OAuth 2

Puoi configurare le informazioni di autenticazione per la tua destinazione tramite `customerAuthenticationConfigurations` dei parametri `/destinations` punto finale. Fai riferimento a [sezione sulle configurazioni di autenticazione dei clienti](./destination-configuration.md#customer-authentication-configurations) nell&#39;articolo sulla configurazione di destinazione e nelle sezioni seguenti per informazioni specifiche sulle configurazioni per ciascun tipo di autenticazione.

## Autenticazione portatore {#bearer}

Per configurare l’autenticazione del tipo di portatore per le destinazioni, è sufficiente configurare il `customerAuthenticationConfigurations` nel `/destinations` punto finale come mostrato di seguito:

```json
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ]
```

## Autenticazione OAuth 2 {#oauth2}

Per informazioni su come impostare i vari flussi OAuth 2 supportati e per il supporto personalizzato OAuth 2, consulta la documentazione dell’SDK di destinazione in [Autenticazione OAuth 2](./oauth2-authentication.md).


## Quando utilizzare il `/credentials` Endpoint API {#when-to-use}

>[!IMPORTANT]
>
>Nella maggior parte dei casi, *non* devono utilizzare `/credentials` Endpoint API. È invece possibile configurare le informazioni di autenticazione per la destinazione tramite la `customerAuthenticationConfigurations` dei parametri `/destinations` punto finale.

La `/credentials` L’endpoint API viene fornito agli sviluppatori di destinazione nei casi in cui è presente un sistema di autenticazione globale tra Adobe e la destinazione e [!DNL Platform] I clienti non devono fornire credenziali di autenticazione per connettersi alla destinazione.

In questo caso, è necessario creare un oggetto credenziali utilizzando il `/credentials` Endpoint API. È inoltre necessario selezionare `PLATFORM_AUTHENTICATION` in [configurazione di destinazione](./destination-configuration.md#destination-delivery). Leggi [Operazioni endpoint API per le credenziali](./credentials-configuration-api.md) per un elenco completo delle operazioni eseguibili nella `/credentials` punto finale.
