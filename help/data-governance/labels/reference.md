---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Etichette di utilizzo dati supportate
topic: labels
translation-type: tm+mt
source-git-commit: d4964231ee957349f666eaf6b0f5729d19c408de
workflow-type: tm+mt
source-wordcount: '1878'
ht-degree: 1%

---


# Etichette di utilizzo dati supportate

 Adobe Experience Platform include l&#39;infrastruttura per la gestione dei dati con l&#39;etichettatura e l&#39;applicazione dell&#39;uso dei dati (DULE, Data Usage Labeling and Enforcement) al suo centro.  Le funzioni DULE consentono l&#39;applicazione di etichette di utilizzo dei dati a set di dati e campi, al fine di classificare i dati in base al tipo di criteri di utilizzo applicabili a tali dati.

In questo documento vengono delineate tutte le etichette di utilizzo dei dati attualmente supportate da [!DNL Experience Platform]. Ulteriori informazioni relative [!DNL Data Governance] e DULE sono disponibili nella panoramica [sulla governance dei](../home.md)dati.

## Etichette contratto

Le etichette &quot;C&quot; del contratto sono utilizzate per classificare i dati che hanno obblighi contrattuali o che sono correlati alle politiche di governance dei dati della tua organizzazione.

| Etichetta | Definizione |
|---|---|
| **C1** | I dati possono essere esportati solo da Adobe Experience Cloud in un modulo aggregato, senza includere identificatori singoli o dispositivo. [Ulteriori informazioni...](#c1) |
| **C2** | I dati non possono essere esportati a terzi. [Ulteriori informazioni...](#c2) |
| **C3** | I dati non possono essere combinati o altrimenti utilizzati con informazioni direttamente identificabili. [Ulteriori informazioni...](#c3) |
| **C4** | I dati non possono essere utilizzati per il targeting di annunci o contenuti, né sul sito né tra siti. [Ulteriori informazioni...](#c4) |
| **C5** | I dati non possono essere utilizzati per il targeting intersito di contenuti o annunci pubblicitari basato su interessi. [Ulteriori informazioni...](#c5) |
| **C6** | I dati non possono essere utilizzati per il targeting di annunci on-site. [Ulteriori informazioni...](#c6) |
| **C7** | I dati non possono essere utilizzati per il targeting on-site del contenuto. [Ulteriori informazioni...](#c7) |
| **C8** | I dati non possono essere utilizzati per la misurazione dei siti Web o delle app dell&#39;organizzazione. [Ulteriori informazioni...](#c8) |
| **C9** | I dati non possono essere utilizzati nei flussi di lavoro Data Science. [Ulteriori informazioni...](#c9) |
| **C10** | I dati non possono essere utilizzati per l&#39;attivazione dell&#39;identità unita. [Ulteriori informazioni...](#c10) |

## Etichette identità

Le etichette di identità &quot;I&quot; vengono utilizzate per classificare i dati in grado di identificare o contattare una persona specifica.

| Etichetta | Definizione |
|---|---|
| **I1** | Dati direttamente identificabili che possono identificare o contattare una persona specifica, anziché un dispositivo. |
| **I2** | Dati identificabili indirettamente che possono essere utilizzati in combinazione con qualsiasi altro dato per identificare o contattare una persona specifica. |

## Etichette sensibili

Le etichette &quot;S&quot; sensibili vengono utilizzate per classificare i dati che voi e la vostra organizzazione considerate sensibili.

Un tipo di dati che si può ritenere sensibili può essere diversi tipi di dati geografici; tuttavia, questa categoria non è limitata ai dati geografici.

| Etichetta | Definizione |
|---|---|
| **S1** | Dati che specificano latitudine e longitudine utilizzabili per determinare la posizione esatta di un dispositivo. |
| **S2** | Dati che possono essere utilizzati per determinare un&#39;area geografica definita in senso ampio. |

## Appendice

Le sezioni seguenti forniscono informazioni aggiuntive sulle etichette di utilizzo dei dati disponibili.

### Dettagli etichetta contratto

Le sezioni seguenti forniscono informazioni dettagliate relative all&#39;attuazione di specifiche etichette &quot;C&quot; del contratto.

#### C1 {#c1}

Alcuni dati possono essere esportati solo da Adobe Experience Cloud in un modulo aggregato, senza includere identificatori singoli o dispositivo. Ad esempio, i dati originati dai social network.

#### C2 {#c2}

Alcuni provider di dati hanno termini nei loro contratti che vietano l&#39;esportazione di dati da dove è stato originariamente raccolto. Ad esempio, i contratti con i social network spesso limitano il trasferimento dei dati che ricevi da loro. L&#39;etichetta C2 è più restrittiva di [C1](#c1), che richiede solo l&#39;aggregazione e dati anonimi.

#### C3 {#c3}

Alcuni fornitori di dati hanno termini nei loro contratti che vietano la combinazione o l&#39;uso di tali dati con informazioni direttamente identificabili. Ad esempio, i contratti per i dati originati da reti pubblicitarie, server di annunci e provider di dati di terze parti spesso includono specifici divieti contrattuali sull&#39;uso di tali dati con dati direttamente identificabili.

#### C4 {#c4}

C4 è l&#39;etichetta più restrittiva; comprende le etichette [C5](#c5), [C6](#c6)e [C7](#c7).

#### C5 {#c5}

Il targeting basato sugli interessi, o personalizzazione, si verifica se sono soddisfatte tre condizioni: I dati raccolti in loco sono (1) utilizzati per fare deduzioni sugli interessi degli utenti, (2) utilizzati in un altro contesto, ad esempio in un altro sito o in un&#39;altra app (fuori sito) E (3) utilizzati per selezionare quali contenuti o annunci vengono serviti in base a tali inferenze.

La combinazione di dati provenienti da diversi siti, inclusa una combinazione di dati sul sito e dati fuori sede o una combinazione di dati provenienti da più fonti esterne al sito, è definita dati intersito. Diversi siti rappresentano contesti diversi, in modo che l’utilizzo di dati intersito in qualsiasi contesto sia diverso dall’originale. I dati intersito vengono in genere raccolti ed elaborati per trarre conclusioni sugli interessi degli utenti. Di conseguenza, l&#39;uso di dati intersito per il targeting di annunci o contenuti si qualifica generalmente come targeting basato sugli interessi, indipendentemente dal fatto che l&#39;annuncio o il contenuto siano visualizzati sul sito o fuori sito. Ad esempio, se i dati sul sito sono stati utilizzati insieme ai dati fuori sito per selezionare quale annuncio pubblicitario mostrare a un utente sul sito dell&#39;organizzazione, tale utilizzo si qualifica come targeting basato sugli interessi. Un altro esempio è rappresentato dal fatto che il retargeting degli annunci agli utenti off-site potrebbe essere considerato un targeting basato sugli interessi.

L&#39;uso di dati esterni al sito da soli per il targeting potrebbe anche essere considerato come targeting basato sugli interessi, dal momento che i dati fuori sede vengono solitamente raccolti ed elaborati per fare deduzioni sugli interessi degli utenti.

Tuttavia, il targeting del contenuto o degli annunci che utilizzano solo dati sul sito non è generalmente qualificato come targeting basato su interessi. Il targeting on-site che altrimenti non viene qualificato come targeting basato sugli interessi viene trattato come due etichette distinte. In modo specifico, Label C6 indirizza al targeting e ai report degli annunci in loco e parla in modo specifico di selezione, consegna e reporting degli annunci, nonché degli indirizzi Label C7 per la selezione, la distribuzione e il reporting dei contenuti in loco (targeting dei contenuti in sito).

In ultima analisi, l&#39;interpretazione dell&#39;etichetta e il modo in cui viene applicato l&#39;uso dei dati con l&#39;etichetta spetta all&#39;utente. Per riferimento, i framework IAB e DAA sono forniti di seguito:

IAB: Personalizzazione. La raccolta e l&#39;elaborazione di informazioni sull&#39;uso di questo servizio per personalizzare successivamente la pubblicità e/o il contenuto per l&#39;utente in altri contesti, come in altri siti Web o app, nel tempo. In genere, il contenuto del sito o dell&#39;app viene utilizzato per trarre conclusioni sui tuoi interessi che informano la selezione futura di pubblicità e/o contenuti.

DAA: Annuncio comportamentale on-line. Raccolta di dati da un particolare computer o dispositivo relativi ai comportamenti di visualizzazione Web nel tempo e tra siti Web non affiliati allo scopo di utilizzare tali dati per prevedere preferenze o interessi degli utenti per la distribuzione di pubblicità a tale computer o dispositivo in base alle preferenze o agli interessi dedotti da tali comportamenti di visualizzazione Web.

#### C6 {#c6}

Gli annunci sono messaggi o notifiche, inclusi testo e immagini, che appaiono su un sito Web o un&#39;app e sono destinati principalmente a promuovere la vendita di beni o servizi. È compito dell&#39;utente determinare lo scopo di tali messaggi o notifiche. Gli annunci sono separati dal contenuto presente sul sito, coperti dall’etichetta [C7](#c7). I dati con un&#39;etichetta C6 non possono essere utilizzati per il targeting di annunci in loco, inclusa la selezione e la consegna di annunci pubblicitari sui siti Web o sulle app dell&#39;organizzazione, o per misurare la consegna e l&#39;efficacia di tali annunci. Ciò include l&#39;utilizzo di dati precedentemente raccolti sul sito sugli interessi degli utenti per selezionare gli annunci, elaborare i dati su quali annunci sono stati visualizzati, quando e dove sono stati visualizzati, e se gli utenti hanno intrapreso qualsiasi azione correlata all&#39;annuncio, ad esempio facendo clic su un annuncio o effettuando un acquisto. Generalmente, trarre conclusioni sulle preferenze degli utenti in base alle attività sul sito di tali utenti e quindi utilizzare tali preferenze nel targeting on-site degli annunci non sarebbe considerato un targeting basato sugli interessi (o personalizzazione), in quanto non soddisferebbe tutti e tre i requisiti necessari per il targeting basato sugli interessi. _[Per i seguenti requisiti, vedere l’etichetta C5.](#c5)_

In ultima analisi, l&#39;interpretazione dell&#39;etichetta e il modo in cui viene applicato l&#39;uso dei dati con l&#39;etichetta spetta all&#39;utente. Per riferimento, i framework IAB e DAA sono forniti di seguito:

IAB: 3. Selezione, consegna e reporting degli annunci: La raccolta di informazioni, e la combinazione con le informazioni raccolte in precedenza, per selezionare e distribuire gli annunci pubblicitari per voi, e per misurare la consegna e l&#39;efficacia di tali pubblicità. Ciò include l&#39;utilizzo delle informazioni raccolte in precedenza sui tuoi interessi per selezionare gli annunci, l&#39;elaborazione dei dati su quali annunci sono stati visualizzati, la frequenza con cui sono stati visualizzati, quando e dove sono stati visualizzati, e se hai intrapreso qualsiasi azione correlata all&#39;annuncio, ad esempio facendo clic su un annuncio o effettuando un acquisto. Questa non include la Personalizzazione, ovvero la raccolta e l&#39;elaborazione di informazioni sull&#39;uso di questo servizio per personalizzare successivamente la pubblicità e/o il contenuto per l&#39;utente in altri contesti, come siti Web o app, nel tempo.

DAA: L&#39;annuncio comportamentale online non include le attività di First Party, Ad Delivery o Ad Reporting, né la pubblicità contestuale (ad es. pubblicità basata sul contenuto della pagina Web visitata, la visita corrente del consumatore in una pagina Web o una query di ricerca).

#### C7 {#c7}

Il contenuto in loco è testo e immagini progettati per informare, educare o intrattenere e non creati per promuovere la vendita di beni o servizi. È compito dell&#39;utente determinare lo scopo del contenuto, specificando se il contenuto potrebbe essere considerato come pubblicità nativa. L’etichetta C7 non è destinata a coprire gli annunci sul sito, che sono coperti dall’etichetta [C6](#c6). I dati con un&#39;etichetta C7 non possono essere utilizzati per il targeting dei contenuti on-site, inclusa la selezione e la distribuzione di contenuti sui siti Web o sulle app dell&#39;organizzazione, né per misurare la consegna e l&#39;efficacia di tali contenuti. Ciò include informazioni precedentemente raccolte sugli interessi degli utenti in determinati contenuti, l&#39;elaborazione dei dati su quale contenuto è stato visualizzato, la frequenza o il periodo di visualizzazione, quando e dove è stato visualizzato, e se gli utenti hanno eseguito azioni correlate ai contenuti, ad esempio facendo clic sui contenuti. Generalmente, trarre conclusioni sulle preferenze degli utenti in base alle attività sul sito di tali utenti e quindi utilizzare tali preferenze nel targeting dei contenuti in loco non sarebbe considerato un targeting basato sugli interessi (o personalizzazione), in quanto non soddisferebbe tutti e tre i requisiti necessari per il targeting basato sugli interessi. _[Per i seguenti requisiti, vedere l’etichetta C5.](#c5)_

In ultima analisi, l&#39;interpretazione dell&#39;etichetta e il modo in cui viene applicato l&#39;uso dei dati con l&#39;etichetta spetta all&#39;utente. Per riferimento, i framework IAB e DAA sono forniti di seguito:

IAB: 4. Selezione, distribuzione e reporting dei contenuti: La raccolta di informazioni, e la combinazione con le informazioni raccolte in precedenza, per selezionare e distribuire contenuti per l&#39;utente e per misurare la consegna e l&#39;efficacia di tali contenuti. Ciò include l&#39;utilizzo delle informazioni raccolte in precedenza sugli interessi dell&#39;utente per selezionare il contenuto, l&#39;elaborazione dei dati su quale contenuto è stato visualizzato, la frequenza o il periodo di visualizzazione, quando e dove è stato visualizzato, e se sono state eseguite azioni correlate al contenuto, ad esempio facendo clic sul contenuto. Questa non include la Personalizzazione, ovvero la raccolta e l&#39;elaborazione di informazioni sull&#39;uso di questo servizio per personalizzare successivamente contenuti e/o pubblicità per l&#39;utente in altri contesti, come siti Web o app, nel tempo.

DAA: L&#39;annuncio comportamentale online non include le attività di First Party, Ad Delivery o Ad Reporting, né la pubblicità contestuale (ad es. pubblicità basata sul contenuto della pagina Web che si sta visitando, la visita di un consumatore a una pagina Web o una query di ricerca).

#### C8 {#c8}

I dati non possono essere utilizzati per misurare, comprendere e segnalare l&#39;utilizzo da parte degli utenti dei siti o delle app dell&#39;organizzazione. Questo non include il targeting basato sugli interessi (targeting tra siti), ovvero la raccolta di informazioni sull&#39;utilizzo di questo servizio per personalizzare successivamente contenuti e/o pubblicità in altri contesti, ad esempio su altri servizi, come siti Web o app, nel tempo.

#### C9 {#c9}

Alcuni contratti includono divieti espliciti sull&#39;uso dei dati per la scienza dei dati. Talvolta tali termini sono formulati in termini che vietano l&#39;uso di dati per l&#39;intelligenza artificiale (AI), l&#39;apprendimento automatico (ML) o la modellazione.

#### C10 {#c10}

Alcuni criteri di utilizzo dei dati limitano l&#39;utilizzo di dati di identità uniti per la personalizzazione. L&#39;etichetta C10 viene applicata automaticamente ai segmenti se i relativi criteri di unione utilizzano l&#39;opzione &quot;grafico privato&quot;.
