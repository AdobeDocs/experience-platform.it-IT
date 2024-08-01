---
title: Domande frequenti su Adobe Experience Platform Web SDK
description: Risposte alle domande frequenti su Adobe Experience Platform Web SDK.
exl-id: 6ddb4b4d-c9b8-471a-bd2e-135dc4202876
source-git-commit: cd2ac132c77d5d2e90c0f881d7b89a3c339fed6f
workflow-type: tm+mt
source-wordcount: '2184'
ht-degree: 2%

---


# Domande frequenti

Questa guida fornisce le risposte alle domande che vengono spesso poste in merito a Adobe Experience Platform Web SDK.

## Cos’è Adobe Experience Platform Web SDK?

Adobe Experience Platform Web SDK è una libreria JavaScript lato client che consente di interagire con i vari servizi di Adobe Experience Cloud.

Experienci Platform L’SDK per web invia i dati all’Edge Network in modo indipendente dalla soluzione (XDM), che quindi li mappa su formati e destinazioni specifici della soluzione e li invia in tempo reale.

Per ulteriori informazioni su Web SDK, guarda il seguente video: [Incontra Alloy.js e non assegnare mai più tag per un eVar o una Mbox](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html).

## Quali sono le differenze tra Adobe Experience Platform Web SDK e le soluzioni precedenti?

### Prima di Experience Platform Web SDK

Attualmente, è necessario implementare diverse librerie JavaScript in base a ogni singola soluzione.

* Ogni soluzione dispone di una libreria, uno schema e un dominio JavaScript propri.
* Nessuna di queste librerie è stata creata per funzionare tra loro.
* I casi di utilizzo tra soluzioni e Adobe Experience Platform richiedono che queste librerie diverse siano interdipendenti, causando attriti di distribuzione.

Anche se i tag in Platform semplificano la distribuzione e la gestione di queste librerie, esistono ancora problemi con:

* Dimensioni della libreria (troppo codice Adobe in una pagina)
* Prestazioni (il caricamento dei siti richiede troppo tempo)
* Più chiamate per un singolo caso d’uso
* In attesa del ritorno dell’ECID prima delle chiamate di personalizzazione (causa ritardo)
* Raccolta di dati frammentati (cos’è un’eVar?)
* Confusione di schemi tra soluzioni (A4T)
* Molte altre cose meno ottimali

Inoltre, attualmente non esiste una libreria JavaScript che invia i dati direttamente a Adobe Experience Platform.

### Con Experience Platform Web SDK

Il nuovo Web SDK invia i dati per le seguenti soluzioni a un’unica destinazione (Edge Network Experience Platform) e risolve i casi d’uso più comuni per le soluzioni di cui sopra.

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* ID visitatore
* Adobe Experience Platform

Seguiranno altre soluzioni.

Adobe Experience Platform Web SDK può anche inviare dati direttamente a Adobe Experience Platform. Questi dati sono in formato XDM e sono mappati allo schema della soluzione lato server.

## Qual è il valore di questo nuovo Web SDK?

**Prestazioni:** l&#39;SDK Web è più piccolo rispetto a tutte le librerie Adobe correnti e fornisce caricamenti di pagina notevolmente più veloci.

**Semplicità:** la combinazione di XDM, Web SDK, tag, Edge Network, soluzioni Adobe Experience Cloud e Adobe Experience Platform crea una raccolta dati semplice da comprendere e da seguire.

* **XDM:** lo schema indipendente dalla soluzione utilizzato per inviare dati ad Adobe. Non è più possibile assegnare tag a eVar o mbox.
* **Web SDK:** semplifica l&#39;invio e la ricezione di dati all&#39;Edge Network di Adobe Experience Platform.
* **Tag:** semplifica la distribuzione e la configurazione dell&#39;SDK Web (e di qualsiasi altro tag JavaScript) in un sito.
* **Edge Network:** indirizzare facilmente i dati a Adobe Experience Platform e alle soluzioni nel formato richiesto.
* **Soluzioni Adobe Experience Platform e Adobe:** Abilitare la proposta di valore.

**Controllo:** Poiché tutti i dati utilizzano un flusso di dati singolo e connesso, è possibile seguire e controllare in modo logico l&#39;aspetto dei dati ogni millisecondo del percorso, da e verso le applicazioni.

**Moderno e pronto per il futuro:** L&#39;SDK per web e la sua connessione all&#39;Edge Network hanno consentito all&#39;Adobe di modernizzare in modo significativo il modo in cui Adobe gestisce la raccolta dati, la personalizzazione, il consenso e il futuro dei cookie di terze parti. Abilita un dominio di prima parte, gestito da Adobe.

**Time-to-value:** L&#39;Adobe ha lavorato sodo (e continuerà) per semplificare al massimo la distribuzione di Web SDK tramite tag e la mappatura dei dati lato client in XDM. Al termine di questo lavoro, tutte le altre soluzioni di Adobe e i servizi Adobe Experience Platform possono essere attivati o disattivati sul lato server. Ad esempio, se utilizzi questo per Adobe Analytics e desideri attivare Target o Experience Platform, puoi semplicemente attivare la configurazione Datastream e illuminare questi casi d’uso.

## Cos’è [!DNL alloy.js]?

[!DNL alloy.js] è il nome della libreria JavaScript dell&#39;SDK Web. Vi si fa riferimento nel codice sorgente e nel nome file dell’SDK.

## I clienti devono acquistare Adobe Experience Platform per utilizzare [!DNL Web SDK]?

No. Qualsiasi cliente di esperienza digitale Adobe può utilizzare gratuitamente Adobe Experience Platform Web SDK. I clienti che desiderano utilizzare [!DNL Web SDK] dovranno configurare le autorizzazioni appropriate per la creazione di schemi, set di dati, spazi dei nomi delle identità e flussi di dati nell&#39;interfaccia utente di Data Collection o Experience Platform.

Per ulteriori informazioni sulla configurazione di queste autorizzazioni, consulta la documentazione sulla [gestione delle autorizzazioni per la raccolta dati](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html).

## Chi deve utilizzare l’SDK per web?

Adobe Experience Platform Web SDK è stato sviluppato per i seguenti clienti:

* Utenti Adobe Experience Platform
   * Se devi inviare i dati direttamente da un dispositivo a Adobe Experience Platform, questo è il metodo ufficialmente consigliato.
   * Adobe è consapevole del fatto che l’utilizzo del connettore Adobe Analytics è più veloce se si dispone già di Adobe Analytics, ma non rappresenta la strategia a lungo termine per la raccolta dei dati.

* Clienti delle soluzioni Adobe Experience Cloud
   * I nuovi clienti di Adobe Analytics, Adobe Audience Manager e Adobe Target devono iniziare con il nuovo Web SDK e non utilizzare le librerie legacy.
   * I clienti esistenti che desiderano ottenere l’implementazione più ottimizzata possibile devono utilizzare il nuovo Web SDK.

## Come posso accedere a Web SDK?

L’SDK per web è attualmente disponibile al pubblico e può essere utilizzato per inviare dati ai prodotti Adobe Experience Cloud. La capacità di inviare dati a soluzioni di terze parti sarà presto disponibile.

L’SDK è gratuito ed è ospitato gratuitamente da Adobe. Se necessario, è possibile scaricarlo e ospitarlo sui propri server senza alcun costo.

Web SDK richiede l&#39;accesso a [configurazioni dello stream di dati](../datastreams/overview.md) e al generatore di schemi [XDM](../xdm/tutorials/create-schema-ui.md) di Experience Platform per consentire ai server Adobe di gestire correttamente i dati in entrata provenienti dall&#39;SDK. Se desideri ottenere l’accesso, contatta il team del tuo account di Adobe per avviare la procedura di richiesta.

## Quali casi di utilizzo sono attualmente supportati dall’SDK per web?

L’SDK per web si sta evolvendo rapidamente. Si stanno elaborando altri casi d’uso. Puoi trovare l&#39;[elenco dei casi d&#39;uso attualmente supportati qui.](https://github.com/orgs/adobe/projects/18/views/1?filterQuery=)

## I clienti attuali devono rinominare i tag dei loro siti?

Dipende. Adobe Experience Platform Web SDK può essere distribuito in due stili diversi. Un futuro documento di migrazione fornirà ulteriori dettagli.

* **Solo un altro tag:** Se il sito è già contrassegnato per le soluzioni e non è possibile riassegnare il tag, ma si desidera inviare i dati ad Edge Network di Adobe Experience Platform per Experienci Platform casi d&#39;uso o le prossime funzionalità di inoltro degli eventi (vedere di seguito), è possibile aggiungere il tag `alloy.js` al sito, dove funziona come &quot;solo un altro tag&quot;.

* **L&#39;unico e unico tag:** Se desideri utilizzare Web SDK per una soluzione di Experience Cloud, devi utilizzarlo per _tutte_ le soluzioni in quella pagina. Ad esempio, se il tuo sito è già taggato per Adobe Analytics e desideri utilizzarlo per Target, devi utilizzarlo per entrambi, così come per qualsiasi altro in futuro.

In altre parole, se decidi di utilizzare Adobe Experience Platform Web SDK per casi di utilizzo non correlati alla soluzione, puoi assegnare al sito i tag `alloy.js` e continuare come se si trattasse di una nuova soluzione. Se desideri utilizzarlo per Adobe Analytics, Target o Audience Manager o per i casi di utilizzo dell’applicazione, potrebbe essere necessario rimuovere uno qualsiasi dei codici legacy dalla pagina.

## Posso eseguire la migrazione degli ECID quando inizio a utilizzare Web SDK in modo che i visitatori del mio sito web non inizino a essere visualizzati come nuovi visitatori?

Sì, Adobe Experience Platform Web SDK fornisce una funzione di migrazione delle identità. Segui le istruzioni per la migrazione degli ID nella [documentazione di Platform Web SDK Identity](/help/web-sdk/identity/overview.md#id-migration) per ulteriori dettagli.

## Quali sono le differenze tra Web SDK e i tag?

* **I tag nell&#39;Experience Platform** gestiscono il codice del dispositivo. Utilizzali per distribuire più facilmente il codice. Sono liberi e potenti.

* **Adobe Experience Platform Web SDK** è il nome ufficiale del nuovo codice che verrebbe distribuito dai tag, ad Adobe nei casi di utilizzo. È anche libero e potente.

* **`alloy.js`** è il nome file del codice Adobe Experience Platform Web SDK.

## Devo utilizzare i tag per distribuire l’SDK web?

No. È possibile scaricare il file `alloy.js` autonomamente.

Tuttavia:

* Adobe Experience Platform Web SDK richiede un ID Datastream che consenta alla rete Edge di identificare il flusso e determinare cosa fare con i dati. Questo ID viene creato in Experience Platform. Ciò non significa che devi utilizzare l’interfaccia utente per creare le proprietà o distribuire il codice JavaScript, ma che devi utilizzare i tag per creare un ID di configurazione.

* I tag non sono solo i migliori gestori di tag e SDK disponibili, ma semplificano notevolmente la distribuzione di `alloy.js` e la mappatura dei dati negli schemi XDM. Se decidi di non utilizzare i tag, dovrai gestire la distribuzione di `alloy.js`, la creazione di eventi e la mappatura dei dati in XDM prima di inviarli. Si tratta di un processo _molto_ più difficile rispetto all&#39;utilizzo dei tag.

* È consigliabile utilizzare i tag per distribuire `alloy.js`, anche se è l&#39;unico tag utilizzato per.

## Cos’è l’inoltro di eventi?

Se utilizzi i nostri SDK e invii XDM all’Edge Network, l’inoltro di eventi per queste nuove funzioni consente di installare nuove estensioni lato server e mappare tali dati su qualsiasi cosa, e inviarli ovunque, dalla nostra rete Edge. Considerala come una &quot;raccolta dati come servizio&quot;. Il pacchetto sarà disponibile a pagamento, oltre ad essere incluso in Adobe Experience Platform.

## Cos’è un dominio CNAME o di prima parte e perché è importante?

Ulteriori informazioni su un CNAME sono disponibili nella [documentazione di Adobe](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/cname.html)

## Adobe Experience Platform Web SDK utilizza i cookie? In caso affermativo, quali cookie utilizza?

Sì, attualmente l’SDK web utilizza un numero di cookie compreso tra uno e sette, a seconda dell’implementazione. Di seguito è riportato un elenco dei cookie che è possibile visualizzare con Web SDK e del modo in cui vengono utilizzati:

| **Nome** | **maxAge** | **Età descrittiva** | **Descrizione** |
|---|---|---|---|
| **kndct_orgid_identity** | 34128000 | 395 giorni | Il cookie di identità memorizza l’ECID, nonché altre informazioni relative all’ECID. |
| **kndctr_orgid_consent_check** | 7200 | 2 ore | Questo cookie basato su sessione segnala al server di cercare le preferenze di consenso lato server. |
| **kndctr_orgid_consent** | 15552000 | 180 giorni | Questo cookie memorizza le preferenze di consenso dell’utente per il sito web. |
| **kndctr_orgid_cluster** | 1800 | 30 minuti | Questo cookie memorizza l’area dell’Edge Network che soddisfa le richieste dell’utente corrente. L’area viene utilizzata nel percorso URL in modo che l’Edge Network possa indirizzare la richiesta all’area corretta. Questo cookie ha una durata di 30 minuti, pertanto se un utente si connette con un indirizzo IP diverso, la richiesta può essere indirizzata all’area più vicina. |
| **mbox** | 63072000 | 2 anni | Questo cookie viene visualizzato quando l’impostazione di migrazione di Target è impostata su true. Questo consentirà al cookie [mbox](https://developer.adobe.com/target/implement/client-side/atjs/atjs-cookies/) di Target di essere impostato dall&#39;SDK Web. |
| **mboxEdgeCluster** | 1800 | 30 minuti | Questo cookie viene visualizzato quando l’impostazione di migrazione di Target è impostata su true. Questo cookie consente a Web SDK di comunicare il cluster Edge corretto a at.js in modo che i profili di Target possano rimanere sincronizzati mentre gli utenti si spostano all&#39;interno di un sito. |
| **AMCV_###@AdobeOrg** | 34128000 | 395 giorni | Questo cookie viene visualizzato solo quando è abilitata la migrazione degli ID su Adobe Experience Platform Web SDK. Questo cookie è utile per la transizione a Web SDK quando alcune parti del sito utilizzano ancora visitor.js. Per ulteriori informazioni, vedere [`idMigrationEnabled`](/help/web-sdk/commands/configure/idmigrationenabled.md). |

Quando si utilizza l’SDK per web, l’Edge Network imposta uno o più cookie qui sopra. L&#39;Edge Network imposta tutti i cookie con gli attributi `secure` e `sameSite="none"`.

Se al momento sul sito web sono presenti sezioni protette e non protette, ciò potrebbe interferire con l’identificazione dell’utente. Quando un utente passa da una sezione protetta del sito a una sezione non protetta, l&#39;Edge Network genera un nuovo `ECID` con la richiesta.

## Quali browser supporta Adobe Experience Platform Web SDK?

Adobe Experience Platform Web SDK è progettato per funzionare in modo ottimale nelle versioni più recenti di Google Chrome, Safari, Firefox, Internet Explorer 11 e Microsoft Edge Chromium. Potresti riscontrare problemi nell’utilizzo di alcune funzioni nelle versioni precedenti dei browser.

## Dove è possibile ottenere ulteriori informazioni su Adobe Experience Platform Web SDK?

* [Documentazione](/help/web-sdk/home.md)
* [Codice Source](https://github.com/adobe/alloy)

### Supporto di Internet Explorer {#support-internet-explore}

Questo SDK utilizza le promesse, un metodo per comunicare il completamento di attività asincrone. L&#39;implementazione [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) utilizzata dall&#39;SDK è supportata in modo nativo da tutti i browser di destinazione eccetto [!DNL Internet Explorer]. Per usare l&#39;SDK su [!DNL Internet Explorer], devi avere `window.Promise` [polyfilled](https://remysharp.com/2010/10/08/what-is-a-polyfill).

Per determinare se si dispone già di `window.Promise` polyfill:

1. Apri il tuo sito Web in [!DNL Internet Explorer].
1. Apri la console di debug del browser.
1. Digitare `window.Promise` nella console, quindi premere Invio.

Se viene visualizzato qualcosa di diverso da `undefined`, è probabile che `window.Promise` sia già stato polilemizzato. Un altro modo per determinare se `window.Promise` è polyfill consiste nel caricare il sito Web dopo aver completato le istruzioni di installazione di cui sopra. Se l&#39;SDK genera un errore durante il riferimento a qualcosa su una promessa, è probabile che non sia stato eseguito il polyfill di `window.Promise`.

Se hai stabilito che devi eseguire il polyfill di `window.Promise`, includi il seguente tag di script sopra il codice di base fornito in precedenza:

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

Questo tag carica uno script che garantisce che `window.Promise` sia un&#39;implementazione Promise valida.

>[!NOTE]
>
>Se scegli di caricare un&#39;implementazione Promise diversa, assicurati che supporti `Promise.prototype.finally`.