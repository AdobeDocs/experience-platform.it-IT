---
title: Guida dell’interfaccia utente per i criteri di unione
type: Documentation
description: Scopri come utilizzare i criteri di unione utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 0489217a-6a53-428c-a531-fd0a0e5bb71f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2458'
ht-degree: 2%

---


# Guida all’interfaccia dei criteri di unione

Adobe Experience Platform consente di unire frammenti di dati provenienti da più origini e di combinarli in modo da ottenere una visualizzazione completa di ciascuno dei singoli clienti. Quando si riuniscono questi dati, i criteri di unione sono le regole utilizzate da [!DNL Experience Platform] per determinare la priorità dei dati e i dati che verranno combinati per creare la visualizzazione unificata.

Utilizzando le API RESTful o l&#39;interfaccia utente, è possibile creare nuovi criteri di unione, gestire criteri esistenti e impostare un regola di unione predefinito per l&#39;organizzazione. In questa guida vengono fornite istruzioni dettagliate per l&#39;utilizzo dei criteri di unione utilizzando l&#39;interfaccia Adobe Experience Platform utente (interfaccia).

Per ulteriori informazioni sui criteri di unione e sul loro ruolo che svolgono all&#39;interno di Experience Platform, iniziare leggendo la panoramica](overview.md) dei [criteri di unione.

## Introduzione

Questa guida richiede una conoscenza pratica di diverse funzionalità importanti [!DNL Experience Platform] . Prima di seguire questa guida, consulta la documentazione relativa ai seguenti servizi:

* [Profilo](../home.md) cliente in tempo reale: fornisce un profilo cliente unificato e in tempo reale basato su dati aggregati provenienti da più fonti.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): abilita il profilo del cliente in tempo reale collegando le identità provenienti da diverse origini dati che vengono inserite in [!DNL Experience Platform].
* [Experience Data Model (XDM):](../../xdm/home.md) il framework standardizzato con cui [!DNL Experience Platform] organizza esperienza del cliente dati.

## Visualizzare i criteri di unione {#view-merge-policies}

>[!CONTEXTUALHELP]
>id="platform_errors_uplib_101221_404"
>title="Criterio di unione non trovato"
>abstract="Questo errore indica che non Experience Platform trovato il regola di unione richiesto. Per risolvere l’errore, prova una delle soluzioni seguenti:<ul><li>Assicurati che nell’URL sia elencato l’ID corretto del criterio di unione.</li><li>Assicurati di disporre della giusta combinazione di sandbox e organizzazione per il criterio di unione a cui stai tentando di accedere.</li></ul>"

Nell&#39;interfaccia utente di [!DNL Experience Platform], è possibile iniziare a utilizzare i criteri di unione selezionando **[!UICONTROL Profili]** nell&#39;area di navigazione a sinistra e quindi selezionando la scheda **[!UICONTROL Criteri di unione]**.

Questa scheda include un elenco di tutti i criteri di unione esistenti per l’organizzazione, nonché i dettagli di ciascun criterio di unione, incluso il nome del criterio, indipendentemente dal fatto che il criterio di unione sia o meno il criterio di unione predefinito, e la classe di schema a cui il criterio di unione si riferisce.

![Viene visualizzata la pagina Sfoglia dei criteri di unione.](../images/merge-policies/landing.png)

Per selezionare i dettagli visibili o per aggiungere altre colonne alla visualizzazione, selezionare ![l&#39;icona](../../images/icons/column-settings.png) delle impostazioni della colonna e selezionare un nome di colonna per aggiungerla o rimuoverla dalla visualizzazione.

![Vengono visualizzate le opzioni disponibili per personalizzare l&#39;unione regola la pagina di navigazione.](../images/merge-policies/adjust-view.png)

## Crea un regola di unione {#create-a-merge-policy}

Per creare un nuovo regola di unione, selezionare **[!UICONTROL Crea regola]** unione sui criteri di unione scheda per immettere il nuovo workflow di unione regola.

![Unisci la pagina di destinazione dei criteri con l&#39;pulsante Crea evidenziata.](../images/merge-policies/create-new.png)

L&#39;unione **[!UICONTROL Nuovo regola]** workflow richiede di fornire informazioni importanti per il nuovo regola di unione attraverso una serie di passaggi guidati. Questi passaggi sono descritti nelle sezioni seguire.

![La nuova unione regola workflow.](../images/merge-policies/create.png)

## [!UICONTROL Configura] {#configure}

Il primo passaggio della workflow consente di configurare il regola di unione fornendo informazioni di base. Queste informazioni includono:

* **[!UICONTROL Nome]**: il nome del regola di unione deve essere descrittivo ma conciso.
* **[!UICONTROL Classe schema]**: classe dello schema XDM associata al criterio di unione. Specifica la classe di schema per la quale viene creato il criterio di unione. Le organizzazioni possono creare più criteri di unione per classe di schema. Attualmente nell&#39;interfaccia utente è disponibile solo la classe [!UICONTROL Profilo individuale XDM]. È possibile visualizzare in anteprima lo schema di unione per la classe dello schema selezionando **[!UICONTROL Visualizza schema di unione]**. Per ulteriori informazioni, vedere la sezione sulla [visualizzazione dello schema](#view-union-schema) di unione che segue.
* **[!UICONTROL ID stitching]**: questo campo definisce come determinare le identità correlate di un cliente. Esistono due valori possibili per lo stitching dell&#39;identità ed è importante comprendere in che modo il tipo di unione dell&#39;identità selezionato influirà sui dati. Per ulteriori informazioni, consulta la panoramica](overview.md) dei [criteri di unione.
   * **[!UICONTROL Nessuna]**: non eseguire alcuna cucitura di identità.
   * **[!UICONTROL Grafico]** privato: esegui lo stitching dell&#39;identità in base al grafico dell&#39;identità privata.
* **[!UICONTROL Criterio di unione predefinito]**: pulsante di attivazione/disattivazione che consente di scegliere se il criterio di unione sarà o meno il criterio predefinito per l&#39;organizzazione. Se il selettore è attivato, viene visualizzato un avviso che richiede di confermare la modifica del criterio di unione predefinito dell&#39;organizzazione. Per ulteriori informazioni sui criteri di unione predefiniti, consulta la [panoramica dei criteri di unione](overview.md).
  ![Un popover che spiega cosa accade quando il criterio di unione viene impostato come criterio di unione predefinito.](../images/merge-policies/create-make-default.png)
* **[!UICONTROL Criterio di unione attivo su Edge]**: pulsante di attivazione/disattivazione che consente di selezionare se il criterio di unione sarà attivo o meno su Edge. Per garantire che tutti i consumatori di profilo lavorino con la stessa vista sugli edge, i criteri di unione possono essere contrassegnati come attivi sull&#39;edge. Affinché un pubblico possa essere attivato sul bordo (contrassegnato come pubblico edge), deve essere legato a un regola di unione contrassegnato come attivo sul bordo. Se un pubblico è **non** associato a un criterio di unione contrassegnato come attivo sul server Edge, il pubblico non verrà contrassegnato come attivo sul server Edge e verrà contrassegnato come pubblico in streaming. Inoltre, ogni sandbox in un&#39;organizzazione può avere solo **un** criterio di unione attivo su Edge.

Una volta completati i campi obbligatori, puoi selezionare **[!UICONTROL Successivo]** per continuare con il flusso di lavoro.

![Schermata Configura completata con il pulsante Avanti evidenziato.](../images/merge-policies/create-complete.png)

## [!UICONTROL Visualizza schema unione] {#view-union-schema}

Quando si crea o si modifica un regola di unione, è possibile visualizzare lo schema di unione per la classe di schema scelta selezionando **[!UICONTROL Visualizza schema]** dell&#39;unione.

![Il pulsante &quot;Visualizza schema unione&quot; è evidenziato nel flusso di lavoro del nuovo criterio di unione.](../images/merge-policies/view-union-schema.png)

Verrà aperta la finestra di dialogo [!UICONTROL Visualizza schema unione], in cui sono visualizzati tutti gli schemi, le identità e le relazioni associati allo schema di unione. Puoi utilizzare la finestra di dialogo per esplorare lo schema di unione nello stesso modo in cui accedi alla scheda [!UICONTROL Schema di unione] nella sezione [!UICONTROL Profili] dell&#39;interfaccia utente di Experience Platform.

Per informazioni dettagliate sugli schemi di unione, tra cui come interagire con essi nella scheda [!UICONTROL Schema unione] o nella finestra di dialogo [!UICONTROL Visualizza schema unione] visualizzata nel flusso di lavoro dei criteri di unione, visita la [guida dell&#39;interfaccia utente dello schema unione](../ui/union-schema.md).

![Finestra di dialogo Visualizza schema di unione.](../images/merge-policies/view-union-schema-dialog.png)

## [!UICONTROL Seleziona set di dati di profilo] {#select-profile-datasets}

**[!UICONTROL Nella schermata Seleziona set di]** dati di profilo, è necessario selezionare il **[!UICONTROL metodo]** di unione che si desidera utilizzare per il regola di unione. Sullo schermo viene visualizzato anche il numero totale di set di [!UICONTROL dati] Profile nell&#39;organizzazione relativi alla classe dello schema selezionata nella schermata precedente.

A seconda del metodo di unione scelto, tutti i set di dati del profilo verranno uniti in base all&#39;ordine in cui sono stati aggiornati l&#39;ultima volta (ordine di data e ora) oppure sarà necessario selezionare i set di dati di profilo da includere nel regola di unione e l&#39;ordine in cui unirli (precedenza del set di dati).

Per ulteriori informazioni sui metodi di unione, fare riferimento alla panoramica](overview.md) dei [criteri di unione.

>[!BEGINTABS]

>[!TAB Marca temporale ordinata]

Se si seleziona **[!UICONTROL Timestamp ordinato]** come metodo di unione, gli attributi dei set di dati aggiornati più di recente avranno la precedenza. Questo vale per tutti i set di dati del profilo.

>[!NOTE]
>
>Il numero tra parentesi quadre accanto a **[!UICONTROL Set di dati profilo]** (ad esempio, `(37)` nell&#39;immagine visualizzata) mostra il numero totale di set di dati profilo che verranno inclusi.

![Immagine che mostra il metodo di unione ordinato per marca temporale in fase di selezione.](../images/merge-policies/timestamp-ordered.png)

>[!TAB Precedenza set di dati]

Se si seleziona **[!UICONTROL Precedenza set di dati]** come metodo di unione, è necessario selezionare i set di dati profilo e assegnarvi manualmente le priorità. Ogni set di dati elencato include anche lo stato dell’ultimo batch acquisito o visualizza un avviso che indica che non è stato acquisito alcun batch in tale set di dati.

È possibile selezionare fino a 50 set di dati dall&#39;elenco dei set di dati da includere nel regola di unione.

>[!NOTE]
>
>Il numero tra parentesi accanto a **[!UICONTROL Set di dati]** di profilo (ad esempio, `(37)` nell&#39;immagine mostrata) mostra il numero totale di set di dati di profilo disponibili per la selezione.

Man mano che i set di dati vengono selezionati, vengono aggiunti alla **[!UICONTROL sezione Seleziona set di]** dati, consentendo di trascinare e rilasciare i set di dati e ordinarli in base alla precedenza desiderata. Man mano che i set di dati vengono regolati nell&#39;elenco, l&#39;ordinale (1, 2, 3, ecc.) accanto al set di dati verrà aggiornato, visualizzando la priorità (1 ha la priorità più alta, quindi 2 e oltre).

La selezione di un set di dati aggiorna anche la **[!UICONTROL sezione dello schema]** dell&#39;Unione, che mostra i campi nello schema dell&#39;unione a cui ogni set di dati contribuisce con i dati. Per ulteriori informazioni sugli schemi di unione, incluso come interagire con le visualizzazioni nel interfaccia, fare riferimento alla [guida allo schema di unione interfaccia](../ui/union-schema.md)

![Un&#39;immagine che mostra la precedenza del set di dati selezionato, insieme alle impostazioni corrispondenti che è necessario scegliere se tale opzione è selezionata.](../images/merge-policies/dataset-precedence.png)

>[!ENDTABS]

## [!UICONTROL Seleziona set di dati ExperienceEvent] {#select-experienceevent-datasets}

Il passaggio successivo della workflow richiede la selezione dei set di dati ExperienceEvent. Questa schermata è influenzata dal metodo di unione selezionato nella [[!UICONTROL schermata Seleziona set di]](#select-profile-datasets) dati profilo.

>[!BEGINTABS]

>[!TAB Marca temporale ordinata]

Se hai selezionato **[!UICONTROL Timestamp ordinato]** come metodo di unione per i set di dati Profile, anche in questo caso gli attributi dei set di dati ExperienceEvent aggiornati più di recente avranno la precedenza.

>[!NOTE]
>
>Il numero tra parentesi quadre accanto a **[!UICONTROL Set di dati ExperienceEvent]** (ad esempio, `(1)` nell&#39;immagine visualizzata) mostra il numero totale di set di dati ExperienceEvent creati dall&#39;organizzazione e correlati alla classe di schema selezionata nella schermata di configurazione del criterio di unione.

![Viene visualizzato il numero totale di set di dati ExperienceEvent che possono essere correlati alla classe dello schema.](../images/merge-policies/timestamp-experienceevent.png)

>[!TAB Precedenza set di dati]

Se hai selezionato **[!UICONTROL Precedenza set di dati]** come metodo di unione per i set di dati profilo, dovrai selezionare i set di dati ExperienceEvent da includere. Puoi selezionare fino a 50 set di dati ExperienceEvent dall’elenco dei set di dati.

>[!NOTE]
>
>Il numero tra parentesi quadre accanto a **[!UICONTROL Set di dati ExperienceEvent]** (ad esempio, `(1)` nell&#39;immagine visualizzata) mostra il numero totale di set di dati ExperienceEvent creati dall&#39;organizzazione e correlati alla classe di schema selezionata nella schermata di configurazione del criterio di unione.

Quando i set di dati vengono selezionati, vengono visualizzati nella [!UICONTROL sezione Seleziona set di] dati.

I set di dati ExperienceEvent non possono essere ordinati manualmente, ma gli attributi nei set di dati ExperienceEvent vengono aggiunti ai set di dati Profile se fanno parte dello stesso frammento di profilo.

Analogamente alla selezione di set di dati di profilo, la selezione di un set di dati ExperienceEvent aggiorna anche la **[!UICONTROL sezione dello schema]** dell&#39;unione, che mostra i campi nello schema dell&#39;unione a cui ogni set di dati contribuisce con i dati. Per ulteriori informazioni sugli schemi di unione, incluso come interagire con le visualizzazioni nel interfaccia, fare riferimento alla guida](../ui/union-schema.md) allo [schema di unione interfaccia.

![Vengono visualizzati i set di dati ExperienceEvent selezionabili.](../images/merge-policies/dataset-precedence-experienceevent.png)

>[!ENDTABS]

## [!UICONTROL Recensione] {#review}

L&#39;ultimo passaggio della workflow consiste nel rivedere il regola di unione. Nella **[!UICONTROL schermata Revisione]** vengono visualizzate informazioni sui regola di unione, inclusi il metodo di unione ID selezionato, il metodo di unione selezionato e i set di dati inclusi. Per visualizzare tutti i set di dati Profile o ExperienceEvent inclusi, selezionare il numero di set di dati per espandere l&#39;elenco a discesa.

Nella schermata di revisione è inclusa anche la **[!UICONTROL tabella di dati]** Anteprima che mostra i record di profilo di esempio utilizzando l&#39;regola di unione. In questo modo è possibile visualizzare in anteprima l&#39;aspetto like un profilo cliente prima di salvare il regola di unione.

Assicurarsi di esaminare attentamente la configurazione dei regola di unione e l&#39;anteprima dei dati prima di selezionare **[!UICONTROL Fine]** per completare il workflow di creazione.

>[!BEGINTABS]

>[!TAB Marca temporale ordinata]

Se hai selezionato **[!UICONTROL Timestamp ordinato]** come metodo di unione per il criterio di unione, l&#39;elenco dei set di dati profilo include tutti i set di dati creati dall&#39;organizzazione relativi alla classe dello schema, in ordine di timestamp. L’elenco dei set di dati ExperienceEvent include tutti i set di dati creati dalla tua organizzazione per la classe di schema selezionata e verranno aggiunti ai set di dati profilo.

La **[!UICONTROL tabella di dati]** Anteprima mostra record di profilo di esempio basati su un ordine di timestamp dei set di dati. Questo consente di visualizzare in anteprima l’aspetto di un profilo cliente prima di salvare il criterio di unione.

Selezionate **[!UICONTROL Fine]** per creare il nuovo regola di unione.

![Viene visualizzata la pagina Revisione. Questa pagina consente di esaminare i dettagli del regola di unione appena creato.](../images/merge-policies/timestamp-review.png)

>[!TAB Precedenza set di dati]

Se è stata selezionata **[!UICONTROL la precedenza]** del set di dati come metodo di unione per il regola di unione, gli elenchi di set di dati Profile ed ExperienceEvent includono rispettivamente solo i set di dati Profile ed ExperienceEvent selezionati durante la creazione workflow. L&#39;ordine dei set di dati Profilo deve corrispondere alla precedenza specificata durante la creazione. In caso contrario, utilizza il [!UICONTROL pulsante Indietro] per tornare ai passaggi workflow precedenti e regolare la priorità.

La **[!UICONTROL tabella di dati]** Anteprima mostra i record di profilo di esempio utilizzando i set di dati selezionati. In questo modo è possibile visualizzare in anteprima l&#39;aspetto like un profilo cliente prima di salvare il regola di unione.

Selezionate **[!UICONTROL Fine]** per creare il nuovo regola di unione.

![Viene visualizzata la pagina Revisione. Questa pagina consente di esaminare i dettagli del regola di unione appena creato.](../images/merge-policies/dataset-precedence-review.png)

>[!ENDTABS]

## Modifica un regola di unione {#edit}

[!UICONTROL Dalla scheda Criteri] di unione è possibile modificare un regola di unione esistente creato per la [!DNL XDM Individual Profile] classe selezionando il nome ]**del**[!UICONTROL  criterio per il regola di unione che si desidera modificare.

Quando viene visualizzata la **[!UICONTROL schermata Modifica unione regola]**, è possibile apportare modifiche al metodo di unione] del nome e [!UICONTROL dell&#39;ID, nonché stabilire se questo regola sia o meno il regola di unione predefinito per l&#39;organizzazione.

Selezionare **[!UICONTROL Successivo]** continuare con l&#39;workflow di unione regola per aggiornare il metodo di unione e i set di dati inclusi nel regola di unione.

![Viene visualizzato il flusso di lavoro per la modifica dei criteri di unione.](../images/merge-policies/edit-screen.png)

Dopo aver apportato le modifiche necessarie, rivedi il criterio di unione e seleziona **[!UICONTROL Fine]** per salvare le modifiche e tornare alla scheda [!UICONTROL Criteri di unione].

>[!WARNING]
>
>La modifica di un criterio di unione può influire sulla segmentazione e sui risultati del profilo, in quanto modificherà il modo in cui i conflitti di dati vengono risolti. Prima di salvare le modifiche apportate ai criteri di unione, assicurati di rivederle attentamente.

![Viene visualizzata la pagina di revisione del flusso di lavoro per la modifica dei criteri.](../images/merge-policies/edit-review.png)

## Violazioni dei criteri di governance dei dati

Quando si crea o si aggiorna un regola di unione, viene eseguito un controllo per determinare se il regola di unione viola uno dei criteri di utilizzo dei dati definiti dall&#39;organizzazione. I criteri di utilizzo dei dati fanno parte di Adobe Experience Platform Data Governance e sono regole che descrivono i tipi di azioni marketing consentite o limitate a eseguire su dati specifici [!DNL Experience Platform] .

Ad esempio, se un regola di unione è stato utilizzato per creare un pubblico attivato in una destinazione di terze parti e l&#39;organizzazione ha avuto un utilizzo dei dati regola impedire l&#39;esportazione di dati specifici a terze parti, si riceverà una **[!UICONTROL violazione della governance dei dati rilevata]** regola notifica quando si tenta di salvare il regola di unione.

Questo notifica include un elenco dei criteri di utilizzo dei dati che sono stati violati e consente di visualizzare i dettagli della violazione selezionando un regola dall&#39;elenco. Dopo aver selezionato un regola violato, il **[!UICONTROL scheda Data lineage]** fornisce il motivo della violazione e le attivazioni interessate, fornendo ciascuno maggiori dettagli su come è stato violato il regola di utilizzo dei dati.

Per ulteriori informazioni sulle modalità di esecuzione della governance dei dati in Adobe Experience Platform, consulta la [Panoramica sulla governance dei dati](../../data-governance/home.md).

## Passaggi successivi

Ora che hai creato e configurato i criteri di unione per la tua organizzazione, puoi utilizzarli per regolare la visualizzazione dei profili dei clienti all&#39;interno di Experience Platform e per creare tipi di pubblico dai dati del tuo profilo. Per ulteriori informazioni su come creare e utilizzare i tipi di pubblico utilizzando l&#39;interfaccia utente e le API di [!DNL Experience Platform], consulta la [panoramica sulla segmentazione](../../segmentation/home.md).
