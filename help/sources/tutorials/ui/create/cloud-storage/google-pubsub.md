---
keywords: ' Experience Platform;casa;argomenti popolari;Google PubSub;google pubsub'
solution: Experience Platform
title: Creare una connessione Google PubSub Source nell'interfaccia utente
topic: ' - Panoramica'
type: Tutorial
description: Scoprite come creare un connettore sorgente Google PubSub utilizzando l'interfaccia utente della piattaforma.
translation-type: tm+mt
source-git-commit: 0af90253f04377149986aedf2e9d3012ca06d4f8
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 1%

---


# Creare una connessione di origine [!DNL Google PubSub] nell&#39;interfaccia utente

>[!NOTE]
>
> Il connettore [!DNL Google PubSub] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, vedere [Panoramica delle sorgenti](../../../../home.md#terms-and-conditions).

Questa esercitazione fornisce i passaggi necessari per creare un [!DNL Google PubSub] (in seguito denominato &quot;[!DNL PubSub]&quot;) utilizzando l&#39;interfaccia utente della piattaforma.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md):  Experience Platform consente l&#39;acquisizione di dati da varie fonti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Piattaforma.
* [Sandbox](../../../../../sandboxes/home.md):  Experience Platform fornisce sandbox virtuali che dividono una singola istanza della piattaforma in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Se si dispone già di una connessione [!DNL PubSub] valida, è possibile ignorare il resto del documento e procedere all&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Raccogli credenziali richieste

Per connettere [!DNL PubSub] alla piattaforma, è necessario fornire un valore valido per le seguenti credenziali:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `projectId` | L&#39;ID progetto necessario per l&#39;autenticazione [!DNL PubSub]. |
| `credentials` | La credenziale o la chiave necessaria per autenticare [!DNL PubSub]. |

Per ulteriori informazioni su questi valori, consultare il seguente documento [PubSub authentication](https://cloud.google.com/pubsub/docs/authentication).

Dopo aver raccolto le credenziali necessarie, puoi seguire i passaggi descritti di seguito per collegare l&#39;account [!DNL Blob] alla piattaforma.

## Collegare l&#39;account [!DNL PubSub]

Nell&#39; [interfaccia utente della piattaforma](https://platform.adobe.com), selezionare **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Sources]. Nella schermata [!UICONTROL Catalog] sono visualizzate diverse sorgenti con le quali è possibile creare un account.

Potete selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, potete trovare l’origine specifica con cui desiderate lavorare utilizzando la barra di ricerca.

Sotto la categoria [!UICONTROL Cloud storage], selezionare **[!UICONTROL Google PubSub]**, quindi selezionare **[!UICONTROL Add data]**.

![catalogo](../../../../images/tutorials/create/google-pubsub/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connect to Google PubSub]**. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Account esistente

Per utilizzare un account esistente, selezionare l&#39;account [!DNL PubSub] con cui si desidera creare un nuovo flusso di dati, quindi selezionare **[!UICONTROL Next]** per continuare.

![esistenti](../../../../images/tutorials/create/google-pubsub/existing.png)

### Nuovo account

Se si sta creando un nuovo account, selezionare **[!UICONTROL New account]**, quindi specificare un nome, una descrizione facoltativa e le credenziali di autenticazione [!DNL PubSub] nel modulo di input. Al termine, selezionare **[!UICONTROL Connect to source]**, quindi concedere un po&#39; di tempo per stabilire la nuova connessione.

![new](../../../../images/tutorials/create/google-pubsub/new.png)

## Passaggi successivi

Seguendo questa esercitazione, è possibile creare una connessione tra l&#39;account [!DNL PubSub] e la piattaforma. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per portare i dati di streaming dall&#39;archiviazione cloud nella piattaforma](../../dataflow/streaming/cloud-storage-streaming.md).
