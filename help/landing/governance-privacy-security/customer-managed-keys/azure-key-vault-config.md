---
title: Configurare un archivio chiavi di Azure
description: Scopri come creare un nuovo account Enterprise con Azure o utilizzare un account Enterprise esistente e creare l’insieme di credenziali delle chiavi.
role: Developer
feature: Privacy
exl-id: 670e3ca3-a833-4b28-9ad4-73685fa5d74d
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# Configurare un insieme di credenziali delle chiavi [!DNL Azure]

Le chiavi gestite dal cliente (CMK) supportano solo le chiavi di un insieme di credenziali delle chiavi [!DNL Microsoft Azure]. Per iniziare, devi lavorare con [!DNL Azure] per creare un nuovo account Enterprise oppure utilizzare un account Enterprise esistente e seguire i passaggi riportati di seguito per creare l&#39;insieme di credenziali delle chiavi.

>[!IMPORTANT]
>
>Sono supportati solo i livelli HSM Standard, Premium e Managed per l&#39;insieme di credenziali delle chiavi [!DNL Azure]. [!DNL Azure Dedicated HSM] e [!DNL Azure Payments HSM] non sono supportati. Per ulteriori informazioni sui servizi di gestione delle chiavi offerti, consulta la [[!DNL Azure] documentazione](https://learn.microsoft.com/en-us/azure/security/fundamentals/key-management#azure-key-management-services).

>[!NOTE]
>
>La documentazione seguente descrive solo i passaggi di base per creare l’insieme di credenziali delle chiavi. Al di fuori di questa guida, devi configurare l’insieme di credenziali delle chiavi in base ai criteri della tua organizzazione.

Accedere al portale [!DNL Azure] e utilizzare la barra di ricerca per individuare **[!DNL Key vaults]** nell&#39;elenco dei servizi.

![Caratteristica di ricerca in [!DNL Microsoft Azure] con [!DNL Key vaults] evidenziata nei risultati di ricerca.](../../images/governance-privacy-security/customer-managed-keys/access-key-vaults.png)

La pagina **[!DNL Key vaults]** viene visualizzata dopo aver selezionato il servizio. Da qui, seleziona **[!DNL Create]**.

![Dashboard [!DNL Key vaults] in [!DNL Microsoft Azure] con [!DNL Create] evidenziato.](../../images/governance-privacy-security/customer-managed-keys/create-key-vault.png)

Utilizzando il modulo fornito, compila i dettagli di base per l’insieme di credenziali delle chiavi, incluso un nome e un gruppo di risorse assegnato.

>[!WARNING]
>
>Anche se la maggior parte delle opzioni può essere lasciata come valori predefiniti, **assicurati di abilitare le opzioni di protezione eliminazione temporanea ed eliminazione**. Se non attivi queste funzioni, potresti rischiare di perdere l’accesso ai dati se l’insieme di credenziali delle chiavi viene eliminato.
>
>![Il flusso di lavoro [!DNL Microsoft Azure] [!DNL Create a Key Vault] con protezione eliminazione temporanea evidenziata.](../../images/governance-privacy-security/customer-managed-keys/basic-config.png)

Da qui, continua a seguire il flusso di lavoro di creazione dell’insieme di credenziali delle chiavi e configura le diverse opzioni in base ai criteri della tua organizzazione.

Una volta raggiunto il passaggio **[!DNL Review + create]**, è possibile rivedere i dettagli dell&#39;insieme di credenziali delle chiavi durante la convalida. Al termine della convalida, selezionare **[!DNL Create]** per completare il processo.

![Gli archivi chiavi di Microsoft Azure esaminano e creano la pagina con l&#39;opzione Crea evidenziata.](../../images/governance-privacy-security/customer-managed-keys/finish-creation.png)

## Configurare l’accesso {#configure-access}

Quindi, abilita il controllo degli accessi basato sul ruolo di Azure per l’insieme di credenziali delle chiavi. Seleziona **[!DNL Access configuration]** nella sezione [!DNL Settings] della navigazione a sinistra, quindi seleziona **[!DNL Azure role-based access control]** per abilitare l&#39;impostazione. Questo passaggio è essenziale in quanto l’app CMK deve essere associata in seguito a un ruolo Azure. L&#39;assegnazione di un ruolo è documentata nei flussi di lavoro [API](./api-set-up.md#assign-to-role) e [UI](./ui-set-up.md#assign-to-role).

![Dashboard [!DNL Microsoft Azure] con [!DNL Access configuration] e [!DNL Azure role-based access control] evidenziati.](../../images/governance-privacy-security/customer-managed-keys/access-configuration.png)

## Configurare le opzioni di rete {#configure-network-options}

Se l&#39;insieme di credenziali delle chiavi è configurato per limitare l&#39;accesso pubblico a determinate reti virtuali o disabilitare completamente l&#39;accesso pubblico, è necessario concedere a [!DNL Microsoft] un&#39;eccezione firewall.

Selezionare **[!DNL Networking]** nel menu di navigazione a sinistra. In **[!DNL Firewalls and virtual networks]**, selezionare la casella di controllo **[!DNL Allow trusted Microsoft services to bypass this firewall]**, quindi selezionare **[!DNL Apply]**.

![Scheda [!DNL Networking] di [!DNL Microsoft Azure] con [!DNL Networking] e [!DNL Allow trusted Microsoft surfaces to bypass this firewall] eccezione evidenziata.](../../images/governance-privacy-security/customer-managed-keys/networking.png)

### Generare una chiave {#generate-a-key}

Dopo aver creato un Key Vault, puoi generare una nuova chiave. Passare alla scheda **[!DNL Keys]** e selezionare **[!DNL Generate/Import]**.

![Scheda [!DNL Keys] di [!DNL Azure] con [!DNL Generate import] evidenziato.](../../images/governance-privacy-security/customer-managed-keys/view-keys.png)

Utilizza il modulo fornito per fornire un nome per la chiave e seleziona **RSA** o **RSA-HSM** per il tipo di chiave. Come minimo, **[!DNL RSA key size]** deve essere di almeno **3072** bit come richiesto da [!DNL Cosmos DB]. [!DNL Azure Data Lake Storage] è compatibile anche con RSA 3027.

>[!NOTE]
>
>Ricorda il nome fornito per la chiave, in quanto è necessario per inviarla ad Adobe.

Utilizzare i controlli rimanenti per configurare la chiave che si desidera generare o importare in base alle proprie esigenze. Al termine, selezionare **[!DNL Create]**.

![Dashboard [!DNL Create a key] con [!DNL 3072] bit evidenziati.](../../images/governance-privacy-security/customer-managed-keys/configure-key.png)

La chiave configurata viene visualizzata nell&#39;elenco delle chiavi per l&#39;archivio.

![Area di lavoro [!DNL Keys] con il nome chiave evidenziato.](../../images/governance-privacy-security/customer-managed-keys/key-added.png)

## Passaggi successivi

Per continuare il processo di configurazione delle chiavi gestite dal cliente una tantum, continuare con le guide di installazione delle chiavi gestite dal cliente [API](./api-set-up.md) o [UI](./ui-set-up.md).
