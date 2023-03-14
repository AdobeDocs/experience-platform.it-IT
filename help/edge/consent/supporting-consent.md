---
title: Supporto delle preferenze di consenso dei clienti tramite Adobe Experience Platform Web SDK
description: Scopri come supportare le preferenze di consenso con Adobe Experience Platform Web SDK.
keywords: consenso;predefinito;consenso predefinito;setConsent;gruppo di campi Privacy dei profili;gruppo di campi Privacy degli eventi di esperienza;gruppo di campi Privacy;
exl-id: 647e4a84-4a66-45d6-8b05-d78786bca63a
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 0%

---

# Preferenze di supporto del consenso dei clienti

Per rispettare la privacy dell&#39;utente, potrebbe essere utile richiedere il consenso dell&#39;utente prima di consentire all&#39;SDK di utilizzare dati specifici dell&#39;utente per determinati scopi. Attualmente, l’SDK consente agli utenti di dare o negare il consenso a tutti gli scopi, ma in futuro Adobe spera di fornire un controllo più granulare su scopi specifici.

Se l’utente acconsente a tutte le finalità, l’SDK può eseguire le seguenti attività:

* Invia dati a e dai server di Adobe.
* Leggi e scrivi cookie o elementi di archiviazione web.

Se l’utente rinuncia a tutte le attività, l’SDK non esegue nessuna di queste attività.

## Configurazione del consenso

Per impostazione predefinita, l’utente ha acconsentito a tutti gli scopi. Per impedire che l&#39;SDK esegua le attività di cui sopra finché l&#39;utente non dà il consenso, passa `"defaultConsent": "pending"` durante la configurazione dell’SDK come segue:

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```

Quando il consenso predefinito per lo scopo generale è impostato su In sospeso, il tentativo di eseguire qualsiasi comando che dipende dalle preferenze di consenso dell’utente (ad esempio, `sendEvent` ) fa sì che il comando venga messo in coda nell&#39;SDK. Questi comandi vengono elaborati solo dopo aver comunicato le preferenze di consenso dell&#39;utente all&#39;SDK.

>[!NOTE]
>
>I comandi vengono accodati solo in memoria. Non vengono salvate nei vari caricamenti di pagina.

Se non desideri raccogliere gli eventi che si sono verificati prima che le preferenze di consenso dell&#39;utente siano impostate, puoi trasmettere `"defaultConsent": "out"` durante la configurazione SDK. Il tentativo di eseguire comandi che dipendono dalle preferenze di consenso dell&#39;utente non avrà alcun effetto finché non avrai comunicato le preferenze di consenso dell&#39;utente all&#39;SDK.

>[!NOTE]
>
>Attualmente, l’SDK supporta solo uno scopo singolo tutto o niente. Anche se prevediamo di creare una serie più solida di finalità o categorie corrispondenti alle diverse funzionalità Adobe e offerte di prodotti, l’implementazione corrente è un approccio &quot;tutto o niente&quot; all’opt-in.  Applicabile solo a Adobe Experience Platform [!DNL Web SDK] e NON altre librerie JavaScript di Adobe.

A questo punto, potrebbe essere preferibile chiedere all’utente di fornire il consenso all’interno dell’interfaccia utente. Una volta raccolte le preferenze dell&#39;utente, comunica tali preferenze all&#39;SDK.

## Comunicazione delle preferenze di consenso tramite lo standard Adobe Experience Platform

L’SDK supporta le versioni 1.0 e 2.0 dello standard di consenso Adobe Experience Platform. Attualmente, gli standard 1.0 e 2.0 supportano solo l’applicazione automatica di una preferenza di consenso &quot;tutto o niente&quot;. Lo standard 1.0 verrà gradualmente eliminato a favore dello standard 2.0. Lo standard 2.0 ti consente di aggiungere ulteriori preferenze di consenso che possono essere utilizzate per applicare manualmente le preferenze di consenso.

### Utilizzo dello standard Adobe versione 2.0

Se utilizzi Adobe Experience Platform, devi includere un gruppo di campi dello schema di privacy nello schema del profilo. Consulta [Governance, privacy e sicurezza in Adobe Experience Platform](../../landing/governance-privacy-security/overview.md) per ulteriori informazioni, consulta la versione 2.0 dello standard Adobe. Puoi aggiungere dati all’interno dell’oggetto valore seguente corrispondenti allo schema del `consents` campo del [!UICONTROL Consensi e preferenze] gruppo di campi del profilo.

Se l’utente acconsente, esegui il comando `setConsent` con la preferenza di raccolta impostata su `y` come segue:

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

Il campo dell’ora deve specificare quando l’utente ha aggiornato per l’ultima volta le preferenze di consenso. Se l’utente sceglie di rinunciare, esegui la `setConsent` con la preferenza di raccolta impostata su `n` come segue:

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

### Utilizzo dello standard Adobe versione 1.0

Se l’utente acconsente, esegui il comando `setConsent` comando con `general` opzione impostata su `in` come segue:

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

Se l’utente sceglie di rinunciare, esegui la `setConsent` comando con `general` opzione impostata su `out` come segue:

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

L&#39;SDK supporta la registrazione delle preferenze di consenso di un utente fornite tramite lo standard Interactive Advertising Bureau Europe (IAB) Transparency and Consent Framework (TCF). La stringa di consenso può essere impostata tramite lo stesso `setConsent` come sopra, come segue:

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

Se il consenso è impostato in questo modo, Real-Time Customer Profile viene aggiornato con le informazioni sul consenso. Affinché ciò funzioni, lo schema XDM del profilo deve contenere [Gruppo di campi schema privacy profilo](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md). Durante l’invio di eventi, le informazioni sul consenso IAB devono essere aggiunte manualmente all’oggetto XDM dell’evento. L’SDK non include automaticamente le informazioni sul consenso negli eventi. Per inviare le informazioni sul consenso negli eventi, è necessario che [Gruppo di campi Privacy evento esperienza](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/experience-event/experienceevent-privacy.schema.md) deve essere aggiunto allo schema Experience Event.

## Invio di più standard in una richiesta

L’SDK supporta anche l’invio di più oggetti di consenso in una richiesta.

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

Dopo aver comunicato le preferenze dell’utente all’SDK utilizzando `setConsent` , l&#39;SDK salva le preferenze dell&#39;utente in un cookie. La prossima volta che l’utente carica il sito web nel browser, l’SDK recupererà e utilizzerà queste preferenze persistenti per determinare se gli eventi possono essere inviati o meno a Adobe.

Per visualizzare la finestra di dialogo di consenso con le preferenze correnti, è necessario memorizzare le preferenze utente in modo indipendente. Non è possibile recuperare le preferenze utente dall’SDK. Per fare in modo che le preferenze utente rimangano sincronizzate con l&#39;SDK, puoi chiamare il `setConsent` a ogni caricamento di pagina. L’SDK effettua una chiamata al server solo se le preferenze sono cambiate.

## Sincronizzazione delle identità durante la configurazione del consenso

Quando il consenso predefinito è in sospeso o in uscita, il `setConsent` potrebbe essere la prima richiesta che viene rilasciata e stabilisce l’identità. Per questo motivo, potrebbe essere importante sincronizzare le identità alla prima richiesta. È possibile aggiungere la mappa delle identità a `setConsent` comando come nel `sendEvent` comando. Consulta [Recupero ID Experience Cloud](../identity/overview.md)
