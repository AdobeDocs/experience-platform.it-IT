---
keywords: Experience Platform;home;argomenti popolari;governance dei dati;etichetta di utilizzo dati api;servizio criteri api;etichette di utilizzo dati supportate;etichette contratto;etichette identità;etichette sensibili
solution: Experience Platform
title: Glossario delle etichette di utilizzo dati
description: Questo documento illustra tutte le etichette di utilizzo dei dati attualmente supportate da Adobe Experience Platform.
exl-id: 70d0702d-def7-4ab2-a861-eaf0f0cde1d4
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '2108'
ht-degree: 1%

---

# Glossario delle etichette di utilizzo dei dati {#data-usage-labels-glossary}

>[!CONTEXTUALHELP]
>id="platform_policies_labeltype"
>title="Tipi di etichette"
>abstract="Esistono diverse categorie di etichette di utilizzo dei dati. Le etichette definite dall&#39;Adobe includono etichette di contratto, etichette di identità ed etichette sensibili. Le etichette definite dalla tua organizzazione sono classificate come etichette personalizzate."
>text="See the data usage labels glossary for more information on these label types."

Le etichette di utilizzo dei dati ti consentono di categorizzare set di dati e campi in base a [criteri di governance](../policies/overview.md) e [criteri di controllo dell’accesso](../../access-control/abac/overview.md) applicabili a tali dati. Adobe Experience Platform fornisce diverse etichette di utilizzo dei dati di base pronte all’uso che puoi utilizzare per iniziare a categorizzare i dati.

Questo documento illustra le etichette di utilizzo dei dati di base attualmente fornite da Experience Platform.

## Etichette contratto

Le etichette &quot;C&quot; del contratto vengono utilizzate per categorizzare i dati che hanno obblighi contrattuali o sono relativi ai criteri di governance dei dati della tua organizzazione.

| Etichetta | Definizione |
| --- | --- |
| [C1](#c1) | I dati possono essere esportati da Adobe Experience Cloud solo in un formato aggregato senza includere identificatori individuali o di dispositivo. |
| [C2](#c2) | I dati non possono essere esportati a terzi. |
| [C3](#c3) | I dati non possono essere combinati o altrimenti utilizzati con informazioni direttamente identificabili. |
| [C4](#c4) | I dati non possono essere utilizzati per il targeting di annunci o contenuti, né sul sito né tra siti diversi. |
| [C5](#c5) | I dati non possono essere utilizzati per il targeting tra siti di contenuti o annunci basato sugli interessi. |
| [C6](#c6) | I dati non possono essere utilizzati per il targeting di annunci nel sito. |
| [C7](#c7) | I dati non possono essere utilizzati per il targeting dei contenuti sul sito. |
| [C8](#c8) | I dati non possono essere utilizzati per la misurazione dei siti web o delle app della tua organizzazione. |
| [C9](#c9) | I dati non possono essere utilizzati nei flussi di lavoro di Data Science. |
| [C10](#c10) | I dati non possono essere utilizzati per l’attivazione di identità unite. |
| [C11](#c11) | I dati non possono essere condivisi con i partner Segment Match. |
| [C12](#c12) | I dati non possono essere esportati in alcun modo. |

## Etichette di identità

Le etichette di identità &quot;I&quot; vengono utilizzate per categorizzare i dati che possono identificare o contattare una persona specifica.

| Etichetta | Definizione |
| --- | --- |
| **I1** | Dati direttamente identificabili che possono identificare o contattare una persona specifica, anziché un dispositivo. |
| **I2** | Dati indirettamente identificabili che possono essere utilizzati in combinazione con altri dati per identificare o contattare una persona specifica. |

## Etichette per dati sensibili {#sensitive}

Le etichette sensibili &quot;S&quot; vengono utilizzate per categorizzare i dati considerati sensibili dall’utente e dall’organizzazione.

Un tipo di dati che si può considerare sensibile può essere diversi tipi di dati geografici; tuttavia, questa categoria non è limitata ai dati geografici.

| Etichetta | Definizione |
| --- | --- |
| **S1** | Dati che specificano latitudine e longitudine e che possono essere utilizzati per determinare la posizione esatta di un dispositivo. |
| **S2** | Dati che possono essere utilizzati per determinare un’area recintata in modo ampio. |
| **PSPD** | I dati personali sensibili consentiti (PSPD) si riferiscono a dati che, ai sensi del contratto, sono consentiti dall’Adobe per il caricamento di dati considerati &quot;sensibili&quot;, &quot;categorie speciali di dati&quot; o termini simili utilizzati dalle leggi applicabili. Ciò esclude specificamente le informazioni sanitarie protette (PHI) e altri dati sanitari regolamentati. |
| **RHD** | Dati che si riferiscono a informazioni protette sulla salute (PHI) o informazioni su un paziente che l&#39;essere Adobe può contrattualmente caricare. |

## Appendice

Le sezioni seguenti forniscono informazioni aggiuntive sulle etichette di utilizzo dei dati disponibili.

### Dettagli etichetta contratto

Le sezioni seguenti forniscono informazioni dettagliate relative all’attuazione di specifici contratti con l’etichetta &quot;C&quot;.

#### C1 {#c1}

Alcuni dati possono essere esportati da Adobe Experience Cloud solo in un modulo aggregato senza includere identificatori individuali o di dispositivo. Ad esempio, dati provenienti dai social network.

#### C2 {#c2}

Alcuni fornitori di dati hanno clausole nei loro contratti che vietano l’esportazione di dati da dove sono stati raccolti originariamente. Ad esempio, i contratti per social network spesso limitano il trasferimento dei dati che ricevi da loro. L&#39;etichetta C2 è più restrittiva di [C1](#c1), che richiede solo l&#39;aggregazione e dati anonimi, ma è meno restrittivo rispetto a [C12](#c12), che impedisce completamente le esportazioni di dati indipendentemente dalla destinazione.

#### C3 {#c3}

Alcuni fornitori di dati hanno clausole nei loro contratti che vietano la combinazione o l’uso di tali dati con informazioni direttamente identificabili. Ad esempio, i contratti per i dati provenienti da reti di annunci, server di annunci e fornitori di dati di terze parti spesso includono divieti contrattuali specifici sull’utilizzo di tali dati con dati direttamente identificabili.

#### C4 {#c4}

C4 comprende le etichette [C5](#c5), [C6](#c6), e [C7](#c7). È una delle etichette più restrittive, seconda solo a [C12](#c12).

#### C5 {#c5}

Il targeting basato sugli interessi, o personalizzazione, si verifica se sono soddisfatte le tre condizioni seguenti: i dati raccolti sul sito sono (1) utilizzati per trarre conclusioni sugli interessi di un utente, (2) utilizzati in un altro contesto, ad esempio su un altro sito o un’altra app (off-site) E (3) utilizzati per selezionare quali contenuti o annunci vengono distribuiti in base a tali conclusioni.

La combinazione di dati provenienti da diversi siti, compresa una combinazione di dati nel sito e dati esterni al sito o una combinazione di dati provenienti da diverse fonti esterne al sito, è definita dati intersito. Siti diversi rappresentano contesti diversi, in modo che l’utilizzo di dati tra siti diversi in qualsiasi contesto sia diverso dall’originale. I dati tra siti vengono generalmente raccolti ed elaborati per trarre conclusioni sugli interessi degli utenti. Di conseguenza, l’utilizzo di dati intersito per il targeting di annunci o contenuti si qualifica generalmente come targeting basato sugli interessi, indipendentemente dal fatto che l’annuncio o il contenuto venga visualizzato sul sito o fuori dal sito. Ad esempio, se i dati nel sito vengono utilizzati in combinazione con i dati esterni al sito per selezionare l’annuncio da mostrare a un utente sul sito di un’organizzazione, tale utilizzo si qualifica come targeting basato sugli interessi. Un altro esempio è che il retargeting degli annunci per utenti fuori dal sito probabilmente si qualificherebbe anche come targeting basato sugli interessi.

Anche l’utilizzo dei soli dati fuori sito per il targeting si qualificherebbe probabilmente come targeting basato sugli interessi, in quanto i dati esterni al sito vengono generalmente raccolti ed elaborati per trarre conclusioni sugli interessi degli utenti.

Tuttavia, il targeting di contenuti o annunci utilizzando solo i dati sul sito in genere non si qualifica come targeting basato sugli interessi. Il targeting sul sito che non è altrimenti qualificato come targeting basato su interessi è trattato come due etichette distinte. In particolare, Label C6 si occupa del targeting e del reporting degli annunci nel sito, in particolare della selezione, distribuzione e reporting degli annunci, mentre Label C7 si occupa della selezione, della consegna e del reporting dei contenuti nel sito (targeting dei contenuti nel sito).

In ultima analisi, spetta a te interpretare l’etichetta e come viene applicato l’utilizzo dei dati con tale etichetta. Per riferimento, di seguito sono riportati i framework IAB e DAA:

IAB: Personalization. La raccolta e l&#39;elaborazione di informazioni sull&#39;utilizzo di questo servizio per personalizzare successivamente pubblicità e/o contenuti per te in altri contesti, ad esempio su altri siti web o app, nel tempo. In genere, il contenuto del sito o dell’app viene utilizzato per trarre conclusioni sui tuoi interessi che informano la futura selezione di pubblicità e/o contenuti.

DAA: pubblicità comportamentale online. Raccogliere dati da un particolare computer o dispositivo riguardo ai comportamenti di visualizzazione web nel tempo e tra siti web non affiliati al fine di utilizzare tali dati per prevedere le preferenze o gli interessi degli utenti di fornire pubblicità a tale computer o dispositivo in base alle preferenze o agli interessi dedotti da tali comportamenti di visualizzazione web.

#### C6 {#c6}

Gli annunci sono messaggi o notifiche, inclusi testo e immagini, visualizzati su un sito web o un’app principalmente destinati a promuovere la vendita di beni o servizi. Spetta a te determinare lo scopo di tali messaggi o notifiche. Gli annunci sono separati dai contenuti nel sito, coperti dall’etichetta [C7](#c7). I dati con etichetta C6 non possono essere utilizzati per il targeting di annunci nel sito, inclusa la selezione e la consegna di annunci sui siti web o sulle app della tua organizzazione o per misurare la consegna e l’efficacia di tali annunci. Ciò include l’utilizzo di dati sul sito raccolti in precedenza sugli interessi degli utenti di selezionare annunci, elaborare dati su quali annunci pubblicitari sono stati mostrati, quando e dove sono stati mostrati e se gli utenti hanno intrapreso azioni relative all’annuncio, ad esempio la selezione di un annuncio o l’acquisto di un prodotto. In genere, trarre conclusioni sulle preferenze di un utente in base alle sue attività nel sito e quindi utilizzare tali preferenze nel targeting degli annunci nel sito non si qualifica come targeting basato sugli interessi (o personalizzazione), in quanto non soddisfa tutti e tre i requisiti necessari per il targeting basato sugli interessi. *[Vedere l&#39;etichetta C5 per questi requisiti.](#c5)*

In ultima analisi, spetta a te interpretare l’etichetta e come viene applicato l’utilizzo dei dati con tale etichetta. Per riferimento, di seguito sono riportati i framework IAB e DAA:

IAB: 3. Selezione, consegna e reporting degli annunci: la raccolta di informazioni e la combinazione con le informazioni raccolte in precedenza, per selezionare e distribuire annunci pubblicitari per te e per misurare la consegna e l’efficacia di tali annunci. Ciò include l’utilizzo di informazioni raccolte in precedenza sui tuoi interessi per selezionare annunci, elaborare dati su quali annunci sono stati mostrati, con quale frequenza sono stati mostrati, quando e dove sono stati mostrati e se hai intrapreso azioni relative all’annuncio, incluso ad esempio la selezione di un annuncio o l’acquisto. Ciò non include la Personalizzazione, ovvero la raccolta e l’elaborazione di informazioni sull’utilizzo di questo servizio per personalizzare successivamente pubblicità e/o contenuti per te in altri contesti, ad esempio siti web o app, nel tempo.

DAA: gli annunci comportamentali online non includono le attività di Prime parti, Consegna di annunci o Generazione di rapporti sugli annunci, né la pubblicità contestuale (ad esempio, la pubblicità basata sul contenuto della pagina web visitata, la visita corrente di un consumatore a una pagina web o una query di ricerca).

#### C7 {#c7}

Il contenuto nel sito è costituito da testo e immagini progettati per informare, educare o intrattenere e non creati per promuovere la vendita di beni o servizi. Spetta a te determinare lo scopo del contenuto, incluso se il contenuto si qualifica come pubblicità nativa. L’etichetta C7 non è destinata a coprire gli annunci in loco, che sono coperti dall’etichetta [C6](#c6). I dati con etichetta C7 non possono essere utilizzati per il targeting di contenuti nel sito, inclusa la selezione e la distribuzione di contenuti sui siti web o sulle app della tua organizzazione, o per misurare la distribuzione e l’efficacia di tali contenuti. Ciò include informazioni raccolte in precedenza sugli interessi degli utenti in contenuti selezionati, l’elaborazione dei dati sul contenuto visualizzato, la frequenza o la durata della visualizzazione, quando e dove è stato visualizzato e se gli utenti hanno intrapreso azioni relative al contenuto, inclusa ad esempio la selezione del contenuto. In genere, trarre conclusioni sulle preferenze di un utente in base alle sue attività nel sito e quindi utilizzare tali preferenze nel targeting dei contenuti nel sito non si qualifica come targeting basato sugli interessi (o personalizzazione), in quanto non soddisfa tutti e tre i requisiti necessari per il targeting basato sugli interessi. *[Vedere l&#39;etichetta C5 per questi requisiti.](#c5)*

In ultima analisi, spetta a te interpretare l’etichetta e come viene applicato l’utilizzo dei dati con tale etichetta. Per riferimento, di seguito sono riportati i framework IAB e DAA:

IAB: 4. Selezione, distribuzione e reporting dei contenuti: la raccolta di informazioni e la combinazione con le informazioni raccolte in precedenza, per selezionare e distribuire i contenuti e per misurare la distribuzione e l’efficacia di tali contenuti. Ciò include l’utilizzo di informazioni sugli interessi raccolte in precedenza per selezionare il contenuto, elaborare i dati su quale contenuto è stato visualizzato, la frequenza o la durata della visualizzazione, quando e dove è stato visualizzato e se l’utente ha intrapreso azioni relative al contenuto, inclusa ad esempio la selezione del contenuto. Ciò non include la Personalizzazione, ovvero la raccolta e l’elaborazione di informazioni sull’utilizzo di questo servizio per personalizzare successivamente contenuto e/o pubblicità per te in altri contesti, ad esempio siti web o app, nel tempo.

DAA: la pubblicità comportamentale online non include le attività di Prime parti, Consegna degli annunci o Generazione di rapporti sugli annunci, né la pubblicità contestuale (ad esempio, la pubblicità basata sul contenuto della pagina web visitata, sulla visita corrente di un consumatore a una pagina web o su una query di ricerca).

#### C8 {#c8}

I dati non possono essere utilizzati per misurare, comprendere e generare rapporti sull’utilizzo da parte degli utenti dei siti o delle app della tua organizzazione. Questo non include il targeting basato sugli interessi (targeting tra siti), che è la raccolta di informazioni sull’utilizzo di questo servizio per personalizzare successivamente contenuti e/o pubblicità per te in altri contesti, ad esempio su altri servizi, come siti web o app, nel tempo.

#### C9 {#c9}

Alcuni contratti includono divieti espliciti sull’uso dei dati per la scienza dei dati. A volte queste sono formulate in termini che vietano l’uso di dati per l’intelligenza artificiale (IA), l’apprendimento automatico (ML) o la modellazione.

#### C10 {#c10}

Alcuni criteri di governance dei dati limitano l’utilizzo di dati di identità uniti per la personalizzazione. L’etichetta C10 viene applicata automaticamente ai segmenti se i relativi criteri di unione utilizzano l’opzione &quot;Private Graph&quot;.

#### C11 {#c11}

Adobe Experience Platform Segment Match consente di abbinare segmenti di prime parti con preferenze di privacy e consenso, facilitando l’arricchimento dei profili e le informazioni a valle. L’etichetta C11 indica i dati che non devono essere utilizzati in [!DNL Segment Match] processi. Dopo aver determinato i set di dati e/o i campi da escludere da Segment Match e aggiunto di conseguenza l’etichetta C11, l’etichetta viene applicata automaticamente dal flusso di lavoro Segment Match.

#### C12 {#c12}

I dati con questa etichetta non possono essere esportati da Platform in alcun modo. I campi etichettati C12 sono esclusi dai download CSV, dal consumo API e dai flussi di lavoro di attivazione.
