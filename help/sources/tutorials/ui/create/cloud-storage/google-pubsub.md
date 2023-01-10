---
keywords: Experience Platform;home;argomenti popolari;Google PubSub;google pubsub
solution: Experience Platform
title: Creare una connessione Google PubSub Source nell'interfaccia utente
type: Tutorial
description: Scopri come creare un connettore sorgente Google PubSub utilizzando l’interfaccia utente di Platform.
exl-id: fb8411f2-ccae-4bb5-b1bf-52b1144534ed
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 1%

---

# Crea un [!DNL Google PubSub] connessione sorgente nell’interfaccia utente

Questa esercitazione fornisce i passaggi per la creazione di un [!DNL Google PubSub] (in appresso denominato &quot;[!DNL PubSub]&quot;) utilizzando l’interfaccia utente di Platform.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): L’Experience Platform consente di acquisire dati da varie sorgenti e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Se disponi già di una [!DNL PubSub] è possibile ignorare il resto del documento e passare all&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Raccogli credenziali richieste

Per connettersi [!DNL PubSub] su Platform, devi fornire un valore valido per le seguenti credenziali:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `projectId` | ID progetto necessario per l&#39;autenticazione [!DNL PubSub]. |
| `credentials` | ID della credenziale o della chiave privata necessaria per l&#39;autenticazione [!DNL PubSub]. |

Per ulteriori informazioni su questi valori, consulta quanto segue [Autenticazione PubSub](https://cloud.google.com/pubsub/docs/authentication) documento. Se utilizzi l’autenticazione basata sull’account del servizio, consulta quanto segue [Guida di PubSub](https://cloud.google.com/docs/authentication/production#create_service_account) per i passaggi su come generare le credenziali.

>[!TIP]
>
>Se utilizzi l’autenticazione basata sull’account del servizio, assicurati di aver concesso un accesso utente sufficiente all’account del servizio e che non vi siano spazi bianchi aggiuntivi nel JSON durante la copia e l’incolla delle credenziali.

Una volta raccolte le credenziali richieste, puoi seguire i passaggi seguenti per collegare il tuo [!DNL PubSub] a Platform.

## Collega il tuo [!DNL PubSub] account

In [Interfaccia utente della piattaforma](https://platform.adobe.com), seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Origini] workspace. La [!UICONTROL Catalogo] in questa schermata vengono visualizzate diverse sorgenti per le quali è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando la barra di ricerca.

Sotto la [!UICONTROL archiviazione cloud] categoria, seleziona **[!UICONTROL Google PubSub]**, quindi seleziona **[!UICONTROL Aggiungi dati]**.

![catalogo](../../../../images/tutorials/create/google-pubsub/catalog.png)

La **[!UICONTROL Connetti a Google PubSub]** viene visualizzata la pagina . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona la [!DNL PubSub] account con cui si desidera creare un nuovo flusso di dati, quindi selezionare **[!UICONTROL Successivo]** per procedere.

![esistente](../../../../images/tutorials/create/google-pubsub/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci un nome, una descrizione facoltativa e [!DNL PubSub] credenziali di autenticazione nel modulo di input. Al termine, seleziona **[!UICONTROL Connetti alla sorgente]** e quindi lasciare un po&#39; di tempo per stabilire la nuova connessione.

![nuovo](../../../../images/tutorials/create/google-pubsub/new.png)

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione tra [!DNL PubSub] account e piattaforma. Ora puoi passare all’esercitazione successiva e [configurare un flusso di dati per portare i dati in streaming dall’archiviazione cloud in Platform](../../dataflow/streaming/cloud-storage-streaming.md).
