---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Panoramica del profilo cliente in tempo reale
topic: guide
translation-type: tm+mt
source-git-commit: 24380653fdae561d294453eaec753a863993dfaf

---


# Panoramica del profilo cliente in tempo reale

Adobe Experience Platform consente di creare esperienze coordinate, coerenti e pertinenti per i clienti, ovunque e quando interagiscono con il tuo marchio. Con il profilo cliente in tempo reale, puoi vedere una visualizzazione olistica di ogni singolo cliente che combina dati da più canali, inclusi dati online, offline, CRM e di terze parti. Il profilo consente di consolidare i diversi dati dei clienti in una visualizzazione unificata che offre un account utilizzabile e con marca temporale per ogni interazione con il cliente. Questa panoramica ti aiuterà a capire il ruolo e l&#39;utilizzo del profilo cliente in tempo reale nella piattaforma di esperienze.

## Informazioni sul profilo cliente in tempo reale

Profilo cliente in tempo reale è un archivio di entità di ricerca generico che unisce i dati da varie risorse di dati aziendali e fornisce l&#39;accesso a tali dati sotto forma di profili cliente individuali ed eventi serie temporali correlati.

Questa funzione consente agli esperti di marketing di promuovere esperienze coordinate, coerenti e pertinenti con il pubblico attraverso più canali, come illustrato nel video seguente:

>[!VIDEO](https://video.tv.adobe.com/v/27251?quality=12&enable10seconds=on&speedcontrol=on)

### Archivio dati profilo

Anche se il profilo cliente in tempo reale elabora i dati acquisiti e utilizza Adobe Experience Platform Identity Service per unire i dati correlati tramite la mappatura dell&#39;identità, mantiene i propri dati nell&#39;archivio dei profili. In altre parole, lo store Profilo è separato dai dati del Catalogo (Data Lake) e del Servizio Identità (grafico identità).

### Servizi profilo e piattaforma

Il rapporto tra il profilo cliente in tempo reale e altri servizi all’interno di Experience Platform è evidenziato nel seguente diagramma:

![La relazione tra i servizi Profilo e altri servizi della Piattaforma esperienza.](images/profile-overview/profile-in-platform.png)

### Profili e dati record

Un profilo è una rappresentazione di un soggetto, un&#39;organizzazione o un individuo, detti anche dati di record. Ad esempio, il profilo di un prodotto può includere uno SKU e una descrizione, mentre il profilo di una persona contiene informazioni come nome, cognome e indirizzo e-mail.

Utilizzando Experience Platform, puoi personalizzare i profili per utilizzare tipi di dati rilevanti per la tua attività. La classe di profilo singolo XDM (Experience Data Model) standard è la classe preferita per la generazione di uno schema per la descrizione dei dati del record cliente e fornisce i dati integrali a molte interazioni tra i servizi della piattaforma. Per ulteriori informazioni sull&#39;utilizzo degli schemi in Experience Platform, consultate la panoramica [di sistema](../xdm/home.md)XDM.

### Eventi delle serie temporali

I dati delle serie temporali forniscono un&#39;istantanea del sistema nel momento in cui un&#39;azione è stata eseguita direttamente o indirettamente da un soggetto, nonché i dati che descrivono l&#39;evento stesso. Rappresentata dalla classe di schema standard XDM ExperienceEvent, i dati delle serie temporali possono descrivere eventi quali elementi aggiunti a un carrello, collegamenti su cui si fa clic e video visualizzati.

I dati delle serie temporali possono essere utilizzati per basare le regole di segmentazione su e gli eventi possono essere accessibili individualmente nel contesto di un profilo.

### Identità

Ogni azienda vuole comunicare con i propri clienti in un modo che si senta personale. Tuttavia, una delle sfide poste dalla distribuzione di esperienze digitali rilevanti ai clienti è capire come collegare i dati disconnessi, che spesso si diffondono tra canali digitali diversi come tablet, telefoni cellulari e laptop.

Servizio identità consente di mettere insieme l&#39;immagine completa del cliente collegando identità da più canali, creando un grafico dell&#39;identità per ogni cliente, in modo da comprenderle meglio. Per ulteriori informazioni, visita la panoramica [del servizio](../identity-service/home.md) identità.

### Segmentazione

Le regole dei segmenti sono create e applicate ai dati del profilo cliente in tempo reale mediante le API RESTful e l’interfaccia utente di Generatore di segmenti. Come spiegato nel video seguente, ADobe Experience Platform Segmentation Service produce i tipi di pubblico necessari per fornire ai clienti esperienze ottimali:

>[!VIDEO](https://video.tv.adobe.com/v/27254?quality=12&enable10seconds=on&speedcontrol=on)

Quando viene creato un segmento di pubblico, l&#39;ID di tale segmento viene aggiunto all&#39;elenco delle appartenenze del segmento per tutti i profili idonei. Per ulteriori informazioni sulla segmentazione, consultare la panoramica [del servizio di](../segmentation/home.md)segmentazione.

### Frammenti di profilo e visualizzazioni unione

Una delle caratteristiche chiave del profilo cliente in tempo reale è la capacità di unificare i dati multicanale. Quando si utilizza il profilo cliente in tempo reale per accedere a un&#39;entità, è possibile ottenere una visualizzazione unita di tutti i frammenti di profilo per tale entità tra i set di dati, denominata visualizzazione unione.

I dati del profilo cliente in tempo reale vengono uniti tra le origini quando l&#39;ID di un&#39;entità o di un profilo vi permette di accedervi o esportati come segmento. Per ulteriori informazioni sull&#39;accesso ai profili e alle viste dell&#39;unione, visita la guida secondaria per gli sviluppatori di API profilo cliente in tempo reale sulle [entità, nota anche come &quot;Accesso profilo&quot;](api/entities.md).

### Unisci criteri

Quando si uniscono i dati da più origini e si combinano per visualizzare una visualizzazione completa di ciascuno dei singoli clienti, i criteri di unione sono le regole utilizzate dalla piattaforma per determinare in che modo i dati verranno assegnati alle priorità e quali verranno combinati per creare tale visualizzazione unificata.

Utilizzando le API RESTful o l&#39;interfaccia utente, puoi creare nuovi criteri di unione, gestire i criteri esistenti e impostare un criterio di unione predefinito per la tua organizzazione. Per ulteriori informazioni sull&#39;utilizzo dei criteri di unione tramite le API, vedere la guida [secondaria dei criteri di](api/merge-policies.md) unione delle API dei profili cliente in tempo reale o la guida [utente dei criteri di](ui/merge-policies.md) unione per informazioni su come utilizzare i criteri di unione utilizzando l&#39;interfaccia utente della piattaforma.

## Componenti in tempo reale

Questa sezione presenta i componenti che consentono al profilo cliente in tempo reale di aggiornare e monitorare i dati di record e delle serie temporali in tempo reale.

### Streaming dell’assimilazione e segmentazione in streaming

L&#39;ingresso in tempo reale è possibile attraverso un processo chiamato caricamento in streaming. Con l&#39;acquisizione dei dati di profilo e serie temporali, il profilo cliente in tempo reale decide automaticamente di includere o escludere tali dati dai segmenti attraverso un processo continuo denominato segmentazione in streaming, prima di unirli ai dati esistenti e di aggiornare la visualizzazione unione. Di conseguenza, puoi eseguire istantaneamente dei calcoli e prendere decisioni per offrire esperienze personalizzate e avanzate ai clienti mentre interagiscono con il tuo marchio.

Durante l&#39;assimilazione, i dati vengono anche sottoposti a convalida per assicurarsi che vengano assimilati correttamente e conformi allo schema su cui si basa il dataset. Per ulteriori informazioni sulle operazioni di convalida effettuate durante l&#39;assimilazione, consultare la panoramica [sulla qualità dell&#39;assimilazione dei](../ingestion/quality/overview.md)dati.

### Proiezioni Edge

Al fine di promuovere esperienze coordinate, coerenti e personalizzate per i clienti attraverso più canali in tempo reale, i dati giusti devono essere prontamente disponibili e costantemente aggiornati man mano che si verificano le modifiche. Adobe Experience Platform consente l&#39;accesso in tempo reale ai dati tramite l&#39;utilizzo di ciò che sono noti come edge.

Un server periferico è un server collocato geograficamente che memorizza i dati e li rende facilmente accessibili alle applicazioni. Ad esempio, le applicazioni Adobe come Adobe Target e Adobe Campaign utilizzano i bordi per fornire esperienze cliente personalizzate in tempo reale. I dati vengono indirizzati a un bordo da una proiezione, con una destinazione di proiezione che definisce il bordo a cui verranno inviati i dati, e una configurazione di proiezione che definisce le informazioni specifiche che verranno rese disponibili sul bordo.

Per saperne di più e iniziare a lavorare con margini e proiezioni, consulta la guida secondaria Proiezioni [Edge API profilo cliente in tempo reale](api/edge-projections.md).

## Governance dei dati e privacy

La governance dei dati è una serie di strategie e tecnologie utilizzate per gestire i dati dei clienti e garantire la conformità a normative, restrizioni e politiche applicabili all&#39;uso dei dati.

Per quanto riguarda l’accesso ai dati, la governance dei dati svolge un ruolo chiave all’interno di Experience Platform a vari livelli:
* Etichettatura dell&#39;uso dei dati
* Criteri di accesso ai dati
* Controllo dell&#39;accesso ai dati per le azioni di marketing

La governance dei dati è gestita in diversi punti. Tra queste, puoi decidere quali dati vengono acquisiti in Piattaforma e quali sono accessibili dopo l’assimilazione per una determinata azione di marketing.

Per ulteriori informazioni, iniziare leggendo la panoramica sulla governance dei [dati](../data-governance/home.md).

### Gestione delle richieste di privacy e rinuncia ai dati

Experience Platform consente ai clienti di inviare richieste di rifiuto correlate all&#39;utilizzo e all&#39;archiviazione dei loro dati nel profilo cliente in tempo reale. Per ulteriori informazioni sulla gestione delle richieste di rifiuto, consultate la documentazione relativa al [rispetto delle richieste](../segmentation/honoring-opt-outs.md)di rifiuto.

## Aggiungere dati al profilo cliente in tempo reale

La piattaforma può essere configurata per inviare i dati relativi a record e serie temporali a Profile, per supportare l’assimilazione in tempo reale dei flussi e l’assimilazione batch. Per ulteriori informazioni, consulta l’esercitazione che illustra come [aggiungere dati al profilo](tutorials/add-profile-data.md)cliente in tempo reale.

>[!Note]
>I dati raccolti tramite le soluzioni Adobe, inclusi Analytics Cloud, Marketing Cloud e Advertising Cloud, fluiscono nella piattaforma Experience e vengono trasferiti in Profile.

## Creare segmenti di pubblico

Il fulcro della tua campagna di marketing è il tuo pubblico. Il profilo cliente in tempo reale fornisce gli strumenti per segmentare la base cliente in audience composte da membri che soddisfano i criteri precisi richiesti. Con la segmentazione, potete isolare i membri del pubblico utilizzando criteri quali:

* Clienti per i quali è passata una settimana dall&#39;ultima operazione di acquisto.
* Clienti per i quali la somma degli acquisti è maggiore di $10.000.
* I clienti che hanno visto un certo numero di campagne marketing univoche da un elenco predefinito, specificato dal proprio ID campagna, e le hanno esplorate entro 30 minuti.

Per iniziare a usare la segmentazione, consulta la panoramica sulla [segmentazione](../segmentation/home.md).

## (Alfa) Configurare gli attributi calcolati

>[!IMPORTANT]
>La funzionalità degli attributi calcolati descritta in questo documento è in alfa. La documentazione e la funzionalità sono soggette a modifiche.

Gli attributi calcolati consentono di calcolare automaticamente il valore dei campi in base ad altri valori, calcoli ed espressioni. Gli attributi calcolati operano a livello di profilo, il che significa che puoi aggregare i valori per tutti i record ed eventi.

Ogni attributo calcolato contiene un&#39;espressione, o &quot;regola&quot;, che valuta i dati in arrivo e memorizza il valore risultante in un attributo di profilo o in un evento. Questi calcoli consentono di rispondere facilmente a domande relative a cose come il valore di acquisto del ciclo di vita, il tempo tra acquisti o il numero di aperture di applicazioni, senza che sia necessario eseguire manualmente calcoli complessi ogni volta che le informazioni sono necessarie.

Per ulteriori informazioni sugli attributi calcolati e istruzioni dettagliate per utilizzarli, consultate la [guida secondaria API Profilo cliente in tempo reale sugli attributi](api/computed-attributes.md)calcolati. Questa guida ti aiuterà a comprendere meglio il ruolo che gli attributi calcolati giocano all’interno di Adobe Experience Platform e include chiamate API di esempio per eseguire operazioni CRUD di base tramite l’API Profilo cliente in tempo reale.