---
title: Comportamento di esportazione del profilo
description: Scopri come il comportamento di esportazione del profilo varia tra i diversi modelli di integrazione supportati nelle destinazioni di Experience Platform.
exl-id: 2be62843-0644-41fa-a860-ccd65472562e
source-git-commit: e6545dfaf5c43ac854986cfdc4f5cb153a07405b
workflow-type: tm+mt
source-wordcount: '2924'
ht-degree: 0%

---

# Comportamento di esportazione del profilo per diversi tipi di destinazione

In Experience Platform, esistono diversi tipi di destinazione, come illustrato nel diagramma seguente. Tali destinazioni presentano modelli di esportazione leggermente diversi per quanto riguarda gli elementi che determinano un’esportazione di destinazione e quelli inclusi in un’esportazione, come descritto nelle sezioni che seguono.

>[!IMPORTANT]
>
>Questa pagina della documentazione descrive solo il comportamento di esportazione del profilo per le connessioni evidenziate nella parte inferiore del diagramma.

![Diagramma dei tipi di destinazioni](/help/destinations/assets/how-destinations-work/types-of-destinations-v4.png)

## Aggregazione dei messaggi nelle destinazioni di streaming

Prima di immergerti in informazioni specifiche per tipo di destinazione, è importante comprendere il concetto di aggregazione dei messaggi per *destinazioni di streaming*.

Le destinazioni di Experienci Platform esportano i dati in integrazioni basate su API come chiamate HTTPS. Una volta che il servizio delle destinazioni viene informato da altri servizi a monte che i profili sono stati aggiornati in seguito all’acquisizione batch, all’acquisizione in streaming, alla segmentazione batch, alla segmentazione in streaming o a modifiche al grafico delle identità, i dati vengono esportati e inviati alle destinazioni di streaming.

I profili vengono aggregati nei messaggi HTTPS prima di essere inviati agli endpoint API di destinazione.

Prendi il [Destinazione facebook](/help/destinations/catalog/social/facebook.md) con un *[aggregazione configurabile](../destination-sdk/functionality/destination-configuration/aggregation-policy.md)* criterio come esempio: i dati vengono inviati in modo aggregato, dove il servizio destinazioni prende tutti i dati in arrivo dal servizio profilo a monte e li aggrega in base a una delle seguenti opzioni, prima di inviarli a Facebook:

* Numero di record (massimo 10,000) o
* Intervallo intervallo di tempo (300 secondi)

Il primo caso in cui viene raggiunta una delle soglie sopra indicate determina un’esportazione in Facebook. Quindi, nella [!DNL Facebook Custom Audiences] dashboard, i tipi di pubblico potrebbero provenire da Experienci Platform con incrementi di 10.000 record. Potresti visualizzare 10.000 record ogni 2-3 minuti perché i dati vengono elaborati e aggregati più rapidamente dell’intervallo di esportazione di 300 secondi e vengono inviati più rapidamente, quindi circa ogni 2-3 minuti finché tutti i record non vengono elaborati. Se non ci sono record sufficienti per comporre un batch di 10.000, il numero corrente di record verrà inviato così com&#39;è quando viene raggiunta la soglia dell&#39;intervallo di tempo, in modo da poter vedere anche i batch più piccoli inviati a Facebook.

Un altro esempio è dato dalla [Destinazione API HTTP](/help/destinations/catalog/streaming/http-destination.md), che ha un *[aggregazione della migliore fatica](../destination-sdk/functionality/destination-configuration/aggregation-policy.md)* policy, con `maxUsersPerRequest: 10`. Ciò significa che un massimo di dieci profili verranno aggregati prima che venga avviata una chiamata HTTP a questa destinazione, ma Experienci Platform tenta di inviare profili alla destinazione non appena il servizio delle destinazioni riceve informazioni di rivalutazione aggiornate da un servizio a monte.

Il criterio di aggregazione è configurabile e gli sviluppatori di destinazione possono decidere come configurarlo per soddisfare al meglio le limitazioni di velocità degli endpoint API a valle. Ulteriori informazioni su [criterio di aggregazione](../destination-sdk/functionality/destination-configuration/aggregation-policy.md) nella documentazione di Destination SDK.

## Destinazioni di esportazione profilo di streaming (enterprise) {#streaming-profile-destinations}

>[!IMPORTANT]
>
> Le destinazioni Enterprise sono disponibili solo per [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/it/legal/product-descriptions/real-time-customer-data-platform.html) clienti.

Il [destinazioni enterprise](/help/destinations/destination-types.md#streaming-profile-export) Ad Experience Platform, Amazon Kinesis, Azure Event Hub e API HTTP.

Experienci Platform ottimizza il comportamento di esportazione del profilo nella destinazione aziendale, per esportare i dati nell’endpoint API solo quando si sono verificati aggiornamenti rilevanti a un profilo in seguito alla qualifica di un pubblico o ad altri eventi significativi. I profili vengono esportati nella destinazione nelle seguenti situazioni:

* L’aggiornamento del profilo è stato determinato da una modifica in [iscrizione al pubblico](/help/xdm/field-groups/profile/segmentation.md) per almeno uno dei tipi di pubblico mappati sulla destinazione. Ad esempio, il profilo è idoneo per uno dei tipi di pubblico mappati sulla destinazione o è uscito da uno dei tipi di pubblico mappati sulla destinazione.
* L’aggiornamento del profilo è stato determinato da una modifica nella [mappa identità](/help/xdm/field-groups/profile/identitymap.md). Ad esempio, a un profilo che si era già qualificato per uno dei tipi di pubblico mappati sulla destinazione è stata aggiunta una nuova identità nell’attributo identity map.
* L’aggiornamento del profilo è stato determinato da una modifica degli attributi per almeno uno degli attributi mappati alla destinazione. Ad esempio, uno degli attributi mappati sulla destinazione nel passaggio di mappatura viene aggiunto a un profilo.

In tutti i casi descritti sopra, solo i profili in cui si sono verificati aggiornamenti rilevanti vengono esportati nella destinazione. Ad esempio, se un pubblico mappato al flusso di destinazione ha un centinaio di membri e cinque nuovi profili sono idonei per il segmento, l’esportazione nella destinazione è incrementale e include solo i cinque nuovi profili.

Tieni presente che tutti gli attributi mappati vengono esportati per un profilo, indipendentemente da dove si trovano le modifiche. Quindi, nell’esempio precedente, tutti gli attributi mappati per questi cinque nuovi profili verranno esportati anche se gli attributi stessi non sono stati modificati.

### Che cosa determina un’esportazione di dati e cosa è incluso nell’esportazione

Per quanto riguarda i dati esportati per un determinato profilo, è importante comprendere i due diversi concetti di *cosa determina un’esportazione di dati nella destinazione aziendale* e *quali dati sono inclusi nell’esportazione*.

| Cosa determina un’esportazione di destinazione | Cosa è incluso nell’esportazione di destinazione |
|---------|----------|
| <ul><li>Gli attributi e i tipi di pubblico mappati fungono da spunto per un’esportazione di destinazione. Ciò significa che se un pubblico mappato cambia stato (da `null` a `realized` o da `realized` a `exiting`) o se vengono aggiornati eventuali attributi mappati, viene avviata un’esportazione di destinazione.</li><li>Poiché al momento non è possibile mappare le identità sulle destinazioni Enterprise, anche le modifiche apportate alle identità di un determinato profilo determinano le esportazioni delle destinazioni.</li><li>Per modifica di un attributo si intende qualsiasi aggiornamento dell&#39;attributo, indipendentemente dal fatto che si tratti o meno dello stesso valore. Ciò significa che una sovrascrittura su un attributo è considerata una modifica anche se il valore stesso non è cambiato.</li></ul> | <ul><li>Il `segmentMembership` L’oggetto include il pubblico mappato nel flusso di dati di attivazione, per il quale lo stato del profilo è cambiato a seguito di un evento di qualificazione o uscita dal pubblico. Tieni presente che altri tipi di pubblico non mappati per i quali il profilo si è qualificato possono far parte dell’esportazione di destinazione, se tali tipi di pubblico appartengono allo stesso [criterio di unione](/help/profile/merge-policies/overview.md) come il pubblico mappato nel flusso di dati di attivazione. </li><li>Tutte le identità in `identityMap` sono inclusi anche gli oggetti (Experienci Platform attualmente non supporta il mapping delle identità nella destinazione enterprise).</li><li>Nell’esportazione della destinazione sono inclusi solo gli attributi mappati.</li></ul> |

{style="table-layout:fixed"}

>[!IMPORTANT]
>
>Le destinazioni Enterprise generano flussi di dati di backfill durante l’attivazione di profili in una destinazione. Ciò significa che la prima esportazione di dati dopo la configurazione di un flusso di lavoro di attivazione in una destinazione includerà i profili qualificati per il pubblico attivato prima che il pubblico venga mappato sulla destinazione.

>[!BEGINSHADEBOX]

Ad esempio, considera questo flusso di dati come una destinazione HTTP in cui tre tipi di pubblico vengono selezionati nel flusso di dati e quattro attributi vengono mappati sulla destinazione.

![flusso di dati di destinazione enterprise](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Un’esportazione di profilo verso la destinazione può essere determinata da un profilo idoneo o in uscita da uno dei *tre segmenti mappati*. Tuttavia, nell’esportazione dei dati, nella `segmentMembership` oggetto, potrebbero essere visualizzati altri tipi di pubblico non mappati, se quel particolare profilo è un membro di essi e se questi condividono lo stesso criterio di unione del pubblico che ha attivato l’esportazione. Se un profilo è idoneo per **Cliente con auto DeLorean** ma è anche membro del gruppo **Guarda il film &quot;Ritorno al futuro&quot;** e **Fantascienza** segmenti, quindi anche questi altri due tipi di pubblico saranno presenti nel `segmentMembership` oggetto dell’esportazione di dati, anche se non sono mappati nel flusso di dati, se condividono lo stesso criterio di unione con **Cliente con auto DeLorean** segmento.

Dal punto di vista degli attributi di profilo, eventuali modifiche ai quattro attributi mappati in precedenza determineranno un’esportazione di destinazione e uno qualsiasi dei quattro attributi mappati presenti nel profilo sarà presente nell’esportazione di dati.

>[!ENDSHADEBOX]

>[!TIP]
>
> Puoi vedere esempi di dati esportati in varie destinazioni Enterprise nella sezione [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md#exported-data), [Hub eventi di Azure](/help/destinations/catalog/cloud-storage/azure-event-hubs.md#exported-data), e [API HTTP](/help/destinations/catalog/streaming/http-destination.md#exported-data) pagine della documentazione di destinazione.

## Destinazioni basate su API di streaming {#streaming-api-based-destinations}

Il comportamento di esportazione del profilo per destinazioni di streaming come Facebook, Trade Desk e altre integrazioni basate su API è molto simile al comportamento descritto in precedenza per le destinazioni Enterprise.

Esempi di destinazioni di streaming sono le destinazioni appartenenti al [categorie sociali e pubblicitarie](/help/destinations/destination-types.md#categories) nel catalogo.

Un Experience Platform ottimizza il comportamento di esportazione del profilo nella destinazione di streaming, per esportare i dati solo in destinazioni basate su API di streaming quando si sono verificati aggiornamenti rilevanti a un profilo in seguito alla qualificazione di un pubblico o ad altri eventi significativi. I profili vengono esportati nella destinazione nelle seguenti situazioni:

* L’aggiornamento del profilo è stato determinato da una modifica in [iscrizione al pubblico](/help/xdm/field-groups/profile/segmentation.md) per almeno uno dei tipi di pubblico mappati sulla destinazione. Ad esempio, il profilo è idoneo per uno dei tipi di pubblico mappati sulla destinazione o è uscito da uno dei tipi di pubblico mappati sulla destinazione.
* L’aggiornamento del profilo è stato determinato da una modifica nella [mappa identità](/help/xdm/field-groups/profile/identitymap.md) per uno spazio dei nomi di identità contrassegnato per l’esportazione per questa istanza di destinazione. Ad esempio, a un profilo che si era già qualificato per uno dei tipi di pubblico mappati sulla destinazione è stata aggiunta una nuova identità nell’attributo identity map.
* L’aggiornamento del profilo è stato determinato da una modifica degli attributi per almeno uno degli attributi mappati alla destinazione. Ad esempio, uno degli attributi mappati sulla destinazione nel passaggio di mappatura viene aggiunto a un profilo.
* Modifiche del consenso per un profilo quando è configurata l’applicazione automatica del consenso e un profilo rinuncia. L’applicazione automatica del consenso invierà un evento di uscita del pubblico alla destinazione in modo che il profilo non venga incluso in alcun targeting nella destinazione.

In tutti i casi descritti sopra, solo i profili in cui si sono verificati aggiornamenti rilevanti vengono esportati nella destinazione. Ad esempio, se un pubblico mappato al flusso di destinazione ha un centinaio di membri e cinque nuovi profili sono idonei per il segmento, l’esportazione nella destinazione è incrementale e include solo i cinque nuovi profili.

Tieni presente che tutti gli attributi mappati vengono esportati per un profilo, indipendentemente da dove si trovano le modifiche. Quindi, nell’esempio precedente, tutti gli attributi mappati per questi cinque nuovi profili verranno esportati anche se gli attributi stessi non sono stati modificati.

### Che cosa determina un’esportazione di dati e cosa è incluso nell’esportazione

Per quanto riguarda i dati esportati per un determinato profilo, è importante comprendere i due diversi concetti di cosa determina un’esportazione di dati nella destinazione API di streaming e quali dati vengono inclusi nell’esportazione.

| Cosa determina un’esportazione di destinazione | Cosa è incluso nell’esportazione di destinazione |
|---------|----------|
| <ul><li>Gli attributi e i tipi di pubblico mappati fungono da spunto per un’esportazione di destinazione. Ciò significa che se un pubblico mappato cambia stato (da `null` a `realized` o da `realized` a `exiting`) o se vengono aggiornati eventuali attributi mappati, viene avviata un’esportazione di destinazione.</li><li>Una modifica nella mappa delle identità è definita come un’identità aggiunta/rimossa per [grafo delle identità](/help/identity-service/ui/identity-graph-viewer.md) del profilo, per gli spazi dei nomi di identità mappati per l’esportazione.</li><li>Per modifica di un attributo si intende qualsiasi aggiornamento dell&#39;attributo, per gli attributi mappati alla destinazione.</li></ul> | <ul><li>I tipi di pubblico mappati sulla destinazione e modificati verranno inclusi nel `segmentMembership` oggetto. In alcuni scenari potrebbero essere esportati utilizzando più chiamate. Inoltre, in alcuni scenari, alcuni tipi di pubblico che non sono stati modificati potrebbero essere inclusi nella chiamata. In ogni caso, verranno esportati solo i tipi di pubblico mappati.</li><li>Tutte le identità dagli spazi dei nomi mappati alla destinazione in `identityMap` sono inclusi anche gli oggetti.</li><li>Nell’esportazione della destinazione sono inclusi solo gli attributi mappati.</li></ul> |

{style="table-layout:fixed"}

>[!IMPORTANT]
>
>Le destinazioni API di streaming riproducono i dati di backfill durante l’attivazione dei profili in una destinazione. Ciò significa che la prima esportazione di dati dopo la configurazione di un flusso di lavoro di attivazione in una destinazione includerà i profili qualificati per il pubblico attivato prima che il pubblico venga mappato sulla destinazione.

>[!BEGINSHADEBOX]

Ad esempio, considera questo flusso di dati come una destinazione di streaming in cui tre tipi di pubblico sono selezionati nel flusso di dati.

![flusso di dati di destinazione streaming](/help/destinations/assets/how-destinations-work/streaming-destination-example-dataflow.png)

Un’esportazione di profilo nella destinazione può essere determinata da un profilo che si qualifica per o esce da uno dei tre segmenti mappati. Se un profilo è qualificato per **Cliente con auto DeLorean** , attiverà un’esportazione. Gli altri tipi di pubblico (**Città - Dallas** e **Sito di base attivo**) potrebbe essere esportato anche nel caso in cui il profilo abbia quel pubblico presente con uno dei possibili stati (`realized` o `exited`). Tipi di pubblico non mappati (come **Fantascienza**) non verrà esportato.

Dal punto di vista degli attributi di profilo, eventuali modifiche ai tre attributi mappati in precedenza determineranno un’esportazione di destinazione.

>[!ENDSHADEBOX]

## Destinazioni batch (basate su file) {#file-based-destinations}

Durante l’esportazione di profili in [destinazioni basate su file](/help/destinations/destination-types.md#file-based) ad Experience Platform, sono disponibili tre tipi di pianificazioni (elencate di seguito) e due opzioni di esportazione file (file completi o incrementali). Tutte queste impostazioni sono impostate a livello di pubblico, anche quando più tipi di pubblico sono mappati su un singolo flusso di dati di destinazione.

* Esportazioni pianificate: configura una destinazione, aggiungi uno o più segmenti, seleziona se desideri esportare file completi o incrementali e seleziona un orario impostato ogni giorno o più volte al giorno in cui i file devono essere esportati. Ad esempio, un orario di esportazione delle 17:00 indica che i profili qualificati per il pubblico verranno esportati alle 17:00.
* Dopo la valutazione del segmento: l’esportazione viene attivata immediatamente dopo l’esecuzione del processo di valutazione del pubblico giornaliero. Ciò significa che i numeri di profilo esportati nel file sono il più possibile simili all’ultima popolazione valutata del segmento.
* Esportazioni su richiesta ([esporta subito il file](/help/destinations/ui/export-file-now.md)): in base all’ultimo processo di valutazione del pubblico, viene esportato un file completo una tantum oltre alle esportazioni regolarmente pianificate.

In una qualsiasi delle situazioni di esportazione precedenti, i file esportati includono i profili idonei per l’esportazione, insieme alle colonne selezionate come attributi XDM per l’esportazione.

>[!TIP]
>
>Quando un pubblico di streaming viene mappato a una destinazione batch, vi è una maggiore probabilità che il numero di profili nel file esportato sia più vicino al numero di utenti nel segmento. Questo perché esiste una maggiore probabilità che l’ultima valutazione del pubblico sia stata eseguita più vicino al tempo di esportazione.

### Esportazioni file incrementali {#incremental-file-exports}

Non tutti gli aggiornamenti di un profilo qualificano un profilo da includere nelle esportazioni di file incrementali. Ad esempio, se un attributo è stato aggiunto o rimosso da un profilo, questo non include il profilo nell’esportazione. Solo i profili per i quali `segmentMembership` L&#39;attributo modificato verrà incluso nei file esportati. In altre parole, solo se il profilo diventa parte del pubblico o viene rimosso dal pubblico, è incluso nelle esportazioni di file incrementali.

Analogamente, se una nuova identità (nuovo indirizzo e-mail, numero di telefono, ECID e così via) viene aggiunta a un profilo in [grafo delle identità](/help/identity-service/ui/identity-graph-viewer.md), che non rappresenta un motivo per includere il profilo in una nuova esportazione di file incrementale.

L’aggiunta di un nuovo pubblico a una mappatura di destinazione non influisce sulle qualifiche e sulle esportazioni di un altro segmento. Le pianificazioni di esportazione sono configurate singolarmente per pubblico e i file vengono esportati separatamente per ogni segmento, anche se i tipi di pubblico sono stati aggiunti allo stesso flusso di dati di destinazione.

>[!BEGINSHADEBOX]

Ad esempio, nell’impostazione di esportazione illustrata di seguito, in cui un pubblico esporta aggiornamenti di file incrementali, tieni presente le seguenti circostanze in cui un profilo è incluso o meno in un’esportazione di file incrementali:

![Esporta l&#39;impostazione con diversi attributi selezionati.](/help/destinations/assets/how-destinations-work/export-selection-batch-destination.png)

* Un profilo viene incluso in un’esportazione di file incrementale quando è idoneo o non idoneo per il segmento.
* Un profilo è *non* incluso in un’esportazione di file incrementale quando un nuovo numero di telefono viene aggiunto al grafico delle identità.
* Un profilo è *non* incluso in un’esportazione di file incrementale quando il valore di uno qualsiasi dei campi XDM mappati come `xdm: loyalty.points`, `xdm: loyalty.tier`, `xdm: personalEmail.address` viene aggiornato su un profilo.
* Quando `segmentMembership.status` Il campo XDM è mappato nel flusso di lavoro di attivazione della destinazione. Anche i profili che escono dal pubblico vengono inclusi nei file incrementali esportati, con un `exited` stato.

>[!ENDSHADEBOX]

### Che cosa determina un’esportazione di dati e cosa è incluso nell’esportazione

In base alle informazioni contenute nella sezione precedente, il comportamento di esportazione del profilo nelle destinazioni basate su file può essere riassunto come descritto di seguito:

**Esportazioni di file completi**

L’intera popolazione attiva del pubblico viene esportata ogni giorno.

| Cosa determina un’esportazione di destinazione | Cosa è incluso nel file esportato |
|---------|----------|
| <ul><li>La pianificazione dell’esportazione impostata nell’interfaccia utente o nell’API e l’azione dell’utente (selezione [Esporta subito il file](/help/destinations/ui/export-file-now.md) nell’interfaccia utente o utilizzando [API di attivazione ad hoc](/help/destinations/api/ad-hoc-activation-api.md)) determinano l&#39;inizio di un&#39;esportazione di destinazione.</li></ul> | Nelle esportazioni di file completi, l’intera popolazione di profili attivi di un segmento, in base alla valutazione del pubblico più recente, viene inclusa in ogni esportazione di file. Come colonne in ciascun file vengono inclusi anche i valori più recenti di ciascun attributo XDM selezionato per l’esportazione. I profili in stato di uscita non vengono inclusi nell’esportazione del file. |

{style="table-layout:fixed"}

**Esportazioni file incrementali**

Nella prima esportazione di file dopo la configurazione del flusso di lavoro di attivazione, viene esportata l’intera popolazione del pubblico. Nelle esportazioni successive, vengono esportati solo i profili modificati.

| Cosa determina un’esportazione di destinazione | Cosa è incluso nel file esportato |
|---------|----------|
| <ul><li>La pianificazione di esportazione impostata nell’interfaccia utente o nell’API determina l’inizio di un’esportazione di destinazione.</li><li>Qualsiasi modifica nell’appartenenza a un pubblico di un profilo, che si qualifichi o meno dal segmento, qualifica un profilo da includere nelle esportazioni incrementali. Modifiche negli attributi o nelle mappe di identità per un profilo *non* qualificano un profilo da includere nelle esportazioni incrementali.</li></ul> | <p>I profili per i quali è stata modificata l’iscrizione al pubblico, insieme alle informazioni più recenti per ogni attributo XDM selezionato per l’esportazione.</p><p>I profili con lo stato di uscita vengono inclusi nelle esportazioni di destinazione, se `segmentMembership.status` Il campo XDM viene selezionato nel passaggio di mappatura.</p> |

{style="table-layout:fixed"}

>[!TIP]
>
>Come promemoria, le modifiche nei valori degli attributi o nelle mappe di identità per un profilo non qualificano un profilo da includere in un’esportazione di file incrementale.

## Passaggi successivi {#next-steps}

Dopo aver letto questo documento, sai cosa aspettarti di vedere nelle esportazioni di profili in destinazioni di streaming, aziendali e basate su file.

Ora, puoi leggere come [le identità vengono gestite](/help/destinations/how-destinations-work/identity-handling.md) nel flusso di lavoro di attivazione.
