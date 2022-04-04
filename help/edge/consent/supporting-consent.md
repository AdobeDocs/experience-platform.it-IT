---
title: Supporto delle preferenze di consenso dei clienti tramite Adobe Experience Platform Web SDK
description: Scopri come supportare le preferenze di consenso con Adobe Experience Platform Web SDK.
keywords: consenso;consenso predefinito;consenso predefinito;setConsent;gruppo di campi Privacy profilo;gruppo di campi Privacy evento esperienza;gruppo di campi Privacy;
exl-id: 647e4a84-4a66-45d6-8b05-d78786bca63a
source-git-commit: 16c8972333fa67fa2e308445f4ad6282510370d1
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 0%

---

# Supporto delle preferenze di consenso dei clienti

Per rispettare la privacy dell&#39;utente, prima di consentire all&#39;SDK di utilizzare dati specifici per determinati scopi, potrebbe essere necessario chiedere il consenso dell&#39;utente. Attualmente, l’SDK consente agli utenti di effettuare o meno il consenso o meno a tutti gli scopi, ma in futuro spera di fornire un controllo più granulare su finalità specifiche.

Se l&#39;utente effettua il consenso a tutti gli scopi, l&#39;SDK può eseguire le seguenti attività:

* Inviare dati ai server di Adobe e da tali server.
* Lettura e scrittura di cookie o elementi di archiviazione Web.

Se l&#39;utente rinuncia a tutti gli scopi, l&#39;SDK non esegue nessuna di queste attività.

## Configurazione del consenso

Per impostazione predefinita, l’utente ha acconsentito a tutti gli scopi. Per impedire all&#39;SDK di eseguire le attività di cui sopra fino a quando l&#39;utente non effettua il consenso, passa `"defaultConsent": "pending"` durante la configurazione dell’SDK, come segue:

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```

Quando il consenso predefinito per lo scopo generale è impostato su in sospeso, tenta di eseguire tutti i comandi che dipendono dalle preferenze di consenso dell&#39;utente (ad esempio, il `sendEvent` restituisce il comando in coda all&#39;interno dell&#39;SDK. Questi comandi non vengono elaborati finché non avrai comunicato le preferenze di consenso dell&#39;utente all&#39;SDK.

>[!NOTE]
>
>I comandi vengono messi in coda solo in memoria. Non vengono salvate tra i caricamenti di pagina.

Se non desideri raccogliere gli eventi che si sono verificati prima dell&#39;impostazione delle preferenze di consenso dell&#39;utente, puoi passare `"defaultConsent": "out"` durante la configurazione dell&#39;SDK. Il tentativo di eseguire qualsiasi comando che dipende dalle preferenze di consenso dell&#39;utente non avrà alcun effetto finché non avrai comunicato le preferenze di consenso dell&#39;utente all&#39;SDK.

>[!NOTE]
>
>Al momento, l&#39;SDK supporta solo una singola funzione completa o nulla. Anche se prevediamo di creare un set più solido di finalità o categorie che corrisponderanno alle diverse funzionalità di Adobe e alle diverse offerte di prodotti, l’implementazione corrente è un approccio totalmente o nulla all’opt-in.  Questo vale solo per Adobe Experience Platform [!DNL Web SDK] e NON altre librerie JavaScript di Adobe.

A questo punto, potresti preferire chiedere all’utente di effettuare il consenso da qualche parte all’interno dell’interfaccia utente. Dopo aver raccolto le preferenze dell&#39;utente, comunica queste preferenze all&#39;SDK.

## Comunicazione delle preferenze di consenso tramite lo standard Adobe Experience Platform

L’SDK supporta le versioni 1.0 e 2.0 dello standard di consenso Adobe Experience Platform. Attualmente, gli standard 1.0 e 2.0 supportano solo l&#39;applicazione automatica di una preferenza di consenso totale o nulla. Lo standard 1.0 viene gradualmente eliminato a favore dello standard 2.0. Lo standard 2.0 ti consente di aggiungere preferenze di consenso aggiuntive che possono essere utilizzate per applicare manualmente le preferenze di consenso.

### Utilizzo della versione standard di Adobe 2.0

Se utilizzi Adobe Experience Platform, dovrai includere un gruppo di campi dello schema di privacy nello schema del profilo. Vedi [Governance, privacy e sicurezza in Adobe Experience Platform](../../landing/governance-privacy-security/overview.md) per ulteriori informazioni su Adobe standard versione 2.0. È possibile aggiungere dati all&#39;interno dell&#39;oggetto value corrispondente allo schema del `consents` campo [!UICONTROL Consensi e preferenze] gruppo di campi del profilo.

Se l&#39;utente effettua il consenso, esegui la `setConsent` con la preferenza di raccolta impostata su `y` come segue:

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: {
        collect: {
          val: "y"
        },
        metadata: {
          time: "2021-03-17T15:48:42-07:00"
        }
      }
    }]
});
```

Il campo temporale deve specificare l’ultima volta che l’utente ha aggiornato le proprie preferenze di consenso. Se l&#39;utente sceglie di rinunciare, esegui la `setConsent` con la preferenza di raccolta impostata su `n` come segue:

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: {
        collect: {
          val: "n"
        },
        metadata: {
          time: "2021-03-17T15:51:30-07:00"
        }
      }
    }]
});
```

### Utilizzo della versione standard di Adobe 1.0

Se l&#39;utente effettua il consenso, esegui la `setConsent` con il comando `general` opzione impostata su `in` come segue:

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

Se l&#39;utente sceglie di rinunciare, esegui la `setConsent` con il comando `general` opzione impostata su `out` come segue:

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

## Comunicazione delle preferenze di consenso tramite lo standard IAB TCF

L’SDK supporta la registrazione delle preferenze di consenso dell’utente fornite tramite lo standard IAB (Interactive Advertising Bureau Europe) Transparency and Consent Framework (TCF) . La stringa di consenso può essere impostata attraverso la stessa `setConsent` come sopra:

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

Quando il consenso è impostato in questo modo, il Profilo del cliente in tempo reale viene aggiornato con le informazioni sul consenso. Affinché questo funzioni, lo schema XDM del profilo deve contenere [Gruppo di campi dello schema Privacy del profilo](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md). Quando si inviano eventi, le informazioni di consenso IAB devono essere aggiunte manualmente all’oggetto XDM dell’evento. L’SDK non include automaticamente le informazioni sul consenso negli eventi. Per inviare le informazioni sul consenso negli eventi, la [Gruppo di campi Privacy degli eventi di esperienza](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/experience-event/experienceevent-privacy.schema.md) deve essere aggiunto allo schema Experience Event (Evento esperienza).

## Invio di più standard in una richiesta

L&#39;SDK supporta anche l&#39;invio di più di un oggetto di consenso in una richiesta.

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: {
        collect: {
          val: "y"
        },
        metadata: {
          time: "2021-03-17T15:48:42-07:00"
        }
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

Dopo aver comunicato le preferenze dell&#39;utente all&#39;SDK utilizzando `setConsent` L&#39;SDK persiste nelle preferenze dell&#39;utente a un cookie. La prossima volta che l’utente carica il tuo sito web nel browser, l’SDK recupererà e utilizzerà queste preferenze persistenti per determinare se gli eventi possono essere inviati ad Adobe.

Sarà necessario memorizzare le preferenze utente in modo indipendente per poter visualizzare la finestra di dialogo di consenso con le preferenze correnti. Non c&#39;è modo di recuperare le preferenze utente dall&#39;SDK. Per assicurarti che le preferenze utente rimangano sincronizzate con l&#39;SDK, puoi chiamare il `setConsent` a ogni caricamento di pagina. L&#39;SDK effettuerà una chiamata al server solo se le preferenze sono cambiate.

## Sincronizzazione delle identità durante l&#39;impostazione del consenso

Quando il consenso predefinito è in sospeso o in uscita, la `setConsent` può essere la prima richiesta che esce e stabilisce l&#39;identità. Per questo motivo, potrebbe essere importante sincronizzare le identità sulla prima richiesta. È possibile aggiungere la mappa di identità a `setConsent` come sul comando `sendEvent` comando. Vedi [Recupero ID Experience Cloud](../identity/overview.md)
