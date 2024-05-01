---
title: Strumenti sandbox
description: Esporta e importa facilmente le configurazioni Sandbox tra sandbox.
exl-id: f1199ab7-11bf-43d9-ab86-15974687d182
source-git-commit: fea62a2aa3c7d175afbfa808f392c3a93a0d31a0
workflow-type: tm+mt
source-wordcount: '2314'
ht-degree: 7%

---

# Strumenti sandbox

>[!NOTE]
>
>Gli strumenti sandbox sono una funzionalità fondamentale che supporta sia [!DNL Real-Time Customer Data Platform] e [!DNL Journey Optimizer] per migliorare l&#39;efficienza del ciclo di sviluppo e la precisione della configurazione.<br><br>Per utilizzare la funzione strumenti sandbox, è necessario disporre delle due autorizzazioni di controllo dell&#39;accesso basate sul ruolo seguenti:<br>- `manage-sandbox` o `view-sandbox`<br>- `manage-package`

Migliora la precisione della configurazione nelle sandbox ed esporta e importa facilmente le configurazioni sandbox tra sandbox con la funzione di strumenti sandbox. Utilizza gli strumenti sandbox per ridurre il time-to-value per il processo di implementazione e spostare le configurazioni corrette tra le sandbox.

È possibile utilizzare la funzione degli strumenti sandbox per selezionare oggetti diversi ed esportarli in un pacchetto. Un pacchetto può essere costituito da uno o più oggetti. <!--or an entire sandbox.-->Tutti gli oggetti inclusi in un pacchetto devono appartenere alla stessa sandbox.

## Oggetti supportati per gli strumenti sandbox {#supported-objects}

La funzione di strumenti sandbox consente di esportare [!DNL Adobe Real-Time Customer Data Platform] e [!DNL Adobe Journey Optimizer] in un pacchetto.

### Oggetti Real-time Customer Data Platform {#real-time-cdp-objects}

La tabella seguente elenca [!DNL Adobe Real-Time Customer Data Platform] oggetti attualmente supportati per gli strumenti sandbox:

| Piattaforma | Oggetto | Dettagli |
| --- | --- | --- |
| Customer Data Platform | Origini | Le credenziali dell’account di origine non vengono replicate nella sandbox di destinazione per motivi di sicurezza e sarà necessario aggiornarle manualmente. Per impostazione predefinita, il flusso di dati di origine viene copiato in stato di bozza. |
| Customer Data Platform | Tipi di pubblico | Solo il **[!UICONTROL Pubblico cliente]** tipo **[!UICONTROL Servizio di segmentazione]** è supportato. Le etichette esistenti per il consenso e la governance verranno copiate nello stesso processo di importazione. Il sistema selezionerà automaticamente il criterio di unione predefinito nella sandbox di destinazione con la stessa classe XDM durante il controllo delle dipendenze dei criteri di unione. |
| Customer Data Platform | Identità | Durante la creazione nella sandbox di destinazione, il sistema deduplica automaticamente gli spazi dei nomi di identità standard Adobe. I tipi di pubblico possono essere copiati solo quando tutti gli attributi nelle regole del pubblico sono abilitati nello schema di unione. Gli schemi necessari devono prima essere spostati e abilitati per il profilo unificato. |
| Customer Data Platform | Schemi | Le etichette esistenti per il consenso e la governance verranno copiate nello stesso processo di importazione. L’utente dispone della flessibilità necessaria per importare schemi senza l’opzione Profilo unificato abilitata. Il caso edge delle relazioni di schema non è incluso nel pacchetto. |
| Customer Data Platform | Set di dati | I set di dati vengono copiati con l’impostazione di profilo unificato disabilitata per impostazione predefinita. |
| Customer Data Platform | Criteri di consenso e governance | Aggiungi a un pacchetto i criteri personalizzati creati da un utente e spostali tra le diverse sandbox. |

I seguenti oggetti vengono importati ma sono in stato bozza o disabilitato:

| Funzione | Oggetto | Stato |
| --- | --- | --- |
| Stato importazione | Flusso di dati di origine | Bozza |
| Stato importazione | Percorso | Bozza |
| Profilo unificato | Set di dati | Profilo unificato disabilitato |
| Criteri | Criteri di governance dei dati | Disabilitata |

### Oggetti Adobe Journey Optimizer {#abobe-journey-optimizer-objects}

La tabella seguente elenca [!DNL Adobe Journey Optimizer] oggetti attualmente supportati per gli strumenti e le limitazioni della sandbox:

| Piattaforma | Oggetto | Dettagli |
| --- | --- | --- |
| [!DNL Adobe Journey Optimizer] | Pubblico | Un pubblico può essere copiato come oggetto dipendente dell’oggetto percorso. Puoi selezionare Crea un nuovo pubblico o riutilizzarne uno esistente nella sandbox di destinazione. |
| [!DNL Adobe Journey Optimizer] | Schema | Gli schemi utilizzati nel percorso possono essere copiati come oggetti dipendenti. Puoi selezionare Crea un nuovo schema o riutilizzarne uno esistente nella sandbox di destinazione. |
| [!DNL Adobe Journey Optimizer] | Criterio di unione | I criteri di unione utilizzati nel percorso possono essere copiati come oggetti dipendenti. Nella sandbox di destinazione, puoi **non può** creare un nuovo criterio di unione, è possibile utilizzarne solo uno esistente. |
| [!DNL Adobe Journey Optimizer] | Percorso - dettagli area di lavoro | La rappresentazione del percorso nell’area di lavoro include gli oggetti del percorso, quali condizioni, azioni, eventi, tipi di pubblico letti e così via, che vengono copiati. L’attività Salta viene esclusa dalla copia. |
| [!DNL Adobe Journey Optimizer] | Evento | Gli eventi e i dettagli dell’evento utilizzati nel percorso vengono copiati. Crea sempre una nuova versione nella sandbox di destinazione. |
| [!DNL Adobe Journey Optimizer] | Azione | I messaggi e-mail e push utilizzati nel percorso possono essere copiati come oggetti dipendenti. Le attività di azione del canale utilizzate nei campi del percorso, che vengono utilizzate per la personalizzazione nel messaggio, non vengono controllate per completezza. I blocchi di contenuto non vengono copiati.<br><br>È possibile copiare l&#39;azione di aggiornamento del profilo utilizzata nel percorso. Vengono copiati anche le azioni personalizzate e i dettagli delle azioni utilizzati nel percorso. Crea sempre una nuova versione nella sandbox di destinazione. |

Le superfici (ad esempio i predefiniti) non vengono copiate. Il sistema seleziona automaticamente la corrispondenza più simile possibile nella sandbox di destinazione in base al tipo di messaggio e al nome della superficie. Se nella sandbox di destinazione non è presente alcuna superficie, la copia della superficie avrà esito negativo e la copia del messaggio avrà esito negativo perché un messaggio richiede che una superficie sia disponibile per l’impostazione. In questo caso, affinché la copia funzioni, è necessario creare almeno una superficie per il canale destro del messaggio.

I tipi di identità personalizzati non sono supportati come oggetti dipendenti durante l’esportazione di un percorso.

## Esportare oggetti in un pacchetto {#export-objects}

>[!NOTE]
>
>Tutte le azioni di esportazione vengono registrate nei registri di audit.

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_remove_object"
>title="Rimuovere un oggetto"
>abstract="Per rimuovere un oggetto dal pacchetto, seleziona la riga da rimuovere e quindi utilizza l’opzione elimina, disponibile al momento della selezione. Non è possibile rimuovere oggetti dai pacchetti pubblicati."

>[!CONTEXTUALHELP]
>id="platform_sandbox_package_expiry"
>title="Impostazioni di scadenza pacchetto"
>abstract="I pacchetti sono impostati per scadere dopo un periodo di inattività in stato di bozza. La data predefinita è impostata a 90 giorni a partire da oggi. Questa data continua a cambiare fino alla pubblicazione del pacchetto. Se un utente visita il pacchetto in stato di bozza domani, la data viene spostata di 1 giorno (a meno che non venga impostata manualmente)."

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_package_status"
>title="Stato pacchetto"
>abstract="Per impostazione predefinita, lo stato è impostato su bozza. Dopo la pubblicazione del pacchetto, lo stato viene modificato in pubblicato. Non è possibile apportare modifiche dopo la pubblicazione del pacchetto."

>[!NOTE]
>
>È possibile importare un pacchetto solo se si dispone dell&#39;autorizzazione per accedere agli oggetti.

Questo esempio documenta il processo di esportazione di uno schema e di aggiunta a un pacchetto. È possibile utilizzare lo stesso processo per esportare altri oggetti, ad esempio set di dati, percorsi e molto altro.

### Aggiungi oggetto a un nuovo pacchetto {#add-object-to-new-package}

Seleziona **[!UICONTROL Schemi]** dal menu di navigazione a sinistra, quindi seleziona la **[!UICONTROL Sfoglia]** , in cui sono elencati gli schemi disponibili. Quindi, seleziona i puntini di sospensione (`...`) accanto allo schema selezionato, e un menu a discesa visualizza i controlli. Seleziona **[!UICONTROL Aggiungi al pacchetto]** dal menu a discesa.

![Elenco di schemi che mostrano il menu a discesa che evidenzia [!UICONTROL Aggiungi al pacchetto] controllo.](../images/ui/sandbox-tooling/add-to-package.png)

Dalla sezione **[!UICONTROL Aggiungi al pacchetto]** , seleziona la **[!UICONTROL Crea nuovo pacchetto]** opzione. Fornisci un [!UICONTROL Nome] per il pacchetto e un&#39;opzione [!UICONTROL Descrizione], quindi seleziona **[!UICONTROL Aggiungi]**.

![Il [!UICONTROL Aggiungi al pacchetto] dialogo con [!UICONTROL Crea nuovo pacchetto] selezionato ed evidenziazione [!UICONTROL Aggiungi].](../images/ui/sandbox-tooling/create-new-package.png)

Viene visualizzata di nuovo la **[!UICONTROL Schemi]** ambiente. È ora possibile aggiungere altri oggetti al pacchetto creato seguendo i passaggi successivi elencati di seguito.

### Aggiungere un oggetto a un pacchetto esistente e pubblicarlo {#add-object-to-existing-package}

Per visualizzare un elenco degli schemi disponibili, seleziona **[!UICONTROL Schemi]** dal menu di navigazione a sinistra, quindi seleziona la **[!UICONTROL Sfoglia]** scheda. Quindi, seleziona i puntini di sospensione (`...`) accanto allo schema selezionato per visualizzare le opzioni di controllo in un menu a discesa. Seleziona **[!UICONTROL Aggiungi al pacchetto]** dal menu a discesa.

![Elenco di schemi che mostrano il menu a discesa che evidenzia [!UICONTROL Aggiungi al pacchetto] controllo.](../images/ui/sandbox-tooling/add-to-package.png)

Il **[!UICONTROL Aggiungi al pacchetto]** viene visualizzata. Seleziona la **[!UICONTROL Pacchetto esistente]** , quindi selezionare **[!UICONTROL Nome pacchetto]** e selezionare il pacchetto richiesto. Infine, seleziona **[!UICONTROL Aggiungi]** per confermare le scelte effettuate.

![[!UICONTROL Aggiungi al pacchetto] , visualizzando un pacchetto selezionato dal menu a discesa.](../images/ui/sandbox-tooling/add-to-existing-package.png)

Viene elencato l&#39;elenco degli oggetti aggiunti al pacchetto. Per pubblicare il pacchetto e renderlo disponibile per l’importazione in sandbox, seleziona **[!UICONTROL Pubblica]**.

![Un elenco di oggetti nel pacchetto, che evidenzia [!UICONTROL Pubblica] opzione.](../images/ui/sandbox-tooling/publish-package.png)

Seleziona **[!UICONTROL Pubblica]** per confermare la pubblicazione del pacchetto.

![Finestra di conferma della pubblicazione del pacchetto, con evidenziazione [!UICONTROL Pubblica] opzione.](../images/ui/sandbox-tooling/publish-package-confirmation.png)

>[!NOTE]
>
>Una volta pubblicato, il contenuto del pacchetto non può essere modificato. Per evitare problemi di compatibilità, accertati che siano state selezionate tutte le risorse necessarie. Se è necessario apportare modifiche, è necessario creare un nuovo pacchetto.

Viene visualizzata di nuovo la **[!UICONTROL Pacchetti]** scheda in [!UICONTROL Sandbox] ambiente, in cui puoi visualizzare il nuovo pacchetto pubblicato.

![Elenco dei pacchetti sandbox che evidenziano il nuovo pacchetto pubblicato.](../images/ui/sandbox-tooling/published-packages.png)

## Importare un pacchetto in una sandbox di destinazione {#import-package-to-target-sandbox}

>[!NOTE]
>
>Tutte le azioni di importazione vengono registrate nei registri di audit.

Per importare il pacchetto in una sandbox di destinazione, passa a Sandbox **[!UICONTROL Sfoglia]** e seleziona l’opzione più (+) accanto al nome della sandbox.

![Le sandbox **[!UICONTROL Sfoglia]** evidenziare la selezione del pacchetto di importazione.](../images/ui/sandbox-tooling/browse-sandboxes.png)

Utilizzando il menu a discesa, seleziona la **[!UICONTROL Nome pacchetto]** desideri importare nella sandbox di destinazione. Aggiungi un **[!UICONTROL Nome processo]**, che saranno utilizzati per il monitoraggio futuro. Per impostazione predefinita, il profilo unificato viene disabilitato quando vengono importati gli schemi del pacchetto. Attiva/Disattiva **Abilitare gli schemi per il profilo** per abilitare questa funzione, seleziona **[!UICONTROL Successivo]**.

![La pagina dei dettagli di importazione che mostra [!UICONTROL Nome pacchetto] selezione a discesa](../images/ui/sandbox-tooling/import-package-to-sandbox.png)

Il [!UICONTROL Oggetto pacchetto e dipendenze] fornisce un elenco di tutte le risorse incluse in questo pacchetto. Il sistema rileva automaticamente gli oggetti dipendenti necessari per la corretta importazione degli oggetti padre selezionati. Eventuali attributi mancanti vengono visualizzati nella parte superiore della pagina. Seleziona **[!UICONTROL Visualizza dettagli]** per una suddivisione più dettagliata.

![Il [!UICONTROL Oggetto pacchetto e dipendenze] pagina mostra gli attributi mancanti.](../images/ui/sandbox-tooling/missing-attributes.png)

>[!NOTE]
>
>Gli oggetti dipendenti possono essere sostituiti con quelli esistenti nella sandbox di destinazione, consentendo di riutilizzare gli oggetti esistenti anziché creare una nuova versione. Ad esempio, quando importi un pacchetto che include schemi, puoi riutilizzare gli spazi dei nomi dei gruppi di campi personalizzati e delle identità esistenti nella sandbox di destinazione. In alternativa, quando importi un pacchetto che include Percorsi, puoi riutilizzare i segmenti esistenti nella sandbox di destinazione.

Per utilizzare un oggetto esistente, selezionare l&#39;icona della matita accanto all&#39;oggetto dipendente.

![Il [!UICONTROL Oggetto pacchetto e dipendenze] mostra un elenco di risorse incluse nel pacchetto.](../images/ui/sandbox-tooling/package-objects-and-dependencies.png)

Vengono visualizzate le opzioni per creare nuovi o utilizzare quelli esistenti. Seleziona **[!UICONTROL Usa esistente]**.

![Il [!UICONTROL Oggetto pacchetto e dipendenze] pagina che mostra le opzioni oggetto dipendente [!UICONTROL Crea nuovo] e [!UICONTROL Usa esistente].](../images/ui/sandbox-tooling/use-existing-object.png)

Il **[!UICONTROL Gruppo di campi]** mostra un elenco di gruppi di campi disponibili per l’oggetto. Seleziona i gruppi di campi richiesti, quindi seleziona **[!UICONTROL Salva]**.

![Un elenco di campi visualizzati sul [!UICONTROL Gruppo di campi] , evidenziando [!UICONTROL Salva] selezione. ](../images/ui/sandbox-tooling/field-group-list.png)

Viene visualizzata di nuovo la [!UICONTROL Oggetto pacchetto e dipendenze] pagina. Da qui, seleziona **[!UICONTROL Fine]** per completare l&#39;importazione del pacchetto.

![Il [!UICONTROL Oggetto pacchetto e dipendenze] mostra un elenco delle risorse incluse nel pacchetto, evidenziando [!UICONTROL Fine].](../images/ui/sandbox-tooling/finish-object-dependencies.png)

## Esportare e importare un’intera sandbox

>[!NOTE]
>
>Attualmente, per l’esportazione o l’importazione di un’intera sandbox sono supportati solo gli oggetti Real-time Customer Data Platform. Al momento, oggetti Adobe Journey Optimizer come i percorsi non sono supportati.

Puoi esportare tutti i tipi di oggetto supportati in un pacchetto sandbox completo, quindi importare il pacchetto in varie sandbox per replicare le configurazioni degli oggetti. Ad esempio, questa funzionalità consente di:

- Se devi reimpostare la sandbox, reimporta una sandbox per riprodurre tutte le configurazioni dell’oggetto
- Importa il pacchetto in altre sandbox e utilizzalo come sandbox blueprint per accelerare il processo di sviluppo.

### Esportare un’intera sandbox {#export-entire-sandbox}

Per esportare un’intera sandbox, passa a [!UICONTROL Sandbox] **[!UICONTROL Pacchetti]** e seleziona **[!UICONTROL Crea pacchetto]**.

![Il [!UICONTROL Sandbox] **[!UICONTROL Pacchetti]** evidenziazione scheda [!UICONTROL Crea pacchetto].](../images/ui/sandbox-tooling/create-sandbox-package.png)

Seleziona **[!UICONTROL Intera sandbox]** per [!UICONTROL Tipo di pacchetto] nel [!UICONTROL Crea pacchetto] . Fornisci un [!UICONTROL Nome pacchetto] per il nuovo pacchetto e selezionare **[!UICONTROL Sandbox]** dal menu a discesa. Infine, seleziona **[!UICONTROL Crea]** per confermare i dati immessi.

![Il [!UICONTROL Crea pacchetto] finestra di dialogo che mostra i campi completati ed evidenzia [!UICONTROL Crea].](../images/ui/sandbox-tooling/create-package-dialog.png)

Il pacchetto è stato creato correttamente, seleziona **[!UICONTROL Pubblica]** per pubblicare il pacchetto.

![Elenco dei pacchetti sandbox che evidenziano il nuovo pacchetto pubblicato.](../images/ui/sandbox-tooling/publish-entire-sandbox-packages.png)

Viene visualizzata di nuovo la **[!UICONTROL Pacchetti]** scheda in [!UICONTROL Sandbox] ambiente, in cui puoi visualizzare il nuovo pacchetto pubblicato.

### Importare l’intero pacchetto sandbox {#import-entire-sandbox-package}

>[!NOTE]
>
>Tutti gli oggetti verranno importati nella sandbox di destinazione come nuovi oggetti. È consigliabile importare un pacchetto sandbox completo in una sandbox vuota.

Per importare il pacchetto in una sandbox di destinazione, passa a [!UICONTROL Sandbox] **[!UICONTROL Sfoglia]** e seleziona l’opzione più (+) accanto al nome della sandbox.

![Le sandbox **[!UICONTROL Sfoglia]** evidenziare la selezione del pacchetto di importazione.](../images/ui/sandbox-tooling/browse-entire-package-sandboxes.png)

Utilizzando il menu a discesa, seleziona la sandbox completa utilizzando **[!UICONTROL Nome pacchetto]** a discesa. Aggiungi un **[!UICONTROL Nome processo]**, che sarà utilizzato per il monitoraggio futuro e un **[!UICONTROL Descrizione processo]**, quindi seleziona **[!UICONTROL Successivo]**.

![La pagina dei dettagli di importazione che mostra [!UICONTROL Nome pacchetto] selezione a discesa](../images/ui/sandbox-tooling/import-full-sandbox-package.png)

>[!NOTE]
>
>È necessario disporre delle autorizzazioni complete per tutti gli oggetti inclusi nel pacchetto. Se non disponi delle autorizzazioni necessarie, l’operazione di importazione non riuscirà e verranno visualizzati messaggi di errore.

Sei portato al [!UICONTROL Oggetto pacchetto e dipendenze] pagina in cui è possibile visualizzare il numero di oggetti e dipendenze importati ed esclusi. Da qui, seleziona **[!UICONTROL Importa]** per completare l&#39;importazione del pacchetto.

![Il [!UICONTROL Oggetto pacchetto e dipendenze] mostra il messaggio in linea dei tipi di oggetto non supportati, evidenziando [!UICONTROL Importa].](../images/ui/sandbox-tooling/finish-dependencies-entire-sandbox.png)

Attendere il completamento dell&#39;importazione. Il tempo necessario per il completamento può variare a seconda del numero di oggetti nel pacchetto. Puoi monitorare il processo di importazione da [!UICONTROL Sandbox] **[!UICONTROL Processi]** scheda.

## Monitorare i dettagli di importazione {#view-import-details}

Per visualizzare i dettagli importati, passare alla [!UICONTROL Sandbox] **[!UICONTROL Processi]** e selezionare il pacchetto dall&#39;elenco. In alternativa, utilizza la barra di ricerca per cercare il pacchetto.

![Le sandbox [!UICONTROL Processi] nella scheda viene evidenziata la selezione del pacchetto di importazione.](../images/ui/sandbox-tooling/imports-tab.png)

<!--### View imported objects {#view-imported-objects}

On the **[!UICONTROL Jobs]** tab in the [!UICONTROL Sandboxes] environment, select **[!UICONTROL View imported objects]** from the right details pane.

Select **[!UICONTROL View imported objects]** from the right details pane on the **[!UICONTROL Jobs]** tab in the [!UICONTROL Sandboxes] environment.

![The sandboxes [!UICONTROL Imports] tab highlights the [!UICONTROL View imported objects] selection in the right pane.](../images/ui/sandbox-tooling/view-imported-objects.png)

Use the arrows to expand objects to view the full list of fields that have been imported into the package.

![The sandboxes [!UICONTROL Imported objects] showing a list of objects imported into the package.](../images/ui/sandbox-tooling/expand-imported-objects.png)-->

Seleziona **[!UICONTROL Visualizza riepilogo importazioni]** dal riquadro dei dettagli a destra nella **[!UICONTROL Processi]** nell’ambiente Sandbox.

![Le sandbox [!UICONTROL Importazioni] La scheda evidenzia [!UICONTROL Visualizza dettagli importazione] nel riquadro di destra.](../images/ui/sandbox-tooling/view-import-details.png)

Il **[!UICONTROL Riepilogo importazione]** mostra una suddivisione delle importazioni con avanzamento in percentuale.

>[!NOTE]
>
>È possibile visualizzare un elenco di oggetti passando a pagine di inventario specifiche.

![Il [!UICONTROL Dettagli importazione] finestra di dialogo che mostra una ripartizione dettagliata delle importazioni.](../images/ui/sandbox-tooling/import-details.png)

Al termine dell’importazione, viene ricevuta una notifica nell’interfaccia utente di Platform. Puoi accedere a queste notifiche dall’icona degli avvisi. Se un processo non riesce, puoi passare alla risoluzione dei problemi da qui.

## Esercitazione video

Il video seguente illustra gli strumenti della sandbox e spiega come creare un nuovo pacchetto, pubblicarlo e importarlo.

>[!VIDEO](https://video.tv.adobe.com/v/3424763/?learn=on)

## Passaggi successivi

Questo documento illustra come utilizzare la funzione di strumenti sandbox nell’interfaccia utente di Experienci Platform. Per informazioni sulle sandbox, consulta [guida utente sulle sandbox](../ui/user-guide.md).

Per informazioni su come eseguire diverse operazioni utilizzando l’API Sandbox, consulta [guida per gli sviluppatori sulle sandbox](../api/getting-started.md). Per una panoramica di alto livello delle sandbox in questo Experience Platform, consulta [panoramica della documentazione](../home.md).
