---
keywords: Experience Platform;home;argomenti popolari;
description: Adobe Experience Platform fornisce modelli preconfigurati che è possibile utilizzare per accelerare il processo di inserimento dei dati. I modelli includono risorse generate automaticamente, ad esempio schemi, set di dati, regole di mappatura, spazi dei nomi delle identità e flussi di dati che puoi utilizzare per l’inserimento di dati da un’origine all’Experience Platform.
title: (Alfa) Crea un flusso di dati delle sorgenti utilizzando i modelli nell’interfaccia utente
hide: true
hidefromtoc: true
source-git-commit: a0ca9cff43b6f8276268467fecf944c664992950
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 1%

---

# (Alfa) Crea un flusso di dati delle sorgenti utilizzando i modelli nell’interfaccia utente

>[!IMPORTANT]
>
>I modelli sono in alfa e al momento sono supportati solo da [[!DNL Marketo Engage] source](../../connectors/adobe-applications/marketo/marketo.md). La documentazione e le funzionalità sono soggette a modifiche.

Adobe Experience Platform fornisce modelli preconfigurati che è possibile utilizzare per accelerare il processo di inserimento dei dati. I modelli includono risorse generate automaticamente, ad esempio schemi, set di dati, regole di mappatura, spazi dei nomi delle identità e flussi di dati che puoi utilizzare per l’inserimento di dati da un’origine all’Experience Platform.

Con i modelli è possibile:

* Riduci il time-to-value dell’acquisizione grazie all’accelerazione della creazione di risorse basate su ML.
* Riduci al minimo gli errori che possono verificarsi durante il processo di inserimento manuale dei dati.
* Aggiorna le risorse generate automaticamente in qualsiasi momento in base ai tuoi casi d’uso.

L’esercitazione seguente fornisce passaggi su come utilizzare i modelli nell’interfaccia utente di Platform utilizzando [[!DNL Marketo Engage] source](../../connectors/adobe-applications/marketo/marketo.md).

## Introduzione

Questa esercitazione richiede una comprensione approfondita dei seguenti componenti dell&#39;Experience Platform:

* [Origini](../../home.md): L’Experience Platform consente di acquisire dati da varie sorgenti e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform.
* [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): Il framework standardizzato in base al quale l’Experience Platform organizza i dati sulla customer experience.
* [Sandbox](../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

## Utilizzare i modelli nell’interfaccia utente di Platform {#use-templates-in-the-platform-ui}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_accounttype"
>title="Selezionare il tipo di business"
>abstract="Seleziona il tipo di business appropriato per il tuo caso d’uso. L’accesso può variare a seconda dell’account di abbonamento Real-time Customer Data Platform."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=it" text="Panoramica di Real-Time CDP"

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla navigazione a sinistra per accedere al [!UICONTROL Origini] workspace. La [!UICONTROL Catalogo] visualizza una varietà di sorgenti che possono essere utilizzate per creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando la barra di ricerca.

Sotto la [!UICONTROL Applicazioni di Adobe] categoria, seleziona **[!UICONTROL Marketo Engage]** quindi seleziona **[!UICONTROL Aggiungi dati]**.

![Un catalogo dell&#39;area di lavoro origini con la sorgente del Marketo Engage evidenziata.](../../images/tutorials/templates/catalog.png)

Viene visualizzata una finestra a comparsa che ti presenta l’opzione per sfogliare i modelli o utilizzare schemi e set di dati esistenti. Per utilizzare le risorse generate automaticamente, seleziona **[!UICONTROL Sfoglia modelli]** quindi seleziona **[!UICONTROL Seleziona]**.

![Una finestra a comparsa con opzioni per sfogliare i modelli o utilizzare risorse esistenti.](../../images/tutorials/templates/browse-templates.png)

### Autenticazione

Viene visualizzato il passaggio di autenticazione , che richiede di creare un nuovo account o di utilizzare un account esistente.

#### Account esistente

Per utilizzare un account esistente, seleziona [!UICONTROL Account esistente] quindi selezionare l&#39;account da utilizzare dall&#39;elenco visualizzato.

![Pagina di selezione per un account esistente con un elenco di account esistenti a cui è possibile accedere.](../../images/tutorials/templates/existing-account.png)

#### Nuovo account

Per creare un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci i dettagli della connessione di origine e le credenziali di autenticazione dell’account. Al termine, seleziona **[!UICONTROL Connetti alla sorgente]** e lasciare un po&#39; di tempo per stabilire la nuova connessione.

![Pagina di autenticazione per un nuovo account con i dettagli della connessione di origine e le credenziali di autenticazione dell’account.](../../images/tutorials/templates/new-account.png)

### Selezionare i modelli

Dopo aver autenticato e selezionato l&#39;account, viene visualizzato un elenco di modelli. Seleziona l’icona di anteprima accanto al nome di un modello per visualizzare in anteprima i dati di esempio dal modello.

![Elenco di modelli con l’icona di anteprima evidenziata.](../../images/tutorials/templates/templates.png)

Viene visualizzata la finestra di anteprima che consente di esplorare ed esaminare i dati di esempio dal modello. Al termine, seleziona **[!UICONTROL Capito]**.

![La finestra di anteprima dei dati di esempio.](../../images/tutorials/templates/preview-sample-data.png)

Quindi, seleziona dall’elenco il modello da utilizzare. È possibile selezionare più modelli e creare più flussi di dati contemporaneamente. Tuttavia, un modello può essere utilizzato solo una volta per account. Dopo aver selezionato i modelli, seleziona **[!UICONTROL Fine]** e consenti la generazione di alcune risorse.

![Elenco di modelli con il modello Ruolo contatto opportunità selezionato.](../../images/tutorials/templates/select-template.png)

### Esaminare le risorse {#review-assets}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_review"
>title="Esamina le risorse generate automaticamente"
>abstract="La generazione di tutte le risorse può richiedere fino a cinque minuti. Se scegli di lasciare la pagina, riceverai una notifica da restituire una volta completate le risorse. Puoi rivedere le risorse una volta generate e configurare ulteriormente il flusso di dati in qualsiasi momento."

La [!UICONTROL Esaminare le risorse dei modelli] In questa pagina vengono visualizzate le risorse generate automaticamente come parte del modello. In questa pagina puoi visualizzare gli schemi, i set di dati, i namespace di identità e i flussi di dati generati automaticamente associati alla connessione di origine.

I flussi di dati generati automaticamente sono abilitati per impostazione predefinita. Seleziona i puntini di sospensione (`...`) accanto al nome del flusso di dati, quindi seleziona **[!UICONTROL Mappature di anteprima]** per visualizzare i set di mappatura creati per il flusso di dati.

![Una finestra a discesa con l’opzione di mappatura anteprima selezionata.](../../images/tutorials/templates/preview.png)

Viene visualizzata una pagina di anteprima che consente di esaminare la relazione di mappatura tra i campi dei dati di origine e i campi dello schema di destinazione. Una volta visualizzate le mappature del flusso di dati. Seleziona **[!UICONTROL Capito.]**

![Finestra di anteprima della mappatura.](../../images/tutorials/templates/preview-mappings.png)

Puoi aggiornare i flussi di dati in qualsiasi momento dopo l’esecuzione. Seleziona i puntini di sospensione (`...`) accanto al nome del flusso di dati, quindi seleziona **[!UICONTROL Aggiornamento del flusso di dati]**. Viene visualizzata la pagina del flusso di lavoro origini in cui è possibile aggiornare i dettagli del flusso di dati, incluse le impostazioni per l’acquisizione parziale, la diagnostica degli errori e le notifiche degli avvisi, nonché la mappatura del flusso di dati.

![Una finestra a discesa con l’opzione Aggiorna flussi di dati selezionata.](../../images/tutorials/templates/update.png)

## Passaggi successivi

Seguendo questa esercitazione, ora hai creato flussi di dati e risorse come schemi, set di dati e namespace di identità utilizzando i modelli. Per informazioni generali sulle fonti, visita il [panoramica di origini](../../home.md).