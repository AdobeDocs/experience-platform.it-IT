---
title: Configurare Adobe Experience Platform Web SDK
description: Scopri come configurare Adobe Experience Platform Web SDK.
source-git-commit: 68174928d3b005d1e5a31b17f3f287e475b5dc86
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 8%

---


# Configurare Web SDK

La configurazione per l&#39;SDK viene eseguita con `configure` comando.

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
>**Le configurazioni Edge sono state rinominate in Datastream. Un ID dello stream di dati è uguale a un ID di configurazione.**

| Tipo | Obbligatorio | Valore predefinito |
| -------- | ------------ | ----------------- |
| Stringa | Sì | Nessuna |

{style="table-layout:auto"}

L’ID di configurazione assegnato, che collega l’SDK agli account e alla configurazione appropriati. Quando si configurano più istanze all’interno di una singola pagina, è necessario configurare un’altra `edgeConfigId` per ogni istanza.

### `context` {#context}

| **Tipo** | Obbligatorio | **Valore predefinito** |
| ---------------- | ------------ | -------------------------------------------------- |
| Array di stringhe | No | `["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"]` |

{style="table-layout:auto"}

Indica le categorie di contesto da raccogliere automaticamente come descritto in [Informazione automatica](../data-collection/automatic-information.md). Se questa configurazione non è specificata, per impostazione predefinita vengono utilizzate tutte le categorie.

>[!IMPORTANT]
>
>Tutte le proprietà di contesto, tranne `highEntropyUserAgentHints`, sono attivate per impostazione predefinita. Se hai specificato manualmente le proprietà del contesto nella configurazione dell’SDK Web, devi abilitare tutte le proprietà del contesto per continuare a raccogliere le informazioni necessarie.

Per abilitare [hint client ad alta entropia](user-agent-client-hints.md#enabling-high-entropy-client-hints) nella distribuzione dell’SDK Web, è necessario includere i `highEntropyUserAgentHints` insieme alla configurazione esistente.

Ad esempio, per recuperare gli hint client ad alta entropia dalle proprietà web, la configurazione sarà simile alla seguente:

`context: ["highEntropyUserAgentHints", "web"]`


### `debugEnabled`

| Tipo | Obbligatorio | Valore predefinito |
| -------- | ------------ | ----------------- |
| Booleano | No | `false` |

{style="table-layout:auto"}

Indica se il debug è abilitato. Impostazione di questa configurazione su `true` abilita le seguenti funzionalità:

| **Funzionalità** | **Funzione** |
| ---------------------- | ------------------ |
| Registrazione della console | Consente di visualizzare i messaggi di debug nella console JavaScript del browser |

{style="table-layout:auto"}

### `edgeDomain` {#edge-domain}

Popola questo campo con il tuo dominio di prime parti. Per ulteriori dettagli, vedi [documentazione](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=it).

Il dominio è simile a `data.{customerdomain.com}` per un sito web all’indirizzo www.{customerdomain.com}

### `edgeBasePath` {#edge-base-path}

Percorso dopo il dominio edge utilizzato per comunicare e interagire con i servizi Adobe.  Spesso questo cambiava solo quando non si utilizzava l’ambiente di produzione predefinito.

| Tipo | Obbligatorio | Valore predefinito |
| -------- | ------------ | ----------------- |
| Stringa | No | vedi |

{style="table-layout:auto"}

### `orgId`

| Tipo | Obbligatorio | Valore predefinito |
| -------- | ------------ | ----------------- |
| Stringa | Sì | Nessuna |

{style="table-layout:auto"}

Assegnato a [!DNL Experience Cloud] ID organizzazione. Quando configuri più istanze all’interno di una pagina, devi configurare un’altra `orgId` per ogni istanza.

## Raccolta dati

### `clickCollectionEnabled` {#clickCollectionEnabled}

| Tipo | Obbligatorio | Valore predefinito |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

{style="table-layout:auto"}

Indica se i dati associati ai clic sui collegamenti vengono raccolti automaticamente. Consulta [Tracciamento automatico dei collegamenti](../data-collection/track-links.md#automaticLinkTracking) per ulteriori informazioni. I collegamenti sono anche etichettati come collegamenti di download se includono un attributo di download o se il collegamento termina con un’estensione di file. I qualificatori dei collegamenti di download possono essere configurati con un’espressione regolare. Il valore predefinito è `"\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"`

### `onBeforeEventSend`

| Tipo | Obbligatorio | Valore predefinito |
| -------- | ------------ | ----------------- |
| Funzione | No | () => non definito |

{style="table-layout:auto"}

Configura un callback chiamato per ogni evento immediatamente prima dell&#39;invio. Un oggetto con il campo `xdm` viene inviato al callback. Per modificare l’elemento inviato, modifica il `xdm` oggetto. All&#39;interno del callback, il `xdm` L&#39;oggetto dispone già dei dati passati nel comando event e delle informazioni raccolte automaticamente. Per ulteriori informazioni sulla tempistica di questo callback e un esempio, vedi [Modifica degli eventi a livello globale](tracking-events.md#modifying-events-globally).

### `onBeforeLinkClickSend` {#onBeforeLinkClickSend}

| Tipo | Obbligatorio | Valore predefinito |
| -------- | ------------ | ----------------- |
| Funzione | No | () => non definito |

{style="table-layout:auto"}

Configura un callback chiamato per ogni evento di tracciamento dei clic di collegamento immediatamente prima dell’invio. Il callback invia un oggetto con `xdm`, `clickedElement`, e `data` campi.

Quando filtri il tracciamento dei collegamenti utilizzando la struttura DOM, puoi utilizzare `clickElement` comando. `clickedElement` è il nodo dell&#39;elemento DOM su cui è stato fatto clic e che ha incapsulato la struttura dei nodi padre.

Per modificare i dati inviati, modifica il `xdm` e/o `data` oggetti. All&#39;interno del callback, il `xdm` L&#39;oggetto dispone già dei dati passati nel comando event e delle informazioni raccolte automaticamente.

* Qualsiasi valore diverso da `false` consente di elaborare l’evento e di inviare il callback.
* Se il callback restituisce `false` l’elaborazione dell’evento viene interrotta senza errori e l’evento non viene inviato. Questo meccanismo consente di filtrare alcuni eventi esaminando i dati dell’evento e restituendoli `false` se l’evento non deve essere inviato.
* Se il callback genera un&#39;eccezione, l&#39;elaborazione dell&#39;evento viene interrotta e l&#39;evento non viene inviato.


## Opzioni privacy

### `defaultConsent` {#default-consent}

| Tipo | Obbligatorio | Valore predefinito |
| -------- | ------------ | ----------------- |
| Oggetto | No | `"in"` |

{style="table-layout:auto"}

Imposta il consenso predefinito dell’utente. Usa questa impostazione quando per l’utente non è già stata salvata alcuna preferenza di consenso. Gli altri valori validi sono `"pending"` e `"out"`. Questo valore predefinito non viene mantenuto nel profilo dell’utente. Il profilo dell’utente viene aggiornato solo quando `setConsent` viene chiamato.
* `"in"`: quando questa impostazione è attiva o non viene fornito alcun valore, il lavoro procede senza le preferenze di consenso dell’utente.
* `"pending"`: quando questa impostazione è impostata, il lavoro viene messo in coda fino a quando l’utente non fornisce le preferenze di consenso.
* `"out"`: quando questa impostazione è impostata, il lavoro viene scartato fino a quando l’utente non fornisce le preferenze di consenso.
Una volta fornite le preferenze dell’utente, il lavoro procede oppure viene interrotto in base alle preferenze dell’utente. Consulta [Consenso di supporto](../consent/supporting-consent.md) per ulteriori informazioni.

## Opzioni di personalizzazione {#personalization}

### `prehidingStyle` {#prehidingStyle}

| Tipo | Obbligatorio | Valore predefinito |
| -------- | ------------ | ----------------- |
| Stringa | No | Nessuna |

{style="table-layout:auto"}

Utilizzato per creare una definizione di stile CSS che nasconde le aree di contenuto della pagina web mentre il contenuto personalizzato viene caricato dal server. Se questa opzione non viene fornita, l’SDK non tenta di nascondere alcuna area di contenuto durante il caricamento del contenuto personalizzato, generando potenzialmente uno &quot;sfarfallio&quot;.

Ad esempio, se un elemento nella pagina web ha un ID di `container`, di cui desideri nascondere il contenuto predefinito mentre il contenuto personalizzato viene caricato dal server, utilizza il seguente stile di pre-hiding:

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

### `targetMigrationEnabled` {#targetMigrationEnabled}

Questa opzione deve essere utilizzata durante la migrazione di singole pagine da [!DNL at.js] all’SDK per web.

Utilizza questa opzione per abilitare Web SDK per la lettura e la scrittura delle versioni precedenti di `mbox` e `mboxEdgeCluster` cookie utilizzati da [!DNL at.js]. In questo modo è possibile mantenere il profilo del visitatore mentre si passa da una pagina che utilizza l’SDK per web a una pagina che utilizza l’SDK [!DNL at.js] e viceversa.

| Tipo | Obbligatorio | Valore predefinito |
| -------- | ------------ | ----------------- |
| Booleano | No | `false` |

## Opzioni del pubblico

### `cookieDestinationsEnabled`

| Tipo | Obbligatorio | Valore predefinito |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

{style="table-layout:auto"}

Abilita [!DNL Audience Manager] destinazioni dei cookie, che consente di impostare i cookie in base alla qualificazione del segmento.

### `urlDestinationsEnabled`

| Tipo | Obbligatorio | Valore predefinito |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

{style="table-layout:auto"}

Abilita [!DNL Audience Manager] Destinazioni URL, che consente l’attivazione di URL basati sulla qualificazione dei segmenti.

## Opzioni di identità

### `idMigrationEnabled` {#id-migration-enabled}

| Tipo | Obbligatorio | Valore predefinito |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

{style="table-layout:auto"}

Se true, l&#39;SDK legge e imposta i cookie AMCV precedenti. Questa opzione facilita la transizione all’utilizzo di Adobe Experience Platform Web SDK, mentre alcune parti del sito potrebbero ancora utilizzare Visitor.js.

Se nella pagina è definita l’API visitatore, l’SDK esegue una query sull’API visitatore per l’ECID. Questa opzione consente di usare pagine con doppio tag con Adobe Experience Platform Web SDK mantenendo lo stesso ECID.

### `thirdPartyCookiesEnabled`

| Tipo | Obbligatorio | Valore predefinito |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

{style="table-layout:auto"}

Abilita l’impostazione di cookie di terze parti Adobe. L&#39;SDK può rendere persistente l&#39;ID visitatore in un contesto di terze parti per consentire l&#39;utilizzo dello stesso ID visitatore in più siti. Utilizza questa opzione se disponi di più siti o desideri condividere i dati con i partner; tuttavia, a volte questa opzione non è desiderata per motivi di privacy.
