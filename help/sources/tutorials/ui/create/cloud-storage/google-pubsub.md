---
title: Creare una connessione Google PubSub Source nell'interfaccia utente
description: Scopri come creare un connettore di origine Google PubSub utilizzando l’interfaccia utente di Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: fb8411f2-ccae-4bb5-b1bf-52b1144534ed
source-git-commit: fcac805e151d6142886eb8e05da0eb1babad2f69
workflow-type: tm+mt
source-wordcount: '1098'
ht-degree: 1%

---

# Crea una connessione sorgente [!DNL Google PubSub] nell&#39;interfaccia utente

>[!IMPORTANT]
>
>L&#39;origine [!DNL Google PubSub] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-time Customer Data Platform Ultimate.

Questo tutorial descrive i passaggi necessari per creare [!DNL Google PubSub] (di seguito &quot;[!DNL PubSub]&quot;) utilizzando l&#39;interfaccia utente di Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Se disponi già di una connessione [!DNL PubSub] valida, puoi saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Raccogli le credenziali richieste

Per connettere l&#39;account [!DNL PubSub] all&#39;Experience Platform, è necessario fornire i valori per le proprietà di connessione descritte di seguito. Per ulteriori informazioni sull&#39;autenticazione e sulla configurazione dei prerequisiti, leggere la [[!DNL PubSub source] panoramica](../../../../connectors/cloud-storage/google-pubsub.md#prerequisites).


>[!BEGINTABS]

>[!TAB Autenticazione basata su progetto]

| Credenziali | Descrizione |
| --- | --- |
| ID Progetto | ID progetto richiesto per autenticare [!DNL PubSub]. |
| Credenziali | Credenziali necessarie per autenticare [!DNL PubSub]. Assicurati di inserire il file JSON completo dopo aver rimosso gli spazi vuoti dalle credenziali. |

>[!TAB Autenticazione basata su argomenti e sottoscrizioni]

| Credenziali | Descrizione |
| --- | --- |
| Credenziali | Credenziali necessarie per autenticare [!DNL PubSub]. Assicurati di inserire il file JSON completo dopo aver rimosso gli spazi vuoti dalle credenziali. |
| Nome argomento | Nome dell&#39;abbonamento [!DNL PubSub]. In [!DNL PubSub], gli abbonamenti consentono di ricevere messaggi, sottoscrivendo l&#39;argomento in cui i messaggi sono stati pubblicati. **Nota**: è possibile utilizzare una singola sottoscrizione [!DNL PubSub] per un solo flusso di dati. Per creare più flussi di dati, devi disporre di più abbonamenti. |
| Nome abbonamento | Nome dell&#39;abbonamento [!DNL PubSub]. In [!DNL PubSub], gli abbonamenti consentono di ricevere messaggi, sottoscrivendo l&#39;argomento in cui i messaggi sono stati pubblicati. |

>[!ENDTABS]

Per ulteriori informazioni su questi valori, consulta il seguente documento di [autenticazione PubSub](https://cloud.google.com/pubsub/docs/authentication). Se utilizzi l&#39;autenticazione basata sull&#39;account del servizio, consulta la [Guida PubSub](https://cloud.google.com/docs/authentication/production#create_service_account) seguente per i passaggi su come generare le credenziali.

>[!TIP]
>
>Se utilizzi l’autenticazione basata sull’account del servizio, assicurati di aver concesso un accesso utente sufficiente all’account del servizio e di non inserire spazi vuoti aggiuntivi nel JSON quando copi e incolla le credenziali.

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per collegare l&#39;account [!DNL PubSub] a Platform.

## Connetti il tuo account [!DNL PubSub]

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Nella schermata [!UICONTROL Catalogo] sono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria [!UICONTROL Archiviazione cloud], seleziona **[!UICONTROL Google PubSub]**, quindi seleziona **[!UICONTROL Aggiungi dati]**.

![Catalogo delle origini nell&#39;interfaccia utente di Experience Platform.](../../../../images/tutorials/create/google-pubsub/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti a Google PubSub]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona l&#39;account [!DNL PubSub] con cui vuoi creare un nuovo flusso di dati, quindi seleziona **[!UICONTROL Successivo]** per continuare.

![La selezione dell&#39;account esistente nel flusso di lavoro di origine.](../../../../images/tutorials/create/google-pubsub/existing.png)

### Nuovo account

>[!TIP]
>
>* Quando crei un account con accesso limitato, devi fornire almeno uno dei tuoi nomi di argomento o di abbonamento. L’autenticazione non riuscirà se mancano entrambi i valori.
>* Una volta creata, non è possibile modificare il tipo di autenticazione di una connessione di base [!DNL Google PubSub]. Per modificare il tipo di autenticazione, è necessario creare una nuova connessione di base.

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci un nome e una descrizione facoltativa per il nuovo account [!DNL PubSub].

![Nuova interfaccia account per l&#39;origine Google PubSub nel flusso di lavoro delle origini](../../../../images/tutorials/create/google-pubsub/new.png)

L&#39;origine [!DNL PubSub] consente di specificare il tipo di accesso da consentire durante l&#39;autenticazione. Puoi impostare l’account in modo che disponga di autenticazione basata su progetto o su argomento e autenticazione basata su abbonamento. L&#39;autenticazione basata sul progetto consente di concedere l&#39;accesso al progetto a livello di radice nel proprio account, mentre l&#39;autenticazione basata su argomenti e sottoscrizioni consente di limitare l&#39;accesso a un particolare argomento e sottoscrizione [!DNL PubSub].

>[!BEGINTABS]

>[!TAB Autenticazione basata su progetto]

Per creare un account con accesso alla cartella principale del progetto [!DNL PubSub]. Seleziona **[!UICONTROL Credenziali di autenticazione Google PubSub]** come tipo di autenticazione e fornisci l&#39;ID progetto e le credenziali. Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![Nuova interfaccia account per l&#39;origine Google PubSub con accesso alla directory principale selezionato.](../../../../images/tutorials/create/google-pubsub/root.png)

>[!TAB Autenticazione basata su argomenti e sottoscrizioni]

Per creare un account con accesso limitato solo a un argomento e a una sottoscrizione [!DNL PubSub] specifici, selezionare **[!UICONTROL Credenziali di autenticazione con ambito pubSub di Google]**, quindi specificare le credenziali, il nome dell&#39;argomento e/o il nome della sottoscrizione. Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![Nuova interfaccia account per l&#39;origine Google PubSub con accesso con ambito selezionato.](../../../../images/tutorials/create/google-pubsub/scoped.png)

>[!ENDTABS]

>[!NOTE]
>
>Le entità (ruoli) assegnate a un progetto [!DNL PubSub] vengono ereditate in tutti gli argomenti e le sottoscrizioni creati all&#39;interno di un progetto [!DNL PubSub]. Se si desidera che un&#39;entità principale (ruolo) abbia accesso a un argomento specifico, è necessario aggiungere anche tale entità principale (ruolo) alla sottoscrizione corrispondente dell&#39;argomento. Per ulteriori informazioni, leggere la [[!DNL PubSub] documentazione sul controllo degli accessi](<https://cloud.google.com/pubsub/docs/access-control>).

## Selezionare i dati

Se l&#39;autenticazione ha esito positivo, viene visualizzato il passaggio [!UICONTROL Seleziona dati], in cui è possibile spostarsi nella gerarchia dei dati di [!DNL PubSub] e selezionare i dati da portare in Experience Platform.

>[!BEGINTABS]

>[!TAB Autenticazione basata su progetto]

Se hai eseguito l&#39;autenticazione con l&#39;accesso basato su progetto, nell&#39;interfaccia [!UICONTROL Seleziona dati] verranno visualizzate tutte le sottoscrizioni del progetto a cui è associato un argomento.

![Il passaggio di dati di selezione del flusso di lavoro origini con autenticazione basata su progetto.](../../../../images/tutorials/create/google-pubsub/root-folders.png)

>[!TAB Autenticazione basata su argomenti e sottoscrizioni]

Se hai eseguito l&#39;autenticazione con un argomento e un accesso basato su abbonamento, la visualizzazione dell&#39;interfaccia [!UICONTROL Seleziona dati] può variare a seconda delle informazioni fornite.

* Se si specifica solo il nome dell&#39;argomento, nell&#39;interfaccia verranno visualizzate tutte le coppie di argomenti-sottoscrizione corrispondenti all&#39;argomento specificato.
* Se fornisci solo il nome dell’abbonamento, l’interfaccia visualizza tutte le coppie di argomenti-abbonamento che corrispondono al nome dell’abbonamento fornito.
* Se vengono forniti sia i nomi degli argomenti che quelli delle sottoscrizioni, l&#39;interfaccia visualizza la coppia argomento-sottoscrizione che corrisponde a entrambi i valori specificati.

![Il passaggio di dati di selezione del flusso di lavoro origini con l&#39;argomento e l&#39;autenticazione basata su sottoscrizione.](../../../../images/tutorials/create/google-pubsub/scoped-folders.png)

>[!ENDTABS]

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione tra il tuo account [!DNL PubSub] e Platform. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per portare dati in streaming dall&#39;archiviazione cloud in Platform](../../dataflow/streaming/cloud-storage-streaming.md).
