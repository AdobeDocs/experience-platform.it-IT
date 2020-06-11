---
title: Configurazione dell’SDK
seo-title: Configurazione di Adobe Experience Platform Web SDK
description: Scopri come configurare l’SDK Web per la piattaforma Experience
seo-description: Scopri come configurare l’SDK Web per la piattaforma Experience
translation-type: tm+mt
source-git-commit: 7d4f364ebb9df1ce58481a35007ea75f86ab7825
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 7%

---


# Configurazione dell’SDK

La configurazione per l’SDK viene effettuata con il `configure` comando.

>[!IImportante]
>`configure` deve essere _sempre_ il primo comando chiamato.

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
| Stringa | Sì | none |

L’ID di configurazione assegnato, che collega l’SDK agli account e alla configurazione appropriati.  Quando si configurano più istanze all&#39;interno di una singola pagina, è necessario configurare un&#39;altra istanza `edgeConfigId` per ciascuna.

### `context`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| ---------------- | ------------ | -------------------------------------------------- |
| Matrice di stringhe | No | `["web", "device", "environment", "placeContext"]` |

Indica le categorie di contesto da raccogliere automaticamente come descritto in Informazioni [](../reference/automatic-information.md)automatiche.  Se questa configurazione non è specificata, per impostazione predefinita vengono utilizzate tutte le categorie.

### `debugEnabled`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Booleano | No | `false` |

Indica se il debug deve essere abilitato. Impostando questa configurazione si `true` abilitano le seguenti funzionalità:

| **Funzione** |  |  |
| ---------------------- | ------------------ |
| Convalida sincrona | Convalida i dati raccolti rispetto allo schema e restituisce un errore nella risposta sotto la seguente etichetta: `collect:error OR success` |
| Registrazione della console | Abilita la visualizzazione dei messaggi di debug nella console JavaScript del browser |

### `edgeDomain`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ------------------ |
| Stringa | No | `beta.adobedc.net` |

Dominio utilizzato per interagire con Adobe Services. Questo viene utilizzato solo se disponete di un dominio di prime parti (CNAME) che esegue il proxy delle richieste all&#39;infrastruttura periferica di Adobe.

### `orgId`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Stringa | Sì | none |

L’ID organizzazione Experience Cloud assegnato.  Quando si configurano più istanze all&#39;interno di una pagina, è necessario configurare un&#39;altra istanza `orgId` per ciascuna.

## Raccolta dati

### `clickCollectionEnabled`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

Indica se i dati associati ai clic del collegamento devono essere raccolti automaticamente. Per i clic considerati come clic del collegamento, vengono raccolti i seguenti dati di interazione [](https://github.com/adobe/xdm/blob/master/docs/reference/context/webinteraction.schema.md) Web:

| **Proprietà** |  |
| ------------ | ----------------------------------- |
| Nome collegamento | Nome determinato dal contesto del collegamento |
| URL collegamento | URL normalizzato |
| Tipo di collegamento | Impostato per scaricare, uscire o altro |

### `onBeforeEventSend`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Funzione | No | () => non definito |

Impostate questa opzione per configurare un callback che viene chiamato per ogni evento appena prima che venga inviato.  Un oggetto con il campo `xdm` viene inviato al callback.  Modificare l&#39;oggetto xdm per modificare l&#39;elemento inviato.  All&#39;interno del callback, l&#39; `xdm` oggetto avrà già i dati passati nel comando dell&#39;evento e le informazioni raccolte automaticamente.  Per ulteriori informazioni sui tempi di questa callback e un esempio, vedere [Modifica degli eventi a livello globale](tracking-events.md#modifying-events-globally).

## Opzioni sulla privacy

### `defaultConsent`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Oggetto | No | `{"general": "in"}` |

Imposta il consenso predefinito dell&#39;utente. Questo viene utilizzato quando non è già stata salvata alcuna preferenza di consenso per l&#39;utente. L&#39;altro valore valido è `{"general": "pending"}`. Una volta impostato, il lavoro verrà messo in coda fino a quando l&#39;utente non fornirà le preferenze di consenso. Dopo aver fornito le preferenze dell&#39;utente, lavorare procede o viene interrotto in base alle preferenze dell&#39;utente. Per ulteriori informazioni, consultate [Supporto](supporting-consent.md) .

## Opzioni di personalizzazione

### `prehidingStyle`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Stringa | No | none |

Utilizzato per creare una definizione di stile CSS che nasconde le aree contenuto della pagina Web mentre il contenuto personalizzato viene caricato dal server. Se non viene fornita questa opzione, l’SDK non tenta di nascondere alcuna area di contenuto mentre viene caricato del contenuto personalizzato, generando potenzialmente uno &quot;sfarfallio&quot;.

Ad esempio, se nella pagina Web era presente un elemento con un ID del `container` cui contenuto predefinito si desidera nascondere mentre il contenuto personalizzato viene caricato dal server, un esempio di stile di prenascondere è il seguente:

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

## Opzioni Pubblico

### `cookieDestinationsEnabled`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

Abilita le destinazioni dei cookie, che consentono di impostare i cookie in base alla qualifica del segmento.

### `urlDestinationsEnabled`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

Abilita le destinazioni URL, che consentono di attivare gli URL in base alla qualifica del segmento.

## Opzioni identità

### `idSyncContainerId`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Numero | No | none |

L&#39;ID contenitore che specifica quali sincronizzazioni ID vengono attivate. Si tratta di un numero intero non negativo che può essere ottenuto dal consulente.

### `idSyncEnabled`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Booleano | No | `true` |

Abilita la funzione di sincronizzazione ID, che consente di attivare gli URL per sincronizzare l’ID utente univoco Adobe con l’ID utente univoco di un’origine dati di terze parti.

### `thirdPartyCookiesEnabled`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Booleano | No | true |

Abilita l&#39;impostazione dei cookie di terze parti di Adobe. L’SDK può mantenere l’ID visitatore in un contesto di terze parti per consentire l’utilizzo dello stesso ID visitatore in più siti. Questa funzione è utile se si dispone di più siti o si desidera condividere i dati con i partner; tuttavia, a volte questo non è desiderato per motivi di privacy.
