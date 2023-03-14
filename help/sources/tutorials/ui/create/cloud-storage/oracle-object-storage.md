---
keywords: Experience Platform;home;argomenti popolari;Oracle archiviazione oggetti;oracle archiviazione oggetti
solution: Experience Platform
title: Creare un Oracle di connessione sorgente archiviazione oggetti nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione sorgente di archiviazione oggetti di Oracle utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 32284163-5dde-4171-8977-f76ceeebcef2
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---

# Creare un [!DNL Oracle Object Storage] Connessione sorgente nell’interfaccia utente

Questo tutorial descrive i passaggi necessari per creare [!DNL Oracle Object Storage] connessione sorgente tramite l’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../../../home.md): un Experience Platform consente di acquisire dati da varie origini, consentendoti allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che permettono di suddividere una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

### Raccogli le credenziali richieste

Accedi per connettersi a [!DNL Oracle Object Storage], è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `serviceUrl` | Il [!DNL Oracle Object Storage] endpoint necessario per l&#39;autenticazione. Il formato dell’endpoint è: `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | Il [!DNL Oracle Object Storage] ID della chiave di accesso richiesto per l’autenticazione. |
| `secretKey` | Il [!DNL Oracle Object Storage] password richiesta per l&#39;autenticazione. |
| `bucketName` | Il nome del bucket consentito è necessario se l’utente dispone di accesso limitato. Il nome del bucket deve contenere tra tre e 63 caratteri, deve iniziare e terminare con una lettera o un numero e può contenere solo lettere minuscole, numeri o trattini (`-`). Il nome del bucket non può essere formattato come un indirizzo IP. |
| `folderPath` | Il percorso della cartella consentito è necessario se l’utente ha limitato l’accesso. |

Per ulteriori informazioni su come ottenere questi valori, consulta [Guida all’autenticazione di Oracle Object Storage](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

Dopo aver raccolto le credenziali richieste, puoi creare un nuovo account Oracle Object Storage per connettersi a Platform seguendo la procedura riportata di seguito.

## Connessione a Oracle Object Storage

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Il [!UICONTROL Catalogo] Nella schermata vengono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la fonte specifica che si desidera utilizzare utilizzando la barra di ricerca.

Sotto [!UICONTROL Archiviazione cloud] categoria, seleziona **[!UICONTROL Oracle archiviazione oggetti]** e quindi seleziona **[!UICONTROL Aggiungi dati]**.

![catalogo](../../../../images/tutorials/create/oracle-object-storage/catalog.png)

### Account esistente

Per utilizzare un account esistente, seleziona la [!DNL Oracle Object Storage] account con cui vuoi creare un nuovo flusso di dati, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![esistente](../../../../images/tutorials/create/oracle-object-storage/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci un nome, una descrizione facoltativa e il tuo [!DNL Oracle Object Storage] credenziali. Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![nuovo](../../../../images/tutorials/create/oracle-object-storage/new.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione con il tuo [!DNL Oracle Object Storage] account. Ora puoi passare alla prossima esercitazione su [configurazione di un flusso di dati per portare i dati dall’archiviazione cloud a Platform](../../dataflow/batch/cloud-storage.md).
