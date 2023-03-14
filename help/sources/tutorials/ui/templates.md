---
description: Adobe Experience Platform fornisce modelli preconfigurati che puoi utilizzare per accelerare il processo di acquisizione dei dati. I modelli includono risorse generate automaticamente come schemi, set di dati, regole di mappatura, identità, spazi dei nomi delle identità e flussi di dati che è possibile utilizzare per importare dati da un’origine all’Experience Platform.
title: (Beta) Crea un flusso di dati di origini utilizzando i modelli nell’interfaccia utente
badge1: "Beta"
hide: true
hidefromtoc: true
exl-id: 48aa36ca-656d-4b9d-954c-48c8da9df1e9
source-git-commit: c4cb3783cbbab6f9bf25ffaa5b27a200c555b181
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 0%

---

# (Beta) Crea un flusso di dati di origini utilizzando i modelli nell’interfaccia utente

>[!IMPORTANT]
>
>I modelli sono in versione beta e sono supportati dalle seguenti origini:
>
>* [[!DNL Marketo Engage]](../../connectors/adobe-applications/marketo/marketo.md)
>* [[!DNL Microsoft Dynamics]](../../connectors/crm/ms-dynamics.md)
>* [[!DNL Salesforce]](../../connectors/crm/salesforce.md)
>
>La documentazione e le funzionalità sono soggette a modifiche.

Adobe Experience Platform fornisce modelli preconfigurati che puoi utilizzare per accelerare il processo di acquisizione dei dati. I modelli includono risorse generate automaticamente come schemi, set di dati, identità, regole di mappatura, spazi dei nomi delle identità e flussi di dati che è possibile utilizzare per importare dati da un’origine all’Experience Platform.

Con i modelli, puoi:

* Riduci il time-to-value dell’acquisizione accelerando la creazione di modelli di risorse.
* Riduci al minimo gli errori che possono verificarsi durante il processo manuale di acquisizione dei dati.
* Aggiorna le risorse generate automaticamente in qualsiasi momento in base ai tuoi casi d’uso.

Il seguente tutorial descrive come utilizzare i modelli nell’interfaccia utente di Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Sorgenti](../../home.md): un Experience Platform consente di acquisire dati da varie origini, consentendoti allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): framework standardizzato tramite il quale Experience Platform organizza i dati sull’esperienza del cliente.
* [Sandbox](../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che permettono di suddividere una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

## Utilizzare i modelli nell’interfaccia utente di Platform {#use-templates-in-the-platform-ui}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_accounttype"
>title="Seleziona tipo di azienda"
>abstract="Seleziona il tipo di azienda appropriato per il tuo caso d’uso. L’accesso può variare a seconda dell’account di abbonamento a Real-time Customer Data Platform."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=it" text="Panoramica di Real-Time CDP"

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] e visualizzare un catalogo delle origini disponibili in Experience Platform.

Utilizza il *[!UICONTROL Categorie]* per filtrare le sorgenti per categoria. In alternativa, immettere un nome di origine nella barra di ricerca per trovare un&#39;origine specifica dal catalogo.

Vai a [!UICONTROL applicazioni Adobe] categoria per visualizzare [!DNL Marketo Engage] scheda sorgente e quindi selezionare [!UICONTROL Aggiungi dati] per iniziare.

![Catalogo dell&#39;area di lavoro origini con l&#39;origine Marketo Engage evidenziata.](../../images/tutorials/templates/catalog.png)

Viene visualizzata una finestra pop-up con la possibilità di sfogliare i modelli o utilizzare schemi e set di dati esistenti.

* **Sfoglia modelli**: i modelli di origini creano automaticamente schemi, identità, set di dati e flussi di dati con le relative regole di mappatura. Puoi personalizzare queste risorse in base alle esigenze.
* **Usa le risorse esistenti**: acquisisci i dati utilizzando i set di dati e gli schemi esistenti creati. Se necessario, puoi anche creare nuovi set di dati e schemi.

Per utilizzare le risorse generate automaticamente, seleziona **[!UICONTROL Sfoglia modelli]** e quindi seleziona **[!UICONTROL Seleziona]**.

![Una finestra pop-up con opzioni per sfogliare i modelli o utilizzare le risorse esistenti.](../../images/tutorials/templates/browse-templates.png)

### Autenticazione

Viene visualizzato il passaggio di autenticazione, in cui viene richiesto di creare un nuovo account o di utilizzare un account esistente.

>[!BEGINTABS]

>[!TAB Usa un account esistente]

Per utilizzare un account esistente, seleziona [!UICONTROL Account esistente] quindi selezionare l&#39;account che si desidera utilizzare dall&#39;elenco visualizzato.

![Pagina di selezione di un account esistente con un elenco di account esistenti a cui è possibile accedere.](../../images/tutorials/templates/existing-account.png)

>[!TAB Crea un nuovo account]

Per creare un nuovo account, seleziona **[!UICONTROL Nuovo account]** e quindi fornire i dettagli della connessione di origine e le credenziali di autenticazione dell&#39;account. Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]** e lascia un po’ di tempo per stabilire la nuova connessione.

![Pagina di autenticazione per un nuovo account con dettagli di connessione di origine e credenziali di autenticazione dell&#39;account.](../../images/tutorials/templates/new-account.png)

>[!ENDTABS]

### Seleziona modelli

A seconda del tipo di azienda selezionato, viene visualizzato un elenco di modelli. Seleziona l’icona di anteprima ![icona anteprima](../../images/tutorials/templates/preview-icon.png) accanto al nome di un modello per visualizzare in anteprima i dati di esempio del modello.

![Elenco di modelli con l’icona Anteprima evidenziata.](../../images/tutorials/templates/templates.png)

Viene visualizzata la finestra di anteprima che consente di esplorare e controllare i dati di esempio dal modello. Al termine, seleziona **[!UICONTROL Capito]**.

![La finestra di anteprima dei dati di esempio.](../../images/tutorials/templates/preview-sample-data.png)

Quindi, seleziona dall’elenco il modello da utilizzare. Puoi selezionare più modelli e creare più flussi di dati contemporaneamente. Tuttavia, un modello può essere utilizzato solo una volta per account. Dopo aver selezionato i modelli, seleziona **[!UICONTROL Fine]** e attendi alcuni istanti per generare le risorse.

Se selezioni uno o più elementi parziali dall’elenco dei modelli disponibili, tutti gli schemi B2B e gli spazi dei nomi di identità verranno comunque generati per garantire che le relazioni B2B tra gli schemi siano configurate correttamente.

>[!NOTE]
>
>I modelli già utilizzati verranno disattivati dalla selezione.

![L’elenco dei modelli con il modello Ruolo contatto opportunità selezionato.](../../images/tutorials/templates/select-template.png)

### Imposta una pianificazione

Il [!DNL Microsoft Dynamics] e [!DNL Salesforce] entrambe le origini supportano la pianificazione dei flussi di dati.

Utilizza l’interfaccia di pianificazione per configurare una pianificazione di acquisizione per i flussi di dati. Imposta la frequenza di acquisizione su **Una volta** per creare un’acquisizione unica.

![Interfaccia di pianificazione per i modelli Dynamics e Salesforce.](../../images/tutorials/templates/schedule.png)

In alternativa, puoi impostare la frequenza di acquisizione su **Minuto**, **Hour**, **Giorno**, o **Settimana**. Se pianifichi il flusso di dati per più acquisizioni, imposta un intervallo di tempo per stabilire un intervallo di tempo tra ogni acquisizione. Ad esempio, una frequenza di acquisizione impostata su **Hour** e un intervallo impostato su **15** significa che il flusso di dati è pianificato per acquisire i dati ogni **15 ore**.

Durante questo passaggio, puoi anche abilitare **retrocompilazione** e definisci una colonna per l’acquisizione incrementale dei dati. La retrocompilazione viene utilizzata per acquisire i dati storici, mentre la colonna definita per l’acquisizione incrementale consente di distinguere i nuovi dati dai dati esistenti.

Una volta completata la configurazione della pianificazione di acquisizione, seleziona **[!UICONTROL Fine]**.

![Interfaccia di pianificazione per i modelli Dynamics e Salesforce con retrocompilazione abilitata.](../../images/tutorials/templates/backfill.png)

### Esaminare le risorse {#review-assets}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_review"
>title="Esaminare le risorse generate automaticamente"
>abstract="La generazione di tutte le risorse può richiedere fino a cinque minuti. Se scegli di uscire dalla pagina, riceverai una notifica da restituire una volta completate le risorse. Puoi rivedere le risorse generate e apportare configurazioni aggiuntive al flusso di dati in qualsiasi momento."

Il [!UICONTROL Rivedere le risorse dei modelli] In questa pagina vengono visualizzate le risorse generate automaticamente come parte del modello. In questa pagina puoi visualizzare gli schemi, i set di dati, gli spazi dei nomi delle identità e i flussi di dati generati automaticamente associati alla connessione sorgente. La generazione di tutte le risorse può richiedere fino a cinque minuti. Se scegli di uscire dalla pagina, riceverai una notifica da restituire una volta completate le risorse. Puoi rivedere le risorse generate e apportare configurazioni aggiuntive al flusso di dati in qualsiasi momento.

I flussi di dati generati automaticamente sono abilitati per impostazione predefinita. Seleziona i puntini di sospensione (`...`) accanto al nome del flusso di dati, quindi seleziona **[!UICONTROL Anteprima mappature]** per visualizzare i set di mappatura creati per il flusso di dati.

![Una finestra a discesa con l’opzione Anteprima mappature selezionata.](../../images/tutorials/templates/preview.png)

Viene visualizzata una pagina di anteprima che consente di esaminare la relazione di mappatura tra i campi dei dati di origine e i campi dello schema di destinazione. Dopo aver visualizzato le mappature del flusso di dati. Seleziona **[!UICONTROL Capito.]**

![Finestra di anteprima della mappatura.](../../images/tutorials/templates/preview-mappings.png)

Puoi aggiornare i flussi di dati in qualsiasi momento dopo l’esecuzione. Seleziona i puntini di sospensione (`...`) accanto al nome del flusso di dati, quindi seleziona **[!UICONTROL Aggiorna flusso di dati]**. Viene visualizzata la pagina del flusso di lavoro delle origini, in cui è possibile aggiornare i dettagli del flusso di dati, incluse le impostazioni per l’acquisizione parziale, la diagnostica degli errori, le notifiche di avviso e la mappatura del flusso di dati.

Puoi utilizzare la vista dell’editor schema per apportare aggiornamenti allo schema generato automaticamente. Visita la guida su [utilizzo dell’editor schema](../../../xdm/tutorials/create-schema-ui.md) per ulteriori informazioni.

![Una finestra a discesa con l’opzione Aggiorna flussi di dati selezionata.](../../images/tutorials/templates/update.png)

## Passaggi successivi

Seguendo questa esercitazione, hai creato flussi di dati e risorse come schemi, set di dati e spazi dei nomi delle identità utilizzando i modelli. Per informazioni generali sulle origini, visitare il [panoramica sulle origini](../../home.md).

## Appendice

La sezione seguente fornisce informazioni aggiuntive relative ai modelli.

### Utilizza il pannello delle notifiche per tornare alla pagina di revisione

I modelli sono supportati dagli avvisi di Adobe Experience Platform e puoi utilizzare il pannello notifiche per ricevere aggiornamenti sullo stato delle risorse e tornare alla pagina di revisione.

Seleziona l’icona di notifica nell’intestazione superiore dell’interfaccia utente di Platform, quindi seleziona l’avviso di stato per visualizzare le risorse da rivedere.

![Il pannello delle notifiche nell’interfaccia utente di Platform con un avviso di notifica che avvisa un flusso di dati non riuscito è evidenziato.](../../images/tutorials/templates/notifications.png)
