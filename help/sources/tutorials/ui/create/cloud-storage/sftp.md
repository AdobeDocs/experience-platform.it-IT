---
keywords: Experience Platform;home;argomenti popolari;SFTP;sftp
solution: Experience Platform
title: Creare una connessione sorgente SFTP nell’interfaccia utente
topic-legacy: overview
type: Tutorial
description: Scopri come creare una connessione sorgente SFTP utilizzando l’interfaccia utente Adobe Experience Platform.
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: ade0da445b18108a7f8720404cc7a65139ed42b1
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 0%

---

# Creare una connessione sorgente [!DNL SFTP] nell&#39;interfaccia utente

Questa esercitazione descrive i passaggi necessari per creare una connessione sorgente [!DNL SFTP] utilizzando l’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standardizzato in base al quale l’Experience Platform organizza i dati sulla customer experience.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md) dello schema: Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md) dell’Editor di schema: Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

>[!IMPORTANT]
>
>Si consiglia di evitare l’esecuzione di nuove righe o ritorni a capo durante l’acquisizione di oggetti JSON con una connessione sorgente [!DNL SFTP]. Per aggirare il limite, utilizza un singolo oggetto JSON per riga e utilizza più righe per i file successivi.

Se disponi già di una connessione [!DNL SFTP] valida, puoi saltare il resto del documento e continuare l&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Raccogli credenziali richieste

Per connettersi a [!DNL SFTP], è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Nome o indirizzo IP associato al server [!DNL SFTP]. |
| `port` | La porta del server [!DNL SFTP] a cui ci si connette. Se non viene fornito, il valore predefinito è `22`. |
| `username` | Il nome utente con accesso al server [!DNL SFTP]. |
| `password` | Password per il server [!DNL SFTP]. |
| `privateKeyContent` | Contenuto della chiave privata SSH codificata Base64. Il tipo di chiave OpenSSH deve essere classificato come RSA o DSA. |
| `passPhrase` | La frase o password per decrittografare la chiave privata se il file di chiave o il contenuto della chiave sono protetti da una frase di passaggio. Se PrivateKeyContent è protetto da password, questo parametro deve essere utilizzato con la passphrase PrivateKeyContent come valore. |

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per creare un nuovo account [!DNL SFTP] per la connessione a Platform.

## Connettiti al server [!DNL SFTP]

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere all’area di lavoro [!UICONTROL Origini]. La schermata [!UICONTROL Catalogo] visualizza una varietà di sorgenti con cui puoi creare un account in entrata.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la categoria [!UICONTROL Archiviazione cloud], seleziona **[!UICONTROL SFTP]**, quindi seleziona **[!UICONTROL Aggiungi dati]**.

![catalogo](../../../../images/tutorials/create/sftp/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti a SFTP]** . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Account esistente

Per collegare un account esistente, seleziona l&#39;account FTP o SFTP con cui desideri connetterti, quindi seleziona **[!UICONTROL Avanti]** per procedere.

![esistente](../../../../images/tutorials/create/sftp/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci un nome e una descrizione facoltativa per il tuo nuovo account [!DNL SFTP].

#### Autenticazione tramite password

[!DNL SFTP] supporta diversi tipi di autenticazione per l&#39;accesso. In **[!UICONTROL Autenticazione account]** seleziona **[!UICONTROL Password]** e quindi fornisci i valori host e porte a cui connettersi, insieme al nome utente e alla password.

![connect-password](../../../../images/tutorials/create/sftp/password.png)

#### Autenticazione tramite chiave pubblica SSH

Per utilizzare le credenziali basate su chiave pubblica SSH, seleziona **[!UICONTROL Chiave pubblica SSH]**, quindi fornisci i valori dell&#39;host e della porta, nonché la combinazione di contenuto chiave privata e passphrase.

>[!IMPORTANT]
>
>SFTP supporta una chiave OpenSSH di tipo RSA o DSA. Assicurati che il contenuto del file chiave inizi con `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` e termini con `"-----END [RSA/DSA] PRIVATE KEY-----"`. Se il file della chiave privata è un file in formato PPK, utilizza lo strumento PuTTY per convertire da PPK a formato OpenSSH.

![connect-ssh](../../../../images/tutorials/create/sftp/ssh-public-key.png)

| Credenziali | Descrizione |
| ---------- | ----------- |
| Contenuto della chiave privata | Contenuto della chiave privata SSH codificata Base64. Il tipo di chiave OpenSSH deve essere classificato come RSA o DSA. |
| Passphrase | Specifica la frase o la password di passaggio per decrittografare la chiave privata se il file di chiave o il contenuto della chiave sono protetti da una frase di passaggio. Se PrivateKeyContent è protetto da password, questo parametro deve essere utilizzato con la passphrase PrivateKeyContent come valore. |


## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account SFTP. Ora puoi continuare l’esercitazione successiva e [configurare un flusso di dati per inserire dati dall’archiviazione cloud in Platform](../../dataflow/batch/cloud-storage.md).
