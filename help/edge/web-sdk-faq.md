---
title: Domande frequenti su SDK Web
seo-title: Domande frequenti su Adobe Experience Platform Web SDK
description: Domande frequenti sull’SDK Adobe Experience Platform Web
seo-description: Domande frequenti sull’SDK Adobe Experience Platform Web
translation-type: tm+mt
source-git-commit: f4f0b00dfd324f69aa2b4348740f6e767e86a6de
workflow-type: tm+mt
source-wordcount: '1808'
ht-degree: 2%

---


# Domande frequenti 

Queste domande frequenti includono domande frequenti sull’SDK Web per Adobi .

## Cos&#39;è Adobe Experience Platform Web SDK?

Adobe Experience Platform Web SDK è una libreria JavaScript lato client che consente ai clienti di Adobe Experience Cloud di interagire con i vari servizi nell&#39;Experience Cloud di .

Invia i dati in modo non dipendente dalla soluzione (XDM) ad Adobe Experience Platform Edge Network, che poi mappa i dati in formati e destinazioni specifici della soluzione e li invia in tempo reale.

**Ulteriori**
[informazioniPresentazione di Adobe Summit](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html)

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

Il nuovo SDK Web invia i dati per le seguenti soluzioni a un&#39;unica destinazione (Adobe Experience Platform Edge Network) e risolve i casi di utilizzo più comuni delle soluzioni indicate sopra.

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* ID visitatore
* Adobe Experience Platform

Altre soluzioni seguiranno nel corso di quest&#39;anno.

Adobe Experience Platform Web SDK può anche inviare dati direttamente ad Adobe Experience Platform. Questi dati sono in XDM ed è mappato allo schema della soluzione lato server.

## Qual è il valore di questo nuovo SDK Web?

**Prestazioni:** l’SDK per Web è più piccolo rispetto all’utilizzo di tutte le librerie di Adobi  correnti e offre carichi di pagina significativamente più veloci.

**Semplicità:** la combinazione di XDM, SDK Web, Experience Platform Launch, soluzioni Experience Edge, Adobe Experience Cloud e Adobe Experience Platform crea un racconto di raccolta dati semplice e intuitivo.

* **XDM:** schema agnostico della soluzione utilizzato per inviare dati al Adobe . Non è più necessario aggiungere tag per le variabili evar o mbox.
* **Adobe Experience Platform Web SDK:** semplifica l&#39;invio e la ricezione di dati ad Adobe Experience Platform Edge Network.
* **Experience Platform Launch:** Semplifica la distribuzione e la configurazione dell&#39;SDK Web (e di altri tag JavaScript) in un sito.
* **Experience Edge:** indirizza facilmente i dati ad Adobe Experience Platform e alle soluzioni nel formato richiesto.
* **Soluzioni Adobe Experience Platform e  Adobe:** Abilita la loro proposta di valore.

**Controllo:** Poiché tutti i dati utilizzano un singolo e collegato flusso di dati, è possibile seguire e controllare logicamente l&#39;aspetto dei dati ogni millisecondo del percorso, da e verso le applicazioni.

**Moderna e pronta per il futuro:** L’SDK Web e la sua connessione a Experience Edge Network hanno consentito  Adobe di modernizzare in modo significativo  Adobe la raccolta dei dati, la personalizzazione, il consenso e il futuro dei cookie di terze parti. Abilita un dominio di prime parti, gestito da  Adobe.

**Time-to-value:**  Adobe ha lavorato duramente (e continuerà) per semplificare il più possibile la distribuzione dell’SDK Web tramite Experience Platform Launch e la mappatura dei dati lato client su XDM.  Al termine del lavoro, tutte le altre soluzioni  Adobe e i servizi Adobe Experience Platform possono essere attivati o disattivati sul lato server. Ad esempio, se utilizzate questo per  Adobe Analytics e desiderate attivare Target o  Experience Platform, potete semplicemente attivare la configurazione Experience Edge e illuminare i casi di utilizzo.

## Cos&#39;è Alloy?

Il nome del codice è già il nome dell’SDK Web per Adobe Experience Platform. Viene utilizzato nel codice sorgente e nel nome del file dell&#39;SDK, anche se Adobe Experience Platform Web SDK è il nome ufficiale.

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

L’SDK Web è attualmente disponibile al pubblico e può essere utilizzato per inviare dati ai prodotti Adobe Experience Cloud. La capacità di inviare dati a soluzioni di terze parti sta arrivando in un futuro prossimo. L’SDK è gratuito, è ospitato  Adobe gratuitamente e può essere scaricato in modo da poter ospitare l’SDK sui propri server, se lo desiderate, gratuitamente. L’SDK per Web della piattaforma richiede l’accesso alle configurazioni di Platform Edge Network e al generatore di schemi Adobe Experience Platform XDM, per consentire  server  di gestire correttamente i dati in entrata provenienti dall’SDK. Per accedere, contatta il tuo Customer Success Manager (CSM) per avviare il processo di richiesta.

## Quali casi di utilizzo sono attualmente supportati dall’SDK Web?

L&#39;SDK Web si sta evolvendo rapidamente. Sono in corso ulteriori lavori. È possibile trovare l&#39; [elenco dei casi di utilizzo attualmente supportati qui.](https://github.com/adobe/alloy/projects/5)

## I clienti attuali devono riassegnare i propri siti?

Dipende. Adobe Experience Platform Web SDK può essere distribuito in due stili diversi. Un documento di migrazione futuro fornirà ulteriori dettagli.

* **Solo un altro tag:** se il sito è già dotato di tag per soluzioni e non è possibile eseguire un nuovo tag, ma si desidera inviare dati ad Adobe Experience Platform Edge Network per casi di utilizzo di Experience Platform o per le prossime funzionalità lato server Experience Platform Launch (vedere di seguito), è possibile aggiungere il  `alloy.js` tag al sito, dove funziona come &quot;solo un altro tag&quot;.

* **L&#39;unico tag:** Se si desidera utilizzare l&#39;SDK Web per una soluzione di Experience Cloud , è necessario utilizzarlo per  __ tutte le soluzioni presenti nella pagina. Ad esempio, se al sito è già assegnato un tag per  Adobe Analytics e desiderate usarlo per Target, è necessario utilizzarlo sia per entrambi, sia per tutti gli altri siti in futuro.

In altre parole, se decidete di utilizzare Adobe Experience Platform Web SDK per i casi di utilizzo non-soluzione, potete assegnare al sito i tag `alloy.js` e continuare come se si trattasse di una nuova soluzione. Se desiderate utilizzarlo per  Adobe Analytics, Target o  Audience Manager, o per i casi di utilizzo di applicazioni, potrebbe essere necessario rimuovere uno qualsiasi dei codici legacy nella pagina.

## È possibile migrare gli ECID quando si inizia a utilizzare Alloy in modo che i visitatori del sito Web non inizino a presentarsi come nuovi visitatori?

Sì, Adobe Experience Platform Web SDK fornisce una funzione di migrazione delle identità. Segui le istruzioni per la migrazione degli ID nella [documentazione dell&#39;identità SDK Web della piattaforma](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#id-migration) per ulteriori dettagli.

## In che modo l’SDK Web è diverso da  Adobe Experience Platform Launch?

* **Experience Platform** Avvia il gestore del codice del dispositivo. Utilizzatelo per distribuire il codice in modo più semplice. È libera e potente.

* **Adobe Experience Platform Web** SDK è il nome ufficiale del nuovo codice che verrà distribuito dal Experience Platform Launch per  casi di utilizzo Adobe. È anche libero e potente.

* **`alloy.js`** è il nome file del codice Adobe Experience Platform Web SDK.

## Devo utilizzare  Adobe Experience Platform Launch per distribuire l&#39;SDK Web?

No. È possibile scaricare il file `alloy.js` personalmente.

Tuttavia:

* Adobe Experience Platform Web SDK richiede un ID di configurazione Experience Edge in modo che la rete periferica possa identificare il flusso e determinare cosa fare con i dati. Questo ID viene creato all&#39;interno del Experience Platform Launch. Ciò non significa che per creare le proprietà o distribuire il codice JavaScript è necessario utilizzare l&#39;Experience Platform Launch, ma è necessario utilizzare l&#39;Experience Platform Launch per creare un ID di configurazione.

*  Adobe Experience Platform Launch non è solo il migliore gestore di tag e SDK disponibile, ma semplifica notevolmente la distribuzione di `alloy.js` e la mappatura dei dati agli schemi XDM. Se decidi di non utilizzare l&#39;Experience Platform Launch, dovrai gestire la distribuzione `alloy.js`, l&#39;evento e la mappatura dei dati in XDM prima di inviarli. Si tratta di un processo _molto_ più difficile che utilizzare l&#39;Experience Platform Launch.

* È consigliabile utilizzare il Experience Platform Launch per distribuire `alloy.js`, anche se è l&#39;unico tag utilizzato.

## Cos&#39;è  lato server Adobe Experience Platform Launch?

Più tardi nel 2020, il Experience Platform Launch rilascerà le funzioni di inoltro lato server. Se utilizzi i nostri SDK e invii XDM a Experience Edge, queste nuove funzionalità ti permetteranno di installare nuove estensioni lato server e mappare tali dati a qualsiasi cosa, e inviarli ovunque, dalla nostra rete Edge. Consideralo come &quot;raccolta di dati come un servizio&quot;.  Questo sarà disponibile per un costo, oltre che per un bundle come parte di Adobe Experience Platform.

## Cos’è un CNAME o un dominio di prime parti e perché è importante?

Ulteriori informazioni su un CNAME sono disponibili nella [documentazione  Adobe](https://docs.adobe.com/content/help/it-IT/id-service/using/reference/analytics-reference/cname.html)

## Adobe Experience Platform Web SDK utilizza i cookie? In caso affermativo, quali cookie vengono utilizzati?

Sì, al momento l&#39;SDK Web utilizza da 1 a 4 cookie a seconda dell&#39;implementazione. Di seguito è riportato un elenco dei 4 cookie che potreste visualizzare con l’SDK Web e il modo in cui vengono utilizzati:

**kndct_orgid_identity:** Il cookie di identità viene utilizzato per memorizzare l’ECID, nonché altre informazioni relative all’ECID.

**kndctr_orgid_assenso:** Questo cookie memorizza le preferenze di consenso dell&#39;utente per il sito Web.

**kndctr_orgid_personalization:** Questo cookie include informazioni sulle sessioni che  Adobe Target utilizza per personalizzare le pagine Web.

**kndctr_orgid_consencheck:** Questo cookie basato su sessione segnala al server di cercare il lato server delle preferenze di consenso.

## Dove è possibile ottenere ulteriori informazioni sull’SDK Web per Adobe Experience Platform?

* [Documentazione](https://docs.adobe.com/content/help/it-IT/experience-platform/edge/home.html)
* [Codice origine](https://github.com/adobe/alloy)
