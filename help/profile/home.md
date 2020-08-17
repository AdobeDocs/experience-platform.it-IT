---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Panoramica del profilo cliente in tempo reale
topic: guide
translation-type: tm+mt
source-git-commit: fa439ebb9d02d4a08c8ed92b18f2db819d089174
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 1%

---


# [!DNL Real-time Customer Profile]panoramica

Adobe Experience Platform consente di creare esperienze coordinate, coerenti e pertinenti per i clienti, indipendentemente da dove e quando interagiscono con il tuo marchio. Con [!DNL Real-time Customer Profile], puoi vedere una visualizzazione olistica di ogni singolo cliente che combina dati provenienti da più canali, inclusi online, offline, CRM e dati di terze parti. [!DNL Profile] consente di consolidare i diversi dati dei clienti in una visualizzazione unificata che offre un account utilizzabile e con marca temporale per ogni interazione con il cliente. Questa panoramica vi aiuterà a capire il ruolo e l’utilizzo di [!DNL Real-time Customer Profile] in [!DNL Experience Platform].

## Informazioni [!DNL Real-time Customer Profile]

[!DNL Real-time Customer Profile] è un archivio di entità di ricerca generico che unisce i dati da varie risorse di dati aziendali e fornisce l&#39;accesso a tali dati sotto forma di profili cliente individuali e relativi eventi delle serie temporali. Questa funzione consente agli esperti di marketing di promuovere esperienze coordinate, coerenti e pertinenti con il pubblico attraverso più canali.

### [!DNL Profile] data store

Anche se [!DNL Real-time Customer Profile] elabora i dati acquisiti e utilizza Adobe Experience Platform [!DNL Identity Service] per unire i dati correlati attraverso la mappatura dell&#39;identità, mantiene i propri dati nello [!DNL Profile] store. In altre parole, lo [!DNL Profile] store è separato dai [!DNL Catalog] dati ([!DNL Data Lake]) e [!DNL Identity Service] dai dati (grafico dell&#39;identità).

### [!DNL Profile] e [!DNL Platform] servizi

La relazione tra [!DNL Real-time Customer Profile] e altri servizi all&#39;interno [!DNL Experience Platform] è evidenziata nel diagramma seguente:

![Relazione tra Profilo e altri servizi  Experience Platform.](images/profile-overview/profile-in-platform.png)

### Profili e dati record

Un profilo è una rappresentazione di un soggetto, un&#39;organizzazione o un individuo, detti anche dati di record. Ad esempio, il profilo di un prodotto può includere uno SKU e una descrizione, mentre il profilo di una persona contiene informazioni come nome, cognome e indirizzo e-mail. Utilizzando [!DNL Experience Platform]questa opzione, puoi personalizzare i profili in modo da utilizzare tipi di dati rilevanti per la tua attività. La classe standard [!DNL Experience Data Model] (XDM) [!DNL Individual Profile] è la classe preferita sulla quale creare uno schema per la descrizione dei dati del record cliente e fornisce i dati integrali a molte interazioni tra i servizi della piattaforma. Per ulteriori informazioni sull&#39;utilizzo degli schemi in [!DNL Experience Platform], iniziare leggendo la panoramica [del sistema](../xdm/home.md)XDM.

### Eventi delle serie temporali

I dati delle serie temporali forniscono un&#39;istantanea del sistema nel momento in cui un&#39;azione è stata eseguita direttamente o indirettamente da un soggetto, nonché i dati che descrivono l&#39;evento stesso. Rappresentata dalla classe di schema standard XDM ExperienceEvent, i dati delle serie temporali possono descrivere eventi quali elementi aggiunti a un carrello, collegamenti su cui si fa clic e video visualizzati. I dati delle serie temporali possono essere utilizzati per basare le regole di segmentazione su e gli eventi possono essere accessibili individualmente nel contesto di un profilo.

### Identità

Ogni azienda vuole comunicare con i propri clienti in un modo che si senta personale. Tuttavia, una delle sfide poste dalla distribuzione di esperienze digitali rilevanti ai clienti è capire come collegare i dati disconnessi, che spesso si diffondono tra canali digitali diversi come tablet, telefoni cellulari e laptop. [!DNL Identity Service] consente di mettere insieme l&#39;immagine completa del cliente collegando identità da più canali, creando un grafico dell&#39;identità per ogni cliente, per comprenderle meglio. Per ulteriori informazioni, visita la panoramica [del servizio](../identity-service/home.md) identità.

### Segmentazione

Adobe Experience Platform [!DNL Segmentation Service] produce i tipi di pubblico necessari per fornire esperienze ai singoli clienti. Quando viene creato un segmento di pubblico, l&#39;ID di tale segmento viene aggiunto all&#39;elenco delle appartenenze del segmento per tutti i profili idonei. Le regole dei segmenti sono create e applicate ai [!DNL Real-time Customer Profile] dati utilizzando le API RESTful e l&#39;interfaccia utente di Generatore di segmenti. Per ulteriori informazioni sulla segmentazione, consultare la panoramica [del servizio di](../segmentation/home.md)segmentazione.

### Frammenti di profilo e schemi di unione {#profile-fragments-and-union-schemas}

Una delle caratteristiche chiave di [!DNL Real-time Customer Profile] è la capacità di unificare i dati multicanale. Quando [!DNL Real-time Customer Profile] viene utilizzato per accedere a un&#39;entità, può fornire una visualizzazione unita di tutti i frammenti di profilo per tale entità tra i set di dati, detta visualizzazione unione e resa possibile attraverso ciò che è noto come schema unione. [!DNL Real-time Customer Profile] i dati vengono uniti tra le origini quando l&#39;ID di un&#39;entità o di un profilo vi consente di accedervi o di esportarli come segmento. Per ulteriori informazioni sull&#39;accesso ai profili e alle visualizzazioni di unione tramite l&#39; [!DNL Real-time Customer Profile] API, visita la guida [all&#39;endpoint](api/entities.md)entità.

### Unisci criteri

Quando si uniscono i dati da più origini e si combinano per visualizzare una visualizzazione completa di ciascuno dei singoli clienti, i criteri di unione sono le regole che [!DNL Platform] vengono utilizzate per determinare in che modo i dati verranno assegnati alle priorità e quali verranno combinati per creare tale visualizzazione unificata. Utilizzando le API RESTful o l&#39;interfaccia utente, puoi creare nuovi criteri di unione, gestire i criteri esistenti e impostare un criterio di unione predefinito per la tua organizzazione. Per ulteriori informazioni sull&#39;utilizzo dei criteri di unione tramite l&#39; [!DNL Real-time Customer Profile] API, vedere la guida [dell&#39;endpoint dei criteri di](api/merge-policies.md)unione. Per utilizzare i criteri di unione utilizzando l&#39; [!DNL Experience Platform] interfaccia utente, fare riferimento alla guida [utente dei criteri di](ui/merge-policies.md)unione.

### (Alfa) Configurare gli attributi calcolati

>[!IMPORTANT]
>La funzionalità degli attributi calcolati descritta in questo documento è in alfa. La documentazione e la funzionalità sono soggette a modifiche.

Gli attributi calcolati consentono di calcolare automaticamente il valore dei campi in base ad altri valori, calcoli ed espressioni. Gli attributi calcolati operano a livello di profilo, il che significa che puoi aggregare i valori per tutti i record ed eventi. Ogni attributo calcolato contiene un&#39;espressione, o &quot;regola&quot;, che valuta i dati in arrivo e memorizza il valore risultante in un attributo di profilo o in un evento. Questi calcoli consentono di rispondere facilmente a domande relative a cose come il valore di acquisto del ciclo di vita, il tempo tra acquisti o il numero di aperture di applicazioni, senza che sia necessario eseguire manualmente calcoli complessi ogni volta che le informazioni sono necessarie. Per ulteriori informazioni sugli attributi calcolati e istruzioni dettagliate per utilizzarli tramite l&#39; [!DNL Real-time Customer Profile] API, consultate la guida [all&#39;endpoint degli attributi](api/computed-attributes.md)calcolati. Questa guida ti aiuterà a comprendere meglio il ruolo che gli attributi calcolati giocano in Adobe Experience Platform e include chiamate API di esempio per eseguire operazioni CRUD di base.

## Componenti in tempo reale

Questa sezione introduce i componenti che consentono [!DNL Real-time Customer Profile] di aggiornare e monitorare dati di record e serie temporali in tempo reale.

### Streaming dell’assimilazione e segmentazione in streaming

L&#39;ingresso in tempo reale è possibile attraverso un processo chiamato caricamento in streaming. Durante l&#39;assimilazione dei dati di profilo e serie temporale, [!DNL Real-time Customer Profile] decide automaticamente di includere o escludere tali dati dai segmenti attraverso un processo continuo denominato segmentazione in streaming, prima di unirli ai dati esistenti e di aggiornare la visualizzazione unione. Di conseguenza, puoi eseguire istantaneamente dei calcoli e prendere decisioni per offrire esperienze personalizzate e avanzate ai clienti mentre interagiscono con il tuo marchio. Durante l&#39;assimilazione, i dati vengono anche sottoposti a convalida per assicurarsi che vengano assimilati correttamente e conformi allo schema su cui si basa il dataset. Per ulteriori informazioni sulle operazioni di convalida effettuate durante l&#39;assimilazione, consultare la panoramica [sulla qualità dell&#39;assimilazione dei](../ingestion/quality/overview.md)dati.

### Configurazioni e destinazioni di proiezione Edge

Al fine di promuovere esperienze coordinate, coerenti e personalizzate per i clienti attraverso più canali in tempo reale, i dati giusti devono essere prontamente disponibili e costantemente aggiornati man mano che si verificano le modifiche. Adobe Experience Platform consente l&#39;accesso in tempo reale ai dati tramite l&#39;utilizzo di ciò che è noto come edge. Un server periferico è un server collocato geograficamente che memorizza i dati e li rende facilmente accessibili alle applicazioni. Ad esempio,  applicazioni di Adobe come  Adobe Target e  Adobe Campaign utilizzano i bordi per fornire esperienze personalizzate ai clienti in tempo reale. I dati vengono indirizzati a un bordo da una proiezione, con una destinazione di proiezione che definisce il bordo a cui verranno inviati i dati, e una configurazione di proiezione che definisce le informazioni specifiche che verranno rese disponibili sul bordo. Per saperne di più e iniziare a lavorare con le proiezioni utilizzando l&#39; [!DNL Real-time Customer Profile] API, fare riferimento alla guida [endpoint di proiezione](api/edge-projections.md)edge.

## Aggiungi dati a [!DNL Real-time Customer Profile]

[!DNL Platform] può essere configurato per inviare i dati del record e della serie temporale a [!DNL Profile], per supportare l’assimilazione in tempo reale dei flussi e l’assimilazione batch. Per ulteriori informazioni, consulta l’esercitazione che illustra come [aggiungere dati al profilo](tutorials/add-profile-data.md)cliente in tempo reale.

>[!NOTE]
>
>I dati raccolti attraverso  soluzioni di Adobe, inclusi [!DNL Analytics Cloud][!DNL Marketing Cloud], e [!DNL Advertising Cloud], fluiscono [!DNL Experience Platform] e vengono ingeriti [!DNL Profile].

### [!DNL Profile] metriche di assimilazione

Observability Insights consente di esporre le metriche chiave in Adobe Experience Platform. Oltre alle statistiche di [!DNL Platform] utilizzo e agli indicatori di prestazioni per diverse [!DNL Platform] funzionalità, sono disponibili metriche [!DNL Profile]correlate specifiche che consentono di conoscere i tassi di richieste in entrata, i tassi di acquisizione di successo, le dimensioni dei record acquisiti e altro ancora. Per saperne di più, leggi innanzitutto la panoramica [](../observability/home.md)Approfondimenti sull&#39;osservazione e per un elenco completo delle [!DNL Profile] metriche, consulta la documentazione sulle metriche [](../observability/metrics.md)disponibili.

## [!DNL Data governance] ed [!DNL Privacy]

[!DNL Data governance] è una serie di strategie e tecnologie utilizzate per gestire i dati dei clienti e garantire la conformità a normative, restrizioni e politiche applicabili all&#39;uso dei dati.

Per quanto riguarda l&#39;accesso ai dati, la governance dei dati svolge un ruolo chiave a [!DNL Experience Platform] vari livelli:
* Etichettatura dell&#39;uso dei dati
* Criteri di accesso ai dati
* Controllo dell&#39;accesso ai dati per le azioni di marketing

[!DNL Data governance] è gestito in diversi punti. Tra queste, puoi decidere in quali dati vengono acquisiti [!DNL Platform] e quali dati sono accessibili dopo l’assimilazione per una determinata azione di marketing. Per ulteriori informazioni, iniziare leggendo la panoramica sulla governance dei [dati](../data-governance/home.md).

### Gestione delle richieste di privacy e rinuncia ai dati

[!DNL Experience Platform] consente ai clienti di inviare richieste di rifiuto relative all&#39;utilizzo e all&#39;archiviazione dei loro dati all&#39;interno [!DNL Real-time Customer Profile]. Per ulteriori informazioni sulla gestione delle richieste di rifiuto, consultate la documentazione relativa al [rispetto delle richieste](../segmentation/honoring-opt-outs.md)di rifiuto.

## [!DNL Profile] linee guida

[!DNL Experience Platform] ha una serie di linee guida da seguire per un uso efficace [!DNL Profile].

| Sezione | Bordo |
| ------- | -------- |
| [!DNL Profile] schema unione | Un massimo di **20** set di dati può contribuire allo schema [!DNL Profile] unione. |
| Relazioni tra più entità | È possibile creare un massimo di **5** relazioni tra più entità. |
| Profondità JSON per associazione multi-entità | La profondità massima JSON è **4**. |
| Dati serie temporali | I dati delle serie temporali **non** sono consentiti nelle entità [!DNL Profile] per utenti diversi. |
| Relazioni tra schemi non persone | Le relazioni di schema non-people **non** sono consentite. |
| Frammento profilo | La dimensione massima consigliata per un frammento di profilo è **10 kB**.<br><br> La dimensione massima assoluta di un frammento di profilo è **1 MB**. |
| Entità non personale | La dimensione totale massima per una singola entità non-persona è **200 MB**. |
| Set di dati per entità non-persona | Un massimo di **1** dataset può essere associato a un&#39;entità non-persona. |

<!--
| Section | Boundary | Enforcement |
| ------- | -------- | ----------- |
| Profile union schema | A maximum of **20** datasets can contribute to the Profile union schema. | A message stating you've reached the maximum number of datasets appears. You must either disable or clean up other obsolete datasets in order to create a new dataset. |
| Multi-entity relationships | A maximum of **5** multi-entity relationship can be created. | A message stating all available mappings have been used appears when the fifth relationship is mapped. An error message letting you know you have exceeded the number of available mappings appears when attempting to map a sixth relationship. | 
| JSON depth for multi-entity association | The maximum JSON depth is **4**. | When trying to use the relationship selector with a field that is more than four levels deep, an error message appears, stating it is ineligible for multi-entity association. |
| Time series data | Time-series data is **not** permitted in Profile for non-people entities. | A message stating that this data cannot be enabled for Profile because it is of an unsupported type appears. |
| Non-people schema relationships | Non-people schema relationships are **not** permitted. | Relationships between two non-people schemas cannot be created. The relationships checkbox will be disabled. |
| Profile fragment | The recommended maximum size of a profile fragment is **10kB**.<br><br> The absolute maximum size of a profile fragment is **1MB**. | If you upload a fragment that is larger than 10kB, a warning appears, stating that performance may be degraded since the fragment exceeds the recommended maximum working size.<br><br> If you upload a fragment that is larger than 1MB, ingestion will fail, and an alert letting you know that records have failed will be sent. |
| Non-person entity | The maximum total size for a single non-person entity is **200MB**. | If you load an object as a non-person entity that is larger than 200MB, an alert will appear, stating that the entity has exceeded the maximum allowable size and will not be useable for segmentation. |
| Datasets per non-person entity | A maximum of **1** dataset can be associated to a non-person entity. | If you try to create a second dataset that is associated to the same non-person entity, an error appears, stating that only one dataset can be active per non-person entity. |

--->

>[!NOTE]
>
>
>Un&#39;entità non-persona fa riferimento a qualsiasi classe XDM che **non** fa parte di [!DNL Profile].

## Passaggi successivi e risorse aggiuntive

Per saperne di più [!DNL Real-time Customer Profile], continuate a leggere la documentazione e completate le vostre lezioni guardando il video sottostante o esplorando altre esercitazioni video [Experience Platform](https://docs.adobe.com/content/help/en/platform-learn/tutorials/overview.html).

>[!WARNING]
>L’ [!DNL Platform] interfaccia utente mostrata nel video seguente non è aggiornata. Consulta la guida [utente Profilo cliente](ui/user-guide.md) in tempo reale per informazioni sulle ultime funzionalità e videate dell&#39;interfaccia utente.

>[!VIDEO](https://video.tv.adobe.com/v/27251?quality=12)