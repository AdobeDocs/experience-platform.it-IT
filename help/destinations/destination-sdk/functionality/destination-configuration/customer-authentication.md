---
description: Scopri come impostare un meccanismo di autenticazione per la destinazione e ottenere informazioni approfondite su ciò che gli utenti vedranno nell’interfaccia utente a seconda del metodo di autenticazione selezionato.
title: Configurazione autenticazione cliente
exl-id: 3912012e-0870-47d2-9a6f-7f1fc469a781
source-git-commit: 82ba4e62d5bb29ba4fef22c5add864a556e62c12
workflow-type: tm+mt
source-wordcount: '1101'
ht-degree: 0%

---

# Configurazione autenticazione cliente

Experience Platform offre grande flessibilità nei protocolli di autenticazione disponibili per partner e clienti. È possibile configurare la destinazione in modo da supportare i metodi di autenticazione standard del settore come [!DNL OAuth2], l&#39;autenticazione del token Bearer, l&#39;autenticazione della password e molti altri.

Questa pagina spiega come impostare la destinazione utilizzando il metodo di autenticazione preferito. In base alla configurazione di autenticazione utilizzata durante la creazione della destinazione, i clienti vedranno diversi tipi di pagine di autenticazione durante la connessione alla destinazione nell’interfaccia utente di Experience Platform.

Per capire dove questo componente si inserisce in un&#39;integrazione creata con Destination SDK, consulta il diagramma nella documentazione delle [opzioni di configurazione](../configuration-options.md) oppure vedi le seguenti pagine di panoramica sulla configurazione di destinazione:

* [Utilizzare Destination SDK per configurare una destinazione di streaming](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Utilizzare Destination SDK per configurare una destinazione basata su file](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

Prima che i clienti possano esportare i dati da Platform alla destinazione, devono creare una nuova connessione tra Experience Platform e la destinazione, seguendo i passaggi descritti nell&#39;esercitazione [connessione di destinazione](../../../ui/connect-destination.md).

Durante la [creazione di una destinazione](../../authoring-api/destination-configuration/create-destination-configuration.md) tramite Destination SDK, la sezione `customerAuthenticationConfigurations` definisce ciò che i clienti visualizzano nella [schermata di autenticazione](../../../ui/connect-destination.md#authenticate). A seconda del tipo di autenticazione di destinazione, i clienti devono fornire vari dettagli di autenticazione, ad esempio:

* Per le destinazioni che utilizzano l&#39;[autenticazione di base](#basic), gli utenti devono fornire un nome utente e una password direttamente nella pagina di autenticazione dell&#39;interfaccia utente Experience Platform.
* Per le destinazioni che utilizzano l&#39;[autenticazione bearer](#bearer), gli utenti devono fornire un token bearer.
* Per le destinazioni che utilizzano l&#39;[autorizzazione OAuth2](#oauth2), gli utenti vengono reindirizzati alla pagina di accesso della destinazione in cui possono accedere con le proprie credenziali.
* Per [destinazioni Amazon S3](#s3), gli utenti devono fornire la propria chiave di accesso [!DNL Amazon S3] e la propria chiave segreta.
* Per [destinazioni BLOB di Azure](#blob), gli utenti devono fornire la stringa di connessione [!DNL Azure Blob].

È possibile configurare i dettagli di autenticazione del cliente tramite l&#39;endpoint `/authoring/destinations`. Consulta le seguenti pagine di riferimento API per esempi dettagliati di chiamate API, in cui puoi configurare i componenti mostrati in questa pagina.

* [Creare una configurazione di destinazione](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Aggiornare una configurazione di destinazione](../../authoring-api/destination-configuration/update-destination-configuration.md)

Questo articolo descrive tutte le configurazioni di autenticazione dei clienti supportate che è possibile utilizzare per la destinazione e mostra ciò che i clienti vedranno nell’interfaccia utente di Experience Platform in base al metodo di autenticazione configurato per la destinazione.

>[!IMPORTANT]
>
>La configurazione dell’autenticazione del cliente non richiede la configurazione di alcun parametro. Puoi copiare e incollare i snippet mostrati in questa pagina nelle chiamate API quando [crei](../../authoring-api/destination-configuration/create-destination-configuration.md) o [aggiorni](../../authoring-api/destination-configuration/update-destination-configuration.md) una configurazione di destinazione e gli utenti vedranno la schermata di autenticazione corrispondente nell&#39;interfaccia utente di Platform.

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **con distinzione tra maiuscole e minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Tipi di integrazione supportati {#supported-integration-types}

Consulta la tabella seguente per informazioni dettagliate sui tipi di integrazioni che supportano le funzionalità descritte in questa pagina.

| Tipo di integrazione | Supporta la funzionalità |
|---|---|
| Integrazioni in tempo reale (streaming) | Sì |
| Integrazioni basate su file (batch) | Sì |

## Configurazione della regola di autenticazione {#authentication-rule}

Quando si utilizza una delle configurazioni di autenticazione cliente descritte in questa pagina, impostare sempre il parametro `authenticationRule` in [consegna di destinazione](destination-delivery.md) su `"CUSTOMER_AUTHENTICATION"`, come illustrato di seguito.

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

Quando si configura il tipo di autenticazione di base, gli utenti devono immettere un nome utente e una password per connettersi alla destinazione.

![Rendering interfaccia utente con autenticazione di base](../../assets/functionality/destination-configuration/basic-authentication-ui.png)

Per impostare l&#39;autenticazione di base per la destinazione, configurare la sezione `customerAuthenticationConfigurations` tramite l&#39;endpoint `/destinations` come illustrato di seguito:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BASIC"
   }
]
```

## Autenticazione Bearer {#bearer}

Quando configuri il tipo di autenticazione bearer, gli utenti devono immettere il token bearer ottenuto dalla destinazione.

![Rendering interfaccia utente con autenticazione Bearer](../../assets/functionality/destination-configuration/bearer-authentication-ui.png)

Per impostare l&#39;autenticazione di tipo Bearer per la destinazione, configurare la sezione `customerAuthenticationConfigurations` tramite l&#39;endpoint `/destinations` come illustrato di seguito:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BEARER"
   }
]
```

## Autenticazione OAuth 2 {#oauth2}

Gli utenti selezionano **[!UICONTROL Connetti alla destinazione]** per attivare il flusso di autenticazione OAuth 2 nella tua destinazione, come mostrato nell&#39;esempio seguente per la destinazione Twitter Tipi di pubblico personalizzati. Per informazioni dettagliate sulla configurazione dell&#39;autenticazione OAuth 2 per l&#39;endpoint di destinazione, leggere la pagina dedicata [Destination SDK autenticazione OAuth 2](oauth2-authorization.md).

![Rendering interfaccia utente con autenticazione OAuth 2](../../assets/functionality/destination-configuration/oauth2-authentication-ui.png)

Per impostare l&#39;autenticazione [!DNL OAuth2] per la destinazione, configurare la sezione `customerAuthenticationConfigurations` tramite l&#39;endpoint `/destinations` come illustrato di seguito:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"OAUTH2"
   }
]
```

## Autenticazione Amazon S3 {#s3}

L&#39;autenticazione [!DNL Amazon S3] è supportata per le destinazioni basate su file in Experience Platform.

Quando configuri il tipo di autenticazione Amazon S3, agli utenti viene richiesto di immettere le credenziali S3.

![Rendering interfaccia utente con autenticazione S3](../../assets/functionality/destination-configuration/s3-authentication-ui.png)

Per impostare l&#39;autenticazione [!DNL Amazon S3] per la destinazione, configurare la sezione `customerAuthenticationConfigurations` tramite l&#39;endpoint `/destinations` come illustrato di seguito:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"S3"
   }
]
```

## Autenticazione BLOB di Azure  {#blob}

L&#39;autenticazione [!DNL Azure Blob Storage] è supportata per le destinazioni basate su file in Experience Platform.

Quando configuri il tipo di autenticazione BLOB di Azure, gli utenti devono immettere la stringa di connessione.

![Rendering interfaccia utente con autenticazione BLOB](../../assets/functionality/destination-configuration/blob-authentication-ui.png)

Per impostare l&#39;autenticazione [!DNL Azure Blob] per la destinazione, configurare il parametro `customerAuthenticationConfigurations` nell&#39;endpoint `/destinations` come illustrato di seguito:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_CONNECTION_STRING"
   }
]
```

## Autenticazione di [!DNL Azure Data Lake Storage] {#adls}

L&#39;autenticazione [!DNL Azure Data Lake Storage] è supportata per le destinazioni basate su file in Experience Platform.

Quando si configura il tipo di autenticazione [!DNL Azure Data Lake Storage], gli utenti devono immettere le credenziali dell&#39;entità servizio Azure e le informazioni sul tenant.

![Rendering interfaccia utente con [!DNL Azure Data Lake Storage] autenticazione](../../assets/functionality/destination-configuration/adls-authentication-ui.png)

Per impostare l&#39;autenticazione di [!DNL Azure Data Lake Storage] (ADLS) per la destinazione, configurare il parametro `customerAuthenticationConfigurations` nell&#39;endpoint `/destinations` come illustrato di seguito:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_SERVICE_PRINCIPAL"
   }
]
```

## SFTP con autenticazione tramite password

L&#39;autenticazione [!DNL SFTP] con password è supportata per le destinazioni basate su file in Experience Platform.

Quando configuri SFTP con il tipo di autenticazione tramite password, gli utenti devono immettere il nome utente e la password SFTP, nonché il dominio e la porta SFTP (la porta predefinita è 22).

![Rendering dell&#39;interfaccia utente con SFTP con autenticazione tramite password](../../assets/functionality/destination-configuration/sftp-password-authentication-ui.png)

Per impostare l&#39;autenticazione SFTP con password per la destinazione, configura il parametro `customerAuthenticationConfigurations` nell&#39;endpoint `/destinations` come illustrato di seguito:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_PASSWORD"
   }
]
```

## SFTP con autenticazione della chiave SSH

L&#39;autenticazione [!DNL SFTP] con chiave [!DNL SSH] è supportata per le destinazioni basate su file in Experience Platform.

Quando configuri SFTP con il tipo di autenticazione della chiave SSH, gli utenti devono immettere il nome utente SFTP e la chiave SSH, nonché il dominio SFTP e la porta (la porta predefinita è 22).

![Rendering dell&#39;interfaccia utente con SFTP con autenticazione con chiave SSH](../../assets/functionality/destination-configuration/sftp-key-authentication-ui.png)

Per impostare l&#39;autenticazione SFTP con chiave SSH per la destinazione, configura il parametro `customerAuthenticationConfigurations` nell&#39;endpoint `/destinations` come illustrato di seguito:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_SSH_KEY"
   }
]
```

## Autenticazione di [!DNL Google Cloud Storage] {#gcs}

L&#39;autenticazione [!DNL Google Cloud Storage] è supportata per le destinazioni basate su file in Experience Platform.

Quando si configura il tipo di autenticazione [!DNL Google Cloud Storage], gli utenti devono immettere il proprio [!DNL Google Cloud Storage] [!UICONTROL ID chiave di accesso] e [!UICONTROL chiave di accesso segreta].

![Rendering interfaccia utente con autenticazione di Google Cloud Storage](../../assets/functionality/destination-configuration/google-cloud-storage-ui.png)

Per impostare l&#39;autenticazione [!DNL Google Cloud Storage] per la destinazione, configurare il parametro `customerAuthenticationConfigurations` nell&#39;endpoint `/destinations` come illustrato di seguito:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"GOOGLE_CLOUD_STORAGE"
   }
]
```

## Passaggi successivi {#next-steps}

Dopo aver letto questo articolo, sarai in grado di comprendere meglio come configurare l’autenticazione utente sulla piattaforma di destinazione.

Per ulteriori informazioni sugli altri componenti di destinazione, consulta i seguenti articoli:

* [Autorizzazione OAuth2](oauth2-authorization.md)
* [Campi dati cliente](customer-data-fields.md)
* [Attributi dell’interfaccia utente](ui-attributes.md)
* [Configurazione dello schema](schema-configuration.md)
* [Configurazione dello spazio dei nomi dell’identità](identity-namespace-configuration.md)
* [Configurazioni di mappatura supportate](supported-mapping-configurations.md)
* [Consegna della destinazione](destination-delivery.md)
* [Configurazione dei metadati del pubblico](audience-metadata-configuration.md)
* [Criterio di aggregazione](aggregation-policy.md)
* [Configurazione batch](batch-configuration.md)
* [Qualifiche del profilo storico](historical-profile-qualifications.md)
