---
keywords: Experience Platform;home;argomenti popolari;schema;schema;enum;identità primaria;identità principale;profilo individuale XDM;evento esperienza;evento esperienza XDM;evento esperienza XDM;evento esperienza;evento esperienza;evento esperienza;evento esperienza XDM;progettazione schema;best practice
solution: Experience Platform
title: Best Practice Per La Modellazione Dei Dati
topic-legacy: overview
description: Questo documento fornisce un’introduzione agli schemi Experience Data Model (XDM) e ai blocchi predefiniti, ai principi e alle best practice per la composizione degli schemi da utilizzare in Adobe Experience Platform.
exl-id: 2455a04e-d589-49b2-a3cb-abb5c0b4e42f
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '2511'
ht-degree: 1%

---

# Best practice per la modellazione dei dati

[!DNL Experience Data Model] (XDM) è il framework principale che standardizza i dati sulla customer experience fornendo strutture e definizioni comuni da utilizzare nei servizi Adobe Experience Platform a valle. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune che ti consente di ottenere informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti ed esprimere gli attributi dei clienti a scopo di personalizzazione.

Poiché XDM è estremamente versatile e personalizzabile dal punto di vista della progettazione, è importante seguire le best practice per la modellazione dei dati durante la progettazione degli schemi. Questo documento illustra le decisioni e le considerazioni chiave da prendere durante la mappatura dei dati sulla customer experience in XDM.

## Introduzione

Prima di leggere questa guida, controlla [XDM System overview](../home.md) per un&#39;introduzione di alto livello a XDM e il suo ruolo all&#39;interno di Experience Platform.

Inoltre, questa guida si concentra esclusivamente su considerazioni chiave relative alla progettazione dello schema. Si consiglia pertanto vivamente di fare riferimento alle [nozioni di base sulla composizione dello schema](./composition.md) per una spiegazione dettagliata dei singoli elementi dello schema menzionati in questa guida.

## Riepilogo delle best practice

L’approccio consigliato per la progettazione del modello dati da utilizzare in Experience Platform può essere riassunto come segue:

1. Comprendere i casi d’uso aziendali per i dati.
1. Identifica le origini dati principali che devono essere portate in [!DNL Platform] per risolvere questi casi d’uso.
1. Identifica tutte le fonti di dati secondarie che potrebbero anche essere di interesse. Ad esempio, se al momento solo una business unit della tua organizzazione è interessata a trasferire i propri dati a [!DNL Platform], anche una business unit simile potrebbe essere interessata a portare in futuro dati simili. La considerazione di queste origini secondarie consente di standardizzare il modello dati in tutta l’organizzazione.
1. Crea un diagramma di relazione di entità di alto livello (ERD) per le origini dati identificate.
1. Converti l’ERD di alto livello in un ERD incentrato su [!DNL Platform] (inclusi profili, eventi di esperienza ed entità di ricerca).

I passaggi relativi all’identificazione delle origini dati applicabili necessarie per eseguire i casi d’uso aziendali variano da un’organizzazione all’altra. Mentre il resto delle sezioni di questo documento si concentra su questi ultimi passaggi di organizzazione e costruzione di un ERD dopo l&#39;identificazione delle fonti di dati, le spiegazioni dei vari componenti del diagramma possono informare le tue decisioni su quale delle tue fonti di dati deve essere migrato a [!DNL Platform].

## Creare un ERD di alto livello

Una volta determinate le origini dati da inserire in [!DNL Platform], crea un ERD di alto livello per aiutare a guidare il processo di mappatura dei dati sugli schemi XDM.

L’esempio seguente rappresenta un ERD semplificato per un’azienda che desidera inserire dati in [!DNL Platform]. Il diagramma evidenzia le entità essenziali che devono essere ordinate in classi XDM, inclusi account cliente, alberghi, indirizzi e diversi eventi di e-commerce comuni.

![](../images/best-practices/erd.png)

## Ordinare le entità in categorie di profili, ricerche ed eventi

Una volta creato un ERD per identificare le entità essenziali che si desidera inserire in [!DNL Platform], queste entità devono essere ordinate in categorie di profilo, ricerca ed evento:

| Categoria | Descrizione |
| --- | --- |
| Entità del profilo | Le entità profilo rappresentano gli attributi relativi a una singola persona, in genere un cliente. Le entità che rientrano in questa categoria devono essere rappresentate da schemi basati sulla classe **[!DNL XDM Individual Profile]**. |
| Entità di ricerca | Le entità di ricerca rappresentano concetti che possono riferirsi a una singola persona, ma che non possono essere utilizzati direttamente per identificare l’individuo. Le entità che rientrano in questa categoria devono essere rappresentate da schemi basati su **classi personalizzate**. |
| Entità evento | Le entità evento rappresentano i concetti relativi alle azioni che un cliente può intraprendere, agli eventi di sistema o a qualsiasi altro concetto in cui desideri tenere traccia dei cambiamenti nel tempo. Le entità che rientrano in questa categoria devono essere rappresentate da schemi basati sulla classe **[!DNL XDM ExperienceEvent]**. |

### Considerazioni sull’ordinamento delle entità

Le sezioni seguenti forniscono ulteriori indicazioni su come ordinare le entità nelle categorie sopra elencate.

#### Attributi del cliente

Se un’entità contiene attributi relativi a un singolo cliente, probabilmente si tratta di un’entità profilo. Alcuni esempi di attributi del cliente includono:

* Dati personali quali nome, data di nascita, genere e ID(i) account.
* Informazioni sulla posizione, ad esempio indirizzi e informazioni GPS.
* Informazioni di contatto quali numeri di telefono e indirizzi e-mail.

#### Tracciamento dei dati nel tempo

Se desideri analizzare in che modo determinati attributi all’interno di un’entità cambiano nel tempo, è più probabile che si tratti di un’entità evento. Ad esempio, l’aggiunta di elementi prodotto a un carrello può essere tracciata come eventi add-to-cart in [!DNL Platform]:

| Customer ID | Tipo | ID prodotto | Quantità | Timestamp |
| --- | --- | --- | --- | --- |
| 1234567 | Add | 275098 | 2 | Ott 1, 10:32 |
| 1234567 | Rimuovi | 275098 | 1 | Ott 1, 10:33 |
| 1234567 | Aggiungi | 486502 | 3 | Ott 1, 10:41 |
| 1234567 | Aggiungi | 910482 | 5 | 3 ottobre, 2:15 PM |

#### Casi di utilizzo della segmentazione

Quando si suddividono in categorie le entità, è importante considerare i segmenti di pubblico che si desidera creare per risolvere i casi d’uso aziendali specifici.

Ad esempio, un&#39;azienda vuole conoscere tutti i membri &quot;Gold&quot; o &quot;Platinum&quot; del loro programma fedeltà che hanno effettuato più di cinque acquisti nell&#39;ultimo anno. In base a questa logica di segmento, si possono trarre le seguenti conclusioni in merito a come dovrebbero essere rappresentate le entità rilevanti:

* &quot;Gold&quot; e &quot;Platinum&quot; rappresentano gli stati di fedeltà applicabili a un singolo cliente. Poiché la logica del segmento riguarda solo lo stato di fedeltà corrente dei clienti, questi dati possono essere modellati come parte di uno schema di profilo. Se desideri tenere traccia delle modifiche nello stato di fedeltà nel tempo, puoi anche creare uno schema di eventi aggiuntivo per le modifiche dello stato di fedeltà.
* Gli acquisti sono eventi che si verificano in un dato momento e la logica del segmento è interessata a eventi di acquisto all’interno di una specifica finestra temporale. Questi dati devono pertanto essere modellati come uno schema di evento.

#### Casi di utilizzo dell’attivazione

Oltre a considerazioni sui casi di utilizzo della segmentazione, devi anche esaminare i casi di utilizzo dell’attivazione per questi segmenti al fine di identificare attributi rilevanti aggiuntivi.

Ad esempio, una società ha creato un segmento di pubblico in base alla regola `country = US`. Quindi, quando attivi quel segmento su determinati target a valle, l&#39;azienda vuole filtrare tutti i profili esportati in base allo stato di origine. Pertanto, anche un attributo `state` deve essere acquisito nell’entità di profilo applicabile.

#### Valori aggregati

In base al caso d’uso e alla granularità dei dati, è necessario decidere se alcuni valori devono essere pre-aggregati prima di essere inclusi in un’entità profilo o evento.

Ad esempio, un’azienda desidera creare un segmento in base al numero di acquisti del carrello. Puoi scegliere di incorporare questi dati alla granularità più bassa includendo ogni evento di acquisto con marca temporale come propria entità. Tuttavia, a volte questo può aumentare il numero di eventi registrati in modo esponenziale. Per ridurre il numero di eventi acquisiti, puoi scegliere di creare un valore aggregato `numberOfPurchases` per un periodo di una settimana o di un mese. Anche altre funzioni aggregate come MIN e MAX possono essere applicate a queste situazioni.

>[!CAUTION]
>
>Al momento Experience Platform non esegue l’aggregazione automatica dei valori, anche se è pianificata per le versioni future. Se si sceglie di utilizzare i valori aggregati, è necessario eseguire i calcoli esternamente prima di inviare i dati a [!DNL Platform].

#### Cardinalità

Le cardinalità stabilite nel tuo ERD possono anche fornire alcuni indizi su come classificare le tue entità. Se esiste una relazione uno-a-molti tra due entità, l’entità che rappresenta i &quot;molti&quot; sarà probabilmente un’entità evento. Tuttavia, ci sono anche casi in cui il &quot;molti&quot; è un set di entità di ricerca che vengono fornite come array all’interno di un’entità di profilo.

>[!NOTE]
>
>Poiché non esiste un approccio universale per adattarsi a tutti i casi d&#39;uso, è importante considerare i pro e i contro di ogni situazione quando si classificano le entità in base alla cardinalità. Per ulteriori informazioni, consulta la sezione [successiva](#pros-and-cons) .

La tabella seguente illustra alcune relazioni di entità comuni e le categorie che possono essere derivate da esse:

| Relazione | Cardinalità | Categorie di entità |
| --- | --- | --- |
| Pagamenti per clienti e carrello | Uno a molti | Un singolo cliente può avere molti cart checkout, che sono eventi che possono essere tracciati nel tempo. I clienti sarebbero quindi un’entità di profilo, mentre Carrello Checkout sarebbe un’entità evento. |
| Clienti e account fedeltà | Uno a uno | Un singolo cliente può avere un solo account fedeltà e viceversa. Poiché la relazione è uno a uno, sia i clienti che i conti fedeltà rappresentano le entità del profilo. |
| Clienti e abbonamenti | Uno a molti | Un singolo cliente può avere molti abbonamenti. Poiché l’azienda si occupa solo degli abbonamenti correnti di un cliente, Customers è un’entità di profilo, mentre Subscriptions è un’entità di ricerca. |

### Propri e contro di diverse classi di entità {#pros-and-cons}

Mentre la sezione precedente fornisce alcune linee guida generali per decidere come categorizzare le entità, è importante comprendere che spesso possono esserci pro e contro per la scelta di una categoria di entità più di un’altra. Il seguente caso di studio ha lo scopo di illustrare come considerare le opzioni disponibili in queste situazioni.

Un&#39;azienda tiene traccia degli abbonamenti attivi per i propri clienti, dove un cliente può avere molti abbonamenti. L’azienda desidera inoltre includere gli abbonamenti per i casi di utilizzo della segmentazione, ad esempio per trovare tutti gli utenti con abbonamenti attivi.

In questo scenario, l&#39;azienda dispone di due opzioni potenziali per rappresentare le sottoscrizioni di un cliente nel proprio modello dati:

1. [Utilizzare gli attributi di profilo](#profile-approach)
1. [Utilizzare le entità evento](#event-approach)

#### Approccio 1: Usa attributi profilo {#profile-approach}

Il primo approccio consiste nell’includere un array di sottoscrizioni come attributi all’interno dell’entità profilo per Clienti. Gli oggetti contenuti in questa matrice conterrebbero campi per `category`, `status`, `planName`, `startDate` e `endDate`.

<img src="../images/best-practices/profile-schema.png" width="800"><br>

**Pro**

* La segmentazione è possibile per il caso d’uso previsto.
* Lo schema conserva solo i record di sottoscrizione più recenti per un cliente.

**Contro**

* L&#39;intero array deve essere ripristinato ogni volta che si verificano modifiche a qualsiasi campo dell&#39;array.
* Se diverse origini di dati o business unit inviano dati all&#39;array, sarà difficile mantenere l&#39;array aggiornato più recente sincronizzato su tutti i canali.

#### Approccio 2: Usa entità evento {#event-approach}

Il secondo approccio consiste nell’utilizzare gli schemi di evento per rappresentare le sottoscrizioni. Questo comporta l’acquisizione degli stessi campi di abbonamento del primo approccio, con l’aggiunta di un ID sottoscrizione, un ID cliente e una marca temporale di quando si è verificato l’evento di abbonamento.

<img src="../images/best-practices/event-schema.png" width="800"><br>

**Pro**

* Le regole di segmentazione possono essere più flessibili (ad esempio, per individuare tutti i clienti che hanno modificato l’abbonamento negli ultimi 30 giorni).
* Quando cambia lo stato di abbonamento di un cliente, non è più necessario aggiornare un array lungo e potenzialmente complesso all’interno degli attributi del profilo del cliente. Ciò è particolarmente utile se si verificano modifiche simultanee all’elenco di abbonamenti del cliente da più sorgenti.

**Contro**

* La segmentazione diventa più complessa per il caso d’uso originale previsto (identificando lo stato degli abbonamenti più recenti dei clienti). Il segmento deve ora essere dotato di una logica aggiuntiva per contrassegnare l’ultimo evento di abbonamento per un cliente al fine di verificarne lo stato.

## Creare schemi in base alle entità categorizzate

Dopo aver ordinato le entità in categorie di profili, ricerche ed eventi, puoi iniziare a convertire il modello dati in schemi XDM. A scopo dimostrativo, il modello di dati di esempio mostrato in precedenza è stato suddiviso in categorie appropriate nel diagramma seguente:

<img src="../images/best-practices/erd-sorted.png" width="800"><br>

La categoria in cui è stata ordinata un&#39;entità deve determinare la classe XDM su cui si basa lo schema. Per ribadire:

* Le entità di profilo devono utilizzare la classe [!DNL XDM Individual Profile] .
* Le entità evento devono utilizzare la classe [!DNL XDM ExperienceEvent] .
* Le entità di ricerca devono utilizzare classi XDM personalizzate definite dall&#39;organizzazione.

>[!NOTE]
>
>Anche se le entità evento saranno quasi sempre rappresentate da schemi separati, le entità nelle categorie di profilo o di ricerca possono essere combinate in un unico schema XDM, a seconda della loro cardinalità.
>
>Ad esempio, poiché l&#39;entità Customers ha una relazione uno-a-uno con l&#39;entità LoyaltyAccounts, lo schema per l&#39;entità Customers potrebbe includere anche un oggetto `LoyaltyAccount` per contenere i campi fedeltà appropriati per ciascun cliente. Tuttavia, se la relazione è da uno a molti, l’entità che rappresenta i &quot;molti&quot; potrebbe essere rappresentata da uno schema separato o da un array di attributi di profilo, a seconda della sua complessità.

Le sezioni seguenti forniscono indicazioni generali sulla costruzione di schemi basati sul tuo ERD.

### Adozione di un approccio di modellazione iterativa

Le [regole di evoluzione dello schema](./composition.md#evolution) impongono che solo le modifiche non distruttive possono essere apportate agli schemi una volta implementati. In altre parole, una volta aggiunto un campo a uno schema e i dati sono stati acquisiti rispetto a tale campo, il campo non può più essere rimosso. È quindi essenziale adottare un approccio di modellazione iterativa quando si creano per la prima volta i propri schemi, a partire da un’implementazione semplificata che diventa progressivamente più complessa nel tempo.

Se non sei sicuro se un particolare campo sia necessario per essere incluso in uno schema, la procedura consigliata consiste nell’escluderlo. Se in seguito viene determinato che il campo è necessario, può sempre essere aggiunto nell’iterazione successiva dello schema.

### Campi di identità

Ad Experience Platform, i campi XDM contrassegnati come identità vengono utilizzati per unire le informazioni sui singoli clienti provenienti da più origini dati. Anche se uno schema può avere più campi contrassegnati come identità, è necessario definire una singola identità primaria affinché lo schema sia abilitato per l&#39;utilizzo in [!DNL Real-time Customer Profile]. Per informazioni più dettagliate sul caso d&#39;uso di questi campi, consulta la sezione sui [campi di identità](./composition.md#identity) nelle nozioni di base sulla composizione dello schema.

Durante la progettazione degli schemi, qualsiasi chiave primaria nelle tabelle di database relazionali sarà probabilmente candidato per le identità principali. Altri esempi di campi di identità applicabili sono gli indirizzi e-mail dei clienti, i numeri di telefono, gli ID account e [ECID](../../identity-service/ecid.md).

### Adobe di gruppi di campi dello schema dell&#39;applicazione

Experience Platform fornisce diversi gruppi di campi di schema XDM predefiniti per l’acquisizione di dati relativi alle seguenti applicazioni di Adobe:

* Adobe Analytics
* Adobe Audience Manager
* Adobe Campaign
* Adobe Target

Ad esempio, il gruppo di campi [[!UICONTROL Adobe Analytics ExperienceEvent Template]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json) consente di mappare i campi specifici di [!DNL Analytics] agli schemi XDM. A seconda delle applicazioni di Adobe con cui stai lavorando, devi utilizzare questi gruppi di campi forniti da Adobe nei tuoi schemi.

<img src="../images/best-practices/analytics-field-group.png" width="700"><br>

I gruppi di campi dell&#39;applicazione di Adobe assegnano automaticamente un&#39;identità primaria predefinita tramite l&#39;uso del campo `identityMap` , che è un oggetto di sola lettura generato dal sistema che mappa i valori di identità standard di un singolo cliente.

Per Adobe Analytics, ECID è l’identità principale predefinita. Se un cliente non fornisce un valore ECID, l’identità principale viene impostata invece come predefinita su AAID.

>[!IMPORTANT]
>
>Quando si utilizzano gruppi di campi dell’applicazione Adobe, nessun altro campo deve essere contrassegnato come identità principale. Se vi sono proprietà aggiuntive che devono essere contrassegnate come identità, questi campi devono essere invece assegnati come identità secondarie.

## Passaggi successivi

Questo documento illustra le linee guida generali e le best practice per la progettazione del modello dati, ad Experience Platform. Per riepilogare:

* Utilizza un approccio dall’alto verso il basso ordinando le tabelle di dati in categorie di profili, ricerche ed eventi prima di costruire gli schemi.
* Spesso sono disponibili diversi approcci e opzioni per la progettazione degli schemi per scopi diversi.
* Il modello dati deve supportare i casi d’uso aziendali, ad esempio la segmentazione o l’analisi dei percorsi cliente.
* Crea gli schemi il più semplice possibile e aggiungi nuovi campi solo quando necessario.

Una volta pronti, consulta l’esercitazione su [creazione di uno schema nell’interfaccia utente](../tutorials/create-schema-ui.md) per istruzioni dettagliate su come creare uno schema, assegnare la classe appropriata per l’entità e aggiungere campi in cui mappare i dati.
