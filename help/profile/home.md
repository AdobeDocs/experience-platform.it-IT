---
keywords: ', Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;profilo unificato;profilo unificato;unificato;Profilo;rtcp;XDM, grafici'
title: Panoramica del profilo cliente in tempo reale
topic: guide
description: Profilo cliente in tempo reale è un archivio di entità di ricerca generico che unisce i dati da varie risorse di dati aziendali e fornisce l'accesso a tali dati sotto forma di profili cliente individuali ed eventi serie temporali correlati. Questa funzione consente agli esperti di marketing di promuovere esperienze coordinate, coerenti e pertinenti con il pubblico attraverso più canali.
translation-type: tm+mt
source-git-commit: e6ecc5dac1d09c7906aa7c7e01139aa194ed662b
workflow-type: tm+mt
source-wordcount: '1883'
ht-degree: 1%

---


# [!DNL Real-time Customer Profile]panoramica

Adobe Experience Platform consente di creare esperienze coordinate, coerenti e pertinenti per i clienti, indipendentemente da dove e quando interagiscono con il tuo marchio. Con [!DNL Real-time Customer Profile], puoi vedere una visione olistica di ciascun cliente combinando dati da più canali, inclusi online, offline, CRM e di terze parti. [!DNL Profile] consente di consolidare i dati dei clienti in una visualizzazione unificata che offre un account utilizzabile e con marca temporale per ogni interazione con il cliente. Questa panoramica ti aiuterà a capire il ruolo e l&#39;uso di [!DNL Real-time Customer Profile] in [!DNL Experience Platform].

## [!DNL Profile] in  Experience Platform

Il rapporto tra Profilo cliente in tempo reale e altri servizi all&#39;interno  Experience Platform è evidenziato nel diagramma seguente:

![](images/profile-overview/profile-in-platform.png)

## Informazioni sui profili

[!DNL Real-time Customer Profile] unisce i dati provenienti da diversi sistemi aziendali e fornisce l&#39;accesso a tali dati sotto forma di profili cliente con gli eventi relativi alle serie temporali. Questa funzione consente agli esperti di marketing di promuovere esperienze coordinate, coerenti e pertinenti con il pubblico attraverso più canali. Nelle sezioni seguenti vengono evidenziati alcuni dei concetti fondamentali che è necessario comprendere per creare e mantenere in modo efficace i profili all&#39;interno della piattaforma.

### Archivio dati profilo

Anche se [!DNL Real-time Customer Profile] elabora i dati acquisiti e utilizza Adobe Experience Platform [!DNL Identity Service] per unire i dati correlati tramite la mappatura dell&#39;identità, essa mantiene i propri dati nell&#39;archivio dati [!DNL Profile]. Lo store [!DNL Profile] è separato dai dati del catalogo nel lago di dati e dai dati [!DNL Identity Service] nel grafico dell&#39;identità.

L&#39;archivio dei profili utilizza un&#39;infrastruttura DB Cosmos di Microsoft Azure e la piattaforma Data Lake utilizza l&#39;archiviazione Data Lake di Microsoft Azure.

### Guardrail profilo

 Experience Platform offre una serie di tutorial per evitare di creare schemi [Experience Data Model (XDM)](../xdm/home.md) che non possono essere supportati dal profilo cliente in tempo reale. Ciò include limiti morbidi che si traducono in un deterioramento delle prestazioni, nonché limiti rigidi che generano errori e interruzioni del sistema. Per ulteriori informazioni, incluso un elenco di linee guida e di esempi di casi di utilizzo, consultare la documentazione [Profile guardrails](guardrails.md).

### (Alfa) Pannello profilo {#profile-dashboard}

>[!IMPORTANT]
>
>La funzionalità del dashboard è attualmente in alfa e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

L&#39;interfaccia utente del Experience Platform  fornisce una dashboard attraverso la quale è possibile visualizzare informazioni importanti sui dati del profilo cliente in tempo reale, come acquisito durante un&#39;istantanea giornaliera. Per informazioni su come accedere e utilizzare il dashboard [!DNL Profile] nell&#39;interfaccia utente e per informazioni dettagliate sulle metriche visualizzate nel dashboard, fare riferimento alla [Guida dell&#39;interfaccia utente del dashboard del profilo](ui/profile-dashboard.md).

### Frammenti di profilo e profili uniti {#profile-fragments-vs-merged-profiles}

Ciascun profilo cliente è composto da più frammenti di profilo che sono stati uniti per formare una singola vista del cliente. Ad esempio, se un cliente interagisce con il tuo marchio su più canali, l&#39;organizzazione avrà più frammenti di profilo correlati a tale singolo cliente che saranno visualizzati in più set di dati. Quando questi frammenti vengono assimilati in Piattaforma, vengono uniti per creare un unico profilo per il cliente.

Quando i dati provenienti da più origini sono in conflitto (ad esempio, un frammento indica il cliente come &quot;singolo&quot; mentre l&#39;altro elenca il cliente come &quot;sposato&quot;), la [unione policy](#merge-policies) determina quali informazioni dare la priorità e includere nel profilo dell&#39;individuo. Pertanto, è probabile che il numero totale di frammenti di profilo all&#39;interno della piattaforma sia sempre superiore al numero totale di profili uniti, in quanto ogni profilo è composto da più frammenti.

### Registra dati

Un profilo è una rappresentazione di un oggetto, un&#39;organizzazione o un individuo, composta da molti attributi (noti anche come dati del record). Ad esempio, il profilo di un prodotto può includere uno SKU e una descrizione, mentre il profilo di una persona contiene informazioni come nome, cognome e indirizzo e-mail. Utilizzando [!DNL Experience Platform], puoi personalizzare i profili per utilizzare dati specifici relativi alla tua attività. La classe [!DNL Experience Data Model] (XDM) standard, [!DNL XDM Individual Profile], è la classe preferita sulla quale creare uno schema per descrivere i dati del record cliente e fornisce i dati integrali a molte interazioni tra i servizi della piattaforma. Per ulteriori informazioni sull&#39;utilizzo degli schemi in [!DNL Experience Platform], iniziare leggendo la [Panoramica del sistema XDM](../xdm/home.md).

### Eventi delle serie temporali

I dati delle serie temporali forniscono un&#39;istantanea del sistema nel momento in cui un&#39;azione è stata eseguita direttamente o indirettamente da un soggetto, nonché i dati che descrivono l&#39;evento stesso. Rappresentata dalla classe di schema standard XDM ExperienceEvent, i dati delle serie temporali possono descrivere eventi quali elementi aggiunti a un carrello, collegamenti su cui si fa clic e video visualizzati. I dati delle serie temporali possono essere utilizzati per basare le regole di segmentazione su e gli eventi possono essere accessibili individualmente nel contesto di un profilo.

### Identità

Ogni azienda vuole comunicare con i propri clienti in un modo che si senta personale. Tuttavia, una delle sfide poste dalla distribuzione di esperienze digitali rilevanti ai clienti è capire come collegare i dati disconnessi, che spesso si diffondono tra canali digitali diversi come tablet, telefoni cellulari e laptop. [!DNL Identity Service] consente di mettere insieme l&#39;immagine completa del cliente collegando identità da più canali e creando un grafico di identità per ogni cliente. Per ulteriori informazioni, visitare la [Panoramica del servizio identità](../identity-service/home.md).

### Unisci criteri

Quando si uniscono i frammenti di dati da più origini e li si combina per visualizzare una visualizzazione completa di ciascuno dei singoli clienti, i criteri di unione sono le regole utilizzate da [!DNL Platform] per determinare in che modo i dati verranno assegnati alle priorità e quali verranno utilizzati per creare il profilo cliente. In presenza di dati in conflitto da più set di dati, il criterio di unione determinerà come devono essere gestiti i dati e quale valore utilizzare. Utilizzando le API RESTful o l&#39;interfaccia utente, puoi creare nuovi criteri di unione, gestire i criteri esistenti e impostare un criterio di unione predefinito per la tua organizzazione.

Per ulteriori informazioni sull&#39;utilizzo dei criteri di unione tramite l&#39;API [!DNL Real-time Customer Profile], vedere la [guida dell&#39;endpoint dei criteri di unione](api/merge-policies.md). Per utilizzare i criteri di unione utilizzando l&#39;interfaccia utente [!DNL Experience Platform], fare riferimento alla [guida per l&#39;interfaccia utente dei criteri di unione](ui/merge-policies.md).

### Schemi dell&#39;Unione {#profile-fragments-and-union-schemas}

Una delle caratteristiche chiave di [!DNL Real-time Customer Profile] è la capacità di unificare i dati multicanale. Se [!DNL Real-time Customer Profile] è utilizzato per accedere a un&#39;entità, può fornire una visualizzazione unita di tutti i frammenti di profilo per tale entità tra set di dati, denominata &quot;visualizzazione unione&quot; e resa possibile attraverso ciò che è noto come schema unione.

Per ulteriori informazioni sugli schemi di unione, inclusa la modalità di accesso agli schemi di unione nell&#39;interfaccia utente, vedere la [guida all&#39;interfaccia utente dello schema di unione](ui/union-schema.md).

### (Alfa) Attributi calcolati

>[!IMPORTANT]
>
>La funzionalità dell&#39;attributo calcolato è in alfa. La documentazione e le funzionalità sono soggette a modifiche.

Gli attributi calcolati consentono di calcolare automaticamente il valore dei campi in base ad altri valori, calcoli ed espressioni. Gli attributi calcolati operano a livello di profilo, il che significa che puoi aggregare i valori per tutti i record ed eventi. Ogni attributo calcolato contiene un&#39;espressione, o &quot;regola&quot;, che valuta i dati in arrivo e memorizza il valore risultante in un attributo di profilo o in un evento. Questi calcoli consentono di rispondere facilmente a domande relative a cose come il valore di acquisto del ciclo di vita, il tempo tra acquisti o il numero di aperture di applicazioni, senza che sia necessario eseguire manualmente calcoli complessi ogni volta che le informazioni sono necessarie. Per ulteriori informazioni sugli attributi calcolati e istruzioni dettagliate per utilizzarli con l&#39;API [!DNL Real-time Customer Profile], vedere la [guida dell&#39;endpoint degli attributi calcolati](api/computed-attributes.md). Questa guida ti aiuterà a comprendere meglio il ruolo che gli attributi calcolati giocano in Adobe Experience Platform e include chiamate API di esempio per eseguire operazioni CRUD di base.

## Profili e segmenti

Adobe Experience Platform [!DNL Segmentation Service] produce i tipi di pubblico necessari per fornire esperienze ai singoli clienti. Quando viene creato un segmento di pubblico, l&#39;ID di tale segmento viene aggiunto all&#39;elenco delle appartenenze del segmento per tutti i profili idonei. Le regole dei segmenti vengono create e applicate ai dati [!DNL Real-time Customer Profile] utilizzando le API RESTful e l&#39;interfaccia utente di Generatore di segmenti. Per ulteriori informazioni sulla segmentazione, consultare la [Panoramica del servizio di segmentazione](../segmentation/home.md).

### Streaming dell’assimilazione e segmentazione in streaming

L&#39;ingresso in tempo reale è possibile attraverso un processo chiamato caricamento in streaming. Durante l&#39;assimilazione dei dati di profilo e serie temporale, [!DNL Real-time Customer Profile] decide automaticamente di includere o escludere tali dati dai segmenti attraverso un processo continuo denominato segmentazione in streaming, prima di unirli ai dati esistenti e di aggiornare la visualizzazione unione. Di conseguenza, puoi eseguire istantaneamente dei calcoli e prendere decisioni per offrire esperienze personalizzate e avanzate ai clienti mentre interagiscono con il tuo marchio. Durante l&#39;assimilazione, i dati vengono anche sottoposti a convalida per assicurarsi che vengano assimilati correttamente e conformi allo schema su cui si basa il dataset. Per ulteriori informazioni sulle operazioni di convalida durante l&#39;assimilazione, leggere la [panoramica sulla qualità di inserimento dei dati](../ingestion/quality/overview.md).

## Proiezioni Edge

Al fine di promuovere esperienze coordinate, coerenti e personalizzate per i clienti attraverso più canali in tempo reale, i dati giusti devono essere prontamente disponibili e costantemente aggiornati man mano che si verificano le modifiche. Adobe Experience Platform consente l&#39;accesso in tempo reale ai dati tramite l&#39;utilizzo di ciò che è noto come edge. Un server periferico è un server collocato geograficamente che memorizza i dati e li rende facilmente accessibili alle applicazioni. Ad esempio,  applicazioni di Adobe come  Adobe Target e  Adobe Campaign utilizzano i bordi per fornire esperienze personalizzate ai clienti in tempo reale. I dati vengono indirizzati a un bordo da una proiezione, con una destinazione di proiezione che definisce il bordo a cui verranno inviati i dati, e una configurazione di proiezione che definisce le informazioni specifiche che verranno rese disponibili sul bordo. Per saperne di più e iniziare a lavorare con le proiezioni utilizzando l&#39;API [!DNL Real-time Customer Profile], fare riferimento alla [edge projection guide](api/edge-projections.md).

## Inserimento di dati in [!DNL Profile]

[!DNL Platform] può essere configurato per inviare dati di record e serie temporali a  [!DNL Profile], supportando l&#39;assimilazione in tempo reale dello streaming e l&#39;inserimento batch. Per ulteriori informazioni, vedere l&#39;esercitazione che descrive come [aggiungere dati al profilo cliente in tempo reale](tutorials/add-profile-data.md).

>[!NOTE]
>
>I dati raccolti attraverso  soluzioni di Adobe, inclusi [!DNL Analytics Cloud], [!DNL Marketing Cloud] e [!DNL Advertising Cloud], scorrono in [!DNL Experience Platform] e vengono assimilati in [!DNL Profile].

### Metriche di assimilazione dei profili

Observability Insights consente di esporre le metriche chiave in Adobe Experience Platform. Oltre alle statistiche sull&#39;utilizzo di [!DNL Experience Platform] e agli indicatori di prestazioni per diverse funzionalità [!DNL Platform], sono disponibili metriche specifiche relative al profilo che consentono di conoscere meglio i tassi di richieste in entrata, i tassi di assimilazione riusciti, le dimensioni dei record acquisiti e altro ancora. Per saperne di più, iniziare leggendo la [Panoramica API di Insights](../observability/api/overview.md) e per un elenco completo delle metriche del profilo cliente in tempo reale, consulta la documentazione sulle [metriche disponibili](../observability/api/metrics.md#available-metrics).

## [!DNL Data governance] ed [!DNL Privacy]

[!DNL Data governance] è una serie di strategie e tecnologie utilizzate per gestire i dati dei clienti e garantire la conformità a normative, restrizioni e politiche applicabili all&#39;uso dei dati.

Per quanto riguarda l&#39;accesso ai dati, la governance dei dati svolge un ruolo chiave all&#39;interno di [!DNL Experience Platform] a vari livelli:
* Etichettatura dell&#39;uso dei dati
* Criteri di accesso ai dati
* Controllo dell&#39;accesso ai dati per le azioni di marketing

[!DNL Data governance] è gestito in diversi punti. Tra queste, puoi scegliere quali dati vengono trasferiti in [!DNL Platform] e quali sono accessibili dopo l&#39;assimilazione per una determinata azione di marketing. Per ulteriori informazioni, iniziare leggendo la [panoramica sulla governance dei dati](../data-governance/home.md).

### Gestione delle richieste di privacy e rinuncia ai dati

[!DNL Experience Platform] consente ai clienti di inviare richieste di rifiuto relative all&#39;utilizzo e all&#39;archiviazione dei loro dati all&#39;interno  [!DNL Real-time Customer Profile]. Per ulteriori informazioni su come vengono gestite le richieste di rifiuto, consultate la documentazione su [rispetto delle richieste di rifiuto](../segmentation/honoring-opt-outs.md).

## Passaggi successivi e risorse aggiuntive

Per ulteriori informazioni sull&#39;utilizzo di dati [!DNL Real-time Customer Profile] utilizzando l&#39;interfaccia utente del Experience Platform  o l&#39;API del profilo, iniziare leggendo rispettivamente la [Guida dell&#39;interfaccia utente del profilo](ui/user-guide.md) o la [Guida per gli sviluppatori di API](api/overview.md).