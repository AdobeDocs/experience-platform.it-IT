---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;criteri di unione;interfaccia utente;interfaccia utente;timestamp ordinato;precedenza set di dati
title: Guida all’interfaccia utente per i criteri di unione
type: Documentation
description: Quando si riuniscono dati provenienti da più origini in Experience Platform, i criteri di unione sono le regole utilizzate da Platform per determinare in che modo i dati verranno definiti come prioritari e quali dati verranno combinati per creare la visualizzazione unificata. Questa guida fornisce istruzioni passo per l’utilizzo dei criteri di unione tramite l’interfaccia utente di Adobe Experience Platform.
exl-id: 0489217a-6a53-428c-a531-fd0a0e5bb71f
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2321'
ht-degree: 0%

---


# Guida all’interfaccia utente per i criteri di unione

Adobe Experience Platform consente di unire frammenti di dati provenienti da più sorgenti e di combinarli per ottenere una visualizzazione completa di ciascuno dei singoli clienti. Quando si uniscono questi dati, i criteri di unione sono regole che [!DNL Platform] utilizza per determinare come assegnare una priorità ai dati e quali saranno i dati combinati per creare la visualizzazione unificata.

Utilizzando le API RESTful o l&#39;interfaccia utente, è possibile creare nuovi criteri di unione, gestire i criteri esistenti e impostare un criterio di unione predefinito per la propria organizzazione. Questa guida fornisce istruzioni passo per l’utilizzo dei criteri di unione tramite l’interfaccia utente di Adobe Experience Platform.

Per ulteriori informazioni sui criteri di unione e sul loro ruolo nell&#39;Experience Platform, si prega di iniziare leggendo il [panoramica dei criteri di unione](overview.md).

## Introduzione

Questa guida richiede una comprensione operativa di diverse importanti [!DNL Experience Platform] funzionalità. Prima di seguire questa guida, consulta la documentazione relativa ai seguenti servizi:

* [Profilo cliente in tempo reale](../home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Servizio Adobe Experience Platform Identity](../../identity-service/home.md): Abilita il profilo del cliente in tempo reale collegando le identità di diverse origini dati in cui viene effettuato l’acquisizione [!DNL Platform].
* [Experience Data Model (XDM)](../../xdm/home.md): Il quadro standardizzato [!DNL Platform] organizza i dati sulla customer experience.

## Visualizza criteri di unione {#view-merge-policies}

All&#39;interno di [!DNL Experience Platform] Per iniziare a utilizzare i criteri di unione, seleziona **[!UICONTROL Profili]** nella navigazione a sinistra e quindi selezionando la **[!UICONTROL Unisci criteri]** scheda . Questa scheda include un elenco di tutti i criteri di unione esistenti per l&#39;organizzazione, nonché i dettagli relativi a ciascun criterio di unione, compreso il nome del criterio, se il criterio di unione è o meno il criterio di unione predefinito e la classe dello schema a cui il criterio di unione fa riferimento.

![Pagina di destinazione dei criteri di unione](../images/merge-policies/landing.png)

Per selezionare i dettagli visibili o per aggiungere ulteriori colonne alla visualizzazione, selezionare **[!UICONTROL Configurare le colonne]** e fai clic sul nome di una colonna per aggiungerla o rimuoverla dalla visualizzazione.

![](../images/merge-policies/adjust-view.png)

## Creare un criterio di unione {#create-a-merge-policy}

Per creare un nuovo criterio di unione, selezionare **[!UICONTROL Crea criterio di unione]** nella scheda criteri di unione per accedere al nuovo flusso di lavoro dei criteri di unione.

![Pagina di destinazione dei criteri di unione con il pulsante di creazione evidenziato.](../images/merge-policies/create-new.png)

La **[!UICONTROL Nuovo criterio di unione]** flusso di lavoro, richiede di fornire informazioni importanti per il nuovo criterio di unione tramite una serie di passaggi guidati. Questi passaggi sono descritti nelle sezioni che seguono.

![Il nuovo flusso di lavoro dei criteri di unione.](../images/merge-policies/create.png)

## [!UICONTROL Configurare gli] {#configure}

Il primo passaggio del flusso di lavoro consente di configurare i criteri di unione fornendo informazioni di base. Queste informazioni includono:

* **[!UICONTROL Nome]**: Il nome del criterio di unione deve essere descrittivo ma conciso.
* **[!UICONTROL Classe schema]**: Classe dello schema XDM associata al criterio di unione. Specifica la classe dello schema per la quale viene creato il criterio di unione. Le organizzazioni possono creare più criteri di unione per classe di schema. Attualmente solo il [!UICONTROL Profilo individuale XDM] La classe è disponibile nell’interfaccia utente di . È possibile visualizzare in anteprima lo schema dell&#39;unione per la classe dello schema selezionando **[!UICONTROL Visualizza schema unione]**. Per ulteriori informazioni, consulta la sezione su [visualizzazione dello schema unione](#view-union-schema) segue.
* **[!UICONTROL unione degli ID]**: Questo campo definisce come determinare le identità correlate di un cliente. Esistono due possibili valori per le unione identità ed è importante comprendere in che modo il tipo di unione identità selezionato influirà sui dati. Per ulteriori informazioni, consulta la sezione [panoramica dei criteri di unione](overview.md).
   * **[!UICONTROL Nessuno]**: Non eseguire alcuna unione di identità.
   * **[!UICONTROL Grafico privato]**: Eseguire unione di identità in base al grafico di identità privata.
* **[!UICONTROL Criterio di unione predefinito]**: Pulsante di attivazione/disattivazione che consente di selezionare se il criterio di unione sarà o meno il valore predefinito per l&#39;organizzazione. Se il selettore è attivato, viene visualizzato un avviso che richiede di confermare la modifica dei criteri di unione predefiniti dell&#39;organizzazione. Consulta la sezione [panoramica dei criteri di unione](overview.md) per ulteriori informazioni sui criteri di unione predefiniti.
   ![](../images/merge-policies/create-make-default.png)
* **[!UICONTROL Criterio di unione attiva sul bordo]**: Pulsante di attivazione/disattivazione che consente di selezionare se il criterio di unione è attivo o meno sul bordo. Per garantire che tutti i consumatori di profili lavorino con la stessa vista sui bordi, i criteri di unione possono essere contrassegnati come attivi sui bordi. Affinché un segmento possa essere attivato sul bordo (contrassegnato come segmento edge), deve essere associato a un criterio di unione contrassegnato come attivo sul bordo. Se un segmento è **not** associato a un criterio di unione contrassegnato come attivo sul bordo, il segmento non sarà contrassegnato come attivo sul bordo e sarà contrassegnato come segmento in streaming. Inoltre, ogni sandbox in un&#39;organizzazione può avere solo **uno** criterio di unione attivo sul bordo.

Una volta completati i campi obbligatori, puoi selezionare **[!UICONTROL Successivo]** per continuare con il flusso di lavoro.

![Schermata Configura completa con il pulsante Successivo evidenziato.](../images/merge-policies/create-complete.png)

## [!UICONTROL Visualizza schema unione] {#view-union-schema}

Quando si crea o si modifica un criterio di unione, è possibile visualizzare lo schema di unione per la classe di schema selezionata selezionando **[!UICONTROL Visualizza schema unione]**.

![](../images/merge-policies/view-union-schema.png)

Viene aperta la [!UICONTROL Visualizza schema unione] finestra di dialogo, che mostra tutti gli schemi, le identità e le relazioni associati allo schema di unione. Puoi utilizzare la finestra di dialogo per esplorare lo schema dell&#39;unione nello stesso modo in cui accedi al [!UICONTROL Schema dell&#39;unione] nella scheda [!UICONTROL Profili] nell’interfaccia utente di Platform.

Per informazioni dettagliate sugli schemi di unione, incluso come interagire con essi nel [!UICONTROL Schema dell&#39;unione] oppure [!UICONTROL Visualizza schema unione] finestra di dialogo visualizzata nel flusso di lavoro dei criteri di unione, visitare il [guida all’interfaccia utente per schema unione](../ui/union-schema.md).

![](../images/merge-policies/view-union-schema-dialog.png)

## [!UICONTROL Seleziona set di dati profilo] {#select-profile-datasets}

Sulla **[!UICONTROL Seleziona set di dati profilo]** seleziona la **[!UICONTROL Metodo Merge]** che si desidera utilizzare per i criteri di unione. Sullo schermo viene inoltre visualizzato il numero totale di [!UICONTROL Set di dati di profilo] nell&#39;organizzazione che si riferiscono alla classe dello schema selezionata nella schermata precedente.

A seconda del metodo di unione scelto, tutti i set di dati Profilo verranno uniti in base all’ordine in cui sono stati aggiornati per l’ultima volta (timestamp ordered) oppure dovrai selezionare i set di dati Profilo da includere nel criterio di unione e l’ordine in cui unirli (precedenza set di dati).

Per ulteriori informazioni sui metodi di unione, consulta la sezione [panoramica dei criteri di unione](overview.md).

### Timestamp ordinato {#timestamp-ordered-profile}

Selezione **[!UICONTROL Timestamp ordinato]** poiché il metodo di unione indica che gli attributi dei set di dati aggiornati più di recente avranno la precedenza. Questo vale per tutti i set di dati di profilo.

>[!NOTE]
>
>Il numero tra parentesi accanto a **[!UICONTROL Set di dati di profilo]** (ad esempio, `(37)` nell’immagine mostrata) mostra il numero totale di set di dati di profilo che verranno inclusi.

![](../images/merge-policies/timestamp-ordered.png)

### Precedenza del set di dati {#dataset-precedence-profile}

Selezione **[!UICONTROL Precedenza del set di dati]** poiché il metodo di unione richiede di selezionare i set di dati Profilo e di assegnarli manualmente una priorità. Ogni set di dati elencato include anche lo stato dell’ultimo batch acquisito o visualizza un avviso che nessun batch è stato acquisito in tale set di dati.

È possibile selezionare fino a 50 set di dati dall’elenco dei set di dati da includere nel criterio di unione.

>[!NOTE]
>
>Il numero tra parentesi accanto a **[!UICONTROL Set di dati di profilo]** (ad esempio, `(37)` nell’immagine mostrata) mostra il numero totale di set di dati di profilo disponibili per la selezione.

Quando sono selezionati, i set di dati vengono aggiunti al **[!UICONTROL Seleziona set di dati]** , che consente di trascinare e rilasciare i set di dati e di ordinarli in base alla precedenza desiderata. Poiché i set di dati vengono regolati nell’elenco, il numero ordinale (1, 2, 3, ecc.) accanto al set di dati viene aggiornato, mostrando la priorità (1 con la priorità più elevata, quindi 2 e successivi).

La selezione di un set di dati aggiorna anche la **[!UICONTROL Schema dell&#39;unione]** , mostrando i campi nello schema unione a cui ogni set di dati contribuisce i dati. Per ulteriori informazioni sugli schemi di unione, tra cui come interagire con le visualizzazioni nell’interfaccia utente, fai riferimento al [guida all’interfaccia utente per schema unione](../ui/union-schema.md)

![](../images/merge-policies/dataset-precedence.png)

## [!UICONTROL Seleziona set di dati ExperienceEvent] {#select-experienceevent-datasets}

Il passaggio successivo nel flusso di lavoro richiede la selezione dei set di dati ExperienceEvent . Questa schermata è influenzata dal metodo di unione selezionato nella [[!UICONTROL Seleziona set di dati profilo]](#select-profile-datasets) schermo.

### Timestamp ordinato {#timestamp-ordered-experienceevent}

Se hai selezionato **[!UICONTROL Timestamp ordinato]** come metodo di unione per i set di dati Profilo, anteporrà anche agli attributi dei set di dati ExperienceEvent aggiornati più di recente.

>[!NOTE]
>
>Il numero tra parentesi accanto a **[!UICONTROL Set di dati ExperienceEvent]** (ad esempio, `(20)` nell&#39;immagine mostrata) mostra il numero totale di set di dati ExperienceEvent creati dalla tua organizzazione relativi alla classe dello schema selezionata nella schermata di configurazione del criterio di unione.

![](../images/merge-policies/timestamp-experienceevent.png)

### Precedenza del set di dati {#dataset-precedence-experienceevent}

Se hai selezionato **[!UICONTROL Precedenza del set di dati]** come metodo di unione per i set di dati Profilo, dovrai selezionare i set di dati ExperienceEvent da includere. Puoi selezionare fino a 50 set di dati ExperienceEvent dall’elenco dei set di dati.

>[!NOTE]
>
>Il numero tra parentesi accanto a **[!UICONTROL Set di dati ExperienceEvent]** (ad esempio, `(20)` nell&#39;immagine mostrata) mostra il numero totale di set di dati ExperienceEvent creati dalla tua organizzazione relativi alla classe dello schema selezionata nella schermata di configurazione del criterio di unione.

Quando sono selezionati, i set di dati vengono visualizzati nella [!UICONTROL Seleziona set di dati] sezione .

I set di dati ExperienceEvent non possono essere ordinati manualmente, ma gli attributi nei set di dati ExperienceEvent vengono aggiunti ai set di dati Profile se fanno parte dello stesso frammento di profilo.

Simile alla selezione dei set di dati Profilo, la selezione di un set di dati ExperienceEvent comporta anche l’aggiornamento del **[!UICONTROL Schema dell&#39;unione]** , mostrando i campi nello schema unione a cui ogni set di dati contribuisce i dati. Per ulteriori informazioni sugli schemi di unione, tra cui come interagire con le visualizzazioni nell’interfaccia utente, fai riferimento al [guida all’interfaccia utente per schema unione](../ui/union-schema.md)

![](../images/merge-policies/dataset-precedence-experienceevent.png)

## [!UICONTROL Revisione] {#review}

Il passaggio finale nel flusso di lavoro consiste nel rivedere i criteri di unione. La **[!UICONTROL Revisione]** vengono visualizzate informazioni sui criteri di unione, compresi il metodo di unione degli ID selezionato, il metodo di unione selezionato e i set di dati inclusi. Per visualizzare tutti i set di dati Profilo o ExperienceEvent inclusi, seleziona il numero di set di dati da espandere all’elenco a discesa.

Nella schermata di revisione è incluso anche il **[!UICONTROL Anteprima dati]** tabella che mostra record di profilo di esempio utilizzando i criteri di unione. Questo consente di visualizzare un&#39;anteprima dell&#39;aspetto di un profilo cliente prima di salvare il criterio di unione.

Prima di selezionare, verificare attentamente la configurazione dei criteri di unione e visualizzare in anteprima i dati **[!UICONTROL Fine]** per completare il flusso di lavoro di creazione.

### Timestamp ordinato {#timestamp-ordered-review}

Se hai selezionato **[!UICONTROL Timestamp ordinato]** come metodo di unione per i criteri di unione, l’elenco dei set di dati Profilo include tutti i set di dati creati dalla tua organizzazione relativi alla classe schema, in ordine di marca temporale. L’elenco dei set di dati ExperienceEvent include tutti i set di dati creati dalla tua organizzazione per la classe di schema selezionata e verrà aggiunto ai set di dati Profilo.

La **[!UICONTROL Anteprima dati]** La tabella mostra record di profilo di esempio basati su un ordine di marca temporale dei set di dati. Questo consente di visualizzare un&#39;anteprima dell&#39;aspetto di un profilo cliente prima di salvare il criterio di unione.

![](../images/merge-policies/timestamp-review.png)

### Precedenza del set di dati {#dataset-precedence-review}

Se hai selezionato **[!UICONTROL Precedenza del set di dati]** come metodo di unione per i criteri di unione, gli elenchi dei set di dati Profile ed ExperienceEvent includono rispettivamente solo i set di dati Profile ed ExperienceEvent selezionati durante il flusso di lavoro di creazione. L’ordine dei set di dati Profilo deve corrispondere alla precedenza specificata durante la creazione. In caso contrario, utilizza il [!UICONTROL Indietro] per tornare ai passaggi del flusso di lavoro precedenti e regolare la priorità.

La **[!UICONTROL Anteprima dati]** La tabella mostra record di profilo di esempio utilizzando i set di dati selezionati. Questo consente di visualizzare un&#39;anteprima dell&#39;aspetto di un profilo cliente prima di salvare il criterio di unione.

![](../images/merge-policies/dataset-precedence-review.png)

### Elenco aggiornato dei criteri di unione {#updated-list}

Dopo aver completato il flusso di lavoro per la creazione di un nuovo criterio di unione, viene visualizzata nuovamente la **[!UICONTROL Unisci criteri]** scheda . L&#39;elenco dei criteri di unione per l&#39;organizzazione deve ora includere i criteri di unione appena creati.

![](../images/merge-policies/new-merge-policy-created.png)

## Modificare un criterio di unione

Da [!UICONTROL Unisci criteri] è possibile modificare un criterio di unione esistente creato per [!DNL XDM Individual Profile] selezionando la **[!UICONTROL Nome del criterio]** per il criterio di unione che si desidera modificare.

![Pagina di destinazione dei criteri di unione](../images/merge-policies/select-edit.png)

Quando il **[!UICONTROL Modifica criterio di unione]** viene visualizzata la schermata , è possibile apportare modifiche al nome e [!UICONTROL unione degli ID] , nonché modificare il criterio di unione predefinito per l&#39;organizzazione.

Seleziona **[!UICONTROL Successivo]** per continuare il flusso di lavoro dei criteri di unione per aggiornare il metodo di unione e i set di dati inclusi nel criterio di unione.

![](../images/merge-policies/edit-screen.png)

Dopo aver apportato le modifiche necessarie, esaminare i criteri di unione e selezionare **[!UICONTROL Fine]** per salvare le modifiche e tornare al [!UICONTROL Unisci criteri] scheda .

>[!WARNING]
>
>La modifica di un criterio di unione può influenzare la segmentazione e i risultati del profilo, in quanto altererà il modo in cui vengono risolti i conflitti di dati. Verificare attentamente le modifiche ai criteri di unione prima di salvarli.

![](../images/merge-policies/edit-review.png)

## Violazioni dei criteri di governance dei dati

Durante la creazione o l&#39;aggiornamento di un criterio di unione, viene eseguito un controllo per determinare se il criterio di unione viola uno qualsiasi dei criteri di utilizzo dei dati definiti dall&#39;organizzazione. I criteri di utilizzo dei dati fanno parte della governance dei dati di Adobe Experience Platform e sono regole che descrivono i tipi di azioni di marketing che sono consentite o a cui è consentito eseguire su specifici [!DNL Platform] dati. Ad esempio, se un criterio di unione è stato utilizzato per creare un segmento attivato per una destinazione di terze parti e l&#39;organizzazione dispone di un criterio di utilizzo dei dati che impedisce l&#39;esportazione di dati specifici a terze parti, riceverai un **[!UICONTROL Violazione dei criteri di governance dei dati rilevata]** notifica quando si tenta di salvare il criterio di unione.

Questa notifica include un elenco dei criteri di utilizzo dei dati che sono stati violati e ti consente di visualizzare i dettagli della violazione selezionando un criterio dall’elenco. Selezionando una politica violata, il **[!UICONTROL Linea di dati]** La scheda fornisce il motivo della violazione e delle attivazioni interessate, ognuna delle quali fornisce ulteriori dettagli su come è stato violato il criterio di utilizzo dei dati.

Per ulteriori informazioni sulle prestazioni della governance dei dati in Adobe Experience Platform, consulta la sezione [Panoramica sulla governance dei dati](../../data-governance/home.md).

![](../images/merge-policies/policy-violation.png)

## Passaggi successivi

Dopo aver creato e configurato i criteri di unione per la tua organizzazione, puoi utilizzarli per regolare la visualizzazione dei profili dei clienti all’interno di Platform e per creare segmenti di pubblico dai dati del profilo. Consulta la sezione [panoramica sulla segmentazione](../../segmentation/home.md) per ulteriori informazioni su come creare e lavorare con i segmenti utilizzando il [!DNL Experience Platform] Interfaccia utente e API.
