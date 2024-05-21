---
title: Creare una connessione sorgente PubSub di Google nell’interfaccia utente
description: Scopri come creare un connettore di origine Google PubSub utilizzando l’interfaccia utente di Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: fb8411f2-ccae-4bb5-b1bf-52b1144534ed
source-git-commit: fcac805e151d6142886eb8e05da0eb1babad2f69
workflow-type: tm+mt
source-wordcount: '1098'
ht-degree: 1%

---

# Creare un [!DNL Google PubSub] connessione sorgente nell’interfaccia utente

>[!IMPORTANT]
>
>Il [!DNL Google PubSub] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-time Customer Data Platform Ultimate.

Questo tutorial descrive i passaggi necessari per creare [!DNL Google PubSub] (in seguito denominati &quot;[!DNL PubSub]&quot;) tramite l’interfaccia utente di Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../../../home.md): un Experience Platform consente di acquisire dati da varie origini, consentendoti allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experienci Platform fornisce sandbox virtuali che permettono di suddividere una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Se disponi già di un [!DNL PubSub] connessione, è possibile saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Raccogli le credenziali richieste

È necessario fornire valori per le proprietà di connessione descritte di seguito per connettere il [!DNL PubSub] da Experience Platform. Per ulteriori informazioni sull&#39;autenticazione e sulla configurazione dei prerequisiti, consultare [[!DNL PubSub source] panoramica](../../../../connectors/cloud-storage/google-pubsub.md#prerequisites).


>[!BEGINTABS]

>[!TAB Autenticazione basata su progetto]

| Credenziali | Descrizione |
| --- | --- |
| ID Progetto | ID progetto richiesto per l’autenticazione [!DNL PubSub]. |
| Credenziali | Credenziali necessarie per l&#39;autenticazione [!DNL PubSub]. Assicurati di inserire il file JSON completo dopo aver rimosso gli spazi vuoti dalle credenziali. |

>[!TAB Autenticazione basata su argomenti e sottoscrizioni]

| Credenziali | Descrizione |
| --- | --- |
| Credenziali | Credenziali necessarie per l&#39;autenticazione [!DNL PubSub]. Assicurati di inserire il file JSON completo dopo aver rimosso gli spazi vuoti dalle credenziali. |
| Nome argomento | Il nome del tuo [!DNL PubSub] abbonamento. In entrata [!DNL PubSub], gli abbonamenti ti consentono di ricevere messaggi, abbonandoti all’argomento in cui i messaggi sono stati pubblicati in. **Nota**: un singolo [!DNL PubSub] l’abbonamento può essere utilizzato per un solo flusso di dati. Per creare più flussi di dati, devi disporre di più abbonamenti. |
| Nome abbonamento | Il nome del tuo [!DNL PubSub] abbonamento. In entrata [!DNL PubSub], gli abbonamenti ti consentono di ricevere messaggi, abbonandoti all’argomento in cui i messaggi sono stati pubblicati in. |

>[!ENDTABS]

Per ulteriori informazioni su questi valori, vedi quanto segue [Autenticazione PubSub](https://cloud.google.com/pubsub/docs/authentication) documento. Se si utilizza l&#39;autenticazione basata sull&#39;account del servizio, vedere [Guida di PubSub](https://cloud.google.com/docs/authentication/production#create_service_account) per i passaggi su come generare le credenziali.

>[!TIP]
>
>Se utilizzi l’autenticazione basata sull’account del servizio, assicurati di aver concesso un accesso utente sufficiente all’account del servizio e di non inserire spazi vuoti aggiuntivi nel JSON quando copi e incolla le credenziali.

Dopo aver raccolto le credenziali richieste, puoi seguire la procedura riportata di seguito per collegare il tuo [!DNL PubSub] da un account a Platform.

## Connetti [!DNL PubSub] account

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Il [!UICONTROL Catalogo] Nella schermata vengono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Sotto [!UICONTROL Archiviazione cloud] categoria, seleziona **[!UICONTROL Google PubSub]** e quindi selezionare **[!UICONTROL Aggiungi dati]**.

![Catalogo delle origini nell’interfaccia utente di Experienci Platform.](../../../../images/tutorials/create/google-pubsub/catalog.png)

Il **[!UICONTROL Connetti a Google PubSub]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona la [!DNL PubSub] account con cui vuoi creare un nuovo flusso di dati, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![La selezione dell’account esistente nel flusso di lavoro sorgenti.](../../../../images/tutorials/create/google-pubsub/existing.png)

### Nuovo account

>[!TIP]
>
>* Quando crei un account con accesso limitato, devi fornire almeno uno dei tuoi nomi di argomento o di abbonamento. L’autenticazione non riuscirà se mancano entrambi i valori.
>* Una volta creato, non è possibile modificare il tipo di autenticazione di un [!DNL Google PubSub] connessione di base. Per modificare il tipo di autenticazione, è necessario creare una nuova connessione di base.

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]** e quindi fornisci un nome e una descrizione facoltativa per il nuovo [!DNL PubSub] account.

![Nuova interfaccia account per l&#39;origine PubSub di Google nel flusso di lavoro delle origini](../../../../images/tutorials/create/google-pubsub/new.png)

Il [!DNL PubSub] origine consente di specificare il tipo di accesso da consentire durante l&#39;autenticazione. Puoi impostare l’account in modo che disponga di autenticazione basata su progetto o su argomento e autenticazione basata su abbonamento. L’autenticazione basata sul progetto consente di concedere l’accesso al progetto a livello principale nel tuo account, mentre l’autenticazione basata su argomento e su sottoscrizione ti consente di limitare l’accesso a un particolare [!DNL PubSub] argomento e abbonamento.

>[!BEGINTABS]

>[!TAB Autenticazione basata su progetto]

Per creare un account con accesso alla directory principale [!DNL PubSub] cartella del progetto. Seleziona **[!UICONTROL Credenziali di autenticazione Google PubSub]** come tipo di autenticazione e fornisci l’ID progetto e le credenziali. Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![La nuova interfaccia dell&#39;account per l&#39;origine Google PubSub con l&#39;accesso root selezionato.](../../../../images/tutorials/create/google-pubsub/root.png)

>[!TAB Autenticazione basata su argomenti e sottoscrizioni]

Per creare un account con accesso limitato solo a un determinato [!DNL PubSub] argomento e abbonamento, seleziona **[!UICONTROL Credenziali di autenticazione con ambito PubSub di Google]** e quindi fornire le credenziali, il nome dell&#39;argomento e/o il nome dell&#39;abbonamento. Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![La nuova interfaccia dell&#39;account per l&#39;origine Google PubSub con l&#39;accesso con ambito selezionato.](../../../../images/tutorials/create/google-pubsub/scoped.png)

>[!ENDTABS]

>[!NOTE]
>
>Entità principale (ruoli) assegnata a un [!DNL PubSub] vengono ereditati in tutti gli argomenti e le sottoscrizioni creati all&#39;interno di un [!DNL PubSub] progetto. Se si desidera che un&#39;entità principale (ruolo) abbia accesso a un argomento specifico, è necessario aggiungere anche tale entità principale (ruolo) alla sottoscrizione corrispondente dell&#39;argomento. Per ulteriori informazioni, leggere [[!DNL PubSub] documentazione sul controllo degli accessi](<https://cloud.google.com/pubsub/docs/access-control>).

## Selezionare i dati

Se l’autenticazione viene eseguita correttamente, accedi al [!UICONTROL Seleziona dati] passaggio, in cui è possibile navigare tra [!DNL PubSub] gerarchia dei dati e selezionare i dati da portare all&#39;Experience Platform.

>[!BEGINTABS]

>[!TAB Autenticazione basata su progetto]

Se hai eseguito l’autenticazione con l’accesso basato su progetto, il [!UICONTROL Seleziona dati] L’interfaccia visualizzerà tutte le sottoscrizioni all’interno del progetto a cui è associato un argomento.

![Il passaggio di dati di selezione del flusso di lavoro sorgenti con autenticazione basata su progetto.](../../../../images/tutorials/create/google-pubsub/root-folders.png)

>[!TAB Autenticazione basata su argomenti e sottoscrizioni]

Se ti sei autenticato con un argomento e un accesso basato su abbonamento, il [!UICONTROL Seleziona dati] La visualizzazione dell&#39;interfaccia può variare a seconda delle informazioni fornite.

* Se si specifica solo il nome dell&#39;argomento, nell&#39;interfaccia verranno visualizzate tutte le coppie di argomenti-sottoscrizione corrispondenti all&#39;argomento specificato.
* Se fornisci solo il nome dell’abbonamento, l’interfaccia visualizza tutte le coppie di argomenti-abbonamento che corrispondono al nome dell’abbonamento fornito.
* Se vengono forniti sia i nomi degli argomenti che quelli delle sottoscrizioni, l&#39;interfaccia visualizza la coppia argomento-sottoscrizione che corrisponde a entrambi i valori specificati.

![Il passaggio Seleziona dati del flusso di lavoro sorgenti con autenticazione basata su argomenti e sottoscrizioni.](../../../../images/tutorials/create/google-pubsub/scoped-folders.png)

>[!ENDTABS]

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione tra [!DNL PubSub] e Platform. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per portare i dati in streaming dall’archiviazione cloud a Platform](../../dataflow/streaming/cloud-storage-streaming.md).
