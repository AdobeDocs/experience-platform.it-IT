---
title: Configurare Adobe Experience Platform Web SDK
description: Scoprite come configurare l’SDK Web per Adobe Experience Platform.
seo-description: 'Scopri come configurare l’SDK Web per Experienci Platform '
keywords: configurare;configurazione;SDK;edge;Web SDK;configure;edgeConfigId;context;web;device;environment;placeContext;debugEnabled;edgeDomain;orgId;clickCollectionEnabled;onBeforeEventSend;defaultConsent;web sdk settings;prehideStyle;opacity;cookieDestinationsEnabled;urlDestinationsEnabled;idMigrationEnabled;thirdParty CookiesEnabled;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 7%

---


# Configurare l’SDK Web della piattaforma

La configurazione per l&#39;SDK viene effettuata con il comando `configure`.

>[!IMPORTANT]
>
>`configure` deve  ** sempre essere il primo comando chiamato.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

È possibile impostare diverse opzioni durante la configurazione. Tutte le opzioni sono disponibili di seguito, raggruppate per categoria.

## Opzioni generali

### `edgeConfigId`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Stringa | Sì | Nessuno |

L’ID di configurazione assegnato, che collega l’SDK agli account e alla configurazione appropriati.  Quando si configurano più istanze all&#39;interno di una singola pagina, è necessario configurare un `edgeConfigId` diverso per ogni istanza.

### `context`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| ---------------- | ------------ | -------------------------------------------------- |
| Matrice di stringhe | No | `["web", "device", "environment", "placeContext"]` |

Indica quali categorie di contesto raccogliere automaticamente come descritto in [Informazioni automatiche](../data-collection/automatic-information.md).  Se questa configurazione non è specificata, per impostazione predefinita vengono utilizzate tutte le categorie.

### `debugEnabled`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Booleano | No | `false` |

Indica se il debug deve essere abilitato. L&#39;impostazione di questa configurazione su `true` abilita le seguenti funzionalità:

| **Funzione** | **Funzione** |
| ---------------------- | ------------------ |
| Convalida sincrona | Convalida i dati raccolti rispetto allo schema e restituisce un errore nella risposta sotto la seguente etichetta: `collect:error OR success` |
| Registrazione della console | Abilita la visualizzazione dei messaggi di debug nella console JavaScript del browser |

### `edgeDomain`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ------------------ |
| Stringa | No | `beta.adobedc.net` |
| Stringa | No | `omtrdc.net` |

Il dominio utilizzato per interagire con  servizi di Adobe. Questo viene utilizzato solo se si dispone di un dominio di prime parti (CNAME) che esegue il proxy delle richieste all&#39;infrastruttura periferica del Adobe .

### `orgId`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Stringa | Sì | Nessuno |

L&#39;ID organizzazione [!DNL Experience Cloud] assegnato.  Quando si configurano più istanze all&#39;interno di una pagina, è necessario configurare un `orgId` diverso per ogni istanza.

## Raccolta dati

### `clickCollectionEnabled` {#clickCollectionEnabled}

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

Indica se i dati associati ai clic del collegamento devono essere raccolti automaticamente. Per ulteriori informazioni, vedere [Tracciamento automatico dei collegamenti](../data-collection/track-links.md#automaticLinkTracking).

### `onBeforeEventSend`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Funzione | No | () => non definito |

Impostate questa opzione per configurare un callback che viene chiamato per ogni evento appena prima che venga inviato.  Un oggetto con il campo `xdm` viene inviato al callback.  Modificare l&#39;oggetto `xdm` per modificare l&#39;elemento inviato.  All&#39;interno del callback, l&#39;oggetto `xdm` avrà già i dati passati nel comando dell&#39;evento e le informazioni raccolte automaticamente. Per ulteriori informazioni sui tempi di questa callback e un esempio, vedere [Modifica di eventi globali](tracking-events.md#modifying-events-globally).

## Opzioni sulla privacy

### `defaultConsent` {#default-consent}

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Oggetto | No | `"in"` |

Imposta il consenso predefinito dell&#39;utente. Questo viene utilizzato quando non è già stata salvata alcuna preferenza di consenso per l&#39;utente. L&#39;altro valore valido è `"pending"`. Una volta impostato, il lavoro verrà messo in coda fino a quando l&#39;utente non fornirà le preferenze di consenso. Dopo aver fornito le preferenze dell&#39;utente, lavorare procede o viene interrotto in base alle preferenze dell&#39;utente. Per ulteriori informazioni, vedere [Supporto di ](../consent/supporting-consent.md).

## Opzioni di personalizzazione

### `prehidingStyle`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Stringa | No | Nessuno |

Utilizzato per creare una definizione di stile CSS che nasconde le aree contenuto della pagina Web mentre il contenuto personalizzato viene caricato dal server. Se non viene fornita questa opzione, l’SDK non tenta di nascondere alcuna area di contenuto mentre viene caricato del contenuto personalizzato, generando potenzialmente uno &quot;sfarfallio&quot;.

Ad esempio, se nella pagina Web era presente un elemento con un ID `container` il cui contenuto predefinito si desidera nascondere mentre il contenuto personalizzato viene caricato dal server, un esempio di stile di prenascondere è il seguente:

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

## Opzioni Pubblico

### `cookieDestinationsEnabled`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

Abilita le destinazioni di cookie [!DNL Audience Manager], che consentono di impostare i cookie in base alla qualifica del segmento.

### `urlDestinationsEnabled`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

Abilita le destinazioni di URL [!DNL Audience Manager], che consentono di attivare gli URL in base alla qualifica del segmento.

## Opzioni identità

### `idMigrationEnabled`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Booleano | No | true |

Se true, l’SDK leggerà e imposterà i cookie AMCV precedenti. In questo modo è possibile passare all’Adobe Experience Platform Web SDK mentre alcune parti del sito potrebbero ancora utilizzare Visitor.js. Inoltre, se nella pagina è definita l’API del visitatore, l’SDK eseguirà una query sull’API del visitatore per l’ECID. Questo consente di aggiungere due tag alle pagine con l’SDK Web AEP e di avere lo stesso ECID.

### `thirdPartyCookiesEnabled`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Booleano | No | true |

Abilita l&#39;impostazione di  cookie di terze parti di Adobe. L’SDK può mantenere l’ID visitatore in un contesto di terze parti per consentire l’utilizzo dello stesso ID visitatore nei diversi siti. Questa funzione è utile se si dispone di più siti o si desidera condividere i dati con i partner; tuttavia, a volte questo non è desiderato per motivi di privacy.
