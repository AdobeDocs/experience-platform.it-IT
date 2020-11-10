---
keywords: Experience Platform;home;popular topics;SFTP;FTP;ftp;sftp
solution: Experience Platform
title: Creare un connettore sorgente FTP o SFTP nell’interfaccia utente
topic: overview
type: Tutorial
description: Questa esercitazione fornisce i passaggi per creare un connettore sorgente FTP o SFTP utilizzando l'interfaccia utente della piattaforma.
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 1%

---


# Creare un connettore sorgente FTP o SFTP nell’interfaccia utente

>[!NOTE]
>
>I connettori FTP e SFTP sono in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la panoramica [](../../../../home.md#terms-and-conditions) Origini.

I connettori di origine in Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce i passaggi per creare un connettore sorgente FTP o SFTP utilizzando l&#39;interfaccia [!DNL Platform] utente.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standard con cui  Experience Platform organizza i dati sull&#39;esperienza dei clienti.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponete già di una connessione FTP o SFTP valida, potete ignorare il resto del documento e procedere all&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Formati di file supportati

[!DNL Experience Platform] supporta i seguenti formati di file da acquisire da origini esterne:

* Valori separati da delimitatore (DSV): Il supporto per i file di dati formattati DSV è attualmente limitato ai valori separati da virgole (CSV). Il valore delle intestazioni dei campi all&#39;interno dei file formattati DSV deve essere costituito solo da caratteri alfanumerici e caratteri di sottolineatura. In futuro verrà fornito il supporto per la DSV.
* JavaScript Object Notation (JSON): I file di dati formattati JSON devono essere conformi a XDM.
* Parquet Apache: I file di dati in formato parquet devono essere conformi a XDM.

### Raccogli credenziali richieste

Per accedere al server FTP o SFTP su [!DNL Platform], dovete fornire il nome host del server, un nome utente e una password.

## Connessione al server FTP o SFTP

Dopo aver raccolto le credenziali necessarie, puoi seguire i passaggi descritti di seguito per creare un nuovo account FTP o SFTP a cui connetterti [!DNL Platform].

Accedete ad [Adobe Experience Platform](https://platform.adobe.com) , quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39; **[!UICONTROL Sources]** area di lavoro. Nella **[!UICONTROL Catalog]** schermata sono visualizzate diverse sorgenti con cui è possibile creare un account in ingresso.

Potete selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l&#39;origine specifica con cui si desidera lavorare utilizzando l&#39;opzione di ricerca.

Sotto la **[!UICONTROL Databases]** categoria, selezionare **[!UICONTROL SFTP]**. Se si tratta della prima volta che si utilizza questo connettore, selezionare **[!UICONTROL Configure]**. In caso contrario, selezionare **[!UICONTROL Add data]** per creare un nuovo connettore FTP o SFTP.

![catalogo](../../../../images/tutorials/create/sftp/catalog.png)

Viene **[!UICONTROL Connect to SFTP]** visualizzata la pagina. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL New account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e le credenziali. Al termine, selezionare **[!UICONTROL Connect]** e quindi concedere un po&#39; di tempo per stabilire la nuova connessione.

Il connettore SFTP fornisce diversi tipi di autenticazione per l&#39;accesso. In **[!UICONTROL Account authentication]** selezionare **[!UICONTROL Password]** per utilizzare una credenziale basata su password.

![connect-password](../../../../images/tutorials/create/sftp/password.png)

In alternativa, puoi selezionare la chiave **[pubblica]** SSH e collegare il tuo account SFTP utilizzando una combinazione di **[!UICONTROL Private key content]** e **[!UICONTROL Passphrase]**.

>[!IMPORTANT]
>
>Il connettore SFTP supporta una chiave RSA/DSA OpenSSH. Assicurati che il contenuto del file chiave inizi con `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"`. Se il file di chiave privata è un file in formato PPK, usate lo strumento PuTTY per convertire da PPK a OpenSSH.

![connect-ssh](../../../../images/tutorials/create/sftp/ssh.png)

| Credenziali | Descrizione |
| ---------- | ----------- |
| Contenuto chiave privata | Un contenuto chiave privata SSH con codifica Base64. La chiave privata SSH deve essere in formato OpenSSH. |
| Passphrase | Specifica la frase di autorizzazione o la password per decifrare la chiave privata se il file chiave o il contenuto chiave sono protetti da una frase di autorizzazione. Se PrivateKeyContent è protetto da password, questo parametro deve essere utilizzato con la passphrase PrivateKeyContent come valore. |

### Account esistente

Per collegare un account esistente, seleziona l&#39;account FTP o SFTP con cui vuoi connetterti, quindi seleziona **[!UICONTROL Next]** per continuare.

![esistenti](../../../../images/tutorials/create/sftp/existing.png)

## Passaggi successivi

Seguendo questa esercitazione hai stabilito una connessione al tuo account FTP o SFTP. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per trasferire i dati dall’archiviazione cloud [!DNL Platform]](../../dataflow/batch/cloud-storage.md).