---
title: Suggerimenti sulla posizione
description: Questo articolo spiega come funzionano i suggerimenti sulla posizione nell’API di Edge Network Server, in modo che le richieste degli utenti finali possano sempre essere indirizzate allo stesso server.
source-git-commit: 7f1d8fba34c5478f0d6e727a5a52af642852c9dd
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---


# Suggerimenti sulla posizione

## Panoramica {#overview}

La [!DNL Adobe Experience Platform Edge Network] utilizza diversi server distribuiti a livello globale per garantire tempi di risposta rapidi indipendentemente dalla posizione dell&#39;utente finale. Utilizza inoltre il routing basato su DNS per garantire che le richieste siano sempre indirizzate al percorso della rete Edge più vicino agli utenti finali.

Se gli utenti finali si connettono a una VPN o passano i tipi di rete sui loro dispositivi mobili nel corso di una sessione, le richieste di rete Edge possono spesso essere indirizzate a una posizione diversa. Il routing a mezza sessione tra server può essere problematico, in quanto le soluzioni Adobe Experience Platform e Adobe Experience Cloud memorizzano informazioni sul profilo utente finale sulla rete Edge.

Qui è dove entrano in gioco i suggerimenti sulla posizione.

Per garantire che gli utenti finali interagiscano sempre con il server regionale di Edge Network contenente i dati di profilo correnti, la funzionalità dei suggerimenti di posizione assicura che tutte le richieste alla rete Edge vengano inviate allo stesso server in cui è stata effettuata la prima richiesta di una sessione. Questo consente agli utenti di avere un’esperienza coerente, indipendentemente dalle modifiche alla rete che possono apportare durante una sessione.

## Utilizzo degli hint posizione

Gli hint di posizione sono inclusi nella risposta della richiesta Edge Network iniziale e in tutte le richieste successive, come mostrato nell’esempio seguente:

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

La `EdgeNetwork` l’ambito contiene tutte le informazioni pertinenti necessarie a Edge Network per instradare di conseguenza le richieste successive. Nella risposta della richiesta iniziale e successiva alla rete Edge, sarà presente una sezione nel handle con un tipo di `locationHint:result`.

Il suggerimento associato al `EdgeNetwork` l&#39;ambito può contenere uno dei seguenti valori:

* `or2`
* `va6`
* `irl1`
* `ind1`
* `jpn3`
* `sgp3`
* `aus3`

**Formato API**

Per garantire che le richieste successive vengano instradate correttamente, inserisci il suggerimento di posizione nel percorso URL delle chiamate API successive tra il percorso di base, in genere `ee`e `v2` Versione API.

```http
POST 'https://edge.adobedc.net/ee/{LOCATION_HINT}/v2/interact?dataStreamId={DataStream_ID}'
```

## Memorizzazione di suggerimenti sulla posizione nei cookie {#storing-hints-in-cookies}

Per garantire che l’hint di posizione restituito da Edge Network persista per la durata della sessione, è possibile memorizzare il valore dell’hint di posizione in un cookie, insieme alla durata del cookie, contenuta in `ttlSeconds` (generalmente 1800 secondi).

Come per la maggior parte dei cookie, è necessario estendere la durata di questo cookie ogni volta che si riceve una risposta da Edge Network. Per garantire la massima compatibilità con l&#39;SDK web, utilizza il nome del cookie `kndctr_{IMSORG}_AdobeOrg_cluster`. Gli ID organizzazione IMS generalmente terminano con `@AdobeOrg`. La `@` deve essere convertito in carattere di sottolineatura per garantire che il cookie sia nel formato corretto.
