---
keywords: Experience Platform;home;argomenti popolari;Query service;query service;connect;connect to query service;SSL;ssl;sslmode;
title: Opzioni SSL di Query Service
description: Scopri il supporto SSL per le connessioni di terze parti a Adobe Experience Platform Query Service e come connettersi utilizzando la modalità SSL verify-full.
exl-id: 41b0a71f-165e-49a2-8a7d-d809f5f683ae
source-git-commit: 229ce98da8f1c97e421ef413826b0d23754d16df
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 1%

---

# [!DNL Query Service] opzioni SSL

Per una maggiore sicurezza, Adobe Experience Platform [!DNL Query Service] fornisce il supporto nativo per le connessioni SSL per crittografare le comunicazioni client/server. Questo documento descrive le opzioni SSL disponibili per le connessioni client di terze parti a [!DNL Query Service] e le modalità di connessione utilizzando il valore del parametro SSL `verify-full`.

## Prerequisiti

In questo documento si presuppone che tu abbia già scaricato un’applicazione client desktop di terze parti da utilizzare con i dati di Platform. Le istruzioni specifiche su come incorporare la sicurezza SSL durante la connessione con un client di terze parti si trovano nella rispettiva documentazione della guida alla connessione. Per un elenco di tutti i [!DNL Query Service] client supportati, vedere la [panoramica delle connessioni client](./overview.md).

## Opzioni SSL disponibili {#available-ssl-options}

Platform supporta varie opzioni SSL per soddisfare le tue esigenze di sicurezza dei dati e bilanciare il sovraccarico di elaborazione della crittografia e dello scambio di chiavi.

I diversi valori dei parametri `sslmode` forniscono diversi livelli di protezione. Crittografando i dati in movimento con certificati SSL, aiuta a prevenire attacchi &quot;man-in-the-middle&quot; (MITM), intercettazioni e impersonazioni. La tabella seguente fornisce una suddivisione delle diverse modalità SSL disponibili e del livello di protezione che forniscono.

>[!NOTE]
>
> Il valore SSL `disable` non è supportato da Adobe Experience Platform a causa della conformità richiesta per la protezione dei dati.

| sslmode | Protezione dalle intercettazioni | Protezione MITM | Descrizione |
|---|---|---|---|
| `allow` | Parziale | No | La sicurezza non è una priorità, ma è più importante disporre di velocità e di un sovraccarico di elaborazione ridotto. Questa modalità opta per la crittografia solo se il server insiste su di essa. |
| `prefer` | Parziale | No | La crittografia non è necessaria, ma la comunicazione verrà crittografata se supportata dal server. |
| `require` | Sì | No | La crittografia è obbligatoria per tutte le comunicazioni. La rete è attendibile per la connessione al server corretto. La convalida del certificato SSL del server non è richiesta. |
| `verify-ca` | Sì | Dipende dal criterio CA | La crittografia è obbligatoria per tutte le comunicazioni. La convalida del server è necessaria prima che i dati vengano condivisi. È necessario configurare un certificato radice nella home directory [!DNL PostgreSQL]. [I dettagli sono forniti di seguito](#instructions) |
| `verify-full` | Sì | Sì | La crittografia è obbligatoria per tutte le comunicazioni. La convalida del server è necessaria prima che i dati vengano condivisi. È necessario configurare un certificato radice nella home directory [!DNL PostgreSQL]. [I dettagli sono forniti di seguito](#instructions). |

>[!NOTE]
>
>La differenza tra `verify-ca` e `verify-full` dipende dai criteri dell&#39;Autorità di certificazione (CA) radice. Se hai creato una tua CA locale per rilasciare certificati privati per le tue applicazioni, l&#39;utilizzo di `verify-ca` spesso fornisce una protezione sufficiente. Se si utilizza una CA pubblica, `verify-ca` consente connessioni a un server che qualcun altro potrebbe aver registrato con la CA. `verify-full` deve sempre essere utilizzato con una CA radice pubblica.

Quando si stabilisce una connessione di terze parti a un database di Platform, si consiglia di utilizzare almeno `sslmode=require` per garantire una connessione sicura per i dati in movimento. La modalità SSL `verify-full` è consigliata per l&#39;utilizzo nella maggior parte degli ambienti sensibili alla sicurezza.

## Imposta un certificato radice per la verifica del server {#root-certificate}

>[!IMPORTANT]
>
>I certificati TLS/SSL sugli ambienti di produzione per l’API Query Service Interactive Postgres sono stati aggiornati mercoledì 24 gennaio 2024.<br>Anche se si tratta di un requisito annuale, in questa occasione anche il certificato radice nella catena è cambiato in seguito all’aggiornamento della gerarchia dei certificati da parte del provider di certificati TLS/SSL di Adobe. Questo problema può interessare alcuni client Postgres se nell’elenco delle autorità di certificazione manca il certificato radice. Ad esempio, per un client CLI PSQL potrebbe essere necessario aggiungere i certificati radice a un file esplicito `~/postgresql/root.crt`. In caso contrario, potrebbe verificarsi un errore. Ad esempio, `psql: error: SSL error: certificate verify failed`. Per ulteriori informazioni su questo problema, consulta la [documentazione ufficiale di PostgreSQL](https://www.postgresql.org/docs/current/libpq-ssl.html#LIBQ-SSL-CERTIFICATES).<br>Il certificato radice da aggiungere può essere scaricato da [https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem).

Per garantire una connessione sicura, l’utilizzo SSL deve essere configurato sia sul client che sul server prima che venga stabilita la connessione. Se SSL è configurato solo sul server, il client potrebbe inviare informazioni riservate come le password prima che venga stabilito che il server richiede un livello di protezione elevato.

Per impostazione predefinita, [!DNL PostgreSQL] non esegue alcuna verifica del certificato del server. Per verificare l&#39;identità del server e garantire una connessione sicura prima dell&#39;invio di dati sensibili (in modalità SSL `verify-full`), è necessario inserire un certificato radice (autofirmato) nel computer locale (`root.crt`) e un certificato foglia firmato dal certificato radice nel server.

Se il parametro `sslmode` è impostato su `verify-full`, libpq verificherà che il server sia affidabile controllando la catena di certificati fino al certificato radice archiviato nel client. Verifica quindi che il nome host corrisponda al nome memorizzato nel certificato del server.

Per consentire la verifica dei certificati del server, è necessario inserire uno o più certificati radice (`root.crt`) nel file [!DNL PostgreSQL] nella home directory. Il percorso del file è simile a `~/.postgresql/root.crt`.

## Abilita la modalità SSL di verifica completa per l&#39;utilizzo con una connessione di terze parti [!DNL Query Service] {#instructions}

Se hai bisogno di un controllo di sicurezza più severo di `sslmode=require`, puoi seguire i passaggi evidenziati per connettere un client di terze parti a [!DNL Query Service] utilizzando la modalità SSL `verify-full`.

>[!NOTE]
>
>Sono disponibili molte opzioni per ottenere un certificato SSL. A causa di una tendenza crescente nei certificati non autorizzati, DigiCert viene utilizzato in questa guida in quanto è un provider globale affidabile di soluzioni TLS/SSL, PKI, IoT e di firma ad alta affidabilità.

1. Passa a [elenco dei certificati radice DigiCert disponibili](https://www.digicert.com/kb/digicert-root-certificates.htm)
1. Cerca &quot;[!DNL DigiCert Global Root G2]&quot; dall&#39;elenco dei certificati disponibili.
1. Seleziona [!DNL **Scarica PEM**] per scaricare il file nel computer locale.
   ![Elenco dei certificati radice DigiCert disponibili con PEM di download evidenziato.](../images/clients/ssl-modes/digicert.png)
1. Rinominare il file del certificato di protezione in `root.crt`.
1. Copiare il file nella cartella [!DNL PostgreSQL]. Il percorso del file necessario varia a seconda del sistema operativo in uso. Se la cartella non esiste già, creala.
   - Se si utilizza macOS, il percorso è `/Users/<username>/.postgresql`
   - Se si utilizza Windows, il percorso è `%appdata%\postgresql`

>[!TIP]
>
>Per trovare il percorso del file `%appdata%` in un sistema operativo Windows, premere ⊞ **Win + R** e immettere `%appdata%` nel campo di ricerca.

Quando il file CRT [!DNL DigiCert Global Root G2] è disponibile nella cartella [!DNL PostgreSQL], è possibile connettersi a [!DNL Query Service] utilizzando l&#39;opzione `sslmode=verify-full` o `sslmode=verify-ca`.

## Passaggi successivi

La lettura di questo documento consente di comprendere meglio le opzioni SSL disponibili per la connessione di un client di terze parti a [!DNL Query Service] e come abilitare l&#39;opzione SSL `verify-full` per crittografare i dati in movimento.

Se non lo hai già fatto, segui le istruzioni su [collegare un client di terze parti a [!DNL Query Service]](./overview.md).
