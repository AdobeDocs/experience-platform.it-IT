---
keywords: Experience Platform;home;popular topics;SFTP;sftp
solution: Experience Platform
title: Creare un connettore sorgente SFTP nell’interfaccia utente
topic: overview
type: Tutorial
description: Questa esercitazione fornisce i passaggi per creare un connettore sorgente SFTP utilizzando l'interfaccia utente della piattaforma.
translation-type: tm+mt
source-git-commit: 7b638f0516804e6a2dbae3982d6284a958230f42
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 0%

---


# Creare un connettore sorgente SFTP nell’interfaccia utente

>[!NOTE]
>
>Il connettore SFTP è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la panoramica [](../../../../home.md#terms-and-conditions) Origini.

Questa esercitazione fornisce i passaggi per creare un connettore sorgente SFTP utilizzando l&#39;interfaccia utente della piattaforma.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standard con cui  Experience Platform organizza i dati sull&#39;esperienza dei clienti.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponete già di una connessione SFTP valida, potete ignorare il resto del documento e procedere all&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Raccogli credenziali richieste

Per connettersi a SFTP, è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Nome o indirizzo IP associato al server SFTP. |
| `username` | Il nome utente con accesso al server SFTP. |
| `password` | La password per il server SFTP. |
| `privateKeyContent` | Il contenuto della chiave privata SSH con codifica Base64. Formato della chiave privata SSH OpenSSH (RSA/DSA). |
| `passPhrase` | La frase di autorizzazione o la password per decifrare la chiave privata se il file chiave o il contenuto chiave sono protetti da una frase di autorizzazione. Se PrivateKeyContent è protetto da password, questo parametro deve essere utilizzato con la passphrase PrivateKeyContent come valore. |

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi descritti di seguito per creare un nuovo account SFTP per la connessione alla piattaforma.

## Connessione al server SFTP

Accedete ad [Adobe Experience Platform](https://platform.adobe.com) , quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39; [!UICONTROL Sources] area di lavoro. Nella [!UICONTROL Catalog] schermata sono visualizzate diverse sorgenti con cui è possibile creare un account in ingresso.

Potete selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l&#39;origine specifica con cui si desidera lavorare utilizzando l&#39;opzione di ricerca.

Sotto la [!UICONTROL Cloud storage] categoria, selezionare **[!UICONTROL SFTP]**. Se si tratta della prima volta che si utilizza questo connettore, selezionare **[!UICONTROL Configure]**. In caso contrario, selezionate **[!UICONTROL Add data]** per creare una nuova connessione SFTP.

![catalogo](../../../../images/tutorials/create/sftp/catalog.png)

Viene **[!UICONTROL Connect to SFTP]** visualizzata la pagina. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL New account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e le credenziali. Al termine, selezionare **[!UICONTROL Connect]** e quindi concedere un po&#39; di tempo per stabilire la nuova connessione.

Il connettore SFTP fornisce diversi tipi di autenticazione per l&#39;accesso. In **[!UICONTROL Account authentication]** selezionare **[!UICONTROL Password]** per utilizzare una credenziale basata su password.

![connect-password](../../../../images/tutorials/create/sftp/password.png)

In alternativa, puoi selezionare la chiave **[pubblica]** SSH e collegare il tuo account SFTP utilizzando una combinazione di [!UICONTROL Private key content] e [!UICONTROL Passphrase].

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

Seguendo questa esercitazione hai stabilito una connessione al tuo account FTP o SFTP. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per trasferire i dati dall’archiviazione cloud alla piattaforma](../../dataflow/batch/cloud-storage.md).