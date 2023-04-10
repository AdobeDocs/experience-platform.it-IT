---
title: Domande frequenti su Adobe Experience Platform Web SDK
description: Risposte alle domande più frequenti sull'SDK Web di Adobe Experience Platform.
exl-id: 6ddb4b4d-c9b8-471a-bd2e-135dc4202876
source-git-commit: a8f6bb8c3e35f4c17812ef944440210b7fe3f87b
workflow-type: tm+mt
source-wordcount: '2104'
ht-degree: 2%

---

# Domande frequenti

Questa guida fornisce le risposte alle domande che vengono spesso poste in merito all’SDK per web di Adobe Experience Platform.

## Cos’è Adobe Experience Platform Web SDK?

Adobe Experience Platform Web SDK è una libreria JavaScript lato client che consente ai clienti di Adobe Experience Cloud di interagire con i vari servizi nell’Experience Cloud.

Invia i dati in modo non agnostico alla soluzione (XDM) ad Adobe Experience Platform Edge Network, che poi mappa i dati in formati e destinazioni specifici della soluzione e li invia in tempo reale.

**Ulteriori informazioni**
[Adobe Summit di presentazione](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html)

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

**Prestazioni:** L&#39;SDK per web è più piccolo dell&#39;utilizzo di tutte le librerie di Adobi correnti e fornisce caricamenti di pagina significativamente più veloci.

**Semplicità:** La combinazione di XDM, Web SDK, tag, Experience Edge, soluzioni Adobe Experience Cloud e Adobe Experience Platform crea una storia di raccolta dati semplice da comprendere e da seguire.

* **XDM:** Lo schema agnostico della soluzione utilizzato per inviare dati ad Adobe. Non è più possibile assegnare tag a eVar o mbox.
* **Adobe Experience Platform Web SDK:** Semplifica l’invio e la ricezione di dati su Adobe Experience Platform Edge Network.
* **Tag:** Semplifica la distribuzione e la configurazione dell’SDK web (e di altri tag JavaScript) su un sito.
* **Experience Edge:** Indirizza facilmente i dati a Adobe Experience Platform e alle soluzioni nel formato di cui hanno bisogno.
* **Soluzioni Adobe Experience Platform ed Adobe:** Abilita la loro proposta di valore.

**Controllo:** Poiché tutti i dati utilizzano un flusso di dati singolo e connesso, è possibile seguire e controllare logicamente l&#39;aspetto dei dati ad ogni millisecondo del percorso, da e verso le applicazioni.

**Moderno e pronto per il futuro:** L’SDK per web e la sua connessione a Experience Edge Network hanno consentito ad Adobe di modernizzare in modo significativo il modo in cui Adobe si occupa della raccolta dei dati, della personalizzazione, del consenso e del futuro dei cookie di terze parti. Abilita un dominio di prima parte, gestito da Adobe.

**Time-to-value:** Adobe ha lavorato duramente (e continuerà) per facilitare il più possibile la distribuzione dell’SDK web tramite tag e la mappatura dei dati lato client su XDM. Al termine del lavoro, tutte le altre soluzioni Adobe e i servizi Adobe Experience Platform possono essere attivati o disattivati sul lato server. Ad esempio, se utilizzi questo per Adobe Analytics e desideri attivare Target o Experience Platform, puoi semplicemente attivare la configurazione di Datastream e accendere questi casi d’uso.

## Cos&#39;è Alloy?

Alloy è il nome del codice per Adobe Experience Platform Web SDK. Viene utilizzato all&#39;interno del codice sorgente e del nome del file dell&#39;SDK, anche se Adobe Experience Platform Web SDK è il nome ufficiale.

## I clienti devono acquistare Adobe Experience Platform per utilizzare i [!DNL Web SDK]?

No. Qualsiasi cliente di Adobe Digital Experience può utilizzare gratuitamente Adobe Experience Platform Web SDK. Clienti che desiderano utilizzare il [!DNL Web SDK] dovrà configurare le autorizzazioni appropriate per creare schemi, set di dati, namespace di identità e flussi di dati nell’interfaccia utente di raccolta dati o Experience Platform.

Per ulteriori informazioni sulla configurazione di queste autorizzazioni, consulta la nostra documentazione su [gestione delle autorizzazioni di raccolta dati](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=en).

## Chi deve utilizzare l&#39;SDK per web?

Adobe Experience Platform Web SDK è stato sviluppato per le seguenti persone:

* Utenti Adobe Experience Platform
   * Se devi inviare dati direttamente da un dispositivo a Adobe Experience Platform, questo è il modo ufficialmente consigliato.
   * Adobe è consapevole del fatto che l’utilizzo del connettore Adobe Analytics è più veloce se il cliente dispone già di Adobe Analytics, ma non è la strategia a lungo termine per la raccolta dei dati.

* Clienti delle soluzioni Adobe Experience Cloud
   * I nuovi clienti Adobe Analytics, Adobe Audience Manager e Adobe Target devono iniziare con il nuovo SDK per web e non utilizzare le librerie legacy.
   * I clienti esistenti che desiderano ottenere l’implementazione più ottimizzata possibile devono utilizzare il nuovo SDK per web.


## Come posso ottenere l&#39;accesso per iniziare a utilizzare Adobe Experience Platform Web SDK?

L’SDK per web è attualmente disponibile al pubblico e può essere utilizzato per inviare dati ai prodotti Adobe Experience Cloud. La capacità di inviare dati a soluzioni di terze parti sta arrivando in un prossimo futuro. L’SDK è gratuito ed è ospitato gratuitamente da Adobe. Se necessario, puoi scaricarlo e ospitarlo sui tuoi server senza alcun costo. Platform Web SDK richiede l’accesso alle configurazioni di Datastream e al generatore di schemi Adobe Experience Platform XDM, affinché i server di Adobe possano gestire correttamente i dati in entrata provenienti dall’SDK. Se desideri ottenere l’accesso, contatta il team dell’account di Adobe per avviare il processo di richiesta.

## Quali casi d’uso sono attualmente supportati dall’SDK per web?

L&#39;SDK per web si sta evolvendo rapidamente. Si stanno lavorando ad altri casi d&#39;uso. È possibile trovare le [elenco dei casi d’uso attualmente supportati qui.](https://github.com/adobe/alloy/projects/5)

## I clienti attuali devono effettuare il retag sui propri siti?

Dipende. Adobe Experience Platform Web SDK può essere distribuito in due stili diversi. Un documento di migrazione futuro fornirà ulteriori dettagli.

* **Solo un altro tag:** Se il sito è già dotato di tag per le soluzioni e non è possibile eseguire il retag, ma si desidera inviare dati ad Adobe Experience Platform Edge Network per Experienci Platform di utilizzo o le prossime funzionalità di inoltro eventi (vedi di seguito), è possibile aggiungere il `alloy.js` al sito, dove funziona come &quot;un altro tag&quot;.

* **Il tag uno e unico:** Se desideri utilizzare l’SDK per web per una soluzione di Experience Cloud, devi utilizzarlo per _tutto_ delle soluzioni presenti in quella pagina. Ad esempio, se il tuo sito è già dotato di tag per Adobe Analytics e lo desideri utilizzare per Target, devi utilizzarlo sia per entrambi che per tutti gli altri in futuro.

In altre parole, se decidi di utilizzare Adobe Experience Platform Web SDK per casi di utilizzo non relativi alla soluzione, puoi assegnare al sito un tag `alloy.js` e proseguite come se si trattasse di una nuova soluzione. Se desideri utilizzarlo per Adobe Analytics, Target o Audience Manager o per casi di utilizzo di applicazioni, potrebbe essere necessario rimuovere uno qualsiasi dei codici legacy nella pagina.

## È possibile migrare gli ECID quando si inizia a utilizzare Alloy in modo che i visitatori del sito web non inizino a essere visualizzati come nuovi visitatori?

Sì, Adobe Experience Platform Web SDK fornisce una funzione di migrazione delle identità. Segui le istruzioni per la migrazione degli ID nella sezione [Documentazione di identità dell’SDK per web Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#id-migration) per ulteriori dettagli.

## In che modo l’SDK per web è diverso dai tag?

* **Experience Platform dei tag** gestire il codice del dispositivo. Utilizzali per distribuire più facilmente il codice. Sono liberi e potenti.

* **Adobe Experience Platform Web SDK** è il nome ufficiale del nuovo codice che verrebbe distribuito dai tag per Adobi di casi d’uso. È anche libero e potente.

* **`alloy.js`** è il nome file del codice Adobe Experience Platform Web SDK.

## Devo utilizzare dei tag per distribuire l&#39;SDK per web?

No. È possibile scaricare `alloy.js` registrati da solo.

Tuttavia:

* Adobe Experience Platform Web SDK richiede un ID Datastream, in modo che la rete perimetrale possa identificare il flusso e determinare cosa fare con i dati. Questo ID viene creato in Experience Platform. Questo non significa che devi utilizzare l&#39;interfaccia utente per creare le proprietà o distribuire il codice JavaScript, ma devi usare i tag per creare un ID di configurazione.

* I tag non sono solo i migliori tag disponibili e l’SDK manager, ma rendono molto semplice la distribuzione `alloy.js` e mappare i dati agli schemi XDM. Se decidi di non utilizzare i tag, dovrai gestire la distribuzione `alloy.js`, evento e mappatura dei dati in XDM prima di inviarli. Questa è una _molto_ processo più difficile rispetto all’utilizzo dei tag.

* Si consiglia di utilizzare i tag per distribuire `alloy.js`, anche se è l’unico tag utilizzato.

## Che cos’è l’inoltro eventi?

Se utilizzi i nostri SDK e invii XDM a Experience Edge, l’inoltro degli eventi per le nuove funzioni ti consente di installare nuove estensioni lato server e mappare tali dati a qualsiasi elemento, e inviarli ovunque, dalla nostra rete Edge. Immaginalo come &quot;raccolta dati come servizio&quot;. Questo sarà disponibile per un costo, oltre a essere incluso nel pacchetto come parte di Adobe Experience Platform.

## Cos’è un CNAME o un dominio di prima parte e perché è importante?

Ulteriori informazioni su un CNAME sono disponibili nella sezione [Documentazione di Adobe](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/cname.html)

## L’SDK web di Adobe Experience Platform utilizza i cookie? In caso affermativo, quali cookie utilizza?

Sì, attualmente l’SDK per web utilizza da uno a sette cookie a seconda dell’implementazione. Di seguito è riportato un elenco dei cookie che potresti visualizzare con l’SDK per web e del modo in cui vengono utilizzati:

| **Nome** | **maxAge** | **Età amichevole** | **Descrizione** |
|---|---|---|---|
| **kndct_orgid_identity** | 34128000 | 395 giorni | Il cookie identity memorizza l’ECID, nonché altre informazioni relative all’ECID. |
| **kndctr_orgid_permission_check** | 7200 | 2 ore | Questo cookie memorizza le preferenze di consenso dell&#39;utente per il sito web. |
| **kndctr_orgid_permission** | 15552000 | 180 giorni | Questo cookie basato su sessione segnala al server di cercare il lato server delle preferenze di consenso. |
| **kndctr_orgid_cluster** | 1800 | 30 minuti | Questo cookie memorizza l&#39;area Experience Edge che serve le richieste dell&#39;utente corrente. L’area viene utilizzata nel percorso URL in modo che Experience Edge possa indirizzare la richiesta all’area corretta. Questo cookie ha una durata di 30 minuti, quindi se un utente si connette con un indirizzo IP diverso, la richiesta può essere indirizzata all’area più vicina. |
| **mbox** | 63072000 | 2 anni | Questo cookie viene visualizzato quando l’impostazione di migrazione di Target è impostata su true. Questo consentirà a Target [cookie mbox](https://developer.adobe.com/target/implement/client-side/atjs/atjs-cookies/) da impostare dall’SDK per web. |
| **mboxEdgeCluster** | 1800 | 30 minuti | Questo cookie viene visualizzato quando l’impostazione di migrazione di Target è impostata su true. Questo cookie consente all’SDK web di comunicare il cluster Edge corretto a at.js in modo che i profili Target possano rimanere sincronizzati mentre gli utenti navigano in un sito. |
| **AMCV_###@AdobeOrg** | 34128000 | 395 giorni | Questo cookie viene visualizzato solo quando è abilitata la migrazione degli ID sull’SDK Web di Adobe Experience Platform. Questo cookie aiuta nella transizione all&#39;SDK web mentre alcune parti del sito utilizzano ancora visitor.js. Consulta la sezione [Documentazione idMigrationEnabled](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en#identity-options) per ulteriori informazioni su questa impostazione. |

Quando utilizzi l’SDK per web, la rete Edge imposta uno o più cookie di cui sopra. La rete Edge imposta tutti i cookie con `secure` e `sameSite="none"` attributi.

Se al momento disponi di sezioni sicure e non sicure sul tuo sito web, ciò potrebbe interferire con l&#39;identificazione dell&#39;utente. Quando un utente passa da una sezione protetta del sito a una sezione non protetta, la rete Edge genera un nuovo `ECID` con la richiesta.

## Quali browser supporta Adobe Experience Platform Web SDK?

Adobe Experience Platform Web SDK è progettato per funzionare in modo ottimale nelle versioni più recenti di Google Chrome, Safari, Firefox, Internet Explorer 11 e Microsoft Edge Chromium. È possibile che si verifichino problemi nell’utilizzo di alcune funzioni nelle versioni precedenti dei browser.

## Dove posso ottenere ulteriori informazioni sull’SDK web di Adobe Experience Platform?

* [Documentazione](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=it)
* [Codice sorgente](https://github.com/adobe/alloy)
