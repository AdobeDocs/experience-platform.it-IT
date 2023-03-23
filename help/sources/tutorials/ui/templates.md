---
description: Adobe Experience Platform fornisce modelli preconfigurati che è possibile utilizzare per accelerare il processo di inserimento dei dati. I modelli includono risorse generate automaticamente, come schemi, set di dati, regole di mappatura, identità, namespace di identità e flussi di dati che puoi utilizzare per l’inserimento di dati da un’origine all’Experience Platform.
title: (Beta) Crea un flusso di dati sorgente utilizzando i modelli nell’interfaccia utente
badge1: "Beta"
hide: true
hidefromtoc: true
exl-id: 48aa36ca-656d-4b9d-954c-48c8da9df1e9
source-git-commit: c4cb3783cbbab6f9bf25ffaa5b27a200c555b181
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 0%

---

# (Beta) Crea un flusso di dati sorgente utilizzando i modelli nell’interfaccia utente

>[!IMPORTANT]
>
>I modelli sono in versione beta e sono supportati dalle seguenti origini:
>
>* [[!DNL Marketo Engage]](../../connectors/adobe-applications/marketo/marketo.md)
>* [[!DNL Microsoft Dynamics]](../../connectors/crm/ms-dynamics.md)
>* [[!DNL Salesforce]](../../connectors/crm/salesforce.md)
>
>La documentazione e le funzionalità sono soggette a modifiche.

Adobe Experience Platform fornisce modelli preconfigurati che è possibile utilizzare per accelerare il processo di inserimento dei dati. I modelli includono risorse generate automaticamente, ad esempio schemi, set di dati, identità, regole di mappatura, spazi dei nomi delle identità e flussi di dati che puoi utilizzare per l’inserimento di dati da un’origine all’Experience Platform.

Con i modelli è possibile:

* Riduci il time-to-value dell’acquisizione grazie all’accelerazione della creazione di risorse modellate.
* Riduci al minimo gli errori che possono verificarsi durante il processo di inserimento manuale dei dati.
* Aggiorna le risorse generate automaticamente in qualsiasi momento in base ai tuoi casi d’uso.

L’esercitazione seguente descrive come utilizzare i modelli nell’interfaccia utente di Platform.

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

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla navigazione a sinistra per accedere al [!UICONTROL Origini] visualizza un catalogo di origini disponibili in Experience Platform.

Utilizza la *[!UICONTROL Categorie]* per filtrare le origini per categoria. In alternativa, immetti un nome di origine nella barra di ricerca per trovare un&#39;origine specifica dal catalogo.

Vai a [!UICONTROL Applicazioni di Adobe] per visualizzare la categoria [!DNL Marketo Engage] scheda di origine e quindi seleziona [!UICONTROL Aggiungi dati] per iniziare.

![Un catalogo dell&#39;area di lavoro origini con la sorgente del Marketo Engage evidenziata.](../../images/tutorials/templates/catalog.png)

Viene visualizzata una finestra a comparsa che ti presenta l’opzione per sfogliare i modelli o utilizzare schemi e set di dati esistenti.

* **Sfoglia modelli**: I modelli di origine creano automaticamente schemi, identità, set di dati e flussi di dati con regole di mappatura. Puoi personalizzare queste risorse in base alle tue esigenze.
* **Utilizzare le risorse esistenti**: Acquisisci i dati utilizzando i set di dati e gli schemi esistenti creati. Se necessario, puoi anche creare nuovi set di dati e schemi.

Per utilizzare le risorse generate automaticamente, seleziona **[!UICONTROL Sfoglia modelli]** quindi seleziona **[!UICONTROL Seleziona]**.

![Una finestra a comparsa con opzioni per sfogliare i modelli o utilizzare risorse esistenti.](../../images/tutorials/templates/browse-templates.png)

### Autenticazione

Viene visualizzato il passaggio di autenticazione , che richiede di creare un nuovo account o di utilizzare un account esistente.

>[!BEGINTABS]

>[!TAB Utilizzare un account esistente]

Per utilizzare un account esistente, seleziona [!UICONTROL Account esistente] quindi selezionare l&#39;account da utilizzare dall&#39;elenco visualizzato.

![Pagina di selezione per un account esistente con un elenco di account esistenti a cui è possibile accedere.](../../images/tutorials/templates/existing-account.png)

>[!TAB Crea un nuovo account]

Per creare un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci i dettagli della connessione di origine e le credenziali di autenticazione dell’account. Al termine, seleziona **[!UICONTROL Connetti alla sorgente]** e lasciare un po&#39; di tempo per stabilire la nuova connessione.

![Pagina di autenticazione per un nuovo account con i dettagli della connessione di origine e le credenziali di autenticazione dell’account.](../../images/tutorials/templates/new-account.png)

>[!ENDTABS]

### Selezionare i modelli

A seconda del tipo di business selezionato, viene visualizzato un elenco di modelli. Seleziona l’icona di anteprima ![icona anteprima](../../images/tutorials/templates/preview-icon.png) accanto al nome di un modello per visualizzare in anteprima i dati di esempio dal modello.

![Elenco di modelli con l’icona di anteprima evidenziata.](../../images/tutorials/templates/templates.png)

Viene visualizzata la finestra di anteprima che consente di esplorare ed esaminare i dati di esempio dal modello. Al termine, seleziona **[!UICONTROL Capito]**.

![La finestra di anteprima dei dati di esempio.](../../images/tutorials/templates/preview-sample-data.png)

Quindi, seleziona dall’elenco il modello da utilizzare. È possibile selezionare più modelli e creare più flussi di dati contemporaneamente. Tuttavia, un modello può essere utilizzato solo una volta per account. Dopo aver selezionato i modelli, seleziona **[!UICONTROL Fine]** e consenti la generazione di alcune risorse.

Se selezioni uno o più elementi parziali dall’elenco dei modelli disponibili, verranno comunque generati tutti gli schemi B2B e i namespace di identità per garantire che le relazioni B2B tra gli schemi siano configurate correttamente.

>[!NOTE]
>
>I modelli già utilizzati verranno disattivati dalla selezione.

![Elenco di modelli con il modello Ruolo contatto opportunità selezionato.](../../images/tutorials/templates/select-template.png)

### Imposta una pianificazione

La [!DNL Microsoft Dynamics] e [!DNL Salesforce] origini supportano entrambi i flussi di dati di pianificazione.

Utilizza l’interfaccia di pianificazione per configurare una pianificazione dell’acquisizione per i flussi di dati. Imposta la frequenza di acquisizione su **Una volta** per creare un’acquisizione una tantum.

![Interfaccia di pianificazione per i modelli Dynamics e Salesforce.](../../images/tutorials/templates/schedule.png)

In alternativa, puoi impostare la frequenza di acquisizione su **Minuto**, **Ora**, **Giorno** oppure **Settimana**. Se pianifichi il flusso di dati per più acquisizioni, devi impostare un intervallo per stabilire un intervallo di tempo tra ogni acquisizione. Ad esempio, una frequenza di acquisizione impostata su **Ora** e un intervallo impostato su **15** significa che il flusso di dati è pianificato per l’acquisizione di dati ogni **15 ore**.

Durante questo passaggio, puoi anche abilitare **backfill** e definire una colonna per l’assimilazione incrementale dei dati. Il backfill viene utilizzato per acquisire i dati storici, mentre la colonna definita per l’acquisizione incrementale consente di differenziare i nuovi dati dai dati esistenti.

Al termine della configurazione della pianificazione dell’acquisizione, seleziona **[!UICONTROL Fine]**.

![Interfaccia di pianificazione per i modelli Dynamics e Salesforce con backfill abilitato.](../../images/tutorials/templates/backfill.png)

### Esaminare le risorse {#review-assets}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_review"
>title="Esamina le risorse generate automaticamente"
>abstract="La generazione di tutte le risorse può richiedere fino a cinque minuti. Se scegli di lasciare la pagina, riceverai una notifica da restituire una volta completate le risorse. Puoi rivedere le risorse una volta generate e configurare ulteriormente il flusso di dati in qualsiasi momento."

La [!UICONTROL Esaminare le risorse dei modelli] In questa pagina vengono visualizzate le risorse generate automaticamente come parte del modello. In questa pagina puoi visualizzare gli schemi, i set di dati, i namespace di identità e i flussi di dati generati automaticamente associati alla connessione di origine. La generazione di tutte le risorse può richiedere fino a cinque minuti. Se scegli di lasciare la pagina, riceverai una notifica da restituire una volta completate le risorse. Puoi rivedere le risorse una volta generate e configurare ulteriormente il flusso di dati in qualsiasi momento.

I flussi di dati generati automaticamente sono abilitati per impostazione predefinita. Seleziona i puntini di sospensione (`...`) accanto al nome del flusso di dati, quindi seleziona **[!UICONTROL Mappature di anteprima]** per visualizzare i set di mappatura creati per il flusso di dati.

![Una finestra a discesa con l’opzione di mappatura anteprima selezionata.](../../images/tutorials/templates/preview.png)

Viene visualizzata una pagina di anteprima che consente di esaminare la relazione di mappatura tra i campi dei dati di origine e i campi dello schema di destinazione. Una volta visualizzate le mappature del flusso di dati. Seleziona **[!UICONTROL Capito.]**

![Finestra di anteprima della mappatura.](../../images/tutorials/templates/preview-mappings.png)

Puoi aggiornare i flussi di dati in qualsiasi momento dopo l’esecuzione. Seleziona i puntini di sospensione (`...`) accanto al nome del flusso di dati, quindi seleziona **[!UICONTROL Aggiornamento del flusso di dati]**. Viene visualizzata la pagina del flusso di lavoro origini in cui è possibile aggiornare i dettagli del flusso di dati, incluse le impostazioni per l’acquisizione parziale, la diagnostica degli errori e le notifiche degli avvisi, nonché la mappatura del flusso di dati.

Puoi utilizzare la vista dell’editor dello schema per apportare aggiornamenti allo schema generato automaticamente. Visita la guida su [utilizzo dell’editor di schemi](../../../xdm/tutorials/create-schema-ui.md) per ulteriori informazioni.

![Una finestra a discesa con l’opzione Aggiorna flussi di dati selezionata.](../../images/tutorials/templates/update.png)

## Passaggi successivi

Seguendo questa esercitazione, ora hai creato flussi di dati e risorse come schemi, set di dati e namespace di identità utilizzando i modelli. Per informazioni generali sulle fonti, visita il [panoramica di origini](../../home.md).

## Appendice

La sezione seguente fornisce ulteriori informazioni sui modelli.

### Utilizza il pannello notifiche per tornare alla pagina di revisione

I modelli sono supportati dagli avvisi di Adobe Experience Platform e puoi utilizzare il pannello di notifica per ricevere aggiornamenti sullo stato delle risorse e anche per tornare alla pagina di revisione.

Seleziona l’icona di notifica nell’intestazione superiore dell’interfaccia utente di Platform, quindi seleziona l’avviso di stato per visualizzare le risorse da esaminare.

![Il pannello Notifiche nell’interfaccia utente di Platform con una notifica che avvisa un flusso di dati non riuscito evidenziato.](../../images/tutorials/templates/notifications.png)
