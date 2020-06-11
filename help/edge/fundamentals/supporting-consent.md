---
title: Consenso di sostegno
seo-title: Supporto delle preferenze di consenso per l’SDK Web di Adobe Experience Platform
description: Scopri come supportare le preferenze di consenso con l’SDK Web della piattaforma Experience
seo-description: Scopri come supportare le preferenze di consenso con l’SDK Web della piattaforma Experience
translation-type: tm+mt
source-git-commit: c86ae6d887f52d8bb4b78dadc06060791c7a02c0
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 0%

---


# Consenso di supporto

Per rispettare la privacy dell&#39;utente, potrebbe essere necessario richiedere il consenso dell&#39;utente prima di consentire all&#39;SDK di utilizzare dati specifici dell&#39;utente per determinati scopi. Al momento, l’SDK consente solo agli utenti di optare per tutti gli scopi, ma in futuro Adobe spera di fornire un controllo più dettagliato su scopi specifici.

Se l’utente sceglie tutti gli scopi, l’SDK può eseguire le seguenti attività:

* Inviare dati ai server Adobe e da questi ultimi.
* Cookie di lettura e scrittura o elementi di memorizzazione Web (fatta eccezione per la persistenza delle preferenze di consenso dell&#39;utente).

Se l’utente rinuncia a tutti gli scopi, l’SDK non esegue nessuna di queste attività.

## Configurazione del consenso

Per impostazione predefinita, l’utente può accedere a tutti gli scopi. Per evitare che l’SDK esegua le attività elencate sopra fino a quando l’utente non effettua il consenso, passa `"defaultConsent": { "general": "pending" }` durante la configurazione dell’SDK come segue:

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": { "general": "pending" }
});
```

Quando il consenso predefinito per lo scopo generale è impostato su in sospeso, il tentativo di eseguire eventuali comandi che dipendono dalle preferenze di consenso dell&#39;utente (ad esempio, il `event` comando) determina la accodamento del comando nell&#39;SDK. Questi comandi non vengono elaborati finché non avrai comunicato all’SDK le preferenze di consenso dell’utente.

A questo punto, potreste preferire chiedere all&#39;utente di scegliere di effettuare il login in un punto qualsiasi dell&#39;interfaccia utente. Dopo aver raccolto le preferenze dell&#39;utente, comunica queste preferenze all&#39;SDK.

## Comunicazione delle preferenze di consenso

Se l&#39;utente sceglie di eseguire il `setConsent` comando con l&#39; `general` opzione impostata su `in` come segue:

```javascript
alloy("setConsent", {
    consent: [{ 
      standard: "Adobe",
      version: "1.0",
      value: { 
        general: "in" 
      }
    }]
});
```

Poiché l’utente ha acconsentito, l’SDK esegue tutti i comandi precedentemente in coda. I comandi futuri che dipendono dal consenso dell&#39;utente _non_ saranno messi in coda e verranno invece eseguiti immediatamente.

Se l&#39;utente sceglie di rifiutare, eseguire il `setConsent` comando con l&#39; `general` opzione impostata su `out` quanto segue:

```javascript
alloy("setConsent", {
    consent: [{ 
      standard: "Adobe",
      version: "1.0",
      value: { 
        general: "out" 
      }
    }]
});
```

>[!NOTE]
>
>Dopo che un utente ha rinunciato, l’SDK non ti consentirà di impostare il consenso degli utenti su `in`.

Poiché l&#39;utente ha scelto di non partecipare, le promesse restituite dai comandi in coda in precedenza vengono rifiutate. I comandi futuri che dipendono dal consenso dell&#39;utente, restituiranno le promesse che vengono parimenti rifiutate. Per ulteriori informazioni sulla gestione o l&#39;eliminazione degli errori, vedere [Esecuzione di comandi](executing-commands.md).

>[!NOTE]
>
>Al momento, l’SDK supporta solo lo `general` scopo. Anche se abbiamo intenzione di costruire un insieme più solido di scopi o categorie che corrisponderà alle diverse funzionalità Adobe e offerte di prodotti, l&#39;implementazione corrente è un approccio tutto o niente per l&#39;opt-in.  Questo vale solo per l’SDK Web di Adobe Experience Platform e NON per altre librerie Adobe JavaScript.

## Persistenza delle preferenze di consenso

Dopo aver comunicato le preferenze utente all’SDK tramite il `setConsent` comando, l’SDK continua a mantenere le preferenze dell’utente in un cookie. Al successivo caricamento del sito Web nel browser, l’SDK recupererà e utilizzerà le preferenze persistenti. Non è necessario eseguire di nuovo il `setConsent` comando, tranne per comunicare una modifica delle preferenze dell&#39;utente, che è possibile eseguire in qualsiasi momento.