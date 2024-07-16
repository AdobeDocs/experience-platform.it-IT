---
title: Hint posizione
description: Questo articolo spiega come funzionano gli hint di posizione nell’API del server Edge Network, in modo che le richieste degli utenti finali possano sempre essere indirizzate allo stesso server.
exl-id: 8cd2f8e2-2065-4b7e-8d35-4ed1a716f1b3
source-git-commit: 2c7a5f007189d897ed32302a2a80c1e16af6af80
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# Hint posizione

## Panoramica {#overview}

[!DNL Adobe Experience Platform Edge Network] utilizza diversi server distribuiti a livello globale per garantire tempi di risposta rapidi indipendentemente dalla posizione dell&#39;utente finale. Utilizza inoltre il routing basato su DNS per garantire che le richieste vengano sempre instradate alla posizione di Edge Network più vicina agli utenti finali.

Se gli utenti finali si connettono a una VPN o cambiano tipi di rete sui loro dispositivi mobili nel corso di una sessione, le richieste di Edge Network possono spesso essere indirizzate a una posizione diversa. Il routing a metà sessione tra server può essere problematico, in quanto le soluzioni Adobe Experience Platform e Adobe Experience Cloud memorizzano le informazioni sul profilo utente finale nell’Edge Network.

Qui entrano in gioco gli hint di posizione.

Per garantire che gli utenti finali interagiscano sempre con il server regionale Edge Network che contiene i loro dati di profilo correnti, la funzionalità degli hint di posizione assicura che tutte le richieste all’Edge Network vengano inviate allo stesso server in cui è stata effettuata la prima richiesta di una sessione. Questo consente agli utenti di avere un’esperienza coerente, indipendentemente dalle modifiche di rete che potrebbero subire nel corso di una sessione.

## Utilizzo degli hint di posizione

Gli hint di posizione sono inclusi nella risposta della richiesta di Edge Network iniziale e in tutte le richieste successive, come illustrato nell’esempio seguente:

```json
{
   "payload":[
      {
         "scope":"EdgeNetwork",
         "hint":"or2",
         "ttlSeconds":1800
      }
   ],
   "type":"locationHint:result"
}
```

L&#39;ambito `EdgeNetwork` contiene tutte le informazioni rilevanti necessarie all&#39;Edge Network per indirizzare di conseguenza le richieste successive. Nella risposta della richiesta iniziale e di ogni richiesta successiva alla rete Edge, sarà presente una sezione nell&#39;handle con un tipo di `locationHint:result`.

L&#39;hint associato all&#39;ambito `EdgeNetwork` può contenere uno dei seguenti valori:

* `or2`
* `va6`
* `irl1`
* `ind1`
* `jpn3`
* `sgp3`
* `aus3`

**Formato API**

Per garantire che le richieste successive vengano indirizzate correttamente, inserisci l’hint di posizione nel percorso URL delle chiamate API successive tra il percorso base, in genere `ee`, e la versione API `v2`.

```http
POST 'https://edge.adobedc.net/ee/{LOCATION_HINT}/v2/interact?dataStreamId={DataStream_ID}'
```

## Memorizzazione degli hint di posizione nei cookie {#storing-hints-in-cookies}

Per garantire che l&#39;hint di posizione restituito dall&#39;Edge Network persista per tutta la durata della sessione, è possibile memorizzare il valore dell&#39;hint di posizione in un cookie, insieme alla durata del cookie, contenuto nel campo `ttlSeconds` (in genere 1800 secondi).

Come per la maggior parte dei cookie, devi estendere la durata di questo cookie ogni volta che viene fornita una risposta dall’Edge Network. Per garantire la massima compatibilità con Web SDK, utilizzare il nome cookie `kndctr_{IMSORG}_AdobeOrg_cluster`. Gli ID organizzazione in genere terminano con `@AdobeOrg`. Il valore `@` deve essere convertito in un carattere di sottolineatura per garantire che il cookie sia nel formato corretto.
