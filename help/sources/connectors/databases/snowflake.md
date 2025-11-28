---
title: Panoramica di Snowflake Source Connector
description: Scopri come collegare Snowflake a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: df066463-1ae6-4ecd-ae0e-fb291cec4bd5
source-git-commit: 687363ab664e43cc854b535760dfbfc55acefd2c
workflow-type: tm+mt
source-wordcount: '1570'
ht-degree: 2%

---

# Origine [!DNL Snowflake]

>[!IMPORTANT]
>
>* L&#39;origine [!DNL Snowflake] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-Time Customer Data Platform Ultimate.
>* Per impostazione predefinita, l&#39;origine [!DNL Snowflake] interpreta `null` come una stringa vuota. Contatta il tuo rappresentante Adobe per assicurarti che i valori `null` siano scritti correttamente come `null` in Adobe Experience Platform.
>* Affinché Experience Platform possa acquisire i dati, i fusi orari per tutte le origini batch basate su tabelle devono essere configurati in formato UTC. L&#39;unico indicatore orario supportato per l&#39;origine [!DNL Snowflake] è TIMESTAMP_NTZ con ora UTC.

[!DNL Snowflake] è una piattaforma di data warehouse basata su cloud progettata per consentire alle organizzazioni di archiviare, elaborare e analizzare grandi volumi di dati in modo efficiente. Progettato per sfruttare la scalabilità e la flessibilità del cloud, [!DNL Snowflake] supporta l&#39;integrazione dei dati, l&#39;analisi avanzata e la condivisione senza soluzione di continuità tra i team. In qualità di servizio completamente gestito, [!DNL Snowflake] elimina le complessità di manutenzione comuni ai database tradizionali, consentendo di concentrarsi su informazioni approfondite e valore dai dati.

È possibile utilizzare l&#39;origine [!DNL Snowflake] per connettersi e trasferire i dati da [!DNL Snowflake] a Adobe Experience Platform. Leggi la documentazione seguente per scoprire come configurare l&#39;origine [!DNL Snowflake] e connettersi ad Experience Platform.

## Prerequisiti {#prerequisites}

Questa sezione descrive le attività di installazione che è necessario completare prima di poter connettere l&#39;origine [!DNL Snowflake] ad Experience Platform.

### Indirizzo IP inserisco nell&#39;elenco Consentiti

Prima di collegare le origini a Experience Platform, è necessario aggiungere al elenco Consentiti di indirizzi IP specifici per l’area geografica. Per ulteriori informazioni, leggere la guida in [inserire nell&#39;elenco Consentiti degli indirizzi IP per la connessione ad Experience Platform](../../ip-address-allow-list.md).

### Raccogli le credenziali richieste

Per autenticare l&#39;origine [!DNL Snowflake], è necessario fornire i valori per le seguenti proprietà delle credenziali.

>[!BEGINTABS]

>[!TAB Autenticazione chiave account (Azure)]

Specificare i valori per le credenziali seguenti per connettere [!DNL Snowflake] ad Experience Platform in Azure utilizzando l&#39;autenticazione della chiave dell&#39;account.

| Credenziali | Descrizione |
| ---------- | ----------- |
| `account` | Un nome di account identifica in modo univoco un account all’interno dell’organizzazione. In questo caso, è necessario identificare in modo univoco un account tra diverse [!DNL Snowflake] organizzazioni. A questo scopo, devi anteporre il nome della tua organizzazione al nome dell’account. Esempio: `myorg-myaccount.snowflakecomputing.com`. Leggi la sezione sul [recupero dell&#39;identificatore dell&#39;account [!DNL Snowflake] &#x200B;](#retrieve-your-account-identifier) per ulteriori informazioni. Per ulteriori informazioni, consulta la [[!DNL Snowflake] documentazione](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `warehouse` | Il data warehouse [!DNL Snowflake] gestisce il processo di esecuzione delle query per l&#39;applicazione. Ogni data warehouse [!DNL Snowflake] è indipendente l&#39;uno dall&#39;altro e deve essere accessibile singolarmente quando si trasferiscono i dati ad Experience Platform. |
| `database` | Il database [!DNL Snowflake] contiene i dati che si desidera inserire nell&#39;Experience Platform. |
| `username` | Nome utente per l&#39;account [!DNL Snowflake]. |
| `password` | Password per l&#39;account utente [!DNL Snowflake]. |
| `role` | Ruolo di controllo di accesso predefinito da utilizzare nella sessione [!DNL Snowflake]. Il ruolo deve essere esistente e già assegnato all&#39;utente specificato. Il ruolo predefinito è `PUBLIC`. |
| `connectionString` | Stringa di connessione utilizzata per connettersi all&#39;istanza [!DNL Snowflake]. Il modello di stringa di connessione per [!DNL Snowflake] è `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |

>[!TAB Autenticazione coppia di chiavi (Azure)]

Per utilizzare l&#39;autenticazione con coppia di chiavi, generare innanzitutto una coppia di chiavi RSA a 2048 bit. Quindi, fornisci i valori per le seguenti credenziali per connettersi ad Experience Platform su Azure utilizzando l’autenticazione con coppia di chiavi.

| Credenziali | Descrizione |
| --- | --- |
| `account` | Un nome di account identifica in modo univoco un account all’interno dell’organizzazione. In questo caso, è necessario identificare in modo univoco un account tra diverse [!DNL Snowflake] organizzazioni. A questo scopo, devi anteporre il nome della tua organizzazione al nome dell’account. Esempio: `myorg-myaccount.snowflakecomputing.com`. Leggi la sezione sul [recupero dell&#39;identificatore dell&#39;account [!DNL Snowflake] &#x200B;](#retrieve-your-account-identifier) per ulteriori informazioni. Per ulteriori informazioni, consulta la [[!DNL Snowflake] documentazione](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | Il nome utente dell&#39;account [!DNL Snowflake]. |
| `privateKey` | La chiave privata con codifica [!DNL Base64-] del tuo account [!DNL Snowflake]. Puoi generare chiavi private crittografate o non crittografate. Se utilizzi una chiave privata crittografata, devi fornire anche una passphrase di chiave privata durante l’autenticazione in Experience Platform. Leggi la sezione sul [recupero della chiave privata](#retrieve-your-private-key) per ulteriori informazioni. |
| `privateKeyPassphrase` | La passphrase per chiave privata è un ulteriore livello di sicurezza da utilizzare per l&#39;autenticazione con una chiave privata crittografata. Se si utilizza una chiave privata non crittografata, non è necessario fornire la passphrase. |
| `port` | Numero di porta utilizzato da [!DNL Snowflake] per la connessione a un server tramite Internet. |
| `database` | Il database [!DNL Snowflake] che contiene i dati da acquisire in Experience Platform. |
| `warehouse` | Il data warehouse [!DNL Snowflake] gestisce il processo di esecuzione delle query per l&#39;applicazione. Ogni data warehouse [!DNL Snowflake] è indipendente l&#39;uno dall&#39;altro e deve essere accessibile singolarmente quando si trasferiscono i dati ad Experience Platform. |

Per ulteriori informazioni su questi valori, fare riferimento alla [[!DNL Snowflake] guida all&#39;autenticazione con coppia di chiavi](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!TAB Autenticazione di base (AWS)]

Specificare i valori per le credenziali seguenti per connettere [!DNL Snowflake] ad Experience Platform su AWS utilizzando l&#39;autenticazione di base.

>[!WARNING]
>
>L&#39;autenticazione di base (o l&#39;autenticazione della chiave dell&#39;account) per l&#39;origine [!DNL Snowflake] diventerà obsoleta a novembre 2025. Devi passare all’autenticazione basata su coppia di chiavi per continuare a utilizzare l’origine e ad acquisire i dati dal database ad Experience Platform. Per ulteriori informazioni sulla deprecazione, leggere la [[!DNL Snowflake] guida alle best practice per ridurre i rischi di compromissione delle credenziali](https://www.snowflake.com/en/resources/white-paper/best-practices-to-mitigate-the-risk-of-credential-compromise/).

| Credenziali | Descrizione |
| --- | --- |
| `host` | L&#39;URL host al quale il tuo account [!DNL Snowflake] si connette. |
| `port` | Numero di porta utilizzato da [!DNL Snowflake] per la connessione a un server tramite Internet. |
| `username` | Il nome utente associato al tuo account [!DNL Snowflake]. |
| `password` | La password associata al tuo account [!DNL Snowflake]. |
| `database` | Il database [!DNL Snowflake] da cui verranno estratti i dati. |
| `schema` | Il nome dello schema associato al database [!DNL Snowflake]. È necessario assicurarsi che anche l&#39;utente a cui si desidera concedere l&#39;accesso al database abbia accesso a questo schema. |
| `warehouse` | Il data warehouse [!DNL Snowflake] in uso. |

>[!TAB Autenticazione coppia di chiavi (AWS)]

Per utilizzare l&#39;autenticazione con coppia di chiavi, generare innanzitutto una coppia di chiavi RSA a 2048 bit. Quindi, fornisci i valori per le seguenti credenziali per connettersi ad Experience Platform su AWS utilizzando l’autenticazione con coppia di chiavi.

| Credenziali | Descrizione |
| --- | --- |
| `account` | Un nome di account identifica in modo univoco un account all’interno dell’organizzazione. In questo caso, è necessario identificare in modo univoco un account tra diverse [!DNL Snowflake] organizzazioni. A questo scopo, devi anteporre il nome della tua organizzazione al nome dell’account. Esempio: `http://myorg-myaccount.snowflakecomputing.com/`. Per ulteriori informazioni, consulta la guida in [recupero dell&#39;identificatore dell&#39;account [!DNL Snowflake] &#x200B;](#etrieve-your-account-identifier). Per ulteriori informazioni, consulta la [[!DNL Snowflake] documentazione](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | Il nome utente dell&#39;account [!DNL Snowflake]. |
| `privateKey` | Chiave privata per l&#39;utente [!DNL Snowflake], con codifica base64 come una singola riga senza intestazioni o interruzioni di riga. Per prepararlo, copiare il contenuto del file PEM, rimuovere le righe `BEGIN`/`END` e tutte le interruzioni di riga, quindi codificare il risultato in base64. Leggi la sezione sul [recupero della chiave privata](#retrieve-your-private-key) per ulteriori informazioni. **Nota:** le chiavi private crittografate non sono attualmente supportate per una connessione AWS. |
| `port` | Numero di porta utilizzato da [!DNL Snowflake] per la connessione a un server tramite Internet. |
| `database` | Il database [!DNL Snowflake] che contiene i dati da acquisire in Experience Platform. |
| `warehouse` | Il data warehouse [!DNL Snowflake] gestisce il processo di esecuzione delle query per l&#39;applicazione. Ogni data warehouse [!DNL Snowflake] è indipendente l&#39;uno dall&#39;altro e deve essere accessibile singolarmente quando si trasferiscono i dati ad Experience Platform. |

Per ulteriori informazioni su questi valori, fare riferimento alla [[!DNL Snowflake] guida all&#39;autenticazione con coppia di chiavi](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

### Recupera l’identificatore dell’account {#retrieve-your-account-identifier}

È necessario recuperare l&#39;identificatore dell&#39;account dal dashboard dell&#39;interfaccia utente di [!DNL Snowflake], poiché verrà utilizzato per autenticare l&#39;istanza di [!DNL Snowflake] in Experience Platform.

Per recuperare l’identificatore dell’account:

* Utilizza il [[!DNL Snowflake] dashboard dell&#39;interfaccia utente dell&#39;applicazione](https://app.snowflake.com/) per accedere al tuo account.
* Nel menu di navigazione a sinistra, seleziona **[!DNL Accounts]**, quindi seleziona **[!DNL Active Accounts]** dall&#39;intestazione.
* Quindi, seleziona l’icona delle informazioni, quindi fai clic sul nome di dominio dell’URL corrente e copialo.

![Dashboard dell&#39;interfaccia utente di Snowflake con il nome di dominio selezionato.](../../images/tutorials/create/snowflake/snowflake-dashboard.png)

### Generare la coppia di chiavi RSA

Utilizza OpenSSL nell’interfaccia della riga di comando per generare una coppia di chiavi RSA a 2048 bit in formato PKCS#8. È consigliabile creare una chiave privata crittografata per la sicurezza, che richiederà una passphrase.

>[!BEGINTABS]

>[!TAB Generare una chiave privata crittografata]

Per generare la chiave privata [!DNL Snowflake] crittografata, eseguire il comando seguente sul terminale:

```bash
openssl genrsa 2048 | openssl pkcs8 -topk8 -v2 des3 -inform PEM -out rsa_key.p8# You will be prompted to enter a passphrase. Store this securely!
```

>[!TAB Generare una chiave privata non crittografata]

Per generare la chiave privata [!DNL Snowflake] non crittografata, eseguire il comando seguente sul terminale:

```bash
openssl genrsa 2048 | openssl pkcs8 -topk8 -inform PEM -out rsa_key.p8 -nocrypt
```

>[!ENDTABS]

### Generare una chiave pubblica dalla chiave privata

Quindi, esegui il comando seguente nell’interfaccia della riga di comando per creare una chiave pubblica basata sulla chiave privata.

```bash
openssl rsa -in rsa_key.p8 -pubout -out rsa_key.pub# You will be prompted to enter the passphrase if the private key is encrypted.
```

### Assegna la chiave pubblica all&#39;utente [!DNL Snowflake]

È necessario utilizzare un ruolo di amministratore [!DNL Snowflake] (come **SECURITYADMIN**) per associare la chiave pubblica generata all&#39;utente del servizio [!DNL Snowflake] che Experience Platform utilizzerà. Per recuperare il contenuto della chiave pubblica, aprire il file `rsa_key.pub` e copiare l&#39;intero contenuto, escluse le righe `-----BEGIN PUBLIC KEY----- and -----END PUBLIC KEY-----`. Eseguire quindi le istruzioni SQL seguenti in [!DNL Snowflake]:

```sql
ALTER USER {YOUR_SNOWFLAKE_USERNAME}>SET RSA_PUBLIC_KEY='{PUBLIC_KEY_CONTENT}';
```

### Codifica la chiave privata in [!DNL Base64]

Experience Platform richiede che la chiave privata sia codificata con [!DNL Base64] e fornita come stringa durante la configurazione della connessione. Utilizzare uno strumento o uno script appropriato per codificare il contenuto del file `rsa_key.p8` in una singola stringa [!DNL Base64].

>[!TIP]
>
>Verificare che non siano presenti spazi o interruzioni di riga aggiuntivi, incluse le righe di intestazione/piè di pagina `(-----BEGIN ENCRYPTED PRIVATE KEY----- and -----END ENCRYPTED PRIVATE KEY-----)`, prima o dopo il processo di codifica, in quanto ciò potrebbe causare errori di autenticazione.

### Verifica configurazioni

Prima di creare la connessione di origine [!DNL Snowflake] in Experience Platform, è necessario assicurarsi che **[!DNL Default Role]** e **[!DNL Default Warehouse]** dell&#39;utente corrispondano ai valori forniti in Experience Platform. È possibile verificare queste impostazioni nell&#39;interfaccia utente di [!DNL Snowflake] utilizzando il comando SQL `DESCRIBE USER {USERNAME}`.

In alternativa, puoi seguire i passaggi riportati di seguito per verificare le impostazioni:

* Selezionare **[!DNL Admin]** nel menu di navigazione a sinistra, quindi selezionare **[!DNL Users & Roles]**.
* Selezionare l&#39;utente appropriato, quindi selezionare i puntini di sospensione (`...`) nell&#39;angolo superiore destro.
* Nella finestra [!DNL Edit user] visualizzata, passa a [!DNL Default Role] per visualizzare il ruolo associato all&#39;utente specificato.
* Nella stessa finestra passare a [!DNL Default Warehouse] per visualizzare il magazzino associato all&#39;utente specificato.

![Interfaccia utente di Snowflake in cui è possibile verificare il proprio ruolo e il proprio data warehouse.](../../images/tutorials/create/snowflake/snowflake-configs.png)

## Passaggi successivi

Al termine dell&#39;installazione, è possibile procedere con la connessione dell&#39;account [!DNL Snowflake] ad Experience Platform. Per ulteriori informazioni, consulta la documentazione seguente:

### Connetti [!DNL Snowflake] ad Experience Platform tramite API

* [Connetti [!DNL Snowflake] ad Experience Platform utilizzando l&#39;API](../../tutorials/api/create/databases/snowflake.md)
* [Esplorare le tabelle di dati utilizzando l’API del servizio Flusso](../../tutorials/api/explore/tabular.md)
* [Creare un flusso di dati per un’origine di database utilizzando l’API del servizio Flusso](../../tutorials/api/collect/database-nosql.md)

### Connetti [!DNL Snowflake] ad Experience Platform tramite l&#39;interfaccia utente

* [Connetti [!DNL Snowflake] ad Experience Platform tramite l&#39;interfaccia utente](../../tutorials/ui/create/databases/snowflake.md)
* [Creare un flusso di dati per una connessione di origine al database nell’interfaccia utente](../../tutorials/ui/dataflow/databases.md)
