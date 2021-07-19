---
title: Creare un’inserzione in Exchange per un’estensione
description: Scopri come aggiungere l’estensione al catalogo pubblico in Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '1162'
ht-degree: 63%

---

# Creare un’inserzione in Exchange per un’estensione

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Adobe Experience Platform dispone di un singolo catalogo unificato in cui gli utenti possono visualizzare le estensioni dei tag disponibili per l’installazione. Questo catalogo è disponibile all’interno del prodotto e contiene estensioni di tre tipi:

1. **Estensioni pubbliche**: si tratta di estensioni completate progettate per l’utilizzo in produzione da parte di qualsiasi utente.
1. **Estensioni private**: si tratta di estensioni completate progettate per la produzione, ma sviluppate da altri utenti della tua azienda e disponibili solo per gli utenti della tua azienda.
1. **Estensioni di sviluppo**: queste estensioni sono in fase di sviluppo attivo e sono disponibili solo all’interno dell’azienda e solo su una proprietà specificamente designata come proprietà di sviluppo.

A parte le estensioni nel catalogo dei prodotti, alcune estensioni sono anche disponibili come inserzioni in [Experience Cloud Exchange Marketplace](https://exchange.adobe.com/experiencecloud.experience-platform-launch.html#product).

Queste consentono agli sviluppatori di estensioni di pubblicare descrizioni delle funzionalità, fornire collegamenti per supporto aggiuntivo o documentazione, e presentare le estensioni a potenziali utenti che potrebbero non essere a conoscenza della società o della funzionalità dell’estensione. Nel Marketplace, all’estensione è associata un’inserzione pubblica che può essere visualizzata senza che l’utente sia autenticato su Platform.  Molti sviluppatori trovano utile sviluppare un’inserzione per Exchange, ma non è un passaggio obbligatorio.

Se non disponi di una società che possa caricare e testare il pacchetto di estensione, registrati per il programma Exchange e inizia a creare un’inserzione.  Questo attiverà la creazione di un account aziendale (richiede un po’ di tempo, al termine riceverai un’e-mail) che puoi utilizzare per caricare e testare l’estensione.  Non è mai necessario rendere pubblica l’inserzione.

Se disponi già di un account aziendale o se non hai intenzione di completare l’inserzione, puoi saltare il resto di questo passaggio e procedere al [caricamento e test dell’estensione](./upload-and-test.md).

## Creare un’inserzione

>[!NOTE]
>
>Il seguente processo descrive la creazione di un elenco di applicazioni nel programma Adobe Exchange. Questo è il termine utilizzato per le varie integrazioni ed estensioni in Adobe Experience Platform.

![Experience Cloud posizione del collegamento ad App Manager](../images/getting-started/app-mgr-link.png)

1. Accedi al [sito Exchange Partner](https://partners.adobe.com/exchangeprogram/experiencecloud). Una volta effettuato l&#39;accesso, seleziona il collegamento **App Manager** accanto al tuo nome.
1. Seleziona la scheda **Crea nuova applicazione** , quindi seleziona **Crea nuova app** per una soluzione personalizzata oppure seleziona un modello applicabile.
1. Specifica le informazioni della tua inserzione. Per informazioni dettagliate su App Manager, consulta l’[articolo completo](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360024197931). Le informazioni sull’elenco devono essere molto chiare sulle attività dell’estensione e sul motivo per cui sono utili. L’elenco funziona come uno spazio di marketing per la tua app. Promuovi l’estensione qui utilizzando descrizioni chiare, collegamenti alle pagine di destinazione sul tuo sito, collegamenti ai documenti di aiuto o indirizzi e-mail di supporto e così via. Anche se lo spazio nelle visualizzazioni delle estensioni è limitato, l&#39;elenco di Exchange offre l&#39;opportunità di promuovere sia l&#39;estensione che la società. Di seguito sono riportati alcuni suggerimenti per migliorare la promozione dell&#39;estensione:
   - **Icona app**: accertati che l’icona per l’inserzione su Exchange abbia le dimensioni appropriate, 512 x 512 per i file png o proporzioni 1:1 per i file jpg.

   >[!NOTE]
   >
   >Si tratta di un formato di file diverso da quello utilizzato nel codice di estensione. L’estensione stessa conterrà come [icona](../manifest.md) un file svg.
   
   - **Immagine in primo piano** : ottieni attenzione utilizzando un&#39;immagine che può rimanere isolata e mostrerà il tuo marchio ed evidenziare la tua applicazione. L&#39;immagine in primo piano è quella mostrata quando qualcuno condivide un collegamento alla tua inserzione o post su di essa sui social media. Deve quindi essere una rappresentazione modello del tuo marchio.
   - **Logo dell’editore dell’app**: questo è il logo aziendale; assicurati che l’icona abbia le dimensioni appropriate, pari a 1280 x 720 oppure 2560 x 1440 (16:9) in formato png o jpg.
   - **Istruzioni di configurazione**  - Informare i clienti su come configurare l&#39;estensione Adobe Experience Platform. Assicurati che siano ben chiare le impostazioni e i passaggi successivi richiesti quando viene visualizzata la [vista di configurazione](../configuration.md), subito dopo l’installazione dell’estensione in una proprietà. 
   - **Tag**: nella prima pagina di modifica dell’inserzione, assicurati di includere la parola “Launch” nel campo “Tag personalizzati”. Questo farà apparire il tuo annuncio nella ricerca di tag nel marketplace di Exchange:
      ![](../images/getting-started/custom-tags.jpg)
   - **Sandbox**  - L&#39;accesso alle soluzioni Adobe avviene tramite un account Sandbox in cui puoi accedere a una versione completamente funzionante di Adobe Experience Platform. Gli account Sandbox sono richiesti quando si crea l’inserzione dell’applicazione. Nella sezione **Connessioni** seleziona le connessioni specifiche applicabili all&#39;applicazione creata (estensione tag) e quando premi **Salva**, la richiesta sandbox verrà generata se necessario.
1. Invia la tua inserzione. Il team di Adobe Exchange esaminerà l’applicazione e fornirà feedback nel caso siano necessari aggiornamenti. Se contrassegni la casella di controllo **pubblica immediatamente** quando invii l&#39;inserzione, questa verrà pubblicata immediatamente dopo l&#39;approvazione. Se desideri pubblicare l’applicazione in un secondo momento, lascia deselezionata la casella di controllo . Quando l&#39;elenco delle estensioni è approvato, accanto ad esso verrà visualizzato un pulsante blu **Pubblica** nella pagina degli elenchi delle estensioni.

### Creare un’inserzione efficace

Le [linee guida per l’invio delle app](https://partners.adobe.com/exchangeprogram/experiencecloud/build/ec-exchange.html) contengono informazioni dettagliate su come creare un’inserzione convincente.

#### Dopo l’invio dell’inserzione Exchange

Dopo l’invio, il team Adobe Exchange esaminerà l’applicazione e la approverà o fornirà commenti in merito a eventuali modifiche da apportare. Questo processo è descritto nelle linee guida per l’invio delle app.

Se non disponi di un login per il sito di Exchange, assicurati che il tuo indirizzo e-mail sia registrato per il programma Exchange seguendo le istruzioni riportate nella [guida alla registrazione per il programma](https://partners.adobe.com/content/mcp/us/en/home/reg-guide.html). Ogni utente deve associare la propria e-mail all’account partner della propria azienda. Le domande su questo processo possono essere indirizzate via e-mail a <ExchangeHelpEC@adobe.com>.

#### Aggiornare l’inserzione Exchange dopo l’approvazione iniziale

Se hai aggiornato l&#39;estensione, o semplicemente se desideri aggiornare l&#39;inserzione su Exchange, accedi al [portale Partner](https://partners.adobe.com/exchangeprogram/experiencecloud) e fai clic sul pulsante App Manager accanto al tuo nome. Seleziona quindi l’applicazione e segui il flusso descritto qui sopra per la creazione dell’inserzione. Dopo il nuovo invio, il team Adobe Exchange controllerà e approverà le modifiche oppure risponderà con eventuali commenti in merito alle modifiche necessarie.

## Collegare il pacchetto di estensione all’inserzione

Dopo aver approvato e reso pubblicamente disponibile l’inserzione, ti consigliamo di fornire un collegamento all’inserzione pubblica nel campo `exchange_url` del file `extension.json` all’interno del pacchetto di estensione.  Questo creerà un collegamento “Ulteriori informazioni” all’interno del catalogo delle estensioni del Platform Launch in modo che gli utenti del prodotto possano trovare la tua inserzione e le relative informazioni.
