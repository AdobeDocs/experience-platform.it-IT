---
title: Comportamento dell’esportazione del profilo
description: Scopri in che modo il comportamento di esportazione del profilo varia tra i diversi pattern di integrazione supportati nelle destinazioni di Experience Platform.
source-git-commit: 4d1f9fa19bd35095e3ccbd8d83bcc33dcd4c45a8
workflow-type: tm+mt
source-wordcount: '2933'
ht-degree: 0%

---

# Comportamento dell’esportazione del profilo per diversi tipi di destinazione

Nell’Experience Platform sono disponibili diversi tipi di destinazione, come illustrato nel diagramma seguente. Tali destinazioni presentano modelli di esportazione leggermente diversi per quanto riguarda gli elementi che determinano l’esportazione di una destinazione e quelli inclusi in un’esportazione, come descritto nelle sezioni più avanti.

>[!IMPORTANT]
>
>Questa pagina di documentazione descrive solo il comportamento di esportazione del profilo per le connessioni evidenziate nella parte inferiore del diagramma.

![Diagramma dei tipi di destinazioni](/help/destinations/assets/how-destinations-work/types-of-destinations-v4.png)

## Criteri di microbatch e aggregazione

Prima di immergersi in informazioni specifiche per tipo di destinazione, è importante comprendere i concetti di microbatch e di policy di aggregazione per *destinazioni di streaming*.

Le destinazioni di Experience Platform esportano i dati nelle integrazioni basate su API come chiamate HTTPS. Una volta che il servizio di destinazioni viene notificato da altri servizi upstream che i profili sono stati aggiornati a seguito dell’acquisizione batch, dell’acquisizione in streaming, della segmentazione batch, dello streaming segmentation o delle modifiche del grafico di identità, i dati vengono esportati e inviati alle destinazioni di streaming.

Viene chiamato il processo tramite il quale i profili vengono aggregati in messaggi HTTPS prima di essere inviati agli endpoint API di destinazione *microbatch*.

Prendi la [Destinazione facebook](/help/destinations/catalog/social/facebook.md) con *[aggregazione configurabile](/help/destinations/destination-sdk/destination-configuration.md#configurable-aggregation)* policy come esempio: i dati vengono inviati in modo aggregato, dove il servizio destinazioni raccoglie tutti i dati in arrivo dal servizio profilo a monte e li aggrega in uno dei modi seguenti, prima di inviarli a Facebook:

* Numero di record (massimo 10.000) o
* Intervallo della finestra temporale (30 minuti)

Una delle soglie sopra soddisfatte determina l’attivazione di un’esportazione in Facebook. Quindi, nella [!DNL Facebook Custom Audiences] dashboard, potresti vedere i tipi di pubblico provenienti da Experience Platform con incrementi di 10.000 record. Potresti visualizzare 10.000 record ogni 10-15 minuti perché i dati vengono elaborati e aggregati più velocemente rispetto all&#39;intervallo di esportazione di 30 minuti, e vengono inviati più velocemente, quindi ogni 10-15 minuti circa fino a quando tutti i record non sono stati elaborati. Se i record non sono sufficienti per creare un batch da 10.000, il numero corrente di record verrà inviato così come avviene quando viene soddisfatta la soglia della finestra temporale, pertanto potresti visualizzare batch più piccoli inviati anche a Facebook.

Un altro esempio: [Destinazione API HTTP](/help/destinations/catalog/streaming/http-destination.md)che ha *[aggregazione dello sforzo migliore](/help/destinations/destination-sdk/destination-configuration.md#best-effort-aggregation)* con `maxUsersPerRequest: 10`. Ciò significa che un massimo di dieci profili saranno aggregati prima che una chiamata HTTP venga attivata a questa destinazione, ma Experience Platform tenta di inviare profili alla destinazione non appena il servizio di destinazioni riceve informazioni di rivalutazione aggiornate da un servizio a monte.

Il criterio di aggregazione è configurabile e gli sviluppatori di destinazione possono decidere come configurare il criterio di aggregazione in modo da soddisfare al meglio le limitazioni di tasso degli endpoint API a valle. Ulteriori informazioni [criterio di aggregazione](/help/destinations/destination-sdk/destination-configuration.md#aggregation) nella documentazione Destination SDK.

## Destinazioni di esportazione del profilo di streaming (enterprise) {#streaming-profile-destinations}

>[!IMPORTANT]
>
> Le destinazioni Enterprise sono disponibili solo per [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) clienti.

La [destinazioni aziendali](/help/destinations/destination-types.md#streaming-profile-export) ad Experience Platform, Amazon Kinesis, Azure Event Hubs e HTTP API.

Experience Platform ottimizza il comportamento di esportazione del profilo nella destinazione enterprise, in modo da esportare i dati nell’endpoint API solo quando si sono verificati aggiornamenti rilevanti a un profilo in seguito alla qualifica del segmento o altri eventi significativi. I profili vengono esportati nella destinazione nelle situazioni seguenti:

* L&#39;aggiornamento del profilo è stato determinato da una modifica in [appartenenza a un segmento](/help/xdm/field-groups/profile/segmentation.md) per almeno uno dei segmenti mappati alla destinazione. Ad esempio, il profilo si è qualificato per uno dei segmenti mappati alla destinazione o è uscito da uno dei segmenti mappati alla destinazione.
* L&#39;aggiornamento del profilo è stato determinato da una modifica nel [mappa identità](/help/xdm/field-groups/profile/identitymap.md). Ad esempio, a un profilo già qualificato per uno dei segmenti mappati alla destinazione è stata aggiunta una nuova identità nell’attributo di mappa identità.
* L&#39;aggiornamento del profilo è stato determinato da una modifica degli attributi per almeno uno degli attributi mappati alla destinazione. Ad esempio, uno degli attributi mappati alla destinazione nel passaggio di mappatura viene aggiunto a un profilo.

In tutti i casi descritti in precedenza, vengono esportati nella destinazione solo i profili in cui si sono verificati aggiornamenti rilevanti. Ad esempio, se un segmento mappato al flusso di destinazione ha un centinaio di membri e cinque nuovi profili sono qualificati per il segmento, l’esportazione nella destinazione è incrementale e include solo i cinque nuovi profili.

Tieni presente che tutti gli attributi mappati vengono esportati per un profilo, indipendentemente da dove si trovano le modifiche. Nell’esempio precedente, quindi, tutti gli attributi mappati per questi cinque nuovi profili verranno esportati anche se gli attributi stessi non sono cambiati.

### Cosa determina un’esportazione di dati e cosa è incluso nell’esportazione

Per quanto riguarda i dati esportati per un determinato profilo, è importante comprendere i due diversi concetti di *cosa determina un’esportazione di dati nella destinazione enterprise* e *quali dati sono inclusi nell&#39;esportazione*.

| Cosa determina un’esportazione di destinazione | Contenuto dell’esportazione di destinazione |
|---------|----------|
| <ul><li>Gli attributi e i segmenti mappati fungono da spunto per un’esportazione di destinazione. Ciò significa che, se un segmento mappato cambia stato (da `null` a `realized` o `realized` a `exiting`) o gli eventuali attributi mappati vengono aggiornati; un’esportazione di destinazione viene avviata.</li><li>Poiché le identità non possono attualmente essere mappate su destinazioni aziendali, anche le modifiche di qualsiasi identità in un determinato profilo determinano le esportazioni di destinazione.</li><li>Una modifica per un attributo è definita come qualsiasi aggiornamento sull&#39;attributo, che sia o meno lo stesso valore. Ciò significa che una sovrascrittura su un attributo viene considerata una modifica anche se il valore stesso non è stato modificato.</li></ul> | <ul><li>La `segmentMembership` l&#39;oggetto include il segmento mappato nel flusso di dati di attivazione per il quale lo stato del profilo è cambiato in seguito a un evento di uscita della qualifica o del segmento. Tieni presente che altri segmenti non mappati per i quali il profilo è qualificato possono far parte dell’esportazione di destinazione, se questi segmenti appartengono allo stesso [criterio di unione](/help/profile/merge-policies/overview.md) come segmento mappato nel flusso di dati di attivazione. </li><li>Tutte le identità nel `identityMap` sono inclusi anche gli oggetti (l&#39;Experience Platform attualmente non supporta la mappatura dell&#39;identità nella destinazione enterprise).</li><li>Solo gli attributi mappati sono inclusi nell’esportazione di destinazione.</li></ul> |

{style="table-layout:fixed"}

>[!IMPORTANT]
>
>Le destinazioni aziendali eseguono il backfill dei dati quando attivano i profili in una destinazione. Ciò significa che la prima esportazione di dati dopo la configurazione di un flusso di lavoro di attivazione a una destinazione includerà i profili qualificati per il segmento attivato prima che il segmento sia mappato alla destinazione.

>[!BEGINSHADEBOX]

Ad esempio, considera questo flusso di dati come una destinazione HTTP in cui tre segmenti sono selezionati nel flusso di dati e quattro attributi sono mappati sulla destinazione.

![flusso di dati di destinazione enterprise](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Un’esportazione di profilo verso la destinazione può essere determinata da un profilo che qualifica o esce da uno dei *tre segmenti mappati*. Tuttavia, nell’esportazione dei dati, nella `segmentMembership` oggetti, potrebbero essere visualizzati altri segmenti non mappati, se quel particolare profilo è membro di tali segmenti e se questi condividono lo stesso criterio di unione del segmento che ha attivato l’esportazione. Se un profilo è idoneo per **Cliente con DeLorean Cars** ma è anche membro del **Guarda il film &quot;Torna al futuro&quot;** e **fan della fantascienza** i segmenti, quindi anche questi altri due segmenti saranno presenti nel `segmentMembership` oggetto dell&#39;esportazione di dati, anche se non mappati nel flusso di dati, se questi condividono lo stesso criterio di unione con il **Cliente con DeLorean Cars** segmento.

Dal punto di vista degli attributi del profilo, eventuali modifiche ai quattro attributi mappati sopra determineranno un’esportazione di destinazione e uno qualsiasi dei quattro attributi mappati presenti sul profilo sarà presente nell’esportazione dei dati.

>[!ENDSHADEBOX]

>[!TIP]
>
> Puoi vedere esempi di dati esportati in varie destinazioni aziendali nella sezione [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md#exported-data), [Hub eventi di Azure](/help/destinations/catalog/cloud-storage/azure-event-hubs.md#exported-data)e [API HTTP](/help/destinations/catalog/streaming/http-destination.md#exported-data) pagine della documentazione di destinazione.

## Destinazioni basate su API in streaming {#streaming-api-based-destinations}

Il comportamento di esportazione del profilo per destinazioni di streaming come Facebook, Trade Desk e altre integrazioni basate su API è molto simile al comportamento descritto in precedenza per le destinazioni aziendali.

Esempi di destinazioni di streaming sono le destinazioni appartenenti al [categorie sociali e pubblicitarie](/help/destinations/destination-types.md#categories) nel catalogo.

Experience Platform ottimizza il comportamento di esportazione del profilo nella destinazione di streaming, in modo da esportare i dati solo nelle destinazioni basate su API in streaming quando si sono verificati aggiornamenti rilevanti a un profilo in seguito alla qualifica del segmento o altri eventi significativi. I profili vengono esportati nella destinazione nelle situazioni seguenti:

* L&#39;aggiornamento del profilo è stato determinato da una modifica in [appartenenza a un segmento](/help/xdm/field-groups/profile/segmentation.md) per almeno uno dei segmenti mappati alla destinazione. Ad esempio, il profilo si è qualificato per uno dei segmenti mappati alla destinazione o è uscito da uno dei segmenti mappati alla destinazione.
* L&#39;aggiornamento del profilo è stato determinato da una modifica nel [mappa identità](/help/xdm/field-groups/profile/identitymap.md) per uno spazio dei nomi di identità contrassegnato per l&#39;esportazione per questa istanza di destinazione. Ad esempio, a un profilo già qualificato per uno dei segmenti mappati alla destinazione è stata aggiunta una nuova identità nell’attributo di mappa identità.
* L&#39;aggiornamento del profilo è stato determinato da una modifica degli attributi per almeno uno degli attributi mappati alla destinazione. Ad esempio, uno degli attributi mappati alla destinazione nel passaggio di mappatura viene aggiunto a un profilo.
* Il consenso cambia per un profilo quando è configurata l’implementazione automatica del consenso e un profilo rifiuta. L’applicazione automatica del consenso invierà un evento di uscita dal pubblico alla destinazione in modo che il profilo non sia incluso in alcun targeting nella destinazione.

In tutti i casi descritti in precedenza, vengono esportati nella destinazione solo i profili in cui si sono verificati aggiornamenti rilevanti. Ad esempio, se un segmento mappato al flusso di destinazione ha un centinaio di membri e cinque nuovi profili sono qualificati per il segmento, l’esportazione nella destinazione è incrementale e include solo i cinque nuovi profili.

Tieni presente che tutti gli attributi mappati vengono esportati per un profilo, indipendentemente da dove si trovano le modifiche. Nell’esempio precedente, quindi, tutti gli attributi mappati per questi cinque nuovi profili verranno esportati anche se gli attributi stessi non sono cambiati.

### Cosa determina un’esportazione di dati e cosa è incluso nell’esportazione

Per quanto riguarda i dati esportati per un determinato profilo, è importante comprendere i due concetti diversi di ciò che determina un’esportazione di dati nella destinazione API di streaming e quali dati vengono inclusi nell’esportazione.

| Cosa determina un’esportazione di destinazione | Contenuto dell’esportazione di destinazione |
|---------|----------|
| <ul><li>Gli attributi e i segmenti mappati fungono da spunto per un’esportazione di destinazione. Ciò significa che, se un segmento mappato cambia stato (da `null` a `realized` o `realized` a `exiting`) o gli eventuali attributi mappati vengono aggiornati; un’esportazione di destinazione viene avviata.</li><li>Una modifica nella mappa di identità è definita come un&#39;identità aggiunta/rimossa per [grafico delle identità](/help/identity-service/ui/identity-graph-viewer.md) del profilo, per i namespace di identità mappati per l’esportazione.</li><li>Una modifica per un attributo viene definita come qualsiasi aggiornamento sull&#39;attributo, per gli attributi mappati sulla destinazione.</li></ul> | <ul><li>I segmenti mappati alla destinazione e modificati verranno inclusi nella variabile `segmentMembership` oggetto. In alcuni scenari potrebbero essere esportati utilizzando più chiamate. Inoltre, in alcuni scenari, alcuni segmenti che non sono stati modificati potrebbero essere inclusi anche nella chiamata . In ogni caso, verranno esportati solo i segmenti mappati.</li><li>Tutte le identità dagli spazi dei nomi mappati alla destinazione nel `identityMap` sono inclusi anche gli oggetti .</li><li>Solo gli attributi mappati sono inclusi nell’esportazione di destinazione.</li></ul> |

{style="table-layout:fixed"}

>[!IMPORTANT]
>
>Le destinazioni API in streaming trasmettono i dati di backfill durante l’attivazione dei profili a una destinazione. Ciò significa che la prima esportazione di dati dopo la configurazione di un flusso di lavoro di attivazione a una destinazione includerà i profili qualificati per il segmento attivato prima che il segmento sia mappato alla destinazione.

>[!BEGINSHADEBOX]

Ad esempio, considera questo flusso di dati in una destinazione di streaming in cui tre segmenti sono selezionati nel flusso di dati.

![flusso di dati di destinazione](/help/destinations/assets/how-destinations-work/streaming-destination-example-dataflow.png)

Un’esportazione di profilo verso la destinazione può essere determinata da un profilo che qualifica o esce da uno dei tre segmenti mappati. Se un profilo è qualificato per **Cliente con DeLorean Cars** questo attiverà un’esportazione. Gli altri segmenti (**Città - Dallas** e **Sito di base attivo** potrebbe essere esportato anche nel caso in cui il profilo abbia quel segmento presente con uno dei possibili stati (`realized` o `exited`). Segmenti non mappati (come **fan della fantascienza**) non verrà esportato.

Dal punto di vista degli attributi del profilo, qualsiasi modifica ai tre attributi mappati sopra determinerà un’esportazione di destinazione.

>[!ENDSHADEBOX]

## Destinazioni batch (basate su file) {#file-based-destinations}

Durante l’esportazione dei profili in [destinazioni basate su file](/help/destinations/destination-types.md#file-based) ad Experience Platform, puoi utilizzare tre tipi di pianificazioni (elencate di seguito) e due opzioni di esportazione file (file completi o incrementali). Tutte queste impostazioni sono impostate a livello di segmento, anche quando più segmenti sono mappati a un singolo flusso di dati di destinazione.

* Esportazioni programmate: Configura una destinazione, aggiungi uno o più segmenti, seleziona se desideri esportare file completi o incrementali e seleziona un’ora impostata ogni giorno o più volte al giorno in cui i file devono essere esportati. Ad esempio, un tempo di esportazione di 5 PM significa che qualunque profilo sia qualificato per il segmento verrà esportato alle 17:00.
* Dopo la valutazione del segmento: L’esportazione viene attivata immediatamente dopo l’esecuzione del processo di valutazione del segmento giornaliero. Ciò significa che i numeri di profilo esportati nel file sono il più vicini possibile alla popolazione valutata più recente del segmento.
* Esportazioni a richiesta ([esporta file](/help/destinations/ui/export-file-now.md)): In base all’ultimo processo di valutazione dei segmenti, un file completo viene esportato una volta sola oltre alle esportazioni pianificate regolarmente.

In una qualsiasi delle situazioni di esportazione di cui sopra, i file esportati includono i profili qualificati per l’esportazione, insieme alle colonne selezionate come attributi XDM per l’esportazione.

>[!TIP]
>
>Quando un segmento in streaming viene mappato su una destinazione batch, c&#39;è una maggiore probabilità che il numero di profili nel file esportato sia più vicino al numero di utenti nel segmento. Ciò è dovuto al fatto che esiste una maggiore probabilità che l’ultima valutazione del segmento sia più vicina al tempo di esportazione.

### Esportazioni incrementali di file {#incremental-file-exports}

Non tutti gli aggiornamenti su un profilo qualificano un profilo da includere nelle esportazioni incrementali di file. Ad esempio, se un attributo è stato aggiunto o rimosso da un profilo, questo non include il profilo nell’esportazione. Solo i profili per i quali il `segmentMembership` L&#39;attributo modificato verrà incluso nei file esportati. In altre parole, solo se il profilo diventa parte del segmento o viene rimosso dal segmento viene incluso nelle esportazioni di file incrementali.

Allo stesso modo, se viene aggiunta una nuova identità (nuovo indirizzo e-mail, numero di telefono, ECID e così via) a un profilo in [grafico delle identità](/help/identity-service/ui/identity-graph-viewer.md), che non rappresenta un motivo per includere il profilo in una nuova esportazione di file incrementali.

Se un nuovo segmento viene aggiunto a una mappatura di destinazione, questo non influisce sulle qualifiche e sulle esportazioni per un altro segmento. Le pianificazioni di esportazione sono configurate singolarmente per segmento e i file vengono esportati separatamente per ogni segmento, anche se i segmenti sono stati aggiunti allo stesso flusso di dati di destinazione.

>[!BEGINSHADEBOX]

Ad esempio, nell’impostazione di esportazione illustrata di seguito, in cui un segmento esporta aggiornamenti di file incrementali, tieni presente le seguenti circostanze in cui un profilo viene incluso o meno in un’esportazione di file incrementali:

![Esporta le impostazioni con diversi attributi selezionati.](/help/destinations/assets/how-destinations-work/export-selection-batch-destination.png)

* Un profilo viene incluso in un’esportazione di file incrementale quando è idoneo o non è idoneo per il segmento.
* Un profilo è *not* incluso in un’esportazione di file incrementale quando viene aggiunto un nuovo numero di telefono al grafico dell’identità.
* Un profilo è *not* incluso in un’esportazione di file incrementale quando il valore di uno qualsiasi dei campi XDM mappati come `xdm: loyalty.points`, `xdm: loyalty.tier`, `xdm: personalEmail.address` viene aggiornato su un profilo.
* Ogni volta che `segmentMembership.status` Il campo XDM è mappato nel flusso di lavoro di attivazione della destinazione, i profili che escono dal segmento sono inclusi anche nei file incrementali esportati, con un `exited` stato.

>[!ENDSHADEBOX]

### Cosa determina un’esportazione di dati e cosa è incluso nell’esportazione

In base alle informazioni contenute nella sezione precedente, il comportamento di esportazione del profilo verso destinazioni basate su file può essere riassunto come descritto di seguito:

**Esportazioni complete di file**

La popolazione attiva completa del segmento viene esportata ogni giorno.

| Cosa determina un’esportazione di destinazione | Contenuto del file esportato |
|---------|----------|
| <ul><li>La pianificazione per l’esportazione impostata nell’interfaccia utente o nell’API e l’azione dell’utente (selezionando [Esporta file ora](/help/destinations/ui/export-file-now.md) nell’interfaccia utente o utilizzando [API di attivazione ad hoc](/help/destinations/api/ad-hoc-activation-api.md)) determina l&#39;inizio di un&#39;esportazione di destinazione.</li></ul> | Nelle esportazioni di file completi, l’intero gruppo di profili attivo di un segmento, in base alla valutazione più recente del segmento, è incluso in ogni esportazione di file. Gli ultimi valori per ogni attributo XDM selezionato per l’esportazione sono inclusi anche come colonne in ciascun file. I profili in stato di uscita non sono inclusi nell’esportazione del file. |

{style="table-layout:fixed"}

**Esportazioni incrementali di file**

Nella prima esportazione di file dopo aver impostato il flusso di lavoro di attivazione, viene esportata l’intera popolazione del segmento. Nelle esportazioni successive, vengono esportati solo i profili modificati.

| Cosa determina un’esportazione di destinazione | Contenuto del file esportato |
|---------|----------|
| <ul><li>La pianificazione per l’esportazione impostata nell’interfaccia utente o nell’API determina l’inizio di un’esportazione di destinazione.</li><li>Qualsiasi modifica nell’appartenenza a un segmento di un profilo, che si qualifichi o meno dal segmento, qualifica un profilo da includere nelle esportazioni incrementali. Modifiche agli attributi o alle mappe di identità per un profilo *non* qualificare un profilo da includere nelle esportazioni incrementali.</li></ul> | <p>I profili per i quali è stata modificata l’appartenenza al segmento, insieme alle informazioni più recenti per ogni attributo XDM selezionato per l’esportazione.</p><p>I profili con lo stato di uscita sono inclusi nelle esportazioni di destinazione, se il `segmentMembership.status` Il campo XDM viene selezionato nella fase di mappatura.</p> |

{style="table-layout:fixed"}

>[!TIP]
>
>Come promemoria, le modifiche apportate ai valori degli attributi o alle mappe di identità per un profilo non qualificano un profilo da includere in un’esportazione di file incrementale.

## Passaggi successivi {#next-steps}

Dopo aver letto questo documento, ora sai cosa aspettarti di vedere nelle esportazioni di profili verso destinazioni in streaming, enterprise e basate su file.

Successivamente, puoi leggere come [le identità vengono gestite](/help/destinations/how-destinations-work/identity-handling.md) nel flusso di lavoro di attivazione.
