---
keywords: Experience Platform;home;argomenti popolari;Query service;query service;connect;connect to query service;SSL;ssl;sslmode;
title: Opzioni SSL del servizio query
description: Scopri il supporto SSL per le connessioni di terze parti a Adobe Experience Platform Query Service e come connettersi utilizzando la modalità SSL verify-full.
source-git-commit: 92dac8e75e1ddda860d255ce1b7d278041c89325
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 1%

---

# [!DNL Query Service] Opzioni SSL

Per una maggiore sicurezza, Adobe Experience Platform [!DNL Query Service] fornisce supporto nativo per le connessioni SSL per crittografare le comunicazioni client/server. Questo documento illustra le opzioni SSL disponibili per le connessioni client di terze parti a [!DNL Query Service] e come connettersi utilizzando `verify-full` Valore del parametro SSL.

## Prerequisiti

Questo documento presuppone che sia già stata scaricata un’applicazione client desktop di terze parti da utilizzare con i dati di Platform. Le istruzioni specifiche su come incorporare la sicurezza SSL quando ci si connette a un client di terze parti sono disponibili nella relativa documentazione della guida alla connessione. Per un elenco di tutti [!DNL Query Service] client supportati, vedi [panoramica delle connessioni client](./overview.md).

## Opzioni SSL disponibili {#available-ssl-options}

Platform supporta varie opzioni SSL per soddisfare le tue esigenze di sicurezza dei dati e bilanciare il sovraccarico di elaborazione della crittografia e dello scambio di chiavi.

I diversi `sslmode` I valori dei parametri forniscono diversi livelli di protezione. La cifratura dei dati in movimento con i certificati SSL aiuta a prevenire attacchi &quot;man-in-the-middle&quot; (MITM), intercettazioni e rappresentazione. La tabella seguente fornisce un’analisi delle diverse modalità SSL disponibili e del livello di protezione fornito.

>[!NOTE]
>
> Il valore SSL `disable` non è supportato da Adobe Experience Platform a causa della conformità necessaria alla protezione dei dati.

| sslmode | Protezione da intercettazioni | Protezione MITM | Descrizione |
|---|---|---|---|
| `allow` | Parziale | No | La sicurezza non è una priorità, la velocità e il sovraccarico di elaborazione sono più importanti. Questa modalità consente la crittografia solo se il server insiste su di essa. |
| `prefer` | Parziale | No | La crittografia non è necessaria, ma la comunicazione verrà crittografata se il server la supporta. |
| `require` | Sì | No | È necessaria la codifica su tutte le comunicazioni. La rete è attendibile per la connessione al server corretto. La convalida del certificato SSL del server non è necessaria. |
| `verify-ca` | Sì | Dipende dalla policy CA | È necessaria la codifica su tutte le comunicazioni. La convalida del server è necessaria prima della condivisione dei dati. Questo richiede l&#39;impostazione di un certificato radice nella directory home di PostgreSQL. [Di seguito sono riportati i dettagli](#instructions) |
| `verify-full` | Sì | Sì | È necessaria la codifica su tutte le comunicazioni. La convalida del server è necessaria prima della condivisione dei dati. Questo richiede l&#39;impostazione di un certificato radice nella directory home di PostgreSQL. [Di seguito sono riportati i dettagli](#instructions). |

>[!NOTE]
>
>La differenza tra `verify-ca` e `verify-full` dipende dal criterio dell’autorità di certificazione principale (CA). Se hai creato una CA locale personalizzata per il rilascio di certificati privati per le applicazioni, utilizzando `verify-ca` offre spesso una protezione sufficiente. Se si utilizza una CA pubblica, `verify-ca` consente connessioni a un server che un altro utente potrebbe aver registrato con la CA. `verify-full` deve essere sempre utilizzato con una CA radice pubblica.

Quando si stabilisce una connessione di terze parti a un database di Platform, si consiglia di utilizzare `sslmode=require` almeno per garantire una connessione sicura per i dati in movimento. La `verify-full` La modalità SSL è consigliata per l’utilizzo nella maggior parte degli ambienti sensibili alla sicurezza.

## Imposta un certificato radice per la verifica del server {#root-certificate}

Per garantire una connessione sicura, prima di effettuare la connessione è necessario configurare l’utilizzo SSL sia sul client che sul server. Se SSL è configurato solo sul server, il client potrebbe inviare informazioni sensibili, ad esempio password, prima che sia stabilito che il server richiede un’elevata sicurezza.

Per impostazione predefinita, [!DNL PostgreSQL] non esegue alcuna verifica del certificato server. Verificare l’identità del server e garantire una connessione sicura prima dell’invio di dati sensibili (come parte di SSL `verify-full` , è necessario inserire un certificato radice (autofirmato) nel computer locale (`root.crt`) e un certificato foglia firmato dal certificato radice sul server.

Se la `sslmode` è impostato su `verify-full`, libpq verificherà che il server sia affidabile controllando la catena di certificati fino al certificato principale memorizzato sul client. Verifica quindi che il nome host corrisponda al nome memorizzato nel certificato del server.

Per consentire la verifica dei certificati del server, è necessario inserire uno o più certificati radice (`root.crt`) nel [!DNL PostgreSQL] nella directory principale. Il percorso del file sarà simile a `~/.postgresql/root.crt`.

## Abilita la modalità SSL verify-full per l’utilizzo con un’altra parte [!DNL Query Service] connection {#instructions}

Se hai bisogno di un controllo di sicurezza più rigoroso di `sslmode=require`, puoi seguire i passaggi evidenziati per collegare un client di terze parti a [!DNL Query Service] utilizzo `verify-full` Modalità SSL.

>[!NOTE]
>
>Sono disponibili numerose opzioni per ottenere un certificato SSL. A causa di una tendenza crescente nei certificati non conformi, DigiCert viene utilizzato in questa guida in quanto sono un fornitore globale affidabile di soluzioni TLS/SSL, PKI, IoT e di firma ad alta garanzia.

1. Passa a [elenco dei certificati radice DigiCert disponibili](https://www.digicert.com/kb/digicert-root-certificates.htm)
1. Cerca &quot;[!DNL DigiCert Global Root CA]&quot; dall&#39;elenco dei certificati disponibili.
1. Seleziona [!DNL **Scarica PEM**] per scaricare il file nel computer locale.
   ![Elenco dei certificati radice DigiCert disponibili con Download PEM evidenziato.](../images/clients/ssl-modes/digicert.png)
1. Rinomina il file del certificato di protezione in `root.crt`.
1. Copia il file nel [!DNL PostgreSQL] cartella. Il percorso del file necessario è diverso a seconda del sistema operativo in uso. Se la cartella non esiste già, crearla.
   - Se utilizzi macOS, il percorso è `/Users/<username>/.postgresql`
   - Se si utilizza Windows, il percorso è `%appdata%\postgresql`

>[!TIP]
>
>Per trovare il tuo `%appdata%` posizione del file in un sistema operativo Windows, premere ⊞ **Win + R** e l&#39;ingresso `%appdata%` nel campo di ricerca.

Dopo la [!DNL DigiCert Global Root CA] Il file CRT è disponibile nel tuo [!DNL PostgreSQL] è possibile connettersi a [!DNL Query Service] utilizzando `sslmode=verify-full` o `sslmode=verify-ca` opzione .

## Passaggi successivi

Leggendo questo documento, hai una migliore comprensione delle opzioni SSL disponibili per la connessione di un client di terze parti a [!DNL Query Service]e inoltre come abilitare il `verify-full` Opzione SSL per crittografare i dati in movimento.

Se non lo hai già fatto, segui le indicazioni su [connessione di un client di terze parti a [!DNL Query Service]](./overview.md).
