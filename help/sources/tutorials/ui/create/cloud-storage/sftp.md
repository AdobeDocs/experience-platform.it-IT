---
title: Creare una connessione Source SFTP nell’interfaccia utente
description: Scopri come creare una connessione sorgente SFTP utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: 9cd1232c9257d27b80ed57c26658b1e4058535e8
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 1%

---

# Crea una connessione di origine [!DNL SFTP] nell&#39;interfaccia utente

Questo tutorial descrive i passaggi necessari per creare una connessione di origine [!DNL SFTP] tramite l&#39;interfaccia utente di Adobe Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato in base al quale Experience Platform organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

>[!IMPORTANT]
>
>Si consiglia di evitare il ritorno a capo o a nuove righe durante l&#39;acquisizione di oggetti JSON con una connessione di origine [!DNL SFTP]. Per aggirare il limite, utilizza un singolo oggetto JSON per riga e utilizza più righe per i file successivi.

Se disponi già di una connessione [!DNL SFTP] valida, puoi saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Raccogli le credenziali richieste

Leggi la [[!DNL SFTP] guida all&#39;autenticazione](../../../../connectors/cloud-storage/sftp.md#gather-required-credentials) per i passaggi dettagliati su come recuperare le credenziali di autenticazione.

## Connetti al server [!DNL SFTP]

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Nella schermata [!UICONTROL Catalogo] sono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria [!UICONTROL Archiviazione cloud], seleziona **[!UICONTROL SFTP]**, quindi **[!UICONTROL Aggiungi dati]**.

![Catalogo delle origini Experienci Platform con l&#39;origine SFTP selezionata.](../../../../images/tutorials/create/sftp/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti a SFTP]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per connettere un account esistente, seleziona l&#39;account FTP o SFTP con cui desideri connetterti, quindi seleziona **[!UICONTROL Avanti]** per continuare.

![Elenco di account SFTP esistenti nell&#39;interfaccia utente di Experience Platform.](../../../../images/tutorials/create/sftp/existing.png)

### Nuovo account

>[!TIP]
>
>* Una volta creata, non è possibile modificare il tipo di autenticazione di una connessione di base [!DNL SFTP]. Per modificare il tipo di autenticazione, è necessario creare una nuova connessione di base.
>
>* SFTP supporta una chiave OpenSSH di tipo RSA o DSA. Assicurarsi che il contenuto del file chiave inizi con `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` e termini con `"-----END [RSA/DSA] PRIVATE KEY-----"`. Se il file della chiave privata è in formato PPK, utilizzare lo strumento PuTTY per convertire il formato PPK in OpenSSH.

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci un nome e una descrizione facoltativa per il nuovo account [!DNL SFTP].

![La schermata del nuovo account per SFTP](../../../../images/tutorials/create/sftp/new.png)

L&#39;origine [!DNL SFTP] supporta sia l&#39;autenticazione di base che l&#39;autenticazione tramite la chiave pubblica SSH.

>[!BEGINTABS]

>[!TAB Autenticazione di base]

Per utilizzare l&#39;autenticazione di base, selezionare **[!UICONTROL Password]**, quindi specificare i valori appropriati per le credenziali seguenti:

* host
* porta
* nome utente
* password

Durante questo passaggio è inoltre possibile configurare il numero massimo di connessioni simultanee, definire il percorso della cartella e abilitare o disabilitare il blocco per il server [!DNL SFTP]. Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]** e attendere alcuni istanti prima di stabilire la connessione.

Per ulteriori informazioni sull&#39;autenticazione, leggere la guida in [raccolta delle credenziali richieste per  [!DNL SFTP]](../../../../connectors/cloud-storage/sftp.md#gather-required-credentials).

![Nuova schermata dell&#39;account per l&#39;origine SFTP con autenticazione di base](../../../../images/tutorials/create/sftp/password.png)

>[!TAB Autenticazione chiave pubblica SSH]

Per utilizzare le credenziali basate su chiave pubblica SSH, selezionare **[!UICONTROL Chiave pubblica SSH]**, quindi specificare i valori appropriati per le credenziali seguenti:

* host
* porta
* nome utente
* contenuto chiave privata
* passphrase

Durante questo passaggio è inoltre possibile configurare il numero massimo di connessioni simultanee, definire il percorso della cartella e abilitare o disabilitare il blocco per il server [!DNL SFTP]. Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]** e attendere alcuni istanti prima di stabilire la connessione.

Per ulteriori informazioni sull&#39;autenticazione, leggere la guida in [raccolta delle credenziali richieste per  [!DNL SFTP]](../../../../connectors/cloud-storage/sftp.md#gather-required-credentials).

![Nuova schermata dell&#39;account per l&#39;origine SFTP con chiave pubblica SSH.](../../../../images/tutorials/create/sftp/ssh.png)

>[!ENDTABS]

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account SFTP. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per portare i dati dall&#39;archiviazione cloud in Platform](../../dataflow/batch/cloud-storage.md).
