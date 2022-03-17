---
title: Configurare Adobe Experience Platform Web SDK
description: Scopri come configurare Adobe Experience Platform Web SDK.
seo-description: Learn how to configure the Experience Platform Web SDK
keywords: configurare;configurazione;SDK;edge;Web SDK;configurare;edgeConfigId;contesto;web;dispositivo;ambiente;placeContext;debugEnabled;edgeDomain;orgId;clickCollectionEnabled;onBeforeEventSend;defaultConsent;impostazioni sdk web;prehidingStyle;opacity;cookieDestinationsEnabled;urlDestinationsEnabled;idMigrationEnabled;thirdPartyParty CookiesEnabled;
exl-id: d1e95afc-0b8a-49c0-a20e-e2ab3d657e45
source-git-commit: 4d0f1b3e064bd7b24e17ff0fafb50d930b128968
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 12%

---

# Configurare l’SDK web per Platform

La configurazione per l’SDK viene eseguita con la `configure` comando.

>[!IMPORTANT]
>
>`configure` è *sempre* il primo comando chiamato.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

È possibile impostare molte opzioni durante la configurazione. Di seguito sono riportate tutte le opzioni, raggruppate per categoria.

## Opzioni generali

### `edgeConfigId`

>[!NOTE]
>
>**Le configurazioni Edge sono state rinominate in Datastreams. Un ID datastream è lo stesso di un ID di configurazione.**

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Stringa | Sì | Nessuna |

{style=&quot;table-layout:auto&quot;}

L&#39;ID di configurazione assegnato, che collega l&#39;SDK agli account e alla configurazione appropriati. Quando configuri più istanze all’interno di una singola pagina, devi configurare un `edgeConfigId` per ogni istanza.

### `context`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| ---------------- | ------------ | -------------------------------------------------- |
| Array di stringhe | No | `["web", "device", "environment", "placeContext"]` |

{style=&quot;table-layout:auto&quot;}

Indica le categorie di contesto da raccogliere automaticamente come descritto in [Informazioni automatiche](../data-collection/automatic-information.md). Se questa configurazione non è specificata, vengono utilizzate tutte le categorie per impostazione predefinita.

### `debugEnabled`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Booleano | No | `false` |

{style=&quot;table-layout:auto&quot;}

Indica se il debug è abilitato. Impostazione della configurazione su `true` abilita le seguenti funzionalità:

| **Funzione** | **Funzione** |
| ---------------------- | ------------------ |
| Registrazione della console | Abilita la visualizzazione dei messaggi di debug nella console JavaScript del browser |

{style=&quot;table-layout:auto&quot;}

### `edgeDomain` {#edge-domain}

Compilare questo campo con il dominio di prime parti. Per maggiori dettagli, consulta la [documentazione](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html?lang=it).

Il dominio è simile a `data.{customerdomain.com}` per un sito web all&#39;indirizzo www.{customerdomain.com}.

### `edgeBasePath` {#edge-base-path}

Percorso successivo a edgeDomain utilizzato per comunicare e interagire con i servizi Adobe.  Spesso questo cambiamento si verifica solo quando non si utilizza l’ambiente di produzione predefinito.

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Stringa | No | ee |

{style=&quot;table-layout:auto&quot;}

### `orgId`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Stringa | Sì | Nessuna |

{style=&quot;table-layout:auto&quot;}

Assegnato [!DNL Experience Cloud] ID organizzazione. Quando configuri più istanze all’interno di una pagina, devi configurare un `orgId` per ogni istanza.

## Raccolta dati

### `clickCollectionEnabled` {#clickCollectionEnabled}

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

{style=&quot;table-layout:auto&quot;}

Indica se i dati associati ai clic sul collegamento vengono raccolti automaticamente. Vedi [Tracciamento automatico dei collegamenti](../data-collection/track-links.md#automaticLinkTracking) per ulteriori informazioni. I collegamenti sono anche etichettati come collegamenti di download se includono un attributo di download o se il collegamento termina con un’estensione di file. I qualificatori di collegamento per il download possono essere configurati con un’espressione regolare. Il valore predefinito è `"\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"`

### `onBeforeEventSend`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Funzione | No | () => non definito |

{style=&quot;table-layout:auto&quot;}

Configura un callback chiamato per ogni evento immediatamente prima dell&#39;invio. Un oggetto con il campo `xdm` viene inviato al callback. Per modificare l’invio, modifica il `xdm` oggetto. All&#39;interno del callback, il `xdm` oggetto dispone già dei dati passati nel comando evento e delle informazioni raccolte automaticamente. Per ulteriori informazioni sulla tempistica di questo callback e un esempio, vedi [Modifica degli eventi a livello globale](tracking-events.md#modifying-events-globally).

## Opzioni privacy

### `defaultConsent` {#default-consent}

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Oggetto | No | `"in"` |

{style=&quot;table-layout:auto&quot;}

Imposta il consenso predefinito dell’utente. Utilizza questa impostazione quando non è già stata salvata alcuna preferenza di consenso per l’utente. Gli altri valori validi sono `"pending"` e `"out"`. Questo valore predefinito non viene mantenuto nel profilo dell’utente. Il profilo dell’utente viene aggiornato solo quando `setConsent` viene chiamato.
* `"in"`: Quando questa impostazione è impostata o non viene fornito alcun valore, il lavoro procede senza le preferenze di consenso dell&#39;utente.
* `"pending"`: Quando questa impostazione è impostata, il lavoro viene messo in coda fino a quando l&#39;utente non fornisce le preferenze di consenso.
* `"out"`: Quando questa impostazione è impostata, il lavoro viene scartato finché l&#39;utente non fornisce le preferenze di consenso.
Dopo aver fornito le preferenze dell&#39;utente, lavorare procede o viene interrotto in base alle preferenze dell&#39;utente. Vedi [Consenso di supporto](../consent/supporting-consent.md) per ulteriori informazioni.

## Opzioni di personalizzazione

### `prehidingStyle`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Stringa | No | Nessuna |

{style=&quot;table-layout:auto&quot;}

Utilizzato per creare una definizione di stile CSS che nasconde le aree contenuto della pagina web mentre il contenuto personalizzato viene caricato dal server. Se non viene fornita questa opzione, l’SDK non tenta di nascondere alcuna area di contenuto durante il caricamento del contenuto personalizzato, generando potenzialmente una visualizzazione momentanea di altri contenuti.

Ad esempio, se un elemento nella pagina web ha un ID di `container`, il cui contenuto predefinito da nascondere durante il caricamento di contenuto personalizzato dal server, utilizza il seguente stile di pre-hiding:

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

## Opzioni del pubblico

### `cookieDestinationsEnabled`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

{style=&quot;table-layout:auto&quot;}

Abilita [!DNL Audience Manager] destinazioni cookie, che consente di impostare cookie in base alla qualifica del segmento.

### `urlDestinationsEnabled`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

{style=&quot;table-layout:auto&quot;}

Abilita [!DNL Audience Manager] Destinazioni URL, che consentono di attivare gli URL in base alla qualifica del segmento.

## Opzioni di identità

### `idMigrationEnabled` {#id-migration-enabled}

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

{style=&quot;table-layout:auto&quot;}

Se true, l&#39;SDK legge e imposta i cookie AMCV precedenti. Questa opzione aiuta nella transizione all&#39;utilizzo di Adobe Experience Platform Web SDK, mentre alcune parti del sito potrebbero ancora utilizzare Visitor.js. Se nella pagina è definita l’API del visitatore, l’SDK invia una query all’API del visitatore per l’ECID. Questa opzione consente di utilizzare pagine con doppio tag con Adobe Experience Platform Web SDK e di disporre comunque dello stesso ECID.

### `thirdPartyCookiesEnabled`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

{style=&quot;table-layout:auto&quot;}

Abilita l’impostazione di cookie di terze parti di Adobe. L&#39;SDK può mantenere l&#39;ID visitatore in un contesto di terze parti per consentire l&#39;utilizzo dello stesso ID visitatore nei diversi siti. Utilizza questa opzione se disponi di più siti o desideri condividere dati con i partner; tuttavia, a volte questa opzione non è desiderata per motivi di privacy.
