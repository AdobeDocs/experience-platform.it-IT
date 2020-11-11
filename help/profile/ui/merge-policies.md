---
keywords: Experience Platform;profile;real-time customer profile;merge policies;UI;user interface;timestamp ordered;dataset precedence
title: Guida all'interfaccia utente per i criteri di unione
topic: guide
translation-type: tm+mt
source-git-commit: 6bfc256b50542e88e28f8a0c40cec7a109a05aa6
workflow-type: tm+mt
source-wordcount: '2551'
ht-degree: 0%

---


# Guida all&#39;interfaccia utente per i criteri di unione

Adobe Experience Platform consente di unire frammenti di dati provenienti da più origini e di combinarli per visualizzare in modo completo i singoli clienti. Quando si uniscono questi dati, i criteri di unione sono le regole che [!DNL Platform] utilizzano per determinare in che modo i dati verranno classificati come priorità e quali dati verranno combinati per creare tale visualizzazione unificata.

Ad esempio, se un cliente interagisce con il tuo marchio su più canali, l&#39;organizzazione avrà più frammenti di profilo correlati a tale singolo cliente che saranno visualizzati in più set di dati. Quando questi frammenti vengono assimilati in Piattaforma, vengono uniti per creare un unico profilo per il cliente. Quando i dati provenienti da più origini sono in conflitto (ad esempio, un frammento indica il cliente come &quot;singolo&quot;, mentre l&#39;altro elenca il cliente come &quot;sposato&quot;), il criterio di unione determina quali informazioni includere nel profilo dell&#39;individuo.

Utilizzando le API RESTful o l&#39;interfaccia utente, puoi creare nuovi criteri di unione, gestire i criteri esistenti e impostare un criterio di unione predefinito per la tua organizzazione. Questa guida fornisce istruzioni dettagliate per l&#39;utilizzo dei criteri di unione tramite l&#39;interfaccia utente (interfaccia utente) di Adobe Experience Platform.

Se preferisci lavorare con i criteri di unione utilizzando l&#39; [!DNL Real-time Customer Profile] API, segui le istruzioni indicate nella guida [API dei criteri di](../api/merge-policies.md)unione.

## Introduzione

Questa guida richiede una conoscenza approfondita di diverse [!DNL Experience Platform] funzioni importanti. Prima di seguire questa guida o di utilizzare le API dei profili, consulta la documentazione relativa ai seguenti servizi:

* [[!DNL Real-time Customer Profile]](../home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Servizio](../../identity-service/home.md)identità Adobe Experience Platform: Abilita il profilo cliente in tempo reale collegando le identità da origini dati diverse in cui viene effettuato il caricamento [!DNL Platform].
* [[!DNL Experience Data Model] (XDM)](../../xdm/home.md): Il framework standard con cui [!DNL Platform] organizzare i dati relativi all&#39;esperienza del cliente.

## Metodi di unione {#merge-methods}

Ciascun frammento di profilo contiene informazioni relative a una sola identità rispetto al numero totale di identità che possono esistere per un singolo utente. Quando si uniscono tali dati per formare un profilo cliente, è possibile che le informazioni siano in conflitto e che sia specificata la priorità. La selezione di un metodo di unione consente di specificare gli attributi del set di dati da assegnare come priorità in caso di conflitto di unione tra i set di dati.

Per i criteri di unione sono disponibili due possibili metodi di unione. Ciascuno di questi metodi è riassunto di seguito con ulteriori dettagli forniti nelle sezioni seguenti:

* **[!UICONTROL Timestamp ordered]:** In caso di conflitto, viene data priorità al frammento di profilo aggiornato più di recente.
   * **Marca temporale personalizzata:** [!UICONTROL Timestamp ordered] supporta inoltre marche temporali personalizzate che hanno la priorità sulle marche temporali del sistema quando si uniscono dati all&#39;interno dello stesso dataset (identità multiple) o tra set di dati. Per ulteriori informazioni, consulta la sezione sull’ [utilizzo di marche temporali](#custom-timestamps)personalizzate.
* **[!UICONTROL Dataset precedence]:** In caso di conflitto, assegnare priorità ai frammenti di profilo basati sul set di dati da cui provengono. Quando si seleziona questa opzione, è necessario scegliere i set di dati correlati e il relativo ordine di priorità.

### Timestamp ordinato {#timestamp-ordered}

Poiché i record di profilo vengono trasferiti  Experience Platform, al momento dell&#39;assimilazione viene ottenuta una marca temporale di sistema che viene aggiunta al record. Se **[!UICONTROL Timestamp ordered]** è selezionato come metodo di unione per un criterio di unione, i profili vengono uniti in base alla marca temporale del sistema. In altre parole, l&#39;unione viene eseguita in base alla marca temporale per l&#39;inserimento del record nella piattaforma.

#### Utilizzo di marche temporali personalizzate {#custom-timestamps}

Talvolta possono verificarsi casi di utilizzo in cui è necessario fornire una marca temporale personalizzata e fare in modo che il criterio di unione rispetti la marca temporale personalizzata anziché la marca temporale del sistema. Alcuni esempi di questo tipo includono il backfill dei dati o la garanzia dell&#39;ordine corretto degli eventi in caso di acquisizione di record non ordinata.

Per utilizzare una marca temporale personalizzata, è **[!UICONTROL External Source System Audit Details Mixin]** necessario aggiungerla allo schema Profilo. Una volta aggiunta, la marca temporale personalizzata può essere compilata utilizzando il `lastUpdatedDate` campo. Quando un record viene assimilato con il `lastUpdatedDate` campo popolato,  Experience Platform utilizzerà tale campo per unire record tra set di dati. Se non `lastUpdatedDate` è presente o non è popolato, la piattaforma continuerà a utilizzare la marca temporale del sistema.

>[!NOTE]
>
>È necessario assicurarsi che la `lastUpdatedDate` marca temporale sia compilata durante l&#39;assimilazione di un aggiornamento sullo stesso record.

Nella schermata seguente sono visualizzati i campi nella finestra di dialogo [!UICONTROL External Source System Audit Details Mixin]. Per istruzioni dettagliate sull’utilizzo degli schemi nell’interfaccia utente della piattaforma, inclusa l’aggiunta di mixin agli schemi, consultate l’ [esercitazione per la creazione di uno schema tramite l’interfaccia utente](../../xdm/tutorials/create-schema-ui.md).

![](../images/merge-policies/custom-timestamp-mixin.png)

Per utilizzare le marche temporali personalizzate mediante l&#39;API, consultare la sezione relativa alla guida dell&#39;endpoint delle policy di [unione sull&#39;utilizzo di marche temporali](../api/merge-policies.md#custom-timestamps)personalizzate.

### Precedenza set di dati {#dataset-precedence}

Se **[!UICONTROL Dataset precedence]** è selezionato come metodo di unione per un criterio di unione, è possibile assegnare priorità ai frammenti di profilo in base al set di dati di provenienza. Un esempio di utilizzo sarebbe se l&#39;organizzazione dispone di informazioni presenti in un set di dati preferito o affidabile rispetto ai dati in un altro set di dati.

Per creare un criterio di unione utilizzando **[!UICONTROL Dataset precedence]**, è necessario selezionare i set di dati Profilo ed ExperienceEvent inclusi, quindi è possibile ordinare manualmente i set di dati Profilo per la precedenza. Una volta selezionati e ordinati i set di dati, al set di dati principale verrà data la priorità più alta, al secondo sarà il secondo più alto e così via.

## [!UICONTROL ID stitching] {#id-stitching}

L&#39;unione delle identità ([!UICONTROL ID stitching]) è il processo di identificazione dei frammenti di dati e di loro combinazione per creare un record di profilo completo. Per illustrare i diversi comportamenti di cucitura, si consideri un singolo cliente che interagisce con un marchio utilizzando due indirizzi e-mail diversi.

* **[!UICONTROL None]:** Quando questa opzione è selezionata, gli ID non vengono uniti. Quando si verifica la segmentazione, le identità che possono appartenere alla stessa persona non vengono unite insieme e la segmentazione considera solo gli attributi associati a ciascun singolo ID quando si determina se un cliente è idoneo per l&#39;appartenenza al segmento. Ciò potrebbe causare l&#39;invio di più profili a un singolo cliente e l&#39;invio di più messaggi di marketing allo stesso cliente.
* **[!UICONTROL Private graph]:** Quando il grafico privato è selezionato, più identità correlate allo stesso individuo vengono unite insieme. Questo consente al cliente di avere un unico profilo e alla segmentazione di considerare più attributi da identità correlate multiple per determinare la qualifica del segmento. In questo scenario, è probabile che il cliente abbia un profilo singolo, si qualifichi per un segmento in base alla combinazione di attributi tra identità diverse e riceva un solo messaggio di marketing.

Per saperne di più sulle identità e sul loro ruolo nella generazione di profili e segmenti, consulta la panoramica [del servizio](../../identity-service/home.md)identità.

## Criterio unione predefinito {#default-merge-policy}

Un&#39;organizzazione può creare un criterio di unione predefinito da utilizzare per l&#39;unione dei frammenti di profilo. Questo consente agli utenti di selezionare facilmente il criterio predefinito quando eseguono azioni in  Experience Platform, come la visualizzazione dei profili dei clienti o la creazione di segmenti. Nella maggior parte dei casi, a meno che non venga specificato un altro criterio di unione, verrà utilizzato il criterio di unione predefinito.

Ciascuna organizzazione può creare più criteri di unione relativi a una singola classe di schema XDM, ma può avere un solo criterio di unione predefinito dichiarato per ogni classe. Ad esempio, l&#39;organizzazione potrebbe disporre di un criterio di unione predefinito correlato alla [!DNL XDM Individual Profile] classe e di un altro criterio di unione predefinito per una classe Product Inventory personalizzata.

Se si crea un nuovo criterio di unione e lo si imposta come predefinito, il precedente criterio di unione predefinito verrà aggiornato automaticamente dal sistema in modo che non sia più il predefinito.

>[!WARNING]
>
>I conteggi dei profili e i segmenti con un criterio di unione predefinito esistente associato potrebbero essere interessati. Tutti i segmenti a cui è applicato un criterio di unione predefinito verranno aggiornati al nuovo criterio di unione predefinito.

## Visualizza criteri di unione {#view-merge-policies}

Nell&#39; [!DNL Experience Platform] interfaccia utente, è possibile iniziare a utilizzare i criteri di unione selezionando **[!UICONTROL Profiles]** nella navigazione a sinistra e quindi selezionando la **[!UICONTROL Merge Policies]** scheda. Questa scheda include un elenco di tutti i criteri di unione esistenti per l&#39;organizzazione, nonché i dettagli per ciascun criterio di unione, incluso il nome del criterio, se il criterio di unione è o meno il criterio di unione predefinito e la classe dello schema a cui il criterio di unione fa riferimento.

![Pagina di destinazione Unisci criteri](../images/merge-policies/landing.png)

Per selezionare i dettagli visibili o per aggiungere ulteriori colonne alla visualizzazione, selezionare **[!UICONTROL Configure columns]** e fare clic sul nome di una colonna per aggiungerla o rimuoverla dalla visualizzazione.

![](../images/merge-policies/adjust-view.png)

## Creare un criterio di unione {#create-a-merge-policy}

Per creare un nuovo criterio di unione, selezionare **[!UICONTROL Create merge policy]** nella scheda Criteri di unione.

![Unisci la pagina di destinazione dei criteri con il pulsante Crea evidenziato.](../images/merge-policies/create-new.png)

Nella schermata del **[!UICONTROL New merge policy]** flusso di lavoro, potete fornire informazioni importanti per il nuovo criterio di unione tramite una serie di passaggi guidati.

![Il nuovo flusso di lavoro dei criteri di unione.](../images/merge-policies/create.png)

### [!UICONTROL Configure] {#configure}

Il primo passaggio del flusso di lavoro consente di configurare il criterio di unione fornendo informazioni di base. Queste informazioni includono:

* **[!UICONTROL Name]**: Il nome del criterio di unione deve essere descrittivo ma conciso.
* **[!UICONTROL Schema class]**: La classe dello schema XDM associata al criterio di unione. Indica la classe dello schema per cui viene creato il criterio di unione. Le organizzazioni possono creare più criteri di unione per classe di schema. Attualmente solo la [!UICONTROL XDM Individual Profile] classe è disponibile nell&#39;interfaccia utente.
* **[!UICONTROL ID stitching]**: Questo campo definisce come determinare le identità correlate di un cliente. Per ulteriori informazioni, consulta la sezione sull’unione degli [ID](#id-stitching) in precedenza in questa guida. Esistono due possibili valori:
   * **[!UICONTROL None]**: Non eseguire alcuna cucitura di identità.
   * **[!UICONTROL Private Graph]**: Esegue l&#39;unione delle identità in base al grafico dell&#39;identità privata.
* **[!UICONTROL Default merge policy]**: Pulsante di attivazione/disattivazione che consente di selezionare se il criterio di unione sarà o meno il valore predefinito per l&#39;organizzazione. Se il selettore è attivato, viene visualizzato un avviso che richiede di confermare la modifica del criterio di unione predefinito dell&#39;organizzazione. Per ulteriori informazioni, vedere la sezione relativa ai criteri di unione [predefiniti](#default-merge-policy) fornita in precedenza in questa guida.
   ![](../images/merge-policies/create-make-default.png)

Una volta completati i campi richiesti, potete scegliere **[!UICONTROL Next]** di continuare il flusso di lavoro.

![Schermata Configura completa con il pulsante Avanti evidenziato.](../images/merge-policies/create-complete.png)

### [!UICONTROL Select Profile datasets] {#select-profile-datasets}

Nella **[!UICONTROL Select Profile datasets]** schermata, è necessario selezionare il **[!UICONTROL Merge method]** criterio di unione che si desidera utilizzare. Viene inoltre visualizzato il numero totale di [!UICONTROL Profile datasets] utenti dell&#39;organizzazione che si riferiscono alla classe dello schema selezionata nella schermata precedente.

A seconda del metodo di unione scelto, tutti i set di dati Profilo verranno uniti in base all&#39;ordine in cui sono stati aggiornati per l&#39;ultima volta (timestamp ordinato) oppure dovrete selezionare i set di dati Profilo da includere nel criterio di unione e l&#39;ordine in cui unirli (precedenza set di dati). Per ulteriori informazioni sui metodi di unione, consultare la sezione sui metodi [di](#merge-methods) unione fornita in precedenza in questo documento.

#### Timestamp ordinato {#timestamp-ordered-profile}

Selezionando **[!UICONTROL Timestamp ordered]** come metodo di unione, gli attributi dei set di dati aggiornati più di recente avranno la precedenza. Questo vale per tutti i set di dati del profilo.

![](../images/merge-policies/timestamp-ordered.png)

#### Precedenza set di dati {#dataset-precedence-profile}

La selezione **[!UICONTROL Dataset precedence]** come metodo di unione richiede la selezione dei set di dati del profilo e la loro priorità manuale. È possibile selezionare fino a 50 set di dati dall&#39;elenco dei dataset. I set di dati selezionati vengono visualizzati sul lato destro dello schermo, consentendo di trascinare e rilasciare i set di dati e ordinarli. Man mano che i set di dati vengono modificati nell&#39;elenco, il numero ordinale (1, 2, 3, ecc.) accanto al set di dati si aggiorna e visualizza la priorità (1 con priorità maggiore, quindi 2 e più avanti).

![](../images/merge-policies/dataset-precedence.png)

### [!UICONTROL Select ExperienceEvent datasets] {#select-experienceevent-datasets}

Il passaggio successivo del flusso di lavoro richiede la selezione dei set di dati ExperienceEvent. Questa schermata è influenzata dal metodo di unione selezionato sullo [[!UICONTROL Select Profile datasets]](#select-profile-datasets) schermo.

In questa schermata viene visualizzato anche il numero totale di **[!UICONTROL ExperienceEvent datasets]** creati dall&#39;organizzazione in relazione alla classe dello schema selezionata nella schermata di configurazione del criterio di unione.

#### Timestamp ordinato {#timestamp-ordered-experienceevent}

Se hai selezionato **[!UICONTROL Timestamp ordered]** come metodo di unione per i set di dati Profilo, anche in questo caso gli attributi dei set di dati ExperienceEvent aggiornati più di recente avranno la precedenza.

![](../images/merge-policies/timestamp-experienceevent.png)

#### Precedenza set di dati {#dataset-precedence-experienceevent}

Se hai selezionato **[!UICONTROL Dataset precedence]** come metodo di unione per i set di dati Profilo, dovrai selezionare i set di dati ExperienceEvent da includere. Dall’elenco dei set di dati potete selezionare fino a 50 set di dati ExperienceEvent. I set di dati selezionati vengono visualizzati sul lato destro dello schermo. I set di dati ExperienceEvent non possono essere ordinati manualmente, ma gli attributi nei set di dati ExperienceEvent vengono aggiunti ai set di dati Profile se fanno parte dello stesso frammento di profilo.

![](../images/merge-policies/dataset-precedence-experienceevent.png)

### [!UICONTROL Review] {#review}

Il passaggio finale del flusso di lavoro consiste nel rivedere il criterio di unione. Nella **[!UICONTROL Review]** schermata vengono visualizzati il nome del nuovo criterio di unione, la classe dello schema su cui si basa, l&#39; [!UICONTROL ID stitching] opzione selezionata, nonché il metodo di unione e i set di dati inclusi nel criterio di unione. Per visualizzare tutti i set di dati Profilo o ExperienceEvent inclusi, selezionate il numero di set di dati per espandere l&#39;elenco a discesa.

Prima di selezionare **[!UICONTROL Finish]** per completare il flusso di lavoro di creazione, verifica attentamente i criteri di unione.

#### Timestamp ordinato {#timestamp-ordered-review}

Se è stato selezionato **[!UICONTROL Timestamp ordered]** come metodo di unione per il criterio di unione, l&#39;elenco dei set di dati del profilo include tutti i set di dati creati dall&#39;organizzazione in relazione alla classe dello schema, in ordine di timestamp. L&#39;elenco dei set di dati ExperienceEvent include tutti i set di dati creati dall&#39;organizzazione per la classe di schema selezionata e che verranno aggiunti ai set di dati Profile.

![](../images/merge-policies/timestamp-review.png)

#### Precedenza set di dati {#dataset-precedence-review}

Se hai selezionato **[!UICONTROL Dataset precedence]** come metodo di unione per il criterio di unione, gli elenchi dei set di dati Profile ed ExperienceEvent includono, rispettivamente, solo i set di dati Profile ed ExperienceEvent selezionati durante il flusso di lavoro di creazione. L&#39;ordine dei set di dati Profilo deve corrispondere alla precedenza specificata durante la creazione. In caso contrario, utilizzate il [!UICONTROL Back] pulsante per tornare ai passaggi del flusso di lavoro precedenti e regolare la priorità.

![](../images/merge-policies/dataset-precedence-review.png)

### Elenco aggiornato dei criteri di unione {#updated-list}

Dopo aver completato il flusso di lavoro per la creazione di un nuovo criterio di unione, viene nuovamente visualizzata la **[!UICONTROL Merge Policies]** scheda. L&#39;elenco dei criteri di unione per l&#39;organizzazione deve ora includere il criterio di unione appena creato.

![](../images/merge-policies/new-merge-policy-created.png)

## Modificare un criterio di unione

Dalla [!UICONTROL Merge Policies] scheda, è possibile modificare un criterio di unione esistente creato per la [!DNL XDM Individual Profile] classe selezionando il criterio di unione **[!UICONTROL Policy name]** da modificare.

![Pagina di destinazione Unisci criteri](../images/merge-policies/select-edit.png)

Quando viene visualizzata la **[!UICONTROL Edit merge policy]** schermata, è possibile apportare modifiche al nome e [!UICONTROL ID stitching], nonché modificare se questo criterio è o meno il criterio di unione predefinito per la propria organizzazione.

Selezionare **[!UICONTROL Next]** per continuare il flusso di lavoro dei criteri di unione per aggiornare il metodo di unione e i set di dati inclusi nel criterio di unione.

![](../images/merge-policies/edit-screen.png)

Dopo aver apportato le modifiche necessarie, rivedete i criteri di unione e selezionate **[!UICONTROL Finish]** per tornare alla **[!UICONTROL Merge policies]** scheda.

>[!WARNING]
>
>La modifica di un criterio di unione può influenzare la segmentazione e i risultati del profilo, in quanto altererà il modo in cui vengono risolti i conflitti di dati.

![](../images/merge-policies/edit-review.png)

## Violazioni dei criteri di governance dei dati

Durante la creazione o l&#39;aggiornamento di un criterio di unione, viene eseguito un controllo per determinare se il criterio di unione viola uno qualsiasi dei criteri di utilizzo dei dati definiti dall&#39;organizzazione. I criteri di utilizzo dei dati fanno parte di Adobe Experience Platform [!DNL Data Governance] e sono regole che descrivono i tipi di azioni di marketing consentite o da cui è consentita l&#39;esecuzione su [!DNL Platform] dati specifici. Ad esempio, se un criterio di unione è stato utilizzato per creare un segmento che si è attivato a una destinazione terza e l&#39;organizzazione dispone di un criterio di utilizzo dei dati che impedisce l&#39;esportazione di dati specifici a terzi, durante il tentativo di salvare il criterio di unione riceverai una **[!UICONTROL Data governance policy violation detected]** notifica.

Questa notifica include un elenco di criteri di utilizzo dei dati che sono stati violati e consente di visualizzare i dettagli della violazione selezionando un criterio dall&#39;elenco. Selezionando un criterio violato, la **[!UICONTROL Data lineage]** scheda fornisce il motivo della violazione e delle attivazioni interessate, ognuna delle quali fornisce maggiori dettagli sulle modalità di violazione del criterio di utilizzo dei dati.

Per ulteriori informazioni sulle modalità di gestione dei dati in Adobe Experience Platform, consultare la panoramica [sulla governance dei](../../data-governance/home.md)dati.

![](../images/merge-policies/policy-violation.png)

## Passaggi successivi

Dopo aver creato e configurato criteri di unione per la tua organizzazione, puoi utilizzarli per regolare la visualizzazione dei profili cliente all&#39;interno della piattaforma e per creare segmenti di pubblico dai dati del profilo. Consulta la panoramica [sulla](../../segmentation/home.md) segmentazione per ulteriori informazioni su come creare e lavorare con i segmenti utilizzando l&#39; [!DNL Experience Platform] interfaccia utente e le API.