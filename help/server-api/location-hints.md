---
title: Hint posizione
description: Questo articolo spiega come funzionano gli hint di posizione nell’API del server di rete Edge, in modo che le richieste degli utenti finali possano sempre essere instradate allo stesso server.
exl-id: 8cd2f8e2-2065-4b7e-8d35-4ed1a716f1b3
source-git-commit: 80c527ab3c82e01fe19e5003e224d63e79b23bdc
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# Hint posizione

## Panoramica {#overview}

Il [!DNL Adobe Experience Platform Edge Network] utilizza diversi server distribuiti a livello globale per garantire tempi di risposta rapidi, indipendentemente dalla posizione dell&#39;utente finale. Utilizza inoltre il routing basato su DNS per garantire che le richieste vengano sempre instradate alla posizione di rete Edge più vicina agli utenti finali.

Se gli utenti finali si connettono a una VPN o cambiano tipi di rete sui loro dispositivi mobili nel corso di una sessione, le richieste di rete Edge possono spesso essere indirizzate a una posizione diversa. Il routing a metà sessione tra server può essere problematico, in quanto le soluzioni Adobe Experience Platform e Adobe Experience Cloud memorizzano le informazioni sul profilo utente finale sulla rete Edge.

Qui entrano in gioco gli hint di posizione.

Per garantire che gli utenti finali interagiscano sempre con il server regionale della rete Edge che contiene i dati del profilo corrente, la funzionalità degli hint di posizione garantisce che tutte le richieste alla rete Edge vengano inviate allo stesso server in cui è stata effettuata la prima richiesta di una sessione. Questo consente agli utenti di avere un’esperienza coerente, indipendentemente dalle modifiche di rete che potrebbero subire nel corso di una sessione.

## Utilizzo degli hint di posizione

Gli hint di posizione sono inclusi nella risposta della richiesta iniziale di Edge Network e in tutte le richieste successive, come illustrato nell’esempio seguente:

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

Il `EdgeNetwork` l’ambito contiene tutte le informazioni pertinenti necessarie alla rete Edge per indirizzare di conseguenza le richieste successive. Nella risposta della richiesta iniziale e di ogni richiesta successiva alla rete Edge, nell’handle sarà presente una sezione con un tipo di `locationHint:result`.

Suggerimento associato a `EdgeNetwork` l&#39;ambito può contenere uno dei seguenti valori:

* `or2`
* `va6`
* `irl1`
* `ind1`
* `jpn3`
* `sgp3`
* `aus3`

**Formato API**

Per garantire che le richieste successive vengano indirizzate correttamente, inserisci l’hint di posizione nel percorso URL delle chiamate API successive tra il percorso base, in genere `ee`, e `v2` Versione API.

```http
POST 'https://edge.adobedc.net/ee/{LOCATION_HINT}/v2/interact?dataStreamId={DataStream_ID}'
```

## Memorizzazione degli hint di posizione nei cookie {#storing-hints-in-cookies}

Per garantire che l’hint di posizione restituito dalla rete Edge persista per la durata della sessione, puoi memorizzarne il valore in un cookie, insieme alla durata del cookie, contenuta nel `ttlSeconds` (in genere 1800 secondi).

Come per la maggior parte dei cookie, è necessario estendere la durata di questo cookie ogni volta che viene inviata una risposta da Edge Network. Per garantire la massima compatibilità con Web SDK, utilizza il nome del cookie `kndctr_{IMSORG}_AdobeOrg_cluster`. Gli ID organizzazione IMS in genere terminano con `@AdobeOrg`. Il `@` il valore deve essere convertito in un carattere di sottolineatura per garantire che il cookie sia nel formato corretto.
