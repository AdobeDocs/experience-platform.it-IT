---
title: Creare una connessione sorgente SFTP nell’interfaccia utente
description: Scopri come creare una connessione sorgente SFTP utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: e92471b386b857fc21947d352f1c1b88431c68bc
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 0%

---

# Creare un [!DNL SFTP] connessione sorgente nell’interfaccia utente

Questo tutorial descrive i passaggi necessari per creare [!DNL SFTP] connessione sorgente tramite l’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale Experienci Platform organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

>[!IMPORTANT]
>
>Si consiglia di evitare il ritorno a capo o a nuove righe durante l’acquisizione di oggetti JSON con un [!DNL SFTP] connessione sorgente. Per aggirare il limite, utilizza un singolo oggetto JSON per riga e utilizza più righe per i file successivi.

Se disponi già di un [!DNL SFTP] connessione, è possibile saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Raccogli le credenziali richieste

Per connettersi a [!DNL SFTP], è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Nome o indirizzo IP associato al [!DNL SFTP] server. |
| `port` | Il [!DNL SFTP] porta server a cui ti stai connettendo. Se non specificato, il valore predefinito è `22`. |
| `username` | Il nome utente con accesso al [!DNL SFTP] server. |
| `password` | La password per [!DNL SFTP] server. |
| `privateKeyContent` | Il contenuto della chiave privata SSH con codifica Base64. Il tipo di chiave OpenSSH deve essere classificato come RSA o DSA. |
| `passPhrase` | La passphrase o password per decrittografare la chiave privata se il file di chiave o il contenuto della chiave è protetto da una passphrase. Se PrivateKeyContent è protetto da password, questo parametro deve essere utilizzato con la passphrase di PrivateKeyContent come valore. |
| `maxConcurrentConnections` | Questo parametro consente di specificare un limite massimo per il numero di connessioni simultanee che Platform creerà durante la connessione al server SFTP. Devi impostare questo valore su un valore inferiore al limite impostato da SFTP. **Nota**: quando questa impostazione è abilitata per un account SFTP esistente, influirà solo sui flussi di dati futuri e non sui flussi di dati esistenti. |
| Percorso della cartella | Percorso della cartella a cui desideri fornire l’accesso. [!DNL SFTP] origine, è possibile specificare il percorso della cartella per specificare l&#39;accesso utente alla sottocartella desiderata. |

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per creare una nuova [!DNL SFTP] per la connessione a Platform.

## Connetti al tuo [!DNL SFTP] server

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Il [!UICONTROL Catalogo] Nella schermata vengono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Sotto [!UICONTROL Archiviazione cloud] categoria, seleziona **[!UICONTROL SFTP]** e quindi seleziona **[!UICONTROL Aggiungi dati]**.

![Il catalogo delle origini Experienci Platform con l’origine SFTP selezionata.](../../../../images/tutorials/create/sftp/catalog.png)

Il **[!UICONTROL Connettersi a SFTP]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per collegare un account esistente, seleziona l’account FTP o SFTP con cui desideri connetterti, quindi fai clic su **[!UICONTROL Successivo]** per procedere.

![Elenco di account SFTP esistenti nell’interfaccia utente di Experienci Platform.](../../../../images/tutorials/create/sftp/existing.png)

### Nuovo account

>[!TIP]
>
>* Una volta creato, non è possibile modificare il tipo di autenticazione di un [!DNL SFTP] connessione di base. Per modificare il tipo di autenticazione, è necessario creare una nuova connessione di base.
>
>* SFTP supporta una chiave OpenSSH di tipo RSA o DSA. Assicurati che il contenuto del file chiave inizi con `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` e termina con `"-----END [RSA/DSA] PRIVATE KEY-----"`. Se il file della chiave privata è in formato PPK, utilizzare lo strumento PuTTY per convertire il formato PPK in OpenSSH.

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]** e quindi fornisci un nome e una descrizione facoltativa per il nuovo [!DNL SFTP] account.

![Schermata Nuovo account per SFTP](../../../../images/tutorials/create/sftp/new.png)

Il [!DNL SFTP] l&#39;origine supporta sia l&#39;autenticazione di base che l&#39;autenticazione tramite la chiave pubblica SSH.

>[!BEGINTABS]

>[!TAB Autenticazione di base]

Per utilizzare l’autenticazione di base, seleziona **[!UICONTROL Password]** e quindi fornire i valori di host e porta a cui connettersi, insieme al nome utente e alla password. Durante questo passaggio, puoi anche designare il percorso della sottocartella a cui desideri fornire l’accesso. Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]**.

![Schermata Nuovo account per l’origine SFTP con autenticazione di base](../../../../images/tutorials/create/sftp/password.png)

>[!TAB Autenticazione chiave pubblica SSH]

Per utilizzare le credenziali basate su chiave pubblica SSH, seleziona **[!UICONTROL Chiave pubblica SSH]**  e quindi fornire i valori di host e porta, nonché la combinazione di contenuto chiave privata e passphrase. Durante questo passaggio, puoi anche designare il percorso della sottocartella a cui desideri fornire l’accesso. Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]**.

![La schermata del nuovo account per l’origine SFTP che utilizza la chiave pubblica SSH.](../../../../images/tutorials/create/sftp/ssh.png)

>[!ENDTABS]

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account SFTP. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per portare i dati dall’archiviazione cloud a Platform](../../dataflow/batch/cloud-storage.md).
