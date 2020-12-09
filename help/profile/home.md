---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;unified profile;Unified Profile;unified;Profile;rtcp;XDM graphs
title: Panoramica del profilo cliente in tempo reale
topic: guide
description: Profilo cliente in tempo reale è un archivio di entità di ricerca generico che unisce i dati da varie risorse di dati aziendali e fornisce l'accesso a tali dati sotto forma di profili cliente individuali ed eventi serie temporali correlati. Questa funzione consente agli esperti di marketing di promuovere esperienze coordinate, coerenti e pertinenti con il pubblico attraverso più canali.
translation-type: tm+mt
source-git-commit: b8d6bd5caf6c6f4d1da218b6ca12cec154d64412
workflow-type: tm+mt
source-wordcount: '1844'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile]panoramica

Adobe Experience Platform consente di creare esperienze coordinate, coerenti e pertinenti per i clienti, indipendentemente da dove e quando interagiscono con il tuo marchio. Con [!DNL Real-time Customer Profile], puoi vedere una visualizzazione olistica di ogni singolo cliente che combina dati provenienti da più canali, inclusi online, offline, CRM e dati di terze parti. [!DNL Profile] consente di consolidare i diversi dati dei clienti in una visualizzazione unificata che offre un account utilizzabile e con marca temporale per ogni interazione con il cliente. Questa panoramica vi aiuterà a capire il ruolo e l’utilizzo di [!DNL Real-time Customer Profile] in [!DNL Experience Platform].

## [!DNL Profile] in  Experience Platform

Il rapporto tra Profilo cliente in tempo reale e altri servizi all&#39;interno  Experience Platform è evidenziato nel diagramma seguente:

![Servizi Adobe Experience Platform.](images/profile-overview/profile-in-platform.png)

### Archivio dati profilo

Anche se [!DNL Real-time Customer Profile] elabora i dati acquisiti e utilizza Adobe Experience Platform [!DNL Identity Service] per unire i dati correlati attraverso la mappatura dell&#39;identità, mantiene i propri dati nello [!DNL Profile] store. Lo [!DNL Profile] store è separato dai [!DNL Catalog] dati presenti nel [!DNL Data Lake] grafico di identità e dai [!DNL Identity Service] dati nel grafico di identità.

L&#39;archivio dei profili utilizza un&#39;infrastruttura DB Cosmos di Microsoft Azure e la piattaforma Data Lake utilizza l&#39;archiviazione Data Lake di Microsoft Azure.

### Guardrail profilo

 Experience Platform offre una serie di tutorial per evitare di creare schemi [XDM (](../xdm/home.md) Experience Data Model) che non possono essere supportati dal profilo cliente in tempo reale. Ciò include limiti morbidi che si traducono in un deterioramento delle prestazioni, nonché limiti rigidi che generano errori e interruzioni del sistema. Per ulteriori informazioni, incluso un elenco di linee guida e di esempi di casi di utilizzo, leggere la documentazione [Profile guardrails](guardrails.md) .

## Informazioni sui profili

[!DNL Real-time Customer Profile] unisce i dati provenienti da diversi sistemi aziendali e fornisce l&#39;accesso a tali dati sotto forma di profili cliente con gli eventi relativi alle serie temporali. Questa funzione consente agli esperti di marketing di promuovere esperienze coordinate, coerenti e pertinenti con il pubblico attraverso più canali. Nelle sezioni seguenti vengono evidenziati alcuni dei concetti fondamentali che è necessario comprendere per creare e mantenere in modo efficace i profili all&#39;interno della piattaforma.

### Frammenti di profilo e profili uniti {#profile-fragments-vs-merged-profiles}

Ciascun profilo cliente è composto da più frammenti di profilo che sono stati uniti per formare una singola vista del cliente. Ad esempio, se un cliente interagisce con il tuo marchio su più canali, l&#39;organizzazione avrà più frammenti di profilo correlati a tale singolo cliente che saranno visualizzati in più set di dati. Quando questi frammenti vengono assimilati in Piattaforma, vengono uniti per creare un unico profilo per il cliente.

Quando i dati provenienti da più origini sono in conflitto (ad esempio, un frammento indica il cliente come &quot;singolo&quot; mentre l&#39;altro elenca il cliente come &quot;sposato&quot;), il criterio [di](#merge-policies) unione determina quali informazioni dare la priorità e includere nel profilo del singolo. Pertanto, è probabile che il numero totale di frammenti di profilo all&#39;interno della piattaforma sia sempre superiore al numero totale di profili uniti, in quanto ogni profilo è composto da più frammenti.

### Registra dati

Un profilo è una rappresentazione di un oggetto, un&#39;organizzazione o un individuo, composta da molti attributi (noti anche come dati del record). Ad esempio, il profilo di un prodotto può includere uno SKU e una descrizione, mentre il profilo di una persona contiene informazioni come nome, cognome e indirizzo e-mail. Utilizzando [!DNL Experience Platform]questa opzione, puoi personalizzare i profili in modo da utilizzare dati specifici relativi alla tua attività. La classe standard [!DNL Experience Data Model] (XDM), [!DNL XDM Individual Profile], è la classe preferita per la quale creare uno schema durante la descrizione dei dati del record cliente, e fornisce i dati integrali a molte interazioni tra i servizi della piattaforma. Per ulteriori informazioni sull&#39;utilizzo degli schemi in [!DNL Experience Platform], iniziare leggendo la panoramica [del sistema](../xdm/home.md)XDM.

### Eventi delle serie temporali

I dati delle serie temporali forniscono un&#39;istantanea del sistema nel momento in cui un&#39;azione è stata eseguita direttamente o indirettamente da un soggetto, nonché i dati che descrivono l&#39;evento stesso. Rappresentata dalla classe di schema standard XDM ExperienceEvent, i dati delle serie temporali possono descrivere eventi quali elementi aggiunti a un carrello, collegamenti su cui si fa clic e video visualizzati. I dati delle serie temporali possono essere utilizzati per basare le regole di segmentazione su e gli eventi possono essere accessibili individualmente nel contesto di un profilo.

### Identità

Ogni azienda vuole comunicare con i propri clienti in un modo che si senta personale. Tuttavia, una delle sfide poste dalla distribuzione di esperienze digitali rilevanti ai clienti è capire come collegare i dati disconnessi, che spesso si diffondono tra canali digitali diversi come tablet, telefoni cellulari e laptop. [!DNL Identity Service] consente di mettere insieme l&#39;immagine completa del cliente collegando identità da più canali e creando un grafico di identità per ogni cliente. Per ulteriori informazioni, visita la panoramica [del servizio](../identity-service/home.md) identità.

### Unisci criteri

Quando si uniscono i frammenti di dati da più origini e li si combina per visualizzare una visualizzazione completa di ciascuno dei singoli clienti, i criteri di unione sono le regole che [!DNL Platform] vengono utilizzate per determinare in che modo i dati verranno classificati come priorità e quali dati verranno utilizzati per creare il profilo cliente. In presenza di dati in conflitto da più set di dati, il criterio di unione determinerà come devono essere gestiti i dati e quale valore utilizzare. Utilizzando le API RESTful o l&#39;interfaccia utente, puoi creare nuovi criteri di unione, gestire i criteri esistenti e impostare un criterio di unione predefinito per la tua organizzazione. Per ulteriori informazioni sull&#39;utilizzo dei criteri di unione tramite l&#39; [!DNL Real-time Customer Profile] API, vedere la guida [dell&#39;endpoint dei criteri di](api/merge-policies.md)unione. Per utilizzare i criteri di unione utilizzando l&#39; [!DNL Experience Platform] interfaccia utente, fare riferimento alla guida [utente dei criteri di](ui/merge-policies.md)unione.

### Schemi dell’Unione {#profile-fragments-and-union-schemas}

Una delle caratteristiche chiave di [!DNL Real-time Customer Profile] è la capacità di unificare i dati multicanale. Quando [!DNL Real-time Customer Profile] viene utilizzato per accedere a un&#39;entità, può fornire all&#39;utente una visualizzazione unita di tutti i frammenti di profilo per l&#39;entità in tutti i set di dati, detta visualizzazione unione e resa possibile tramite ciò che è noto come schema unione. [!DNL Real-time Customer Profile] i dati vengono uniti tra le origini quando l&#39;ID di un&#39;entità o di un profilo vi consente di accedervi o di esportarli come segmento. Per ulteriori informazioni sull&#39;accesso ai profili e alle visualizzazioni di unione tramite l&#39; [!DNL Real-time Customer Profile] API, visita la guida [all&#39;endpoint](api/entities.md)entità.

### Segmentazione

Adobe Experience Platform [!DNL Segmentation Service] produce i tipi di pubblico necessari per fornire esperienze ai singoli clienti. Quando viene creato un segmento di pubblico, l&#39;ID di tale segmento viene aggiunto all&#39;elenco delle appartenenze del segmento per tutti i profili idonei. Le regole dei segmenti sono create e applicate ai [!DNL Real-time Customer Profile] dati utilizzando le API RESTful e l&#39;interfaccia utente di Generatore di segmenti. Per ulteriori informazioni sulla segmentazione, consultare la panoramica [del servizio di](../segmentation/home.md)segmentazione.

### (Alfa) Configurare gli attributi calcolati

>[!IMPORTANT]
>
>La funzionalità dell&#39;attributo calcolato è in alfa. La documentazione e le funzionalità sono soggette a modifiche.

Gli attributi calcolati consentono di calcolare automaticamente il valore dei campi in base ad altri valori, calcoli ed espressioni. Gli attributi calcolati operano a livello di profilo, il che significa che puoi aggregare i valori per tutti i record ed eventi. Ogni attributo calcolato contiene un&#39;espressione, o &quot;regola&quot;, che valuta i dati in arrivo e memorizza il valore risultante in un attributo di profilo o in un evento. Questi calcoli consentono di rispondere facilmente a domande relative a cose come il valore di acquisto del ciclo di vita, il tempo tra acquisti o il numero di aperture di applicazioni, senza che sia necessario eseguire manualmente calcoli complessi ogni volta che le informazioni sono necessarie. Per ulteriori informazioni sugli attributi calcolati e istruzioni dettagliate per utilizzarli tramite l&#39; [!DNL Real-time Customer Profile] API, consultate la guida [all&#39;endpoint degli attributi](api/computed-attributes.md)calcolati. Questa guida ti aiuterà a comprendere meglio il ruolo che gli attributi calcolati giocano in Adobe Experience Platform e include chiamate API di esempio per eseguire operazioni CRUD di base.

## Componenti in tempo reale

Questa sezione introduce i componenti che consentono [!DNL Real-time Customer Profile] di aggiornare e monitorare dati di record e serie temporali in tempo reale.

### Streaming dell’assimilazione e segmentazione in streaming

L&#39;ingresso in tempo reale è possibile attraverso un processo chiamato caricamento in streaming. Durante l&#39;assimilazione dei dati di profilo e serie temporale, [!DNL Real-time Customer Profile] decide automaticamente di includere o escludere tali dati dai segmenti attraverso un processo continuo denominato segmentazione in streaming, prima di unirli ai dati esistenti e di aggiornare la visualizzazione unione. Di conseguenza, puoi eseguire istantaneamente dei calcoli e prendere decisioni per offrire esperienze personalizzate e avanzate ai clienti mentre interagiscono con il tuo marchio. Durante l&#39;assimilazione, i dati vengono anche sottoposti a convalida per assicurarsi che vengano assimilati correttamente e conformi allo schema su cui si basa il dataset. Per ulteriori informazioni sulle operazioni di convalida effettuate durante l&#39;assimilazione, consultare la panoramica [sulla qualità dell&#39;assimilazione dei](../ingestion/quality/overview.md)dati.

### Configurazioni e destinazioni di proiezione Edge

Al fine di promuovere esperienze coordinate, coerenti e personalizzate per i clienti attraverso più canali in tempo reale, i dati giusti devono essere prontamente disponibili e costantemente aggiornati man mano che si verificano le modifiche. Adobe Experience Platform consente l&#39;accesso in tempo reale ai dati tramite l&#39;utilizzo di ciò che è noto come edge. Un server periferico è un server collocato geograficamente che memorizza i dati e li rende facilmente accessibili alle applicazioni. Ad esempio,  applicazioni di Adobe come  Adobe Target e  Adobe Campaign utilizzano i bordi per fornire esperienze personalizzate ai clienti in tempo reale. I dati vengono indirizzati a un bordo da una proiezione, con una destinazione di proiezione che definisce il bordo a cui verranno inviati i dati, e una configurazione di proiezione che definisce le informazioni specifiche che verranno rese disponibili sul bordo. Per saperne di più e iniziare a lavorare con le proiezioni utilizzando l&#39; [!DNL Real-time Customer Profile] API, fare riferimento alla guida [endpoint di proiezione](api/edge-projections.md)edge.

## Assegna dati a [!DNL Profile]

[!DNL Platform] può essere configurato per inviare dati di record e serie temporali a [!DNL Profile], supportando l&#39;assimilazione in tempo reale dello streaming e l&#39;inserimento batch. Per ulteriori informazioni, consulta l’esercitazione che illustra come [aggiungere dati al profilo](tutorials/add-profile-data.md)cliente in tempo reale.

>[!NOTE]
>
>I dati raccolti attraverso  soluzioni di Adobe, inclusi [!DNL Analytics Cloud][!DNL Marketing Cloud], e [!DNL Advertising Cloud], fluiscono [!DNL Experience Platform] e vengono ingeriti [!DNL Profile].

### [!DNL Profile] metriche di assimilazione

Observability Insights consente di esporre le metriche chiave in Adobe Experience Platform. Oltre alle statistiche di [!DNL Platform] utilizzo e agli indicatori di prestazioni per diverse [!DNL Platform] funzionalità, sono disponibili metriche [!DNL Profile]correlate specifiche che consentono di conoscere i tassi di richieste in entrata, i tassi di acquisizione di successo, le dimensioni dei record acquisiti e altro ancora. Per saperne di più, inizia leggendo la panoramica [API](../observability/api/overview.md)Observability Insights e per un elenco completo delle [!DNL Profile] metriche, consulta la documentazione sulle metriche [](../observability/api/metrics.md#available-metrics)disponibili.

## [!DNL Data governance] ed [!DNL Privacy]

[!DNL Data governance] è una serie di strategie e tecnologie utilizzate per gestire i dati dei clienti e garantire la conformità a normative, restrizioni e politiche applicabili all&#39;uso dei dati.

Per quanto riguarda l&#39;accesso ai dati, la governance dei dati svolge un ruolo chiave a [!DNL Experience Platform] vari livelli:
* Etichettatura dell&#39;uso dei dati
* Criteri di accesso ai dati
* Controllo dell&#39;accesso ai dati per le azioni di marketing

[!DNL Data governance] è gestito in diversi punti. tra cui la scelta di quali dati vengono acquisiti [!DNL Platform] e quali dati sono accessibili dopo l’assimilazione per una determinata azione di marketing. Per ulteriori informazioni, iniziare leggendo la panoramica sulla governance dei [dati](../data-governance/home.md).

### Gestione delle richieste di privacy e rinuncia ai dati

[!DNL Experience Platform] consente ai clienti di inviare richieste di rifiuto relative all&#39;utilizzo e all&#39;archiviazione dei loro dati all&#39;interno [!DNL Real-time Customer Profile]. Per ulteriori informazioni sulla gestione delle richieste di rifiuto, consultate la documentazione relativa al [rispetto delle richieste](../segmentation/honoring-opt-outs.md)di rifiuto.

## Passaggi successivi e risorse aggiuntive

Per ulteriori informazioni sull&#39;utilizzo [!DNL Real-time Customer Profile], consulta la guida [all&#39;interfaccia utente](ui/user-guide.md) profilo o la guida [per gli sviluppatori](api/overview.md)API.

>[!WARNING]
>
>L’interfaccia utente del Experience Platform  viene aggiornata di frequente e può essere cambiata dopo la registrazione del video. Consulta la guida [utente Profilo cliente](ui/user-guide.md) in tempo reale per informazioni sulle ultime funzionalità e videate dell&#39;interfaccia utente.

>[!VIDEO](https://video.tv.adobe.com/v/27251?quality=12)