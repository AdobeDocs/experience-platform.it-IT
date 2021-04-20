---
keywords: Experience Platform;home;argomenti comuni;connettore sorgente Marketo;connettore Marketo;sorgente Marketo;Marketo
solution: Experience Platform
title: Creare un connettore sorgente di Marketo Engage nell’interfaccia utente
topic: ' - Panoramica'
type: Tutorial
description: Questa esercitazione fornisce passaggi per creare un connettore di origine di Marketo Engage nell’interfaccia utente per inserire dati B2B in Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 5d4d88f88ab184c679a4cf425283a71983c929f3
workflow-type: tm+mt
source-wordcount: '1318'
ht-degree: 0%

---


# (Beta) Crea un connettore sorgente [!DNL Marketo Engage] nell’interfaccia utente

>[!IMPORTANT]
>
>La sorgente [!DNL Marketo Engage] è attualmente in versione beta. La funzione e la documentazione sono soggette a modifica. Inoltre, è necessario assicurarsi di utilizzare una sandbox non di produzione quando si utilizza il connettore durante il programma beta. Per ulteriori informazioni sulle sandbox, consulta la [documentazione sulle sandbox](https://experienceleague.adobe.com/docs/experience-platform/sandbox/home.html?lang=en#understanding-sandboxes).

Questa esercitazione fornisce passaggi per creare un connettore sorgente [!DNL Marketo Engage] (in seguito denominato &quot;[!DNL Marketo]&quot;) nell&#39;interfaccia utente per inserire i dati dei consumatori in Adobe Experience Platform.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): L’Experience Platform consente di acquisire dati da varie sorgenti e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform.
* [Experience Data Model (XDM)](../../../../../xdm/home.md): Il framework standardizzato in base al quale l’Experience Platform organizza i dati sulla customer experience.
   * [Creare e modificare schemi nell’interfaccia utente](../../../../../xdm/ui/resources/schemas.md): Scopri come creare e modificare schemi nell’interfaccia utente di .
* [Namespace](../../../../../identity-service/namespaces.md) di identità: Gli spazi dei nomi di identità sono un componente di  [!DNL Identity Service] che funge da indicatori del contesto a cui si riferisce un’identità. Un&#39;identità completa include un valore ID e uno spazio dei nomi.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

### Raccogli credenziali richieste

Per accedere al tuo account [!DNL Marketo] su Platform, devi fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `munchkinId` | L&#39;ID Munchkin è l&#39;identificatore univoco per una specifica istanza [!DNL Marketo]. |
| `clientId` | L&#39;ID client univoco dell&#39;istanza [!DNL Marketo]. |
| `clientSecret` | Il segreto client univoco dell&#39;istanza [!DNL Marketo]. |

Per ulteriori informazioni sull&#39;acquisizione di questi valori, consulta la [[!DNL Marketo] guida all&#39;autenticazione](../../../../connectors/adobe-applications/marketo/marketo-auth.md).

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi descritti nella sezione successiva.

## Connetti il tuo account [!DNL Marketo]

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all’area di lavoro [!UICONTROL Sources]. Nella schermata [!UICONTROL Catalog] sono visualizzate diverse origini per le quali è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando la barra di ricerca.

Sotto la categoria [!UICONTROL Adobe applications], selezionare **[!UICONTROL Marketo Engage]**. Quindi, seleziona **[!UICONTROL Add data]** per creare un nuovo flusso di dati [!DNL Marketo].

![catalogo](../../../../images/tutorials/create/marketo/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connect to Marketo Engage]** . In questa pagina puoi utilizzare un nuovo account o accedere a un account esistente.

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL New account]**. Nel modulo di input visualizzato, specificare un nome account, una descrizione facoltativa e le credenziali di autenticazione [!DNL Marketo]. Al termine, selezionare **[!UICONTROL Connect to source]** e quindi concedere un po&#39; di tempo per l&#39;impostazione della nuova connessione.

![nuovo account](../../../../images/tutorials/create/marketo/new.png)

### Account esistente

Per creare un flusso di dati con un account esistente, selezionare **[!UICONTROL Existing account]**, quindi selezionare l&#39;account [!DNL Marketo] che si desidera utilizzare. Selezionare **[!UICONTROL Next]** per continuare.

![esistente](../../../../images/tutorials/create/marketo/existing.png)

## Selezionare un set di dati

Dopo aver creato l’account [!DNL Marketo], il passaggio successivo fornisce un’interfaccia per esplorare i set di dati [!DNL Marketo].

La metà sinistra dell&#39;interfaccia è un browser di directory che visualizza i 10 set di dati [!DNL Marketo]. Una connessione di origine [!DNL Marketo] completamente funzionante richiede l’acquisizione di nove set di dati diversi. Se utilizzi anche la funzione di marketing basato su account ( [!DNL Marketo's] ), devi anche creare un decimo flusso di dati per acquisire il set di dati [!UICONTROL Named Accounts] .

>[!NOTE]
>
>Per motivi di brevità, l’esercitazione seguente utilizza [!UICONTROL Named Acccounts] come esempio, ma i passaggi descritti di seguito si applicano a uno qualsiasi dei 10 set di dati [!DNL Marketo].

Seleziona il set di dati da acquisire prima, quindi seleziona **[!UICONTROL Next]**.

![select-data](../../../../images/tutorials/create/marketo/select-data.png)

## Mappatura di campi dati su uno schema XDM

Viene visualizzato il passaggio [!UICONTROL Mapping] , che fornisce un’interfaccia per mappare il set di dati [!DNL Marketo] a un set di dati di Platform.

Scegli un set di dati in entrata in cui acquisire i dati. Puoi utilizzare un set di dati esistente o crearne uno nuovo.

### Utilizzare un set di dati esistente

Per acquisire dati in un set di dati esistente, seleziona **[!UICONTROL Use existing dataset]**, quindi seleziona l’icona del set di dati.

![set di dati esistente](../../../../images/tutorials/create/marketo/existing-dataset.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Select dataset]**. Trova il set di dati con lo schema appropriato da utilizzare, selezionalo, quindi seleziona **[!UICONTROL Confirm]**.

![select-existing-dataset](../../../../images/tutorials/create/marketo/select-dataset.png)

### Utilizzare un nuovo set di dati

Per acquisire i dati in un nuovo set di dati, seleziona **[!UICONTROL Create new dataset]** e immetti un nome e una descrizione per il set di dati nei campi forniti.

È possibile cercare uno schema immettendone il nome nella barra di ricerca **[!UICONTROL Select schema]**. Puoi anche selezionare l’icona a discesa per visualizzare un elenco degli schemi esistenti. In alternativa, puoi selezionare **[!UICONTROL Advanced search]** per accedere alla pagina degli schemi esistenti, inclusi i rispettivi dettagli.

Attiva il pulsante **[!UICONTROL Profile dataset]** per abilitare il set di dati di destinazione per [!DNL Profile], consentendo di creare una visualizzazione olistica degli attributi e dei comportamenti di un’entità. I dati di tutti i set di dati abilitati [!DNL Profile] verranno inclusi in [!DNL Profile] e le modifiche vengono applicate al momento del salvataggio del flusso di dati.

![create-new-dataset](../../../../images/tutorials/create/marketo/new-dataset-schema.png)

Dopo aver selezionato uno schema, scorri verso il basso per visualizzare la finestra di dialogo di mappatura per iniziare a mappare i campi del set di dati [!DNL Marketo] ai campi XDM di destinazione appropriati.

### Mappatura dei campi di origine del set di dati [!DNL Marketo] per eseguire il targeting dei campi XDM

Ogni set di dati [!DNL Marketo] ha le proprie regole di mappatura specifiche da seguire. Per ulteriori informazioni su come mappare i set di dati [!DNL Marketo] in XDM, consulta quanto segue:

* [Attività](../../../../connectors/adobe-applications/mapping/marketo.md#activities)
* [Programmi](../../../../connectors/adobe-applications/mapping/marketo.md#programs)
* [Partecipazioni al programma](../../../../connectors/adobe-applications/mapping/marketo.md#program-memberships)
* [Aziende](../../../../connectors/adobe-applications/mapping/marketo.md#companies)
* [Elenchi statici](../../../../connectors/adobe-applications/mapping/marketo.md#static-lists)
* [appartenenze a elenchi statici](../../../../connectors/adobe-applications/mapping/marketo.md#static-list-memberships)
* [Account denominati](../../../../connectors/adobe-applications/mapping/marketo.md#named-accounts)
* [Opportunità](../../../../connectors/adobe-applications/mapping/marketo.md#opportunities)
* [Ruoli di contatto opportunità](../../../../connectors/adobe-applications/mapping/marketo.md#opportunity-contact-roles)
* [Persone](../../../../connectors/adobe-applications/mapping/marketo.md#persons)

Seleziona **[!UICONTROL Preview data]** per visualizzare i risultati della mappatura in base al set di dati selezionato.

![mappatura](../../../../images/tutorials/create/marketo/mapping.png)

Il [!UICONTROL Preview] fornisce un’interfaccia per esplorare i risultati della mappatura di fino a 100 righe di dati di esempio dal set di dati selezionato.

![anteprima](../../../../images/tutorials/create/marketo/mapping-preview.png)

Una volta mappati i campi di origine ai campi di destinazione appropriati, seleziona **[!UICONTROL Close]**.

## Fornire i dettagli del flusso di dati

Viene visualizzato il passaggio [!UICONTROL Dataflow detail] , che consente di fornire un nome e una breve descrizione del nuovo flusso di dati.

![dettaglio del flusso di dati](../../../../images/tutorials/create/marketo/dataflow-detail.png)

Abilita l’opzione **[!UICONTROL Error diagnostics]** per consentire la generazione di messaggi di errore dettagliati per i batch appena acquisiti, che puoi scaricare utilizzando l’API.

![errori](../../../../images/tutorials/create/marketo/errors.png)

Il connettore [!DNL Marketo] utilizza l’acquisizione batch per acquisire tutti i record storici e utilizza l’acquisizione in streaming per aggiornamenti in tempo reale. Questo consente al connettore di continuare lo streaming durante l’acquisizione di eventuali record errati. Attiva l&#39;interruttore **[!UICONTROL Partial ingestion]** e imposta il valore massimo [!UICONTROL Error threshold %] per evitare errori nel flusso di dati.

**[!UICONTROL Partial ingestion]** consente di acquisire dati contenenti errori fino a una determinata soglia. Per ulteriori informazioni, consulta la [panoramica sull’acquisizione parziale dei batch](../../../../../ingestion/batch-ingestion/partial.md).

Dopo aver fornito i dettagli del flusso di dati e impostato la soglia di errore su max, seleziona **[!UICONTROL Next]**.

![assimilazione parziale](../../../../images/tutorials/create/marketo/partial-ingestion.png)

## Controlla il tuo flusso di dati

Viene visualizzato il passaggio **[!UICONTROL Review]** , che consente di rivedere il nuovo flusso di dati prima della creazione. I dettagli sono raggruppati nelle seguenti categorie:

* **[!UICONTROL Connection]**: Mostra il tipo di origine, il percorso pertinente del file di origine scelto e la quantità di colonne all&#39;interno del file di origine.
* **[!UICONTROL Assign dataset & map fields]**: Mostra il set di dati in cui vengono acquisiti i dati di origine, incluso lo schema a cui il set di dati aderisce.

Dopo aver esaminato il flusso di dati, seleziona **[!UICONTROL Finish]** e consenti la creazione del flusso di dati.

![revisione](../../../../images/tutorials/create/marketo/review.png)

## Monitorare il flusso di dati

Una volta creato il flusso di dati, puoi monitorare i dati che vengono acquisiti tramite di esso per visualizzare informazioni sui tassi di acquisizione, sul successo e sugli errori. Per ulteriori informazioni su come monitorare i flussi di dati, consulta l’esercitazione sul [monitoraggio dei flussi di dati nell’interfaccia utente](../../../../../dataflows/ui/monitor-sources.md).

## Eliminare gli attributi

Gli attributi personalizzati nei set di dati non possono essere nascosti o rimossi retroattivamente. Se desideri nascondere o rimuovere un attributo personalizzato da un set di dati esistente, devi creare un nuovo set di dati senza questo attributo personalizzato, un nuovo schema XDM e configurare un nuovo flusso di dati per il nuovo set di dati creato. È inoltre necessario disattivare o eliminare il flusso di dati originale costituito dal set di dati con l’attributo personalizzato che si desidera nascondere o rimuovere.

## Elimina il flusso di dati

È possibile eliminare i flussi di dati che non sono più necessari o che sono stati creati in modo errato utilizzando la funzione **[!UICONTROL Delete]** disponibile nell&#39;area di lavoro [!UICONTROL Dataflows]. Per ulteriori informazioni su come eliminare i flussi di dati, consulta l’esercitazione sull’ [eliminazione dei flussi di dati nell’interfaccia utente](../../delete.md).

## Passaggi successivi

Seguendo questa esercitazione, hai creato correttamente un flusso di dati per inserire i dati [!DNL Marketo] . I dati in arrivo possono ora essere utilizzati dai servizi Platform a valle, come [!DNL Real-time Customer Profile] e [!DNL Data Science Workspace]. Per ulteriori informazioni, consulta i seguenti documenti:

* [[!DNL Real-time Customer Profile] panoramica](../../../../profile/home.md)
* [[!DNL Data Science Workspace] panoramica](../../../../data-science-workspace/home.md)
