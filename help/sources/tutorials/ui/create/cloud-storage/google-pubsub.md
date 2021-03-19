---
keywords: Experience Platform;home;argomenti popolari;Google PubSub;google pubsub
solution: Experience Platform
title: Creare una connessione Google PubSub Source nell'interfaccia utente
topic: ' - Panoramica'
type: Tutorial
description: Scopri come creare un connettore sorgente Google PubSub utilizzando l’interfaccia utente di Platform.
translation-type: tm+mt
source-git-commit: b5358ce206888c413035b46fe751520fd9aefb14
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 1%

---


# Creare una connessione sorgente [!DNL Google PubSub] nell&#39;interfaccia utente

>[!NOTE]
>
> Il connettore [!DNL Google PubSub] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la [Panoramica delle sorgenti](../../../../home.md#terms-and-conditions) .

Questa esercitazione descrive i passaggi necessari per creare un [!DNL Google PubSub] (in seguito denominato &quot;[!DNL PubSub]&quot;) utilizzando l’interfaccia utente di Platform.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): L’Experience Platform consente di acquisire dati da varie sorgenti e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Se disponi già di una connessione [!DNL PubSub] valida, puoi saltare il resto del documento e continuare l&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Raccogli credenziali richieste

Per connettersi a [!DNL PubSub] Platform, è necessario fornire un valore valido per le seguenti credenziali:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `projectId` | L&#39;ID del progetto necessario per l&#39;autenticazione [!DNL PubSub]. |
| `credentials` | L&#39;ID della chiave privata o credenziale necessario per l&#39;autenticazione [!DNL PubSub]. |

Per ulteriori informazioni su questi valori, consulta il seguente documento [PubSub authentication](https://cloud.google.com/pubsub/docs/authentication) . Se utilizzi l&#39;autenticazione basata sull&#39;account del servizio, consulta la seguente [Guida PubSub](https://cloud.google.com/docs/authentication/production#create_service_account) per i passaggi su come generare le credenziali.

>[!TIP]
>
>Se utilizzi l’autenticazione basata sull’account del servizio, assicurati di aver concesso un accesso utente sufficiente all’account del servizio e che non vi siano spazi bianchi aggiuntivi nel JSON durante la copia e l’incolla delle credenziali.

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per collegare il tuo account [!DNL PubSub] a Platform.

## Connetti il tuo account [!DNL PubSub]

Nella [Interfaccia utente della piattaforma](https://platform.adobe.com), seleziona **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all’area di lavoro [!UICONTROL Sources]. Nella schermata [!UICONTROL Catalog] sono visualizzate diverse origini per le quali è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando la barra di ricerca.

Sotto la categoria [!UICONTROL Cloud storage], selezionare **[!UICONTROL Google PubSub]**, quindi selezionare **[!UICONTROL Add data]**.

![catalogo](../../../../images/tutorials/create/google-pubsub/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connect to Google PubSub]** . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, selezionare l&#39;account [!DNL PubSub] con cui si desidera creare un nuovo flusso di dati, quindi selezionare **[!UICONTROL Next]** per continuare.

![esistente](../../../../images/tutorials/create/google-pubsub/existing.png)

### Nuovo account

Se si sta creando un nuovo account, selezionare **[!UICONTROL New account]**, quindi specificare un nome, una descrizione facoltativa e le credenziali di autenticazione [!DNL PubSub] nel modulo di input. Al termine, selezionare **[!UICONTROL Connect to source]** e quindi concedere un po&#39; di tempo per l&#39;impostazione della nuova connessione.

![nuovo](../../../../images/tutorials/create/google-pubsub/new.png)

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione tra l’account [!DNL PubSub] e Platform. Ora puoi continuare l’esercitazione successiva e [configurare un flusso di dati per portare i dati in streaming dall’archiviazione cloud in Platform](../../dataflow/streaming/cloud-storage-streaming.md).
