---
title: Risoluzione dei problemi di identità nella raccolta dati
description: Diagnosticare i problemi di identità comuni nelle implementazioni di Web SDK, tra cui l’inflazione dei visitatori, le incoerenze ECID, i conflitti tra cookie e i problemi FPID.
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 0%

---

# Risoluzione dei problemi di identità nella raccolta dati

I problemi di identità spesso emergono come sintomi nei rapporti a valle (conteggi di visitatori gonfiati, profili frammentati o personalizzazione interrotta) anziché come errori nell’implementazione stessa. Questa pagina consente di diagnosticare e risolvere i problemi di identità più comuni nelle implementazioni di Web SDK. Per informazioni generali sul funzionamento dell&#39;identità nella raccolta dati, vedere [panoramica identità](./overview.md).

## Controllare i valori di identità {#inspect-identity}

Prima di risolvere un problema specifico, recuperare i valori di identità correnti utilizzati dal Web SDK. Utilizza il comando [`getIdentity`](/help/collection/js/commands/getidentity.md) per visualizzare l&#39;ECID e altri segnali di identità:

```js
alloy("getIdentity", { namespaces: ["ECID", "CORE"] }).then(function(result) {
  console.log("ECID:", result.identity.ECID);
  console.log("CORE ID:", result.identity.CORE);
  console.log("Edge region:", result.edge.regionID);
});
```

Puoi anche esaminare i valori di identità negli strumenti di sviluppo del browser:

1. Apri la scheda **Applicazione** (Chrome/Edge) o **Archiviazione** (Firefox/Safari).
2. Cerca i cookie con il prefisso `kndctr_` nel tuo dominio. Il cookie `kndctr_<ORG_ID>_AdobeOrg_identity` contiene l&#39;ECID.
3. Apri la scheda **Rete** e trova una richiesta `interact` o `collect` ad Edge Network. Controllare il payload della richiesta per `identityMap` e il payload di risposta per gli handle di identità.

## Problemi comuni {#common-issues}

+++**Inflazione conteggio visitatori**

**Sintomo**: i rapporti di Analytics mostrano più visitatori univoci del previsto, oppure la stessa persona appare come più visitatori nelle sessioni.

**Possibili cause**:

| Causa | Come identificare | Risoluzione |
| --- | --- | --- |
| Durata cookie breve | Verificare la scadenza dei cookie `kndctr_` nel browser. Se scadono entro 7 giorni o meno, i criteri del browser probabilmente limitano la durata dei cookie. | Implementa [ID dispositivo di prime parti (FPID)](./fpid.md) impostati da un server utilizzando un record A/AAAA DNS per una persistenza dei cookie più lunga. |
| FPID mancante alla prima richiesta | Esamina la prima richiesta di Edge Network al caricamento della pagina. Se non è presente alcun cookie FPID, Edge Network genera un nuovo ECID. Se l’FPID è impostato dopo la prima richiesta, l’ECID generato in tale prima richiesta è orfano. | Imposta il cookie FPID prima che il Web SDK invii la sua prima richiesta. Vedere [Quando impostare il cookie](./fpid.md#when-to-set-cookie). |
| Mancata corrispondenza di `orgId` tra domini | Confronta il valore di configurazione `orgId` nei tuoi domini. I valori non corrispondenti causano ambiti di identità separati. | Utilizza lo stesso [`orgId`](/help/collection/js/commands/configure/orgid.md) in tutti i domini dell&#39;organizzazione. |
| Banner di consenso eliminazione dei cookie | Se l’implementazione del consenso cancella tutti i cookie prima che il consenso venga concesso e poi il Web SDK viene inizializzato, viene generato un nuovo ECID. | Configura il banner di consenso per mantenere i cookie `kndctr_` o ritarda l&#39;inizializzazione di Web SDK fino a quando non viene stabilito il consenso. Vedi anche [Consenso e identità](./consent.md). |
| Cookie FPID impostati da JavaScript | I cookie impostati con `document.cookie` sono soggetti a restrizioni del browser (ITP, ETP) che ne limitano la durata, talvolta fino a 24 ore. | Imposta i cookie FPID dal server utilizzando un record A/AAAA DNS, non da JavaScript. |

+++

+++**ECID cambia in modo imprevisto tra le pagine**

**Sintomo**: ECID è diverso in pagine diverse dello stesso dominio o cambia a ogni caricamento di pagina.

**Passaggi diagnostici**:

1. Verificare che il cookie di identità `kndctr_` sia presente in entrambe le pagine. Se manca in una pagina, verificare che il Web SDK sia configurato in tale pagina.
2. Verifica che il dominio del cookie sia impostato su un livello sufficiente. Un cookie impostato su `shop.example.com` non è disponibile su `www.example.com`. Assicurati che l’infrastruttura di prima parte per la raccolta e l’impostazione dei cookie utilizzi lo stesso ambito di dominio.
3. Cerca JavaScript che cancelli i cookie durante la navigazione (ad esempio, script aggressivi di consenso ai cookie o strumenti per la privacy).
4. Se utilizzi un’applicazione a pagina singola, verifica che il Web SDK sia configurato una sola volta al momento dell’inizializzazione dell’app, non reinizializzato a ogni modifica del percorso. La reinizializzazione può generare un nuovo ECID.

+++

+++**FPID non sta eseguendo il seeding dell&#39;ECID**

**Sintomo**: hai impostato un cookie FPID, ma `getIdentity` restituisce un ECID non coerente tra le visite, oppure l&#39;FPID non viene visualizzato nei payload delle richieste di Edge Network.

**Passaggi diagnostici**:

1. **Verifica il formato del cookie FPID**: l&#39;FPID deve essere un [UUIDv4](https://datatracker.ietf.org/doc/html/rfc4122) valido. Apri gli strumenti di sviluppo del browser, individua il cookie FPID e verifica che il valore corrisponda al pattern `xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx`.
2. **Controllare il nome del cookie nel flusso di dati**: se si utilizza il metodo cookie [flusso di dati](./fpid.md#setting-cookie-datastreams), il nome del cookie configurato nel flusso di dati deve corrispondere esattamente al nome del cookie impostato dal server.
3. **Conferma l&#39;invio del cookie alla richiesta**: nella scheda Rete, controlla l&#39;intestazione `Cookie` della richiesta Edge Network. Il cookie FPID deve essere incluso.
4. **Verifica priorità identità**: se un ECID esistente è già memorizzato in un cookie `kndctr_`, ha la precedenza sull&#39;FPID. L’FPID crea un nuovo ECID solo quando non è presente alcun ECID esistente. Vedi [Funzionamento degli FPID](./fpid.md#how-fpids-work) per l&#39;ordine di priorità completo.
5. **Convalida il CNAME**: se utilizzi il metodo cookie dello stream di dati, verifica che il CNAME della raccolta di prime parti sia configurato correttamente e che le richieste vengano instradate attraverso di esso.

+++

+++**L&#39;identità tra domini diversi non funziona**

**Sintomo**: un visitatore che fa clic da uno dei tuoi domini a un altro viene considerato come un nuovo visitatore nel dominio di destinazione.

**Passaggi diagnostici**:

1. **Controlla l&#39;URL**: controlla l&#39;URL di destinazione quando il visitatore fa clic sul collegamento. Deve contenere un parametro della stringa di query `adobe_mc`. Se manca il parametro, il dominio di origine non lo aggiunge. Vedere [Implementare la condivisione tra domini](./cross-domain-sharing.md#implement-cross-domain-sharing).
2. **Controllare la tempistica**: il parametro `adobe_mc` scade dopo cinque minuti. Se il caricamento della pagina di destinazione richiede troppo tempo (ad esempio a causa di reindirizzamenti o rete lenta), il parametro può scadere prima che il Web SDK possa leggerlo.
3. **Verifica `orgId` corrispondenza**: entrambi i domini devono utilizzare lo stesso [`orgId`](/help/collection/js/commands/configure/orgid.md). Se gli ID organizzazione non corrispondono, il dominio di destinazione rifiuta l’identità consegnata.
4. **Conferma che il Web SDK si trova nella destinazione**: la pagina di destinazione deve avere il Web SDK installato e configurato. Senza di esso, il parametro `adobe_mc` viene ignorato.
5. **Verifica stripping URL**: alcuni servizi di reindirizzamento, CDN o parametri della stringa di query sconosciuti nella striscia logica lato server. Verificare che `adobe_mc` sopravviva a eventuali reindirizzamenti intermedi tra le pagine di origine e di destinazione.

+++

+++**Handoff identità da dispositivo mobile a Web non riuscito**

**Sintomo**: un visitatore che inizia nell&#39;app mobile e apre un WebView o un browser mobile viene considerato come un nuovo visitatore sul lato web.

**Passaggi diagnostici**:

1. **Verificare l&#39;URL**: registrare l&#39;URL passato a WebView. Deve contenere un parametro `adobe_mc` generato da [`getUrlVariables`](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#geturlvariables).
2. **Verifica versioni di SDK**: la versione dell&#39;identità mobile per l&#39;estensione Edge Network deve essere 1.1.0 o successiva e la versione del SDK Web 2.11.0 o successiva.
3. **Controllare la tempistica**: come la condivisione tra domini diversi, il parametro `adobe_mc` scade dopo cinque minuti. Verificare che WebView venga caricato immediatamente dopo la costruzione dell&#39;URL.
4. **Conferma `orgId` corrispondenza**: l&#39;ID organizzazione Experience Cloud deve essere lo stesso nelle configurazioni di SDK per dispositivi mobili e SDK Web.

+++
