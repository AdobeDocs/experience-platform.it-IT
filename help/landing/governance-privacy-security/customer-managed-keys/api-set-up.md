---
title: Configurare e configurare le chiavi gestite dal cliente tramite l’API
description: Scopri come configurare l’app CMK con il tenant di Azure e inviare l’ID della chiave di crittografia a Adobe Experience Platform.
exl-id: c9a1888e-421f-4bb4-b4c7-968fb1d61746
source-git-commit: 4f08e8fcc8d53b981af60226f1397a1d1ac4d8dc
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 1%

---

# Configurare e configurare le chiavi gestite dal cliente tramite l’API

Questo documento descrive il processo di abilitazione della funzione chiavi gestite dal cliente (CMK) in Adobe Experience Platform utilizzando l’API. Per istruzioni su come completare questo processo utilizzando l’interfaccia utente, consulta [Documento di configurazione della CMK per l’interfaccia utente](./ui-set-up.md).

## Prerequisiti

Per visualizzare e visitare il [!UICONTROL Crittografia] in Adobe Experience Platform, è necessario aver creato un ruolo e assegnato il [!UICONTROL Gestisci chiave gestita dal cliente] autorizzazione per quel ruolo. Qualsiasi utente che dispone di [!UICONTROL Gestisci chiave gestita dal cliente] L’autorizzazione può abilitare la CMK per la loro organizzazione.

Per ulteriori informazioni sull’assegnazione di ruoli e autorizzazioni in Experienci Platform, consulta [configurare la documentazione sulle autorizzazioni](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html?lang=it).

Per attivare la CMK, [[!DNL Azure] L’insieme di credenziali delle chiavi deve essere configurato](./azure-key-vault-config.md) con le seguenti impostazioni:

* [Abilita protezione eliminazione](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [Abilita eliminazione temporanea](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [Configurare l’accesso tramite [!DNL Azure] controllo degli accessi basato su ruoli](https://learn.microsoft.com/en-us/azure/role-based-access-control/)
* [Configurare un [!DNL Azure] Key Vault](./azure-key-vault-config.md)

## Configurare l’app CMK {#register-app}

Dopo aver configurato l&#39;insieme di credenziali delle chiavi, il passaggio successivo consiste nel registrarsi per l&#39;applicazione CMK che verrà collegata al [!DNL Azure] tenant.

### Introduzione

La registrazione dell’app CMK richiede di effettuare chiamate alle API di Platform. Per informazioni dettagliate su come raccogliere le intestazioni di autenticazione necessarie per effettuare queste chiamate, vedi [Guida all’autenticazione API di Platform](../../api-authentication.md).

La guida all’autenticazione fornisce istruzioni su come generare un valore univoco per il `x-api-key` richiesta, tutte le operazioni API in questa guida utilizzano il valore statico `acp_provisioning` invece. Devi comunque fornire i tuoi valori per `{ACCESS_TOKEN}` e `{ORG_ID}`, tuttavia.

In tutte le chiamate API mostrate in questa guida, `platform.adobe.io` viene utilizzato come percorso principale, che per impostazione predefinita corrisponde all&#39;area VA7. Se la tua organizzazione utilizza un’area geografica diversa, `platform` deve essere seguito da un trattino e dal codice di regione assegnato alla tua organizzazione: `nld2` per NLD2 o `aus5` per AUS5 (ad esempio: `platform-aus5.adobe.io`). Se non conosci l’area geografica della tua organizzazione, contatta l’amministratore di sistema.

### Recuperare un URL di autenticazione {#fetch-authentication-url}

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

![Finestra di dialogo per la richiesta di autorizzazione di Microsoft con [!UICONTROL Accetta] evidenziato.](../../images/governance-privacy-security/customer-managed-keys/app-permission.png)

### Assegnare l&#39;app CMK a un ruolo {#assign-to-role}

Dopo aver completato il processo di autenticazione, torna al [!DNL Azure] Key Vault e selezione **[!DNL Access control]** nel menu di navigazione a sinistra. Da qui, seleziona **[!DNL Add]** seguito da **[!DNL Add role assignment]**.

![Dashboard di Microsoft Azure con [!DNL Add] e [!DNL Add role assignment] evidenziato.](../../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

Nella schermata successiva viene richiesto di scegliere un ruolo per l&#39;assegnazione. Seleziona **[!DNL Key Vault Crypto Service Encryption User]** prima di selezionare **[!DNL Next]** per continuare.

>[!NOTE]
>
>Se si dispone di [!DNL Managed-HSM Key Vault] livello, è necessario selezionare il **[!DNL Managed HSM Crypto Service Encryption User]** ruolo utente.

![Dashboard di Microsoft Azure con [!DNL Key Vault Crypto Service Encryption User] evidenziato.](../../images/governance-privacy-security/customer-managed-keys/select-role.png)

Nella schermata successiva scegliere **[!DNL Select members]** per aprire una finestra di dialogo nella barra a destra. Utilizzare la barra di ricerca per individuare l&#39;entità servizio per l&#39;applicazione CMK e selezionarla dall&#39;elenco. Al termine, seleziona **[!DNL Save]**.

>[!NOTE]
>
>Se l&#39;applicazione non è presente nell&#39;elenco, l&#39;entità servizio non è stata accettata nel tenant. Per assicurarti di disporre dei privilegi corretti, utilizza [!DNL Azure] amministratore o rappresentante.

## Abilita la configurazione della chiave di crittografia su Experienci Platform {#send-to-adobe}

Dopo aver installato l’app CMK su [!DNL Azure], puoi inviare l’identificatore della chiave di crittografia ad Adobe. Seleziona **[!DNL Keys]** nel menu di navigazione a sinistra, seguito dal nome della chiave che desideri inviare.

![Dashboard di Microsoft Azure con [!DNL Keys] e il nome chiave evidenziato.](../../images/governance-privacy-security/customer-managed-keys/select-key.png)

Seleziona la versione più recente della chiave e viene visualizzata la pagina dei relativi dettagli. Da qui, puoi facoltativamente configurare le operazioni consentite per la chiave.

>[!IMPORTANT]
>
>Le operazioni minime richieste per la chiave sono le **[!DNL Wrap Key]** e **[!DNL Unwrap Key]** autorizzazioni. Puoi includere [!DNL Encrypt], [!DNL Decrypt], [!DNL Sign], e [!DNL Verify] dovrebbe volere.

Il **[!UICONTROL Identificatore chiave]** visualizza l’identificatore URI della chiave. Copia questo valore URI da utilizzare nel passaggio successivo.

![I dettagli della chiave del dashboard di Microsoft Azure con [!DNL Permitted operations] ed evidenziate le sezioni copia URL chiave.](../../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

Dopo aver ottenuto l’URI dell’insieme di credenziali delle chiavi, puoi inviarlo utilizzando una richiesta POST all’endpoint di configurazione CMK.

>[!NOTE]
>
>Con Adobe vengono memorizzati solo l’insieme di credenziali delle chiavi e il nome della chiave, non la versione della chiave.

**Richiesta**

+++ Richiesta di esempio per inviare l’URI dell’insieme di credenziali delle chiavi all’endpoint di configurazione CMK.

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
| `name` | Un nome per la configurazione. Assicurati di ricordare questo valore in quanto necessario per controllare lo stato della configurazione in un [passaggio successivo](#check-status). Il valore distingue tra maiuscole e minuscole. |
| `type` | Il tipo di configurazione. Deve essere impostato su `BYOK_CONFIG`. |
| `imsOrgId` | ID organizzazione. Questo ID deve essere lo stesso valore fornito in `x-gw-ims-org-id` intestazione. |
| `configData` | Questa proprietà contiene i seguenti dettagli sulla configurazione:<ul><li>`providerType`: deve essere impostato su `AZURE_KEYVAULT`.</li><li>`keyVaultKeyIdentifier`: URI dell’insieme di credenziali delle chiavi copiato [precedente](#send-to-adobe).</li></ul> |

+++

**Risposta**

+++ In caso di esito positivo, la risposta restituisce i dettagli del processo di configurazione.

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
    "imsOrgId": "{ORG_ID}",
    "status": "NEW"
  },
  "status": "CREATED"
}
```

+++

L’elaborazione del processo dovrebbe essere completata entro pochi minuti.

## Verificare lo stato della configurazione {#check-status}

Per controllare lo stato della richiesta di configurazione, puoi effettuare una richiesta GET.

**Richiesta**

È necessario aggiungere `name` della configurazione da controllare nel percorso (`config1` nell’esempio seguente) e includono un `configType` parametro query impostato su `BYOK_CONFIG`.

+++ Una richiesta di esempio per controllare lo stato della richiesta di configurazione.

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/manager/customer/config/config1?configType=BYOK_CONFIG \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

+++

**Risposta**

+++ In caso di esito positivo, la risposta restituisce lo stato del processo.

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
  "imsOrgId": "{ORG_ID}",
  "subscriptionId": "cf978863-7325-47b1-8fd9-554b9fdb6c36",
  "id": "4df7886b-a122-4391-880b-47888d5c5b92",
  "rowType": "BYOK_KEY"
}
```

+++

Il `status` l&#39;attributo può avere uno dei quattro valori con i seguenti significati:

1. `RUNNING`: verifica che Platform possa accedere all’insieme di credenziali delle chiavi e delle chiavi.
1. `UPDATE_EXISTING_RESOURCES`: il sistema sta aggiungendo l’insieme di credenziali e il nome della chiave agli archivi di dati in tutte le sandbox dell’organizzazione.
1. `COMPLETED`: l’insieme di credenziali delle chiavi e il nome della chiave sono stati aggiunti correttamente agli archivi dati.
1. `FAILED`: si è verificato un problema, principalmente relativo alla chiave, all’insieme di credenziali delle chiavi o alla configurazione di app multi-tenant.

## Passaggi successivi

Completando i passaggi precedenti, hai abilitato correttamente la CMK per la tua organizzazione. I dati acquisiti negli archivi di dati primari ora vengono crittografati e decrittografati utilizzando le chiavi nella [!DNL Azure] Key Vault Per ulteriori informazioni sulla crittografia dei dati in Adobe Experience Platform, consulta [documentazione sulla crittografia](../encryption.md).
