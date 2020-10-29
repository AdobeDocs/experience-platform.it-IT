---
keywords: Experience Platform;home;popular topics;schema;Schema;enum;;primary identity;primary identity;XDM individual profile;Experience event;XDM Experience Event;XDM ExperienceEvent;experienceEvent;experienceevent;XDM Experienceevenet;schema design
solution: Experience Platform
title: Best practice per la modellazione dei dati in Adobe Experience Platform
topic: overview
description: Questo documento fornisce un'introduzione agli schemi di Experience Data Model (XDM) e ai blocchi costitutivi, ai principi e alle procedure ottimali per la composizione degli schemi da utilizzare in Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: e15df78978c06da254319d9d394be35c4668caa9
workflow-type: tm+mt
source-wordcount: '2472'
ht-degree: 1%

---


# Best practice per la modellazione dei dati in Adobe Experience Platform

[!DNL Experience Data Model] (XDM) è il framework di base che standardizza i dati relativi all&#39;esperienza dei clienti fornendo strutture e definizioni comuni da utilizzare nei servizi Adobe Experience Platform a valle. Aderendo agli standard XDM, tutti i dati sull&#39;esperienza cliente possono essere incorporati in una rappresentazione comune che consente di ottenere informazioni preziose dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti ed esprimere gli attributi del cliente a fini di personalizzazione.

Poiché XDM è estremamente versatile e personalizzabile dal punto di vista della progettazione, è importante seguire le best practice per la modellazione dei dati durante la progettazione degli schemi. Questo documento illustra le decisioni e le considerazioni chiave da prendere per la mappatura dei dati sull&#39;esperienza cliente in XDM.

## Introduzione

Prima di leggere questa guida, consulta la panoramica [del sistema](../home.md) XDM per un&#39;introduzione di alto livello a XDM e il suo ruolo all&#39;interno  Experience Platform.

Inoltre, questa guida si concentra esclusivamente su considerazioni chiave relative alla progettazione dello schema. Si consiglia pertanto vivamente di fare riferimento alle [nozioni di base della composizione](./composition.md) dello schema per una spiegazione dettagliata dei singoli elementi dello schema citati in questa guida.

## Riepilogo delle procedure ottimali

L&#39;approccio consigliato per la progettazione del modello dati da utilizzare  Experience Platform può essere riassunto come segue:

1. Comprendere i casi di utilizzo aziendale per i dati.
1. Identificare le origini dati primarie a cui è necessario indirizzare [!DNL Platform] i casi di utilizzo.
1. Identificare eventuali origini dati secondarie che potrebbero anche essere di interesse. Ad esempio, se al momento solo una business unit della tua organizzazione è interessata a portare i propri dati a [!DNL Platform], una business unit simile potrebbe essere interessata a portare in futuro dati simili. La considerazione di queste origini secondarie consente di standardizzare il modello dati in tutta l&#39;organizzazione.
1. Crea un diagramma delle relazioni di entità di alto livello (ERD) per le origini dati identificate.
1. Convertite l’ERD di alto livello in un ERD [!DNL Platform]incentrato (inclusi profili, eventi esperienza ed entità di ricerca).

I passaggi relativi all&#39;identificazione delle origini dati applicabili necessarie per eseguire i casi d&#39;uso aziendali variano da un&#39;organizzazione all&#39;altra. Mentre il resto delle sezioni di questo documento si concentra sulle ultime fasi di organizzazione e costruzione di un ERD dopo l&#39;identificazione delle origini dati, le spiegazioni dei vari componenti del diagramma possono informare l&#39;utente delle decisioni su quale delle origini dati deve essere migrato [!DNL Platform].

## Creare un ERD di alto livello

Una volta determinate le origini dati in cui si desidera eseguire il processo di mappatura dei dati agli schemi XDM, [!DNL Platform]creare un ERD di alto livello.

L’esempio seguente rappresenta un ERD semplificato per una società che desidera inserire dati in [!DNL Platform]. Il diagramma evidenzia le entità essenziali che devono essere ordinate in classi XDM, inclusi account cliente, alberghi, indirizzi ed eventi di e-commerce comuni.

![](../images/best-practices/erd.png)

## Ordinare le entità in categorie di profilo, ricerca ed evento

Una volta creato un ERD per identificare le entità essenziali in cui si desidera eseguire l&#39;operazione, queste entità devono essere ordinate in categorie di profilo, ricerca ed evento: [!DNL Platform]

| Categoria | Descrizione |
| --- | --- |
| Entità profilo | Le entità profilo rappresentano gli attributi relativi a una singola persona, in genere un cliente. Le entità che rientrano in questa categoria devono essere rappresentate da schemi basati sulla **[!DNL XDM Individual Profile]classe**. |
| Entità di ricerca | Le entità di ricerca rappresentano concetti che possono essere correlati a una singola persona, ma che non possono essere utilizzati direttamente per identificare l&#39;individuo. Le entità che rientrano in questa categoria devono essere rappresentate da schemi basati su classi **** personalizzate. |
| Entità evento | Le entità evento rappresentano concetti relativi alle azioni che un cliente può intraprendere, agli eventi di sistema o a qualsiasi altro concetto in cui desideri tenere traccia dei cambiamenti nel tempo. Le entità che rientrano in questa categoria devono essere rappresentate da schemi basati sulla **[!DNL XDM ExperienceEvent]classe**. |

### Considerazioni per l&#39;ordinamento delle entità

Le sezioni seguenti forniscono ulteriori indicazioni su come ordinare le entità nelle categorie sopra indicate.

#### Attributi del cliente

Se un&#39;entità contiene attributi relativi a un singolo cliente, è molto probabile che sia un&#39;entità profilo. Alcuni esempi di attributi del cliente:

* Dati personali come nome, data di nascita, genere e ID account.
* Informazioni sulla posizione, ad esempio indirizzi e informazioni GPS.
* Informazioni di contatto, ad esempio numeri di telefono e indirizzi e-mail.

#### Monitoraggio dei dati nel tempo

Se si desidera analizzare il modo in cui determinati attributi all&#39;interno di un&#39;entità cambiano nel tempo, è più probabile che si tratti di un&#39;entità evento. Ad esempio, l&#39;aggiunta di prodotti a un carrello può essere tracciata come eventi da aggiungere al carrello in [!DNL Platform]:

| Customer ID | Tipo | ID prodotto | Quantità | Timestamp |
| --- | --- | --- | --- | --- |
| 1234567 | Add | 275098 | 2 | Ott 1, 10:32 |
| 1234567 | Rimuovi | 275098 | 1 | Ott 1, 10:33 |
| 1234567 | Add | 486502 | 1 | Ott 1, 10:41 |
| 1234567 | Add | 910482 | 5 | Ott 3, 2:15 PM |

#### Casi di utilizzo della segmentazione

Quando si suddividono in categorie le entità, è importante considerare i segmenti di pubblico che è possibile creare per risolvere i casi di utilizzo aziendali specifici.

Ad esempio, un&#39;azienda desidera conoscere tutti i membri &quot;Gold&quot; o &quot;Platinum&quot; del programma fedeltà che hanno fatto più di cinque acquisti nell&#39;ultimo anno. In base a questa logica di segmento, si possono trarre le seguenti conclusioni in merito alla presentazione delle entità rilevanti:

* &quot;Gold&quot; e &quot;Platinum&quot; rappresentano gli stati di fedeltà applicabili a un singolo cliente. Poiché la logica del segmento riguarda solo lo stato di fedeltà corrente dei clienti, questi dati possono essere modellati come parte di uno schema di profilo. Se desiderate tenere traccia delle modifiche nello stato di fedeltà nel tempo, potete anche creare uno schema aggiuntivo per le modifiche allo stato di fedeltà.
* Gli acquisti sono eventi che si verificano in un particolare momento e la logica del segmento riguarda gli eventi di acquisto all&#39;interno di una specifica finestra temporale. Tali dati devono pertanto essere modellati come schema di evento.

#### Casi di utilizzo dell&#39;attivazione

Oltre a considerazioni relative ai casi di utilizzo della segmentazione, è necessario esaminare anche i casi di utilizzo dell&#39;attivazione per tali segmenti al fine di identificare attributi rilevanti aggiuntivi.

Ad esempio, una società ha creato un segmento di pubblico basato sulla regola che `country = US`. Quindi, quando si attiva il segmento per alcuni target a valle, l&#39;azienda desidera filtrare tutti i profili esportati in base allo stato dell&#39;origine. Pertanto, un `state` attributo deve essere acquisito anche nell&#39;entità profilo applicabile.

#### Valori aggregati

In base al caso di utilizzo e alla granularità dei dati, è necessario decidere se alcuni valori devono essere pre-aggregati prima di essere inclusi in un&#39;entità profilo o evento.

Ad esempio, una società desidera creare un segmento basato sul numero di acquisti del carrello. Potete scegliere di incorporare questi dati alla granularità più bassa includendo ogni evento di acquisto con marca temporale come propria entità. Tuttavia, a volte questo può aumentare il numero di eventi registrati in modo esponenziale. Per ridurre il numero di eventi acquisiti, potete scegliere di creare un valore aggregato `numberOfPurchases` per un periodo di una settimana o di un mese. Altre funzioni di aggregazione come MIN e MAX possono essere applicate anche a queste situazioni.

>[!CAUTION]
>
> Experience Platform attualmente non esegue l&#39;aggregazione automatica dei valori, sebbene sia pianificata per le release future. Se si sceglie di utilizzare i valori aggregati, è necessario eseguire i calcoli esternamente prima di inviare i dati a [!DNL Platform].

#### Cardinalità

Le cardinalità stabilite nel vostro ERD possono anche fornire alcuni indizi su come classificare le vostre entità. Se esiste una relazione uno-molti tra due entità, l&#39;entità che rappresenta &quot;molte&quot; sarà probabilmente un&#39;entità evento. Tuttavia, in alcuni casi il &quot;many&quot; è un insieme di entità di ricerca fornite come array all&#39;interno di un&#39;entità di profilo.

>[!NOTE]
>
>Poiché non esiste un approccio universale per adattarsi a tutti i casi di utilizzo, è importante considerare i pro e i contro di ogni situazione quando si classificano le entità in base alla cardinalità. Per ulteriori informazioni, consulta la sezione [](#pros-and-cons) successiva.

Nella tabella seguente sono illustrate alcune relazioni di entità comuni e le categorie che possono essere derivate da esse:

| Relazione | Cardinalità | Categorie di entità |
| --- | --- | --- |
| Clienti e carrello | Da uno a molti | Un singolo cliente può avere molti pagamenti del carrello, che sono eventi che possono essere tracciati nel tempo. I clienti sarebbero quindi un&#39;entità di profilo, mentre i Checkout carrello sarebbero un&#39;entità evento. |
| Clienti e account fedeltà | Uno a uno | Un singolo cliente può avere un solo account fedeltà e viceversa. Poiché la relazione è uno a uno, sia i clienti che i conti fedeltà rappresentano entità di profilo. |
| Clienti e iscrizioni | Da uno a molti | Un singolo cliente può avere molte iscrizioni. Poiché la società riguarda solo le sottoscrizioni correnti di un cliente, Customers è un&#39;entità di profilo, mentre Subscriptions è un&#39;entità di ricerca. |

### Profili e svantaggi di diverse classi di entità {#pros-and-cons}

Mentre la sezione precedente fornisce alcune linee guida generali per decidere come classificare le entità, è importante comprendere che spesso possono esserci pro e contro per scegliere una categoria di entità più un&#39;altra. Il seguente caso di studio illustra come valutare le opzioni disponibili in queste situazioni.

Una società tiene traccia delle sottoscrizioni attive per i propri clienti, dove un cliente può avere molte sottoscrizioni. La società desidera inoltre includere iscrizioni per i casi di utilizzo della segmentazione, ad esempio la ricerca di tutti gli utenti con iscrizioni attive.

In questo scenario, la società dispone di due opzioni potenziali per rappresentare le sottoscrizioni di un cliente nel proprio modello dati:

1. [Usa attributi di profilo](#profile-approach)
1. [Utilizzare le entità evento](#event-approach)

#### Approccio 1: Usa attributi di profilo {#profile-approach}

Il primo approccio consiste nell&#39;includere un array di sottoscrizioni come attributi all&#39;interno dell&#39;entità profilo per Customers (Clienti). Gli oggetti contenuti in questa matrice contengono campi per `category`, `status`, `planName`, `startDate`e `endDate`.

<img src="../images/best-practices/profile-schema.png" width="800"><br>

**Pros**

* La segmentazione è possibile per il caso di utilizzo previsto.
* Lo schema mantiene solo i record di sottoscrizione più recenti per un cliente.

**Cons**

* L&#39;intero array deve essere ripristinato ogni volta che si verificano modifiche a qualsiasi campo dell&#39;array.
* Se origini dati o unità aziendali diverse inviano dati all&#39;array, sarà difficile mantenere l&#39;array aggiornato più recente sincronizzato su tutti i canali.

#### Approccio 2: Utilizzare le entità evento {#event-approach}

Il secondo approccio consiste nell’utilizzare gli schemi evento per rappresentare le sottoscrizioni. Ciò comporta l’assimilazione degli stessi campi di iscrizione del primo approccio, con l’aggiunta di un ID iscrizione, un ID cliente e una marca temporale del momento in cui si è verificato l’evento di iscrizione.

<img src="../images/best-practices/event-schema.png" width="800"><br>

**Pros**

* Le regole di segmentazione possono essere più flessibili (ad esempio, trovare tutti i clienti che hanno modificato le iscrizioni negli ultimi 30 giorni).
* Quando lo stato di iscrizione di un cliente cambia, non è più necessario aggiornare un array lungo e potenzialmente complesso negli attributi del profilo del cliente. Ciò è particolarmente utile se si verificano modifiche simultanee all&#39;elenco di iscrizione del cliente da più origini.

**Cons**

* La segmentazione diventa più complessa per il caso di utilizzo previsto originale (identificando lo stato delle iscrizioni più recenti dei clienti). Il segmento ora ha bisogno di logica aggiuntiva per contrassegnare l&#39;ultimo evento di iscrizione per un cliente al fine di controllarne lo stato.

## Creare schemi basati sulle entità categorizzate

Una volta ordinate le entità in categorie di profili, ricerche ed eventi, potete iniziare a convertire il modello dati in schemi XDM. A scopo dimostrativo, il modello di dati di esempio illustrato in precedenza è stato suddiviso in categorie appropriate nel diagramma seguente:

<img src="../images/best-practices/erd-sorted.png" width="800"><br>

La categoria in cui è stata ordinata un&#39;entità deve determinare la classe XDM su cui si basa lo schema. Per ribadire:

* Le entità di profilo devono utilizzare la [!DNL XDM Individual Profile] classe.
* Le entità evento devono utilizzare la [!DNL XDM ExperienceEvent] classe.
* Le entità di ricerca devono utilizzare classi XDM personalizzate definite dall&#39;organizzazione.

>[!NOTE]
>
>Anche se le entità evento saranno quasi sempre rappresentate da schemi separati, le entità nelle categorie di profilo o di ricerca possono essere combinate in un unico schema XDM, a seconda della loro cardinalità.
>
>Ad esempio, poiché l&#39;entità Customers ha una relazione uno-a-uno con l&#39;entità LoyaltyAccounts, lo schema per l&#39;entità Customers potrebbe includere anche un `LoyaltyAccount` oggetto che contenga i campi fedeltà appropriati per ciascun cliente. Se la relazione è uno-molti, tuttavia, l&#39;entità che rappresenta &quot;molti&quot; potrebbe essere rappresentata da uno schema separato o da un array di attributi di profilo, a seconda della sua complessità.

Le sezioni seguenti forniscono indicazioni generali sulla creazione di schemi basati sul vostro ERD.

### Adozione di un approccio di modellazione iterativa

Le [regole dell&#39;evoluzione](./composition.md#evolution) dello schema stabiliscono che solo le modifiche non distruttive possono essere apportate agli schemi una volta implementate. In altre parole, se si aggiunge un campo a uno schema e i dati sono stati acquisiti rispetto a tale campo, non sarà più possibile rimuoverlo. È quindi essenziale adottare un approccio di modellazione iterativa quando si creano per la prima volta gli schemi, a partire da un&#39;implementazione semplificata che diventa progressivamente più complessa nel tempo.

Se non si è certi che un particolare campo sia necessario includere in uno schema, è consigliabile non includerlo. Se in seguito viene determinato che il campo è necessario, può sempre essere aggiunto nell&#39;iterazione successiva dello schema.

### Campi identità

 Experience Platform, i campi XDM contrassegnati come identità vengono utilizzati per unire informazioni sui singoli clienti provenienti da più origini dati. Anche se uno schema può avere più campi contrassegnati come identità, è necessario definire una singola identità primaria affinché lo schema sia abilitato per l&#39;uso in [!DNL Real-time Customer Profile]. Per informazioni dettagliate sull&#39;uso di questi campi, vedere la sezione relativa ai campi [di](./composition.md#identity) identità nelle nozioni di base della composizione dello schema.

Durante la progettazione degli schemi, eventuali chiavi primarie nelle tabelle di database relazionali saranno probabilmente i candidati per le identità primarie. Altri esempi di campi di identità applicabili sono indirizzi e-mail del cliente, numeri di telefono, ID account e [ECID](../../identity-service/ecid.md).

###  Adobe di mixaggi delle applicazioni

 Experience Platform fornisce diversi mixin XDM out-of-the-box per l&#39;acquisizione di dati relativi alle seguenti applicazioni di Adobe :

* Adobe Analytics
* Adobe Audience Manager
* Adobe Campaign
* Adobe Target

Ad esempio, [[!UICONTROL Adobe Analytics ExperienceEvent Template Mixin]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json) consente di mappare campi [!DNL Analytics]specifici agli schemi XDM. A seconda delle applicazioni del Adobe  con cui state lavorando, dovete usare questi mixin  Adobe negli schemi.

<img src="../images/best-practices/analytics-mixin.png" width="700"><br>

 mixin di applicazioni di Adobe assegnano automaticamente un&#39;identità primaria predefinita tramite l&#39;uso del `identityMap` campo, un oggetto di sola lettura generato dal sistema che associa valori di identità standard per un singolo cliente.

Per  Adobe Analytics, ECID è l&#39;identità principale predefinita. Se un cliente non fornisce un valore ECID, per impostazione predefinita l&#39;identità principale sarà AAID.

>[!IMPORTANT]
>
>Quando utilizzate  mixin di applicazioni di Adobe, nessun altro campo deve essere contrassegnato come identità principale. Se esistono altre proprietà da contrassegnare come identità, questi campi devono essere assegnati come identità secondarie.

## Passaggi successivi

Questo documento ha trattato le linee guida generali e le procedure ottimali per la progettazione del modello dati per  Experience Platform. Per riepilogare:

* Utilizzate un approccio dall&#39;alto verso il basso, ordinando le tabelle di dati in categorie di profili, ricerche ed eventi prima di creare gli schemi.
* Spesso sono disponibili diversi approcci e opzioni per la progettazione di schemi per diversi scopi.
* Il modello dati deve supportare i casi di utilizzo della segmentazione.
* Semplificate il più possibile gli schemi e aggiungete nuovi campi solo quando necessario.

Una volta pronti, vedete l&#39;esercitazione sulla [creazione di uno schema nell&#39;interfaccia utente](../tutorials/create-schema-ui.md) per istruzioni dettagliate su come creare uno schema, assegnare la classe appropriata per l&#39;entità e aggiungere campi per la mappatura dei dati.