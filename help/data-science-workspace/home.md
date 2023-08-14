---
keywords: Experience Platform;home;Data Science Workspace;argomenti popolari;data science workspace;data science science workspace;data science
solution: Experience Platform
title: Panoramica di Data Science Workspace
description: Questa guida fornisce una panoramica dei concetti chiave relativi a Data Science Workspace in Adobe Experience Platform.
exl-id: bef25073-0dfb-453d-8c32-7f44d917d62d
source-git-commit: fa52aa668d21f71c0da6b35c933713f068e36b28
workflow-type: tm+mt
source-wordcount: '2448'
ht-degree: 0%

---

# Panoramica di Data Science Workspace

>[!NOTE]
>
>La presenza della documentazione su una funzione di Experience League non ne garantisce la disponibilità per tutti i clienti. Questa funzione è disponibile solo per i clienti esistenti che hanno acquistato una licenza Adobe Experience Platform o Adobe Experience Platform Intelligence. Fai riferimento alla descrizione ufficiale del prodotto per comprendere le funzioni e altri dettagli associati agli SKU/prodotti acquistati.


Adobe Experience Platform [!DNL Data Science Workspace] utilizza l’apprendimento automatico e l’intelligenza artificiale per sfruttare le informazioni provenienti dai tuoi dati. Integrato in Adobe Experience Platform, [!DNL Data Science Workspace] consente di effettuare previsioni utilizzando i contenuti e i dati delle risorse tra le soluzioni Adobe.

I data scientist di tutti i livelli di competenza troveranno strumenti sofisticati e facili da utilizzare che supportano lo sviluppo rapido, la formazione e il tuning delle ricette di apprendimento automatico, tutti vantaggi della tecnologia di intelligenza artificiale, senza la complessità.

Con [!DNL Data Science Workspace], i data scientist possono creare facilmente API di servizi intelligenti basate sull’apprendimento automatico. Questi servizi funzionano con altri servizi di Adobe, tra cui Adobe Target e Adobe Analytics Cloud, per aiutarti ad automatizzare esperienze digitali personalizzate e mirate nelle app web, desktop e mobili.

Questa guida fornisce una panoramica dei concetti chiave relativi a [!DNL Data Science Workspace].

## Introduzione

Le aziende odierne danno la massima priorità al data mining per previsioni e approfondimenti che le aiuteranno a personalizzare le esperienze dei clienti e a fornire più valore ai clienti e al business.
Per quanto importante, passare dai dati alle informazioni può comportare costi elevati. In genere, per sviluppare modelli di apprendimento automatico, o ricette, che alimentano i servizi intelligenti, è necessario ricorrere a data scientist qualificati che conducano ricerche di dati intensive e dispendiose in termini di tempo. Il processo è lungo, la tecnologia è complessa e i data scientist competenti possono essere difficili da trovare.

Con [!DNL Data Science Workspace], Adobe Experience Platform consente di portare nell’azienda un’intelligenza artificiale incentrata sull’esperienza, semplificando e accelerando la conversione dei dati in informazioni e codice con:
- Un framework di apprendimento automatico e runtime
- Accesso integrato ai dati memorizzati in Adobe Experience Platform
- Uno schema di dati unificato basato su [!DNL Experience Data Model] (XDM)
- La potenza di elaborazione essenziale per l’apprendimento automatico/IA e la gestione di grandi set di dati
- Ricette di apprendimento automatico precompilate per accelerare il passaggio alle esperienze basate sull’intelligenza artificiale
- Authoring semplificato, riutilizzo e modifica di ricette per data scientist di vari livelli di competenza
- Pubblicazione e condivisione di servizi intelligenti in pochi clic, senza dover ricorrere a uno sviluppatore, e monitoraggio e aggiornamento per l’ottimizzazione continua di esperienze cliente personalizzate

I data scientist di tutti i livelli di competenza otterranno informazioni approfondite prima possibile ed esperienze digitali più efficaci.

## Introduzione

Prima di immergerti nei dettagli di [!DNL Data Science Workspace], ecco una breve sintesi dei termini chiave:

| Termine | Definizione |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [!DNL Data Science Workspace] | [!DNL Data Science Workspace] entro [!DNL Experience Platform] consente ai clienti di creare modelli di apprendimento automatico utilizzando i dati in [!DNL Experience Platform] e soluzioni di Adobe per generare insight intelligenti e previsioni per intrecciare esperienze digitali piacevoli per l’utente finale. |
| Intelligenza artificiale | L&#39;intelligenza artificiale è una teoria e uno sviluppo di sistemi informatici che sono in grado di eseguire compiti che normalmente richiedono intelligenza umana, come la percezione visiva, il riconoscimento vocale, il processo decisionale e la traduzione tra lingue diverse. |
| Apprendimento automatico | L&#39;apprendimento automatico è il campo di studio che consente ai computer di apprendere senza essere esplicitamente programmati. |
| [!DNL Sensei] Framework ML | [!DNL Sensei] Il framework ML è un framework di apprendimento automatico unificato in tutti gli Adobi che sfrutta i dati su [!DNL Experience Platform] consentire ai data scientist di sviluppare servizi di intelligence basati sull’apprendimento automatico in modo più rapido, scalabile e riutilizzabile. |
| [!DNL Experience Data Model] | [!DNL Experience Data Model] (XDM) è lo sforzo di standardizzazione condotto dall’Adobe per definire schemi standard come [!DNL Profile] e [!DNL ExperienceEvent], per la gestione della customer experience. |
| [!DNL JupyterLab] | [!DNL JupyterLab] è un’interfaccia open-source basata su web per Project Jupyter ed è strettamente integrata in [!DNL Experience Platform]. |
| Ricette | Una ricetta è il termine Adobe per una specifica di modello ed è un contenitore di livello superiore che rappresenta un apprendimento automatico specifico, un algoritmo di intelligenza artificiale o un insieme di algoritmi, una logica di elaborazione e una configurazione necessarie per creare ed eseguire un modello addestrato e quindi contribuire a risolvere problemi di business specifici. |
| Modello | Un modello è un’istanza di una ricetta di apprendimento automatico che viene addestrata utilizzando dati e configurazioni storici per risolvere un caso d’uso aziendale. |
| Formazione | La formazione è il processo di apprendimento dei pattern e delle informazioni dai dati etichettati. |
| Modello addestrato | Un modello addestrato rappresenta l’output eseguibile di un processo di apprendimento del modello, in cui un set di dati di addestramento è stato applicato all’istanza del modello. Un modello addestrato manterrà un riferimento a qualsiasi servizio web intelligente creato da esso. Il modello addestrato è adatto per il punteggio e la creazione di un servizio web intelligente. Le modifiche a un modello addestrato possono essere tracciate come nuova versione. |
| Punteggio | Il punteggio è il processo di generazione di informazioni dai dati utilizzando un modello addestrato. |
| Servizio | Un servizio implementato espone funzionalità di un’intelligenza artificiale, un modello di apprendimento automatico o un algoritmo avanzato tramite un’API in modo che possa essere utilizzato da altri servizi o applicazioni per creare app intelligenti. |

Il grafico seguente illustra la relazione gerarchica tra le composizioni, i modelli, le esecuzioni di formazione e le esecuzioni di punteggio.

![](./images/home/recipe_hiearchy_ui.png)

## Comprensione di [!DNL Data Science Workspace]

Con [!DNL Data Science Workspace]Inoltre, i data scientist possono semplificare il complicato processo di ricerca di informazioni in set di dati di grandi dimensioni. Basato su un quadro comune di apprendimento automatico e runtime, [!DNL Data Science Workspace] offre funzioni avanzate di gestione dei flussi di lavoro, gestione dei modelli e scalabilità. I servizi intelligenti supportano il riutilizzo di formule di apprendimento automatico per potenziare una serie di applicazioni create utilizzando prodotti e soluzioni di Adobe.

### Accesso ai dati unico

I dati sono la pietra angolare dell’intelligenza artificiale e dell’apprendimento automatico.

[!DNL Data Science Workspace] è completamente integrato con Adobe Experience Platform, incluso Data Lake, [!DNL Real-Time Customer Profile], e [!DNL Unified Edge]. Esplora tutti i dati organizzativi memorizzati in Adobe Experience Platform contemporaneamente, insieme a big data comuni e librerie di apprendimento profondo, come [!DNL Spark] ML e [!DNL TensorFlow]. Se non trovi ciò che ti serve, acquisisci i tuoi set di dati utilizzando lo schema XDM standardizzato.

### Ricette di apprendimento automatico precompilate

[!DNL Data Science Workspace] include ricette di apprendimento automatico precompilate per esigenze aziendali comuni, come la previsione delle vendite al dettaglio e il rilevamento delle anomalie, in modo che data scientist e sviluppatori non debbano iniziare da zero. Attualmente sono disponibili tre ricette, [previsione di acquisto prodotto](./pre-built-recipes/product-purchase-prediction.md), [prodotti consigliati](./pre-built-recipes/product-recommendations.md), e [vendite al dettaglio](./pre-built-recipes/retail-sales.md).

[//]: # (The built-in recipe gallery offers recommendations for prebuilt recipes based on your business needs.)

Se preferisci, puoi adattare una ricetta predefinita alle tue esigenze, importare una ricetta o iniziare da zero per creare una ricetta personalizzata. Tuttavia, una volta che hai preparato e ottimizzato una ricetta, la creazione di un servizio intelligente personalizzato non richiede uno sviluppatore, ma richiede solo pochi clic e sei pronto per creare un’esperienza digitale mirata e personalizzata.

### Flusso di lavoro incentrato sul data scientist

Qualunque sia il tuo livello di competenza nella scienza dei dati, [!DNL Data Science Workspace] consente di semplificare e accelerare il processo di ricerca di informazioni approfondite nei dati e di applicarle alle esperienze digitali.

### Esplorazione dei dati

Trovare i dati giusti e prepararli è la parte più laboriosa della creazione di una ricetta efficace. [!DNL Data Science Workspace] e Adobe Experience Platform ti aiuterà a passare più rapidamente dai dati alle informazioni.

In Adobe Experience Platform, i dati cross-channel sono centralizzati e memorizzati nello schema standardizzato XDM, in modo che siano più facili da trovare, comprendere e pulire. Un singolo archivio di dati basato su uno schema comune può consentirti di risparmiare innumerevoli ore di esplorazione e preparazione dei dati.

Durante la navigazione, utilizzare R, [!DNL Python], o Scala con integrato, in hosting [!DNL Jupyter Notebook] per sfogliare il catalogo di dati su [!DNL Platform]. Utilizzando una di queste lingue, puoi anche sfruttare [!DNL Spark] ML e TensorFlow. Iniziare da zero o utilizzare uno dei modelli di blocco appunti forniti per problemi di business specifici.

Come parte del flusso di lavoro di esplorazione dei dati, puoi anche acquisire nuovi dati o utilizzare funzioni esistenti per facilitare la preparazione dei dati.

### Authoring

Con [!DNL Data Science Workspace], decidi come creare le ricette.

- Risparmia tempo cercando una ricetta predefinita che soddisfi le tue esigenze aziendali e che puoi utilizzare così come è o configurare per soddisfare esigenze specifiche.
- Crea una ricetta da zero, utilizzando il runtime di authoring in Jupyter Notebook per sviluppare e registrare la ricetta.
- Caricare in una ricetta creata al di fuori di Adobe Experience Platform [!DNL Data Science Workspace] o importare il codice della ricetta da un archivio, ad esempio [!DNL Git], utilizzando l’autenticazione e l’integrazione disponibili tra [!DNL Git] e [!DNL Data Science Workspace].

### Sperimentazione

Data Science Workspace offre una flessibilità straordinaria nel processo di sperimentazione. Inizia con la tua ricetta. Quindi crea un’istanza separata, utilizzando lo stesso algoritmo di base associato a caratteristiche univoche, ad esempio i parametri di hyper-tuning. Puoi creare tutte le istanze necessarie, addestrando e assegnando a ogni istanza il numero di volte desiderato. Mentre li alleni, [!DNL Data Science Workspace] tiene traccia di ricette, istanze di ricette e istanze formate, insieme a metriche di valutazione, in modo da non doverlo fare.

### Operazionalizzazione

Quando sei soddisfatto della tua ricetta, sono solo pochi clic per creare un servizio intelligente. Non è richiesta alcuna codifica: puoi farlo autonomamente, senza coinvolgere uno sviluppatore o un ingegnere. Infine, pubblica il servizio intelligente in Adobe IO ed è pronto per essere utilizzato dal team di esperienza digitale.

<!--You can also publish your intelligent service to the Service Gallery, where it's available to specific people, specific organizations, or everyone who develops data solutions on Adobe Experience Platform. You can even share it with your external partners, and they can share their intelligent service with you. And the next time you're starting a new recipe, you can check the Service Gallery to see if there's a similar intelligent service you can use to get started. -->

### Miglioramento continuo

[!DNL Data Science Workspace] tiene traccia di dove vengono richiamati i servizi intelligenti e delle loro prestazioni. Man mano che i dati entrano in funzione, puoi valutare la precisione del servizio intelligente per chiudere il ciclo e riqualificare le ricette in base alle esigenze per migliorare le prestazioni. Il risultato è un continuo perfezionamento nella precisione della personalizzazione del cliente.

### Accesso a nuove funzioni e set di dati

I data scientist possono sfruttare le nuove tecnologie e i nuovi set di dati non appena sono disponibili tramite i servizi Adobe. Attraverso frequenti aggiornamenti, facciamo il lavoro di integrazione di set di dati e tecnologie nella piattaforma, quindi non è necessario.

### Sicurezza e tranquillità

La protezione dei dati è una priorità fondamentale, ad Adobe. Adobe protegge i dati con processi di sicurezza e controlli sviluppati per rispettare gli standard, le normative e le certificazioni accettati dal settore.

La sicurezza è integrata nel software e nei servizi come parte del ciclo di vita sicuro dei prodotti Adobe.
Per informazioni sulla sicurezza dei dati e del software di Adobe, sulla conformità e altro ancora, visita la pagina dedicata alla sicurezza all’indirizzo https://www.adobe.com/security.html.

## [!DNL Data Science Workspace] in azione

Le previsioni e le informazioni forniscono le informazioni necessarie per fornire un’esperienza altamente personalizzata a ogni cliente che visita il sito web, contatta il call center o si impegna in altre esperienze digitali. Ecco come avviene il tuo lavoro quotidiano con [!DNL Data Science Workspace].

### Definire il problema

Tutto inizia con un problema di business. Ad esempio, un call center online ha bisogno di contesto per aiutarli a trasformare un sentimento negativo del cliente in positivo.

Ci sono molti dati sul cliente. Hanno navigato nel sito, inserito articoli nel carrello e persino effettuato ordini. Potrebbero aver ricevuto e-mail, utilizzato coupon o contattato il call center in precedenza. La ricetta, quindi, deve utilizzare i dati disponibili sul cliente e le sue attività per determinare la propensione ad acquistare e consigliare un’offerta che il cliente probabilmente apprezzerà e utilizzerà.

![](./images/home/example_problem.png)

Al momento del contatto del call center, il cliente ha ancora due paia di scarpe nel carrello, ma ha rimosso una camicia. Con queste informazioni, il servizio intelligente potrebbe consigliare all’agente del call center di offrire un coupon per il 20% di sconto sulle scarpe durante la chiamata. Se il cliente utilizza il coupon, tali informazioni vengono aggiunte al set di dati e le previsioni diventano ancora migliori la prossima volta che il cliente chiama.

### Esplorare e preparare i dati

In base al problema di business definito, sai che la ricetta deve esaminare tutte le transazioni web del cliente, incluse visite al sito, ricerche, visualizzazioni di pagina, collegamenti selezionati, azioni del carrello, offerte ricevute, e-mail ricevute, interazioni con i call center e così via.

In genere, un data scientist impiega fino al 75% del tempo necessario per creare una ricetta per l’esplorazione e la trasformazione dei dati. I dati spesso provengono da più archivi e vengono salvati in schemi diversi; devono essere combinati e mappati prima di poter essere utilizzati per creare una ricetta.

[//]: # (Your first step is to check the recipe gallery to see if an existing recipe meets your needs, or comes close. An alternative is to import a recipe you created outside of Adobe Experience Platform. Starting with an existing recipe often streamlines the data exploration phase and makes it easier for a data scientist.)

Se inizi da zero o configuri una ricetta esistente, inizia la ricerca dei dati in un catalogo dati centralizzato e standardizzato per la tua organizzazione, il che semplifica notevolmente la ricerca. Potresti anche notare che un altro data scientist della tua organizzazione ha già identificato un set di dati simile e scegliere di perfezionarlo invece di iniziare da zero.
Tutti i dati in Adobe Experience Platform sono conformi a uno schema XDM standardizzato, eliminando la necessità di creare un modello complesso per unire i dati o ottenere assistenza da un data engineer.

Se i dati necessari non vengono trovati immediatamente, ma si trovano al di fuori di Adobe Experience Platform, è relativamente semplice acquisire set di dati aggiuntivi, che si trasformeranno anche nello schema XDM standardizzato.\
È possibile utilizzare [!DNL Jupyter Notebook] per semplificare la pre-elaborazione dei dati, ad esempio partendo da un modello di notebook o da un notebook già utilizzato in precedenza per aumentare la propensione all&#39;acquisto.

![](./images/home/notebook_templates-new.png)

### Creare la ricetta

Se hai già trovato una ricetta che soddisfa tutte le tue esigenze, puoi passare alla sperimentazione. Oppure, puoi modificare un po’ la ricetta o crearne una da zero - sfruttando il [!DNL Data Science Workspace] runtime di authoring in [!DNL Jupyter Notebook]. L’utilizzo del runtime di authoring consente di utilizzare sia [!DNL Data Science Workspace] flusso di lavoro di formazione e valutazione e converti la ricetta in un secondo momento in modo che possa essere memorizzata e riutilizzata da altri nella tua organizzazione.

Puoi anche importare una ricetta in [!DNL Data Science Workspace] e approfitta dei flussi di lavoro di sperimentazione per creare il tuo servizio intelligente.

### Sperimentate la ricetta

Con una ricetta che incorpora i tuoi algoritmi di apprendimento automatico di base, molte istanze di ricetta possono essere create con una singola ricetta. Queste istanze di ricette sono denominate modelli. Un modello richiede formazione e valutazione per ottimizzarne l&#39;efficienza operativa e l&#39;efficacia, un processo tipicamente costituito da tentativi ed errori.

![](./images/home/recipe_hiearchy_ui.png)

Durante l’addestramento dei modelli, vengono generate le esecuzioni dei corsi di formazione e le valutazioni. [!DNL Data Science Workspace] tiene traccia delle metriche di valutazione per ogni modello univoco e delle relative esecuzioni di addestramento. Le metriche di valutazione generate tramite la sperimentazione ti consentiranno di determinare l’esecuzione del corso di formazione con le prestazioni migliori.

![](./images/home/evaluation_metrics.png)

Visita il [API](./models-recipes/train-evaluate-model-api.md) o [UI](./models-recipes/train-evaluate-model-ui.md) tutorial su come addestrare e valutare i modelli in [!DNL Data Science Workspace].

### Operazionalizzare il modello

Dopo aver selezionato la ricetta più adatta alle tue esigenze aziendali, puoi creare un servizio intelligente in [!DNL Data Science Workspace] senza assistenza per gli sviluppatori. Sono sufficienti un paio di clic, non è richiesta alcuna codifica. Un servizio intelligente pubblicato è accessibile agli altri membri dell’organizzazione senza la necessità di ricreare il modello.

Un servizio intelligente pubblicato è configurabile per addestrarsi automaticamente di tanto in tanto utilizzando i nuovi dati man mano che diventano disponibili. In questo modo l&#39;efficienza e l&#39;efficacia del servizio vengono mantenute con il passare del tempo.

## Passaggi successivi

[!DNL Data Science Workspace] consente di semplificare e semplificare il flusso di lavoro della data science, dalla raccolta di dati agli algoritmi fino ai servizi intelligenti per data scientist di tutti i livelli di competenza. Con strumenti sofisticati [!DNL Data Science Workspace] fornisce, puoi ridurre in modo significativo il tempo che intercorre tra i dati e gli approfondimenti.

Ancora più importante, [!DNL Data Science Workspace] mette la data science e le funzionalità di ottimizzazione algoritmica della principale piattaforma di marketing Adobe nelle mani dei data scientist di livello enterprise. Per la prima volta, le aziende possono implementare algoritmi proprietari nella piattaforma, sfruttando le potenti funzionalità di machine learning e AI di Adobe per fornire ai clienti esperienze altamente personalizzate su vasta scala.

Con la combinazione di competenze del brand e apprendimento automatico e capacità di intelligenza artificiale degli Adobi, le aziende hanno la possibilità di promuovere più valore e fedeltà al brand offrendo ai clienti ciò che desiderano, prima che lo richiedano.

Per ulteriori informazioni, ad esempio un flusso di lavoro giornaliero completo, leggi [Procedura dettagliata su Data Science Workspace](./walkthrough.md) documentazione.

## Risorse aggiuntive

Il video seguente è stato progettato per comprendere [!DNL Data Science Workspace].

>[!VIDEO](https://video.tv.adobe.com/v/30567?quality=12&amp;enable10seconds=on&amp;speedcontrol=on)