---
title: Database di Azure
description: Scopri i passaggi preliminari necessari per collegare i database di Azure ad Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
badgeBeta: label="Beta" type="Informative"
last-substantial-update: 2025-04-29T00:00:00Z
exl-id: 2f082898-aa0e-47a1-a4bf-077c21afdfee
source-git-commit: 0c8ff1029beee3f58cbf536b11b40551b6f6c2ed
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 3%

---

# [!DNL Azure Databricks]

>[!AVAILABILITY]
>
>* L&#39;origine [!DNL Azure Databricks] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-Time CDP Ultimate.
>
>* L&#39;origine [!DNL Azure Databricks] è in versione beta. Leggi i [termini e condizioni](../../home.md#terms-and-conditions) nella panoramica delle origini per ulteriori informazioni sull&#39;utilizzo di origini con etichetta beta.

[!DNL Azure Databricks] è una piattaforma basata su cloud progettata per l&#39;analisi dei dati, l&#39;apprendimento automatico e l&#39;intelligenza artificiale. È possibile utilizzare [!DNL Databricks] per l&#39;integrazione con [!DNL Azure] e fornire un ambiente olistico per la creazione, la distribuzione e la gestione di soluzioni di dati su larga scala.

Utilizza l&#39;origine [!DNL Databricks] per connettere il tuo account e acquisire i dati di [!DNL Databricks] in Adobe Experience Platform.

## Prerequisiti

Completa i passaggi preliminari per connettere correttamente l&#39;account [!DNL Databricks] ad Experience Platform.

### Recuperare le credenziali del contenitore

Recupera le credenziali di Experience Platform [!DNL Azure Blob Storage] per consentire al tuo account [!DNL Databricks] di accedervi in un secondo momento.

Per recuperare le credenziali, effettuare una richiesta GET all&#39;endpoint `/credentials` dell&#39;API [!DNL Connectors].

**Formato API**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source
```

**Richiesta**

La richiesta seguente recupera le credenziali per l&#39;Experience Platform [!DNL Azure Blob Storage].

Esempio di richiesta +++View

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Risposta**

In caso di esito positivo, la risposta fornisce le credenziali (`containerName`, `SASToken`, `storageAccountName`) per un utilizzo successivo nella configurazione [!DNL Apache Spark] per [!DNL Databricks].

+++Visualizza esempio di risposta

```json
{
    "containerName": "dlz-databricks-container",
    "SASToken": "sv=2020-10-02&si=dlz-b1f4060b-6bbd-4043-9bd9-a5f5be72de30&sr=c&sp=racwdlm&sig=zVQfmuElZJzOKkUk8z5lChrJ3YQUE2h6EShDZOsVeMc%3D",
    "storageAccountName": "sndbxdtlndga8m7ajbvgc64k",
    "SASUri": "https://sndbxdtlndga8m7ajbvgc64k.blob.core.windows.net/dlz-databricks-container?sv=2020-10-02&si=dlz-b1f4060b-6bbd-4043-9bd9-a5f5be72de30&sr=c&sp=racwdlm&sig=zVQfmuElZJzOKkUk8z5lChrJ3YQUE2h6EShDZOsVeMc%3D",
    "expiryDate": "2025-07-05"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `containerName` | Nome del contenitore [!DNL Azure Blob Storage]. Questo valore verrà utilizzato in seguito al completamento della configurazione di [!DNL Apache Spark] per [!DNL Databricks]. |
| `SASToken` | Il token di firma di accesso condiviso per [!DNL Azure Blob Storage]. Questa stringa contiene tutte le informazioni necessarie per autorizzare una richiesta. |
| `storageAccountName` | Il nome dell&#39;account di archiviazione. |
| `SASUri` | URI della firma di accesso condiviso per [!DNL Azure Blob Storage]. Questa stringa è una combinazione dell&#39;URI di [!DNL Azure Blob Storage] per il quale si sta eseguendo l&#39;autenticazione e del token SAS corrispondente. |
| `expiryDate` | Data di scadenza del token SAS. È necessario aggiornare il token prima della data di scadenza per continuare a utilizzarlo nell&#39;applicazione per il caricamento di dati in [!DNL Azure Blob Storage]. Se non aggiorni manualmente il token prima della data di scadenza indicata, questo verrà aggiornato automaticamente e fornirà un nuovo token quando viene eseguita la chiamata delle credenziali di GET. |

+++

### Aggiorna le credenziali

>[!NOTE]
>
>Le credenziali esistenti verranno revocate dopo l&#39;aggiornamento delle credenziali. Pertanto, è necessario aggiornare [!DNL Spark] configurazioni di conseguenza ogni volta che si aggiornano le credenziali di archiviazione. In caso contrario, il flusso di dati non riuscirà.

Per aggiornare le credenziali, eseguire una richiesta POST e includere `action=refresh` come parametro di query.

**Formato API**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source&action=refresh
```

**Richiesta**

La richiesta seguente aggiorna le credenziali per [!DNL Azure Blob Storage].

Esempio di richiesta +++View

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce le nuove credenziali.

+++Visualizza esempio di risposta

```json
{
    "containerName": "dlz-databricks-container",
    "SASToken": "sv=2020-10-02&si=dlz-6e17e5d6-de18-4efc-88c7-45f37d242617&sr=c&sp=racwdlm&sig=wvA4K3fcEmqAA%2FPvcMhB%2FA8y8RLwVJ7zhdWbxvT1uFM%3D",
    "storageAccountName": "sndbxdtlndga8m7ajbvgc64k",
    "SASUri": "https://sndbxdtlndga8m7ajbvgc64k.blob.core.windows.net/dlz-databricks-container?sv=2020-10-02&si=dlz-6e17e5d6-de18-4efc-88c7-45f37d242617&sr=c&sp=racwdlm&sig=wvA4K3fcEmqAA%2FPvcMhB%2FA8y8RLwVJ7zhdWbxvT1uFM%3D",
    "expiryDate": "2025-07-20"
}
```

+++

### Configura l&#39;accesso a [!DNL Azure Blob Storage]

>[!IMPORTANT]
>
>* Se il cluster è stato terminato, il servizio lo riavvia automaticamente durante l&#39;esecuzione di un flusso. Tuttavia, è necessario assicurarsi che il cluster sia attivo durante la creazione di una connessione o di un flusso di dati. Inoltre, il cluster deve essere attivo se si eseguono azioni quali l&#39;anteprima o l&#39;esplorazione dei dati, in quanto tali azioni non possono richiedere il riavvio automatico di un cluster terminato.
>
>* Il contenitore [!DNL Azure] include una cartella denominata `adobe-managed-staging`. Per garantire l&#39;acquisizione diretta dei dati, **non** modificare questa cartella.


Successivamente, è necessario assicurarsi che il cluster [!DNL Databricks] abbia accesso all&#39;account Experience Platform [!DNL Azure Blob Storage]. In questo modo è possibile utilizzare [!DNL Azure Blob Storage] come posizione provvisoria per la scrittura dei dati della tabella [!DNL delta lake].

Per fornire l&#39;accesso, è necessario configurare un token SAS nel cluster [!DNL Databricks] come parte della configurazione [!DNL Apache Spark].

Nell&#39;interfaccia di [!DNL Databricks], selezionare **[!DNL Advanced options]**, quindi immettere quanto segue nella casella di input [!DNL Spark config].

```shell
fs.azure.sas.{CONTAINER_NAME}.{STORAGE-ACCOUNT}.blob.core.windows.net {SAS-TOKEN}
```

| Proprietà | Descrizione |
| --- | --- |
| Nome contenitore | Nome del contenitore. È possibile ottenere questo valore recuperando le credenziali di [!DNL Azure Blob Storage]. |
| Account di archiviazione | Il nome dell&#39;account di archiviazione. È possibile ottenere questo valore recuperando le credenziali di [!DNL Azure Blob Storage]. |
| Token SAS | Il token di firma di accesso condiviso per [!DNL Azure Blob Storage]. È possibile ottenere questo valore recuperando le credenziali di [!DNL Azure Blob Storage]. |

![Interfaccia utente di Database in Azure.](../../images/tutorials/create/databricks/databricks-ui.png)

## Connetti [!DNL Databricks] ad Experience Platform tramite API

Ora che hai completato i passaggi preliminari, puoi passare alla guida su [connessione dell&#39;account  [!DNL Databricks] ad Experience Platform tramite l&#39;API](../../tutorials/api/create/databases/databricks.md).
