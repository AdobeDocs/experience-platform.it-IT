---
title: Domande frequenti su Adobe Experience Platform Web SDK
description: Risposte alle domande frequenti su Adobe Experience Platform Web SDK.
exl-id: 6ddb4b4d-c9b8-471a-bd2e-135dc4202876
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '2104'
ht-degree: 2%

---

# Domande frequenti

Questa guida fornisce le risposte alle domande che vengono spesso poste in merito a Adobe Experience Platform Web SDK.

## Cos’è Adobe Experience Platform Web SDK?

Adobe Experience Platform Web SDK è una libreria JavaScript lato client che consente ai clienti di Adobe Experience Cloud di interagire con i vari servizi dell’Experience Cloud.

Invia i dati in modo indipendente dalla soluzione (XDM) a Adobe Experience Platform Edge Network, che quindi li mappa su formati e destinazioni specifici della soluzione e li invia in tempo reale.

**Ulteriori informazioni**
[presentazione Adobe Summit](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html)

## Quali sono le differenze tra Adobe Experience Platform Web SDK e le soluzioni precedenti?

### Prima di Adobe Experience Platform SDK

Attualmente, è necessario distribuire librerie JavaScript diverse in base a ogni singola soluzione.

* Ogni soluzione ha la propria libreria JavaScript, il proprio schema e dominio.
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

### Con Adobe Experience Platform Web SDK

Il nuovo Web SDK invia i dati per le seguenti soluzioni a un’unica destinazione (Adobe Experience Platform Edge Network) e risolve i casi di utilizzo più comuni per le soluzioni di cui sopra.

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* ID visitatore
* Adobe Experience Platform

Altre soluzioni seguiranno verso la fine dell&#39;anno.

Adobe Experience Platform Web SDK può anche inviare dati direttamente a Adobe Experience Platform. Questi dati sono in XDM e sono mappati allo schema della soluzione lato server.

## Qual è il valore di questo nuovo Web SDK?

**Prestazioni:** L’SDK per web è più piccolo rispetto all’utilizzo di tutte le librerie di Adobi correnti e fornisce caricamenti di pagina significativamente più veloci.

**Semplicità** La combinazione di XDM, Web SDK, tag, Edge Network, soluzioni Adobe Experience Cloud e Adobe Experience Platform crea una storia di raccolta dati facile da capire e da seguire.

* **XDM:** Schema indipendente dalla soluzione utilizzato per inviare dati ad Adobe. Non è più possibile assegnare tag a eVar o mbox.
* **Adobe Experience Platform Web SDK:** Semplifica l&#39;invio e la ricezione di dati a Adobe Experience Platform Edge Network.
* **Tag:** Semplifica la distribuzione e la configurazione dell’SDK per web (e di qualsiasi altro tag JavaScript) su un sito.
* **Rete Edge:** Indirizza facilmente i dati a Adobe Experience Platform e alle soluzioni nel formato richiesto.
* **Soluzioni Adobe Experience Platform e Adobe:** Abilita la proposta di valore.

**Controllo:** Poiché tutti i dati utilizzano un flusso di dati singolo e connesso, è possibile seguire e controllare in modo logico l&#39;aspetto dei dati ogni millisecondo del percorso, da e verso le applicazioni.

**Moderno e pronto per il futuro:** L’SDK per web e la sua connessione alla rete Edge hanno consentito a Adobe di modernizzare in modo significativo il modo in cui Adobe gestisce la raccolta di dati, la personalizzazione, il consenso e il futuro dei cookie di terze parti. Abilita un dominio di prima parte, gestito da Adobe.

**Time-to-value:** Adobe ha lavorato sodo (e continuerà) per semplificare il più possibile l’implementazione dell’SDK web tramite tag e la mappatura dei dati lato client su XDM. Al termine di questo lavoro, tutte le altre soluzioni di Adobe e i servizi Adobe Experience Platform possono essere attivati o disattivati sul lato server. Ad esempio, se utilizzi questo per Adobe Analytics e desideri attivare Target o Experienci Platform, puoi semplicemente attivare la configurazione Datastream e illuminare questi casi d’uso.

## Che cos&#39;è Alloy?

Alloy è il nome di codice per Adobe Experience Platform Web SDK. Viene utilizzato all&#39;interno del codice sorgente e del nome file dell&#39;SDK, anche se Adobe Experience Platform Web SDK è il nome ufficiale.

## I clienti devono acquistare Adobe Experience Platform per utilizzare [!DNL Web SDK]?

No. Qualsiasi cliente di esperienza digitale Adobe può utilizzare gratuitamente Adobe Experience Platform Web SDK. Clienti che desiderano utilizzare [!DNL Web SDK] dovrà configurare le autorizzazioni corrette per la creazione di schemi, set di dati, spazi dei nomi delle identità e flussi di dati nell’interfaccia utente di Data Collection o nell’interfaccia utente di Experienci Platform.

Per ulteriori informazioni sulla configurazione di queste autorizzazioni, consulta la documentazione su [gestione autorizzazioni raccolta dati](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=en).

## Chi deve utilizzare l’SDK per web?

Adobe Experience Platform Web SDK è stato sviluppato per i seguenti utenti:

* Utenti Adobe Experience Platform
   * Se devi inviare i dati direttamente da un dispositivo a Adobe Experience Platform, questo è il metodo ufficialmente consigliato.
   * Adobe è consapevole del fatto che l’utilizzo del connettore Adobe Analytics è più veloce se il cliente dispone già di Adobe Analytics, ma non rappresenta la strategia a lungo termine per la raccolta dei dati.

* Clienti delle soluzioni Adobe Experience Cloud
   * I nuovi clienti di Adobe Analytics, Adobe Audience Manager e Adobe Target devono iniziare con il nuovo Web SDK e non utilizzare le librerie legacy.
   * I clienti esistenti che desiderano ottenere l’implementazione più ottimizzata possibile devono utilizzare il nuovo Web SDK.


## Come posso ottenere l’accesso per iniziare a utilizzare Adobe Experience Platform Web SDK?

L’SDK per web è attualmente disponibile al pubblico e può essere utilizzato per inviare dati ai prodotti Adobe Experience Cloud. La capacità di inviare dati a soluzioni di terze parti sarà presto disponibile. L’SDK è gratuito ed è ospitato gratuitamente da Adobe. Se necessario, è possibile scaricarlo e ospitarlo sui propri server senza alcun costo. Platform Web SDK richiede l’accesso alle configurazioni dello stream di dati e al generatore di schemi XDM di Adobe Experience Platform per consentire ai server di Adobe di gestire correttamente i dati in entrata provenienti dall’SDK. Se desideri ottenere l’accesso, contatta il team del tuo account di Adobe per avviare la procedura di richiesta.

## Quali casi di utilizzo sono attualmente supportati dall’SDK per web?

L’SDK per web si sta evolvendo rapidamente. Si stanno elaborando altri casi d’uso. È possibile trovare [elenco dei casi d’uso attualmente supportati qui.](https://github.com/adobe/alloy/projects/5)

## I clienti attuali devono rinominare i tag dei loro siti?

Dipende. Adobe Experience Platform Web SDK può essere distribuito in due stili diversi. Un futuro documento di migrazione fornirà ulteriori dettagli.

* **Solo un altro tag:** Se al sito sono già stati assegnati dei tag per le soluzioni e non è possibile assegnare nuovi tag, ma si desidera inviare i dati a Adobe Experience Platform Edge Network, ad Experience Platform per i casi d&#39;uso o per le prossime funzioni di inoltro degli eventi (vedere di seguito), è possibile aggiungere `alloy.js` sul sito, dove funziona come &quot;solo un altro tag&quot;.

* **L’unico tag:** Se desideri utilizzare l’SDK web per una soluzione di Experience Cloud, devi utilizzarlo per _tutto_ delle soluzioni sulla pagina. Ad esempio, se il tuo sito è già taggato per Adobe Analytics e desideri utilizzarlo per Target, devi utilizzarlo per entrambi, così come per qualsiasi altro in futuro.

In altre parole, se decidi di utilizzare Adobe Experience Platform Web SDK per casi di utilizzo non correlati alla soluzione, puoi assegnare al sito i tag `alloy.js` e andare avanti come se si trattasse di una nuova soluzione. Se desideri utilizzarlo per Adobe Analytics, Target o Audienci Manager o per i casi di utilizzo dell’applicazione, potrebbe essere necessario rimuovere uno qualsiasi dei codici legacy dalla pagina.

## Posso eseguire la migrazione degli ECID quando inizio a utilizzare Alloy in modo che i visitatori del mio sito web non inizino a essere visualizzati come nuovi visitatori?

Sì, Adobe Experience Platform Web SDK fornisce una funzione di migrazione delle identità. Segui le istruzioni per la migrazione degli ID in [Documentazione di identità di Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#id-migration) per ulteriori dettagli.

## Quali sono le differenze tra Web SDK e i tag?

* **Tag nell’Experience Platform** gestisci il codice del dispositivo. Utilizzali per distribuire più facilmente il codice. Sono liberi e potenti.

* **Adobe Experience Platform Web SDK** è il nome ufficiale del nuovo codice che verrebbe distribuito dai tag, ad Adobe nei casi di utilizzo. È anche libero e potente.

* **`alloy.js`** è il nome file del codice Adobe Experience Platform Web SDK.

## Devo utilizzare i tag per distribuire l’SDK web?

No. È possibile scaricare `alloy.js` archiviati.

Tuttavia:

* Adobe Experience Platform Web SDK richiede un ID Datastream che consenta alla rete Edge di identificare il flusso e determinare cosa fare con i dati. Questo ID viene creato in Experienci Platform. Ciò non significa che devi utilizzare l’interfaccia utente per creare le proprietà o distribuire il codice JavaScript, ma che devi utilizzare i tag per creare un ID di configurazione.

* I tag non sono solo i migliori gestori di tag e SDK disponibili, ma semplificano anche la distribuzione `alloy.js` e mappare i dati su schemi XDM. Se decidi di non utilizzare i tag, dovrai gestire la distribuzione `alloy.js`, eventi e mappatura dei dati in XDM prima di inviarli. Questo è un _molto_ processo più difficile rispetto all’utilizzo dei tag.

* È consigliabile utilizzare i tag per distribuire `alloy.js`, anche se è l’unico tag per cui lo utilizzi.

## Cos’è l’inoltro di eventi?

Se utilizzi i nostri SDK e invii XDM alla rete Edge, l’inoltro di eventi con queste nuove funzioni consente di installare nuove estensioni lato server e mappare tali dati su qualsiasi cosa dalla nostra rete Edge, inviandoli ovunque. Considerala come una &quot;raccolta dati come servizio&quot;. Il pacchetto sarà disponibile a pagamento, oltre ad essere incluso in Adobe Experience Platform.

## Cos’è un dominio CNAME o di prima parte e perché è importante?

Ulteriori informazioni su un CNAME sono disponibili nel [Documentazione di Adobe](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/cname.html)

## Adobe Experience Platform Web SDK utilizza i cookie? In caso affermativo, quali cookie utilizza?

Sì, attualmente l’SDK web utilizza un numero di cookie compreso tra uno e sette, a seconda dell’implementazione. Di seguito è riportato un elenco dei cookie che è possibile visualizzare con Web SDK e del modo in cui vengono utilizzati:

| **Nome** | **maxAge** | **Età amichevole** | **Descrizione** |
|---|---|---|---|
| **kndct_orgid_identity** | 34128000 | 395 giorni | Il cookie di identità memorizza l’ECID, nonché altre informazioni relative all’ECID. |
| **kndctr_orgid_consent_check** | 7200 | 2 ore | Questo cookie memorizza le preferenze di consenso dell’utente per il sito web. |
| **kndctr_orgid_consent** | 15552000 | 180 giorni | Questo cookie basato su sessione segnala al server di cercare le preferenze di consenso lato server. |
| **kndctr_orgid_cluster** | 1800 | 30 minuti | Questo cookie memorizza l’area della rete Edge che soddisfa le richieste dell’utente corrente. L’area viene utilizzata nel percorso URL in modo che la rete Edge possa indirizzare la richiesta all’area corretta. Questo cookie ha una durata di 30 minuti, pertanto se un utente si connette con un indirizzo IP diverso, la richiesta può essere indirizzata all’area più vicina. |
| **mbox** | 63072000 | 2 anni | Questo cookie viene visualizzato quando l’impostazione di migrazione di Target è impostata su true. Questo consentirà a Target di [cookie mbox](https://developer.adobe.com/target/implement/client-side/atjs/atjs-cookies/) deve essere impostato dall’SDK per web. |
| **mboxEdgeCluster** | 1800 | 30 minuti | Questo cookie viene visualizzato quando l’impostazione di migrazione di Target è impostata su true. Questo cookie consente a Web SDK di comunicare il cluster Edge corretto a at.js in modo che i profili di Target possano rimanere sincronizzati mentre gli utenti si spostano all&#39;interno di un sito. |
| **AMCV_###@AdobeOrg** | 34128000 | 395 giorni | Questo cookie viene visualizzato solo quando è abilitata la migrazione degli ID su Adobe Experience Platform Web SDK. Questo cookie è utile per la transizione a Web SDK quando alcune parti del sito utilizzano ancora visitor.js. Consulta la [Documentazione di idMigrationEnabled](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en#identity-options) per ulteriori informazioni su questa impostazione. |

Quando si utilizza l’SDK per web, la rete Edge imposta uno o più cookie di cui sopra. La rete Edge imposta tutti i cookie con `secure` e `sameSite="none"` attributi.

Se al momento sul sito web sono presenti sezioni protette e non protette, ciò potrebbe interferire con l’identificazione dell’utente. Quando un utente passa da una sezione protetta del sito a una non protetta, la rete Edge genera una nuova `ECID` con la richiesta.

## Quali browser supporta Adobe Experience Platform Web SDK?

Adobe Experience Platform Web SDK è progettato per funzionare in modo ottimale nelle versioni più recenti di Google Chrome, Safari, Firefox, Internet Explorer 11 e Microsoft Edge Chromium. Potresti riscontrare problemi nell’utilizzo di alcune funzioni nelle versioni precedenti dei browser.

## Dove è possibile ottenere ulteriori informazioni su Adobe Experience Platform Web SDK?

* [Documentazione](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=it)
* [Codice sorgente](https://github.com/adobe/alloy)
