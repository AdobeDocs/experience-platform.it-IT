---
title: Domande frequenti su Adobe Experience Platform Web SDK
description: Risposte alle domande frequenti su Adobe Experience Platform Web SDK.
exl-id: 6ddb4b4d-c9b8-471a-bd2e-135dc4202876
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '1999'
ht-degree: 2%

---

# Domande frequenti

Questa guida fornisce le risposte alle domande che vengono spesso poste in merito a Adobe Experience Platform Web SDK.

## Quali sono le differenze tra Adobe Experience Platform Web SDK e le soluzioni precedenti?

### Prima di Experience Platform Web SDK

Attualmente, è necessario implementare diverse librerie JavaScript in base a ogni singola soluzione.

* Ogni soluzione dispone di una libreria, uno schema e un dominio JavaScript propri.
* Nessuna di queste librerie è stata creata per funzionare tra loro.
* I casi di utilizzo tra soluzioni e Adobe Experience Platform richiedono che queste librerie diverse siano interdipendenti, causando attriti di distribuzione.

Anche se i tag in Experience Platform rendono più semplice la distribuzione e la gestione di queste librerie, esistono ancora problemi con:

* Dimensioni della libreria (troppo codice Adobe in una pagina)
* Prestazioni (il caricamento dei siti richiede troppo tempo)
* Più chiamate per un singolo caso d’uso
* In attesa del ritorno dell’ECID prima delle chiamate di personalizzazione (causa ritardo)
* Raccolta di dati frammentati (cos’è un’eVar?)
* Confusione di schemi tra soluzioni (A4T)
* Molte altre cose meno ottimali

Inoltre, attualmente non esiste una libreria JavaScript che invia i dati direttamente a Adobe Experience Platform.

### Con Experience Platform Web SDK

Il nuovo SDK web invia i dati per le seguenti soluzioni a un’unica destinazione (Experience Platform Edge Network) e risolve i casi d’uso più comuni per le soluzioni di cui sopra.

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* ID visitatore
* Adobe Experience Platform

Seguiranno altre soluzioni.

Adobe Experience Platform Web SDK può anche inviare dati direttamente a Adobe Experience Platform. Questi dati sono in formato XDM e sono mappati allo schema della soluzione lato server.

## Qual è il valore di questo nuovo Web SDK?

**Prestazioni:** il SDK Web è più piccolo rispetto a tutte le librerie Adobe correnti e fornisce caricamenti di pagina notevolmente più veloci.

**Semplicità:** La combinazione di XDM, Web SDK, tag, Edge Network, soluzioni Adobe Experience Cloud e Adobe Experience Platform crea una raccolta dati semplice da comprendere e da seguire.

* **XDM:** lo schema indipendente dalla soluzione utilizzato per inviare dati ad Adobe. Non è più possibile assegnare tag a eVar o mbox.
* **Web SDK:** semplifica l&#39;invio e la ricezione di dati a Adobe Experience Platform Edge Network.
* **Tag:** semplifica la distribuzione e la configurazione del Web SDK (e di qualsiasi altro tag JavaScript) in un sito.
* **Edge Network:** Indirizza facilmente i dati a Adobe Experience Platform e alle soluzioni nel formato richiesto.
* **Soluzioni Adobe Experience Platform e Adobe:** Abilitare la proposta di valore.

**Controllo:** Poiché tutti i dati utilizzano un flusso di dati singolo e connesso, è possibile seguire e controllare in modo logico l&#39;aspetto dei dati ogni millisecondo del percorso, da e verso le applicazioni.

**Moderno e pronto per il futuro:** Il Web SDK e la sua connessione ad Edge Network hanno consentito ad Adobe di modernizzare in modo significativo il modo in cui Adobe gestisce la raccolta dati, la personalizzazione, il consenso e il futuro dei cookie di terze parti. Abilita un dominio di prima parte, gestito da Adobe.

**Time-to-value:** Adobe ha lavorato sodo (e continuerà) per semplificare al massimo la distribuzione del Web SDK tramite tag e la mappatura dei dati lato client su XDM. Al termine di questo lavoro, tutte le altre soluzioni Adobe e i servizi Adobe Experience Platform possono essere attivati o disattivati lato server. Ad esempio, se utilizzi questo per Adobe Analytics e desideri attivare Target o Experience Platform, puoi semplicemente attivare la configurazione Datastream e illuminare questi casi d’uso.

## Cos’è [!DNL alloy.js]?

[!DNL alloy.js] è il nome della libreria Web SDK JavaScript. Viene fatto riferimento a esso nel codice sorgente e nel nome file di SDK.

## I clienti devono acquistare Adobe Experience Platform per utilizzare [!DNL Web SDK]?

No. Qualsiasi cliente di Adobe Digital Experience può utilizzare gratuitamente Adobe Experience Platform Web SDK.

* I clienti che *non* hanno accesso ad Experience Platform o Real-time CDP e desiderano utilizzare [!DNL Web SDK] dovranno configurare le autorizzazioni appropriate per la creazione di schemi e flussi di dati nell&#39;interfaccia utente di Data Collection o nell&#39;interfaccia utente di Experience Platform.
* I clienti che hanno accesso ad Experience Platform o Real-time CDP e desiderano utilizzare [!DNL Web SDK] dovranno configurare le autorizzazioni appropriate per la creazione di schemi, set di dati, spazi dei nomi delle identità e flussi di dati nell&#39;interfaccia utente di Data Collection o nell&#39;interfaccia utente di Experience Platform.

Per ulteriori informazioni sulla configurazione di queste autorizzazioni, consulta la documentazione sulla [gestione delle autorizzazioni per la raccolta dati](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html).

## Chi deve utilizzare il Web SDK?

Adobe Experience Platform Web SDK è stato sviluppato per i seguenti clienti:

* Utenti Adobe Experience Platform
   * Se devi inviare i dati direttamente da un dispositivo a Adobe Experience Platform, questo è il metodo ufficialmente consigliato.
   * Adobe sa che l’utilizzo del connettore Adobe Analytics è più veloce se si dispone già di Adobe Analytics, ma non rappresenta la strategia a lungo termine per la raccolta dei dati.

* Clienti delle soluzioni Adobe Experience Cloud
   * I nuovi clienti di Adobe Analytics, Adobe Audience Manager e Adobe Target devono iniziare con il nuovo Web SDK e non utilizzare le librerie legacy.
   * I clienti esistenti che desiderano ottenere l’implementazione più ottimizzata possibile devono utilizzare il nuovo Web SDK.

## Come si accede al Web SDK?

Il Web SDK è attualmente disponibile al pubblico e può essere utilizzato per inviare dati ai prodotti Adobe Experience Cloud. La capacità di inviare dati a soluzioni di terze parti sarà presto disponibile.

SDK è gratuito ed è ospitato gratuitamente da Adobe. Se necessario, è possibile scaricarlo e ospitarlo sui propri server senza alcun costo.

Il Web SDK richiede l&#39;accesso a [configurazioni dello stream di dati](/help/datastreams/overview.md) e al generatore di schemi XDM di Experience Platform [&#128279;](/help/xdm/tutorials/create-schema-ui.md) per consentire ai server Adobe di gestire correttamente i dati in entrata provenienti da SDK. Se desideri ottenere l’accesso, contatta il team del tuo account Adobe per avviare il processo di richiesta.

## Quali casi d’uso sono attualmente supportati dal Web SDK?

Il Web SDK si sta evolvendo rapidamente. Si stanno elaborando altri casi d’uso. Puoi trovare l&#39;[elenco dei casi d&#39;uso attualmente supportati qui.](https://github.com/orgs/adobe/projects/18/views/1?filterQuery=)

## I clienti attuali devono rinominare i tag dei loro siti?

Dipende. Adobe Experience Platform Web SDK può essere distribuito in due stili diversi. Un futuro documento di migrazione fornirà ulteriori dettagli.

* **Solo un altro tag:** Se il sito è già contrassegnato per le soluzioni e non è possibile riassegnare il tag, ma si desidera inviare i dati a Adobe Experience Platform Edge Network per i casi d&#39;uso di Experience Platform o per le prossime funzionalità di inoltro degli eventi (vedere di seguito), è possibile aggiungere il tag `alloy.js` al sito, dove funziona come &quot;solo un altro tag&quot;.

* **L&#39;unico e unico tag:** Se si desidera utilizzare il Web SDK per una soluzione Experience Cloud, è necessario utilizzarlo per _tutte_ le soluzioni della pagina. Ad esempio, se il tuo sito è già taggato per Adobe Analytics e desideri utilizzarlo per Target, devi utilizzarlo per entrambi, così come per qualsiasi altro in futuro.

In altre parole, se si decide di utilizzare Adobe Experience Platform Web SDK per casi di utilizzo non correlati alla soluzione, è possibile assegnare al sito il tag `alloy.js` e continuare come se si trattasse di una nuova soluzione. Se desideri utilizzarlo per Adobe Analytics, Target o Audience Manager o per i casi di utilizzo dell’applicazione, potrebbe essere necessario rimuovere uno qualsiasi dei codici legacy dalla pagina.

## È possibile eseguire la migrazione degli ECID quando si inizia a utilizzare Web SDK in modo che i visitatori del sito Web non vengano visualizzati come nuovi visitatori?

Sì, Adobe Experience Platform Web SDK fornisce una funzione di migrazione delle identità. Segui le istruzioni per la migrazione degli ID nella [documentazione di Experience Platform Web SDK Identity](/help/collection/use-cases/identity/id-overview.md#migrating-visitor-api-ecid) per ulteriori dettagli.

## Quali sono le differenze tra il Web SDK e i tag?

* **I tag in Experience Platform** gestiscono il codice del dispositivo. Utilizzali per distribuire più facilmente il codice. Sono liberi e potenti.

* **Adobe Experience Platform Web SDK** è il nome ufficiale del nuovo codice che verrebbe distribuito dai tag per i casi di utilizzo di Adobe. È anche libero e potente.

* **`alloy.js`** è il nome file del codice Adobe Experience Platform Web SDK.

## È necessario utilizzare i tag per distribuire il Web SDK?

No. È possibile scaricare il file `alloy.js` autonomamente.

Tuttavia:

* Adobe Experience Platform Web SDK richiede un ID Datastream che consenta alla rete Edge di identificare il flusso e determinare cosa fare con i dati. Questo ID viene creato in Experience Platform. Ciò non significa che devi utilizzare l’interfaccia utente per creare le proprietà o distribuire il codice JavaScript, ma che devi utilizzare i tag per creare un ID di configurazione.

* I tag non sono solo i migliori tag disponibili e SDK Manager, ma semplificano notevolmente la distribuzione di `alloy.js` e la mappatura dei dati negli schemi XDM. Se decidi di non utilizzare i tag, dovrai gestire la distribuzione di `alloy.js`, la creazione di eventi e la mappatura dei dati in XDM prima di inviarli. Si tratta di un processo _molto_ più difficile rispetto all&#39;utilizzo dei tag.

* È consigliabile utilizzare i tag per distribuire `alloy.js`, anche se è l&#39;unico tag utilizzato per.

## Cos’è l’inoltro di eventi?

Se utilizzi i nostri SDK e invii XDM ad Edge Network, l’inoltro di eventi per queste nuove funzioni consente di installare nuove estensioni lato server e mappare tali dati su qualsiasi cosa dalla nostra rete Edge di e inviarli ovunque. Considerala come una &quot;raccolta dati come servizio&quot;. Il pacchetto sarà disponibile a pagamento, oltre ad essere incluso in Adobe Experience Platform.

## Cos’è un dominio CNAME o di prima parte e perché è importante?

Ulteriori informazioni su un CNAME sono disponibili nella [documentazione di Adobe](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/cname.html)

## Adobe Experience Platform Web SDK utilizza i cookie? In caso affermativo, quali cookie utilizza?

Sì, attualmente il Web SDK utilizza da uno a sette cookie, a seconda dell’implementazione. Di seguito è riportato un elenco dei cookie che è possibile visualizzare con il Web SDK e il modo in cui vengono utilizzati:

| **Nome** | **maxAge** | **Età descrittiva** | **Descrizione** |
|---|---|---|---|
| **kndct_orgid_identity** | 34128000 | 395 giorni | Il cookie di identità memorizza l’ECID, nonché altre informazioni relative all’ECID. |
| **kndctr_orgid_consent_check** | 7200 | 2 ore | Questo cookie basato su sessione segnala al server di cercare le preferenze di consenso lato server. |
| **kndctr_orgid_consent** | 15552000 | 180 giorni | Questo cookie memorizza le preferenze di consenso dell’utente per il sito web. |
| **kndctr_orgid_cluster** | 1800 | 30 minuti | Questo cookie memorizza l’area Edge Network che soddisfa le richieste dell’utente corrente. L’area viene utilizzata nel percorso URL in modo che Edge Network possa indirizzare la richiesta all’area corretta. Questo cookie ha una durata di 30 minuti, pertanto se un utente si connette con un indirizzo IP diverso, la richiesta può essere indirizzata all’area più vicina. |
| **mbox** | 63072000 | 2 anni | Questo cookie viene visualizzato quando l’impostazione di migrazione di Target è impostata su true. In questo modo il cookie [mbox](https://developer.adobe.com/target/implement/client-side/atjs/atjs-cookies/) di destinazione potrà essere impostato dal Web SDK. |
| **mboxEdgeCluster** | 1800 | 30 minuti | Questo cookie viene visualizzato quando l’impostazione di migrazione di Target è impostata su true. Questo cookie consente al Web SDK di comunicare il cluster Edge corretto a at.js in modo che i profili di Target possano rimanere sincronizzati mentre gli utenti si spostano all’interno di un sito. |
| **AMCV_###@AdobeOrg** | 34128000 | 395 giorni | Questo cookie viene visualizzato solo quando è abilitata la migrazione degli ID sul Web SDK di Adobe Experience Platform. Questo cookie è utile per la transizione al Web SDK quando alcune parti del sito utilizzano ancora visitor.js. Per ulteriori informazioni, vedere [`idMigrationEnabled`](/help/collection/js/commands/configure/idmigrationenabled.md). |

Quando si utilizza il Web SDK, Edge Network imposta uno o più cookie indicati sopra. Edge Network imposta tutti i cookie con gli attributi `secure` e `sameSite="none"`.

Se al momento sul sito web sono presenti sezioni protette e non protette, ciò potrebbe interferire con l’identificazione dell’utente. Quando un utente passa da una sezione protetta del sito a una non protetta, Edge Network genera un nuovo `ECID` con la richiesta.

## Quali browser sono supportati da Adobe Experience Platform Web SDK?

Adobe Experience Platform Web SDK è progettato per funzionare in modo ottimale nelle versioni più recenti di Google Chrome, Safari, Firefox e Microsoft Edge Chromium. È possibile che si verifichino problemi durante l&#39;utilizzo di alcune funzionalità nelle versioni precedenti dei browser o nei browser obsoleti, ad esempio Internet Explorer.

## Dove è possibile ottenere il codice sorgente sul Web SDK?

Vedi l&#39;archivio [Alloy](https://github.com/adobe/alloy) su GitHub.
