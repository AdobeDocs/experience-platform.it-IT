---
title: ID dispositivo di prime parti nell’SDK per web di Platform
description: Scopri come configurare gli ID dispositivo di prime parti (FPID) per l’SDK web di Adobe Experience Platform.
exl-id: c3b17175-8a57-43c9-b8a0-b874fecca952
source-git-commit: 700dea7ed7f35797b3a3fe4bf09f5e266577363b
workflow-type: tm+mt
source-wordcount: '1776'
ht-degree: 1%

---

# ID dispositivo di prime parti nell’SDK per web di Platform

L&#39;SDK Web di Adobe Experience Platform assegna [ID Adobe Experience Cloud (ECID)](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=en) ai visitatori del sito web tramite l’uso di cookie, al fine di monitorare il comportamento degli utenti. Per tenere conto delle restrizioni del browser alla durata dei cookie, puoi scegliere di impostare e gestire gli identificatori dei dispositivi. Questi sono denominati ID dispositivo di prime parti (FPID).

>[!NOTE]
>
>Il supporto per gli ID dispositivo di prime parti è disponibile solo quando si inviano dati a Platform Edge Network tramite l’SDK per web di Platform.

Questo documento illustra come configurare ID dispositivo di prime parti per l’implementazione dell’SDK per web di Platform.

## Prerequisiti

Questa guida presuppone che tu abbia familiarità con il funzionamento dei dati di identità per Platform Web SDK, incluso il ruolo degli ECID e `identityMap`. Vedi la panoramica su [Dati di identità nell’SDK per web](./overview.md) per ulteriori informazioni.

## Utilizzo di FPID

Gli FPID tengono traccia dei visitatori tramite l’utilizzo di cookie di prime parti. I cookie di prime parti sono più efficaci quando vengono impostati utilizzando un server che sfrutta un DNS [Record](https://datatracker.ietf.org/doc/html/rfc1035) (per IPv4) o [Record AAAA](https://datatracker.ietf.org/doc/html/rfc3596) (per IPv6), a differenza di un codice CNAME DNS o JavaScript.

>[!IMPORTANT]
>
>I record A o AAAA sono supportati solo per l’impostazione e il tracciamento dei cookie. Il metodo principale per la raccolta dei dati è tramite un CNAME DNS. In altre parole, gli FPID vengono impostati utilizzando un record A o AAAA e vengono quindi inviati ad Adobe utilizzando un CNAME.
>
>La [Programma di certificazione gestito da Adobe](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html#adobe-managed-certificate-program) è ancora supportato anche per la raccolta dati di prime parti.

Una volta impostato un cookie FPID, il suo valore può essere recuperato e inviato ad Adobe durante la raccolta dei dati dell’evento. I FPID raccolti vengono utilizzati come semi per generare ECID, che continuano ad essere gli identificatori principali nelle applicazioni Adobe Experience Cloud.

Per inviare un FPID per un visitatore di un sito web a Platform Edge Network, è necessario includere il FPID nel `identityMap` per quel visitatore. Vedi la sezione più avanti in questo documento su [utilizzo di FPID in `identityMap`](#identityMap) per ulteriori informazioni.

### Requisiti di formattazione ID

Platform Edge Network accetta solo ID conformi alle [Formato UUIDv4](https://datatracker.ietf.org/doc/html/rfc4122). Gli ID dispositivo che non sono in formato UUIDv4 verranno rifiutati.

La generazione di un UUID comporterà quasi sempre un ID univoco casuale, con la probabilità che si verifichi una collisione trascurabile. Non è possibile inviare UIDv4 utilizzando indirizzi IP o altre informazioni personali identificabili (PII). Gli UUID sono onnipresenti e le librerie possono essere trovate praticamente per ogni linguaggio di programmazione per generarli.

## Impostazione di un cookie utilizzando il proprio server

Quando imposti un cookie utilizzando un server di tua proprietà, puoi utilizzare diversi metodi per impedire che il cookie venga limitato a causa dei criteri del browser:

* Generare cookie utilizzando i linguaggi di scripting sul lato server
* Imposta i cookie in risposta a una richiesta API effettuata a un sottodominio o a un altro endpoint sul sito
* Generare cookie con un CMS
* Generare cookie utilizzando una rete CDN

>[!IMPORTANT]
>
>Cookie impostati tramite JavaScript `document.cookie` quasi mai sarà protetto dai criteri del browser che limitano la durata dei cookie.

### Quando impostare il cookie

Il cookie FPID dovrebbe essere impostato idealmente prima di effettuare richieste alla rete Edge. Tuttavia, in scenari in cui ciò non sia possibile, un ECID viene ancora generato utilizzando i metodi esistenti e agisce come identificatore principale finché il cookie esiste.

Presupponendo che l’ECID sia influenzato da un criterio di eliminazione del browser, ma il FPID non lo è, il FPID diventerà l’identificatore principale nella prossima visita e verrà utilizzato per generare l’ECID in ogni visita successiva.

### Impostazione della scadenza del cookie

L’impostazione della scadenza di un cookie è qualcosa che deve essere attentamente considerata durante l’implementazione della funzionalità FPID. Quando prendi questa decisione, devi tenere conto dei paesi o delle regioni in cui la tua organizzazione opera insieme alle leggi e alle politiche in ciascuna di queste regioni.

Come parte di questa decisione, puoi adottare un criterio di impostazione dei cookie a livello aziendale o uno che varia per gli utenti in ogni impostazione internazionale in cui operi.

Indipendentemente dall’impostazione scelta per la scadenza iniziale di un cookie, devi assicurarti di includere una logica che estenda la scadenza del cookie ogni volta che si verifica una nuova visita al sito.

## Impatto dei flag dei cookie

Esistono diversi flag per cookie che influiscono sul modo in cui i cookie vengono trattati su diversi browser:

* [`HTTPOnly`](#http-only)
* [`Secure`](#secure)
* [`SameSite`](#same-site)

### `HTTPOnly` {#http-only}

Cookie impostati utilizzando `HTTPOnly` Impossibile accedere al flag utilizzando script sul lato client. Ciò significa che se imposti un `HTTPOnly` flag quando si imposta il FPID, è necessario utilizzare un linguaggio di script lato server per leggere il valore del cookie per l’inclusione nel `identityMap`.

Se scegli di far leggere il valore del cookie FPID a Platform Edge Network, imposta la `HTTPOnly` Questo flag assicura che il valore non sia accessibile da alcuno script sul lato client, ma non avrà alcun impatto negativo sulla capacità di Platform Edge Network di leggere il cookie.

>[!NOTE]
>
>Uso del `HTTPOnly` Il flag non ha un impatto sui criteri dei cookie che possono limitare la durata dei cookie. Tuttavia, è comunque qualcosa che si dovrebbe considerare quando si imposta e si legge il valore del FPID.

### `Secure` {#secure}

Cookie impostati con il `Secure` Gli attributi vengono inviati al server solo con una richiesta crittografata tramite il protocollo HTTPS. L’utilizzo di questo flag può essere utile per garantire che gli aggressori man-in-the-middle non possano accedere facilmente al valore del cookie . Quando possibile, è sempre una buona idea impostare `Secure` bandiera.

### `SameSite` {#same-site}

La `SameSite` l’attributo consente ai server di determinare se i cookie vengono inviati con richieste intersito. L&#39;attributo fornisce una certa protezione contro attacchi di falsificazione cross-site. Esistono tre valori possibili: `Strict`, `Lax` e `None`. Consulta il team interno per determinare quale impostazione è più adatta alla tua organizzazione.

Se no `SameSite` L&#39;attributo è specificato, l&#39;impostazione predefinita per alcuni browser è ora `SameSite=Lax`.

## Utilizzo di FPID in `identityMap` {#identityMap}

Di seguito è riportato un esempio di come impostare un FPID su di esso come proprio nel `identityMap`:

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-42d3-9456-426614174000",
        "authenticatedState": "ambiguous",
        "primary": true
      }
    ]
  }
}
```

Come per altri tipi di identità, puoi includere il FPID con altre identità all’interno di `identityMap`. Di seguito è riportato un esempio del FPID incluso con un ID CRM autenticato:

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-42d3-9456-426614174000",
        "authenticatedState": "ambiguous",
        "primary": true
      }
    ],
    "EMAIL": [
      {
        "id": "email@mail.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

Se il FPID è contenuto in un cookie letto da Edge Network quando è abilitata la raccolta dati di prime parti, devi acquisire solo l’ID CRM autenticato:

```json
{
  "identityMap": {
    "EMAIL": [
      {
        "id": "email@mail.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

I seguenti `identityMap` causerebbe una risposta di errore da parte di Edge Network in quanto manca il `primary` indicatore del FPID. Almeno uno degli ID presenti in `identityMap` deve essere contrassegnato come `primary`.

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-12d3-a456-426614174000",
        "authenticatedState": "ambiguous"
      }
    ],
    "EMAIL": [
      {
        "id": "email@mail.com",
        "authenticatedState": "authenticated"
      }
    ]
  }
}
```

La risposta di errore restituita da Experience Edge in questo caso è simile alla seguente:

```json
{
    "type": "https://ns.adobe.com/aep/errors/EXEG-0306-400",
    "status": 400,
    "title": "No primary identity set in request (event)",
    "detail": "No primary identity found in the input event. Update the request accordingly to your schema and try again.",
    "report": {
        "requestId": "{REQUEST_ID}",
        "configId": "{CONFIG_ID}",
        "orgId": "{ORG_ID}"
    }
}
```

## Gerarchia ID

Se sono presenti sia un ECID che un FPID, l’ECID viene assegnato come priorità nell’identificazione dell’utente. In questo modo, quando un ECID esistente è presente nell’archivio dei cookie del browser, continuerà ad essere l’identificatore principale e i conteggi dei visitatori esistenti non rischiano di essere interessati. Per gli utenti esistenti, il FPID non diventerà l’identità principale fino alla scadenza o all’eliminazione dell’ECID a seguito di una politica del browser o di un processo manuale.

Le identità hanno priorità nel seguente ordine:

1. ECID incluso nel `identityMap`
1. ECID memorizzato in un cookie
1. FPID incluso nel `identityMap`
1. FPID memorizzato in un cookie

## Migrazione a ID dispositivo di prime parti

Se effettui la migrazione all’utilizzo di FPID da un’implementazione precedente, potrebbe essere difficile visualizzare l’aspetto della transizione a un livello basso.

Per illustrare questo processo, considera uno scenario che coinvolge un cliente che ha visitato il tuo sito in precedenza e quale impatto avrebbe una migrazione FPID sul modo in cui tale cliente viene identificato nelle soluzioni di Adobe.

![Diagramma che mostra come i valori ID di un cliente vengono aggiornati tra le visite dopo la migrazione a FPID](../images/identity/tracking/visits.png)

| Visita | Descrizione |
| --- | --- |
| Prima visita | Supponi di non aver ancora avviato l’impostazione del cookie FPID. L&#39;ECID contenuto nel [Cookie AMCV](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html#section-c55af54828dc4cce89f6118655d694c8) sarà l’identificatore utilizzato per identificare il visitatore. |
| Seconda visita | È stato avviato il rollout della soluzione ID dispositivo di prime parti. L’ECID esistente è ancora presente e continua ad essere l’identificatore principale per l’identificazione dei visitatori. |
| Terza visita | Tra la seconda e la terza visita, è trascorso un periodo di tempo sufficiente perché l’ECID è stato eliminato a causa dei criteri del browser. Tuttavia, poiché il FPID è stato impostato utilizzando un record A DNS, il FPID persiste. Il FPID viene ora considerato l’ID principale e utilizzato per generare l’ECID, scritto sul dispositivo dell’utente finale. Ora l’utente viene considerato un nuovo visitatore nelle soluzioni Adobe Experience Platform ed Experience Cloud. |
| Quarta visita | Tra la terza e la quarta visita, è trascorso un periodo di tempo sufficiente perché l’ECID è stato eliminato a causa dei criteri del browser. Come la visita precedente, il FPID rimane dovuto al modo in cui è stato impostato. Questa volta viene generato lo stesso ECID della visita precedente. L’utente viene visualizzato nelle soluzioni di Experience Platform e Experience Cloud dello stesso utente della visita precedente. |
| Quinta visita | Tra la quarta e la quinta visita, l’utente finale ha cancellato tutti i cookie nel proprio browser. Viene generato un nuovo FPID che viene utilizzato per impostare la creazione di un nuovo ECID. Ora l’utente viene considerato un nuovo visitatore nelle soluzioni Adobe Experience Platform ed Experience Cloud. |

{style=&quot;table-layout:auto&quot;}

## Domande frequenti

Di seguito è riportato un elenco di risposte alle domande frequenti sugli ID dispositivo di prime parti.

### In che modo il seeding di un ID è diverso dalla semplice generazione di un ID?

Il concetto di seeding è univoco in quanto il FPID passato a Adobe Experience Cloud viene convertito in un ECID utilizzando un algoritmo deterministico. Ogni volta che lo stesso FPID viene inviato alla rete Adobe Experience Platform Edge, lo stesso ECID viene impostato dal FPID.

### Quando deve essere generato l’ID dispositivo di prima parte?

Per ridurre l’inflazione potenziale dei visitatori, è necessario generare il FPID prima di effettuare la prima richiesta utilizzando l’SDK per web di Platform. Tuttavia, se non riesci a farlo, per tale utente verrà comunque generato un ECID che verrà utilizzato come identificatore principale. Il FPID generato non diventerà l’identificatore principale fino a quando l’ECID non sarà più presente.

### Quali metodi di raccolta dati supportano gli ID dispositivo di prime parti?

Attualmente solo Platform Web SDK supporta FPID.

### Gli FPID sono memorizzati su qualsiasi soluzione Platform o Experience Cloud?

Una volta che il FPID è stato utilizzato per generare un ECID, viene eliminato dal `identityMap` e sostituito con l’ECID generato. Il FPID non viene memorizzato in alcuna soluzione Adobe Experience Platform o Experience Cloud.
