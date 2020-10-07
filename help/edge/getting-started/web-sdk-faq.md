---
title: Domande frequenti su SDK Web
seo-title: Domande frequenti su Adobe Experience Platform Web SDK
description: Domande frequenti sull’SDK Adobe Experience Platform Web
seo-description: Domande frequenti sull’SDK Adobe Experience Platform Web
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '1683'
ht-degree: 2%

---


# Domande frequenti 

Queste domande frequenti includono domande frequenti sull’SDK Web per Adobi .

## Cos&#39;è Adobe Experience Platform Web SDK?

Adobe Experience Platform Web SDK è una libreria JavaScript lato client che consente ai clienti di Adobe Experience Cloud di interagire con i vari servizi nell&#39;Experience Cloud di .

Invia i dati in modo non dipendente dalla soluzione (XDM) ad Adobe Experience Platform Edge Network, che poi mappa i dati in formati e destinazioni specifici della soluzione e li invia in tempo reale.

**Maggiori informazioni**[presentazione al Adobe](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html)

## In che modo Adobe Experience Platform Web SDK differisce dalle soluzioni precedenti?

### Prima di Adobe Experience Platform SDK

Attualmente, è necessario distribuire librerie JavaScript diverse basate su ogni singola soluzione.

* Ogni soluzione dispone di una propria libreria, schema e dominio JavaScript.
* Nessuna di queste librerie è stata creata per lavorare tra di loro.
* I casi di utilizzo tra soluzioni e Adobe Experience Platform richiedono l&#39;interdipendenza di queste librerie diverse, con conseguente attrito nella distribuzione.

Anche se  Adobe Experience Platform Launch semplifica il più possibile l&#39;implementazione e la gestione di queste librerie, permangono problemi con:

* Dimensione libreria ( codice Adobe eccessivo su una pagina)
* Prestazioni (il caricamento dei siti richiede troppo tempo)
* Chiamate multiple per un singolo caso di utilizzo
* Attesa del ritorno ECID prima delle chiamate di personalizzazione (causa ritardo)
* Raccolta di dati frammentata (cos&#39;è un evar?)
* Confusione dello schema tra le soluzioni (A4T)
* Molte altre cose meno ottimali

Inoltre, al momento non esiste alcuna libreria JavaScript che invia dati direttamente ad Adobe Experience Platform.

### Con Adobe Experience Platform Web SDK

Il nuovo SDK Web invia i dati per le seguenti soluzioni a un&#39;unica destinazione (AEP Edge Network) e risolve i casi di utilizzo della soluzione più comuni indicati sopra.

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* ID visitatore
* Adobe Experience Platform

Altre soluzioni seguiranno nel corso di quest&#39;anno.

Adobe Experience Platform Web SDK può anche inviare dati direttamente ad Adobe Experience Platform. Questi dati sono in XDM ed è mappato allo schema della soluzione lato server.

## Qual è il valore di questo nuovo SDK Web?

**Prestazioni:** L’SDK Web è più piccolo rispetto all’utilizzo di tutte le librerie di Adobi  correnti e offre caricamenti di pagina significativamente più veloci.

**Semplicità:** La combinazione di XDM, SDK Web, Launch, Experience Edge, soluzioni Adobe Experience Cloud e Adobe Experience Platform crea un racconto semplice e intuitivo sulla raccolta dei dati.

* **XDM:** Lo schema agnostico della soluzione utilizzato per inviare dati al Adobe . Non è più necessario aggiungere tag per le variabili evar o mbox.
* **SDK Web:** Semplifica l&#39;invio e la ricezione di dati ad Adobe Experience Platform Edge Network.
* **Avvia:** Semplifica la distribuzione e la configurazione dell’SDK Web (e di eventuali altri tag JavaScript) in un sito.
* **Experience Edge:** Distribuisci facilmente i dati ad Adobe Experience Platform e alle soluzioni nel formato richiesto.
* **Soluzioni Adobe Experience Platform e  Adobe:** Abilitare la relativa proposta di valore.

**Controllo:** Poiché tutti i dati utilizzano un singolo e collegato flusso di dati, è possibile seguire e controllare logicamente l&#39;aspetto dei dati ad ogni millisecondo del suo percorso, da e verso le applicazioni.

**Moderno e pronto per il futuro:** L’SDK Web e la sua connessione a Experience Edge Network hanno consentito  Adobe di modernizzare in modo significativo  Adobe la raccolta dei dati, la personalizzazione, il consenso e il futuro dei cookie di terze parti. Abilita un dominio di prime parti, gestito da  Adobe.

**Time-to-value:**  Adobe ha lavorato duramente (e continuerà) per semplificare il più possibile la distribuzione dell’SDK Web tramite Launch e la mappatura dei dati lato client su XDM.  Al termine del lavoro, tutte le altre soluzioni  Adobe e i servizi Adobe Experience Platform possono essere attivati o disattivati sul lato server. Ad esempio, se utilizzate questo per  Adobe Analytics e desiderate attivare Target o  Experience Platform, potete semplicemente attivare la configurazione Experience Edge e illuminare i casi di utilizzo.

## Che cosa è `alloy.js`?

`Alloy.js` è il nome del file per l’SDK Web di Adobe Experience Platform. Adobe Experience Platform Web SDK è il nome ufficiale, ma molti sviluppatori lo chiamano &quot;lega&quot;.

## I clienti devono acquistare Adobe Experience Platform per utilizzare l&#39;SDK Web?

No. Qualsiasi cliente &#39;esperienza digitale può utilizzarla. Totalmente libero. Tutti i clienti che desiderano utilizzare l’SDK Web avranno accesso alla creazione di schemi e set di dati nell’interfaccia utente di Adobe Experience Platform.

## Chi dovrebbe usare l’SDK Web?

Adobe Experience Platform Web SDK è stato sviluppato per le seguenti persone:

* Utenti Adobe Experience Platform

   Se devi inviare i dati direttamente da un dispositivo ad Adobe Experience Platform, questo è il modo ufficialmente consigliato.

    Adobe è consapevole del fatto che l&#39;utilizzo del connettore Adobe Analytics  è più rapido se il cliente ha già  Adobe Analytics, ma non è la strategia a lungo termine per la raccolta dei dati.

* Clienti delle soluzioni Adobe Experience Cloud

   I nuovi clienti  Adobe Analytics, Adobe Audience Manager e  Adobe Target dovrebbero iniziare con il nuovo SDK Web e non utilizzare librerie precedenti.

   I clienti esistenti che desiderano ottenere l’implementazione più ottimizzata possibile devono utilizzare il nuovo SDK Web.


## Come posso accedere per iniziare a utilizzare Adobe Experience Platform Web SDK?

L’SDK Web è attualmente disponibile al pubblico e può essere utilizzato per inviare dati ai prodotti Adobe Experience Cloud. La capacità di inviare dati a soluzioni di terze parti sta arrivando in un futuro prossimo. Se desiderate accedere all’SDK Web, contattate il vostro software manager certificato (CSM) per avviare il processo di richiesta.

## Quali casi di utilizzo sono attualmente supportati dall’SDK Web?

L&#39;SDK Web si sta evolvendo rapidamente. Sono in corso ulteriori lavori. L’ [elenco dei casi di utilizzo attualmente supportati è disponibile qui.](https://github.com/adobe/alloy/projects/5)

## I clienti attuali devono riassegnare i propri siti?

Dipende. Adobe Experience Platform Web SDK può essere distribuito in due stili diversi. Un documento di migrazione futuro fornirà ulteriori dettagli.

* **Un altro tag:** Se al sito sono già stati assegnati tag per soluzioni e non è possibile eseguire un nuovo tag, ma si desidera inviare i dati ad Adobe Experience Platform Edge Network per casi di utilizzo  Experience Platform o per le prossime funzioni lato server di Launch (vedi sotto), è possibile aggiungere il `alloy.js` tag al sito, dove funziona come &quot;un altro tag&quot;.

* **Il tag uno e solo:** Se desiderate utilizzare l&#39;SDK Web per una soluzione di Experience Cloud , dovete utilizzarlo per tutte le soluzioni presenti nella pagina. Ad esempio, se il sito dispone già di tag per Analytics e lo desiderate utilizzare per Target, dovete utilizzarlo sia per entrambi, sia per tutti gli altri siti in futuro.

In altre parole, se decidi di utilizzare l’SDK Web per Adobe Experience Platform per i casi di utilizzo non-soluzione, puoi assegnare un tag al sito `alloy.js` e continuare come se si trattasse di una nuova soluzione. Se desiderate utilizzarlo per  Adobe Analytics, Target o  Audience Manager, o per i casi di utilizzo di applicazioni, potrebbe essere necessario rimuovere uno qualsiasi dei codici legacy nella pagina.

## È possibile migrare gli ECID quando si inizia a utilizzare Alloy in modo che i visitatori del sito Web non inizino a presentarsi come nuovi visitatori?

Sì, Adobe Experience Platform Web SDK fornisce una funzione di migrazione delle identità. Seguite le istruzioni riportate in [questo documento](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/identity.html#id-migration) per ulteriori dettagli.

## In che modo l’SDK Web è diverso da  Adobe Experience Platform Launch?

* **Launch** è il gestore del codice del dispositivo. Utilizzatelo per distribuire il codice in modo più semplice. È libera e potente.

* **Adobe Experience Platform Web SDK** è il nome ufficiale del nuovo codice che verrà distribuito da Launch per  casi di utilizzo Adobi. È anche libero e potente.

* **`alloy.js`** è il nome file del codice Adobe Experience Platform Web SDK.

## Devo utilizzare  Adobe Experience Platform Launch per distribuire l&#39;SDK Web?

No. Potete scaricare il `alloy.js` file manualmente.

Tuttavia:

* Adobe Experience Platform Web SDK richiede un ID di configurazione Experience Edge che consente alla rete periferica di identificare il flusso e determinare le operazioni da eseguire con i dati. Questo ID viene creato in Launch. Ciò non significa che devi usare Launch per creare proprietà o distribuire il codice JavaScript, ma devi usare Launch per creare un ID di configurazione.

*  Adobe Experience Platform Launch non è solo il migliore gestore di tag e SDK disponibile, ma semplifica notevolmente la distribuzione `alloy.js` e la mappatura dei dati agli schemi XDM. Se decidi di non utilizzare Launch, devi gestire la distribuzione, l&#39;evento `alloy.js`e la mappatura dei dati in XDM prima di inviarli. Si tratta di un processo molto più difficile rispetto all&#39;utilizzo di Launch.

* È consigliabile utilizzare Launch per la distribuzione, anche se è l&#39;unico tag utilizzato per `alloy.js`la distribuzione.

## Cos&#39;è XDM ed è necessario utilizzare per l&#39;SDK Web?

XDM è il formato di dati utilizzato per inviare i dati all&#39;Adobe Experience Platform e all&#39;SDK Web. La documentazione [SDK per](https://docs.adobe.com/content/help/en/experience-platform/edge/get-started/quick-start-with-launch.html#prepare-a-schema) Web illustra come impostare facilmente uno schema che potrai quindi personalizzare in base alle tue esigenze specifiche.

## Cos&#39;è  lato server Adobe Experience Platform Launch?

Più tardi nel 2020, Launch rilascerà le funzioni di inoltro lato server. Se utilizzi i nostri SDK e invii XDM a Experience Edge, queste nuove funzionalità ti permetteranno di installare nuove estensioni lato server e mappare tali dati a qualsiasi cosa, e inviarli ovunque, dalla nostra rete Edge. Consideralo come &quot;raccolta di dati come servizio&quot;.  Questo sarà disponibile per un costo, oltre che per un bundle nell&#39;Adobe Experience Platform.

**Maggiori informazioni**[presentazione al Adobe](https://adobe.bluejeans.com/playback/s/9LhauPOnRSUTYg6RMHAw4oJekhYfOQgdBLlNekVJdWevYktpxqX2IYyl5fz2Wxh9)

## Cos’è un CNAME o un dominio di prime parti e perché è importante?

Ulteriori informazioni su un CNAME sono disponibili nella documentazione del [Adobe](https://docs.adobe.com/content/help/it-IT/id-service/using/reference/analytics-reference/cname.html)

## Dove è possibile ottenere ulteriori informazioni sull’SDK Web per Adobe Experience Platform?

* [Documentazione](https://docs.adobe.com/content/help/it-IT/experience-platform/edge/home.html)
* [Codice origine](https://github.com/adobe/alloy)
