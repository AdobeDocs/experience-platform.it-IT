---
description: Questa configurazione determina il modo in cui gli utenti Adobe Experience Platform si autenticano nell’endpoint di destinazione per attivare i dati.
title: Opzioni di configurazione per le credenziali nell’SDK di destinazione
source-git-commit: 11f6421665acc2041aa9483b1e0efb6fe48b6dfb
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# Configurazione dell’autenticazione {#credentials}

## Tipi di autenticazione supportati {#supported-authentication-types}

Adobe Experience Platform supporta diversi tipi di autenticazione:

* Autenticazione portatore
* OAuth 2 con codice di autorizzazione
* OUAth 2 con password
* Assegnazione di credenziali client a OAuth 2

Per i vari flussi OAuth 2 supportati e per il supporto personalizzato OAuth 2, consulta la documentazione SDK di destinazione sull’ [autenticazione OAuth 2](./oauth2-authentication.md).

Puoi configurare le informazioni di autenticazione per la destinazione tramite i parametri `customerAuthenticationConfigurations` dell’ endpoint `/destinations` . Fai riferimento alla sezione [configurazioni di autenticazione dei clienti](./destination-configuration.md#customer-authentication-configurations) nell&#39;articolo sulla configurazione di destinazione.

## Quando utilizzare l’endpoint API `/credentials` {#when-to-use}

>[!IMPORTANT]
>
>Nella maggior parte dei casi, *non* non è necessario utilizzare l’endpoint API `/credentials`. Puoi invece configurare le informazioni di autenticazione per la destinazione tramite i parametri `customerAuthenticationConfigurations` dell’ endpoint `/destinations` .

Utilizza l’ `activation/authoring/credentials` endpoint API e seleziona `PLATFORM_AUTHENTICATION` nella [configurazione di destinazione](./destination-configuration.md#destination-delivery) se è presente un sistema di autenticazione globale tra Adobe e la destinazione e il cliente [!DNL Platform] non deve fornire credenziali di autenticazione per connettersi alla destinazione. In questo caso è necessario creare un oggetto credenziali utilizzando l&#39;endpoint API `/credentials`. Leggi [Operazioni endpoint API delle credenziali](./credentials-configuration-api.md) per un elenco completo delle operazioni eseguibili sull&#39;endpoint `/credentials`.