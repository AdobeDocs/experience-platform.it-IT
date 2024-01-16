---
title: ID dispositivo di prime parti in Web SDK
description: Scopri come configurare gli ID dispositivo di prime parti (FPID) per Adobe Experience Platform Web SDK.
exl-id: c3b17175-8a57-43c9-b8a0-b874fecca952
source-git-commit: dea75b92847320284e1dc1b939f3ae11a12077a8
workflow-type: tm+mt
source-wordcount: '1734'
ht-degree: 0%

---

# ID dispositivo di prime parti in Web SDK

Adobe Experience Platform Web SDK assegna [Adobe Experience Cloud ID (ECID)](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=it) ai visitatori del sito web utilizzando i cookie, per monitorare il comportamento degli utenti. Per tenere conto delle restrizioni del browser sulla durata dei cookie, puoi invece scegliere di impostare e gestire gli identificatori dei tuoi dispositivi. Questi sono denominati ID dispositivo di prime parti (FPID, first party device ID).

>[!NOTE]
>
>Il supporto per ID dispositivo di prime parti è disponibile solo quando si inviano dati a Platform Edge Network tramite Platform Web SDK.

>[!IMPORTANT]
>
>Gli ID dispositivo di prime parti non sono compatibili con [cookie di terze parti](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#identity) funzionalità di Web SDK.
>Puoi utilizzare gli ID dispositivo di prime parti oppure cookie di terze parti, ma non puoi utilizzare entrambe le funzioni contemporaneamente.

Questo documento illustra come configurare gli ID dispositivo di prime parti per l’implementazione di Platform Web SDK.

## Prerequisiti

Questa guida presuppone che tu abbia familiarità con il funzionamento dei dati di identità per Platform Web SDK, incluso il ruolo di ECID e `identityMap`. Consulta la panoramica su [dati di identità nel Web SDK](./overview.md) per ulteriori informazioni.

## Utilizzo degli FPID

Gli FPID tengono traccia dei visitatori utilizzando cookie di prime parti. I cookie di prime parti sono più efficaci quando vengono impostati utilizzando un server che utilizza un DNS [Un record](https://datatracker.ietf.org/doc/html/rfc1035) (per IPv4) oppure [record AAAA](https://datatracker.ietf.org/doc/html/rfc3596) (per IPv6), anziché un codice DNS CNAME o JavaScript.

>[!IMPORTANT]
>
>`A` o `AAAA` i record sono supportati solo per l’impostazione e il tracciamento dei cookie. Il metodo principale per la raccolta dei dati è tramite un CNAME DNS. In altre parole, gli FPID vengono impostati utilizzando un record A o AAAA e quindi inviati ad Adobe utilizzando un CNAME.
>
>Il [Programma di certificazione gestito da Adobe](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html#adobe-managed-certificate-program) è ancora supportato anche per la raccolta dati di prime parti.

Una volta impostato un cookie FPID, il relativo valore può essere recuperato e inviato all’Adobe durante la raccolta dei dati dell’evento. Gli FPID raccolti vengono utilizzati come seed per generare ECID, che continuano a essere gli identificatori primari nelle applicazioni Adobe Experience Cloud.

Per inviare un FPID per un visitatore del sito web alla rete Edge di Platform, devi includere l’FPID nel `identityMap` per quel visitatore. Vedi la sezione più avanti in questo documento su [utilizzo degli FPID in `identityMap`](#identityMap) per ulteriori informazioni.

### Requisiti di formattazione degli ID

Platform Edge Network accetta solo ID conformi alla [Formato UUIDv4](https://datatracker.ietf.org/doc/html/rfc4122). Gli ID dispositivo non in formato UUIDv4 verranno rifiutati.

La generazione di un UUID si tradurrà quasi sempre in un ID casuale univoco, con una probabilità di collisione trascurabile. Non è possibile eseguire il seeding di UUIDv4 utilizzando indirizzi IP o qualsiasi altra informazione personale identificabile (PII). Gli UUID sono onnipresenti e le librerie possono essere trovate praticamente per ogni linguaggio di programmazione per generarli.

## Impostazione di un cookie con il tuo server

Quando imposti un cookie utilizzando un server di tua proprietà, è possibile utilizzare diversi metodi per impedire che il cookie venga limitato a causa dei criteri del browser:

* Generare cookie utilizzando linguaggi di script lato server
* Imposta i cookie in risposta a una richiesta API effettuata a un sottodominio o a un altro endpoint sul sito
* Generare cookie utilizzando un CMS
* Generare cookie utilizzando una rete CDN

>[!IMPORTANT]
>
>Cookie impostati con JavaScript `document.cookie` Il metodo non sarà quasi mai protetto dai criteri del browser che limitano la durata dei cookie.

### Quando impostare il cookie

Il cookie FPID dovrebbe idealmente essere impostato prima di effettuare qualsiasi richiesta alla rete Edge. Tuttavia, negli scenari in cui ciò non è possibile, un ECID viene comunque generato utilizzando i metodi esistenti e funge da identificatore primario finché il cookie esiste.

Supponendo che l’ECID sia infine interessato da un criterio di eliminazione del browser, ma l’FPID non lo è, l’FPID diventerà l’identificatore primario alla visita successiva e verrà utilizzato per seed l’ECID a ogni visita successiva.

### Impostazione della scadenza per il cookie

Impostare la scadenza di un cookie è un aspetto che deve essere attentamente considerato quando si implementa la funzionalità FPID. Nel decidere questa opzione, è necessario considerare i paesi o le aree geografiche in cui l&#39;organizzazione opera insieme alle leggi e alle politiche in ognuna di queste aree.

Come parte di questa decisione, puoi adottare un criterio di impostazione dei cookie a livello aziendale o diverso a seconda delle impostazioni internazionali.

Indipendentemente dall’impostazione scelta per la scadenza iniziale di un cookie, è necessario assicurarsi di includere una logica che estenda la scadenza del cookie ogni volta che si verifica una nuova visita al sito.

## Impatto dei flag dei cookie

Esistono diversi flag di cookie che influiscono sul modo in cui i cookie vengono trattati nei diversi browser:

* [&quot;HTTPOnly&quot;](#http-only)
* [&quot;Secure&quot;](#secure)
* [&quot;SameSite&quot;](#same-site)

### `HTTPOnly` {#http-only}

Cookie impostati tramite `HTTPOnly` Impossibile accedere al flag tramite script lato client. Ciò significa che se si imposta un `HTTPOnly` quando si imposta il FPID, è necessario utilizzare un linguaggio di script lato server per leggere il valore del cookie da includere nel `identityMap`.

Se scegli di fare in modo che Platform Edge Network legga il valore del cookie FPID, impostando `HTTPOnly` Questo flag assicura che il valore non sia accessibile da alcuno script lato client, ma non abbia alcun impatto negativo sulla capacità di Platform Edge Network di leggere il cookie.

>[!NOTE]
>
>Uso del `HTTPOnly` Questo flag non ha alcun impatto sui criteri dei cookie che possono limitare la durata dei cookie. Tuttavia, è ancora qualcosa da considerare quando imposti e leggi il valore dell’FPID.

### `Secure` {#secure}

Cookie impostati con `Secure` L&#39;attributo viene inviato solo al server con una richiesta crittografata tramite il protocollo HTTPS. L’utilizzo di questo flag può contribuire a garantire che gli aggressori man-in-the-middle non possano accedere facilmente al valore del cookie. Quando possibile, è sempre consigliabile impostare `Secure` flag.

### `SameSite` {#same-site}

Il `SameSite` Questo attributo consente ai server di determinare se i cookie vengono inviati con richieste tra siti diversi. L’attributo fornisce una certa protezione contro gli attacchi di tipo cross-site forgery. Esistono tre valori possibili: `Strict`, `Lax`, e `None`. Consulta il team interno per determinare quale impostazione è corretta per la tua organizzazione.

In caso negativo `SameSite` è specificato, l&#39;impostazione predefinita per alcuni browser è ora `SameSite=Lax`.

## Utilizzo degli FPID in `identityMap` {#identityMap}

Di seguito è riportato un esempio di impostazione di un FPID nel `identityMap`:

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

Come con altri tipi di identità, puoi includere l’FPID con altre identità in `identityMap`. Di seguito è riportato un esempio dell’FPID incluso con un ID del sistema di gestione delle relazioni con i clienti autenticato:

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

Se l’FPID è contenuto in un cookie letto dalla rete Edge quando è abilitata la raccolta dati di prime parti, devi acquisire solo l’ID CRM autenticato:

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

I seguenti elementi `identityMap` si tradurrebbe in una risposta di errore da parte di Edge Network poiché manca il `primary` per l&#39;identificatore FPID. Almeno uno degli ID presenti in `identityMap` deve essere contrassegnato come `primary`.

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

La risposta di errore restituita da Edge Network in questo caso è simile alla seguente:

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

Quando sono presenti sia un ECID che un FPID, all’ECID viene assegnata la priorità di identificare l’utente. In questo modo, quando un ECID esistente è presente nell’archivio dei cookie del browser, rimane l’identificatore principale e i conteggi dei visitatori esistenti non rischiano di essere interessati. Per gli utenti esistenti, l’FPID non diventerà l’identità principale fino alla scadenza dell’ECID o alla sua eliminazione in seguito a una policy del browser o a un processo manuale.

Le identità hanno la priorità nel seguente ordine:

1. ECID incluso in `identityMap`
1. ECID memorizzato in un cookie
1. FPID incluso nel `identityMap`
1. FPID memorizzato in un cookie

## Migrazione agli ID dispositivo di prime parti

Se stai eseguendo la migrazione a utilizzando gli FPID da un’implementazione precedente, potrebbe essere difficile visualizzare l’aspetto della transizione a un livello basso.

Per illustrare questo processo, considera uno scenario che coinvolge un cliente che ha già visitato il tuo sito e quale impatto avrebbe una migrazione FPID su come quel cliente viene identificato nelle soluzioni Adobe.

![Diagramma che mostra come i valori ID di un cliente vengono aggiornati tra le visite dopo la migrazione agli FPID](../assets/identity/tracking/visits.png)

>[!IMPORTANT]
>
>Il `ECID` il cookie ha sempre la priorità rispetto al `FPID`.

| Visita | Descrizione |
| --- | --- |
| Prima visita | Supponiamo che non abbiate ancora iniziato a impostare il cookie FPID. L’ECID contenuto nel [Cookie AMCV](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html#section-c55af54828dc4cce89f6118655d694c8) sarà l’identificatore utilizzato per identificare il visitatore. |
| Seconda visita | Rollout della soluzione ID dispositivo di prime parti avviato. L’ECID esistente è ancora presente e rimane l’identificatore primario per l’identificazione dei visitatori. |
| Terza visita | Tra la seconda e la terza visita, è trascorso abbastanza tempo da consentire l’eliminazione dell’ECID a causa dei criteri del browser. Tuttavia, poiché l’FPID è stato impostato utilizzando un record A DNS, l’FPID persiste. L’FPID è ora considerato l’ID primario e viene utilizzato per seed l’ECID, che viene scritto sul dispositivo dell’utente finale. L’utente viene ora considerato un nuovo visitatore nelle soluzioni Adobe Experience Platform e Experience Cloud. |
| Quarta visita | Tra la terza e la quarta visita, è trascorso abbastanza tempo da consentire l’eliminazione dell’ECID a causa dei criteri del browser. Come la visita precedente, l’FPID rimane dovuto al modo in cui è stato impostato. Questa volta viene generato lo stesso ECID della visita precedente. L’utente viene visualizzato in tutte le soluzioni di Experience Platform e Experience Cloud come lo stesso utente della visita precedente. |
| Quinta visita | Tra la quarta e la quinta visita, l’utente finale ha cancellato tutti i cookie nel suo browser. Viene generato un nuovo FPID e utilizzato per la creazione di un nuovo ECID. L’utente viene ora considerato un nuovo visitatore nelle soluzioni Adobe Experience Platform e Experience Cloud. |

{style="table-layout:auto"}

## Domande frequenti

Di seguito è riportato un elenco di risposte alle domande più frequenti sugli ID dispositivo di prime parti.

### In che modo il seeding di un ID è diverso dalla semplice generazione di un ID?

Il concetto di seeding è unico in quanto l&#39;FPID passato a Adobe Experience Cloud viene convertito in un ECID utilizzando un algoritmo deterministico. Ogni volta che lo stesso FPID viene inviato alla rete Edge di Adobe Experience Platform, viene generato lo stesso ECID dall’FPID.

### Quando deve essere generato l’ID dispositivo di prime parti?

Per ridurre l’inflazione di visitatori potenziali, è necessario generare l’FPID prima di effettuare la prima richiesta utilizzando l’SDK per web. Tuttavia, se non riesci a eseguire questa operazione, per tale utente verrà comunque generato un ECID che verrà utilizzato come identificatore primario. L’FPID generato non diventerà l’identificatore primario fino a quando l’ECID non sarà più presente.

### Quali metodi di raccolta dati supportano gli ID dispositivo di prime parti?

Attualmente solo Web SDK supporta gli FPID.

### Gli FPID sono memorizzati su qualsiasi piattaforma o soluzione Experience Cloud?

Una volta che l’FPID è stato utilizzato per la generazione di un ECID, viene rilasciato dal `identityMap` e sostituito con l’ECID generato. L’FPID non viene memorizzato in alcuna soluzione Adobe Experience Platform o Experience Cloud.
