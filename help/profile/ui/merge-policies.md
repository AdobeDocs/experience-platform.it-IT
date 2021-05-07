---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;criteri di unione;interfaccia utente;interfaccia utente;timestamp ordinato;precedenza set di dati
title: Guida all’interfaccia utente per i criteri di unione
topic-legacy: guide
type: Documentation
description: Adobe Experience Platform consente di unire frammenti di dati provenienti da più sorgenti e di combinarli per ottenere una visualizzazione completa di ciascuno dei singoli clienti. Quando si riuniscono questi dati, i criteri di unione sono le regole utilizzate da Platform per determinare in che modo i dati verranno definiti come prioritari e quali dati verranno combinati per creare una visualizzazione unificata.
exl-id: 0489217a-6a53-428c-a531-fd0a0e5bb71f
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '2879'
ht-degree: 0%

---

# Guida all’interfaccia utente per i criteri di unione

Adobe Experience Platform consente di unire frammenti di dati provenienti da più sorgenti e di combinarli per ottenere una visualizzazione completa di ciascuno dei singoli clienti. Quando si riuniscono questi dati, i criteri di unione sono le regole utilizzate da [!DNL Platform] per determinare in che modo i dati verranno definiti come prioritari e quali dati verranno combinati per creare una visualizzazione unificata.

Ad esempio, se un cliente interagisce con il tuo marchio su più canali, la tua organizzazione avrà più frammenti di profilo relativi al singolo cliente che compaiono in più set di dati. Quando questi frammenti vengono acquisiti in Platform, vengono uniti per creare un singolo profilo per quel cliente. Quando i dati provenienti da più origini sono in conflitto (ad esempio, un frammento elenca il cliente come &quot;singolo&quot;, mentre l’altro elenca il cliente come &quot;sposato&quot;), il criterio di unione determina quali informazioni includere nel profilo dell’utente.

Utilizzando le API RESTful o l&#39;interfaccia utente, è possibile creare nuovi criteri di unione, gestire i criteri esistenti e impostare un criterio di unione predefinito per la propria organizzazione. Questa guida fornisce istruzioni passo per l’utilizzo dei criteri di unione tramite l’interfaccia utente di Adobe Experience Platform.

Se preferisci lavorare con i criteri di unione utilizzando l&#39;API [!DNL Real-time Customer Profile], segui le istruzioni descritte nella [guida API dei criteri di unione](../api/merge-policies.md).

## Introduzione

Questa guida richiede una comprensione approfondita di diverse importanti funzioni [!DNL Experience Platform] . Prima di seguire questa guida o di utilizzare le API di profilo, consulta la documentazione relativa ai seguenti servizi:

* [Profilo](../home.md) cliente in tempo reale: Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Servizio](../../identity-service/home.md) Adobe Experience Platform Identity: Abilita il Profilo del cliente in tempo reale collegando le identità da diverse sorgenti di dati in  [!DNL Platform].
* [Experience Data Model (XDM)](../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Platform] vengono organizzati i dati sulla customer experience.

## Metodi di unione {#merge-methods}

Ogni frammento di profilo contiene informazioni per una sola identità sul numero totale di identità che possono esistere per un singolo utente. Quando unisci i dati per formare un profilo cliente, è possibile che tali informazioni siano in conflitto e occorre specificare la priorità. La selezione di un metodo di unione consente di specificare quali attributi del set di dati dare la priorità se si verifica un conflitto di unione tra i set di dati.

Sono disponibili due possibili metodi di unione per i criteri di unione. Ciascuno di questi metodi è riassunto di seguito con ulteriori dettagli forniti nelle sezioni seguenti:

* **[!UICONTROL Timestamp ordered]:** In caso di conflitto, viene data priorità al frammento di profilo aggiornato più di recente.
   * **Marca temporale personalizzata:** [!UICONTROL Timestamp ordered] supporta anche marche temporali personalizzate che hanno priorità rispetto alle marche temporali del sistema quando si uniscono dati all’interno dello stesso set di dati (più identità) o tra set di dati. Per ulteriori informazioni, consulta la sezione sull’ [utilizzo di marche temporali personalizzate](#custom-timestamps).
* **[!UICONTROL Dataset precedence]:** In caso di conflitto, assegna priorità ai frammenti di profilo in base al set di dati da cui provengono. Quando selezioni questa opzione, devi scegliere i set di dati correlati e il loro ordine di priorità.

### Timestamp ordered {#timestamp-ordered}

Poiché i record di profilo vengono acquisiti in Experience Platform, al momento dell’acquisizione viene ottenuta una marca temporale di sistema che viene aggiunta al record. Quando **[!UICONTROL Timestamp ordered]** è selezionato come metodo di unione per un criterio di unione, i profili vengono uniti in base alla marca temporale del sistema. In altre parole, l’unione viene eseguita in base alla marca temporale per quando il record è stato acquisito in Platform.

#### Utilizzo di marche temporali personalizzate {#custom-timestamps}

Talvolta possono verificarsi casi d’uso in cui è necessario fornire una marca temporale personalizzata e il criterio di unione rispetta la marca temporale personalizzata anziché quella di sistema. Esempi di ciò includono il recupero dei dati o la garanzia dell’ordine corretto degli eventi se i record vengono acquisiti in modo errato.

Per utilizzare una marca temporale personalizzata, è necessario aggiungere allo schema del profilo il gruppo di campi **[!UICONTROL External Source System Audit Details]dello schema**. Una volta aggiunta, la marca temporale personalizzata può essere compilata utilizzando il campo `lastUpdatedDate` . Quando un record viene acquisito con il campo `lastUpdatedDate` popolato, Experience Platform lo utilizzerà per unire i record tra i set di dati. Se `lastUpdatedDate` non è presente o non è popolato, Platform continuerà a utilizzare la marca temporale del sistema.

>[!NOTE]
>
>È necessario assicurarsi che la marca temporale `lastUpdatedDate` sia compilata quando si acquisisce un aggiornamento sullo stesso record.

La schermata seguente mostra i campi nel gruppo di campi [!UICONTROL External Source System Audit Details] . Per istruzioni dettagliate sull’utilizzo degli schemi tramite l’interfaccia utente di Platform e su come aggiungere gruppi di campi agli schemi, visita l’ [esercitazione per creare uno schema utilizzando l’interfaccia utente](../../xdm/tutorials/create-schema-ui.md) .

![](../images/merge-policies/custom-timestamp-field-group.png)

Per utilizzare le marche temporali personalizzate utilizzando l&#39;API, consulta la sezione [guida all&#39;endpoint dei criteri di unione sull&#39;utilizzo di marche temporali personalizzate](../api/merge-policies.md#custom-timestamps).

### Precedenza del set di dati {#dataset-precedence}

Quando **[!UICONTROL Dataset precedence]** è selezionato come metodo di unione per un criterio di unione, è possibile assegnare la priorità ai frammenti di profilo in base al set di dati da cui provengono. Un esempio di caso d’uso è quello di informazioni presenti in un set di dati preferito o attendibile rispetto ai dati di un altro set di dati.

Per creare un criterio di unione utilizzando **[!UICONTROL Dataset precedence]**, è necessario selezionare i set di dati Profilo ed ExperienceEvent inclusi, quindi è possibile ordinare manualmente i set di dati Profilo per la precedenza. Una volta selezionati e ordinati i set di dati, al set di dati principale verrà data la priorità più alta, al secondo e così via.

## [!UICONTROL ID stitching] {#id-stitching}

L’unione delle identità ([!UICONTROL ID stitching]) è il processo di identificazione dei frammenti di dati e di loro combinazione per formare un record completo del profilo. Per illustrare i diversi comportamenti di unione, considera un singolo cliente che interagisce con un marchio utilizzando due indirizzi e-mail diversi.

* **[!UICONTROL None]:** Quando questa opzione è selezionata, gli ID non vengono uniti. Quando si verifica la segmentazione, le identità che possono appartenere alla stessa persona non vengono unite e la segmentazione considera solo gli attributi associati a ciascun singolo ID quando si determina se un cliente è idoneo per l’appartenenza al segmento. Questo potrebbe comportare l’invio di più messaggi di marketing allo stesso cliente a un singolo cliente con più profili e ciascun profilo potrebbe qualificarsi per segmenti diversi.
* **[!UICONTROL Private graph]:** Quando il grafico privato è selezionato, più identità correlate allo stesso individuo vengono unite insieme. Questo fa sì che il cliente abbia un singolo profilo e consenta alla segmentazione di considerare più attributi da più identità correlate durante la determinazione della qualifica del segmento. In questo scenario, è probabile che il cliente abbia un singolo profilo, si qualifichi per un segmento in base alla combinazione di attributi tra identità e riceva un solo messaggio di marketing.

Per ulteriori informazioni sulle identità e sul loro ruolo nella generazione di profili e segmenti, leggi la [panoramica del servizio Identity](../../identity-service/home.md).

## Criterio di unione predefinito {#default-merge-policy}

Un&#39;organizzazione può creare un criterio di unione predefinito da utilizzare per l&#39;unione dei frammenti di profilo. Questo consente agli utenti di selezionare facilmente il criterio predefinito durante l’esecuzione di azioni, ad Experience Platform la visualizzazione dei profili dei clienti o la creazione di segmenti. Nella maggior parte dei casi, a meno che non venga specificato un altro criterio di unione, verrà utilizzato il criterio di unione predefinito.

Ciascuna organizzazione può creare più criteri di unione relativi a una singola classe di schema XDM, tuttavia può avere un solo criterio di unione predefinito dichiarato per ogni classe. Ad esempio, l&#39;organizzazione potrebbe disporre di un criterio di unione predefinito correlato alla classe [!DNL XDM Individual Profile] e di un diverso criterio di unione predefinito per una classe di inventario prodotto personalizzata.

Se si crea un nuovo criterio di unione e lo si imposta come predefinito, il precedente criterio di unione predefinito verrà aggiornato automaticamente dal sistema in modo che non sia più il predefinito.

>[!WARNING]
>
>Potrebbero essere interessati i conteggi e i segmenti di profilo con un criterio di unione predefinito esistente. Tutti i segmenti a cui è stato applicato un criterio di unione predefinito verranno aggiornati al nuovo criterio di unione predefinito.

## Visualizza criteri di unione {#view-merge-policies}

Nell’interfaccia utente di [!DNL Experience Platform] è possibile iniziare a utilizzare i criteri di unione selezionando **[!UICONTROL Profiles]** nel menu di navigazione a sinistra e quindi selezionando la scheda **[!UICONTROL Merge Policies]** . Questa scheda include un elenco di tutti i criteri di unione esistenti per l&#39;organizzazione, nonché i dettagli relativi a ciascun criterio di unione, compreso il nome del criterio, se il criterio di unione è o meno il criterio di unione predefinito e la classe dello schema a cui il criterio di unione fa riferimento.

![Pagina di destinazione dei criteri di unione](../images/merge-policies/landing.png)

Per selezionare i dettagli visibili o per aggiungere ulteriori colonne alla visualizzazione, selezionare **[!UICONTROL Configure columns]** e fare clic sul nome di una colonna per aggiungerlo o rimuoverlo dalla visualizzazione.

![](../images/merge-policies/adjust-view.png)

## Creare un criterio di unione {#create-a-merge-policy}

Per creare un nuovo criterio di unione, selezionare **[!UICONTROL Create merge policy]** nella scheda Criteri di unione.

![Pagina di destinazione dei criteri di unione con il pulsante di creazione evidenziato.](../images/merge-policies/create-new.png)

Nella schermata del flusso di lavoro **[!UICONTROL New merge policy]** è possibile fornire informazioni importanti per il nuovo criterio di unione tramite una serie di passaggi guidati.

![Il nuovo flusso di lavoro dei criteri di unione.](../images/merge-policies/create.png)

### [!UICONTROL Configure] {#configure}

Il primo passaggio del flusso di lavoro consente di configurare i criteri di unione fornendo informazioni di base. Queste informazioni includono:

* **[!UICONTROL Name]**: Il nome del criterio di unione deve essere descrittivo ma conciso.
* **[!UICONTROL Schema class]**: Classe dello schema XDM associata al criterio di unione. Specifica la classe dello schema per la quale viene creato il criterio di unione. Le organizzazioni possono creare più criteri di unione per classe di schema. Attualmente nell’interfaccia utente è disponibile solo la classe [!UICONTROL XDM Individual Profile] . È possibile visualizzare in anteprima lo schema dell&#39;unione per la classe dello schema selezionando **[!UICONTROL View Union Schema]**. Per ulteriori informazioni, consulta la sezione sulla [visualizzazione dello schema di unione](#view-union-schema) che segue.
* **[!UICONTROL ID stitching]**: Questo campo definisce come determinare le identità correlate di un cliente. Per ulteriori informazioni, consulta la sezione precedente su [unione degli ID](#id-stitching) in questa guida. Esistono due possibili valori:
   * **[!UICONTROL None]**: Non eseguire alcuna unione di identità.
   * **[!UICONTROL Private Graph]**: Eseguire unione di identità in base al grafico di identità privata.
* **[!UICONTROL Default merge policy]**: Pulsante di attivazione/disattivazione che consente di selezionare se il criterio di unione sarà o meno il valore predefinito per l&#39;organizzazione. Se il selettore è attivato, viene visualizzato un avviso che richiede di confermare la modifica dei criteri di unione predefiniti dell&#39;organizzazione. Per ulteriori informazioni, consulta la sezione sui [criteri di unione predefiniti](#default-merge-policy) precedente in questa guida.
   ![](../images/merge-policies/create-make-default.png)

Una volta completati i campi obbligatori, puoi selezionare **[!UICONTROL Next]** per continuare con il flusso di lavoro.

![Schermata Configura completa con il pulsante Successivo evidenziato.](../images/merge-policies/create-complete.png)

#### [!UICONTROL View Union Schema] {#view-union-schema}

Quando crei o modifichi un criterio di unione, puoi visualizzare lo schema di unione per la classe di schema selezionata selezionando **[!UICONTROL View Union Schema]**.

![](../images/merge-policies/view-union-schema.png)

Viene visualizzata la finestra di dialogo [!UICONTROL View Union Schema], che mostra tutti gli schemi, le identità e le relazioni che contribuiscono allo schema dell&#39;unione. Puoi utilizzare la finestra di dialogo per esplorare lo schema dell’unione nello stesso modo in cui accedi alla scheda [!UICONTROL Union Schema] nella sezione [!UICONTROL Profiles] dell’interfaccia utente di Platform.

Per informazioni dettagliate sugli schemi di unione, tra cui come interagire con essi nella scheda [!UICONTROL Union Schema] o nella finestra di dialogo [!UICONTROL View Union Schema] mostrata nel flusso di lavoro dei criteri di unione, visita la [guida all’interfaccia utente dello schema di unione](union-schema.md).

![](../images/merge-policies/view-union-schema-dialog.png)


### [!UICONTROL Select Profile datasets] {#select-profile-datasets}

Nella schermata **[!UICONTROL Select Profile datasets]** è necessario selezionare il **[!UICONTROL Merge method]** che si desidera utilizzare per i criteri di unione. Sullo schermo viene inoltre visualizzato il numero totale di [!UICONTROL Profile datasets] nella tua organizzazione che si riferiscono alla classe dello schema selezionata nella schermata precedente.

A seconda del metodo di unione scelto, tutti i set di dati Profilo verranno uniti in base all’ordine in cui sono stati aggiornati per l’ultima volta (timestamp ordered) oppure dovrai selezionare i set di dati Profilo da includere nel criterio di unione e l’ordine in cui unirli (precedenza set di dati). Per ulteriori informazioni sui metodi di unione, consultare la sezione [metodi di unione](#merge-methods) fornita in precedenza in questo documento.

#### Timestamp ordered {#timestamp-ordered-profile}

Selezionando **[!UICONTROL Timestamp ordered]** come metodo di unione, gli attributi dei set di dati aggiornati più di recente avranno la precedenza. Questo vale per tutti i set di dati di profilo.

![](../images/merge-policies/timestamp-ordered.png)

#### Precedenza del set di dati {#dataset-precedence-profile}

Selezionando **[!UICONTROL Dataset precedence]** come metodo di unione è necessario selezionare i set di dati Profilo e assegnarli manualmente una priorità. Ogni set di dati elencato include anche lo stato dell’ultimo batch acquisito o visualizza un avviso che nessun batch è stato acquisito in tale set di dati.

È possibile selezionare fino a 50 set di dati dall’elenco dei set di dati da includere nel criterio di unione. I set di dati selezionati vengono aggiunti alla sezione **[!UICONTROL Select datasets]** per consentire di trascinare e rilasciare i set di dati e ordinarli in base alla precedenza desiderata. Poiché i set di dati vengono regolati nell’elenco, il numero ordinale (1, 2, 3, ecc.) accanto al set di dati viene aggiornato, mostrando la priorità (1 con la priorità più elevata, quindi 2 e successivi).

La selezione di un set di dati aggiorna anche la sezione **[!UICONTROL Union schema]** , mostrando i campi nello schema di unione a cui ogni set di dati contribuisce i dati. Per ulteriori informazioni sugli schemi di unione, tra cui come interagire con le visualizzazioni nell&#39;interfaccia utente, fai riferimento alla [guida all&#39;interfaccia utente dello schema di unione](union-schema.md)

![](../images/merge-policies/dataset-precedence.png)

### [!UICONTROL Select ExperienceEvent datasets] {#select-experienceevent-datasets}

Il passaggio successivo nel flusso di lavoro richiede la selezione dei set di dati ExperienceEvent . Questa schermata è influenzata dal metodo di unione selezionato nella schermata [[!UICONTROL Select Profile datasets]](#select-profile-datasets).

In questa schermata viene inoltre visualizzato il numero totale di **[!UICONTROL ExperienceEvent datasets]** creati dalla tua organizzazione in relazione alla classe dello schema selezionata nella schermata di configurazione del criterio di unione.

#### Timestamp ordered {#timestamp-ordered-experienceevent}

Se hai selezionato **[!UICONTROL Timestamp ordered]** come metodo di unione per i set di dati di Profilo, prevarranno anche gli attributi dei set di dati ExperienceEvent aggiornati più di recente.

![](../images/merge-policies/timestamp-experienceevent.png)

#### Precedenza del set di dati {#dataset-precedence-experienceevent}

Se hai selezionato **[!UICONTROL Dataset precedence]** come metodo di unione per i set di dati di Profilo, dovrai selezionare i set di dati ExperienceEvent da includere. Puoi selezionare fino a 50 set di dati ExperienceEvent dall’elenco dei set di dati. I set di dati selezionati vengono visualizzati nella sezione [!UICONTROL Select datasets] .

I set di dati ExperienceEvent non possono essere ordinati manualmente, ma gli attributi nei set di dati ExperienceEvent vengono aggiunti ai set di dati Profile se fanno parte dello stesso frammento di profilo.

Analogamente alla selezione dei set di dati Profilo, la selezione di un set di dati ExperienceEvent comporta l’aggiornamento della sezione **[!UICONTROL Union schema]** , che mostra i campi nello schema di unione a cui ogni set di dati contribuisce i dati. Per ulteriori informazioni sugli schemi di unione, tra cui come interagire con le visualizzazioni nell&#39;interfaccia utente, fai riferimento alla [guida all&#39;interfaccia utente dello schema di unione](union-schema.md)

![](../images/merge-policies/dataset-precedence-experienceevent.png)

### [!UICONTROL Review] {#review}

Il passaggio finale nel flusso di lavoro consiste nel rivedere i criteri di unione. Nella schermata **[!UICONTROL Review]** vengono visualizzati il nome del nuovo criterio di unione, la classe dello schema su cui si basa, l&#39;opzione [!UICONTROL ID stitching] selezionata, il metodo di unione e i set di dati inclusi nel criterio di unione. Per visualizzare tutti i set di dati Profilo o ExperienceEvent inclusi, seleziona il numero di set di dati da espandere all’elenco a discesa.

Per completare il flusso di lavoro di creazione, controlla attentamente i criteri di unione prima di selezionare **[!UICONTROL Finish]**.

#### Timestamp ordered {#timestamp-ordered-review}

Se hai selezionato **[!UICONTROL Timestamp ordered]** come metodo di unione per i criteri di unione, l’elenco dei set di dati Profilo include tutti i set di dati creati dalla tua organizzazione relativi alla classe dello schema, in ordine di marca temporale. L’elenco dei set di dati ExperienceEvent include tutti i set di dati creati dalla tua organizzazione per la classe di schema selezionata e verrà aggiunto ai set di dati Profilo.

![](../images/merge-policies/timestamp-review.png)

#### Precedenza del set di dati {#dataset-precedence-review}

Se hai selezionato **[!UICONTROL Dataset precedence]** come metodo di unione per i criteri di unione, gli elenchi dei set di dati Profilo ed ExperienceEvent includono rispettivamente solo i set di dati Profilo ed ExperienceEvent selezionati durante il flusso di lavoro di creazione. L’ordine dei set di dati Profilo deve corrispondere alla precedenza specificata durante la creazione. In caso contrario, utilizza il pulsante [!UICONTROL Back] per tornare ai passaggi del flusso di lavoro precedenti e regolare la priorità.

![](../images/merge-policies/dataset-precedence-review.png)

### Elenco aggiornato dei criteri di unione {#updated-list}

Dopo aver completato il flusso di lavoro per creare un nuovo criterio di unione, vieni riportato alla scheda **[!UICONTROL Merge Policies]** . L&#39;elenco dei criteri di unione per l&#39;organizzazione deve ora includere i criteri di unione appena creati.

![](../images/merge-policies/new-merge-policy-created.png)

## Modificare un criterio di unione

Dalla scheda [!UICONTROL Merge Policies] è possibile modificare un criterio di unione esistente creato per la classe [!DNL XDM Individual Profile] selezionando **[!UICONTROL Policy name]** per il criterio di unione che si desidera modificare.

![Pagina di destinazione dei criteri di unione](../images/merge-policies/select-edit.png)

Quando viene visualizzata la schermata **[!UICONTROL Edit merge policy]**, è possibile apportare modifiche al nome e a [!UICONTROL ID stitching], nonché modificare se questo criterio è o meno il criterio di unione predefinito per l&#39;organizzazione.

Selezionare **[!UICONTROL Next]** per continuare il flusso di lavoro dei criteri di unione per aggiornare il metodo di unione e i set di dati inclusi nel criterio di unione.

![](../images/merge-policies/edit-screen.png)

Dopo aver apportato le modifiche necessarie, controlla i criteri di unione e seleziona **[!UICONTROL Finish]** per tornare alla scheda **[!UICONTROL Merge policies]**.

>[!WARNING]
>
>La modifica di un criterio di unione può influenzare la segmentazione e i risultati del profilo, in quanto altererà il modo in cui vengono risolti i conflitti di dati.

![](../images/merge-policies/edit-review.png)

## Violazioni dei criteri di governance dei dati

Durante la creazione o l&#39;aggiornamento di un criterio di unione, viene eseguito un controllo per determinare se il criterio di unione viola uno qualsiasi dei criteri di utilizzo dei dati definiti dall&#39;organizzazione. I criteri di utilizzo dei dati fanno parte di Adobe Experience Platform [!DNL Data Governance] e sono regole che descrivono i tipi di azioni di marketing che possono essere eseguite su dati [!DNL Platform] specifici o da cui sono state limitate. Ad esempio, se un criterio di unione è stato utilizzato per creare un segmento attivato in una destinazione di terze parti e l&#39;organizzazione dispone di un criterio di utilizzo dei dati che impedisce l&#39;esportazione di dati specifici a terze parti, durante il tentativo di salvare il criterio di unione riceverai una notifica **[!UICONTROL Data governance policy violation detected]**.

Questa notifica include un elenco dei criteri di utilizzo dei dati che sono stati violati e ti consente di visualizzare i dettagli della violazione selezionando un criterio dall’elenco. Selezionando un criterio violato, la scheda **[!UICONTROL Data lineage]** fornisce il motivo della violazione e delle attivazioni interessate, ognuna delle quali fornisce maggiori dettagli sulla violazione dei criteri di utilizzo dei dati.

Per ulteriori informazioni sulle modalità di esecuzione della governance dei dati in Adobe Experience Platform, consulta la [Panoramica sulla governance dei dati](../../data-governance/home.md).

![](../images/merge-policies/policy-violation.png)

## Passaggi successivi

Dopo aver creato e configurato i criteri di unione per la tua organizzazione, puoi utilizzarli per regolare la visualizzazione dei profili dei clienti all’interno di Platform e per creare segmenti di pubblico dai dati del profilo. Per ulteriori informazioni su come creare e lavorare con i segmenti utilizzando l’ [!DNL Experience Platform] interfaccia utente e API, consulta la [Panoramica sulla segmentazione](../../segmentation/home.md) .
