---
keywords: Experience Platform;home;argomenti popolari;schema;schema;enum;identità primaria;identità primaria;profilo individuale XDM;evento esperienza;XDM Experience Event;XDM ExperienceEvent;experienceEvent;experienceevent;XDM Experienceevenet;progettazione schema;best practice
solution: Experience Platform
title: Best Practice Per La Modellazione Dei Dati
description: Questo documento fornisce un’introduzione agli schemi Experience Data Model (XDM) e ai blocchi predefiniti, ai principi e alle best practice per la composizione degli schemi da utilizzare in Adobe Experience Platform.
exl-id: 2455a04e-d589-49b2-a3cb-abb5c0b4e42f
source-git-commit: b82bbdf7957e5a8d331d61f02293efdaf878971c
workflow-type: tm+mt
source-wordcount: '3096'
ht-degree: 1%

---

# Best practice per la modellazione dei dati

[!DNL Experience Data Model] (XDM) è il framework principale che standardizza i dati sull’esperienza del cliente, fornendo strutture e definizioni comuni da utilizzare nei servizi Adobe Experience Platform a valle. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune e utilizzati per ottenere informazioni preziose dalle azioni dei clienti, definire il pubblico dei clienti ed esprimere gli attributi dei clienti a scopo di personalizzazione.

Poiché XDM è estremamente versatile e personalizzabile dalla progettazione, è importante seguire le best practice per la modellazione dei dati durante la progettazione degli schemi. Questo documento descrive le decisioni chiave e le considerazioni da fare durante la mappatura dei dati sull’esperienza del cliente su XDM.

## Introduzione

Prima di leggere questa guida, controlla [Panoramica del sistema XDM](../home.md) per un’introduzione di alto livello a XDM e al suo ruolo all’interno di Experienci Platform.

Poiché questa guida si concentra esclusivamente su considerazioni chiave relative alla progettazione dello schema, si consiglia vivamente di leggere la [nozioni di base sulla composizione dello schema](./composition.md) per una spiegazione dettagliata dei singoli elementi dello schema menzionati in questa guida.

## Riepilogo delle best practice {#summary}

L’approccio consigliato per la progettazione del modello dati da utilizzare in Experienci Platform può essere riassunto come segue:

1. Comprendi i casi d’uso aziendali per i tuoi dati.
1. Identifica le origini dati primarie da inserire in [!DNL Platform] per risolvere tali casi d’uso.
1. Identifica eventuali fonti di dati secondari che potrebbero essere di interesse. Ad esempio, se attualmente solo una business unit dell’organizzazione è interessata a trasferire i propri dati in [!DNL Platform]Tuttavia, una business unit simile potrebbe essere interessata in futuro anche alla portabilità di dati simili. L’analisi di queste origini secondarie consente di standardizzare il modello dati dell’intera organizzazione.
1. Creare un diagramma di relazione tra entità (ERD) di alto livello per le origini dati identificate.
1. Conversione di ERD di alto livello in un [!DNL Platform]ERD incentrato su (inclusi profili, eventi esperienza ed entità di ricerca).

I passaggi relativi all’identificazione delle origini dati applicabili necessari per eseguire i casi di utilizzo aziendali variano da organizzazione a organizzazione. Mentre il resto delle sezioni di questo documento si concentrano sugli ultimi passaggi di organizzazione e costruzione di un ERD dopo l&#39;identificazione delle origini dati, le spiegazioni dei vari componenti del diagramma possono orientare le decisioni su quali delle origini dati migrare [!DNL Platform].

## Creare un ERD di alto livello {#create-an-erd}

Una volta determinate le origini dati da inserire in [!DNL Platform], crea un ERD di alto livello per guidare il processo di mappatura dei dati sugli schemi XDM.

L’esempio seguente rappresenta un’ERD semplificata per un’azienda che desidera inserire dati in [!DNL Platform]. Il diagramma evidenzia le entità essenziali che devono essere ordinate in classi XDM, inclusi account cliente, hotel, indirizzi e diversi eventi di e-commerce comuni.

![Un diagramma relazionale di entità che evidenzia le entità essenziali da ordinare in classi XDM per l’acquisizione dei dati.](../images/best-practices/erd.png)

## Ordinare le entità in categorie di profili, ricerche ed eventi {#sort-entities}

Dopo aver creato un ERD per identificare le entità essenziali da inserire in [!DNL Platform], queste entità devono essere ordinate in categorie di profilo, ricerca ed eventi:

| Categoria | Descrizione |
| --- | --- |
| Entità profilo | Le entità profilo rappresentano attributi relativi a una singola persona, in genere un cliente. Le entità che rientrano in questa categoria devono essere rappresentate da schemi basati su **[!DNL XDM Individual Profile]classe**. |
| Entità di ricerca | Le entità di ricerca rappresentano concetti che possono essere correlati a una singola persona, ma non possono essere utilizzati direttamente per identificare l’individuo. Le entità che rientrano in questa categoria devono essere rappresentate da schemi basati su **classi personalizzate** e sono collegati a profili ed eventi tramite [relazioni tra schemi](../tutorials/relationship-ui.md). |
| Entità evento | Le entità evento rappresentano concetti relativi alle azioni che un cliente può intraprendere, agli eventi di sistema o a qualsiasi altro concetto in cui è possibile tenere traccia delle modifiche nel tempo. Le entità che rientrano in questa categoria devono essere rappresentate da schemi basati su **[!DNL XDM ExperienceEvent]classe**. |

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

Se desideri analizzare il modo in cui determinati attributi all’interno di un’entità cambiano nel tempo, è molto probabile che si tratti di un’entità evento. Ad esempio, l’aggiunta di elementi di prodotto a un carrello può essere tracciata come evento aggiuntivo al carrello in [!DNL Platform]:

| Customer ID | Tipo | ID prodotto | Quantità | Marca temporale |
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

Ad esempio, un’azienda ha creato un pubblico in base alla regola che `country = US`. Quindi, quando attiva il pubblico su determinati target a valle, l’azienda vuole filtrare tutti i profili esportati in base allo stato dell’abitazione. Pertanto, un `state` L&#39;attributo deve essere acquisito anche nell&#39;entità profilo applicabile.

#### Valori aggregati {#aggregated-values}

In base al caso d’uso e alla granularità dei dati, è necessario decidere se alcuni valori devono essere preaggregati prima di essere inclusi in un profilo o in un’entità evento.

Ad esempio, un’azienda desidera creare un pubblico in base al numero di acquisti effettuati nel carrello. Puoi scegliere di incorporare questi dati con la granularità più bassa includendo ogni evento di acquisto con marca temporale come propria entità. Tuttavia, a volte questo può aumentare esponenzialmente il numero di eventi registrati. Per ridurre il numero di eventi acquisiti, puoi creare un valore aggregato `numberOfPurchases` in un periodo di una settimana o di un mese. Altre funzioni di aggregazione come MIN e MAX possono essere applicate a queste situazioni.

>[!CAUTION]
>
>Experienci Platform al momento non esegue l’aggregazione automatica dei valori, anche se questa operazione è pianificata per le versioni future. Se si sceglie di utilizzare valori aggregati, è necessario eseguire i calcoli esternamente prima di inviare i dati a [!DNL Platform].

#### Cardinalità {#cardinality}

Le cardinalità stabilite nella ERD possono anche fornire alcuni indizi su come categorizzare le entità. Se esiste una relazione uno-a-molti tra due entità, è probabile che l’entità che rappresenta il &quot;molti&quot; sia un’entità evento. Tuttavia, ci sono anche casi in cui &quot;molti&quot; è un set di entità di ricerca che vengono fornite come array all’interno di un’entità profilo.

>[!NOTE]
>
>Poiché non esiste un approccio universale per adattarsi a tutti i casi d’uso, è importante considerare i pro e i contro di ogni situazione quando si categorizzano le entità in base alla cardinalità. Consulta la [sezione successiva](#pros-and-cons) per ulteriori informazioni.

La tabella seguente illustra alcune relazioni di entità comuni e le categorie che possono essere derivate da esse:

| Relazione | Cardinalità | Categorie di entità |
| --- | --- | --- |
| Clienti e carrello Pagamenti | Da uno a molti | Un singolo cliente può avere molti checkout nel carrello, che sono eventi che possono essere tracciati nel tempo. I clienti sarebbero quindi un’entità profilo, mentre Cart Checkouts sarebbe un’entità evento. |
| Clienti e account fedeltà | Uno a uno | Un singolo cliente può avere un solo account fedeltà e un account fedeltà può appartenere a un solo cliente. Poiché la relazione è uno a uno, sia Clienti che Conti fedeltà rappresentano entità profilo. |
| Clienti e abbonamenti | Da uno a molti | Un singolo cliente può avere molti abbonamenti. Poiché l’azienda si occupa solo degli abbonamenti correnti di un cliente, Clienti è un’entità profilo, mentre Abbonamenti è un’entità ricerca. |

{style="table-layout:auto"}

### Pro e contro di diverse classi di entità {#pros-and-cons}

Sebbene la sezione precedente abbia fornito alcune linee guida generali per decidere come categorizzare le entità, è importante comprendere che spesso ci possono essere pro e contro nella scelta di una categoria di entità rispetto a un’altra. Il seguente caso di studio ha lo scopo di illustrare come considerare le opzioni in queste situazioni.

Un’azienda tiene traccia degli abbonamenti attivi per i propri clienti, dove un cliente può avere molti abbonamenti. L’azienda desidera inoltre includere gli abbonamenti per i casi di utilizzo della segmentazione, ad esempio per trovare tutti gli utenti con abbonamenti attivi.

In questo scenario, l’azienda ha due potenziali opzioni per rappresentare gli abbonamenti di un cliente nel suo modello di dati:

1. [Utilizzare gli attributi del profilo](#profile-approach)
1. [Utilizzare le entità evento](#event-approach)

#### Approccio 1: utilizzare gli attributi del profilo {#profile-approach}

Il primo approccio consiste nell’includere un array di abbonamenti come attributi all’interno dell’entità profilo per i clienti. Gli oggetti in questa matrice conterrebbero campi per `category`, `status`, `planName`, `startDate`, e `endDate`.

![Lo schema Clienti nell’Editor di schema con la classe e la struttura evidenziate](../images/best-practices/profile-schema.png)

**Pro**

* La segmentazione è fattibile per il caso d’uso previsto.
* Lo schema mantiene solo i record di abbonamento più recenti per un cliente.

**Contro**

* L’intero array deve essere ridefinito ogni volta che si verificano modifiche a qualsiasi campo dell’array.
* Se diverse origini dati o unità aziendali inseriscono dati nell&#39;array, diventa difficile mantenere sincronizzato l&#39;array aggiornato più recente su tutti i canali.

#### Approccio 2: utilizzare entità evento {#event-approach}

Il secondo approccio consiste nell’utilizzare gli schemi evento per rappresentare gli abbonamenti. Ciò comporta l’acquisizione degli stessi campi di abbonamento del primo approccio, con l’aggiunta di un ID di abbonamento, un ID cliente e una marca temporale indicante quando si è verificato l’evento di abbonamento.

![Un diagramma dello schema Eventi di abbonamento con la classe XDM Experience Event e la struttura delle sottoscrizioni evidenziate.](../images/best-practices/event-schema.png)

**Pro**

* Le regole di segmentazione possono essere più flessibili (ad esempio, trovare tutti i clienti che hanno modificato i loro abbonamenti negli ultimi 30 giorni).
* Quando lo stato di abbonamento di un cliente cambia, non è più necessario aggiornare un array lungo e potenzialmente complesso all’interno degli attributi di profilo del cliente. Questa funzione è particolarmente utile se si verificano modifiche simultanee all’elenco di abbonamento del cliente da più sorgenti.

**Contro**

* La segmentazione diventa più complessa per il caso d’uso originale (identificando lo stato degli abbonamenti più recenti dei clienti). Il pubblico ora ha bisogno di una logica aggiuntiva per contrassegnare l’ultimo evento di abbonamento affinché un cliente possa verificarne lo stato.
* Gli eventi hanno un rischio maggiore di scadere automaticamente ed essere eliminati dall’archivio dei profili. Consulta la guida su [Scadenze degli eventi esperienza](../../profile/event-expirations.md) per ulteriori informazioni.

## Creare schemi in base alle entità categorizzate {#schemas-for-categorized-entities}

Dopo aver ordinato le entità in categorie di profilo, ricerca ed eventi, puoi iniziare a convertire il modello dati in schemi XDM. A scopo dimostrativo, il modello dati di esempio mostrato in precedenza è stato suddiviso nelle categorie appropriate nel diagramma seguente:

![Un diagramma degli schemi contenuti nelle entità profilo, ricerca ed evento](../images/best-practices/erd-sorted.png)

La categoria in cui è stato ordinato un’entità deve determinare la classe XDM su cui si basa il relativo schema. Per ribadire:

* Le entità profilo devono utilizzare [!DNL XDM Individual Profile] classe.
* Le entità evento devono utilizzare [!DNL XDM ExperienceEvent] classe.
* Le entità di ricerca devono utilizzare classi XDM personalizzate definite dall’organizzazione. Le entità profilo ed evento possono quindi fare riferimento a tali entità di ricerca attraverso relazioni di schema.

>[!NOTE]
>
>Anche se le entità evento sono quasi sempre rappresentate da schemi separati, le entità nelle categorie di profilo o di ricerca possono essere combinate insieme in un singolo schema XDM, a seconda della loro cardinalità.
>
>Ad esempio, poiché l&#39;entità Clienti ha una relazione uno-a-uno con l&#39;entità Conti fedeltà, lo schema per l&#39;entità Clienti potrebbe includere anche un `LoyaltyAccount` per contenere i campi fedeltà appropriati per ciascun cliente. Se la relazione è uno a molti, tuttavia, l’entità che rappresenta il &quot;molti&quot; potrebbe essere rappresentata da uno schema separato o da un array di attributi di profilo, a seconda della complessità.

Le sezioni seguenti forniscono indicazioni generali sulla creazione di schemi basati sulla ERD.

### Adottare un approccio di modellazione iterativa {#iterative-modeling}

Il [regole di evoluzione dello schema](./composition.md#evolution) Stabiliscono che solo le modifiche non distruttive possono essere apportate agli schemi una volta implementati. In altre parole, una volta aggiunto un campo a uno schema e i dati sono stati acquisiti in base a tale campo, il campo non può più essere rimosso. È quindi essenziale adottare un approccio di modellazione iterativa quando si creano per la prima volta gli schemi, a partire da un’implementazione semplificata che aumenta progressivamente la complessità nel tempo.

Se non sei sicuro se un particolare campo sia necessario da includere in uno schema, la best practice consiste nell’escludere tale campo. Se in seguito viene stabilito che il campo è necessario, può sempre essere aggiunto nella successiva iterazione dello schema.

### Campi di identità {#identity-fields}

Ad Experience Platform, i campi XDM contrassegnati come identità vengono utilizzati per unire informazioni su singoli clienti provenienti da più origini dati. Anche se uno schema può avere più campi contrassegnati come identità, è necessario definire un’unica identità primaria affinché lo schema possa essere abilitato per l’utilizzo in [!DNL Real-Time Customer Profile]. Consulta la sezione su [campi di identità](./composition.md#identity) nelle nozioni di base sulla composizione dello schema, per informazioni più dettagliate sul caso d’uso di questi campi.

Durante la progettazione degli schemi, eventuali chiavi primarie nelle tabelle del database relazionale sono probabilmente candidate per le identità primarie. Altri esempi di campi di identità applicabili sono gli indirizzi e-mail dei clienti, i numeri di telefono, gli ID account e [ECID](../../identity-service/features/ecid.md).

### Adobe di gruppi di campi dello schema dell’applicazione {#adobe-application-schema-field-groups}

L’Experience Platform fornisce diversi gruppi di campi di schema XDM predefiniti per l’acquisizione di dati relativi alle seguenti applicazioni di Adobe:

* Adobe Analytics
* Adobe Audience Manager
* Adobe Campaign
* Adobe Target

Ad esempio, puoi utilizzare [[!UICONTROL Modello Adobe Analytics ExperienceEvent] gruppo di campi](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json) da mappare [!DNL Analytics]campi specifici per gli schemi XDM. A seconda delle applicazioni di Adobe con cui stai lavorando, dovresti utilizzare questi gruppi di campi forniti dall’Adobe nei tuoi schemi.

![Un diagramma di schema del [!UICONTROL Modello Adobe Analytics ExperienceEvent].](../images/best-practices/analytics-field-group.png)

Adobe di gruppi di campi dell’applicazione che assegnano automaticamente un’identità primaria predefinita tramite l’utilizzo di `identityMap` è un oggetto generato dal sistema e di sola lettura che mappa i valori di identità standard per un singolo cliente.

Per Adobe Analytics, ECID è l’identità primaria predefinita. Se un valore ECID non viene fornito da un cliente, l’identità primaria utilizza per impostazione predefinita AAID.

>[!IMPORTANT]
>
>Quando si utilizzano i gruppi di campi dell’applicazione Adobe, nessun altro campo deve essere contrassegnato come identità primaria. Se esistono proprietà aggiuntive che devono essere contrassegnate come identità, questi campi devono essere assegnati come identità secondarie.

## Campi di convalida dei dati {#data-validation-fields}

Per evitare che dati errati vengano acquisiti in Platform, ti consigliamo di definire i criteri per la convalida a livello di campo durante la creazione degli schemi. Per impostare vincoli per un campo specifico, selezionare il campo dall&#39;Editor schema per aprire [!UICONTROL Proprietà campo] barra laterale. Consulta la documentazione su [proprietà del campo specifiche del tipo](../ui/fields/overview.md#type-specific-properties) per una descrizione esatta dei campi disponibili.

![Editor di schema con i campi vincolo evidenziati nel [!UICONTROL Proprietà campo] barra laterale.](../images/best-practices/data-validation-fields.png)

>[!TIP]
>
>Di seguito è riportata una raccolta di suggerimenti per la modellazione dei dati durante la creazione di uno schema:<br><ul><li>**Considerare le identità primarie**: ad Adobe prodotti come Web SDK, Mobile SDK, Adobe Analytics e Adobe Journey Optimizer, `identityMap` Questo campo spesso funge da identità primaria. Evita di designare campi aggiuntivi come identità primarie per tale schema.</li><li>**Evita di utilizzare `_id` come identità**: evita di utilizzare `_id` negli schemi Experience Event come identità. Ha lo scopo di garantire l&#39;univocità dei record e non di utilizzarli come identità.</li><li>**Imposta vincoli di lunghezza**: è consigliabile impostare lunghezze minime e massime per i campi contrassegnati come identità. Queste limitazioni contribuiscono a mantenere la coerenza e la qualità dei dati.</li><li>**Applicare pattern per valori coerenti**: se i valori di identità seguono un pattern specifico, utilizza [!UICONTROL Pattern] per applicare questo vincolo. Questa impostazione può includere solo regole come cifre, lettere maiuscole o minuscole o combinazioni di caratteri specifiche. Utilizza espressioni regolari per far corrispondere i pattern nelle stringhe.</li><li>**Limitare le eVar nello schema di Analytics**: in genere, uno schema di Analytics deve avere un solo eVar designato come identità. Se intendi utilizzare più di un eVar come identità, devi verificare nuovamente se la struttura dati può essere ottimizzata.</li><li>**Assicurare l&#39;univocità di un campo selezionato**: il campo scelto deve essere univoco rispetto all’identità primaria nello schema. In caso contrario, non contrassegnarlo come identità. Ad esempio, se più clienti possono fornire lo stesso indirizzo e-mail, lo spazio dei nomi non è un’identità adatta. Questo principio si applica anche ad altri spazi dei nomi di identità come i numeri di telefono.</li></ul>

## Passaggi successivi

Questo documento illustra le linee guida generali e le best practice per la progettazione del modello dati, ad Experience Platform. Per riepilogare:

* Prima di creare gli schemi, utilizza un approccio discendente che consiste nell’ordinare le tabelle di dati in categorie di profilo, ricerca ed eventi.
* Spesso esistono diversi approcci e opzioni per la progettazione di schemi per scopi diversi.
* Il modello dati deve supportare i casi di utilizzo aziendali, ad esempio la segmentazione o l’analisi del percorso di clienti.
* Rendi gli schemi il più semplici possibile e aggiungi nuovi campi solo se assolutamente necessario.

Quando sei pronto, consulta l’esercitazione su [creazione di uno schema nell’interfaccia utente](../tutorials/create-schema-ui.md) per istruzioni dettagliate su come creare uno schema, assegna la classe appropriata per l’entità e aggiungi campi a cui mappare i dati.
