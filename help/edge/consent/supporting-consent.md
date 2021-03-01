---
title: Supporto delle preferenze di consenso dei clienti tramite l’SDK per web di Adobe Experience Platform
description: Scopri come supportare le preferenze di consenso con l’SDK web di Adobe Experience Platform.
keywords: consenso;consenso predefinito;consenso predefinito;setConsent;Mixin privacy profilo;Mixin privacy evento esperienza;Mixin privacy privacy Privacy;
translation-type: tm+mt
source-git-commit: 308c10eb0d1f78dad2b8b6158f28d0384a65c78c
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 0%

---


# Supporto delle preferenze di consenso dei clienti

Per rispettare la privacy dell&#39;utente, prima di consentire all&#39;SDK di utilizzare dati specifici per determinati scopi, potrebbe essere necessario chiedere il consenso dell&#39;utente. Al momento, l’SDK consente agli utenti di effettuare o meno l’opt-in, ma in futuro Adobe spera di fornire un controllo più granulare su finalità specifiche.

Se l&#39;utente effettua il consenso a tutti gli scopi, l&#39;SDK può eseguire le seguenti attività:

* Inviare dati ai server Adobe e da tali server.
* Lettura e scrittura di cookie o elementi di archiviazione Web.

Se l&#39;utente rinuncia a tutti gli scopi, l&#39;SDK non esegue nessuna di queste attività.

## Configurazione del consenso

Per impostazione predefinita, l’utente ha acconsentito a tutti gli scopi. Per impedire all&#39;SDK di eseguire le attività di cui sopra fino a quando l&#39;utente non effettua il consenso, passa `"defaultConsent": "pending"` durante la configurazione dell&#39;SDK come segue:

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```

Quando il consenso predefinito per lo scopo generale è impostato su in sospeso, il tentativo di eseguire i comandi che dipendono dalle preferenze di consenso dell&#39;utente (ad esempio, il comando `event`) determina la messa in coda del comando all&#39;interno dell&#39;SDK. Questi comandi non vengono elaborati finché non avrai comunicato le preferenze di consenso dell&#39;utente all&#39;SDK.

A questo punto, potresti preferire chiedere all’utente di effettuare il consenso da qualche parte all’interno dell’interfaccia utente. Dopo aver raccolto le preferenze dell&#39;utente, comunica queste preferenze all&#39;SDK.

## Comunicazione delle preferenze di consenso tramite Adobe Standard

Se l&#39;utente effettua il consenso, esegui il comando `setConsent` con l&#39;opzione `general` impostata su `in` come segue:

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

Poiché l’utente ha ora acconsentito, l’SDK esegue tutti i comandi in coda in precedenza. I comandi futuri che dipendono dal consenso dell’utente non verranno messi in coda e verranno invece eseguiti immediatamente.

Se l&#39;utente sceglie di rinunciare, eseguire il comando `setConsent` con l&#39;opzione `general` impostata su `out` come segue:

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
>Dopo che un utente ha rinunciato, l&#39;SDK non ti consente di impostare il consenso degli utenti su `in`.

Poiché l’utente ha scelto di rinunciare, le promesse restituite dai comandi in coda in precedenza vengono rifiutate. I comandi futuri che dipendono dal consenso dell&#39;utente restituiranno promesse che sono state rifiutate in modo simile. Per ulteriori informazioni sulla gestione o l&#39;eliminazione degli errori, fare riferimento a [Comandi di esecuzione](../fundamentals/executing-commands.md).

>[!NOTE]
>
>Attualmente, l&#39;SDK supporta solo lo scopo `general`. Anche se prevediamo di creare un set più solido di finalità o categorie che corrisponderanno alle diverse funzionalità e offerte di prodotti Adobe, l’implementazione corrente è un approccio totalmente o nulla all’opt-in.  Questo vale solo per Adobe Experience Platform [!DNL Web SDK] e NON per altre librerie JavaScript di Adobe.

## Comunicazione delle preferenze di consenso tramite lo standard IAB TCF

L’SDK supporta la registrazione delle preferenze di consenso dell’utente fornite tramite lo standard IAB (Interactive Advertising Bureau Europe) Transparency and Consent Framework (TCF) . La stringa di consenso può essere impostata tramite lo stesso comando `setConsent` come sopra:

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

Quando il consenso è impostato in questo modo, il Profilo del cliente in tempo reale viene aggiornato con le informazioni sul consenso. Affinché questo funzioni, lo schema XDM del profilo deve contenere il [Mixin privacy profilo](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md). Quando si inviano eventi, le informazioni di consenso IAB devono essere aggiunte manualmente all’oggetto XDM dell’evento. L’SDK non include automaticamente le informazioni sul consenso negli eventi. Per inviare le informazioni sul consenso negli eventi, è necessario aggiungere [Experience Event Privacy Mixin](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/experience-event/experienceevent-privacy.schema.md) allo schema Experience Event (Evento esperienza).

## Invio di entrambi gli standard in una richiesta

L&#39;SDK supporta anche l&#39;invio di più di un oggetto di consenso in una richiesta.

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

Dopo aver comunicato le preferenze utente all&#39;SDK utilizzando il comando `setConsent` , l&#39;SDK continua a mantenere le preferenze dell&#39;utente in un cookie. La prossima volta che l’utente carica il sito web nel browser, l’SDK recupererà e utilizzerà queste preferenze persistenti per determinare se gli eventi possono essere inviati ad Adobe. Non è necessario eseguire nuovamente il comando `setConsent`, ad eccezione di comunicare una modifica nelle preferenze dell&#39;utente, operazione che è possibile eseguire in qualsiasi momento.

## Sincronizzazione delle identità durante l&#39;impostazione del consenso

Quando il consenso predefinito è in sospeso, la `setConsent` può essere la prima richiesta che viene effettuata e stabilisce l&#39;identità. Per questo motivo, potrebbe essere importante sincronizzare le identità sulla prima richiesta. È possibile aggiungere la mappa di identità al comando `setConsent` come nel comando `sendEvent`. Consulta [Recupero Experience Cloud ID](../identity/overview.md)

