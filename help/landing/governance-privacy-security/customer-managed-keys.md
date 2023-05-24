---
title: Chiavi gestite dal cliente in Adobe Experience Platform
description: Scopri come impostare le tue chiavi di crittografia per i dati memorizzati in Adobe Experience Platform.
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1617'
ht-degree: 1%

---

# Chiavi gestite dal cliente in Adobe Experience Platform

I dati memorizzati su Adobe Experience Platform vengono crittografati a riposo utilizzando chiavi a livello di sistema. Se utilizzi un’applicazione basata su Platform, puoi scegliere di utilizzare le tue chiavi di crittografia, garantendo un maggiore controllo sulla sicurezza dei dati.

>[!NOTE]
>
>I dati nel data lake di Adobe Experience Platform e nell’archivio profili (CosmosDB) sono crittografati utilizzando CMK.

Questo documento descrive il processo di abilitazione della funzione chiavi gestite dal cliente (CMK) in Platform.

## Prerequisiti

Per abilitare la CMK, [!DNL Azure] L’insieme di credenziali delle chiavi deve essere configurato con le seguenti impostazioni:

* [Abilita protezione eliminazione](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [Abilita eliminazione temporanea](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [Configurare l’accesso tramite [!DNL Azure] controllo degli accessi basato su ruoli](https://learn.microsoft.com/en-us/azure/role-based-access-control/)

## Riepilogo del processo

La CMK è inclusa nell’offerta Healthcare Shield e nell’offerta Privacy and Security Shield di Adobe. Dopo che la tua organizzazione ha acquistato una licenza per una di queste offerte, puoi iniziare un processo una tantum per impostare la funzione.

>[!WARNING]
>
>Dopo aver configurato la CMK, non è possibile ripristinare le chiavi gestite dal sistema. Sei responsabile della gestione sicura delle chiavi e dell’accesso all’insieme di credenziali delle chiavi, alla chiave e all’app CMK in [!DNL Azure] per evitare la perdita dell&#39;accesso ai dati.

Il processo è il seguente:

1. [Configurare un [!DNL Azure] Key Vault](#create-key-vault) in base ai criteri della tua organizzazione, quindi [generare una chiave di crittografia](#generate-a-key) che alla fine sarà condiviso con Adobe.
1. Utilizzare le chiamate API per [configurare l’app CMK](#register-app) con il [!DNL Azure] tenant.
1. Utilizzare le chiamate API per [invia la chiave di crittografia ID all&#39;Adobe](#send-to-adobe) e avviare il processo di abilitazione per la feature.
1. [Verifica lo stato della configurazione](#check-status) per verificare se CMK è stato abilitato.

Una volta completato il processo di configurazione, tutti i dati inseriti in Platform in tutte le sandbox verranno crittografati utilizzando [!DNL Azure] impostazione della chiave. Per utilizzare la CMK, puoi sfruttare [!DNL Microsoft Azure] funzionalità che possono far parte del loro [programma di anteprima pubblica](https://azure.microsoft.com/en-ca/support/legal/preview-supplemental-terms/).

## Configurare un [!DNL Azure] Key Vault {#create-key-vault}

CMK supporta solo le chiavi di un [!DNL Microsoft Azure] Key Vault Per iniziare, devi lavorare con [!DNL Azure] per creare un nuovo account aziendale o utilizzare un account aziendale esistente e seguire i passaggi riportati di seguito per creare l&#39;insieme di credenziali delle chiavi.

>[!IMPORTANT]
>
>Solo i livelli di servizio Premium e Standard per [!DNL Azure] Sono supportati Key Vault. [!DNL Azure Managed HSM], [!DNL Azure Dedicated HSM] e [!DNL Azure Payments HSM] non sono supportati. Consulta la sezione [[!DNL Azure] documentazione](https://learn.microsoft.com/en-us/azure/security/fundamentals/key-management#azure-key-management-services) per ulteriori informazioni sui servizi di gestione delle chiavi offerti.

>[!NOTE]
>
>La documentazione seguente descrive solo i passaggi di base per creare l’insieme di credenziali delle chiavi. Al di fuori di questa guida, devi configurare l’archivio chiavi in base ai criteri della tua organizzazione.

Accedi a [!DNL Azure] e utilizza la barra di ricerca per individuare **[!DNL Key vaults]** nell’elenco dei servizi.

![Cerca e seleziona gli archivi di chiavi](../images/governance-privacy-security/customer-managed-keys/access-key-vaults.png)

Il **[!DNL Key vaults]** dopo aver selezionato il servizio. Da qui, seleziona **[!DNL Create]**.

![Crea insieme di credenziali delle chiavi](../images/governance-privacy-security/customer-managed-keys/create-key-vault.png)

Utilizzando il modulo fornito, compila i dettagli di base per l’insieme di credenziali delle chiavi, incluso un nome e un gruppo di risorse assegnato.

>[!WARNING]
>
>Anche se la maggior parte delle opzioni può essere lasciata come valori predefiniti, **assicurarsi di attivare le opzioni di protezione eliminazione temporanea e rimozione temporanea**. Se non si attivano queste funzioni, si potrebbe rischiare di perdere l&#39;accesso ai dati se l&#39;insieme di credenziali delle chiavi viene eliminato.
>
>![Abilita protezione eliminazione](../images/governance-privacy-security/customer-managed-keys/basic-config.png)

Da qui, continua a passare attraverso il flusso di lavoro di creazione dell’archivio chiave e configura le diverse opzioni in base ai criteri della tua organizzazione.

Una volta raggiunto il **[!DNL Review + create]** passaggio, è possibile rivedere i dettagli dell&#39;insieme di credenziali delle chiavi durante la convalida. Al termine della convalida, seleziona **[!DNL Create]** per completare il processo.

![Configurazione di base per l’insieme di credenziali delle chiavi](../images/governance-privacy-security/customer-managed-keys/finish-creation.png)

### Configurare le opzioni di rete

Se l&#39;insieme di credenziali delle chiavi è configurato per limitare l&#39;accesso pubblico a determinate reti virtuali o disabilitare completamente l&#39;accesso pubblico, è necessario concedere a Microsoft un&#39;eccezione firewall.

Seleziona **[!DNL Networking]** (Progetti) nel pannello di navigazione a sinistra. Sotto **[!DNL Firewalls and virtual networks]**, seleziona la casella di controllo **[!DNL Allow trusted Microsoft services to bypass this firewall]**, quindi seleziona **[!DNL Apply]**.

![Configurazione di base per l’insieme di credenziali delle chiavi](../images/governance-privacy-security/customer-managed-keys/networking.png)

### Generare una chiave {#generate-a-key}

Dopo aver creato un insieme di credenziali delle chiavi, puoi generare una nuova chiave. Accedi a **[!DNL Keys]** e seleziona **[!DNL Generate/Import]**.

![Generare una chiave](../images/governance-privacy-security/customer-managed-keys/view-keys.png)

Utilizza il modulo fornito per fornire un nome per la chiave e seleziona **RSA** per il tipo di chiave. Come minimo, il **[!DNL RSA key size]** deve essere almeno **3072** bit come richiesto da [!DNL Cosmos DB]. [!DNL Azure Data Lake Storage] è compatibile anche con RSA 3027.

>[!NOTE]
>
>Ricorda il nome fornito per la chiave, poiché verrà utilizzato in un passaggio successivo quando [invio della chiave all’Adobe](#send-to-adobe).

Utilizzare i controlli rimanenti per configurare la chiave che si desidera generare o importare in base alle proprie esigenze. Al termine, seleziona **[!DNL Create]**.

![Configura chiave](../images/governance-privacy-security/customer-managed-keys/configure-key.png)

La chiave configurata viene visualizzata nell&#39;elenco delle chiavi per l&#39;archivio.

![Chiave aggiunta](../images/governance-privacy-security/customer-managed-keys/key-added.png)

## Configurare l’app CMK {#register-app}

Dopo aver configurato l&#39;insieme di credenziali delle chiavi, il passaggio successivo consiste nel registrarsi per l&#39;applicazione CMK che verrà collegata al [!DNL Azure] tenant.

### Introduzione

La registrazione dell’app CMK richiede di effettuare chiamate alle API di Platform. Per informazioni dettagliate su come raccogliere le intestazioni di autenticazione necessarie per effettuare queste chiamate, vedi [Guida all’autenticazione API di Platform](../../landing/api-authentication.md).

La guida all’autenticazione fornisce istruzioni su come generare un valore univoco per il `x-api-key` richiesta, tutte le operazioni API in questa guida utilizzano il valore statico `acp_provisioning` invece. Devi comunque fornire i tuoi valori per `{ACCESS_TOKEN}` e `{ORG_ID}`, tuttavia.

In tutte le chiamate API mostrate in questa guida, `platform.adobe.io` viene utilizzato come percorso principale, che per impostazione predefinita corrisponde all&#39;area VA7. Se la tua organizzazione utilizza un’area geografica diversa, `platform` deve essere seguito da un trattino e dal codice di regione assegnato alla tua organizzazione: `nld2` per NLD2 o `aus5` per AUS5 (ad esempio: `platform-aus5.adobe.io`). Se non conosci l’area geografica della tua organizzazione, contatta l’amministratore di sistema.

### Recuperare un URL di autenticazione

GET Per avviare il processo di registrazione, effettua una richiesta all’endpoint di registrazione dell’app per recuperare l’URL di autenticazione richiesto per la tua organizzazione.

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/manager/byok/app-registration \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce `applicationRedirectUrl` contenente l&#39;URL di autenticazione.

```json
{
    "id": "byok",
    "name": "acpebae9422Caepcmkmultitenantapp",
    "applicationUri": "https://adobe.com/acpebae9422Caepcmkmultitenantapp",
    "applicationId": "e463a445-c6ac-4ca2-b36a-b5146fcf6a52",
    "applicationRedirectUrl": "https://login.microsoftonline.com/common/oauth2/authorize?response_type=code&client_id=e463a445-c6ac-4ca2-b36a-b5146fcf6a52&redirect_uri=https://adobe.com/acpebae9422Caepcmkmultitenantapp&scope=user.read"
}
```

Copiare e incollare `applicationRedirectUrl` in un browser per aprire una finestra di dialogo di autenticazione. Seleziona **[!DNL Accept]** per aggiungere l’entità del servizio app CMK al tuo [!DNL Azure] tenant.

![Accetta richiesta di autorizzazione](../images/governance-privacy-security/customer-managed-keys/app-permission.png)

### Assegnare l&#39;app CMK a un ruolo {#assign-to-role}

Dopo aver completato il processo di autenticazione, torna al [!DNL Azure] Key Vault e selezione **[!DNL Access control]** nel menu di navigazione a sinistra. Da qui, seleziona **[!DNL Add]** seguito da **[!DNL Add role assignment]**.

![Aggiungi assegnazione ruolo](../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

Nella schermata successiva viene richiesto di scegliere un ruolo per l&#39;assegnazione. Seleziona **[!DNL Key Vault Crypto Service Encryption User]** prima di selezionare **[!DNL Next]** per continuare.

![Seleziona ruolo](../images/governance-privacy-security/customer-managed-keys/select-role.png)

Nella schermata successiva scegliere **[!DNL Select members]** per aprire una finestra di dialogo nella barra a destra. Utilizzare la barra di ricerca per individuare l&#39;entità servizio per l&#39;applicazione CMK e selezionarla dall&#39;elenco. Al termine, seleziona **[!DNL Save]**.

>[!NOTE]
>
>Se l&#39;applicazione non è presente nell&#39;elenco, l&#39;entità servizio non è stata accettata nel tenant. Lavora con il [!DNL Azure] amministratore o rappresentante per assicurarsi di disporre dei privilegi corretti.

## Abilita la configurazione della chiave di crittografia su Experience Platform {#send-to-adobe}

Dopo aver installato l’app CMK su [!DNL Azure], puoi inviare l’identificatore della chiave di crittografia ad Adobe. Seleziona **[!DNL Keys]** nel menu di navigazione a sinistra, seguito dal nome della chiave che desideri inviare.

![Seleziona chiave](../images/governance-privacy-security/customer-managed-keys/select-key.png)

Seleziona la versione più recente della chiave e viene visualizzata la pagina dei relativi dettagli. Da qui è possibile configurare facoltativamente le operazioni consentite per la chiave. Come minimo, alla chiave deve essere concesso il **[!DNL Wrap Key]** e **[!DNL Unwrap Key]** autorizzazioni.

Il **[!UICONTROL Identificatore chiave]** visualizza l’identificatore URI della chiave. Copia questo valore URI da utilizzare nel passaggio successivo.

![Copia URL chiave](../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

Dopo aver ottenuto l’URI dell’insieme di credenziali delle chiavi, puoi inviarlo utilizzando una richiesta POST all’endpoint di configurazione CMK.

>[!NOTE]
>
>Con Adobe vengono memorizzati solo l’insieme di credenziali delle chiavi e il nome della chiave, non la versione della chiave.

**Richiesta**

```shell
curl -X POST \
  https://platform.adobe.io/data/infrastructure/manager/customer/config \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
        "name": "Config1",
        "type": "BYOK_CONFIG",
        "imsOrgId": "{ORG_ID}",
        "configData": {
          "providerType": "AZURE_KEYVAULT",
          "keyVaultKeyIdentifier": "https://adobecmkexample.vault.azure.net/keys/adobeCMK-key/7c1d50lo28234cc895534c00d7eb4eb4"
        }
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Un nome per la configurazione. Assicurati di ricordare questo valore in quanto sarà necessario per controllare lo stato della configurazione in un [passaggio successivo](#check-status). Il valore distingue tra maiuscole e minuscole. |
| `type` | Il tipo di configurazione. Deve essere impostato su `BYOK_CONFIG`. |
| `imsOrgId` | Il tuo ID organizzazione. Questo deve essere lo stesso valore fornito in `x-gw-ims-org-id` intestazione. |
| `configData` | Contiene i seguenti dettagli sulla configurazione:<ul><li>`providerType`: Deve essere impostato su `AZURE_KEYVAULT`.</li><li>`keyVaultKeyIdentifier`: URI dell’insieme di credenziali delle chiavi copiato [precedente](#send-to-adobe).</li></ul> |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli del processo di configurazione.

```json
{
  "id": "4df7886b-a122-4391-880b-47888d5c5b92",
  "config": {
    "configData": {
      "keyVaultUri": "https://adobecmkexample.vault.azure.net",
      "keyVaultKeyIdentifier": "https://adobecmkexample.vault.azure.net/keys/adobeCMK-key/7c1d50lo28234cc895534c00d7eb4eb4",
      "keyVersion": "7c1d50lo28234cc895534c00d7eb4eb4",
      "keyName": "Config1",
      "providerType": "AZURE_KEYVAULT"
    },
    "name": "acpcf978863Aaepcmkmultitenantapp",
    "type": "BYOK_CONFIG",
    "imsOrgId": "{IMS_ORG}",
    "status": "NEW"
  },
  "status": "CREATED"
}
```

L’elaborazione del processo dovrebbe essere completata entro pochi minuti.

## Verificare lo stato della configurazione {#check-status}

Per controllare lo stato della richiesta di configurazione, puoi effettuare una richiesta GET.

**Richiesta**

È necessario aggiungere `name` della configurazione da controllare nel percorso (`config1` nell’esempio seguente) e includono un `configType` parametro query impostato su `BYOK_CONFIG`.

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/manager/customer/config/config1?configType=BYOK_CONFIG \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato del processo.

```json
{
  "name": "acpcf978863Aaepcmkmultitenantapp",
  "type": "BYOK_CONFIG",
  "status": "COMPLETED",
  "configData": {
    "keyVaultUri": "https://adobecmkexample.vault.azure.net",
    "keyVaultKeyIdentifier": "https://adobecmkexample.vault.azure.net/keys/adobeCMK-key/7c1d50lo28234cc895534c00d7eb4eb4",
    "keyVersion": "7c1d50lo28234cc895534c00d7eb4eb4",
    "keyName": "Config1",
    "providerType": "AZURE_KEYVAULT"
  },
  "imsOrgId": "{IMS_ORG}",
  "subscriptionId": "cf978863-7325-47b1-8fd9-554b9fdb6c36",
  "id": "4df7886b-a122-4391-880b-47888d5c5b92",
  "rowType": "BYOK_KEY"
}
```

Il `status` l&#39;attributo può avere uno dei quattro valori con i seguenti significati:

1. `RUNNING`: verifica che Platform sia in grado di accedere all’insieme di credenziali delle chiavi e delle chiavi.
1. `UPDATE_EXISTING_RESOURCES`: il sistema sta aggiungendo l’insieme di credenziali e il nome della chiave agli archivi di dati in tutte le sandbox dell’organizzazione.
1. `COMPLETED`: l’insieme di credenziali delle chiavi e il nome della chiave sono stati aggiunti agli archivi dati.
1. `FAILED`: si è verificato un problema, principalmente relativo alla chiave, all’insieme di credenziali delle chiavi o alla configurazione di app multi-tenant.

## Passaggi successivi

Completando i passaggi precedenti, hai abilitato correttamente la CMK per la tua organizzazione. I dati acquisiti in Platform verranno ora crittografati e decrittografati utilizzando le chiavi nella [!DNL Azure] Key Vault Se desideri revocare l’accesso di Platform ai tuoi dati, puoi rimuovere il ruolo utente associato all’applicazione dall’archivio chiavi in [!DNL Azure].

Dopo aver disabilitato l’accesso all’applicazione, possono essere necessarie da pochi minuti a 24 ore affinché i dati non siano più accessibili in Platform. Lo stesso ritardo si applica ai dati che diventano nuovamente disponibili quando si riabilita l’accesso all’applicazione.

>[!WARNING]
>
>Una volta che l’app Key Vault, Key o CMK è disabilitata e i dati non sono più accessibili in Platform, non sarà più possibile effettuare operazioni a valle relative a tali dati. Prima di apportare modifiche alla configurazione, assicurati di comprendere gli effetti a valle della revoca dell’accesso di Platform ai dati.
