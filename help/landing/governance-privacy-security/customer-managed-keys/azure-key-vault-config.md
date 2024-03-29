---
title: Configurare un archivio chiavi di Azure
description: Scopri come creare un nuovo account Enterprise con Azure o utilizzare un account Enterprise esistente e creare l’insieme di credenziali delle chiavi.
exl-id: 670e3ca3-a833-4b28-9ad4-73685fa5d74d
source-git-commit: 4f08e8fcc8d53b981af60226f1397a1d1ac4d8dc
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# Configurare un [!DNL Azure] Key Vault

Le chiavi gestite dal cliente (CMK) supportano solo le chiavi di un [!DNL Microsoft Azure] Key Vault Per iniziare, devi lavorare con [!DNL Azure] per creare un nuovo account aziendale o utilizzare un account aziendale esistente e seguire i passaggi riportati di seguito per creare l&#39;insieme di credenziali delle chiavi.

>[!IMPORTANT]
>
>Solo i livelli HSM Standard, Premium e Managed per [!DNL Azure] Sono supportati Key Vault. [!DNL Azure Dedicated HSM] e [!DNL Azure Payments HSM] non sono supportati. Consulta la sezione [[!DNL Azure] documentazione](https://learn.microsoft.com/en-us/azure/security/fundamentals/key-management#azure-key-management-services) per ulteriori informazioni sui servizi di gestione delle chiavi offerti.

>[!NOTE]
>
>La documentazione seguente descrive solo i passaggi di base per creare l’insieme di credenziali delle chiavi. Al di fuori di questa guida, devi configurare l’insieme di credenziali delle chiavi in base ai criteri della tua organizzazione.

Accedi a [!DNL Azure] e utilizza la barra di ricerca per individuare **[!DNL Key vaults]** nell’elenco dei servizi.

![La funzione di ricerca in [!DNL Microsoft Azure] con [!DNL Key vaults] nei risultati della ricerca.](../../images/governance-privacy-security/customer-managed-keys/access-key-vaults.png)

Il **[!DNL Key vaults]** dopo aver selezionato il servizio. Da qui, seleziona **[!DNL Create]**.

![Il [!DNL Key vaults] dashboard in [!DNL Microsoft Azure] con [!DNL Create] evidenziato.](../../images/governance-privacy-security/customer-managed-keys/create-key-vault.png)

Utilizzando il modulo fornito, compila i dettagli di base per l’insieme di credenziali delle chiavi, incluso un nome e un gruppo di risorse assegnato.

>[!WARNING]
>
>Anche se la maggior parte delle opzioni può essere lasciata come valori predefiniti, **assicurarsi di attivare le opzioni di protezione eliminazione temporanea e rimozione temporanea**. Se non attivi queste funzioni, potresti rischiare di perdere l’accesso ai dati se l’insieme di credenziali delle chiavi viene eliminato.
>
>![Il [!DNL Microsoft Azure] [!DNL Create a Key Vault] flusso di lavoro con protezione eliminazione temporanea ed eliminazione evidenziata.](../../images/governance-privacy-security/customer-managed-keys/basic-config.png)

Da qui, continua a seguire il flusso di lavoro di creazione dell’insieme di credenziali delle chiavi e configura le diverse opzioni in base ai criteri della tua organizzazione.

Una volta raggiunto il **[!DNL Review + create]** passaggio, puoi rivedere i dettagli dell’insieme di credenziali delle chiavi durante la convalida. Al termine della convalida, seleziona **[!DNL Create]** per completare il processo.

![La pagina Revisione e creazione degli archivi chiavi di Microsoft Azure è evidenziata dall&#39;opzione Crea.](../../images/governance-privacy-security/customer-managed-keys/finish-creation.png)

## Configurare l’accesso {#configure-access}

Quindi, abilita il controllo degli accessi basato sul ruolo di Azure per l’insieme di credenziali delle chiavi. Seleziona **[!DNL Access configuration]** nel [!DNL Settings] nella sezione di navigazione a sinistra, quindi seleziona **[!DNL Azure role-based access control]** per attivare l&#39;impostazione. Questo passaggio è essenziale in quanto l’app CMK deve essere associata in seguito a un ruolo Azure. L’assegnazione di un ruolo è documentata in entrambi [API](./api-set-up.md#assign-to-role) e [UI](./ui-set-up.md#assign-to-role) flussi di lavoro.

![Il [!DNL Microsoft Azure] dashboard con [!DNL Access configuration] e [!DNL Azure role-based access control] evidenziato.](../../images/governance-privacy-security/customer-managed-keys/access-configuration.png)

## Configurare le opzioni di rete {#configure-network-options}

Se l&#39;insieme di credenziali delle chiavi è configurato per limitare l&#39;accesso pubblico a determinate reti virtuali o disabilitare completamente l&#39;accesso pubblico, è necessario concedere [!DNL Microsoft] un&#39;eccezione firewall.

Seleziona **[!DNL Networking]** nel menu di navigazione a sinistra. Sotto **[!DNL Firewalls and virtual networks]**, seleziona la casella di controllo **[!DNL Allow trusted Microsoft services to bypass this firewall]**, quindi seleziona **[!DNL Apply]**.

![Il [!DNL Networking] scheda di [!DNL Microsoft Azure] con [!DNL Networking] e [!DNL Allow trusted Microsoft surfaces to bypass this firewall] eccezione evidenziata.](../../images/governance-privacy-security/customer-managed-keys/networking.png)

### Generare una chiave {#generate-a-key}

Dopo aver creato un Key Vault, puoi generare una nuova chiave. Accedi a **[!DNL Keys]** e seleziona **[!DNL Generate/Import]**.

![Il [!DNL Keys] scheda di [!DNL Azure] con [!DNL Generate import] evidenziato.](../../images/governance-privacy-security/customer-managed-keys/view-keys.png)

Utilizza il modulo fornito per fornire un nome per la chiave e seleziona una delle seguenti opzioni **RSA** o **RSA-HSM** per il tipo di chiave. Come minimo, il **[!DNL RSA key size]** deve essere almeno **3072** bit come richiesto da [!DNL Cosmos DB]. [!DNL Azure Data Lake Storage] è compatibile anche con RSA 3027.

>[!NOTE]
>
>Ricorda il nome fornito per la chiave, in quanto è necessario per inviarla all’Adobe.

Utilizzare i controlli rimanenti per configurare la chiave che si desidera generare o importare in base alle proprie esigenze. Al termine, seleziona **[!DNL Create]**.

![Il [!DNL Create a key] dashboard con [!DNL 3072] bit evidenziati.](../../images/governance-privacy-security/customer-managed-keys/configure-key.png)

La chiave configurata viene visualizzata nell&#39;elenco delle chiavi per l&#39;archivio.

![Il [!DNL Keys] area di lavoro con il nome chiave evidenziato.](../../images/governance-privacy-security/customer-managed-keys/key-added.png)

## Passaggi successivi

Per continuare il processo una tantum per l&#39;impostazione della funzionalità delle chiavi gestite dal cliente, continuare con [API](./api-set-up.md) o [UI](./ui-set-up.md) guide alla configurazione delle chiavi gestite dal cliente.
