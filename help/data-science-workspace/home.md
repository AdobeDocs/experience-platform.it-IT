---
keywords: ' Experience Platform;home;Data Science Workspace;argomenti più comuni;data Science workspace;data Science'
solution: Experience Platform
title: Panoramica di Analysis Workspace
topic: overview
description: Questa guida fornisce una panoramica dei concetti chiave relativi a Data Science Workspace in Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '2388'
ht-degree: 0%

---


# Panoramica di Analysis Workspace

Adobe Experience Platform [!DNL Data Science Workspace] utilizza l&#39;apprendimento automatico e l&#39;intelligenza artificiale per liberare informazioni dai dati. Integrato in Adobe Experience Platform, [!DNL Data Science Workspace] consente di creare previsioni utilizzando i contenuti e le risorse dati nelle soluzioni  Adobe.

I Data Scienziati di tutti i livelli di abilità troveranno strumenti sofisticati e facili da usare che supportano lo sviluppo rapido, la formazione e l&#39;ottimizzazione delle ricette di machine learning - tutti i vantaggi della tecnologia AI, senza la complessità.

Con [!DNL Data Science Workspace], gli esperti di dati possono creare facilmente API di servizi intelligenti, basate sull&#39;apprendimento automatico. Questi servizi funzionano con altri servizi  Adobe, inclusi  Adobe Target e Adobe Analytics Cloud, per aiutarti a automatizzare esperienze digitali personalizzate e mirate nelle app Web, desktop e mobili.

Questa guida fornisce una panoramica dei concetti chiave relativi a [!DNL Data Science Workspace].

## Introduzione

L&#39;azienda di oggi pone un&#39;alta priorità nell&#39;estrarre grandi dati per previsioni e informazioni che li aiuteranno a personalizzare le esperienze dei clienti e a fornire più valore ai clienti - e al business.
Per quanto importante, passare dai dati agli approfondimenti può costare molto. In genere richiede esperti esperti informatici che effettuano ricerche approfondite e lunghe sui dati per sviluppare modelli di apprendimento automatico, o ricette, che forniscono servizi intelligenti. Il processo è lungo, la tecnologia è complessa, e gli esperti scienziati di dati possono essere difficili da trovare.

Con [!DNL Data Science Workspace], Adobe Experience Platform consente di portare l&#39;intelligenza artificiale basata sull&#39;esperienza nell&#39;azienda, semplificando e accelerando la creazione di dati-approfondimenti-codice con:
- Framework di machine learning e runtime
- Accesso integrato ai dati archiviati in Adobe Experience Platform
- Uno schema dati unificato basato su [!DNL Experience Data Model] (XDM)
- Potenza di elaborazione essenziale per l&#39;apprendimento delle macchine/AI e la gestione di grandi insiemi di dati
- Ricette di machine learning preconfigurate per accelerare il passaggio a esperienze basate sull&#39;intelligenza artificiale
- Authoring, riutilizzo e modifica semplificati delle ricette per gli scienziati di dati con diversi livelli di abilità
- Pubblicazione e condivisione intelligente dei servizi in pochi clic, senza dover ricorrere a uno sviluppatore, e monitoraggio e riqualificazione per ottimizzare costantemente le esperienze dei clienti personalizzate

I Data Scienziati di tutti i livelli di competenza riusciranno a ottenere informazioni più rapidamente ed efficaci esperienze digitali prima.

## Introduzione

Prima di iniziare a conoscere i dettagli di [!DNL Data Science Workspace], ecco un breve riepilogo dei termini chiave:

| Termine | Definizione |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [!DNL Data Science Workspace] | [!DNL Data Science Workspace] all&#39;interno di  [!DNL Experience Platform] consente ai clienti di creare modelli di machine learning utilizzando dati tra le soluzioni di Adobe  [!DNL Experience Platform] e  per generare informazioni e previsioni intelligenti per creare esperienze digitali coinvolgenti per gli utenti finali. |
| Intelligenza artificiale | L&#39;intelligenza artificiale è una teoria e sviluppo di sistemi informatici in grado di eseguire attività che normalmente richiedono intelligenza umana, come la percezione visiva, il riconoscimento vocale, il processo decisionale e la traduzione tra le lingue. |
| Apprendimento automatico | L&#39;apprendimento automatico è il campo di studio che consente ai computer di imparare senza essere esplicitamente programmati. |
| [!DNL Sensei] Framework ML | [!DNL Sensei] ML Framework è un framework di machine learning unificato in  Adobe che sfrutta i dati  [!DNL Experience Platform] per consentire agli esperti di informatica di sviluppare servizi di intelligence guidati dall&#39;apprendimento automatico in modo più rapido, scalabile e riutilizzabile. |
| [!DNL Experience Data Model] | [!DNL Experience Data Model] (XDM) è lo sforzo di standardizzazione condotto da  Adobe per definire schemi standard quali  [!DNL Profile] e  [!DNL ExperienceEvent], per la gestione dell&#39;esperienza cliente. |
| [!DNL JupyterLab] | [!DNL JupyterLab] è un&#39;interfaccia Web open-source per Project Jupyter ed è strettamente integrata in  [!DNL Experience Platform]. |
| Ricette | Una ricetta è  termine  Adobe per una specifica di modello ed è un contenitore di primo livello che rappresenta uno specifico machine learning, un algoritmo AI o un insieme di algoritmi, una logica di elaborazione e una configurazione necessarie per creare ed eseguire un modello qualificato e quindi aiutare a risolvere problemi aziendali specifici. |
| Modello | Un modello è un&#39;istanza di una ricetta di machine learning che viene formata utilizzando dati storici e configurazioni per risolvere un caso d&#39;uso aziendale. |
| Formazione | La formazione è il processo di apprendimento di schemi e approfondimenti da dati etichettati. |
| Modello | Un modello preparato rappresenta l&#39;output eseguibile di un processo di formazione modello, in cui un insieme di dati di formazione è stato applicato all&#39;istanza del modello. Un modello qualificato manterrà un riferimento a qualsiasi servizio Web intelligente creato da esso. Il modello addestrato è adatto per il punteggio e la creazione di un servizio Web intelligente. Le modifiche a un modello qualificato possono essere tracciate come nuova versione. |
| Punteggio | Il punteggio è il processo di generazione di informazioni dai dati utilizzando un modello qualificato. |
| Servizio | Un servizio distribuito espone la funzionalità di un&#39;intelligenza artificiale, di un modello di machine learning o di un algoritmo avanzato attraverso un&#39;API, in modo che possa essere utilizzato da altri servizi o applicazioni per creare app intelligenti. |

Il grafico seguente delinea la relazione gerarchica tra Ricette, Modelli, Esecuzione formazione ed Esecuzione punteggio.

![](./images/home/recipe_hiearchy_ui.png)

## Comprensione di [!DNL Data Science Workspace]

Con [!DNL Data Science Workspace], gli esperti di dati possono semplificare il complicato processo di scoperta di informazioni in insiemi di dati di grandi dimensioni. Basato su un framework di machine learning e runtime comuni, [!DNL Data Science Workspace] offre gestione avanzata del flusso di lavoro, gestione dei modelli e scalabilità. I servizi intelligenti supportano il riutilizzo di ricette di machine learning per alimentare una serie di applicazioni create con prodotti e soluzioni  Adobe.

### Accesso diretto ai dati

I dati sono la pietra angolare dell&#39;intelligenza artificiale e dell&#39;apprendimento automatico.

[!DNL Data Science Workspace] è completamente integrato con Adobe Experience Platform, incluso il Data Lake  [!DNL Real-time Customer Profile], e  [!DNL Unified Edge]. Esplorate tutti i dati aziendali archiviati in Adobe Experience Platform contemporaneamente, insieme ai dati di grandi dimensioni e alle librerie di formazione approfondita comuni, come [!DNL Spark] ML e [!DNL TensorFlow]. In caso contrario, è necessario acquisire i propri set di dati utilizzando lo schema standard XDM.

### Ricette precostruite per l&#39;apprendimento automatico

[!DNL Data Science Workspace] include ricette precostruite per l&#39;apprendimento automatico per le esigenze aziendali più comuni, come la previsione delle vendite al dettaglio e il rilevamento delle anomalie, in modo che gli esperti e gli sviluppatori di dati non debbano iniziare da zero. Attualmente sono disponibili tre ricette: [previsione di acquisto di prodotti](./pre-built-recipes/product-purchase-prediction.md), [raccomandazioni di prodotti](./pre-built-recipes/product-recommendations.md) e [vendite al dettaglio](./pre-built-recipes/retail-sales.md).

[//]: # (The built-in recipe gallery offers recommendations for prebuilt recipes based on your business needs.)

Se preferite, potete adattare una ricetta predefinita alle vostre esigenze, importare una ricetta o iniziare da zero per creare una ricetta personalizzata. Tuttavia, una volta avviata la formazione e l&#39;ottimizzazione di una ricetta, la creazione di un servizio intelligente personalizzato non richiede uno sviluppatore, ma solo pochi clic e si è pronti a creare un&#39;esperienza digitale mirata e personalizzata.

### Flusso di lavoro incentrato sullo scienziato informatico

Qualunque sia il livello di esperienza nella scienza dei dati, [!DNL Data Science Workspace] consente di semplificare e accelerare il processo di ricerca di informazioni nei dati e di applicazione alle esperienze digitali.

### Esplorazione dei dati

Trovare i dati giusti e prepararli è la parte più impegnativa della costruzione di una ricetta efficace. [!DNL Data Science Workspace] e Adobe Experience Platform ti aiuterà a passare dai dati agli approfondimenti più rapidamente.

In Adobe Experience Platform, i dati multicanale sono centralizzati e memorizzati nello schema standard XDM, per cui i dati sono più facili da trovare, comprendere e pulire. Un unico archivio di dati basato su uno schema comune può consentirti di risparmiare innumerevoli ore di esplorazione e preparazione dei dati.

Mentre sfogliate, utilizzate R, [!DNL Python] o Scala con la [!DNL Jupyter Notebook] in hosting integrata per sfogliare il catalogo di dati su [!DNL Platform]. Utilizzando una di queste lingue, è inoltre possibile sfruttare i formati [!DNL Spark] ML e TensorFlow. Partire da zero o utilizzare uno dei modelli di notebook forniti per problemi aziendali specifici.

Come parte del flusso di lavoro di esplorazione dei dati, puoi anche acquisire nuovi dati o utilizzare funzionalità esistenti per facilitare la preparazione dei dati.

### Authoring

Con [!DNL Data Science Workspace] potete decidere come creare le ricette.

- Risparmiate tempo sfogliando una ricetta precostruita per soddisfare le vostre esigenze aziendali, che potete utilizzare così come è o configurare per soddisfare i vostri requisiti specifici.
- Create una ricetta da zero, utilizzando il runtime di authoring in Jupyter Notebook per sviluppare e registrare la ricetta.
- Caricate una ricetta creata all&#39;esterno di Adobe Experience Platform in [!DNL Data Science Workspace] o importate codice di ricetta da un repository, come [!DNL Git], utilizzando l&#39;autenticazione e l&#39;integrazione disponibili tra [!DNL Git] e [!DNL Data Science Workspace].

### Sperimentazione

Data Science Workspace offre un&#39;incredibile flessibilità al processo di sperimentazione. Iniziate con la vostra ricetta. Quindi create un&#39;istanza separata, utilizzando lo stesso algoritmo di base associato a caratteristiche univoche, come i parametri di Hyper-tuning. Potete creare tutte le istanze necessarie, formando e assegnando un punteggio a ciascuna istanza il numero desiderato di volte. Durante la formazione, [!DNL Data Science Workspace] tiene traccia delle ricette, delle istanze delle ricette e delle istanze formate, insieme alle metriche di valutazione, in modo da non doverlo fare.

### Operazionismo

Quando sei soddisfatto della tua ricetta, sono solo pochi clic per creare un servizio intelligente. Non è richiesta alcuna codifica: è possibile eseguire questa operazione autonomamente, senza coinvolgere sviluppatori o tecnici. Infine, pubblicate il servizio intelligente su  I/O Adobe ed è pronto per il vostro team di esperienza digitale da utilizzare.

<!--You can also publish your intelligent service to the Service Gallery, where it's available to specific people, specific organizations, or everyone who develops data solutions on Adobe Experience Platform. You can even share it with your external partners, and they can share their intelligent service with you. And the next time you're starting a new recipe, you can check the Service Gallery to see if there's a similar intelligent service you can use to get started. -->

### Miglioramento continuo

[!DNL Data Science Workspace] traccia le aree in cui vengono richiamati i servizi intelligenti e le relative prestazioni. Quando i dati entrano, potete valutare l&#39;accuratezza intelligente del servizio per chiudere il ciclo e riformare le ricette in base alle necessità per migliorare le prestazioni. Il risultato è un perfezionamento continuo nella precisione della personalizzazione dei clienti.

### Accesso a nuove funzioni e set di dati

Gli esperti informatici possono sfruttare le nuove tecnologie e i nuovi insiemi di dati non appena disponibili tramite  servizi di Adobe. Grazie a aggiornamenti frequenti, ci occupiamo dell&#39;integrazione di dataset e tecnologie nella piattaforma, per cui non è necessario.

### Sicurezza e tranquillità

Proteggere i dati è una priorità assoluta per  Adobe.  Adobe protegge i tuoi dati con processi e controlli di sicurezza sviluppati per contribuire a rispettare gli standard, le normative e le certificazioni accettati dal settore.

La sicurezza è integrata in software e servizi come parte del ciclo di vita del prodotto protetto  Adobe.
Per informazioni  sicurezza dei dati di Adobe e del software, conformità e altro ancora, visitare la pagina dedicata alla sicurezza all&#39;indirizzo https://www.adobe.com/security.html.

## [!DNL Data Science Workspace] in azione

Previsioni e approfondimenti forniscono le informazioni necessarie per fornire un&#39;esperienza altamente personalizzata a ogni cliente che visita il tuo sito Web, contatta il tuo call center o partecipa ad altre esperienze digitali. Ecco come si realizza il lavoro quotidiano con [!DNL Data Science Workspace].

### Definire il problema

Tutto inizia con un problema di business. Ad esempio, un call center online ha bisogno di un contesto che li aiuti a trasformare un sentimento negativo del cliente in positivo.

Ci sono un sacco di dati sul cliente. Hanno visitato il sito, messo gli articoli nel loro carrello, e anche gli ordini inseriti. Potrebbero aver ricevuto e-mail, usato buoni o contattato il call center in precedenza. La ricetta, quindi, deve utilizzare i dati disponibili sul cliente e le sue attività per determinare la propensione ad acquistare e consigliare un&#39;offerta che il cliente probabilmente apprezzerà e utilizzerà.

![](./images/home/example_problem.png)

Al momento del contatto del call center, il cliente ha ancora due paia di scarpe nel carrello, ma ha rimosso una camicia. Con queste informazioni, il servizio intelligente potrebbe raccomandare che l&#39;agente del call center offra un coupon per il 20% di sconto sulle scarpe durante la chiamata. Se il cliente utilizza il coupon, tali informazioni vengono aggiunte al set di dati e le previsioni diventano ancora migliori al successivo richiamo del cliente.

### Esplorare e preparare i dati

In base al problema aziendale definito, la ricetta dovrebbe esaminare tutte le transazioni web del cliente, incluse visite al sito, ricerche, visualizzazioni di pagina, collegamenti su cui si è fatto clic, azioni sul carrello, offerte ricevute, e-mail ricevute, interazioni con il call center e così via.

Un esperto di dati in genere spende fino al 75% del tempo necessario per creare una ricetta che esplora e trasforma i dati. I dati provengono spesso da più repository e vengono salvati in schemi diversi; per poter creare una ricetta, è necessario combinarli e mapparli.

[//]: # (Your first step is to check the recipe gallery to see if an existing recipe meets your needs, or comes close. An alternative is to import a recipe you created outside of Adobe Experience Platform. Starting with an existing recipe often streamlines the data exploration phase and makes it easier for a data scientist.)

Se iniziate da zero o configurate una ricetta esistente, iniziate la ricerca dei dati in un catalogo dati centralizzato e standardizzato per la vostra organizzazione, il che semplifica notevolmente la ricerca. Potreste anche scoprire che un altro esperto di dati nella vostra organizzazione ha già identificato un set di dati simile e scegliere di perfezionare tale set di dati invece di iniziare da zero.
Tutti i dati in Adobe Experience Platform sono conformi a uno schema XDM standard, eliminando la necessità di creare un modello complesso per l&#39;unione dei dati o di ottenere assistenza da un tecnico dei dati.

Se non si trovano immediatamente i dati necessari, ma esistono al di fuori di Adobe Experience Platform, è relativamente semplice acquisire set di dati aggiuntivi, che si trasformeranno anche nello schema XDM standard.\
È possibile utilizzare [!DNL Jupyter Notebook] per semplificare la pre-elaborazione dei dati, a partire da un modello di blocco appunti o da un blocco appunti precedentemente utilizzato per la propensione all&#39;acquisto.

![](./images/home/notebook_templates.png)

### Creazione della ricetta

Se avete già trovato una ricetta che soddisfa tutte le vostre esigenze, potete passare alla sperimentazione. In alternativa, è possibile modificare un po&#39; la ricetta o crearne una da zero, sfruttando il runtime di authoring [!DNL Data Science Workspace] in [!DNL Jupyter Notebook]. Il runtime di authoring consente di utilizzare il flusso di lavoro di formazione e valutazione [!DNL Data Science Workspace] e convertire la ricetta in un secondo momento, in modo che possa essere memorizzata e riutilizzata da altri utenti dell&#39;organizzazione.

Potete anche importare una ricetta in [!DNL Data Science Workspace] e sfruttare i flussi di lavoro di sperimentazione durante la creazione del servizio intelligente.

### Sperimentare con la ricetta

Con una ricetta che incorpora gli algoritmi di machine learning di base, molte istanze di ricette possono essere create con una singola ricetta. Tali istanze di ricette sono denominate modelli. Un modello richiede formazione e valutazione per ottimizzarne l&#39;efficienza operativa e l&#39;efficacia, un processo generalmente costituito da tentativi ed errori.

![](./images/home/recipe_hiearchy_ui.png)

Durante la formazione dei modelli, vengono generati percorsi di formazione e valutazioni. [!DNL Data Science Workspace] tiene traccia delle metriche di valutazione per ciascun modello univoco e delle relative esecuzioni di formazione. Le metriche di valutazione generate mediante la sperimentazione consentiranno di determinare l&#39;esecuzione della formazione che esegue meglio.

![](./images/home/evaluation_metrics.png)

È possibile visitare l&#39;esercitazione [API](./models-recipes/train-evaluate-model-api.md) o [UI](./models-recipes/train-evaluate-model-ui.md) su come formare e valutare i modelli in [!DNL Data Science Workspace].

### Operazionalizzare il modello

Dopo aver selezionato la ricetta più adatta alle esigenze aziendali, è possibile creare un servizio intelligente in [!DNL Data Science Workspace] senza assistenza da parte dello sviluppatore. Sono solo un paio di click - non è necessaria la codifica. Un servizio intelligente pubblicato è accessibile ad altri membri dell&#39;organizzazione senza la necessità di ricreare il modello.

Un servizio intelligente pubblicato è configurabile per formarsi automaticamente di tanto in tanto utilizzando nuovi dati man mano che diventano disponibili. In questo modo, il vostro servizio mantiene la sua efficienza e la sua efficacia man mano che il tempo continua.

## Passaggi successivi

[!DNL Data Science Workspace] consente di semplificare e semplificare il flusso di lavoro basato sulla scienza dei dati, dalla raccolta dei dati agli algoritmi fino ai servizi intelligenti per gli esperti di dati di tutti i livelli di competenza. Grazie agli strumenti sofisticati [!DNL Data Science Workspace], è possibile ridurre notevolmente il tempo dai dati agli approfondimenti.

Più importante, [!DNL Data Science Workspace] mette le funzionalità di ottimizzazione algoritmica e scienza dei dati di  Adobe  piattaforma di marketing leader nelle mani di esperti aziendali. Per la prima volta, le aziende possono portare algoritmi proprietari alla piattaforma, sfruttando  potente machine learning  capacità di intelligenza artificiale e di intelligenza artificiale per offrire esperienze cliente altamente personalizzate su vasta scala.

Con il matrimonio di competenze di marchio e  Adobe  machine learning e intelligenza artificiale, le aziende hanno il potere di promuovere più valore commerciale e fedeltà di marchio dando ai clienti ciò che vogliono, prima di chiederlo.

Per ulteriori informazioni, ad esempio un flusso di lavoro giornaliero completo, consultare la documentazione di [Data Science Workspace](./walkthrough.md)

## Risorse aggiuntive

Il seguente video è stato progettato per consentire agli utenti di comprendere meglio [!DNL Data Science Workspace].

>[!VIDEO](https://video.tv.adobe.com/v/30567?quality=12&amp;enable10seconds=on&amp;speedcontrol=on)

