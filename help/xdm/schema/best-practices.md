---
keywords: Experience Platform;home;argomenti popolari;schema;schema;enum;identità primaria;identità primaria;profilo individuale XDM;evento esperienza;XDM Experience Event;XDM ExperienceEvent;experienceEvent;experienceevent;XDM Experienceevenet;progettazione schema;best practice
solution: Experience Platform
title: Best Practice Per La Modellazione Dei Dati
description: Questo documento fornisce un’introduzione agli schemi Experience Data Model (XDM) e ai blocchi predefiniti, ai principi e alle best practice per la composizione degli schemi da utilizzare in Adobe Experience Platform.
exl-id: 2455a04e-d589-49b2-a3cb-abb5c0b4e42f
source-git-commit: b144a93374fc627f9001b80695cad3f17e28a6fe
workflow-type: tm+mt
source-wordcount: '3214'
ht-degree: 1%

---

# Best practice per la modellazione dei dati

[!DNL Experience Data Model] (XDM) è il framework di base che standardizza i dati sull&#39;esperienza del cliente fornendo strutture e definizioni comuni da utilizzare nei servizi Adobe Experience Platform a valle. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune e utilizzati per ottenere informazioni preziose dalle azioni dei clienti, definire il pubblico dei clienti ed esprimere gli attributi dei clienti a scopo di personalizzazione.

Poiché XDM è estremamente versatile e personalizzabile dalla progettazione, è importante seguire le best practice per la modellazione dei dati durante la progettazione degli schemi. Questo documento descrive le decisioni chiave e le considerazioni da fare durante la mappatura dei dati sull’esperienza del cliente su XDM.

## Introduzione

Prima di leggere questa guida, controlla [Panoramica del sistema XDM](../home.md) per un&#39;introduzione di alto livello a XDM e al suo ruolo nell&#39;Experience Platform.

Poiché questa guida si concentra esclusivamente su considerazioni chiave relative alla progettazione dello schema, si consiglia vivamente di leggere le [nozioni di base sulla composizione dello schema](./composition.md) per le spiegazioni dettagliate dei singoli elementi dello schema menzionati in questa guida.

## Riepilogo delle best practice {#summary}

L’approccio consigliato per la progettazione del modello dati da utilizzare in Experience Platform può essere riassunto come segue:

1. Comprendi i casi d’uso aziendali per i tuoi dati.
1. Identifica le origini di dati primarie da inserire in Platform per affrontare tali casi d’uso.
1. Identifica eventuali fonti di dati secondari che potrebbero essere di interesse. Ad esempio, se attualmente solo una business unit dell’organizzazione è interessata a trasferire i propri dati su Platform, anche una simile business unit potrebbe essere interessata a trasferire dati simili in futuro. L’analisi di queste origini secondarie consente di standardizzare il modello dati dell’intera organizzazione.
1. Creare un diagramma di relazione tra entità (ERD) di alto livello per le origini dati identificate.
1. Converti l’ERD di alto livello in ERD incentrato sulla piattaforma (inclusi profili, eventi di esperienza ed entità di ricerca).

I passaggi relativi all’identificazione delle origini dati applicabili necessari per eseguire i casi di utilizzo aziendali variano da organizzazione a organizzazione. Mentre il resto delle sezioni di questo documento si concentrano sugli ultimi passaggi dell’organizzazione e della costruzione di un’ERD dopo l’identificazione delle sorgenti di dati, le spiegazioni dei vari componenti del diagramma possono orientare le decisioni su quali delle sorgenti di dati migrare a Platform.

## Creare un ERD di alto livello {#create-an-erd}

Dopo aver determinato le origini dati da inserire in Platform, crea un ERD di alto livello per guidare il processo di mappatura dei dati sugli schemi XDM.

L’esempio seguente rappresenta un’ERD semplificata per un’azienda che desidera inserire dati in Platform. Il diagramma evidenzia le entità essenziali che devono essere ordinate in classi XDM, inclusi account cliente, hotel e diversi eventi di e-commerce comuni.

![Diagramma relazionale di entità che evidenzia le entità essenziali da ordinare in classi XDM per l&#39;acquisizione dei dati.](../images/best-practices/erd.png)

## Ordinare le entità in categorie di profili, ricerche ed eventi {#sort-entities}

Dopo aver creato un’ERD per identificare le entità essenziali da inserire in Platform, queste entità devono essere ordinate in categorie di profilo, ricerca ed eventi:

| Categoria | Descrizione |
| --- | --- |
| Entità profilo | Le entità profilo rappresentano attributi relativi a una singola persona, in genere un cliente. Le entità che rientrano in questa categoria devono essere rappresentate da schemi basati sulla classe **[!DNL XDM Individual Profile]**. |
| Entità di ricerca | Le entità di ricerca rappresentano concetti che possono essere correlati a una singola persona, ma non possono essere utilizzati direttamente per identificare l’individuo. Le entità che rientrano in questa categoria devono essere rappresentate da schemi basati su **classi personalizzate** e sono collegate a profili ed eventi tramite [relazioni tra schemi](../tutorials/relationship-ui.md). |
| Entità evento | Le entità evento rappresentano concetti relativi alle azioni che un cliente può intraprendere, agli eventi di sistema o a qualsiasi altro concetto in cui è possibile tenere traccia delle modifiche nel tempo. Le entità che rientrano in questa categoria devono essere rappresentate da schemi basati sulla classe **[!DNL XDM ExperienceEvent]**. |

{style="table-layout:auto"}

### Considerazioni sull’ordinamento delle entità {#considerations}

Le sezioni seguenti forniscono ulteriori indicazioni su come ordinare le entità in base alle categorie sopra indicate.

#### Dati mutabili e immutabili {#mutable-and-immutable-data}

Un modo principale di ordinare tra le categorie di entità consiste nel determinare se i dati acquisiti sono mutabili o meno.

Gli attributi appartenenti a profili o entità di ricerca sono in genere mutabili. Ad esempio, le preferenze di un cliente potrebbero cambiare nel tempo e i parametri di un piano di abbonamento possono essere aggiornati a seconda delle tendenze di mercato.

Al contrario, i dati dell’evento sono in genere immutabili. Poiché gli eventi sono associati a una marca temporale specifica, lo &quot;snapshot di sistema&quot; fornito da un evento non cambia. Ad esempio, un evento può acquisire le preferenze di un cliente durante il pagamento di un carrello e non cambia anche se le preferenze del cliente finiscono per cambiare in un secondo momento. I dati evento non possono essere modificati dopo la registrazione.

Per riepilogare, i profili e le entità di ricerca contengono attributi mutabili e rappresentano le informazioni più recenti sui soggetti che acquisiscono, mentre gli eventi sono record immutabili del sistema in un momento specifico.

#### Attributi del cliente {#customer-attributes}

Se un’entità contiene attributi relativi a un singolo cliente, è molto probabilmente un’entità profilo. Esempi di attributi del cliente includono:

* Dettagli personali come nome, data di nascita, genere e ID account.
* Informazioni sulla posizione come indirizzi e informazioni GPS.
* Informazioni di contatto come numeri di telefono e indirizzi e-mail.

#### Tracciamento dei dati nel tempo {#track-data}

Se desideri analizzare il modo in cui determinati attributi all’interno di un’entità cambiano nel tempo, è molto probabile che si tratti di un’entità evento. Ad esempio, l’aggiunta di elementi di prodotto a un carrello può essere tracciata come evento aggiuntivo al carrello in Platform:

| ID cliente | Tipo | ID prodotto | Quantità | Timestamp |
| --- | --- | --- | --- | --- |
| 1234567 | Add | 275098 | 2 | 1 ott 10:32 |
| 1234567 | Rimuovi | 275098 | 1 | 1 ott 10:33 |
| 1234567 | Add | 486502 | 1 | 1 ott 10:41 |
| 1234567 | Add | 910482 | 5 | 3 ottobre, 14:15 |

{style="table-layout:auto"}

#### Casi di utilizzo della segmentazione {#segmentation-use-cases}

Quando categorizzi le entità, è importante considerare i tipi di pubblico che puoi creare per affrontare casi d’uso aziendali specifici.

Ad esempio, un’azienda vuole conoscere tutti i membri &quot;Gold&quot; o &quot;Platinum&quot; del proprio programma fedeltà che hanno effettuato più di cinque acquisti nell’ultimo anno. In base a questa logica di segmentazione, è possibile trarre le seguenti conclusioni in merito a come dovrebbero essere rappresentate le entità rilevanti:

* &quot;Gold&quot; e &quot;Platinum&quot; rappresentano gli stati di fedeltà applicabili a un singolo cliente. Poiché la logica di segmentazione riguarda solo lo stato di fedeltà corrente dei clienti, questi dati possono essere modellati come parte di uno schema di profilo. Se desideri tenere traccia delle modifiche allo stato di fedeltà nel tempo, puoi anche creare uno schema di evento aggiuntivo per le modifiche allo stato di fedeltà.
* Gli acquisti sono eventi che si verificano in un determinato momento e la logica di segmentazione riguarda gli eventi di acquisto entro un intervallo di tempo specificato. Questi dati devono quindi essere modellati come schema di eventi.

#### Casi di utilizzo dell’attivazione {#activation-use-cases}

Oltre alle considerazioni relative ai casi di utilizzo della segmentazione, è necessario esaminare i casi di utilizzo dell’attivazione per tali tipi di pubblico per identificare attributi rilevanti aggiuntivi.

Ad esempio, un&#39;azienda ha creato un pubblico in base alla regola che `country = US`. Quindi, quando attiva il pubblico su determinati target a valle, l’azienda vuole filtrare tutti i profili esportati in base allo stato dell’abitazione. Pertanto, un attributo `state` deve essere acquisito anche nell&#39;entità profilo applicabile.

#### Valori aggregati {#aggregated-values}

In base al caso d’uso e alla granularità dei dati, è necessario decidere se alcuni valori devono essere preaggregati prima di essere inclusi in un profilo o in un’entità evento.

Ad esempio, un’azienda desidera creare un pubblico in base al numero di acquisti effettuati nel carrello. Puoi scegliere di incorporare questi dati con la granularità più bassa includendo ogni evento di acquisto con marca temporale come propria entità. Tuttavia, a volte questo può aumentare esponenzialmente il numero di eventi registrati. Per ridurre il numero di eventi acquisiti, puoi scegliere di creare un valore aggregato `numberOfPurchases` per un periodo di una settimana o di un mese. Altre funzioni di aggregazione come MIN e MAX possono essere applicate a queste situazioni.

>[!CAUTION]
>
>Experience Platform al momento non esegue l’aggregazione automatica dei valori, anche se questa operazione è pianificata per le versioni future. Se scegli di utilizzare valori aggregati, devi eseguire i calcoli esternamente prima di inviare i dati a Platform.

#### Cardinalità {#cardinality}

Le cardinalità stabilite nella ERD possono anche fornire alcuni indizi su come categorizzare le entità. Se esiste una relazione uno-a-molti tra due entità, è probabile che l’entità che rappresenta il &quot;molti&quot; sia un’entità evento. Tuttavia, ci sono anche casi in cui &quot;molti&quot; è un set di entità di ricerca che vengono fornite come array all’interno di un’entità profilo.

>[!NOTE]
>
>Poiché non esiste un approccio universale per adattarsi a tutti i casi d’uso, è importante considerare i pro e i contro di ogni situazione quando si categorizzano le entità in base alla cardinalità. Per ulteriori informazioni, consulta la [sezione successiva](#pros-and-cons).

La tabella seguente illustra alcune relazioni di entità comuni e le categorie che possono essere derivate da esse:

| Relazione | Cardinalità | Categorie di entità |
| --- | --- | --- |
| Pagamento cliente e carrello | Da uno a molti | Un singolo cliente può avere molti checkout nel carrello, che sono eventi che possono essere tracciati nel tempo. Il cliente sarà quindi un’entità profilo, mentre Cart Checkout sarà un’entità evento. |
| Account cliente e fedeltà | Uno a uno | Un singolo cliente può avere un solo account fedeltà e un account fedeltà può appartenere a un solo cliente. Poiché la relazione è uno a uno, sia l&#39;account cliente che l&#39;account fedeltà rappresentano entità profilo. |
| Cliente e abbonamento | Da uno a molti | Un singolo cliente può avere molti abbonamenti. Poiché l’azienda si occupa solo degli abbonamenti correnti di un cliente, il cliente è un’entità profilo, mentre l’abbonamento è un’entità ricerca. |

{style="table-layout:auto"}

### Pro e contro di diverse classi di entità {#pros-and-cons}

Sebbene la sezione precedente abbia fornito alcune linee guida generali per decidere come categorizzare le entità, è importante comprendere che spesso ci possono essere pro e contro nella scelta di una categoria di entità rispetto a un’altra. Il seguente caso di studio ha lo scopo di illustrare come considerare le opzioni in queste situazioni.

Un’azienda tiene traccia degli abbonamenti attivi per i propri clienti, dove un cliente può avere molti abbonamenti. L’azienda desidera inoltre includere gli abbonamenti per i casi di utilizzo della segmentazione, ad esempio per trovare tutti gli utenti con abbonamenti attivi.

In questo scenario, l’azienda ha due potenziali opzioni per rappresentare gli abbonamenti di un cliente nel suo modello di dati:

1. [Utilizzare gli attributi del profilo](#profile-approach)
1. [Utilizzare le entità evento](#event-approach)

#### Approccio 1: utilizzare gli attributi del profilo {#profile-approach}

Il primo approccio consiste nell&#39;includere un array di `subscriptionID` all&#39;interno dell&#39;entità profilo per il cliente.

![Schema cliente nell&#39;Editor schema con la classe e la struttura evidenziate](../images/best-practices/profile-schema.png)

**Pro**

* La segmentazione è fattibile per il caso d’uso previsto.
* Lo schema mantiene solo i record di abbonamento più recenti per un cliente.

**Contro**

* L’intero array deve essere ridefinito ogni volta che si verificano modifiche a qualsiasi campo dell’array.
* Se diverse origini dati o unità aziendali inseriscono dati nell&#39;array, diventa difficile mantenere sincronizzato l&#39;array aggiornato più recente su tutti i canali.

#### Approccio 2: utilizzare entità evento {#event-approach}

Il secondo approccio consiste nell’utilizzare gli schemi di evento per rappresentare un evento di abbonamento. Questo includerebbe l’ID abbonamento insieme a un ID cliente e una marca temporale di quando si è verificato l’evento di abbonamento.

![Diagramma dello schema Evento di sottoscrizione con la classe XDM Experience Event e la struttura delle sottoscrizioni evidenziate.](../images/best-practices/event-schema.png)

**Pro**

* Le regole di segmentazione possono essere più flessibili (ad esempio, trovare tutti i clienti che hanno modificato i loro abbonamenti negli ultimi 30 giorni).
* Quando lo stato di abbonamento di un cliente cambia, non è più necessario aggiornare un array lungo e potenzialmente complesso all’interno degli attributi di profilo del cliente. Questa funzione è particolarmente utile se si verificano modifiche simultanee all’elenco di abbonamento del cliente da più sorgenti.

**Contro**

* La segmentazione diventa più complessa per il caso d’uso originale (identificando lo stato degli abbonamenti più recenti dei clienti). Il pubblico ora ha bisogno di una logica aggiuntiva per contrassegnare l’ultimo evento di abbonamento affinché un cliente possa verificarne lo stato.
* Gli eventi hanno un rischio maggiore di scadere automaticamente ed essere eliminati dall’archivio dei profili. Per ulteriori informazioni, consulta la guida su [Scadenze evento esperienza](../../profile/event-expirations.md).

## Creare schemi in base alle entità categorizzate {#schemas-for-categorized-entities}

Dopo aver ordinato le entità in categorie di profilo, ricerca ed eventi, puoi iniziare a convertire il modello dati in schemi XDM. A scopo dimostrativo, il modello dati di esempio mostrato in precedenza è stato suddiviso nelle categorie appropriate nel diagramma seguente:

![Diagramma degli schemi contenuti nelle entità profilo, ricerca ed evento](../images/best-practices/erd-sorted.png)

La categoria in cui è stato ordinato un’entità deve determinare la classe XDM su cui si basa il relativo schema. Per ribadire:

* Le entità profilo devono utilizzare la classe [!DNL XDM Individual Profile].
* Le entità evento devono utilizzare la classe [!DNL XDM ExperienceEvent].
* Le entità di ricerca devono utilizzare classi XDM personalizzate definite dall’organizzazione. Le entità profilo ed evento possono quindi fare riferimento a tali entità di ricerca attraverso relazioni di schema.

>[!NOTE]
>
>Anche se le entità evento sono quasi sempre rappresentate da schemi separati, le entità nelle categorie di profilo o di ricerca possono essere combinate insieme in un singolo schema XDM, a seconda della loro cardinalità.
>
>Ad esempio, poiché l&#39;entità cliente ha una relazione uno-a-uno con l&#39;entità LoyaltyAccount, lo schema per l&#39;entità cliente potrebbe includere anche un oggetto `LoyaltyAccount` per contenere i campi fedeltà appropriati per ogni cliente. Se la relazione è uno a molti, tuttavia, l’entità che rappresenta il &quot;molti&quot; potrebbe essere rappresentata da uno schema separato o da un array di attributi di profilo, a seconda della complessità.

Le sezioni seguenti forniscono indicazioni generali sulla creazione di schemi basati sulla ERD.

### Adottare un approccio di modellazione iterativa {#iterative-modeling}

Le [regole dell&#39;evoluzione dello schema](./composition.md#evolution) prevedono che solo le modifiche non distruttive possano essere apportate agli schemi una volta implementati. In altre parole, una volta aggiunto un campo a uno schema e i dati sono stati acquisiti in base a tale campo, il campo non può più essere rimosso. È quindi essenziale adottare un approccio di modellazione iterativa quando si creano per la prima volta gli schemi, a partire da un’implementazione semplificata che aumenta progressivamente la complessità nel tempo.

Se non sei sicuro se un particolare campo sia necessario da includere in uno schema, la best practice consiste nell’escludere tale campo. Se in seguito viene stabilito che il campo è necessario, può sempre essere aggiunto nella successiva iterazione dello schema.

### Campi di identità {#identity-fields}

Ad Experience Platform, i campi XDM contrassegnati come identità vengono utilizzati per unire informazioni su singoli clienti provenienti da più origini dati. Anche se uno schema può avere più campi contrassegnati come identità, è necessario definire una singola identità primaria affinché lo schema possa essere abilitato per l&#39;utilizzo in [!DNL Real-Time Customer Profile]. Per informazioni più dettagliate sul caso d&#39;uso di questi campi, consulta la sezione sui [campi di identità](./composition.md#identity) nelle nozioni di base sulla composizione dello schema.

Durante la progettazione degli schemi, eventuali chiavi primarie nelle tabelle del database relazionale sono probabilmente candidate per le identità primarie. Altri esempi di campi di identità applicabili sono gli indirizzi e-mail dei clienti, i numeri di telefono, gli ID account e [ECID](../../identity-service/features/ecid.md).

### Adobe di gruppi di campi dello schema dell’applicazione {#adobe-application-schema-field-groups}

L’Experience Platform fornisce diversi gruppi di campi di schema XDM predefiniti per l’acquisizione di dati relativi alle seguenti applicazioni Adobe:

* Adobe Analytics
* Adobe Audience Manager
* Adobe Campaign
* Adobe Target

Ad esempio, puoi utilizzare il gruppo di campi ](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json) del modello [[!UICONTROL Adobe Analytics ExperienceEvent] per mappare campi specifici di [!DNL Analytics] agli schemi XDM. A seconda delle applicazioni di Adobe che utilizzi, nei tuoi schemi dovresti utilizzare i gruppi di campi forniti dall’Adobe.

![Un diagramma schema del [!UICONTROL modello Adobe Analytics ExperienceEvent].](../images/best-practices/analytics-field-group.png)

I gruppi di campi dell&#39;applicazione Adobe assegnano automaticamente un&#39;identità primaria predefinita tramite l&#39;utilizzo del campo `identityMap`, che è un oggetto generato dal sistema e di sola lettura che mappa i valori di identità standard per un singolo cliente.

Per Adobe Analytics, ECID è l’identità primaria predefinita. Se un valore ECID non viene fornito da un cliente, l’identità primaria utilizza per impostazione predefinita AAID.

>[!IMPORTANT]
>
>Quando si utilizzano i gruppi di campi dell’applicazione Adobe, nessun altro campo deve essere contrassegnato come identità primaria. Se esistono proprietà aggiuntive che devono essere contrassegnate come identità, questi campi devono essere assegnati come identità secondarie.

## Campi di convalida dei dati {#data-validation-fields}

Quando si acquisiscono i dati nel data lake, la convalida dei dati viene applicata solo per i campi vincolati. Per convalidare un particolare campo durante un’acquisizione batch, è necessario contrassegnare il campo come vincolato nello schema XDM. Per evitare che dati errati vengano acquisiti in Platform, ti consigliamo di definire i criteri per la convalida a livello di campo quando crei gli schemi.

>[!IMPORTANT]
>
>La convalida non viene applicata alle colonne nidificate. Se il formato del campo si trova all’interno di una colonna array, i dati non verranno convalidati.

Per impostare vincoli per un campo specifico, selezionare il campo dall&#39;Editor schema per aprire la barra laterale **[!UICONTROL Proprietà campo]**. Per una descrizione esatta dei campi disponibili, consulta la documentazione sulle [proprietà dei campi specifiche per tipo](../ui/fields/overview.md#type-specific-properties).

![Editor schema con campi vincolo evidenziati nella barra laterale [!UICONTROL Proprietà campo].](../images/best-practices/data-validation-fields.png)

### Suggerimenti per mantenere l&#39;integrità dei dati {#data-integrity-tips}

Di seguito è riportata una raccolta di suggerimenti per mantenere l&#39;integrità dei dati durante la creazione di uno schema.

* **Considera le identità primarie**: per Adobe come Web SDK, Mobile SDK, Adobe Analytics e Adobe Journey Optimizer, il campo `identityMap` spesso funge da identità primaria. Evita di designare campi aggiuntivi come identità primarie per tale schema.
* **Assicurarsi che `_id` non sia utilizzato come identità**: il campo `_id` negli schemi Experience Event non può essere utilizzato come identità in quanto è destinato all&#39;univocità dei record.
* **Imposta vincoli di lunghezza**: è consigliabile impostare lunghezze minime e massime nei campi contrassegnati come identità. Un avviso viene attivato se si tenta di assegnare uno spazio dei nomi personalizzato a un campo di identità senza soddisfare i vincoli di lunghezza minima e massima. Queste limitazioni contribuiscono a mantenere la coerenza e la qualità dei dati.
* **Applica pattern per valori coerenti**: se i valori di identità seguono un pattern specifico, è necessario utilizzare l&#39;impostazione **[!UICONTROL Pattern]** per applicare questo vincolo. Questa impostazione può includere solo regole come cifre, lettere maiuscole o minuscole o combinazioni di caratteri specifiche. Utilizza espressioni regolari per far corrispondere i pattern nelle stringhe.
* **Limita le eVar negli schemi di Analytics**: in genere, uno schema di Analytics deve avere un solo eVar designato come identità. Se intendi utilizzare più di un eVar come identità, devi verificare nuovamente se la struttura dati può essere ottimizzata.
* **Assicurare l&#39;univocità di un campo selezionato**: il campo scelto deve essere univoco rispetto all&#39;identità primaria nello schema. In caso contrario, non contrassegnarlo come identità. Ad esempio, se più clienti possono fornire lo stesso indirizzo e-mail, lo spazio dei nomi non è un’identità adatta. Questo principio si applica anche ad altri spazi dei nomi di identità come i numeri di telefono. Se si contrassegna un campo non univoco come identità, si potrebbe verificare una compressione indesiderata del profilo.
* **Verifica lunghezza minima stringa**: tutti i campi stringa devono contenere almeno un carattere, poiché i valori stringa non devono mai essere vuoti. I valori Null per i campi non obbligatori, tuttavia, sono accettabili.

## Passaggi successivi

Questo documento illustra le linee guida generali e le best practice per la progettazione del modello dati, ad Experience Platform. Per riepilogare:

* Prima di creare gli schemi, utilizza un approccio discendente che consiste nell’ordinare le tabelle di dati in categorie di profilo, ricerca ed eventi.
* Spesso esistono diversi approcci e opzioni per la progettazione di schemi per scopi diversi.
* Il modello dati deve supportare i casi di utilizzo aziendali, ad esempio la segmentazione o l’analisi del percorso di clienti.
* Rendi gli schemi il più semplici possibile e aggiungi nuovi campi solo se assolutamente necessario.

Quando sei pronto, consulta l&#39;esercitazione su [creazione di uno schema nell&#39;interfaccia utente](../tutorials/create-schema-ui.md) per istruzioni dettagliate su come creare uno schema, assegnare la classe appropriata per l&#39;entità e aggiungere campi a cui mappare i dati.
