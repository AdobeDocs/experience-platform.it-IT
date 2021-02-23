---
keywords: ' Experience Platform;home;argomenti più comuni; Archiviazione oggetti Oracli; archiviazione oggetti oracle'
solution: Experience Platform
title: Creare una connessione di origine archivio oggetti  Oracle nell'interfaccia utente
topic: ' - Panoramica'
type: Tutorial
description: Scoprite come creare una connessione di origine Archiviazione oggetto  Oracle utilizzando l'interfaccia utente di Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: c1453a9f0be42f834d35af871051324df8dadf80
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 1%

---


# Creare una connessione di origine [!DNL Oracle Object Storage] nell&#39;interfaccia utente

Questa esercitazione fornisce i passaggi necessari per creare una connessione di origine [!DNL Oracle Object Storage] utilizzando l&#39;interfaccia utente di Adobe Experience Platform.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md):  Experience Platform consente l&#39;acquisizione di dati da varie fonti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Piattaforma.
* [Sandbox](../../../../../sandboxes/home.md):  Experience Platform fornisce sandbox virtuali che dividono una singola istanza della piattaforma in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

### Raccogli credenziali richieste

Per connettersi a [!DNL Oracle Object Storage], è necessario fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `serviceUrl` | L&#39;endpoint [!DNL Oracle Object Storage] richiesto per l&#39;autenticazione. Il formato dell&#39;endpoint è: `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | ID chiave di accesso [!DNL Oracle Object Storage] richiesto per l&#39;autenticazione. |
| `secretKey` | La [!DNL Oracle Object Storage] password necessaria per l&#39;autenticazione. |
| `bucketName` | Il nome del bucket consentito richiesto se l&#39;utente dispone di un accesso limitato. Il nome del bucket deve essere compreso tra tre e 63 caratteri, deve iniziare e terminare con una lettera o un numero e può contenere solo lettere minuscole, numeri o trattini (`-`). Impossibile formattare il nome del bucket come indirizzo IP. |
| `folderPath` | Percorso della cartella consentito richiesto se l&#39;utente ha limitato l&#39;accesso. |

Per ulteriori informazioni su come ottenere questi valori, fare riferimento alla [ Guida all&#39;autenticazione dell&#39;archiviazione oggetti di Oracle](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

Dopo aver raccolto le credenziali necessarie, è possibile seguire i passaggi descritti di seguito per creare un nuovo account di archiviazione oggetti  Oracle da connettere alla piattaforma.

## Connetti a  archivio oggetti Oracle

Nell&#39;interfaccia utente della piattaforma, selezionare **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Sources]. Nella schermata [!UICONTROL Catalog] sono visualizzate diverse sorgenti con cui è possibile creare un account.

Potete selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, potete trovare l’origine specifica con cui desiderate lavorare utilizzando la barra di ricerca.

Sotto la categoria [!UICONTROL Cloud storage], selezionare **[!UICONTROL Oracle Object Storage]**, quindi selezionare **[!UICONTROL Add data]**.

![catalogo](../../../../images/tutorials/create/oracle-object-storage/catalog.png)

### Account esistente

Per utilizzare un account esistente, selezionare l&#39;account [!DNL Oracle Object Storage] con cui si desidera creare un nuovo flusso di dati, quindi selezionare **[!UICONTROL Next]** per continuare.

![esistenti](../../../../images/tutorials/create/oracle-object-storage/existing.png)

### Nuovo account

Se state creando un nuovo account, selezionate **[!UICONTROL New account]**, quindi fornite un nome, una descrizione facoltativa e le vostre credenziali [!DNL Oracle Object Storage]. Al termine, selezionare **[!UICONTROL Connect to source]**, quindi concedere un po&#39; di tempo per stabilire la nuova connessione.

![new](../../../../images/tutorials/create/oracle-object-storage/new.png)

## Passaggi successivi

Seguendo questa esercitazione, è stata stabilita una connessione all&#39;account [!DNL Oracle Object Storage]. È ora possibile seguire l&#39;esercitazione successiva sulla [configurazione di un flusso di dati per trasferire i dati dall&#39;archiviazione cloud alla piattaforma ](../../dataflow/batch/cloud-storage.md).
