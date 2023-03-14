---
keywords: Experience Platform;home;argomenti popolari;Query service;query service;connect;connect to query service;SSL;ssl;sslmode;
title: Opzioni SSL di Query Service
description: Scopri il supporto SSL per le connessioni di terze parti a Adobe Experience Platform Query Service e come connettersi utilizzando la modalità SSL verify-full.
exl-id: 41b0a71f-165e-49a2-8a7d-d809f5f683ae
source-git-commit: 75e97efcb68439f1b837af93b62c96f43e5d7a31
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 1%

---

# [!DNL Query Service] Opzioni SSL

Per una maggiore sicurezza, Adobe Experience Platform [!DNL Query Service] fornisce supporto nativo per le connessioni SSL per crittografare le comunicazioni client/server. Questo documento descrive le opzioni SSL disponibili per le connessioni client di terze parti a [!DNL Query Service] e come connettersi utilizzando `verify-full` Valore del parametro SSL.

## Prerequisiti

In questo documento si presuppone che tu abbia già scaricato un’applicazione client desktop di terze parti da utilizzare con i dati di Platform. Le istruzioni specifiche su come incorporare la sicurezza SSL durante la connessione con un client di terze parti si trovano nella rispettiva documentazione della guida alla connessione. Per un elenco di tutti [!DNL Query Service] client supportati, vedi [panoramica delle connessioni client](./overview.md).

## Opzioni SSL disponibili {#available-ssl-options}

Platform supporta varie opzioni SSL per soddisfare le tue esigenze di sicurezza dei dati e bilanciare il sovraccarico di elaborazione della crittografia e dello scambio di chiavi.

Le diverse `sslmode` I valori dei parametri forniscono diversi livelli di protezione. Crittografando i dati in movimento con certificati SSL, aiuta a prevenire attacchi &quot;man-in-the-middle&quot; (MITM), intercettazioni e impersonazioni. La tabella seguente fornisce una suddivisione delle diverse modalità SSL disponibili e del livello di protezione che forniscono.

>[!NOTE]
>
> Il valore SSL `disable` non è supportato da Adobe Experience Platform a causa della conformità alla protezione dei dati richiesta.

| sslmode | Protezione dalle intercettazioni | Protezione MITM | Descrizione |
|---|---|---|---|
| `allow` | Parziale | No | La sicurezza non è una priorità, ma è più importante disporre di velocità e di un sovraccarico di elaborazione ridotto. Questa modalità opta per la crittografia solo se il server insiste su di essa. |
| `prefer` | Parziale | No | La crittografia non è necessaria, ma la comunicazione verrà crittografata se supportata dal server. |
| `require` | Sì | No | La crittografia è obbligatoria per tutte le comunicazioni. La rete è attendibile per la connessione al server corretto. La convalida del certificato SSL del server non è richiesta. |
| `verify-ca` | Sì | Dipende dal criterio CA | La crittografia è obbligatoria per tutte le comunicazioni. La convalida del server è necessaria prima che i dati vengano condivisi. È necessario impostare un certificato radice nel [!DNL PostgreSQL] home directory. [I dettagli sono forniti di seguito](#instructions) |
| `verify-full` | Sì | Sì | La crittografia è obbligatoria per tutte le comunicazioni. La convalida del server è necessaria prima che i dati vengano condivisi. È necessario impostare un certificato radice nel [!DNL PostgreSQL] home directory. [I dettagli sono forniti di seguito](#instructions). |

>[!NOTE]
>
>La differenza tra `verify-ca` e `verify-full` dipende dai criteri dell&#39;autorità di certificazione (CA) radice. Se hai creato una tua CA locale per rilasciare certificati privati per le tue applicazioni, utilizza `verify-ca` spesso fornisce una protezione sufficiente. Se utilizzi una CA pubblica, `verify-ca` consente connessioni a un server registrato da un altro utente con la CA. `verify-full` deve essere sempre utilizzato con una CA radice pubblica.

Quando stabilisci una connessione di terze parti a un database Platform, ti consigliamo di utilizzare `sslmode=require` almeno per garantire una connessione sicura per i dati in movimento. Il `verify-full` La modalità SSL è consigliata per l’utilizzo nella maggior parte degli ambienti sensibili alla sicurezza.

## Imposta un certificato radice per la verifica del server {#root-certificate}

Per garantire una connessione sicura, l’utilizzo SSL deve essere configurato sia sul client che sul server prima che venga stabilita la connessione. Se SSL è configurato solo sul server, il client potrebbe inviare informazioni riservate come le password prima che venga stabilito che il server richiede un livello di protezione elevato.

Per impostazione predefinita, [!DNL PostgreSQL] non esegue alcuna verifica del certificato del server. Verificare l&#39;identità del server e assicurare una connessione sicura prima dell&#39;invio di dati sensibili (come parte di SSL) `verify-full` ), è necessario inserire un certificato radice (autofirmato) nel computer locale (`root.crt`) e un certificato foglia firmato dal certificato radice sul server.

Se il `sslmode` il parametro è impostato su `verify-full`, libpq verificherà che il server sia affidabile controllando la catena di certificati fino al certificato radice memorizzato sul client. Verifica quindi che il nome host corrisponda al nome memorizzato nel certificato del server.

Per consentire la verifica dei certificati del server, è necessario inserire uno o più certificati radice (`root.crt`) in [!DNL PostgreSQL] nella home directory. Il percorso del file è simile a `~/.postgresql/root.crt`.

## Abilita la modalità SSL &quot;verify-full&quot; per l’utilizzo con una terza parte [!DNL Query Service] connessione {#instructions}

Se hai bisogno di controlli di sicurezza più severi rispetto a `sslmode=require`, puoi seguire i passaggi evidenziati per collegare un client di terze parti a [!DNL Query Service] utilizzo `verify-full` Modalità SSL.

>[!NOTE]
>
>Sono disponibili molte opzioni per ottenere un certificato SSL. A causa di una tendenza crescente nei certificati non autorizzati, DigiCert viene utilizzato in questa guida in quanto è un provider globale affidabile di soluzioni TLS/SSL, PKI, IoT e di firma ad alta affidabilità.

1. Accedi a [elenco dei certificati radice DigiCert disponibili](https://www.digicert.com/kb/digicert-root-certificates.htm)
1. Cerca &quot;[!DNL DigiCert Global Root CA]&quot; dall’elenco dei certificati disponibili.
1. Seleziona [!DNL **Scarica PEM**] per scaricare il file sul computer locale.
   ![Elenco dei certificati radice DigiCert disponibili con Download PEM evidenziato.](../images/clients/ssl-modes/digicert.png)
1. Rinomina il file del certificato di protezione in `root.crt`.
1. Copia il file in [!DNL PostgreSQL] cartella. Il percorso del file necessario varia a seconda del sistema operativo in uso. Se la cartella non esiste già, creala.
   - Se utilizzi macOS, il percorso è `/Users/<username>/.postgresql`
   - Se si utilizza Windows, il percorso è `%appdata%\postgresql`

>[!TIP]
>
>Per trovare `%appdata%` in un sistema operativo Windows, premere ⊞ **Win + R** e input `%appdata%` nel campo di ricerca.

Dopo il [!DNL DigiCert Global Root CA] Il file CRT è disponibile nel [!DNL PostgreSQL] cartella, è possibile connettersi a [!DNL Query Service] utilizzando `sslmode=verify-full` o `sslmode=verify-ca` opzione.

## Passaggi successivi

Leggendo questo documento, avrai una migliore comprensione delle opzioni SSL disponibili per la connessione di un client di terze parti a [!DNL Query Service], e anche come abilitare `verify-full` Opzione SSL per crittografare i dati in movimento.

Se non lo hai già fatto, segui le istruzioni su [connessione di un client di terze parti a [!DNL Query Service]](./overview.md).
