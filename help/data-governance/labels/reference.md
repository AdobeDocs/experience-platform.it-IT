---
keywords: Experience Platform;home;argomenti popolari;governance dei dati;etichetta di utilizzo dati api;api servizio criteri;etichette di utilizzo dati supportate;etichette contratto;etichette identità;etichette sensibili
solution: Experience Platform
title: Glossario delle etichette di utilizzo dati
description: Questo documento illustra tutte le etichette di utilizzo dei dati attualmente supportate da Adobe Experience Platform.
exl-id: 70d0702d-def7-4ab2-a861-eaf0f0cde1d4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2257'
ht-degree: 7%

---

# Glossario delle etichette di utilizzo dei dati {#data-usage-labels-glossary}

>[!CONTEXTUALHELP]
>id="platform_policies_labeltype"
>title="Tipi di etichette"
>abstract="Esistono diverse categorie di etichette di utilizzo dei dati. Le etichette definite da Adobe includono etichette per contratti, per identità e per dati sensibili. Le etichette definite dalla tua organizzazione vengono classificate come etichette personalizzate."
>text="See the data usage labels glossary for more information on these label types."

Le etichette di utilizzo dei dati consentono di categorizzare i set di dati e i campi in base a [criteri di governance](../policies/overview.md) e [criteri di controllo dell&#39;accesso](../../access-control/abac/overview.md) applicabili a tali dati. Adobe Experience Platform fornisce diverse etichette di utilizzo dei dati di base pronte all’uso che puoi utilizzare per iniziare a categorizzare i dati.

Questo documento illustra le etichette di utilizzo dei dati di base attualmente fornite da Experience Platform.

## Etichette per contratti {#contract}

Le etichette &quot;C&quot; del contratto vengono utilizzate per categorizzare i dati che hanno obblighi contrattuali o sono relativi ai criteri di governance dei dati della tua organizzazione.

| Etichetta | Definizione |
| --- | --- |
| [C1](#c1) | I dati possono essere esportati da Adobe Experience Cloud solo in un modulo aggregato senza includere identificatori individuali o di dispositivo. |
| [C2](#c2) | I dati non possono essere esportati a terzi. |
| [C3](#c3) | I dati non possono essere combinati o altrimenti utilizzati con informazioni direttamente identificabili. |
| [C4](#c4) | I dati non possono essere utilizzati per il targeting di annunci o contenuti, né sul sito né tra siti diversi. |
| [C5](#c5) | I dati non possono essere utilizzati per il targeting tra siti di contenuti o annunci basato sugli interessi. |
| [C6](#c6) | I dati non possono essere utilizzati per il targeting di annunci nel sito. |
| [C7](#c7) | I dati non possono essere utilizzati per il targeting dei contenuti sul sito. |
| [C8](#c8) | I dati non possono essere utilizzati per la misurazione dei siti web o delle app della tua organizzazione. |
| [C9](#c9) | I dati non possono essere utilizzati nei flussi di lavoro di data science. |
| [C10](#c10) | I dati non possono essere utilizzati per l’attivazione di identità unite. |
| [C11](#c11) | I dati non possono essere condivisi con i partner di corrispondenza dei segmenti. |
| [C12](#c12) | I dati non possono essere esportati in alcun modo. |

## Etichette di identità {#identity}

Le etichette di identità “I” vengono utilizzate per categorizzare i dati che possono identificare o contattare una persona specifica.

| Etichetta | Definizione |
| --- | --- |
| **I1** | Dati direttamente identificabili che possono identificare o contattare una persona specifica, anziché un dispositivo. |
| **I2** | Dati indirettamente identificabili che possono essere utilizzati in combinazione con altri dati per identificare o contattare una persona specifica. |

## Etichette per dati sensibili {#sensitive}

Le etichette sensibili &quot;S&quot; vengono utilizzate per categorizzare i dati considerati sensibili dall’utente e dall’organizzazione.

Un tipo di dati che si può considerare sensibile può essere diversi tipi di dati geografici; tuttavia, questa categoria non è limitata ai dati geografici.

| Etichetta | Definizione |
| --- | --- |
| **S1** | Dati che specificano la latitudine e la longitudine utilizzati per determinare la posizione esatta di un dispositivo. |
| **S2** | Dati che possono essere utilizzati per determinare un’area recintata in modo ampio. |
| **PSPD** | I dati personali sensibili consentiti (PSPD) si riferiscono a dati che Adobe consente contrattualmente di caricare e che sono considerati &quot;sensibili&quot;, &quot;categorie speciali di dati&quot; o termini simili utilizzati dalle leggi applicabili. Ciò esclude specificamente le informazioni sanitarie protette (PHI) e altri dati sanitari regolamentati. |
| **RHD** | Dati che si riferiscono a informazioni protette sulla salute (PHI) o informazioni su un paziente che Adobe ti consente contrattualmente di caricare. |

## Etichette per ecosistemi partner {#partner}

Le etichette dell’ecosistema partner vengono utilizzate per categorizzare i dati ottenuti da fonti esterne all’organizzazione.

Questa etichetta viene utilizzata per determinare l’utilizzo dei dati dei potenziali clienti.

| Etichetta | Definizione |
| --- | --- |
| **Terze parti** | I dati di terze parti sono dati forniti da un fornitore di dati di terze parti. Un fornitore di dati di terze parti è un’entità che ha concluso un accordo con l’organizzazione che ti autorizza ad accedere ai dati di terze parti, utilizzarli, visualizzarli e trasmetterli insieme ad Experience Platform. |
| **Arricchimento di terze parti** | Dati raccolti da un’organizzazione terza che non è direttamente correlata alla persona interessata. L’etichetta deve essere applicata ai dati di terze parti utilizzati per arricchire i profili di prime parti. |
| **Prospezione di terze parti** | Dati raccolti da un’organizzazione terza che non è direttamente correlata alla persona interessata. L’etichetta deve essere applicata ai dati di terze parti utilizzati nella parte superiore della ricerca di funnel per clienti nuovi. |

## Appendice

Le sezioni seguenti forniscono informazioni aggiuntive sulle etichette di utilizzo dei dati disponibili.

### Dettagli etichetta contratto

Le sezioni seguenti forniscono informazioni dettagliate relative all’attuazione di specifici contratti con l’etichetta &quot;C&quot;.

#### C1 {#c1}

Alcuni dati possono essere esportati da Adobe Experience Cloud solo in un modulo aggregato senza includere identificatori individuali o di dispositivo. Ad esempio, dati provenienti dai social network.

#### C2 {#c2}

Alcuni fornitori di dati hanno clausole nei loro contratti che vietano l’esportazione di dati da dove sono stati raccolti originariamente. Ad esempio, i contratti per social network spesso limitano il trasferimento dei dati che ricevi da loro. L&#39;etichetta C2 è più restrittiva di [C1](#c1), che richiede solo l&#39;aggregazione e dati anonimi, ma è meno restrittiva di [C12](#c12), il che impedisce completamente le esportazioni di dati indipendentemente dalla destinazione.

#### C3 {#c3}

Alcuni fornitori di dati hanno clausole nei loro contratti che vietano la combinazione o l’uso di tali dati con informazioni direttamente identificabili. Ad esempio, i contratti per i dati provenienti da reti di annunci, server di annunci e fornitori di dati di terze parti spesso includono divieti contrattuali specifici sull’utilizzo di tali dati con dati direttamente identificabili.

#### C4 {#c4}

C4 include le etichette [C5](#c5), [C6](#c6) e [C7](#c7). È una delle etichette più restrittive, seconda solo a [C12](#c12).

#### C5 {#c5}

Il targeting basato sugli interessi, o personalizzazione, si verifica se sono soddisfatte le tre condizioni seguenti: i dati raccolti sul sito sono (1) utilizzati per trarre conclusioni sugli interessi di un utente, (2) utilizzati in un altro contesto, ad esempio su un altro sito o un’altra app (off-site) E (3) utilizzati per selezionare quali contenuti o annunci vengono distribuiti in base a tali conclusioni.

La combinazione di dati provenienti da diversi siti, compresa una combinazione di dati nel sito e dati esterni al sito o una combinazione di dati provenienti da diverse fonti esterne al sito, è definita dati intersito. Siti diversi rappresentano contesti diversi, in modo che l’utilizzo di dati tra siti diversi in qualsiasi contesto sia diverso dall’originale. I dati tra siti vengono generalmente raccolti ed elaborati per trarre conclusioni sugli interessi degli utenti. Di conseguenza, l’utilizzo di dati intersito per il targeting di annunci o contenuti si qualifica generalmente come targeting basato sugli interessi, indipendentemente dal fatto che l’annuncio o il contenuto venga visualizzato sul sito o fuori dal sito. Ad esempio, se i dati nel sito vengono utilizzati in combinazione con i dati esterni al sito per selezionare l’annuncio da mostrare a un utente sul sito di un’organizzazione, tale utilizzo si qualifica come targeting basato sugli interessi. Un altro esempio è che il retargeting degli annunci per utenti fuori dal sito probabilmente si qualificherebbe anche come targeting basato sugli interessi.

Anche l’utilizzo dei soli dati fuori sito per il targeting si qualificherebbe probabilmente come targeting basato sugli interessi, in quanto i dati esterni al sito vengono generalmente raccolti ed elaborati per trarre conclusioni sugli interessi degli utenti.

Tuttavia, il targeting di contenuti o annunci utilizzando solo i dati sul sito in genere non si qualifica come targeting basato sugli interessi. Il targeting sul sito che non è altrimenti qualificato come targeting basato su interessi è trattato come due etichette distinte. In particolare, Label C6 si occupa del targeting e del reporting degli annunci nel sito, in particolare della selezione, distribuzione e reporting degli annunci, mentre Label C7 si occupa della selezione, della consegna e del reporting dei contenuti nel sito (targeting dei contenuti nel sito).

In ultima analisi, spetta a te interpretare l’etichetta e come viene applicato l’utilizzo dei dati con tale etichetta. Per riferimento, di seguito sono riportati i framework IAB e DAA:

IAB: Personalization. La raccolta e l&#39;elaborazione di informazioni sull&#39;utilizzo di questo servizio per personalizzare successivamente pubblicità e/o contenuti per te in altri contesti, ad esempio su altri siti web o app, nel tempo. In genere, il contenuto del sito o dell’app viene utilizzato per trarre conclusioni sui tuoi interessi che informano la futura selezione di pubblicità e/o contenuti.

DAA: pubblicità comportamentale online. Raccogliere dati da un particolare computer o dispositivo riguardo ai comportamenti di visualizzazione web nel tempo e tra siti web non affiliati al fine di utilizzare tali dati per prevedere le preferenze o gli interessi degli utenti di fornire pubblicità a tale computer o dispositivo in base alle preferenze o agli interessi dedotti da tali comportamenti di visualizzazione web.

#### C6 {#c6}

Gli annunci sono messaggi o notifiche, inclusi testo e immagini, visualizzati su un sito web o un’app principalmente destinati a promuovere la vendita di beni o servizi. Spetta a te determinare lo scopo di tali messaggi o notifiche. Gli annunci sono distinti dal contenuto nel sito e sono coperti dall&#39;etichetta [C7](#c7). I dati con etichetta C6 non possono essere utilizzati per il targeting di annunci nel sito, inclusa la selezione e la consegna di annunci sui siti web o sulle app della tua organizzazione o per misurare la consegna e l’efficacia di tali annunci. Ciò include l’utilizzo di dati sul sito raccolti in precedenza sugli interessi degli utenti di selezionare annunci, elaborare dati su quali annunci pubblicitari sono stati mostrati, quando e dove sono stati mostrati e se gli utenti hanno intrapreso azioni relative all’annuncio, ad esempio la selezione di un annuncio o l’acquisto di un prodotto. In genere, trarre conclusioni sulle preferenze di un utente in base alle sue attività nel sito e quindi utilizzare tali preferenze nel targeting degli annunci nel sito non si qualifica come targeting basato sugli interessi (o personalizzazione), in quanto non soddisfa tutti e tre i requisiti necessari per il targeting basato sugli interessi. *[Per i requisiti, vedere l&#39;etichetta C5.](#c5)*

In ultima analisi, spetta a te interpretare l’etichetta e come viene applicato l’utilizzo dei dati con tale etichetta. Per riferimento, di seguito sono riportati i framework IAB e DAA:

IAB: 3. Selezione, consegna e reporting degli annunci: la raccolta di informazioni e la combinazione con le informazioni raccolte in precedenza, per selezionare e distribuire annunci pubblicitari per te e per misurare la consegna e l’efficacia di tali annunci. Ciò include l’utilizzo di informazioni raccolte in precedenza sui tuoi interessi per selezionare annunci, elaborare dati su quali annunci sono stati mostrati, con quale frequenza sono stati mostrati, quando e dove sono stati mostrati e se hai intrapreso azioni relative all’annuncio, incluso ad esempio la selezione di un annuncio o l’acquisto. Questo non include Personalization, che è la raccolta e l’elaborazione di informazioni sull’utilizzo di questo servizio per personalizzare successivamente pubblicità e/o contenuti per te in altri contesti, come siti web o app, nel tempo.

DAA: la pubblicità comportamentale online non include le attività di Prime parti, Consegna degli annunci o Generazione di rapporti sugli annunci, o la pubblicità contestuale (ad esempio, la pubblicità basata sul contenuto della pagina web visitata, la visita corrente di un consumatore a una pagina web o una query di ricerca).

#### C7 {#c7}

Il contenuto nel sito è costituito da testo e immagini progettati per informare, educare o intrattenere e non creati per promuovere la vendita di beni o servizi. Spetta a te determinare lo scopo del contenuto, incluso se il contenuto si qualifica come pubblicità nativa. L&#39;etichetta C7 non copre gli annunci nel sito, che sono coperti dall&#39;etichetta [C6](#c6). I dati con etichetta C7 non possono essere utilizzati per il targeting di contenuti nel sito, inclusa la selezione e la distribuzione di contenuti sui siti web o sulle app della tua organizzazione, o per misurare la distribuzione e l’efficacia di tali contenuti. Ciò include informazioni raccolte in precedenza sugli interessi degli utenti in contenuti selezionati, l’elaborazione dei dati sul contenuto visualizzato, la frequenza o la durata della visualizzazione, quando e dove è stato visualizzato e se gli utenti hanno intrapreso azioni relative al contenuto, inclusa ad esempio la selezione del contenuto. In genere, trarre conclusioni sulle preferenze di un utente in base alle sue attività nel sito e quindi utilizzare tali preferenze nel targeting dei contenuti nel sito non si qualifica come targeting basato sugli interessi (o personalizzazione), in quanto non soddisfa tutti e tre i requisiti necessari per il targeting basato sugli interessi. *[Per i requisiti, vedere l&#39;etichetta C5.](#c5)*

In ultima analisi, spetta a te interpretare l’etichetta e come viene applicato l’utilizzo dei dati con tale etichetta. Per riferimento, di seguito sono riportati i framework IAB e DAA:

IAB: 4. Selezione, distribuzione e reporting dei contenuti: la raccolta di informazioni e la combinazione con le informazioni raccolte in precedenza, per selezionare e distribuire i contenuti e per misurare la distribuzione e l’efficacia di tali contenuti. Ciò include l’utilizzo di informazioni sugli interessi raccolte in precedenza per selezionare il contenuto, elaborare i dati su quale contenuto è stato visualizzato, la frequenza o la durata della visualizzazione, quando e dove è stato visualizzato e se l’utente ha intrapreso azioni relative al contenuto, inclusa ad esempio la selezione del contenuto. Questo non include Personalization, che è la raccolta e l’elaborazione di informazioni sull’utilizzo di questo servizio per personalizzare successivamente contenuti e/o pubblicità per te in altri contesti, come siti web o app, nel tempo.

DAA: la pubblicità comportamentale online non include le attività di Prime parti, Consegna degli annunci o Generazione di rapporti sugli annunci, né la pubblicità contestuale (ad esempio, la pubblicità basata sul contenuto della pagina web visitata, sulla visita corrente di un consumatore a una pagina web o su una query di ricerca).

#### C8 {#c8}

I dati non possono essere utilizzati per misurare, comprendere e generare rapporti sull’utilizzo da parte degli utenti dei siti o delle app della tua organizzazione. Questo non include il targeting basato sugli interessi (targeting tra siti), che è la raccolta di informazioni sull’utilizzo di questo servizio per personalizzare successivamente contenuti e/o pubblicità per te in altri contesti, ad esempio su altri servizi, come siti web o app, nel tempo.

#### C9 {#c9}

Alcuni contratti includono divieti espliciti sull’uso dei dati per la scienza dei dati. A volte queste sono formulate in termini che vietano l’uso di dati per l’intelligenza artificiale (IA), l’apprendimento automatico (ML) o la modellazione.

#### C10 {#c10}

Alcuni criteri di governance dei dati limitano l’utilizzo di dati di identità uniti per la personalizzazione. L’etichetta C10 viene applicata automaticamente ai tipi di pubblico se i loro criteri di unione utilizzano l’opzione &quot;Private Graph&quot; (grafico privato).

#### C11 {#c11}

Adobe Experience Platform Segment Match consente di abbinare i tipi di pubblico generati da Experience Platform con le preferenze di privacy e consenso, facilitando l’arricchimento dei profili e le informazioni a valle. L&#39;etichetta C11 indica i dati che non devono essere utilizzati nei processi [!DNL Segment Match]. Dopo aver determinato i set di dati e/o i campi da escludere da Segment Match e aggiunto di conseguenza l’etichetta C11, l’etichetta viene applicata automaticamente dal flusso di lavoro Segment Match.

#### C12 {#c12}

I dati con questa etichetta non possono essere esportati da Experience Platform in alcun modo. I campi etichettati C12 sono esclusi dai download CSV, dal consumo API e dai flussi di lavoro di attivazione.
