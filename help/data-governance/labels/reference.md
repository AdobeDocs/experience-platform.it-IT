---
keywords: Experience Platform;home;argomenti popolari;governance dei dati;api dell'etichetta di utilizzo dei dati;api del servizio criteri;etichette di utilizzo dei dati supportate;etichette di contratto;etichette di identità;etichette sensibili
solution: Experience Platform
title: Glossario delle etichette di utilizzo dei dati
topic-legacy: labels
description: Questo documento delinea tutte le etichette di utilizzo dei dati attualmente supportate da Adobe Experience Platform.
exl-id: 70d0702d-def7-4ab2-a861-eaf0f0cde1d4
source-git-commit: 1ab97c63bc169965ca759f2dd8b411c175559fb8
workflow-type: tm+mt
source-wordcount: '2083'
ht-degree: 2%

---

# Glossario delle etichette di utilizzo dei dati {#data-usage-labels-glossary}

>[!CONTEXTUALHELP]
>id="platform_policies_labeltype"
>title="Tipi di etichette"
>abstract="Esistono diverse categorie di etichette di utilizzo dei dati. Le etichette definite in Adobe includono etichette di contratto, etichette di identità ed etichette sensibili. Le etichette definite dall&#39;organizzazione vengono classificate come etichette personalizzate."
>text="See the data usage labels glossary for more information on these label types."

Le etichette di utilizzo dei dati ti consentono di classificare set di dati e campi in base ai criteri di utilizzo applicati a tali dati. La governance dei dati di Adobe Experience Platform fornisce diverse etichette di utilizzo dei dati di base pronte all’uso che puoi utilizzare per iniziare a categorizzare i tuoi dati.

Questo documento delinea le etichette di utilizzo dei dati di base attualmente fornite da [!DNL Experience Platform]. Ulteriori informazioni sulla governance dei dati sono disponibili nella sezione [Panoramica sulla governance dei dati](../home.md).

## Etichette per i contratti

Le etichette &quot;C&quot; del contratto vengono utilizzate per classificare i dati che hanno obblighi contrattuali o sono correlati alle politiche di governance dei dati della tua organizzazione.

| Etichetta | Definizione |
| --- | --- |
| **C1** | I dati possono essere esportati solo da Adobe Experience Cloud in forma aggregata senza includere identificatori individuali o di dispositivi. [Ulteriori informazioni...](#c1) |
| **C2** | I dati non possono essere esportati in terze parti. [Ulteriori informazioni...](#c2) |
| **C3** | I dati non possono essere combinati o altrimenti utilizzati con informazioni direttamente identificabili. [Ulteriori informazioni...](#c3) |
| **C4** | I dati non possono essere utilizzati per il targeting di annunci o contenuti, sia sul sito che tra siti diversi. [Ulteriori informazioni...](#c4) |
| **C5** | I dati non possono essere utilizzati per il targeting intersito basato su interessi di contenuti o annunci. [Ulteriori informazioni...](#c5) |
| **C6** | I dati non possono essere utilizzati per il targeting degli annunci sul sito. [Ulteriori informazioni...](#c6) |
| **C7** | I dati non possono essere utilizzati per il targeting sul sito del contenuto. [Ulteriori informazioni...](#c7) |
| **C8** | I dati non possono essere utilizzati per la misurazione dei siti web o delle app dell’organizzazione. [Ulteriori informazioni...](#c8) |
| **C9** | I dati non possono essere utilizzati nei flussi di lavoro Data Science. [Ulteriori informazioni...](#c9) |
| **C10** | I dati non possono essere utilizzati per l&#39;attivazione di identità unita. [Ulteriori informazioni...](#c10) |
| **C11** | I dati non possono essere condivisi con i partner di corrispondenza dei segmenti. [Ulteriori informazioni...](#c11) |

## Etichette di identità

Le etichette di identità &quot;I&quot; vengono utilizzate per classificare i dati che possono identificare o contattare una persona specifica.

| Etichetta | Definizione |
| --- | --- |
| **I1** | Dati direttamente identificabili che possono identificare o contattare una persona specifica, anziché un dispositivo. |
| **I2** | Dati indirettamente identificabili che possono essere utilizzati in combinazione con qualsiasi altro dato per identificare o contattare una persona specifica. |

## Etichette sensibili {#sensitive}

Le etichette &quot;S&quot; sensibili vengono utilizzate per classificare i dati che tu e la tua organizzazione consideri sensibili.

Un tipo di dati che si può considerare sensibili può essere di diversi tipi di dati geografici; tuttavia, questa categoria non si limita ai dati geografici.

| Etichetta | Definizione |
| --- | --- |
| **S1** | Dati che specificano latitudine e longitudine utilizzabili per determinare la posizione precisa di un dispositivo. |
| **S2** | Dati che possono essere utilizzati per determinare un&#39;area geografica ampiamente definita. |
| **PSPD** | Dati personali sensibili consentiti (PSPD) si riferisce a dati che sono contrattualmente autorizzati dall’Adobe a caricare che sono considerati &quot;sensibili&quot;, &quot;categorie speciali di dati&quot; o un termine simile utilizzato dalle leggi applicabili. Ciò esclude specificamente le informazioni sulla salute protetta (PHI) e altri dati sanitari regolamentati. |
| **RHD** | Dati che si riferiscono a informazioni sulla salute protetta (PHI) o informazioni su un paziente che l&#39;Adobe consente contrattualmente di caricare. |

## Appendice

Le sezioni seguenti forniscono informazioni aggiuntive sulle etichette di utilizzo dei dati disponibili.

### Dettagli etichetta contratto

Le sezioni seguenti forniscono informazioni dettagliate relative all&#39;attuazione di etichette specifiche per i contratti &quot;C&quot;.

#### C1 {#c1}

Alcuni dati possono essere esportati solo da Adobe Experience Cloud in forma aggregata senza includere identificatori di dispositivi o singoli. Ad esempio, i dati provenienti dai social network.

#### C2 {#c2}

Alcuni fornitori di dati hanno termini nei loro contratti che vietano l&#39;esportazione di dati da dove sono stati originariamente raccolti. Ad esempio, i contratti di social network spesso limitano il trasferimento dei dati che ricevi da loro. L&#39;etichetta C2 è più restrittiva di [C1](#c1), che richiede solo l’aggregazione e dati anonimi.

#### C3 {#c3}

Alcuni fornitori di dati hanno termini nei loro contratti che vietano la combinazione o l&#39;uso di tali dati con informazioni direttamente identificabili. Ad esempio, i contratti per i dati provenienti da reti di annunci, server di annunci e fornitori di dati di terze parti spesso includono specifici divieti contrattuali sull&#39;uso di tali dati con dati direttamente identificabili.

#### C4 {#c4}

C4 è l&#39;etichetta più restrittiva - include le etichette [C5](#c5), [C6](#c6)e [C7](#c7).

#### C5 {#c5}

Il targeting basato sugli interessi, o personalizzazione, si verifica se sono soddisfatte le tre condizioni seguenti: I dati raccolti sul sito sono (1) utilizzati per fare deduzioni sugli interessi degli utenti, (2) viene utilizzato in un altro contesto, ad esempio su un altro sito o un&#39;app (fuori sito) E (3) viene utilizzato per selezionare quali contenuti o annunci vengono serviti in base a tali deduzioni.

La combinazione di dati provenienti da più siti, compresa una combinazione di dati in loco e dati fuori sito o una combinazione di dati provenienti da più fonti esterne al sito, è definita dati intersito. Siti diversi rappresentano contesti diversi in modo tale che l’utilizzo di dati intersito in qualsiasi contesto sia diverso dall’originale. I dati intersito vengono in genere raccolti ed elaborati per fare deduzioni sugli interessi degli utenti. Di conseguenza, l’utilizzo di dati intersito per il targeting di annunci o contenuti si qualifica in genere come targeting basato sugli interessi, indipendentemente dal fatto che l’annuncio o il contenuto siano visualizzati sul sito o fuori dal sito. Ad esempio, se i dati sul sito sono stati utilizzati insieme ai dati fuori sede per selezionare l’annuncio da mostrare a un utente sul sito di un’organizzazione, tale utilizzo si qualifica come targeting basato sugli interessi. Un altro esempio è rappresentato dal fatto che il retargeting degli annunci agli utenti fuori sede potrebbe essere qualificato come targeting basato sugli interessi.

L’utilizzo dei soli dati fuori sede per il targeting potrebbe anche essere considerato un targeting basato sugli interessi, in quanto i dati fuori sede vengono solitamente raccolti ed elaborati per fare deduzioni sugli interessi degli utenti.

Tuttavia, il targeting di contenuti o annunci che utilizzano solo dati sul sito non si qualifica in genere come targeting basato sugli interessi. Il targeting in sito che altrimenti non è qualificato come targeting basato sugli interessi viene trattato come due etichette distinte. In particolare, Label C6 riguarda il targeting e il reporting degli annunci sul sito e parla in modo specifico di selezione, consegna e reporting degli annunci, e Label C7 indica gli indirizzi per la selezione, la consegna e il reporting dei contenuti sul sito (targeting dei contenuti sul sito).

In definitiva, spetta a te interpretare l&#39;etichetta e come viene applicato l&#39;uso dei dati con quell&#39;etichetta. Per riferimento, i framework IAB e DAA sono forniti di seguito:

IAB: Personalizzazione. La raccolta e l&#39;elaborazione di informazioni sull&#39;utilizzo di questo servizio per personalizzare successivamente pubblicità e/o contenuti per l&#39;utente in altri contesti, ad esempio su altri siti web o applicazioni, nel tempo. In genere, il contenuto del sito o dell’app viene utilizzato per fare deduzioni sui tuoi interessi che informano la selezione futura di pubblicità e/o contenuti.

DAA: Comunicazioni comportamentali on-line. Raccolta di dati da un determinato computer o dispositivo relativi a comportamenti di visualizzazione web nel tempo e su siti web non affiliati allo scopo di utilizzare tali dati per prevedere le preferenze o gli interessi degli utenti per la distribuzione di pubblicità a quel computer o dispositivo in base a preferenze o interessi dedotti da tali comportamenti di visualizzazione web.

#### C6 {#c6}

Gli annunci sono messaggi o notifiche, compresi testo e immagini, che compaiono su un sito web o un&#39;app e sono destinati principalmente a promuovere la vendita di beni o servizi. Spetta a te determinare lo scopo di tali messaggi o notifiche. Gli annunci sono separati dal contenuto sul sito, coperti dall’etichetta [C7](#c7). I dati con un&#39;etichetta C6 non possono essere utilizzati per il targeting degli annunci in sito, inclusa la selezione e la consegna di annunci pubblicitari sui siti web o sulle app della tua organizzazione o per misurare la consegna e l&#39;efficacia di tali annunci. Ciò include l&#39;utilizzo di dati precedentemente raccolti sul sito relativi agli interessi degli utenti per selezionare gli annunci, elaborare i dati su cosa gli annunci sono stati mostrati, quando e dove sono stati mostrati, e se gli utenti hanno preso qualsiasi azione correlata all&#39;annuncio, come la selezione di un annuncio o l&#39;effettuazione di un acquisto. In genere, fare deduzioni sulle preferenze degli utenti in base alle attività in loco degli utenti e quindi utilizzare tali preferenze nel targeting degli annunci in sito non si qualifica come targeting basato sugli interessi (o personalizzazione), in quanto non soddisferebbe tutti e tre i requisiti necessari per il targeting basato sugli interessi. *[Cfr. l&#39;etichetta C5 per questi requisiti.](#c5)*

In definitiva, spetta a te interpretare l&#39;etichetta e come viene applicato l&#39;uso dei dati con quell&#39;etichetta. Per riferimento, i framework IAB e DAA sono forniti di seguito:

IAB: 3. Selezione, consegna, reporting di annunci: La raccolta di informazioni, e la combinazione con le informazioni raccolte in precedenza, per selezionare e consegnare pubblicità per voi, e per misurare la consegna e l&#39;efficacia di tali pubblicità. Ciò include l&#39;utilizzo di informazioni raccolte in precedenza sui tuoi interessi per selezionare gli annunci, l&#39;elaborazione di dati su quali annunci sono stati mostrati, la frequenza con cui sono stati visualizzati, quando e dove sono stati visualizzati e se hai intrapreso azioni relative all&#39;annuncio, ad esempio selezionando un annuncio o effettuando un acquisto. Ciò non include Personalizzazione, ovvero la raccolta e l&#39;elaborazione di informazioni sull&#39;utilizzo di questo servizio per personalizzare successivamente pubblicità e/o contenuti per l&#39;utente in altri contesti, come siti web o app, nel tempo.

DAA: La pubblicità comportamentale online non include le attività di Prime parti, di Ad Delivery o di Ad Reporting o di pubblicità contestuale (ad esempio pubblicità basata sul contenuto della pagina web visitata, la visita corrente del consumatore a una pagina web o una query di ricerca).

#### C7 {#c7}

Il contenuto in sito è testo e immagini progettati per informare, educare o intrattenere e non creati per promuovere la vendita di beni o servizi. Spetta a te determinare lo scopo del contenuto, compreso se il contenuto potrebbe essere qualificato come pubblicità nativa. L&#39;etichetta C7 non è destinata a coprire gli annunci in loco che sono coperti dall&#39;etichetta [C6](#c6). I dati con un’etichetta C7 non possono essere utilizzati per il targeting dei contenuti sul sito, inclusa la selezione e la consegna di contenuti sui siti web o sulle app della tua organizzazione, o per misurare la consegna e l’efficacia di tali contenuti. Ciò include informazioni raccolte in precedenza sugli interessi degli utenti in contenuti selezionati, l’elaborazione di dati su quale contenuto è stato visualizzato, quanto spesso o per quanto tempo è stato visualizzato, quando e dove è stato visualizzato, e se gli utenti hanno intrapreso azioni relative al contenuto, ad esempio la selezione del contenuto. Generalmente, fare deduzioni sulle preferenze degli utenti in base alle attività in loco degli utenti e quindi utilizzare tali preferenze nel targeting dei contenuti in sito non si qualifica come targeting basato sugli interessi (o personalizzazione), in quanto non soddisferebbe tutti e tre i requisiti necessari per il targeting basato sugli interessi. *[Cfr. l&#39;etichetta C5 per questi requisiti.](#c5)*

In definitiva, spetta a te interpretare l&#39;etichetta e come viene applicato l&#39;uso dei dati con quell&#39;etichetta. Per riferimento, i framework IAB e DAA sono forniti di seguito:

IAB: 4. Selezione del contenuto, consegna, reporting: La raccolta di informazioni e la combinazione con le informazioni raccolte in precedenza, per selezionare e distribuire contenuti al posto tuo e per misurare la consegna e l’efficacia di tali contenuti. Ciò include l’utilizzo di informazioni raccolte in precedenza sugli interessi per selezionare il contenuto, l’elaborazione di dati su quale contenuto è stato visualizzato, la frequenza o il tempo di visualizzazione, quando e dove è stato visualizzato, e se sono state intraprese azioni relative al contenuto, ad esempio la selezione del contenuto. Non include Personalizzazione, ovvero la raccolta e l&#39;elaborazione di informazioni sull&#39;utilizzo di questo servizio per personalizzare successivamente i contenuti e/o la pubblicità in altri contesti, come siti web o app, nel tempo.

DAA: La pubblicità comportamentale online non include le attività di Prime parti, di Ad Delivery o Ad Reporting o di pubblicità contestuale (ad esempio pubblicità basata sul contenuto della pagina web in visita, la visita corrente del consumatore a una pagina web o una query di ricerca).

#### C8 {#c8}

I dati non possono essere utilizzati per misurare, comprendere e creare rapporti sull&#39;utilizzo dei siti o delle app da parte degli utenti dell&#39;organizzazione. Questo non include il targeting basato sugli interessi (targeting intersito), ovvero la raccolta di informazioni sull’utilizzo di questo servizio per personalizzare successivamente contenuti e/o pubblicità in altri contesti, ad esempio su altri servizi, come siti web o app, nel tempo.

#### C9 {#c9}

Alcuni contratti includono divieti espliciti sull&#39;uso dei dati per la scienza dei dati. A volte tali termini sono formulati in termini che vietano l’uso di dati per l’intelligenza artificiale (AI), l’apprendimento automatico (ML) o la modellazione.

#### C10 {#c10}

Alcuni criteri di utilizzo dei dati limitano l’utilizzo di dati di identità uniti per la personalizzazione. L’etichetta C10 viene applicata automaticamente ai segmenti se i relativi criteri di unione utilizzano l’opzione &quot;grafico privato&quot;.

#### C11 {#c11}

Adobe Experience Platform Segment Match consente di associare segmenti di prime parti con preferenze di privacy e consenso, facilitando l’arricchimento dei profili e delle informazioni a valle. L’etichetta C11 indica i dati che non devono essere utilizzati in [!DNL Segment Match] processi. Dopo aver determinato quali set di dati e/o campi si desidera escludere da Segment Match (Confronta segmento) e aggiunto di conseguenza l’etichetta C11, l’etichetta viene applicata automaticamente dal flusso di lavoro Segment Match (Corrispondenza segmento).
