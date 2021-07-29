---
title: Domande frequenti su Adobe Experience Platform Web SDK
description: Risposte alle domande più frequenti sull'SDK Web di Adobe Experience Platform.
exl-id: 6ddb4b4d-c9b8-471a-bd2e-135dc4202876
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '1802'
ht-degree: 1%

---

# Domande frequenti

Questa guida fornisce le risposte alle domande che vengono spesso poste in merito all’SDK per web di Adobe Experience Platform.

## Cos’è Adobe Experience Platform Web SDK?

Adobe Experience Platform Web SDK è una libreria JavaScript lato client che consente ai clienti di Adobe Experience Cloud di interagire con i vari servizi nell’Experience Cloud.

Invia i dati in modo non agnostico alla soluzione (XDM) ad Adobe Experience Platform Edge Network, che poi mappa i dati in formati e destinazioni specifici della soluzione e li invia in tempo reale.

**Ulteriori**
[informazioniPresentazione di Adobe Summit](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html)

## Quali sono le differenze tra Adobe Experience Platform Web SDK e le soluzioni precedenti?

### Prima dell’SDK di Adobe Experience Platform

Attualmente, devi distribuire librerie JavaScript diverse in base a ogni singola soluzione.

* Ogni soluzione dispone di una libreria JavaScript, di uno schema e di un dominio propri.
* Nessuna di queste librerie è stata creata per funzionare tra loro.
* I casi di utilizzo tra soluzioni e Adobe Experience Platform richiedono l’interdipendenza di queste librerie diverse, causando problemi di distribuzione.

Anche se i tag in Platform semplificano il più possibile la distribuzione e la gestione di queste librerie, ci sono ancora problemi con:

* Dimensione libreria (codice troppo Adobe su una pagina)
* Prestazioni (il caricamento dei siti richiede troppo tempo)
* Chiamate multiple per un singolo caso d&#39;uso
* In attesa della restituzione di ECID prima delle chiamate di personalizzazione (causa il ritardo)
* Raccolta dati a frattura (cos’è un evar?)
* Confusione dello schema tra le soluzioni (A4T)
* Molte altre cose meno ottimali

Inoltre, attualmente non esiste alcuna libreria JavaScript che invia dati direttamente ad Adobe Experience Platform.

### Con Adobe Experience Platform Web SDK

Il nuovo SDK web invia i dati per le seguenti soluzioni a un’unica destinazione (Adobe Experience Platform Edge Network) e risolve i casi d’uso più comuni delle soluzioni sopra indicate.

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* ID visitatore
* Adobe Experience Platform

Altre soluzioni seguiranno nel corso dell&#39;anno.

Adobe Experience Platform Web SDK può anche inviare dati direttamente a Adobe Experience Platform. Questi dati sono in XDM e sono mappati sullo schema della soluzione lato server.

## Qual è il valore di questo nuovo SDK web?

**Prestazioni:** l&#39;SDK per web è più piccolo dell&#39;utilizzo di tutte le librerie di Adobe correnti e fornisce caricamenti di pagina significativamente più veloci.

**Semplicità:** la combinazione di XDM, SDK per web, tag, Experience Edge, soluzioni Adobe Experience Cloud e Adobe Experience Platform crea una storia di raccolta dati semplice da comprendere e da seguire.

* **XDM:** schema agnostico della soluzione utilizzato per inviare dati ad Adobe. Non è più possibile assegnare tag a eVar o mbox.
* **Adobe Experience Platform Web SDK:** consente di inviare e ricevere facilmente i dati in Adobe Experience Platform Edge Network.
* **Tag:** semplifica la distribuzione e la configurazione dell&#39;SDK web (e di altri tag JavaScript) su un sito.
* **Experience Edge:** indirizza facilmente i dati a Adobe Experience Platform e alle soluzioni nel formato di cui hanno bisogno.
* **Soluzioni Adobe Experience Platform ed Adobe:** abilita la loro proposta di valore.

**Controllo:** poiché tutti i dati utilizzano un flusso di dati singolo e connesso, puoi seguire e controllare logicamente l&#39;aspetto dei dati ad ogni millisecondo del percorso, da e verso le applicazioni.

**Moderno e pronto per il futuro:** l’SDK per web e la sua connessione a Experience Edge Network hanno consentito ad Adobe di modernizzare in modo significativo il modo in cui Adobe si occupa della raccolta, personalizzazione, consenso e il futuro dei cookie di terze parti. Abilita un dominio di prima parte, gestito da Adobe.

**Time-to-value:** Adobe ha lavorato duramente (e continuerà) per facilitare il più possibile la distribuzione dell’SDK web tramite tag e la mappatura dei dati lato client su XDM.  Al termine del lavoro, tutte le altre soluzioni Adobe e i servizi Adobe Experience Platform possono essere attivati o disattivati sul lato server. Ad esempio, se utilizzi questo per Adobe Analytics e desideri attivare Target o Experience Platform, puoi semplicemente attivare la configurazione di Datastream e accendere questi casi d’uso.

## Cos&#39;è Alloy?

Alloy è il nome del codice per Adobe Experience Platform Web SDK. Viene utilizzato all&#39;interno del codice sorgente e del nome del file dell&#39;SDK, anche se Adobe Experience Platform Web SDK è il nome ufficiale.

## I clienti devono acquistare Adobe Experience Platform per utilizzare l’SDK per web?

No. Qualsiasi cliente Digital Experience di Adobe può usarlo. Totalmente libero. Ai clienti che desiderano utilizzare l’SDK per web verrà concesso l’accesso per creare schemi e set di dati nell’interfaccia utente di Adobe Experience Platform.

## Chi deve utilizzare l&#39;SDK per web?

Adobe Experience Platform Web SDK è stato sviluppato per le seguenti persone:

* Utenti Adobe Experience Platform

   Se devi inviare dati direttamente da un dispositivo a Adobe Experience Platform, questo è il modo ufficialmente consigliato.

   Adobe è consapevole del fatto che l’utilizzo del connettore Adobe Analytics è più veloce se il cliente dispone già di Adobe Analytics, ma non è la strategia a lungo termine per la raccolta dei dati.

* Clienti delle soluzioni Adobe Experience Cloud

   I nuovi clienti Adobe Analytics, Adobe Audience Manager e Adobe Target devono iniziare con il nuovo SDK per web e non utilizzare le librerie legacy.

   I clienti esistenti che desiderano ottenere l’implementazione più ottimizzata possibile devono utilizzare il nuovo SDK per web.


## Come posso ottenere l&#39;accesso per iniziare a utilizzare Adobe Experience Platform Web SDK?

L’SDK per web è attualmente disponibile al pubblico e può essere utilizzato per inviare dati ai prodotti Adobe Experience Cloud. La capacità di inviare dati a soluzioni di terze parti sta arrivando in un prossimo futuro. L&#39;SDK è gratuito, è ospitato gratuitamente da Adobe e può essere scaricato in modo da poterlo ospitare gratuitamente sui tuoi server. Platform Web SDK richiede l’accesso alle configurazioni di Datastream e al generatore di schemi Adobe Experience Platform XDM, affinché i server di Adobe possano gestire correttamente i dati in entrata provenienti dall’SDK. Per accedere, contatta il tuo Customer Success Manager (CSM) per avviare il processo di richiesta.

## Quali casi d’uso sono attualmente supportati dall’SDK per web?

L&#39;SDK per web si sta evolvendo rapidamente. Si stanno lavorando ad altri casi d&#39;uso. È possibile trovare l&#39; [elenco dei casi d&#39;uso attualmente supportati qui.](https://github.com/adobe/alloy/projects/5)

## I clienti attuali devono effettuare il retag sui propri siti?

Dipende. Adobe Experience Platform Web SDK può essere distribuito in due stili diversi. Un documento di migrazione futuro fornirà ulteriori dettagli.

* **Solo un altro tag:** se il sito dispone già di tag per le soluzioni e non è possibile eseguire il retag, ma desideri inviare dati a Adobe Experience Platform Edge Network per Experienci Platform di utilizzo o alle prossime funzionalità di inoltro eventi (vedi sotto), puoi aggiungere il  `alloy.js` tag al sito, dove funziona come &quot;un altro tag&quot;.

* **Tag uno e solo:** se desideri utilizzare l&#39;SDK per web per una soluzione di Experience Cloud, devi utilizzarlo per  __ tutte le soluzioni presenti in quella pagina. Ad esempio, se il tuo sito è già dotato di tag per Adobe Analytics e lo desideri utilizzare per Target, devi utilizzarlo sia per entrambi che per tutti gli altri in futuro.

In altre parole, se decidi di utilizzare Adobe Experience Platform Web SDK per casi di utilizzo non relativi alla soluzione, puoi assegnare al sito i tag `alloy.js` e continuare come se si trattasse di una nuova soluzione. Se desideri utilizzarlo per Adobe Analytics, Target o Audience Manager o per casi di utilizzo di applicazioni, potrebbe essere necessario rimuovere uno qualsiasi dei codici legacy nella pagina.

## È possibile migrare gli ECID quando si inizia a utilizzare Alloy in modo che i visitatori del sito web non inizino a essere visualizzati come nuovi visitatori?

Sì, Adobe Experience Platform Web SDK fornisce una funzione di migrazione delle identità. Per ulteriori informazioni, segui le istruzioni per la migrazione degli ID nella [documentazione relativa all’identità dell’SDK per web della piattaforma](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#id-migration) .

## In che modo l’SDK per web è diverso dai tag?

* **I tag in Experience** Platform gestiscono il codice del dispositivo. Utilizzali per distribuire più facilmente il codice. Sono liberi e potenti.

* **Adobe Experience Platform Web** SDK è il nome ufficiale del nuovo codice che verrebbe distribuito dai tag, ad Adobe i casi di utilizzo. È anche libero e potente.

* **`alloy.js`** è il nome file del codice Adobe Experience Platform Web SDK.

## Devo utilizzare dei tag per distribuire l&#39;SDK per web?

No. Puoi scaricare il file `alloy.js` direttamente.

Tuttavia:

* Adobe Experience Platform Web SDK richiede un ID Datastream, in modo che la rete perimetrale possa identificare il flusso e determinare cosa fare con i dati. Questo ID viene creato in Experience Platform. Ciò non significa che devi utilizzare l’interfaccia utente di raccolta dati per creare proprietà o distribuire il codice JavaScript, ma che devi usare i tag per creare un ID di configurazione.

* I tag non sono solo il migliore gestore di tag e SDK disponibile, ma rendono molto semplice distribuire `alloy.js` e mappare i dati sugli schemi XDM. Se decidi di non utilizzare i tag, dovrai gestire la distribuzione `alloy.js`, l’evento e la mappatura dei dati in XDM prima di inviarli. Si tratta di un processo _molto_ più difficile che utilizzare i tag.

* Si consiglia di utilizzare i tag per distribuire `alloy.js`, anche se è l’unico tag a cui si utilizza.

## Che cos’è l’inoltro eventi?

Se utilizzi i nostri SDK e invii XDM a Experience Edge, l’inoltro degli eventi per le nuove funzioni ti consente di installare nuove estensioni lato server e mappare tali dati a qualsiasi elemento, e inviarli ovunque, dalla nostra rete Edge. Immaginalo come &quot;raccolta dati come servizio&quot;.  Questo sarà disponibile per un costo, oltre a essere incluso nel pacchetto come parte di Adobe Experience Platform.

## Cos’è un CNAME o un dominio di prima parte e perché è importante?

Ulteriori informazioni su un CNAME sono disponibili nella documentazione [Adobe](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/cname.html)

## L’SDK web di Adobe Experience Platform utilizza i cookie? In caso affermativo, quali cookie utilizza?

Sì, attualmente l&#39;SDK per web utilizza da 1 a 4 cookie a seconda dell&#39;implementazione. Di seguito è riportato un elenco dei 4 cookie che potresti vedere con l’SDK per web e del modo in cui vengono utilizzati:

**kndct_orgid_identity:** il cookie di identità viene utilizzato per memorizzare l’ECID, nonché altre informazioni relative all’ECID.

**kndctr_orgid_permission:** questo cookie memorizza le preferenze di consenso dell’utente per il sito web.

**kndctr_orgid_personalization:** questo cookie include informazioni sulla sessione utilizzate da Adobe Target per personalizzare le pagine web.

**kndctr_orgid_permission check:** questo cookie basato su sessione invia un segnale al server per cercare il lato server delle preferenze di consenso.

## Quali browser supporta Adobe Experience Platform Web SDK?

Adobe Experience Platform Web SDK è progettato per funzionare in modo ottimale nelle versioni più recenti di Google Chrome, Safari, Firefox, Internet Explorer 11 e Microsoft Edge Chromium. È possibile che si verifichino problemi durante l’utilizzo di alcune funzioni nelle versioni precedenti dei browser.

## Dove posso ottenere ulteriori informazioni sull’SDK web di Adobe Experience Platform?

* [Documentazione](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
* [Codice sorgente](https://github.com/adobe/alloy)
