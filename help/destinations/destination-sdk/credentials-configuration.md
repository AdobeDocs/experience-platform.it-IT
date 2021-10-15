---
description: Utilizza le configurazioni di autenticazione supportate nell’SDK di destinazione di Adobe Experience Platform per autenticare gli utenti e attivare i dati nell’endpoint di destinazione.
title: Configurazione dell’autenticazione
exl-id: 33eaab24-f867-4744-b424-4ba71727373c
source-git-commit: 485c1359f8ef5fef0c5aa324cd08de00b0b4bb2f
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# Configurazione dell’autenticazione {#credentials}

## Tipi di autenticazione supportati {#supported-authentication-types}

L’SDK di destinazione di Adobe Experience Platform supporta diversi tipi di autenticazione:

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
