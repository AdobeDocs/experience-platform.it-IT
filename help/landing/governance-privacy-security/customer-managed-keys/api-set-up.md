---
title: Configurare e configurare le chiavi gestite dal cliente tramite l’API
description: Scopri come configurare l’app CMK con il tenant di Azure e inviare l’ID della chiave di crittografia a Adobe Experience Platform.
role: Developer
feature: API, Privacy
exl-id: c9a1888e-421f-4bb4-b4c7-968fb1d61746
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 1%

---

# Configurare e configurare le chiavi gestite dal cliente tramite l’API

Questo documento descrive il processo di abilitazione della funzione chiavi gestite dal cliente (CMK) in Adobe Experience Platform utilizzando l’API. Per istruzioni su come completare il processo utilizzando l&#39;interfaccia utente, fare riferimento al documento di installazione della CMK [UI](./ui-set-up.md).

## Prerequisiti

Per visualizzare e visitare la sezione [!UICONTROL Crittografia] in Adobe Experience Platform, è necessario aver creato un ruolo e assegnato l&#39;autorizzazione [!UICONTROL Gestione chiave gestita dal cliente] a tale ruolo. Qualsiasi utente con l&#39;autorizzazione [!UICONTROL Gestione chiave gestita dal cliente] può abilitare la CMK per la propria organizzazione.

Per ulteriori informazioni sull&#39;assegnazione di ruoli e autorizzazioni in Experience Platform, consulta la [documentazione sulla configurazione delle autorizzazioni](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

Per abilitare CMK, l&#39;insieme di credenziali delle chiavi [[!DNL Azure] deve essere configurato](./azure-key-vault-config.md) con le impostazioni seguenti:

* [Abilita protezione eliminazione](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [Abilita eliminazione temporanea](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [Configurare l&#39;accesso utilizzando [!DNL Azure] il controllo dell&#39;accesso basato su ruolo](https://learn.microsoft.com/en-us/azure/role-based-access-control/)
* [Configura un insieme di credenziali delle chiavi  [!DNL Azure] ](./azure-key-vault-config.md)

## Configurare l’app CMK {#register-app}

Dopo aver configurato l&#39;insieme di credenziali delle chiavi, il passaggio successivo consiste nel registrarsi per l&#39;applicazione CMK che verrà collegata al tenant [!DNL Azure].

### Introduzione

La registrazione dell’app CMK richiede di effettuare chiamate alle API di Platform. Per informazioni dettagliate su come raccogliere le intestazioni di autenticazione necessarie per effettuare queste chiamate, consulta la [Guida all&#39;autenticazione API di Platform](../../api-authentication.md).

Mentre la guida all&#39;autenticazione fornisce istruzioni su come generare un valore univoco per l&#39;intestazione richiesta `x-api-key` richiesta richiesta, tutte le operazioni API in questa guida utilizzano il valore statico `acp_provisioning`. È comunque necessario fornire valori personalizzati per `{ACCESS_TOKEN}` e `{ORG_ID}`.

In tutte le chiamate API mostrate in questa guida, `platform.adobe.io` viene utilizzato come percorso principale, che per impostazione predefinita corrisponde all&#39;area VA7. Se l&#39;organizzazione utilizza un&#39;area geografica diversa, `platform` deve essere seguito da un trattino e il codice di area deve essere assegnato all&#39;organizzazione: `nld2` per NLD2 o `aus5` per AUS5 (ad esempio: `platform-aus5.adobe.io`). Se non conosci l’area geografica della tua organizzazione, contatta l’amministratore di sistema.

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

In caso di esito positivo, la risposta restituisce una proprietà `applicationRedirectUrl`, contenente l’URL di autenticazione.

```json
{
    "id": "byok",
    "name": "acpebae9422Caepcmkmultitenantapp",
    "applicationUri": "https://adobe.com/acpebae9422Caepcmkmultitenantapp",
    "applicationId": "e463a445-c6ac-4ca2-b36a-b5146fcf6a52",
    "applicationRedirectUrl": "https://login.microsoftonline.com/common/oauth2/authorize?response_type=code&client_id=e463a445-c6ac-4ca2-b36a-b5146fcf6a52&redirect_uri=https://adobe.com/acpebae9422Caepcmkmultitenantapp&scope=user.read"
}
```

Copiare e incollare l&#39;indirizzo `applicationRedirectUrl` in un browser per aprire una finestra di dialogo di autenticazione. Selezionare **[!DNL Accept]** per aggiungere l&#39;entità servizio app CMK al tenant [!DNL Azure].

![Finestra di dialogo per la richiesta di autorizzazione di Microsoft con [!UICONTROL Accept] evidenziato.](../../images/governance-privacy-security/customer-managed-keys/app-permission.png)

### Assegnare l&#39;app CMK a un ruolo {#assign-to-role}

Dopo aver completato il processo di autenticazione, torna all&#39;insieme di credenziali delle chiavi [!DNL Azure] e seleziona **[!DNL Access control]** nell&#39;area di navigazione a sinistra. Da qui, seleziona **[!DNL Add]** seguito da **[!DNL Add role assignment]**.

![Dashboard di Microsoft Azure con [!DNL Add] e [!DNL Add role assignment] evidenziati.](../../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

Nella schermata successiva viene richiesto di scegliere un ruolo per l&#39;assegnazione. Selezionare **[!DNL Key Vault Crypto Service Encryption User]** prima di selezionare **[!DNL Next]** per continuare.

>[!NOTE]
>
>Se si dispone del livello [!DNL Managed-HSM Key Vault], è necessario selezionare il ruolo utente **[!DNL Managed HSM Crypto Service Encryption User]**.

![Dashboard di Microsoft Azure con [!DNL Key Vault Crypto Service Encryption User] evidenziato.](../../images/governance-privacy-security/customer-managed-keys/select-role.png)

Nella schermata successiva, scegli **[!DNL Select members]** per aprire una finestra di dialogo nella barra a destra. Utilizzare la barra di ricerca per individuare l&#39;entità servizio per l&#39;applicazione CMK e selezionarla dall&#39;elenco. Al termine, selezionare **[!DNL Save]**.

>[!NOTE]
>
>Se l&#39;applicazione non è presente nell&#39;elenco, l&#39;entità servizio non è stata accettata nel tenant. Per assicurarsi di disporre dei privilegi corretti, rivolgersi all&#39;amministratore o al rappresentante [!DNL Azure].

## Abilita la configurazione della chiave di crittografia su Experience Platform {#send-to-adobe}

Dopo aver installato l&#39;app CMK in [!DNL Azure], puoi inviare l&#39;identificatore della chiave di crittografia ad Adobe. Selezionare **[!DNL Keys]** nel menu di navigazione a sinistra, seguito dal nome della chiave che si desidera inviare.

![Dashboard di Microsoft Azure con l&#39;oggetto [!DNL Keys] e il nome della chiave evidenziato.](../../images/governance-privacy-security/customer-managed-keys/select-key.png)

Seleziona la versione più recente della chiave e viene visualizzata la pagina dei relativi dettagli. Da qui, puoi facoltativamente configurare le operazioni consentite per la chiave.

>[!IMPORTANT]
>
>Le operazioni minime richieste per la chiave sono le autorizzazioni **[!DNL Wrap Key]** e **[!DNL Unwrap Key]**. Puoi includere [!DNL Encrypt], [!DNL Decrypt], [!DNL Sign] e [!DNL Verify] nel caso lo desideri.

Nel campo **[!UICONTROL Identificatore chiave]** viene visualizzato l&#39;identificatore URI della chiave. Copia questo valore URI da utilizzare nel passaggio successivo.

![Dettagli della chiave del dashboard di Microsoft Azure con le sezioni [!DNL Permitted operations] e Copia URL chiave evidenziate.](../../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

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
| `name` | Un nome per la configurazione. Assicurati di ricordare questo valore in quanto è necessario per controllare lo stato della configurazione in un [passaggio successivo](#check-status). Il valore distingue tra maiuscole e minuscole. |
| `type` | Il tipo di configurazione. Deve essere impostato su `BYOK_CONFIG`. |
| `imsOrgId` | ID organizzazione. Questo ID deve essere lo stesso valore fornito nell&#39;intestazione `x-gw-ims-org-id`. |
| `configData` | Questa proprietà contiene i seguenti dettagli sulla configurazione:<ul><li>`providerType`: deve essere impostato su `AZURE_KEYVAULT`.</li><li>`keyVaultKeyIdentifier`: URI dell&#39;insieme di credenziali delle chiavi copiato [prima](#send-to-adobe).</li></ul> |

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

Aggiungere `name` della configurazione da controllare al percorso (`config1` nell&#39;esempio seguente) e includere un parametro di query `configType` impostato su `BYOK_CONFIG`.

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

L&#39;attributo `status` può avere uno dei quattro valori con i seguenti significati:

1. `RUNNING`: verifica che Platform possa accedere all&#39;insieme di credenziali chiave e chiave.
1. `UPDATE_EXISTING_RESOURCES`: il sistema sta aggiungendo l&#39;insieme di credenziali e il nome della chiave agli archivi dati in tutte le sandbox dell&#39;organizzazione.
1. `COMPLETED`: l&#39;insieme di credenziali delle chiavi e il nome della chiave sono stati aggiunti agli archivi dati.
1. `FAILED`: si è verificato un problema, principalmente relativo alla chiave, all&#39;insieme di credenziali delle chiavi o alla configurazione di app multi-tenant.

## Passaggi successivi

Completando i passaggi precedenti, hai abilitato correttamente la CMK per la tua organizzazione. I dati acquisiti negli archivi dati primari verranno ora crittografati e decrittografati utilizzando le chiavi nell&#39;insieme di credenziali delle chiavi [!DNL Azure]. Per ulteriori informazioni sulla crittografia dei dati in Adobe Experience Platform, consulta la [documentazione sulla crittografia](../encryption.md).
