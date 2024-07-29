---
title: Panoramica del connettore Source di Snowflake
description: Scopri come collegare il Snowflake a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: df066463-1ae6-4ecd-ae0e-fb291cec4bd5
source-git-commit: 8d6baef1549498e137d336ac2c8a42428496dedf
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---

# Origine [!DNL Snowflake]

>[!IMPORTANT]
>
>* L&#39;origine [!DNL Snowflake] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-time Customer Data Platform Ultimate.
>* Per impostazione predefinita, l&#39;origine [!DNL Snowflake] interpreta `null` come una stringa vuota. Contatta il tuo rappresentante di Adobe per assicurarti che i valori `null` siano scritti correttamente come `null` in Adobe Experience Platform.
>* Ad Experience Platform, per acquisire i dati, i fusi orari per tutte le origini batch basate su tabelle devono essere configurati in formato UTC. L&#39;unico indicatore orario supportato per l&#39;origine [!DNL Snowflake] è TIMESTAMP_NTZ con ora UTC.

Adobe Experience Platform consente di acquisire i dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

Experience Platform fornisce supporto per l’acquisizione di dati da un database di terze parti. Platform può connettersi a diversi tipi di database, ad esempio database relazionali, NoSQL o data warehouse. Il supporto per i provider di database include [!DNL Snowflake].

## Prerequisiti {#prerequisites}

In questa sezione vengono illustrate le attività di installazione che è necessario completare prima di connettere l&#39;origine [!DNL Snowflake] all&#39;Experience Platform.

### Recupera l’identificatore dell’account {#retrieve-your-account-identifier}

È necessario recuperare l&#39;identificatore dell&#39;account dal dashboard dell&#39;interfaccia utente di [!DNL Snowflake] perché verrà utilizzato l&#39;identificatore dell&#39;account per autenticare l&#39;istanza di [!DNL Snowflake] in Experience Platform.

Per recuperare l’identificatore dell’account:

* Accedi al tuo account nel [[!DNL Snowflake] dashboard dell&#39;interfaccia utente dell&#39;applicazione](https://app.snowflake.com/).
* Nel menu di navigazione a sinistra, seleziona **[!DNL Accounts]**, seguito da **[!DNL Active Accounts]** dall&#39;intestazione.
* Quindi, seleziona l’icona delle informazioni, quindi fai clic sul nome di dominio dell’URL corrente e copialo.

![Dashboard dell&#39;interfaccia utente del Snowflake con il nome di dominio selezionato.](../../images/tutorials/create/snowflake/snowflake-dashboard.png)

### Recupera la chiave privata {#retrieve-your-private-key}

Se si utilizza l&#39;autenticazione con coppia di chiavi per la connessione [!DNL Snowflake], è necessario generare anche la chiave privata prima di connettersi a Experience Platform.

>[!BEGINTABS]

>[!TAB Crea una chiave privata crittografata]

Per generare la chiave privata [!DNL Snowflake] crittografata, eseguire il comando seguente sul terminale:

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -v2 des3 -inform PEM -out rsa_key.p8
```

In caso di esito positivo, dovresti ricevere la tua chiave privata in formato PEM.

```shell
-----BEGIN ENCRYPTED PRIVATE KEY-----
MIIE6T...
-----END ENCRYPTED PRIVATE KEY-----
```

>[!TAB Crea una chiave privata non crittografata]

Per generare la chiave privata [!DNL Snowflake] non crittografata, eseguire il comando seguente sul terminale:

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -inform PEM -out rsa_key.p8 -nocrypt
```

In caso di esito positivo, dovresti ricevere la tua chiave privata in formato PEM.

```shell
-----BEGIN PRIVATE KEY-----
MIIE6T...
-----END PRIVATE KEY-----
```

>[!ENDTABS]

Quindi, prendere la chiave privata e codificarla in [!DNL Base64]. Assicurati di non eseguire alcuna trasformazione o conversione di formato nella chiave privata [!DNL Snowflake]. Inoltre, è necessario verificare che non siano presenti caratteri di nuova riga finali alla fine della chiave privata, prima di codificarla in [!DNL Base64].

### Verifica configurazioni

Prima di poter creare una connessione di origine per i dati di [!DNL Snowflake], è necessario verificare che siano soddisfatte le seguenti configurazioni:

* Il magazzino predefinito assegnato a un determinato utente deve essere uguale al magazzino immesso durante l&#39;autenticazione in Experience Platform.
* Il ruolo predefinito assegnato a un determinato utente deve avere accesso allo stesso database immesso durante l’autenticazione in Experience Platform.

Per verificare il ruolo e il magazzino:

* Selezionare **[!DNL Admin]** nel menu di navigazione a sinistra, quindi selezionare **[!DNL Users & Roles]**.
* Selezionare l&#39;utente appropriato, quindi selezionare i puntini di sospensione (`...`) nell&#39;angolo superiore destro.
* Nella finestra [!DNL Edit user] visualizzata, passa a [!DNL Default Role] per visualizzare il ruolo associato all&#39;utente specificato.
* Nella stessa finestra passare a [!DNL Default Warehouse] per visualizzare il magazzino associato all&#39;utente specificato.

![Interfaccia utente del Snowflake in cui è possibile verificare il proprio ruolo e il proprio data warehouse.](../../images/tutorials/create/snowflake/snowflake-configs.png)

Una volta codificata correttamente, è possibile utilizzare la chiave privata con codifica [!DNL Base64] su Experience Platform per autenticare l&#39;account [!DNL Snowflake].

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un elenco consentiti. La mancata aggiunta all’elenco consentiti degli indirizzi IP specifici per l’area geografica potrebbe causare errori o prestazioni non ottimali durante l’utilizzo delle origini. Per ulteriori informazioni, vedere la pagina [elenco consentiti indirizzo IP](../../ip-address-allow-list.md).

La documentazione seguente fornisce informazioni su come connettere [!DNL Snowflake] a Platform tramite API o tramite l&#39;interfaccia utente:

## Connetti [!DNL Snowflake] a Platform tramite API

* [Creare una connessione di base al Snowflake utilizzando l’API del servizio Flusso](../../tutorials/api/create/databases/snowflake.md)
* [Esplorare le tabelle di dati utilizzando l’API del servizio Flusso](../../tutorials/api/explore/tabular.md)
* [Creare un flusso di dati per un’origine di database utilizzando l’API del servizio Flusso](../../tutorials/api/collect/database-nosql.md)

## Connetti [!DNL Snowflake] a Platform tramite l&#39;interfaccia utente

* [Creare una connessione sorgente del Snowflake nell’interfaccia utente](../../tutorials/ui/create/databases/snowflake.md)
* [Creare un flusso di dati per una connessione di origine al database nell’interfaccia utente](../../tutorials/ui/dataflow/databases.md)
