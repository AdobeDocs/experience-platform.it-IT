---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;criteri di unione;interfaccia utente;interfaccia utente;timestamp ordinato;precedenza set di dati
title: Guida all’interfaccia utente per i criteri di unione
type: Documentation
description: Quando si riuniscono dati provenienti da più origini in Experience Platform, i criteri di unione sono le regole utilizzate da Platform per determinare in che modo i dati verranno definiti come prioritari e quali dati verranno combinati per creare la visualizzazione unificata. Questa guida fornisce istruzioni passo per l’utilizzo dei criteri di unione tramite l’interfaccia utente di Adobe Experience Platform.
exl-id: 0489217a-6a53-428c-a531-fd0a0e5bb71f
source-git-commit: a6a49b4cf9c89b5c6b4679f36daede93590ffb3c
workflow-type: tm+mt
source-wordcount: '2193'
ht-degree: 0%

---


# Guida all’interfaccia utente per i criteri di unione

Adobe Experience Platform consente di unire frammenti di dati provenienti da più sorgenti e di combinarli per ottenere una visualizzazione completa di ciascuno dei singoli clienti. Quando si riuniscono questi dati, i criteri di unione sono le regole utilizzate da [!DNL Platform] per determinare in che modo i dati verranno definiti come prioritari e quali dati verranno combinati per creare la visualizzazione unificata.

Utilizzando le API RESTful o l&#39;interfaccia utente, è possibile creare nuovi criteri di unione, gestire i criteri esistenti e impostare un criterio di unione predefinito per la propria organizzazione. Questa guida fornisce istruzioni passo per l’utilizzo dei criteri di unione tramite l’interfaccia utente di Adobe Experience Platform.

Per ulteriori informazioni sui criteri di unione e sul ruolo svolto in Experience Platform, leggere la [panoramica dei criteri di unione](overview.md).

## Introduzione

Questa guida richiede una comprensione approfondita di diverse importanti funzioni [!DNL Experience Platform] . Prima di seguire questa guida, consulta la documentazione relativa ai seguenti servizi:

* [Profilo](../home.md) cliente in tempo reale: Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Servizio](../../identity-service/home.md) Adobe Experience Platform Identity: Abilita il Profilo del cliente in tempo reale collegando le identità da diverse sorgenti di dati in  [!DNL Platform].
* [Experience Data Model (XDM)](../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Platform] vengono organizzati i dati sulla customer experience.

## Visualizza criteri di unione {#view-merge-policies}

Nell&#39;interfaccia utente di [!DNL Experience Platform] è possibile iniziare a lavorare con i criteri di unione selezionando **[!UICONTROL Profili]** nel menu di navigazione a sinistra e quindi selezionando la scheda **[!UICONTROL Criteri di unione]** . Questa scheda include un elenco di tutti i criteri di unione esistenti per l&#39;organizzazione, nonché i dettagli relativi a ciascun criterio di unione, compreso il nome del criterio, se il criterio di unione è o meno il criterio di unione predefinito e la classe dello schema a cui il criterio di unione fa riferimento.

![Pagina di destinazione dei criteri di unione](../images/merge-policies/landing.png)

Per selezionare i dettagli visibili o per aggiungere ulteriori colonne alla visualizzazione, selezionare **[!UICONTROL Configura colonne]** e fare clic sul nome di una colonna per aggiungerla o rimuoverla dalla visualizzazione.

![](../images/merge-policies/adjust-view.png)

## Creare un criterio di unione {#create-a-merge-policy}

Per creare un nuovo criterio di unione, selezionare **[!UICONTROL Crea criterio di unione]** nella scheda Criteri di unione per accedere al nuovo flusso di lavoro dei criteri di unione.

![Pagina di destinazione dei criteri di unione con il pulsante di creazione evidenziato.](../images/merge-policies/create-new.png)

Il flusso di lavoro **[!UICONTROL Nuovo criterio di unione]** richiede di fornire informazioni importanti per il nuovo criterio di unione tramite una serie di passaggi guidati. Questi passaggi sono descritti nelle sezioni che seguono.

![Il nuovo flusso di lavoro dei criteri di unione.](../images/merge-policies/create.png)

## [!UICONTROL Configurare gli] {#configure}

Il primo passaggio del flusso di lavoro consente di configurare i criteri di unione fornendo informazioni di base. Queste informazioni includono:

* **[!UICONTROL Nome]**: Il nome del criterio di unione deve essere descrittivo ma conciso.
* **[!UICONTROL Classe]** schema: Classe dello schema XDM associata al criterio di unione. Specifica la classe dello schema per la quale viene creato il criterio di unione. Le organizzazioni possono creare più criteri di unione per classe di schema. Attualmente nell’interfaccia utente è disponibile solo la classe [!UICONTROL Profilo individuale XDM] . È possibile visualizzare in anteprima lo schema unione per la classe dello schema selezionando **[!UICONTROL Visualizza schema unione]**. Per ulteriori informazioni, consulta la sezione sulla [visualizzazione dello schema di unione](#view-union-schema) che segue.
* **[!UICONTROL Stitching]** ID: Questo campo definisce come determinare le identità correlate di un cliente. Esistono due possibili valori per le unione identità ed è importante comprendere in che modo il tipo di unione identità selezionato influirà sui dati. Per ulteriori informazioni, consulta la [panoramica dei criteri di unione](overview.md).
   * **[!UICONTROL Nessuno]**: Non eseguire alcuna unione di identità.
   * **[!UICONTROL Grafico]** privato: Eseguire unione di identità in base al grafico di identità privata.
* **[!UICONTROL Criterio]** di unione predefinito: Pulsante di attivazione/disattivazione che consente di selezionare se il criterio di unione sarà o meno il valore predefinito per l&#39;organizzazione. Se il selettore è attivato, viene visualizzato un avviso che richiede di confermare la modifica dei criteri di unione predefiniti dell&#39;organizzazione. Per ulteriori informazioni sui criteri di unione predefiniti, consulta la [panoramica dei criteri di unione](overview.md) .
   ![](../images/merge-policies/create-make-default.png)

Una volta completati i campi obbligatori, puoi selezionare **[!UICONTROL Avanti]** per continuare con il flusso di lavoro.

![Schermata Configura completa con il pulsante Successivo evidenziato.](../images/merge-policies/create-complete.png)

## [!UICONTROL Visualizza schema unione] {#view-union-schema}

Durante la creazione o la modifica di un criterio di unione, è possibile visualizzare lo schema di unione per la classe di schema selezionata selezionando **[!UICONTROL Visualizza schema unione]**.

![](../images/merge-policies/view-union-schema.png)

Viene visualizzata la finestra di dialogo [!UICONTROL Visualizza schema unione], che mostra tutti gli schemi, le identità e le relazioni che contribuiscono allo schema di unione. Puoi utilizzare la finestra di dialogo per esplorare lo schema dell’unione nello stesso modo in cui accedi alla scheda [!UICONTROL Schema dell’Unione] nella sezione [!UICONTROL Profili] dell’interfaccia utente della piattaforma.

Per informazioni dettagliate sugli schemi di unione, tra cui come interagire con essi nella scheda [!UICONTROL Schema dell&#39;unione] o nella finestra di dialogo [!UICONTROL Visualizza schema dell&#39;unione] mostrata nel flusso di lavoro dei criteri di unione, visita la [guida dell&#39;interfaccia utente dello schema dell&#39;unione](../ui/union-schema.md).

![](../images/merge-policies/view-union-schema-dialog.png)

## [!UICONTROL Seleziona set di dati profilo] {#select-profile-datasets}

Nella schermata **[!UICONTROL Seleziona set di dati profilo]**, è necessario selezionare il metodo **[!UICONTROL Merge]** che si desidera utilizzare per i criteri di unione. Sullo schermo viene inoltre visualizzato il numero totale di [!UICONTROL Set di dati di profilo] nella tua organizzazione che si riferiscono alla classe di schema selezionata nella schermata precedente.

A seconda del metodo di unione scelto, tutti i set di dati Profilo verranno uniti in base all’ordine in cui sono stati aggiornati per l’ultima volta (timestamp ordered) oppure dovrai selezionare i set di dati Profilo da includere nel criterio di unione e l’ordine in cui unirli (precedenza set di dati).

Per ulteriori informazioni sui metodi di unione, fare riferimento alla [panoramica dei criteri di unione](overview.md).

### Timestamp ordinato {#timestamp-ordered-profile}

Selezionando **[!UICONTROL Timestamp ordered]** come metodo di unione, gli attributi dei set di dati aggiornati più di recente avranno la precedenza. Questo vale per tutti i set di dati di profilo.

>[!NOTE]
>
>Il numero tra parentesi accanto a **[!UICONTROL Set di dati di profilo]** (ad esempio, `(37)` nell’immagine mostrata) mostra il numero totale di set di dati di profilo che verranno inclusi.

![](../images/merge-policies/timestamp-ordered.png)

### Precedenza del set di dati {#dataset-precedence-profile}

Quando si seleziona **[!UICONTROL Precedenza set di dati]** come metodo di unione, è necessario selezionare i set di dati Profilo e assegnarli manualmente una priorità. Ogni set di dati elencato include anche lo stato dell’ultimo batch acquisito o visualizza un avviso che nessun batch è stato acquisito in tale set di dati.

È possibile selezionare fino a 50 set di dati dall’elenco dei set di dati da includere nel criterio di unione.

>[!NOTE]
>
>Il numero tra parentesi accanto a **[!UICONTROL Set di dati di profilo]** (ad esempio, `(37)` nell’immagine mostrata) mostra il numero totale di set di dati di profilo disponibili per la selezione.

I set di dati selezionati vengono aggiunti alla sezione **[!UICONTROL Seleziona set di dati]** per consentire di trascinare e rilasciare i set di dati e ordinarli in base alla precedenza desiderata. Poiché i set di dati vengono regolati nell’elenco, il numero ordinale (1, 2, 3, ecc.) accanto al set di dati viene aggiornato, mostrando la priorità (1 con la priorità più elevata, quindi 2 e successivi).

Quando si seleziona un set di dati, viene aggiornata anche la sezione **[!UICONTROL Schema dell’Unione]** , che mostra i campi dello schema dell’unione a cui ogni set di dati contribuisce i dati. Per ulteriori informazioni sugli schemi di unione, tra cui come interagire con le visualizzazioni nell&#39;interfaccia utente, fai riferimento alla [guida all&#39;interfaccia utente dello schema di unione](../ui/union-schema.md)

![](../images/merge-policies/dataset-precedence.png)

## [!UICONTROL Seleziona set di dati ExperienceEvent] {#select-experienceevent-datasets}

Il passaggio successivo nel flusso di lavoro richiede la selezione dei set di dati ExperienceEvent . Questa schermata è influenzata dal metodo di unione selezionato nella schermata [[!UICONTROL Seleziona set di dati profilo]](#select-profile-datasets) .

### Timestamp ordinato {#timestamp-ordered-experienceevent}

Se hai selezionato **[!UICONTROL Timestamp ordered]** come metodo di unione per i set di dati di Profilo, prevarranno anche gli attributi dei set di dati ExperienceEvent aggiornati più di recente.

>[!NOTE]
>
>Il numero tra parentesi accanto a **[!UICONTROL Set di dati ExperienceEvent]** (ad esempio, `(20)` nell&#39;immagine mostrata) mostra il numero totale di set di dati ExperienceEvent creati dall&#39;organizzazione e relativi alla classe di schema selezionata nella schermata di configurazione dei criteri di unione.

![](../images/merge-policies/timestamp-experienceevent.png)

### Precedenza del set di dati {#dataset-precedence-experienceevent}

Se hai selezionato **[!UICONTROL Precedenza set di dati]** come metodo di unione per i set di dati Profilo, dovrai selezionare i set di dati ExperienceEvent per includere. Puoi selezionare fino a 50 set di dati ExperienceEvent dall’elenco dei set di dati.

>[!NOTE]
>
>Il numero tra parentesi accanto a **[!UICONTROL Set di dati ExperienceEvent]** (ad esempio, `(20)` nell&#39;immagine mostrata) mostra il numero totale di set di dati ExperienceEvent creati dall&#39;organizzazione e relativi alla classe di schema selezionata nella schermata di configurazione dei criteri di unione.

I set di dati selezionati vengono visualizzati nella sezione [!UICONTROL Seleziona set di dati] .

I set di dati ExperienceEvent non possono essere ordinati manualmente, ma gli attributi nei set di dati ExperienceEvent vengono aggiunti ai set di dati Profile se fanno parte dello stesso frammento di profilo.

Analogamente alla selezione dei set di dati Profilo, la selezione di un set di dati ExperienceEvent aggiorna anche la sezione **[!UICONTROL Schema dell’Unione]** , mostrando i campi nello schema dell’unione a cui ogni set di dati contribuisce i dati. Per ulteriori informazioni sugli schemi di unione, tra cui come interagire con le visualizzazioni nell&#39;interfaccia utente, fai riferimento alla [guida all&#39;interfaccia utente dello schema di unione](../ui/union-schema.md)

![](../images/merge-policies/dataset-precedence-experienceevent.png)

## [!UICONTROL Revisione] {#review}

Il passaggio finale nel flusso di lavoro consiste nel rivedere i criteri di unione. La schermata **[!UICONTROL Rivedi]** visualizza informazioni sui criteri di unione, tra cui il metodo di unione degli ID selezionato, il metodo di unione selezionato e i set di dati inclusi. Per visualizzare tutti i set di dati Profilo o ExperienceEvent inclusi, seleziona il numero di set di dati da espandere all’elenco a discesa.

Nella schermata di revisione è inclusa anche la tabella **[!UICONTROL Anteprima dati]** che mostra i record di profilo di esempio utilizzando i criteri di unione. Questo consente di visualizzare un&#39;anteprima dell&#39;aspetto di un profilo cliente prima di salvare il criterio di unione.

Prima di selezionare **[!UICONTROL Fine]** per completare il flusso di lavoro di creazione, controlla attentamente la configurazione dei criteri di unione e visualizza in anteprima i dati.

### Timestamp ordinato {#timestamp-ordered-review}

Se hai selezionato **[!UICONTROL Timestamp ordered]** come metodo di unione per i criteri di unione, l&#39;elenco dei set di dati di profilo include tutti i set di dati creati dalla tua organizzazione relativi alla classe dello schema, in ordine di timestamp. L’elenco dei set di dati ExperienceEvent include tutti i set di dati creati dalla tua organizzazione per la classe di schema selezionata e verrà aggiunto ai set di dati Profilo.

La tabella **[!UICONTROL Preview data]** mostra record di profilo di esempio in base a un ordine di marca temporale dei set di dati. Questo consente di visualizzare un&#39;anteprima dell&#39;aspetto di un profilo cliente prima di salvare il criterio di unione.

![](../images/merge-policies/timestamp-review.png)

### Precedenza del set di dati {#dataset-precedence-review}

Se hai selezionato **[!UICONTROL Precedenza set di dati]** come metodo di unione per il criterio di unione, gli elenchi dei set di dati Profilo ed ExperienceEvent includono rispettivamente solo i set di dati Profilo ed ExperienceEvent selezionati durante il flusso di lavoro di creazione. L’ordine dei set di dati Profilo deve corrispondere alla precedenza specificata durante la creazione. In caso contrario, utilizza il pulsante [!UICONTROL Indietro] per tornare ai passaggi del flusso di lavoro precedenti e regolare la priorità.

La tabella **[!UICONTROL Preview data]** mostra record di profilo di esempio utilizzando i set di dati selezionati. Questo consente di visualizzare un&#39;anteprima dell&#39;aspetto di un profilo cliente prima di salvare il criterio di unione.

![](../images/merge-policies/dataset-precedence-review.png)

### Elenco aggiornato dei criteri di unione {#updated-list}

Dopo aver completato il flusso di lavoro per creare un nuovo criterio di unione, vieni riportato alla scheda **[!UICONTROL Criteri di unione]** . L&#39;elenco dei criteri di unione per l&#39;organizzazione deve ora includere i criteri di unione appena creati.

![](../images/merge-policies/new-merge-policy-created.png)

## Modificare un criterio di unione

Dalla scheda [!UICONTROL Criteri di unione] è possibile modificare un criterio di unione esistente creato per la classe [!DNL XDM Individual Profile] selezionando il **[!UICONTROL Nome criterio]** per il criterio di unione che si desidera modificare.

![Pagina di destinazione dei criteri di unione](../images/merge-policies/select-edit.png)

Quando viene visualizzata la schermata **[!UICONTROL Modifica criterio di unione]**, è possibile apportare modifiche al nome e al metodo [!UICONTROL unione ID], nonché modificare se questo criterio è o meno il criterio di unione predefinito per la propria organizzazione.

Selezionare **[!UICONTROL Avanti]** per continuare il flusso di lavoro dei criteri di unione per aggiornare il metodo di unione e i set di dati inclusi nel criterio di unione.

![](../images/merge-policies/edit-screen.png)

Dopo aver apportato le modifiche necessarie, controlla i criteri di unione e seleziona **[!UICONTROL Fine]** per salvare le modifiche e tornare alla scheda [!UICONTROL Criteri di unione] .

>[!WARNING]
>
>La modifica di un criterio di unione può influenzare la segmentazione e i risultati del profilo, in quanto altererà il modo in cui vengono risolti i conflitti di dati. Verificare attentamente le modifiche ai criteri di unione prima di salvarli.

![](../images/merge-policies/edit-review.png)

## Violazioni dei criteri di governance dei dati

Durante la creazione o l&#39;aggiornamento di un criterio di unione, viene eseguito un controllo per determinare se il criterio di unione viola uno qualsiasi dei criteri di utilizzo dei dati definiti dall&#39;organizzazione. I criteri di utilizzo dei dati fanno parte di Adobe Experience Platform [!DNL Data Governance] e sono regole che descrivono i tipi di azioni di marketing che possono essere eseguite su dati [!DNL Platform] specifici o da cui sono state limitate. Ad esempio, se un criterio di unione è stato utilizzato per creare un segmento attivato in una destinazione di terze parti e l&#39;organizzazione dispone di un criterio di utilizzo dei dati che impedisce l&#39;esportazione di dati specifici a terze parti, durante il tentativo di salvare il criterio di unione riceverai una notifica **[!UICONTROL violazione dei criteri di governance dei dati rilevata]**.

Questa notifica include un elenco dei criteri di utilizzo dei dati che sono stati violati e ti consente di visualizzare i dettagli della violazione selezionando un criterio dall’elenco. Selezionando un criterio violato, la scheda **[!UICONTROL Linea dati]** fornisce il motivo della violazione e delle attivazioni interessate, ognuna delle quali fornisce maggiori dettagli sulle modalità di violazione dei criteri di utilizzo dei dati.

Per ulteriori informazioni sulle modalità di esecuzione della governance dei dati in Adobe Experience Platform, consulta la [Panoramica sulla governance dei dati](../../data-governance/home.md).

![](../images/merge-policies/policy-violation.png)

## Passaggi successivi

Dopo aver creato e configurato i criteri di unione per la tua organizzazione, puoi utilizzarli per regolare la visualizzazione dei profili dei clienti all’interno di Platform e per creare segmenti di pubblico dai dati del profilo. Per ulteriori informazioni su come creare e lavorare con i segmenti utilizzando l’ [!DNL Experience Platform] interfaccia utente e API, consulta la [panoramica sulla segmentazione](../../segmentation/home.md) .
