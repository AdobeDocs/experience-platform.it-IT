---
keywords: Experience Platform;home;argomenti comuni;archiviazione oggetti Oracle;archiviazione oggetti oracle
solution: Experience Platform
title: Creare una connessione di Oracle dell’origine di archiviazione degli oggetti nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione sorgente Oracle Object Storage utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 32284163-5dde-4171-8977-f76ceeebcef2
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---

# Crea un [!DNL Oracle Object Storage] Connessione sorgente nell’interfaccia utente

Questa esercitazione descrive i passaggi necessari per creare un [!DNL Oracle Object Storage] connessione sorgente tramite l’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): L’Experience Platform consente di acquisire dati da varie sorgenti e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

### Raccogli credenziali richieste

In per connettersi a [!DNL Oracle Object Storage], è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `serviceUrl` | La [!DNL Oracle Object Storage] endpoint necessario per l&#39;autenticazione. Il formato dell&#39;endpoint è: `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | La [!DNL Oracle Object Storage] ID chiave di accesso richiesto per l&#39;autenticazione. |
| `secretKey` | La [!DNL Oracle Object Storage] password necessaria per l&#39;autenticazione. |
| `bucketName` | Il nome del bucket consentito richiesto se l’utente ha accesso limitato. Il nome del bucket deve essere lungo tra i tre e i 63 caratteri, deve iniziare e terminare con una lettera o un numero e può contenere solo lettere minuscole, numeri o trattini (`-`). Impossibile formattare il nome del bucket come indirizzo IP. |
| `folderPath` | Percorso della cartella consentito richiesto se l&#39;utente dispone di accesso limitato. |

Per ulteriori informazioni su come ottenere questi valori, consulta la [Guida all’autenticazione di Oracle Object Storage](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per creare un nuovo account Oracle Object Storage per la connessione a Platform.

## Connettersi all&#39;archiviazione oggetti Oracle

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla navigazione a sinistra per accedere al [!UICONTROL Origini] workspace. La [!UICONTROL Catalogo] in questa schermata vengono visualizzate diverse sorgenti con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando la barra di ricerca.

Sotto la [!UICONTROL archiviazione cloud] categoria, seleziona **[!UICONTROL Archiviazione oggetti Oracle]** quindi seleziona **[!UICONTROL Aggiungi dati]**.

![catalogo](../../../../images/tutorials/create/oracle-object-storage/catalog.png)

### Account esistente

Per utilizzare un account esistente, seleziona la [!DNL Oracle Object Storage] account con cui si desidera creare un nuovo flusso di dati, quindi selezionare **[!UICONTROL Successivo]** per procedere.

![esistente](../../../../images/tutorials/create/oracle-object-storage/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci un nome, una descrizione facoltativa e [!DNL Oracle Object Storage] credenziali. Al termine, seleziona **[!UICONTROL Connetti alla sorgente]** e quindi lasciare un po&#39; di tempo per stabilire la nuova connessione.

![nuovo](../../../../images/tutorials/create/oracle-object-storage/new.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo [!DNL Oracle Object Storage] conto. Ora puoi passare all’esercitazione successiva su [configurazione di un flusso di dati per l’importazione di dati dall’archiviazione cloud in Platform](../../dataflow/batch/cloud-storage.md).
