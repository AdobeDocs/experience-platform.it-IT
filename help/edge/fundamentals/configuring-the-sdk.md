---
title: Configurare Adobe Experience Platform Web SDK
description: Scopri come configurare Adobe Experience Platform Web SDK.
seo-description: Scopri come configurare Experience Platform Web SDK
keywords: configurare;configurazione;SDK;edge;Web SDK;configurare;edgeConfigId;contesto;web;dispositivo;ambiente;placeContext;debugEnabled;edgeDomain;orgId;clickCollectionEnabled;onBeforeEventSend;defaultConsent;impostazioni sdk web;prehidingStyle;opacity;cookieDestinationsEnabled;urlDestinationsEnabled;idMigrationEnabled;thirdPartyParty CookiesEnabled;
translation-type: tm+mt
source-git-commit: f78da58ba7a593d9c161030833d9b69e2ba57c9a
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 7%

---


# Configurare l’SDK web per Platform

La configurazione dell’SDK viene eseguita con il comando `configure` .

>[!IMPORTANT]
>
>`configure` deve  ** sempre essere il primo comando chiamato.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

È possibile impostare molte opzioni durante la configurazione. Di seguito sono riportate tutte le opzioni, raggruppate per categoria.

## Opzioni generali

### `edgeConfigId`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Stringa | Sì | Nessuno |

L&#39;ID di configurazione assegnato, che collega l&#39;SDK agli account e alla configurazione appropriati.  Quando configuri più istanze all’interno di una singola pagina, devi configurare un `edgeConfigId` diverso per ogni istanza.

### `context`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| ---------------- | ------------ | -------------------------------------------------- |
| Array di stringhe | No | `["web", "device", "environment", "placeContext"]` |

Indica le categorie di contesto da raccogliere automaticamente come descritto in [Informazioni automatiche](../data-collection/automatic-information.md).  Se questa configurazione non è specificata, tutte le categorie vengono utilizzate per impostazione predefinita.

### `debugEnabled`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Booleano | No | `false` |

Indica se il debug deve essere abilitato. L&#39;impostazione di questa configurazione su `true` abilita le seguenti funzionalità:

| **Funzione** | **Funzione** |
| ---------------------- | ------------------ |
| Convalida sincrona | Convalida i dati raccolti rispetto allo schema e restituisce un errore nella risposta sotto la seguente etichetta: `collect:error OR success` |
| Registrazione della console | Abilita la visualizzazione dei messaggi di debug nella console JavaScript del browser |

### `edgeDomain` {#edge-domain}

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ------------------ |
| Stringa | No | `beta.adobedc.net` |
| Stringa | No | `omtrdc.net` |

Dominio utilizzato per interagire con i servizi Adobe. Viene utilizzato solo se disponi di un dominio di prima parte (CNAME) che esegue il proxy delle richieste all’infrastruttura Edge di Adobe.

### `orgId`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Stringa | Sì | Nessuno |

L&#39;ID organizzazione [!DNL Experience Cloud] assegnato.  Quando configuri più istanze all’interno di una pagina, devi configurare un `orgId` diverso per ogni istanza.

## Raccolta dati

### `clickCollectionEnabled` {#clickCollectionEnabled}

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

Indica se i dati associati ai clic sul collegamento devono essere raccolti automaticamente. Per ulteriori informazioni, consulta [Tracciamento automatico dei collegamenti](../data-collection/track-links.md#automaticLinkTracking) .

### `onBeforeEventSend`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Funzione | No | () => non definito |

Imposta questa opzione per configurare un callback chiamato per ogni evento immediatamente prima dell’invio.  Un oggetto con il campo `xdm` viene inviato al callback.  Modificare l&#39;oggetto `xdm` per modificare l&#39;invio.  All&#39;interno del callback, l&#39;oggetto `xdm` avrà già i dati passati nel comando evento e le informazioni raccolte automaticamente. Per ulteriori informazioni sulla tempistica di questo callback e un esempio, vedere [Modifica degli eventi a livello globale](tracking-events.md#modifying-events-globally).

## Opzioni privacy

### `defaultConsent` {#default-consent}

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Oggetto | No | `"in"` |

Imposta il consenso predefinito dell’utente. Questa opzione viene utilizzata quando non è già stata salvata alcuna preferenza di consenso per l’utente. Gli altri valori validi sono `"pending"` e `"out"`. Questo valore predefinito non viene mantenuto nel profilo dell’utente. Solo quando viene chiamato setConsent il profilo dell&#39;utente viene aggiornato.
* `"in"`: Quando questo viene impostato o non viene fornito alcun valore, il lavoro procede senza le preferenze di consenso dell&#39;utente.
* `"pending"`: Una volta impostato, il lavoro verrà messo in coda fino a quando l&#39;utente non fornirà le preferenze di consenso.
* `"out"`: Una volta impostato, il lavoro verrà scartato finché l&#39;utente non fornirà le preferenze di consenso.
Dopo aver fornito le preferenze dell&#39;utente, lavorare procede o viene interrotto in base alle preferenze dell&#39;utente. Per ulteriori informazioni, consulta [Supporto del consenso](../consent/supporting-consent.md) .

## Opzioni di personalizzazione

### `prehidingStyle`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Stringa | No | Nessuno |

Utilizzato per creare una definizione di stile CSS che nasconde le aree contenuto della pagina web mentre il contenuto personalizzato viene caricato dal server. Se non viene fornita questa opzione, l’SDK non tenta di nascondere alcuna area di contenuto durante il caricamento del contenuto personalizzato, generando potenzialmente una visualizzazione momentanea di altri contenuti.

Ad esempio, se sulla pagina web era presente un elemento con un ID `container` il cui contenuto predefinito si desidera nascondere durante il caricamento del contenuto personalizzato dal server, un esempio di stile di pre-hiding sarebbe il seguente:

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

## Opzioni del pubblico

### `cookieDestinationsEnabled`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

Abilita le destinazioni dei cookie [!DNL Audience Manager], che consentono di impostare cookie in base alla qualifica del segmento.

### `urlDestinationsEnabled`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

Abilita le destinazioni URL [!DNL Audience Manager], che consentono di attivare gli URL in base alla qualifica del segmento.

## Opzioni di identità

### `idMigrationEnabled` {#id-migration-enabled}

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Booleano | No | true |

Se true, l’SDK legge e imposta i cookie AMCV precedenti. Questo aiuta nella transizione all&#39;utilizzo di Adobe Experience Platform Web SDK mentre alcune parti del sito potrebbero ancora utilizzare Visitor.js. Inoltre, se nella pagina è definita l’API visitatore, l’SDK eseguirà una query sull’API visitatore per l’ECID. Questo consente di utilizzare due pagine di tag con Adobe Experience Platform Web SDK e di disporre comunque dello stesso ECID.

### `thirdPartyCookiesEnabled`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Booleano | No | true |

Abilita l’impostazione di cookie di terze parti di Adobe. L’SDK può mantenere l’ID visitatore in un contesto di terze parti per consentire l’utilizzo dello stesso ID visitatore nei diversi siti. Questa funzione è utile se disponi di più siti o se desideri condividere dati con i partner; tuttavia, a volte questo non è desiderato per motivi di privacy.
