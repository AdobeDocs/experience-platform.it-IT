---
title: Supporto delle preferenze di consenso dei clienti tramite Adobe Experience Platform Web SDK
description: Scoprite come supportare le preferenze di consenso con Adobe Experience Platform Web SDK.
keywords: consenso;consenso predefinito;consenso predefinito;setConsent;Profile Privacy Mixin;Experience Event Privacy Mixin;Privacy Mixin;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 0%

---


# Supporto delle preferenze di consenso dei clienti

Per rispettare la privacy dell&#39;utente, potrebbe essere necessario richiedere il consenso dell&#39;utente prima di consentire all&#39;SDK di utilizzare dati specifici dell&#39;utente per determinati scopi. Al momento, l’SDK consente solo agli utenti di optare per tutti gli scopi, ma in futuro  Adobe spera di fornire un controllo più dettagliato su scopi specifici.

Se l’utente sceglie tutti gli scopi, l’SDK può eseguire le seguenti attività:

* Inviare dati a e da  server  Adobi.
* Cookie di lettura e scrittura o elementi di memorizzazione Web (fatta eccezione per la persistenza delle preferenze di consenso dell&#39;utente).

Se l’utente rinuncia a tutti gli scopi, l’SDK non esegue nessuna di queste attività.

## Configurazione del consenso

Per impostazione predefinita, l’utente può accedere a tutti gli scopi. Per evitare che l&#39;SDK esegua le attività descritte sopra fino a quando l&#39;utente non effettua l&#39;accesso, passa `"defaultConsent": "pending"` durante la configurazione dell&#39;SDK come segue:

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```

Quando il consenso predefinito per lo scopo generale è impostato su in sospeso, il tentativo di eseguire qualsiasi comando che dipenda dalle preferenze di consenso dell&#39;utente (ad esempio, il comando `event`) determina la accodamento del comando nell&#39;SDK. Questi comandi non vengono elaborati finché non avrai comunicato all’SDK le preferenze di consenso dell’utente.

A questo punto, potreste preferire chiedere all&#39;utente di scegliere di effettuare il login in un punto qualsiasi dell&#39;interfaccia utente. Dopo aver raccolto le preferenze dell&#39;utente, comunica queste preferenze all&#39;SDK.

## Comunicazione delle preferenze di consenso tramite  Adobe Standard

Se l&#39;utente sceglie, eseguire il comando `setConsent` con l&#39;opzione `general` impostata su `in` come segue:

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

Poiché l’utente ha acconsentito, l’SDK esegue tutti i comandi precedentemente in coda. I comandi futuri che dipendono dal consenso dell&#39;utente non saranno messi in coda e verranno invece eseguiti immediatamente.

Se l&#39;utente sceglie di rifiutare, eseguire il comando `setConsent` con l&#39;opzione `general` impostata su `out` come segue:

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
>Dopo che un utente ha rinunciato, l&#39;SDK non ti permetterà di impostare il consenso degli utenti su `in`.

Poiché l&#39;utente ha scelto di non partecipare, le promesse restituite dai comandi in coda in precedenza vengono rifiutate. I comandi futuri che dipendono dal consenso dell&#39;utente, restituiranno le promesse che vengono parimenti rifiutate. Per ulteriori informazioni sulla gestione o l&#39;eliminazione degli errori, fare riferimento a [Esecuzione di comandi](../fundamentals/executing-commands.md).

>[!NOTE]
>
>Al momento, l&#39;SDK supporta solo lo scopo `general`. Anche se abbiamo intenzione di costruire una serie più solida di scopi o categorie che corrisponderanno alle diverse funzionalità del Adobe  e alle offerte di prodotti, l&#39;implementazione corrente è un approccio tutto o niente per l&#39;opt-in.  Ciò vale solo per le librerie JavaScript di Adobe Experience Platform [!DNL Web SDK] e NON  altri Adobi.

## Comunicazione delle preferenze di consenso tramite lo standard IAB TCF

L&#39;SDK supporta la registrazione delle preferenze di consenso dell&#39;utente fornite tramite lo standard IAB (Interactive Advertising Bureau Europe) Transparency and Consent Framework (TCF). La stringa di consenso può essere impostata tramite lo stesso comando `setConsent` come sopra:

```javascript
alloy("setConsent", {
    consent: [{
      standard: "IAB TCF",
      version: "2.0",
      value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
      gdprApplies: true
    }]
});
```

Quando il consenso è impostato in questo modo, il profilo cliente in tempo reale viene aggiornato con le informazioni sul consenso. Affinché questo funzioni, lo schema XDM del profilo deve contenere il [Mixin della privacy del profilo](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md). Quando si inviano eventi, le informazioni di consenso IAB devono essere aggiunte manualmente all&#39;oggetto XDM dell&#39;evento. L&#39;SDK non include automaticamente le informazioni sul consenso negli eventi. Per inviare le informazioni di consenso negli eventi, è necessario aggiungere allo schema dell&#39;evento esperienza [Experience Event Privacy Mixin](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/experience-event/experienceevent-privacy.schema.md).

## Invio di entrambi gli standard in un&#39;unica richiesta

L’SDK supporta inoltre l’invio di più oggetti di consenso in una richiesta.

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "1.0",
      value: {
        general: "in"
      }
    },{
      standard: "IAB TCF",
      version: "2.0",
      value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
      gdprApplies: true
    }]
});
```

## Persistenza delle preferenze di consenso

Dopo aver comunicato le preferenze dell&#39;utente all&#39;SDK utilizzando il comando `setConsent`, l&#39;SDK continua a mantenere le preferenze dell&#39;utente su un cookie. La volta successiva che l’utente carica il sito Web nel browser, l’SDK recupererà e utilizzerà queste preferenze persistenti per determinare se gli eventi possono essere inviati o meno al Adobe . Non è necessario eseguire nuovamente il comando `setConsent`, tranne per comunicare una modifica nelle preferenze dell&#39;utente, che è possibile eseguire in qualsiasi momento.

## Sincronizzazione delle identità durante l&#39;impostazione del consenso

Quando il consenso predefinito è in sospeso, la `setConsent` potrebbe essere la prima richiesta che esce e stabilisce l&#39;identità. Per questo motivo, potrebbe essere importante sincronizzare le identità sulla prima richiesta. La mappa identità può essere aggiunta al comando `setConsent` proprio come nel comando `sendEvent`. Vedere [Recupero  ID Experience Cloud](../identity/overview.md)

