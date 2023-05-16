---
description: Scopri come impostare un meccanismo di autenticazione per la tua destinazione e ottenere informazioni su ciò che gli utenti visualizzeranno nell’interfaccia utente a seconda del metodo di autenticazione selezionato.
title: Configurazione dell’autenticazione cliente
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '1094'
ht-degree: 0%

---


# Configurazione dell’autenticazione cliente

L&#39;Experience Platform offre una grande flessibilità nei protocolli di autenticazione disponibili per partner e clienti. Puoi configurare la destinazione per supportare qualsiasi metodo di autenticazione standard del settore, ad esempio [!DNL OAuth2], autenticazione del token portatore, autenticazione della password e molto altro.

Questa pagina spiega come impostare la destinazione utilizzando il metodo di autenticazione preferito. In base alla configurazione di autenticazione utilizzata al momento della creazione della destinazione, i clienti visualizzeranno diversi tipi di pagine di autenticazione quando si connettono alla destinazione nell’interfaccia utente di Experience Platform.

Per capire dove si trova questo componente in un’integrazione creata con Destination SDK, consulta il diagramma nella sezione [opzioni di configurazione](../configuration-options.md) documentazione o consulta le seguenti pagine di panoramica della configurazione di destinazione:

* [Utilizza Destination SDK per configurare una destinazione di streaming](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Utilizzare Destination SDK per configurare una destinazione basata su file](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

Per poter esportare i dati da Platform alla destinazione, i clienti devono creare una nuova connessione tra Experience Platform e la destinazione seguendo i passaggi descritti in [connessione di destinazione](../../../ui/connect-destination.md) esercitazione.

Quando [creazione di una destinazione](../../authoring-api/destination-configuration/create-destination-configuration.md) attraverso la Destination SDK, `customerAuthenticationConfigurations` definisce gli elementi visualizzati dai clienti nella sezione [schermata di autenticazione](../../../ui/connect-destination.md#authenticate). A seconda del tipo di autenticazione di destinazione, i clienti devono fornire vari dettagli di autenticazione, ad esempio:

* Per le destinazioni che utilizzano [autenticazione di base](#basic), gli utenti devono fornire un nome utente e una password direttamente nella pagina di autenticazione dell’interfaccia utente di Experience Platform.
* Per le destinazioni che utilizzano [autenticazione portatore](#bearer), gli utenti devono fornire un token portatore.
* Per le destinazioni che utilizzano [Autenticazione OAuth2](#oauth2), gli utenti vengono reindirizzati alla pagina di accesso della tua destinazione in cui possono accedere con le loro credenziali.
* Per [Amazon S3](#s3) destinazioni, gli utenti devono fornire le loro [!DNL Amazon S3] chiave di accesso e chiave segreta.
* Per [BLOB di Azure](#blob) destinazioni, gli utenti devono fornire le loro [!DNL Azure Blob] stringa di connessione.

Puoi configurare i dettagli di autenticazione dei clienti tramite `/authoring/destinations` punto finale. Per esempi dettagliati sulle chiamate API , consulta le pagine di riferimento API seguenti dove puoi configurare i componenti mostrati in questa pagina.

* [Creare una configurazione di destinazione](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Aggiornare una configurazione di destinazione](../../authoring-api/destination-configuration/update-destination-configuration.md)

Questo articolo descrive tutte le configurazioni di autenticazione dei clienti supportate che puoi utilizzare per la tua destinazione e mostra cosa vedranno i clienti nell&#39;interfaccia utente di Experience Platform in base al metodo di autenticazione impostato per la tua destinazione.

>[!IMPORTANT]
>
>La configurazione di autenticazione del cliente non richiede la configurazione di alcun parametro. Puoi copiare e incollare i snippet mostrati in questa pagina nelle chiamate API quando [creazione](../../authoring-api/destination-configuration/create-destination-configuration.md) o [aggiornamento](../../authoring-api/destination-configuration/update-destination-configuration.md) una configurazione di destinazione; gli utenti visualizzeranno la schermata di autenticazione corrispondente nell’interfaccia utente di Platform.

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **distinzione tra maiuscole e minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Tipi di integrazione supportati {#supported-integration-types}

Per informazioni dettagliate sui tipi di integrazioni che supportano le funzionalità descritte in questa pagina, consulta la tabella seguente.

| Tipo di integrazione | Supporta funzionalità |
|---|---|
| Integrazioni in tempo reale (streaming) | Sì |
| Integrazioni basate su file (batch) | Sì |

## Configurazione della regola di autenticazione {#authentication-rule}

Quando utilizzi una delle configurazioni di autenticazione del cliente descritte in questa pagina, imposta sempre la variabile `authenticationRule` in [consegna a destinazione](destination-delivery.md) a `"CUSTOMER_AUTHENTICATION"`, come illustrato di seguito.

```json {line-numbers="true" highlight="4"
{
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ]
}
```

## Autenticazione di base {#basic}

L’autenticazione di base è supportata per le integrazioni in tempo reale (streaming) in Experience Platform.

Quando configuri il tipo di autenticazione di base, gli utenti devono immettere un nome utente e una password per connettersi alla tua destinazione.

![Rendering dell’interfaccia utente con autenticazione di base](../../assets/functionality/destination-configuration/basic-authentication-ui.png)

Per impostare l’autenticazione di base per la destinazione, configura la `customerAuthenticationConfigurations` tramite `/destinations` punto finale come mostrato di seguito:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BASIC"
   }
]
```

## Autenticazione portatore {#bearer}

Quando configuri il tipo di autenticazione portatore, gli utenti devono inserire il token portatore ottenuto dalla destinazione.

![Rendering dell’interfaccia utente con autenticazione al portatore](../../assets/functionality/destination-configuration/bearer-authentication-ui.png)

Per impostare l’autenticazione del tipo di portatore per la destinazione, configura la `customerAuthenticationConfigurations` tramite `/destinations` punto finale come mostrato di seguito:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BEARER"
   }
]
```

## Autenticazione OAuth 2 {#oauth2}

Utenti selezionati **[!UICONTROL Connetti alla destinazione]** per attivare il flusso di autenticazione OAuth 2 nella destinazione, come mostrato nell’esempio seguente per la destinazione di tipi di pubblico personalizzati Twitter. Per informazioni dettagliate sulla configurazione dell’autenticazione OAuth 2 per l’endpoint di destinazione, consulta l’ [Destination SDK pagina di autenticazione OAuth 2](oauth2-authentication.md).

![Rendering dell’interfaccia utente con autenticazione OAuth 2](../../assets/functionality/destination-configuration/oauth2-authentication-ui.png)

Configurazione [!DNL OAuth2] autenticazione per la destinazione, configura `customerAuthenticationConfigurations` tramite `/destinations` punto finale come mostrato di seguito:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"OAUTH2"
   }
]
```

## Autenticazione Amazon S3 {#s3}

[!DNL Amazon S3] l’autenticazione è supportata, ad Experience Platform, per le destinazioni basate su file.

Quando configuri il tipo di autenticazione Amazon S3, gli utenti devono immettere le proprie credenziali S3.

![Rendering dell’interfaccia utente con autenticazione S3](../../assets/functionality/destination-configuration/s3-authentication-ui.png)

Configurazione [!DNL Amazon S3] autenticazione per la destinazione, configura `customerAuthenticationConfigurations` tramite `/destinations` punto finale come mostrato di seguito:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"S3"
   }
]
```

## Autenticazione BLOB di Azure  {#blob}

[!DNL Azure Blob Storage] l’autenticazione è supportata, ad Experience Platform, per le destinazioni basate su file.

Quando configuri il tipo di autenticazione BLOB di Azure, gli utenti devono immettere la stringa di connessione.

![Rendering dell’interfaccia utente con autenticazione BLOB](../../assets/functionality/destination-configuration/blob-authentication-ui.png)

Configurazione [!DNL Azure Blob] autenticazione per la destinazione, configura `customerAuthenticationConfigurations` nel `/destinations` punto finale come mostrato di seguito:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_CONNECTION_STRING"
   }
]
```

## [!DNL Azure Data Lake Storage] autenticazione {#adls}

[!DNL Azure Data Lake Storage] l’autenticazione è supportata, ad Experience Platform, per le destinazioni basate su file.

Quando configuri le [!DNL Azure Data Lake Storage] tipo di autenticazione, gli utenti devono inserire le credenziali dell’entità servizio Azure e le relative informazioni sul tenant.

![Rendering dell’interfaccia utente con [!DNL Azure Data Lake Storage] autenticazione](../../assets/functionality/destination-configuration/adls-authentication-ui.png)

Configurazione [!DNL Azure Data Lake Storage] (ADLS) autenticazione per la destinazione, configura il `customerAuthenticationConfigurations` nel `/destinations` punto finale come mostrato di seguito:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_SERVICE_PRINCIPAL"
   }
]
```

## SFTP con autenticazione tramite password

[!DNL SFTP] l’autenticazione con password è supportata, ad Experience Platform, per le destinazioni basate su file.

Quando configuri l’SFTP con il tipo di autenticazione tramite password, gli utenti devono immettere il nome utente e la password SFTP, nonché il dominio e la porta SFTP (la porta predefinita è 22).

![Rendering dell’interfaccia utente con SFTP con autenticazione tramite password](../../assets/functionality/destination-configuration/sftp-password-authentication-ui.png)

Per impostare l’autenticazione SFTP con password per la destinazione, configura la `customerAuthenticationConfigurations` nel `/destinations` punto finale come mostrato di seguito:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_PASSWORD"
   }
]
```

## SFTP con autenticazione a chiave SSH

[!DNL SFTP] autenticazione con [!DNL SSH] key è supportato per le destinazioni basate su file in Experience Platform.

Quando configuri l’SFTP con il tipo di autenticazione chiave SSH, gli utenti devono inserire il nome utente SFTP e la chiave SSH, nonché il dominio e la porta SFTP (la porta predefinita è 22).

![Rendering dell’interfaccia utente con SFTP con autenticazione a chiave SSH](../../assets/functionality/destination-configuration/sftp-key-authentication-ui.png)

Per impostare l’autenticazione SFTP con la chiave SSH per la destinazione, configura la `customerAuthenticationConfigurations` nel `/destinations` punto finale come mostrato di seguito:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_SSH_KEY"
   }
]
```

## [!DNL Google Cloud Storage] autenticazione {#gcs}

[!DNL Google Cloud Storage] l’autenticazione è supportata, ad Experience Platform, per le destinazioni basate su file.

Quando configuri le [!DNL Google Cloud Storage] tipo di autenticazione, gli utenti sono tenuti a immettere il proprio [!DNL Google Cloud Storage] [!UICONTROL ID chiave di accesso] e [!UICONTROL chiave di accesso segreta].

![Rendering dell’interfaccia utente con autenticazione Google Cloud Storage](../../assets/functionality/destination-configuration/google-cloud-storage-ui.png)

Configurazione [!DNL Google Cloud Storage] autenticazione per la destinazione, configura `customerAuthenticationConfigurations` nel `/destinations` punto finale come mostrato di seguito:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"GOOGLE_CLOUD_STORAGE"
   }
]
```

## Passaggi successivi {#next-steps}

Dopo aver letto questo articolo, dovresti avere una migliore comprensione di come configurare l’autenticazione degli utenti sulla piattaforma di destinazione.

Per ulteriori informazioni sugli altri componenti di destinazione, consulta i seguenti articoli:

* [Autenticazione OAuth2](oauth2-authentication.md)
* [Campi dati cliente](customer-data-fields.md)
* [Attributi dell&#39;interfaccia utente](ui-attributes.md)
* [Configurazione dello schema](schema-configuration.md)
* [Configurazione dello spazio dei nomi identità](identity-namespace-configuration.md)
* [Configurazioni di mappatura supportate](supported-mapping-configurations.md)
* [Consegna delle destinazioni](destination-delivery.md)
* [Configurazione dei metadati del pubblico](audience-metadata-configuration.md)
* [Criteri di aggregazione](aggregation-policy.md)
* [Configurazione batch](batch-configuration.md)
* [Qualifiche di profilo storiche](historical-profile-qualifications.md)