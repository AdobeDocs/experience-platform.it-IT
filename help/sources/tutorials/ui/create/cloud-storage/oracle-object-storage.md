---
keywords: Experience Platform;home;argomenti popolari;Oracle archiviazione oggetti;oracle archiviazione oggetti
solution: Experience Platform
title: Creare un Oracle di connessione Source Object Storage nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione sorgente di archiviazione oggetti di Oracle utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 32284163-5dde-4171-8977-f76ceeebcef2
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 1%

---

# Crea una connessione Source [!DNL Oracle Object Storage] nell&#39;interfaccia utente

Questo tutorial descrive i passaggi per la creazione di una connessione di origine [!DNL Oracle Object Storage] tramite l&#39;interfaccia utente di Adobe Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

### Raccogli le credenziali richieste

In per connettersi a [!DNL Oracle Object Storage], è necessario fornire i valori per le proprietà di connessione seguenti:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `serviceUrl` | Endpoint [!DNL Oracle Object Storage] richiesto per l&#39;autenticazione. Formato endpoint: `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | ID della chiave di accesso [!DNL Oracle Object Storage] richiesto per l&#39;autenticazione. |
| `secretKey` | La password [!DNL Oracle Object Storage] richiesta per l&#39;autenticazione. |
| `bucketName` | Il nome del bucket consentito è necessario se l’utente dispone di accesso limitato. Il nome del bucket deve contenere tra tre e 63 caratteri, deve iniziare e terminare con una lettera o un numero e può contenere solo lettere minuscole, numeri o trattini (`-`). Il nome del bucket non può essere formattato come un indirizzo IP. |
| `folderPath` | Il percorso della cartella consentito è necessario se l’utente ha limitato l’accesso. |

Per ulteriori informazioni su come ottenere questi valori, fare riferimento alla [Guida all&#39;autenticazione di Oracle Object Storage](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

Dopo aver raccolto le credenziali richieste, puoi creare un nuovo account Oracle Object Storage per connettersi a Platform seguendo la procedura riportata di seguito.

## Connessione a Oracle Object Storage

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Nella schermata [!UICONTROL Catalogo] sono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la fonte specifica che si desidera utilizzare utilizzando la barra di ricerca.

Nella categoria [!UICONTROL Archiviazione cloud], seleziona **[!UICONTROL Archiviazione oggetti Oracle]**, quindi seleziona **[!UICONTROL Aggiungi dati]**.

![catalogo](../../../../images/tutorials/create/oracle-object-storage/catalog.png)

### Account esistente

Per utilizzare un account esistente, seleziona l&#39;account [!DNL Oracle Object Storage] con cui vuoi creare un nuovo flusso di dati, quindi seleziona **[!UICONTROL Successivo]** per continuare.

![esistente](../../../../images/tutorials/create/oracle-object-storage/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci un nome, una descrizione facoltativa e le tue credenziali di [!DNL Oracle Object Storage]. Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![nuovo](../../../../images/tutorials/create/oracle-object-storage/new.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL Oracle Object Storage]. Ora puoi passare alla prossima esercitazione su [configurazione di un flusso di dati per portare dati dall&#39;archiviazione cloud in Platform](../../dataflow/batch/cloud-storage.md).
