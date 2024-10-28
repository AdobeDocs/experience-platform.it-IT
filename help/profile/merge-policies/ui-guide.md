---
title: Guida dell’interfaccia utente per i criteri di unione
type: Documentation
description: Scopri come utilizzare i criteri di unione utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 0489217a-6a53-428c-a531-fd0a0e5bb71f
source-git-commit: 400b20578e9a13fa2f41462b188707a34a462ea9
workflow-type: tm+mt
source-wordcount: '2455'
ht-degree: 0%

---


# Guida all’interfaccia dei criteri di unione

Adobe Experience Platform consente di unire frammenti di dati provenienti da più origini e di combinarli in modo da ottenere una visualizzazione completa di ciascuno dei singoli clienti. Quando si riuniscono questi dati, i criteri di unione sono le regole utilizzate da [!DNL Platform] per determinare la priorità dei dati e i dati che verranno combinati per creare la visualizzazione unificata.

Utilizzando le API RESTful o l’interfaccia utente di, puoi creare nuovi criteri di unione, gestire i criteri esistenti e impostare un criterio di unione predefinito per la tua organizzazione. Questa guida fornisce istruzioni dettagliate per l’utilizzo dei criteri di unione tramite l’interfaccia utente di Adobe Experience Platform.

Per ulteriori informazioni sui criteri di unione e sul ruolo che svolgono all&#39;interno di Experience Platform, leggere la [panoramica dei criteri di unione](overview.md).

## Introduzione

Questa guida richiede una buona conoscenza di diverse importanti funzionalità di [!DNL Experience Platform]. Prima di seguire questa guida, consulta la documentazione relativa ai seguenti servizi:

* [Profilo cliente in tempo reale](../home.md): fornisce un profilo consumatore unificato in tempo reale basato su dati aggregati provenienti da più origini.
* [Servizio Adobe Experience Platform Identity](../../identity-service/home.md): abilita il profilo cliente in tempo reale collegando le identità da diverse origini dati acquisite in [!DNL Platform].
* [Experience Data Model (XDM)](../../xdm/home.md): framework standardizzato tramite il quale [!DNL Platform] organizza i dati sull&#39;esperienza del cliente.

## Visualizza criteri di unione {#view-merge-policies}

>[!CONTEXTUALHELP]
>id="platform_errors_uplib_101221_404"
>title="Criterio di unione non trovato"
>abstract="Platform non è riuscito a trovare il criterio di unione richiesto. Per risolvere l’errore, prova una delle soluzioni seguenti:<ul><li>Verifica che nell’URL sia elencato l’ID corretto del criterio di unione.</li><li>Assicurati di disporre della combinazione corretta di sandbox e organizzazione per il criterio di unione a cui stai tentando di accedere.</li></ul>"

Nell&#39;interfaccia utente di [!DNL Experience Platform], è possibile iniziare a utilizzare i criteri di unione selezionando **[!UICONTROL Profili]** nell&#39;area di navigazione a sinistra e quindi selezionando la scheda **[!UICONTROL Criteri di unione]**.

Questa scheda include un elenco di tutti i criteri di unione esistenti per l’organizzazione, nonché i dettagli di ciascun criterio di unione, incluso il nome del criterio, indipendentemente dal fatto che il criterio di unione sia o meno il criterio di unione predefinito, e la classe di schema a cui il criterio di unione si riferisce.

![Viene visualizzata la pagina Sfoglia dei criteri di unione.](../images/merge-policies/landing.png)

Per selezionare i dettagli visibili o per aggiungere altre colonne alla visualizzazione, selezionare ![l&#39;icona delle impostazioni di colonna](../../images/icons/column-settings.png) e selezionare un nome di colonna per aggiungerla o rimuoverla dalla visualizzazione.

![Vengono visualizzate le opzioni disponibili per personalizzare la pagina Sfoglia dei criteri di unione.](../images/merge-policies/adjust-view.png)

## Creare un criterio di unione {#create-a-merge-policy}

Per creare un nuovo criterio di unione, seleziona **[!UICONTROL Crea criterio di unione]** nella scheda Criteri di unione per accedere al nuovo flusso di lavoro del criterio di unione.

![Pagina di destinazione dei criteri di unione con il pulsante Crea evidenziato.](../images/merge-policies/create-new.png)

Il flusso di lavoro **[!UICONTROL Nuovo criterio di unione]** richiede di fornire informazioni importanti per il nuovo criterio di unione tramite una serie di passaggi guidati. Questi passaggi sono descritti nelle sezioni che seguono.

![Nuovo flusso di lavoro per i criteri di unione.](../images/merge-policies/create.png)

## [!UICONTROL Configura] {#configure}

Il primo passaggio nel flusso di lavoro consente di configurare il criterio di unione fornendo informazioni di base. Queste informazioni includono:

* **[!UICONTROL Nome]**: il nome del criterio di unione deve essere descrittivo ma conciso.
* **[!UICONTROL Classe schema]**: classe dello schema XDM associata al criterio di unione. Specifica la classe di schema per la quale viene creato il criterio di unione. Le organizzazioni possono creare più criteri di unione per classe di schema. Attualmente nell&#39;interfaccia utente è disponibile solo la classe [!UICONTROL Profilo individuale XDM]. È possibile visualizzare in anteprima lo schema di unione per la classe dello schema selezionando **[!UICONTROL Visualizza schema di unione]**. Per ulteriori informazioni, vedere la sezione seguente [visualizzazione dello schema di unione](#view-union-schema).
* **[!UICONTROL Unione ID]**: questo campo definisce come determinare le identità correlate di un cliente. Esistono due possibili valori per l’unione di identità ed è importante comprendere in che modo il tipo di unione di identità selezionato influirà sui dati. Per ulteriori informazioni, consulta la [panoramica dei criteri di unione](overview.md).
   * **[!UICONTROL Nessuno]**: non eseguire alcuna unione di identità.
   * **[!UICONTROL Grafico privato]**: esegui l&#39;unione delle identità in base al grafico delle identità private.
* **[!UICONTROL Criterio di unione predefinito]**: pulsante di attivazione/disattivazione che consente di scegliere se il criterio di unione sarà o meno il criterio predefinito per l&#39;organizzazione. Se il selettore è attivato, viene visualizzato un avviso che richiede di confermare la modifica del criterio di unione predefinito dell&#39;organizzazione. Per ulteriori informazioni sui criteri di unione predefiniti, consulta la [panoramica dei criteri di unione](overview.md).
  ![Un popover che spiega cosa accade quando il criterio di unione viene impostato come criterio di unione predefinito.](../images/merge-policies/create-make-default.png)
* **[!UICONTROL Criterio di unione attivo su Edge]**: pulsante di attivazione/disattivazione che consente di selezionare se il criterio di unione sarà attivo o meno su Edge. Per garantire che tutti i consumatori di profili utilizzino la stessa vista sugli spigoli, i criteri di unione possono essere contrassegnati come attivi sugli spigoli. Per attivare un pubblico in Edge (contrassegnato come pubblico Edge), è necessario legarlo a un criterio di unione contrassegnato come attivo in Edge. Se un pubblico è **non** associato a un criterio di unione contrassegnato come attivo sul server Edge, il pubblico non verrà contrassegnato come attivo sul server Edge e verrà contrassegnato come pubblico in streaming. Inoltre, ogni sandbox in un&#39;organizzazione può avere solo **un** criterio di unione attivo su Edge.

Una volta completati i campi obbligatori, puoi selezionare **[!UICONTROL Successivo]** per continuare con il flusso di lavoro.

![Schermata Configura completata con il pulsante Avanti evidenziato.](../images/merge-policies/create-complete.png)

## [!UICONTROL Visualizza schema unione] {#view-union-schema}

Quando crei o modifichi un criterio di unione, puoi visualizzare lo schema di unione per la classe di schema selezionata selezionando **[!UICONTROL Visualizza schema di unione]**.

![Il pulsante &quot;Visualizza schema unione&quot; è evidenziato nel flusso di lavoro del nuovo criterio di unione.](../images/merge-policies/view-union-schema.png)

Verrà aperta la finestra di dialogo [!UICONTROL Visualizza schema unione], in cui sono visualizzati tutti gli schemi, le identità e le relazioni associati allo schema di unione. Puoi utilizzare la finestra di dialogo per esplorare lo schema di unione nello stesso modo in cui accedi alla scheda [!UICONTROL Schema di unione] nella sezione [!UICONTROL Profili] dell&#39;interfaccia utente di Platform.

Per informazioni dettagliate sugli schemi di unione, tra cui come interagire con essi nella scheda [!UICONTROL Schema unione] o nella finestra di dialogo [!UICONTROL Visualizza schema unione] visualizzata nel flusso di lavoro dei criteri di unione, visita la [guida dell&#39;interfaccia utente dello schema unione](../ui/union-schema.md).

![Finestra di dialogo Visualizza schema di unione.](../images/merge-policies/view-union-schema-dialog.png)

## [!UICONTROL Seleziona set di dati profilo] {#select-profile-datasets}

Nella schermata **[!UICONTROL Seleziona set di dati profilo]**, è necessario selezionare il **[!UICONTROL metodo di unione]** che si desidera utilizzare per il criterio di unione. Sullo schermo viene visualizzato anche il numero totale di [!UICONTROL set di dati profilo] nell&#39;organizzazione relativi alla classe dello schema selezionata nella schermata precedente.

A seconda del metodo di unione scelto, tutti i set di dati profilo verranno uniti in base all’ordine in cui sono stati aggiornati l’ultima volta (marca temporale ordinata) oppure dovrai selezionare i set di dati profilo da includere nel criterio di unione e l’ordine in cui unirli (precedenza set di dati).

Per ulteriori informazioni sui metodi di unione, consulta la [panoramica dei criteri di unione](overview.md).

>[!BEGINTABS]

>[!TAB Timestamp ordinato]

Se si seleziona **[!UICONTROL Timestamp ordinato]** come metodo di unione, gli attributi dei set di dati aggiornati più di recente avranno la precedenza. Questo si applica a tutti i set di dati profilo.

>[!NOTE]
>
>Il numero tra parentesi quadre accanto a **[!UICONTROL Set di dati profilo]** (ad esempio, `(37)` nell&#39;immagine visualizzata) mostra il numero totale di set di dati profilo che verranno inclusi.

![Immagine che mostra il metodo di unione ordinato per marca temporale in fase di selezione.](../images/merge-policies/timestamp-ordered.png)

>[!TAB Precedenza set di dati]

Se si seleziona **[!UICONTROL Precedenza set di dati]** come metodo di unione, è necessario selezionare i set di dati profilo e assegnarvi manualmente le priorità. Ogni set di dati elencato include anche lo stato dell’ultimo batch acquisito o visualizza un avviso che indica che non è stato acquisito alcun batch in tale set di dati.

Dall’elenco dei set di dati puoi selezionare fino a 50 set di dati da includere nel criterio di unione.

>[!NOTE]
>
>Il numero tra parentesi quadre accanto a **[!UICONTROL Set di dati profilo]** (ad esempio, `(37)` nell&#39;immagine mostrata) mostra il numero totale di set di dati profilo disponibili per la selezione.

Quando i set di dati vengono selezionati, vengono aggiunti alla sezione **[!UICONTROL Seleziona set di dati]**, che consente di trascinare e rilasciare i set di dati e di ordinarli in base alla precedenza desiderata. Man mano che i set di dati vengono regolati nell’elenco, viene aggiornato il numero ordinale (1, 2, 3, ecc.) accanto al set di dati, con priorità visualizzabile (1 a cui viene assegnata la priorità più alta, quindi 2 e in avanti).

La selezione di un set di dati aggiorna anche la sezione **[!UICONTROL Schema di unione]**, mostrando i campi nello schema di unione a cui ogni set di dati contribuisce. Per ulteriori informazioni sugli schemi di unione, tra cui come interagire con le visualizzazioni nell&#39;interfaccia utente, consulta la [guida dell&#39;interfaccia utente dello schema di unione](../ui/union-schema.md)

![Immagine che mostra la precedenza del set di dati selezionato, insieme alle impostazioni corrispondenti che è necessario scegliere se tale opzione è selezionata.](../images/merge-policies/dataset-precedence.png)

>[!ENDTABS]

## [!UICONTROL Seleziona set di dati ExperienceEvent] {#select-experienceevent-datasets}

Il passaggio successivo nel flusso di lavoro richiede la selezione di set di dati ExperienceEvent. Questa schermata è influenzata dal metodo di unione selezionato nella schermata [[!UICONTROL Seleziona set di dati profilo]](#select-profile-datasets).

>[!BEGINTABS]

>[!TAB Timestamp ordinato]

Se hai selezionato **[!UICONTROL Timestamp ordinato]** come metodo di unione per i set di dati profilo, anche qui avranno la precedenza gli attributi dei set di dati ExperienceEvent aggiornati più di recente.

>[!NOTE]
>
>Il numero tra parentesi quadre accanto a **[!UICONTROL Set di dati ExperienceEvent]** (ad esempio, `(1)` nell&#39;immagine visualizzata) mostra il numero totale di set di dati ExperienceEvent creati dall&#39;organizzazione e correlati alla classe di schema selezionata nella schermata di configurazione del criterio di unione.

![Viene visualizzato il numero totale di set di dati ExperienceEvent che possono essere correlati alla classe dello schema.](../images/merge-policies/timestamp-experienceevent.png)

>[!TAB Precedenza set di dati]

Se hai selezionato **[!UICONTROL Precedenza set di dati]** come metodo di unione per i set di dati profilo, dovrai selezionare i set di dati ExperienceEvent da includere. Puoi selezionare fino a 50 set di dati ExperienceEvent dall’elenco dei set di dati.

>[!NOTE]
>
>Il numero tra parentesi quadre accanto a **[!UICONTROL Set di dati ExperienceEvent]** (ad esempio, `(1)` nell&#39;immagine visualizzata) mostra il numero totale di set di dati ExperienceEvent creati dall&#39;organizzazione e correlati alla classe di schema selezionata nella schermata di configurazione del criterio di unione.

I set di dati selezionati vengono visualizzati nella sezione [!UICONTROL Seleziona set di dati].

I set di dati ExperienceEvent non possono essere ordinati manualmente, ma gli attributi nei set di dati ExperienceEvent vengono aggiunti ai set di dati profilo se fanno parte dello stesso frammento di profilo.

Analogamente alla selezione dei set di dati profilo, la selezione di un set di dati ExperienceEvent aggiorna anche la sezione **[!UICONTROL Schema di unione]**, mostrando i campi nello schema di unione a cui ogni set di dati contribuisce. Per ulteriori informazioni sugli schemi di unione, tra cui come interagire con le visualizzazioni nell&#39;interfaccia utente, consulta la [guida dell&#39;interfaccia utente dello schema di unione](../ui/union-schema.md).

![Vengono visualizzati i set di dati ExperienceEvent selezionabili.](../images/merge-policies/dataset-precedence-experienceevent.png)

>[!ENDTABS]

## [!UICONTROL Revisione] {#review}

L’ultimo passaggio nel flusso di lavoro consiste nel rivedere il criterio di unione. Nella schermata **[!UICONTROL Revisione]** vengono visualizzate informazioni sul criterio di unione, inclusi il metodo di unione ID selezionato, il metodo di unione selezionato e i set di dati inclusi. Per visualizzare tutti i set di dati Profilo o ExperienceEvent inclusi, seleziona il numero di set di dati per espandere l’elenco a discesa.

Nella schermata di revisione è inclusa anche la tabella **[!UICONTROL Anteprima dati]** che mostra i record del profilo di esempio che utilizzano i criteri di unione. Questo consente di visualizzare in anteprima l’aspetto di un profilo cliente prima di salvare il criterio di unione.

Verifica attentamente la configurazione dei criteri di unione e visualizza in anteprima i dati prima di selezionare **[!UICONTROL Fine]** per completare il flusso di lavoro di creazione.

>[!BEGINTABS]

>[!TAB Timestamp ordinato]

Se hai selezionato **[!UICONTROL Timestamp ordinato]** come metodo di unione per il criterio di unione, l&#39;elenco dei set di dati profilo include tutti i set di dati creati dall&#39;organizzazione relativi alla classe dello schema, in ordine di timestamp. L’elenco dei set di dati ExperienceEvent include tutti i set di dati creati dalla tua organizzazione per la classe di schema selezionata e verranno aggiunti ai set di dati profilo.

La tabella **[!UICONTROL Anteprima dati]** mostra record di profilo di esempio in base a un ordine di marca temporale dei set di dati. Questo consente di visualizzare in anteprima l’aspetto di un profilo cliente prima di salvare il criterio di unione.

Seleziona **[!UICONTROL Fine]** per creare il nuovo criterio di unione.

![Viene visualizzata la pagina Revisione. Questa pagina consente di esaminare i dettagli del criterio di unione appena creato.](../images/merge-policies/timestamp-review.png)

>[!TAB Precedenza set di dati]

Se hai selezionato **[!UICONTROL Precedenza set di dati]** come metodo di unione per il criterio di unione, gli elenchi dei set di dati Profile ed ExperienceEvent includono solo i set di dati Profile ed ExperienceEvent selezionati rispettivamente durante il flusso di lavoro di creazione. L’ordine dei set di dati profilo deve corrispondere alla precedenza specificata durante la creazione. In caso contrario, utilizzare il pulsante [!UICONTROL Indietro] per tornare ai passaggi del flusso di lavoro precedenti e regolare la priorità.

La tabella **[!UICONTROL Anteprima dati]** mostra i record del profilo di esempio che utilizzano i set di dati selezionati. Questo consente di visualizzare in anteprima l’aspetto di un profilo cliente prima di salvare il criterio di unione.

Seleziona **[!UICONTROL Fine]** per creare il nuovo criterio di unione.

![Viene visualizzata la pagina Revisione. Questa pagina consente di esaminare i dettagli del criterio di unione appena creato.](../images/merge-policies/dataset-precedence-review.png)

>[!ENDTABS]

## Modificare un criterio di unione {#edit}

Dalla scheda [!UICONTROL Criteri di unione], è possibile modificare un criterio di unione esistente creato per la classe [!DNL XDM Individual Profile] selezionando il **[!UICONTROL Nome criterio]** per il criterio di unione che si desidera modificare.

Quando viene visualizzata la schermata **[!UICONTROL Modifica criterio di unione]**, è possibile modificare il nome e il metodo [!UICONTROL unione ID], nonché specificare se questo criterio è il criterio di unione predefinito per l&#39;organizzazione.

Selezionare **[!UICONTROL Avanti]** per continuare il flusso di lavoro dei criteri di unione per aggiornare il metodo di unione e i set di dati inclusi nel criterio di unione.

![Viene visualizzato il flusso di lavoro per la modifica dei criteri di unione.](../images/merge-policies/edit-screen.png)

Dopo aver apportato le modifiche necessarie, rivedi il criterio di unione e seleziona **[!UICONTROL Fine]** per salvare le modifiche e tornare alla scheda [!UICONTROL Criteri di unione].

>[!WARNING]
>
>La modifica di un criterio di unione può influire sulla segmentazione e sui risultati del profilo, in quanto modificherà il modo in cui i conflitti di dati vengono risolti. Prima di salvare le modifiche apportate ai criteri di unione, assicurati di rivederle attentamente.

![Viene visualizzata la pagina di revisione del flusso di lavoro per la modifica dei criteri.](../images/merge-policies/edit-review.png)

## Violazioni dei criteri di governance dei dati

Durante la creazione o l’aggiornamento di un criterio di unione, viene eseguito un controllo per determinare se tale criterio viola uno dei criteri di utilizzo dei dati definiti dall’organizzazione. I criteri di utilizzo dei dati fanno parte della governance dei dati di Adobe Experience Platform e sono regole che descrivono i tipi di azioni di marketing che è consentito eseguire o meno su dati specifici di [!DNL Platform].

Ad esempio, se per creare un pubblico che si è attivato in una destinazione di terze parti è stato utilizzato un criterio di unione e nell&#39;organizzazione sono stati rilevati criteri di utilizzo dei dati che impediscono l&#39;esportazione di dati specifici a terze parti, durante il tentativo di salvataggio del criterio di unione verrà visualizzata una notifica di **[!UICONTROL violazione del criterio di governance dei dati]**.

Questa notifica include un elenco dei criteri di utilizzo dei dati che sono stati violati e consente di visualizzare i dettagli della violazione selezionando un criterio dall’elenco. Quando si seleziona un criterio violato, la scheda **[!UICONTROL Derivazione dati]** fornisce il motivo della violazione e le attivazioni interessate, ognuna delle quali fornisce ulteriori dettagli su come il criterio di utilizzo dei dati è stato violato.

Per ulteriori informazioni sulle modalità di esecuzione della governance dei dati in Adobe Experience Platform, consulta la [Panoramica sulla governance dei dati](../../data-governance/home.md).

## Passaggi successivi

Dopo aver creato e configurato i criteri di unione per la tua organizzazione, puoi utilizzarli per regolare la visualizzazione dei profili dei clienti in Platform e per creare tipi di pubblico dai dati del profilo. Per ulteriori informazioni su come creare e utilizzare i tipi di pubblico utilizzando l&#39;interfaccia utente e le API di [!DNL Experience Platform], consulta la [panoramica sulla segmentazione](../../segmentation/home.md).
