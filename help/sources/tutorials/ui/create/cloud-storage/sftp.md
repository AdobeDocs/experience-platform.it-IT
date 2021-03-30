---
keywords: Experience Platform;home;argomenti popolari;SFTP;sftp
solution: Experience Platform
title: Creare una connessione sorgente SFTP nell’interfaccia utente
topic: ' - Panoramica'
type: Tutorial
description: Scopri come creare una connessione sorgente SFTP utilizzando l’interfaccia utente Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 0e11acc4a599d360cb3048445003f61848ad23d3
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 1%

---


# Creare una connessione sorgente SFTP nell’interfaccia utente

Questa esercitazione descrive i passaggi necessari per creare una connessione sorgente SFTP utilizzando l’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standardizzato in base al quale l’Experience Platform organizza i dati sulla customer experience.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md) dello schema: Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md) dell’Editor di schema: Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

>[!IMPORTANT]
>
>Si consiglia di evitare la restituzione di nuove righe o ritorni a capo durante l’acquisizione di oggetti JSON con una connessione sorgente SFTP. Per aggirare il limite, utilizza un singolo oggetto JSON per riga e utilizza più righe per i file successivi.

Se disponi già di una connessione SFTP valida, puoi saltare il resto del documento e continuare l&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Raccogli credenziali richieste

Per connettersi a SFTP, devi fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Nome o indirizzo IP associato al server SFTP. |
| `username` | Il nome utente con accesso al server SFTP. |
| `password` | Password per il server SFTP. |
| `privateKeyContent` | Contenuto della chiave privata SSH codificata Base64. Il tipo di chiave OpenSSH deve essere classificato come RSA o DSA. |
| `passPhrase` | La frase o password per decrittografare la chiave privata se il file di chiave o il contenuto della chiave sono protetti da una frase di passaggio. Se PrivateKeyContent è protetto da password, questo parametro deve essere utilizzato con la passphrase PrivateKeyContent come valore. |

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per creare un nuovo account SFTP per la connessione a Platform.

## Connessione al server SFTP

Accedi a [Adobe Experience Platform](https://platform.adobe.com) e seleziona **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Sources]. Nella schermata [!UICONTROL Catalog] sono visualizzate diverse origini per le quali è possibile creare un account in entrata.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la categoria [!UICONTROL Cloud storage], selezionare **[!UICONTROL SFTP]**. Se questa è la prima volta che utilizzi questo connettore, seleziona **[!UICONTROL Configure]**. In caso contrario, seleziona **[!UICONTROL Add data]** per creare una nuova connessione SFTP.

![catalogo](../../../../images/tutorials/create/sftp/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connect to SFTP]** . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Nuovo account

Se utilizzi nuove credenziali, seleziona **[!UICONTROL New account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e le credenziali. Al termine, selezionare **[!UICONTROL Connect]** e quindi concedere un po&#39; di tempo per l&#39;impostazione della nuova connessione.

Il connettore SFTP fornisce diversi tipi di autenticazione per l’accesso. In **[!UICONTROL Account authentication]** selezionare **[!UICONTROL Password]** per utilizzare una credenziale basata su password.

![connect-password](../../../../images/tutorials/create/sftp/password.png)

In alternativa, puoi selezionare **[Chiave pubblica SSH]** e collegare il tuo account SFTP utilizzando una combinazione di [!UICONTROL Private key content] e [!UICONTROL Passphrase].

>[!IMPORTANT]
>
>Il connettore SFTP supporta una chiave OpenSSH di tipo RSA o DSA. Assicurati che il contenuto del file chiave inizi con `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` e termini con `"-----END [RSA/DSA] PRIVATE KEY-----"`. Se il file della chiave privata è un file in formato PPK, utilizza lo strumento PuTTY per convertire da PPK a formato OpenSSH.

![connect-ssh](../../../../images/tutorials/create/sftp/ssh.png)

| Credenziali | Descrizione |
| ---------- | ----------- |
| Contenuto della chiave privata | Contenuto della chiave privata SSH codificata Base64. Il tipo di chiave OpenSSH deve essere classificato come RSA o DSA. |
| Passphrase | Specifica la frase o la password di passaggio per decrittografare la chiave privata se il file di chiave o il contenuto della chiave sono protetti da una frase di passaggio. Se PrivateKeyContent è protetto da password, questo parametro deve essere utilizzato con la passphrase PrivateKeyContent come valore. |

### Account esistente

Per collegare un account esistente, seleziona l&#39;account FTP o SFTP con cui desideri connetterti, quindi seleziona **[!UICONTROL Next]** per procedere.

![esistente](../../../../images/tutorials/create/sftp/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account FTP o SFTP. Ora puoi continuare l’esercitazione successiva e [configurare un flusso di dati per inserire dati dall’archiviazione cloud in Platform](../../dataflow/batch/cloud-storage.md).