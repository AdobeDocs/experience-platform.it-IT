---
keywords: Experience Platform;home;argomenti popolari;SFTP;sftp
solution: Experience Platform
title: Creare una connessione sorgente SFTP nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione sorgente SFTP utilizzando l’interfaccia utente Adobe Experience Platform.
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 0%

---

# Crea un [!DNL SFTP] connessione sorgente nell’interfaccia utente

Questa esercitazione descrive i passaggi necessari per creare un [!DNL SFTP] connessione sorgente tramite l’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standardizzato in base al quale l’Experience Platform organizza i dati sulla customer experience.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’Editor di schema](../../../../../xdm/tutorials/create-schema-ui.md): Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

>[!IMPORTANT]
>
>Si consiglia di evitare la restituzione di nuove righe o carrelli durante l’acquisizione di oggetti JSON con un [!DNL SFTP] connessione di origine. Per aggirare il limite, utilizza un singolo oggetto JSON per riga e utilizza più righe per i file successivi.

Se disponi già di una [!DNL SFTP] è possibile ignorare il resto del documento e passare all&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Raccogli credenziali richieste

Per connettersi a [!DNL SFTP], è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Nome o indirizzo IP associato al tuo [!DNL SFTP] server. |
| `port` | La [!DNL SFTP] porta server a cui ci si connette. Se non viene fornito, il valore predefinito è `22`. |
| `username` | Il nome utente con accesso al tuo [!DNL SFTP] server. |
| `password` | La password [!DNL SFTP] server. |
| `privateKeyContent` | Contenuto della chiave privata SSH codificata Base64. Il tipo di chiave OpenSSH deve essere classificato come RSA o DSA. |
| `passPhrase` | La frase o password per decrittografare la chiave privata se il file di chiave o il contenuto della chiave sono protetti da una frase di passaggio. Se PrivateKeyContent è protetto da password, questo parametro deve essere utilizzato con la passphrase PrivateKeyContent come valore. |
| `maxConcurrentConnections` | Questo parametro consente di specificare un limite massimo per il numero di connessioni simultanee che Platform creerà quando si connette al server SFTP. Devi impostare questo valore affinché sia inferiore al limite impostato da SFTP. **Nota**: Quando questa impostazione è abilitata per un account SFTP esistente, influenzerà solo i flussi di dati futuri e non i flussi di dati esistenti. |

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per creare una nuova [!DNL SFTP] account per la connessione a Platform.

## Collegati al tuo [!DNL SFTP] server

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Origini] workspace. La [!UICONTROL Catalogo] in viene visualizzata una varietà di sorgenti con cui è possibile creare un account in entrata.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la [!UICONTROL archiviazione cloud] categoria, seleziona **[!UICONTROL SFTP]** quindi seleziona **[!UICONTROL Aggiungi dati]**.

![Catalogo delle sorgenti di Experience Platform con la sorgente SFTP selezionata.](../../../../images/tutorials/create/sftp/catalog.png)

La **[!UICONTROL Connessione a SFTP]** viene visualizzata la pagina . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Account esistente

Per collegare un account esistente, seleziona l’account FTP o SFTP con cui desideri connetterti, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![Elenco degli account SFTP esistenti nell’interfaccia utente di Experience Platform.](../../../../images/tutorials/create/sftp/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci un nome e una descrizione facoltativa per il nuovo [!DNL SFTP] conto.

![La nuova schermata dell’account per SFTP](../../../../images/tutorials/create/sftp/new.png)

#### Autenticazione tramite password

[!DNL SFTP] supporta diversi tipi di autenticazione per l&#39;accesso. Sotto **[!UICONTROL Autenticazione account]** select **[!UICONTROL Password]** e quindi fornire i valori host e porta a cui connettersi, insieme al nome utente e alla password.

![La nuova schermata dell’account per la sorgente SFTP utilizzando l’autenticazione di base](../../../../images/tutorials/create/sftp/password.png)

#### Autenticazione tramite chiave pubblica SSH

Per utilizzare le credenziali basate su chiave pubblica SSH, seleziona **[!UICONTROL Chiave pubblica SSH]**  e quindi fornisci i valori host e porta, nonché la combinazione di contenuto chiave privata e passphrase.

>[!IMPORTANT]
>
>SFTP supporta una chiave OpenSSH di tipo RSA o DSA. Assicurati che il contenuto del tuo file chiave inizi con `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` e termina con `"-----END [RSA/DSA] PRIVATE KEY-----"`. Se il file della chiave privata è un file in formato PPK, utilizza lo strumento PuTTY per convertire da PPK a formato OpenSSH.

![La nuova schermata dell’account per l’origine SFTP utilizzando la chiave pubblica SSH.](../../../../images/tutorials/create/sftp/ssh.png)

| Credenziali | Descrizione |
| ---------- | ----------- |
| Contenuto della chiave privata | Contenuto della chiave privata SSH codificata Base64. Il tipo di chiave OpenSSH deve essere classificato come RSA o DSA. |
| Passphrase | Specifica la frase o la password di passaggio per decrittografare la chiave privata se il file di chiave o il contenuto della chiave sono protetti da una frase di passaggio. Se PrivateKeyContent è protetto da password, questo parametro deve essere utilizzato con la passphrase PrivateKeyContent come valore. |


## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account SFTP. Ora puoi passare all’esercitazione successiva e [configurare un flusso di dati per l’importazione di dati dall’archiviazione cloud in Platform](../../dataflow/batch/cloud-storage.md).
