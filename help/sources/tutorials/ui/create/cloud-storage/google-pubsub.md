---
title: Creare una connessione sorgente PubSub di Google nell’interfaccia utente
description: Scopri come creare un connettore di origine Google PubSub utilizzando l’interfaccia utente di Platform.
exl-id: fb8411f2-ccae-4bb5-b1bf-52b1144534ed
source-git-commit: 2b72d384e8edd91c662364dfac31ce4edff79172
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 1%

---

# Creare un [!DNL Google PubSub] connessione sorgente nell’interfaccia utente

Questo tutorial descrive i passaggi necessari per creare [!DNL Google PubSub] (in seguito denominati &quot;[!DNL PubSub]&quot;) tramite l’interfaccia utente di Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../../../home.md): un Experience Platform consente di acquisire dati da varie origini, consentendoti allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che permettono di suddividere una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Se disponi già di un [!DNL PubSub] connessione, è possibile saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Raccogli le credenziali richieste

Per connettersi [!DNL PubSub] In Platform, devi fornire un valore valido per le seguenti credenziali:

| Credenziali | Descrizione |
| ---------- | ----------- |
| Progetto ID | ID progetto richiesto per l’autenticazione [!DNL PubSub]. |
| Credenziali  | ID della chiave privata o delle credenziali richiesto per l&#39;autenticazione [!DNL PubSub]. |
| ID argomento | ID per [!DNL PubSub] risorsa che rappresenta un feed di messaggi. È necessario specificare un ID argomento se si desidera fornire l&#39;accesso a un flusso di dati specifico nel [!DNL Google PubSub] sorgente. |
| ID abbonamento | L’ID del tuo [!DNL PubSub] abbonamento. In entrata [!DNL PubSub], gli abbonamenti ti consentono di ricevere messaggi, abbonandoti all’argomento in cui i messaggi sono stati pubblicati in. |

Per ulteriori informazioni su questi valori, vedi quanto segue [Autenticazione PubSub](https://cloud.google.com/pubsub/docs/authentication) documento. Se si utilizza l&#39;autenticazione basata sull&#39;account del servizio, vedere [Guida di PubSub](https://cloud.google.com/docs/authentication/production#create_service_account) per i passaggi su come generare le credenziali.

>[!TIP]
>
>Se utilizzi l’autenticazione basata sull’account del servizio, assicurati di aver concesso un accesso utente sufficiente all’account del servizio e di non inserire spazi vuoti aggiuntivi nel JSON quando copi e incolla le credenziali.

Dopo aver raccolto le credenziali richieste, puoi seguire la procedura riportata di seguito per collegare il tuo [!DNL PubSub] da un account a Platform.

## Connetti [!DNL PubSub] account

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Il [!UICONTROL Catalogo] Nella schermata vengono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Sotto [!UICONTROL Archiviazione cloud] categoria, seleziona **[!UICONTROL Google PubSub]**, quindi selezionare **[!UICONTROL Aggiungi dati]**.

![Catalogo delle origini nell’interfaccia utente di Experience Platform.](../../../../images/tutorials/create/google-pubsub/catalog.png)

Il **[!UICONTROL Connetti a Google PubSub]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona la [!DNL PubSub] account con cui vuoi creare un nuovo flusso di dati, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![La selezione dell’account esistente nel flusso di lavoro sorgenti.](../../../../images/tutorials/create/google-pubsub/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci un nome, una descrizione facoltativa e il tuo [!DNL PubSub] credenziali di autenticazione nel modulo di input. Durante questo passaggio, puoi definire i dati a cui il tuo account ha accesso fornendo un ID argomento. Solo gli abbonamenti associati a tale ID argomento saranno accessibili.

>[!NOTE]
>
>Le entità (ruoli) assegnate a un progetto pubsub vengono ereditate in tutti gli argomenti e le sottoscrizioni creati all&#39;interno di un [!DNL PubSub] progetto. Se si desidera aggiungere un&#39;entità principale (ruolo) per poter accedere a un argomento specifico, è necessario aggiungere anche tale entità principale (ruolo) alla sottoscrizione corrispondente dell&#39;argomento. Per ulteriori informazioni, leggere [[!DNL PubSub] documentazione sul controllo degli accessi](https://cloud.google.com/pubsub/docs/access-control).

Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![La nuova interfaccia account nel flusso di lavoro origini.](../../../../images/tutorials/create/google-pubsub/new.png)

## Passaggi successivi

Seguendo questa esercitazione, è possibile creare una connessione tra [!DNL PubSub] e Platform. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per portare i dati in streaming dall’archiviazione cloud a Platform](../../dataflow/streaming/cloud-storage-streaming.md).
