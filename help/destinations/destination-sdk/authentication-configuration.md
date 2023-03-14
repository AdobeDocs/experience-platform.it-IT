---
description: Utilizza le configurazioni di autenticazione supportate in Adobe Experience Platform Destination SDK per autenticare gli utenti e attivare i dati nell’endpoint di destinazione.
title: Configurazione dell’autenticazione
exl-id: 33eaab24-f867-4744-b424-4ba71727373c
source-git-commit: 59ac7749d788d8527da3578ec140248f7acf8e98
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# Configurazione dell’autenticazione {#credentials}

## Tipi di autenticazione supportati {#supported-authentication-types}

La configurazione di autenticazione selezionata determina il modo in cui Experience Platform si autentica nella destinazione, nell’interfaccia utente di Platform.

Adobe Experience Platform Destination SDK supporta diversi tipi di autenticazione:

* [Autenticazione Bearer](#bearer)
* [Autenticazione di base](#basic)
* [[!DNL Amazon S3] autenticazione](#s3)
* [[!DNL Azure Blob] Archiviazione](#blob)
* [[!DNL Azure Data Lake Storage]](#adls)
* [[!DNL Google Cloud Storage]](#gcs)
* [SFTP con chiave SSH](#sftp-ssh)
* [SFTP con password](#sftp-password)
* [OAuth 2 con codice di autorizzazione](#oauth2)
* [OAUth 2 con concessione password](#oauth2)
* [OAuth 2 con concessione di credenziali client](#oauth2)

È possibile configurare le informazioni di autenticazione per la destinazione tramite `customerAuthenticationConfigurations` parametri di `/destinations` endpoint.

Per informazioni dettagliate sulla configurazione dell’autenticazione per ciascun tipo di destinazione, consulta le sezioni seguenti:

* [Configurazioni di autenticazione per le destinazioni di streaming](destination-configuration.md#customer-authentication-configurations)
* [Configurazioni di autenticazione per destinazioni basate su file](file-based-destination-configuration.md#customer-authentication-configurations)

## Autenticazione di base {#basic}

L’autenticazione di base è supportata per le destinazioni di streaming in Experience Platform.

Quando si configura il tipo di autenticazione di base, gli utenti devono immettere un nome utente e una password per connettersi alla destinazione.

Per impostare l’autenticazione di base per la destinazione, configura `customerAuthenticationConfigurations` sezione tramite `/destinations` endpoint come mostrato di seguito:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BASIC"
   }
]
```

## Autenticazione Bearer {#bearer}

L’autenticazione Bearer è supportata per le destinazioni di streaming in Experience Platform.

Per impostare l&#39;autenticazione di tipo Bearer per la destinazione, configurare `customerAuthenticationConfigurations` parametro in `/destinations` endpoint come mostrato di seguito:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BEARER"
   }
]
```

## [!DNL Amazon S3] autenticazione {#s3}

[!DNL Amazon S3] l’autenticazione è supportata per le destinazioni basate su file in Experience Platform.

Per impostare [!DNL Amazon S3] per la destinazione, configura il `customerAuthenticationConfigurations` parametro in `/destinations` endpoint come mostrato di seguito:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"S3"
   }
]
```

## [!DNL Azure Blob Storage] {#blob}

[!DNL Azure Blob Storage] l’autenticazione è supportata per le destinazioni basate su file in Experience Platform.

Per impostare [!DNL Azure Blob] per la destinazione, configura il `customerAuthenticationConfigurations` parametro in `/destinations` endpoint come mostrato di seguito:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_CONNECTION_STRING"
   }
]
```

## [!DNL Azure Data Lake Storage] {#adls}

[!DNL Azure Data Lake Storage] l’autenticazione è supportata per le destinazioni basate su file in Experience Platform.

Per impostare [!DNL Azure Data Lake Storage] (ADLS) per la destinazione, configura il `customerAuthenticationConfigurations` parametro in `/destinations` endpoint come mostrato di seguito:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_SERVICE_PRINCIPAL"
   }
]
```

## [!DNL Google Cloud Storage] {#gcs}

[!DNL Google Cloud Storage] l’autenticazione è supportata per le destinazioni basate su file in Experience Platform.

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"GOOGLE_CLOUD_STORAGE"
   }
]
```


## [!DNL SFTP] autenticazione con [!DNL SSH] chiave {#sftp-ssh}

[!DNL SFTP] autenticazione con [!DNL SSH] La chiave è supportata per le destinazioni basate su file in Experience Platform.

Per impostare l’autenticazione SFTP con chiave SSH per la destinazione, configura la `customerAuthenticationConfigurations` parametro in `/destinations` endpoint come mostrato di seguito:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_SSH_KEY"
   }
]
```

## [!DNL SFTP] autenticazione con password {#sftp-password}

[!DNL SFTP] l’autenticazione con password è supportata per le destinazioni basate su file in Experience Platform.

Per impostare l’autenticazione SFTP con password per la destinazione, configura la `customerAuthenticationConfigurations` parametro in `/destinations` endpoint come mostrato di seguito:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_PASSWORD"
   }
]
```

## [!DNL OAuth 2] autenticazione {#oauth2}

[!DNL OAuth 2] l’autenticazione è supportata per le destinazioni di streaming in Experience Platform.

Per informazioni su come impostare i vari [!DNL OAuth 2] flussi, nonché per [!DNL OAuth 2] , leggi la documentazione Destination SDK su [[!DNL OAuth 2] autenticazione](./oauth2-authentication.md).


## Quando utilizzare il `/credentials` Endpoint API {#when-to-use}

>[!IMPORTANT]
>
>Nella maggior parte dei casi, *non* devono utilizzare `/credentials` Endpoint API È invece possibile configurare le informazioni di autenticazione per la destinazione tramite `customerAuthenticationConfigurations` parametri di `/destinations` endpoint.

Il `/credentials` L’endpoint API viene fornito agli sviluppatori di destinazione nei casi in cui è presente un sistema di autenticazione globale tra Adobe e la destinazione e [!DNL Platform] I clienti non devono fornire credenziali di autenticazione per connettersi alla destinazione.

In questo caso, è necessario creare un oggetto credenziali utilizzando `/credentials` Endpoint API Devi anche selezionare `PLATFORM_AUTHENTICATION` nel [configurazione di destinazione](./destination-configuration.md#destination-delivery). Letto [Operazioni dell’endpoint API delle credenziali](./credentials-configuration-api.md) per un elenco completo delle operazioni che è possibile eseguire `/credentials` endpoint.
