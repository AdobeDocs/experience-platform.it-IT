---
description: Utilizza le configurazioni di autenticazione supportate in Adobe Experience Platform Destination SDK per autenticare gli utenti e attivare i dati nell’endpoint di destinazione.
title: Configurazione dell’autenticazione
exl-id: 33eaab24-f867-4744-b424-4ba71727373c
source-git-commit: 9b4c7da5aa02ae27608c2841b1d825445ac3015e
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Configurazione dell’autenticazione {#credentials}

## Tipi di autenticazione supportati {#supported-authentication-types}

La configurazione di autenticazione selezionata determina il modo in cui Experience Platform si autentica nella destinazione, nell’interfaccia utente di Platform.

Adobe Experience Platform Destination SDK supporta diversi tipi di autenticazione:

* [Autenticazione portatore](#bearer)
* [[!DNL Amazon S3] autenticazione](#s3)
* [[!DNL Azure Blob] Storage](#blob)
* [[!DNL Azure Data Lake Storage]](#adls)
* [[!DNL Google Cloud Storage]](#gcs)
* [SFTP con chiave SSH](#sftp-ssh)
* [SFTP con password](#sftp-password)
* [OAuth 2 con codice di autorizzazione](#oauth2)
* [OUAth 2 con password](#oauth2)
* [Assegnazione di credenziali client a OAuth 2](#oauth2)

Puoi configurare le informazioni di autenticazione per la tua destinazione tramite `customerAuthenticationConfigurations` dei parametri `/destinations` punto finale.

Per informazioni dettagliate sulla configurazione dell&#39;autenticazione per ciascun tipo di destinazione, fare riferimento alle sezioni seguenti:

* [Configurazioni di autenticazione per le destinazioni di streaming](destination-configuration.md#customer-authentication-configurations)
* [Configurazioni di autenticazione per destinazioni basate su file](file-based-destination-configuration.md#customer-authentication-configurations)

## Autenticazione portatore {#bearer}

Ad Experience Platform, l’autenticazione al portatore è supportata per le destinazioni di streaming.

Per impostare l’autenticazione del tipo di portatore per la destinazione, configura la `customerAuthenticationConfigurations` nel `/destinations` punto finale come mostrato di seguito:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BEARER"
   }
]
```

## [!DNL Amazon S3] autenticazione {#s3}

[!DNL Amazon S3] l’autenticazione è supportata, ad Experience Platform, per le destinazioni basate su file.

Configurazione [!DNL Amazon S3] autenticazione per la destinazione, configura `customerAuthenticationConfigurations` nel `/destinations` punto finale come mostrato di seguito:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"S3"
   }
]
```

## [!DNL Azure Blob Storage] {#blob}

[!DNL Azure Blob Storage] l’autenticazione è supportata, ad Experience Platform, per le destinazioni basate su file.

Configurazione [!DNL Azure Blob] autenticazione per la destinazione, configura `customerAuthenticationConfigurations` nel `/destinations` punto finale come mostrato di seguito:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_CONNECTION_STRING"
   }
]
```

## [!DNL Azure Data Lake Storage] {#adls}

[!DNL Azure Data Lake Storage] l’autenticazione è supportata, ad Experience Platform, per le destinazioni basate su file.

Configurazione [!DNL Azure Data Lake Storage] (ADLS) autenticazione per la destinazione, configura il `customerAuthenticationConfigurations` nel `/destinations` punto finale come mostrato di seguito:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_SERVICE_PRINCIPAL"
   }
]
```

## [!DNL Google Cloud Storage] {#gcs}

[!DNL Google Cloud Storage] l’autenticazione è supportata, ad Experience Platform, per le destinazioni basate su file.

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"GOOGLE_CLOUD_STORAGE"
   }
]
```


## [!DNL SFTP] autenticazione con [!DNL SSH] key {#sftp-ssh}

[!DNL SFTP] autenticazione con [!DNL SSH] key è supportato per le destinazioni basate su file in Experience Platform.

Per impostare l’autenticazione SFTP con la chiave SSH per la destinazione, configura la `customerAuthenticationConfigurations` nel `/destinations` punto finale come mostrato di seguito:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_SSH_KEY"
   }
]
```

## [!DNL SFTP] autenticazione con password {#sftp-password}

[!DNL SFTP] l’autenticazione con password è supportata, ad Experience Platform, per le destinazioni basate su file.

Per impostare l’autenticazione SFTP con password per la destinazione, configura la `customerAuthenticationConfigurations` nel `/destinations` punto finale come mostrato di seguito:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_PASSWORD"
   }
]
```

## [!DNL OAuth 2] autenticazione {#oauth2}

[!DNL OAuth 2] l’autenticazione è supportata per le destinazioni di streaming in Experience Platform.

Per informazioni su come impostare i vari [!DNL OAuth 2] flussi, nonché per [!DNL OAuth 2] supporto, leggi la documentazione Destination SDK su [[!DNL OAuth 2] autenticazione](./oauth2-authentication.md).


## Quando utilizzare il `/credentials` Endpoint API {#when-to-use}

>[!IMPORTANT]
>
>Nella maggior parte dei casi, *non* devono utilizzare `/credentials` Endpoint API. È invece possibile configurare le informazioni di autenticazione per la destinazione tramite la `customerAuthenticationConfigurations` dei parametri `/destinations` punto finale.

La `/credentials` L’endpoint API viene fornito agli sviluppatori di destinazione nei casi in cui è presente un sistema di autenticazione globale tra Adobe e la destinazione e [!DNL Platform] I clienti non devono fornire credenziali di autenticazione per connettersi alla destinazione.

In questo caso, è necessario creare un oggetto credenziali utilizzando il `/credentials` Endpoint API. È inoltre necessario selezionare `PLATFORM_AUTHENTICATION` in [configurazione di destinazione](./destination-configuration.md#destination-delivery). Leggi [Operazioni endpoint API per le credenziali](./credentials-configuration-api.md) per un elenco completo delle operazioni eseguibili nella `/credentials` punto finale.
