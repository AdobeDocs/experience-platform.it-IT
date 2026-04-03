---
title: Utilizzo di identityMap nella raccolta dati
description: Scopri come creare e inviare payload identityMap per identificare i visitatori noti negli spazi dei nomi nell’implementazione di Web SDK.
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1671'
ht-degree: 0%

---

# Utilizzo di identityMap nella raccolta dati

L&#39;oggetto payload `identityMap` è il modo in cui si comunica all&#39;Edge Network chi è un visitatore oltre il livello di dispositivo [ECID](./overview.md). Quando un visitatore effettua l’accesso, completa un acquisto o viene altrimenti reso noto, puoi inviare identificatori a livello di persona (ID del sistema di gestione delle relazioni con i clienti, e-mail con hash, ID fedeltà, ecc.) insieme all’ECID. Questi identificatori a livello di persona forniscono informazioni preziose ai servizi a valle in modo che possano:

* **Unisci l&#39;attività a una persona su più dispositivi e canali.** [Identity Service](/help/identity-service/home.md) collega le identità inviate a un [grafo delle identità](/help/identity-service/features/identity-graph-viewer.md), connettendo un comportamento anonimo a livello di dispositivo a una persona nota.
* **Creare profili cliente unificati.** [Real-Time Customer Profile](/help/profile/home.md) utilizza l&#39;identità primaria impostata per ancorare eventi e attributi a un singolo profilo, consentendo la segmentazione a livello di persona e la creazione di tipi di pubblico.
* **Attiva i tipi di pubblico nelle destinazioni a valle.** Molte [Destinazioni](/help/destinations/home.md) richiedono identità a livello di persona risolte (e-mail con hash, numeri di telefono, ecc.) per far corrispondere i tipi di pubblico alle basi utente.
* **Orchestrazione di percorsi multicanale.** [Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=it) utilizza identità risolte per attivare e personalizzare percorsi tra canali e-mail, push e in-app in base al comportamento autenticato di un visitatore.

In questa pagina viene descritto come creare payload `identityMap`, scegliere le impostazioni corrette per ogni identità e gestire scenari di implementazione comuni.

## Struttura del payload {#structure}

`identityMap` è un oggetto JSON in cui ogni chiave di primo livello è uno spazio dei nomi e il valore è un array di descrittori di identità. È possibile includere uno o più spazi dei nomi in un singolo payload e ogni descrittore contiene tre campi: `id`, `authenticatedState` e `primary`.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

| Campo | Tipo | Obbligatorio | Descrizione |
| --- | --- | --- | --- |
| `id` | Stringa | Sì | Il valore dell&#39;identificatore (ad esempio, `user@example.com` o `ABC123`). |
| `authenticatedState` | Stringa | Sì | Con quanta sicurezza sai che questa identità appartiene al visitatore. I valori validi includono `ambiguous`, `authenticated` e `loggedOut`. |
| `primary` | Booleano | Sì | Indica se questa identità deve essere l&#39;identificatore primario dell&#39;evento. Una sola identità in tutti gli spazi dei nomi deve essere contrassegnata `primary: true`. |

Le sezioni seguenti descrivono in dettaglio ciascuna parte del payload.

### Chiavi dello spazio dei nomi {#namespace-keys}

Ogni chiave di primo livello in `identityMap` è uno spazio dei nomi [identity](/help/identity-service/features/namespaces.md), ovvero una stringa che classifica il tipo di identificatore, ad esempio `CRMID`, `Email`, `Phone` o `LoyaltyId`. Gli spazi dei nomi devono esistere in Identity Service prima di poter essere inseriti in un payload. È possibile includere più chiavi dello spazio dei nomi nello stesso evento quando si dispone di più identificatori per il visitatore.

Non è necessario includere l’ECID come chiave dello spazio dei nomi. Edge Network aggiunge automaticamente l’ECID al payload di identità. Se includi esplicitamente l&#39;ECID, non contrassegnarlo come `primary` quando è presente anche un&#39;identità a livello di persona.

### `id` {#id}

Il campo `id` è la stringa dell&#39;identificatore stesso, ovvero il valore che indica ad Experience Platform quale persona o dispositivo specifico rappresenta questa identità. Ogni [spazio dei nomi identità](/help/identity-service/features/namespaces.md) prevede un formato di valore specifico e l&#39;invio di un valore nel formato errato crea un&#39;identità distinta che non può essere unita alla versione formattata correttamente, con conseguente frammentazione dei profili.

Prima di includere un valore in `identityMap`, preparalo in base al formato previsto dallo spazio dei nomi di destinazione:

| Tipi di spazio dei nomi comuni | Come preparare il valore | Esempio |
| --- | --- | --- |
| **CRM/ID interno** | Utilizza l’identificatore esatto assegnato dal sistema di record. Mantieni il formato coerente in tutti gli eventi (maiuscole/minuscole, zeri iniziali, prefissi). | `ABC-12345`, `00098765` |
| **E-mail (raw)** | Minore è la distinzione tra maiuscole e minuscole tra l&#39;indirizzo e-mail completo e lo spazio vuoto iniziale e finale. | `user@example.com` |
| **E-mail con hash** | Metti in minuscolo e taglia prima l’indirizzo e-mail, quindi applica l’hash con SHA-256. Invia la stringa esadecimale risultante di 64 caratteri. Non aggiungere un sale a meno che la definizione dello spazio dei nomi non ne richieda uno. | `a1b2c3d4e5f6a7b8c9...` |
| **Telefono (E.164)** | Formattare il numero in [E.164](https://en.wikipedia.org/wiki/E.164): un `+` iniziale, il codice paese e il numero dell&#39;utente con sottoscrizione senza spazi o punteggiatura. | `+15551234567` |
| **FPID** | Genera una stringa [UUIDv4](https://datatracker.ietf.org/doc/html/rfc4122). Consulta [ID dispositivo di prime parti](./fpid.md) per i requisiti di generazione. | `123e4567-e89b-42d3-9456-426614174000` |

Per l&#39;elenco completo degli spazi dei nomi standard e delle relative definizioni, vedere [Panoramica dello spazio dei nomi delle identità](/help/identity-service/features/namespaces.md#standard).

>[!TIP]
>
>Il valore `id` distingue tra maiuscole e minuscole. `User@Example.com` e `user@example.com` sono trattati come due identità separate. Normalizza le maiuscole/minuscole prima di inviare il valore (di solito inserendo minuscole nelle e-mail e rimuovendo gli spazi vuoti) per evitare di creare identità duplicate nel grafico.

#### Raccolta di `id` in fase di runtime {#collect-id}

L’identificatore necessario è raramente disponibile direttamente sulla pagina. Le strategie comuni di raccolta includono:

* **Livello dati**: leggi l&#39;identificatore dal livello dati del tuo sito dopo che il visitatore ha effettuato l&#39;accesso. Questa posizione è l’approccio più affidabile perché il livello dati viene popolato dal backend dell’applicazione e riflette lo stato di sessione autenticato.
* **Token di autenticazione o cookie di sessione**: decodifica o cerca l&#39;identificatore da un cookie JWT o di sessione impostato dal sistema di autenticazione. Verifica che il token sia ancora attivo prima di utilizzare il valore.
* **Arricchimento lato server**: utilizza [Preparazione dati per raccolta dati](/help/datastreams/data-prep.md) o una [regola di inoltro eventi](/help/tags/ui/event-forwarding/overview.md) per mappare o trasformare l&#39;identificatore in Edge prima che raggiunga i servizi a valle. Questa posizione è utile quando il client ha solo un token di sessione opaco mappato a un ID interno sul lato server.

>[!TIP]
>
>Se un determinato valore `id` viene risolto in una stringa vuota, `null` o `undefined`, non includere lo spazio dei nomi in `identityMap`. L&#39;invio di un elemento `id` vuoto crea un record di identità interrotto. Controlla l’implementazione con un controllo prima di creare il payload.

### `authenticatedState` {#authenticated-state}

Il campo `authenticatedState` indica ai servizi a valle il livello di attendibilità da inserire in una determinata identità. I seguenti valori sono validi per questo campo:

| Valore | Quando utilizzare |
| --- | --- |
| **`authenticated`** | Il visitatore ha dimostrato attivamente la propria identità durante la sessione corrente (ad esempio, effettuando l’accesso con le credenziali, completando l’MFA o una verifica simile). |
| **`loggedOut`** | Il visitatore era precedentemente autenticato ma da allora si è disconnesso. L’identità è ancora associata al dispositivo, ma la sessione non è più attiva. |
| **`ambiguous`** | L’identità non può essere confermata come appartenente al visitatore corrente. Utilizza questo valore per gli identificatori a livello di dispositivo come FPID o qualsiasi identificatore in cui non si è ancora verificata l’autenticazione. |

>[!TIP]
>
>Il valore `authenticatedState` influisce sul modo in cui Adobe Experience Platform Identity Service crea e unisce i grafici delle identità. L&#39;invio di `authenticated` per un&#39;identità non verificata può creare collegamenti tra dispositivi non corretti e difficili da annullare.

### `primary` {#primary-identity}

Ogni payload `identityMap` deve avere esattamente un&#39;identità contrassegnata come `primary: true`. L’identità primaria determina quale identità viene utilizzata come ancoraggio per l’evento in Experience Platform.

Segui queste linee guida quando imposti l’identità primaria:

* **Se è disponibile un&#39;identità a livello di persona** (il visitatore ha effettuato l&#39;accesso), contrassegna lo spazio dei nomi a livello di persona come primario e l&#39;ECID come non primario. Questo comunica ad Experience Platform di ancorare l’evento alla persona anziché al dispositivo.
* **Quando sono disponibili solo identità a livello di dispositivo** (il visitatore è anonimo), l&#39;ECID viene utilizzato automaticamente come identità primaria. Non è necessario includere l&#39;ECID in `identityMap`, l&#39;Edge Network lo aggiunge automaticamente.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ],
    "Email": [
      {
        "id": "user@example.com",
        "authenticatedState": "authenticated",
        "primary": false
      }
    ]
  }
}
```

## Invio di identityMap nell’implementazione {#send-identity}

>[!BEGINTABS]

>[!TAB Libreria JavaScript]

Passa `identityMap` nell&#39;oggetto `xdm` di una chiamata [`sendEvent`](/help/collection/js/commands/sendevent/overview.md):

```js
alloy("sendEvent", {
  xdm: {
    identityMap: {
      CRMID: [
        {
          id: "abc-123-xyz",
          authenticatedState: "authenticated",
          primary: true
        }
      ]
    },
    eventType: "web.webpagedetails.pageViews"
  }
});
```

>[!TAB Estensione tag Web SDK]

Utilizza il tipo di elemento dati [Identity map](/help/tags/extensions/client/web-sdk/data-element-types.md#identity-map) per generare il payload dell&#39;identità nell&#39;interfaccia utente Tag:

1. Creare un elemento dati con estensione **[!UICONTROL Adobe Experience Platform Web SDK]** e tipo di elemento dati **[!UICONTROL Identity map]**.
2. Aggiungi le identità specificando lo spazio dei nomi, l’elemento dati o il valore che viene risolto nell’identificatore e lo stato autenticato.
3. Contrassegna una sola identità come principale.
4. Fai riferimento a questo elemento dati nell&#39;azione **[!UICONTROL Send event]** in **[!UICONTROL Identity map]**.

>[!ENDTABS]

## Scenari comuni {#common-scenarios}

+++**Accesso**

Quando un visitatore effettua l&#39;accesso, invia il proprio identificatore a livello di persona con `authenticatedState: "authenticated"` e `primary: true`. Includi questa identità sul primo evento dopo l’autenticazione e su tutti gli eventi successivi nella sessione.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

+++

+++**Disconnessione**

Quando un visitatore si disconnette, aggiorna `authenticatedState` in `loggedOut` mantenendo lo stesso identificatore. In questo modo viene mantenuta l’associazione tra il dispositivo e la persona segnalando al contempo che la sessione non è più attiva.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "loggedOut",
        "primary": false
      }
    ]
  }
}
```

Dopo la disconnessione, l’ECID torna ad essere l’identità primaria effettiva (Edge Network lo applica automaticamente). Non contrassegnare un’identità a livello di persona diversa come primaria a meno che il visitatore non effettui l’accesso con un account diverso.

>[!IMPORTANT]
>
>Non interrompere completamente l&#39;invio dell&#39;identificatore dopo la disconnessione. Il passaggio da `authenticated` a `loggedOut` indica ai servizi a valle che la sessione è terminata. Omettendo completamente l’identificatore si lascia un vuoto nel grafico delle identità che può causare la frammentazione dei profili.

+++

+++**Più spazi dei nomi**

Puoi inviare più spazi dei nomi di identità nello stesso evento. Questo scenario è comune quando un visitatore ha effettuato l’accesso e sono disponibili diversi identificatori (ad esempio, un ID del sistema di gestione delle relazioni con i clienti, un’e-mail con hash e un ID fedeltà). Includere tutti gli identificatori noti, contrassegnarne solo uno come primario e impostare gli altri su `primary: false`.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ],
    "Email_LC_SHA256": [
      {
        "id": "a1b2c3d4e5f6...",
        "authenticatedState": "authenticated",
        "primary": false
      }
    ],
    "LoyaltyId": [
      {
        "id": "LOY-98765",
        "authenticatedState": "authenticated",
        "primary": false
      }
    ]
  }
}
```

>[!TIP]
>
>L&#39;invio di più spazi dei nomi con lo stesso `authenticatedState` nello stesso evento fornisce al servizio Identity il segnale più forte per il collegamento di tali identità. Includi tutti gli identificatori disponibili al punto di autenticazione anziché distribuirli tra eventi separati.

+++

+++**Visitatori anonimi**

Per i visitatori anonimi, in genere non è necessario inviare alcun `identityMap`. Edge Network assegna automaticamente un ECID e lo utilizza come identità primaria. Se utilizzi [ID dispositivo di prime parti](./fpid.md), l&#39;FPID è l&#39;unica identità da includere per i visitatori anonimi.

+++

## Effetti di identityMap sul grafo delle identità {#identity-graph}

Ogni payload `identityMap` che raggiunge Experience Platform viene elaborato da [Identity Service](/help/identity-service/home.md), che collega le identità inviate a un [grafo di identità](/help/identity-service/features/identity-graph-viewer.md). Gli spazi dei nomi inclusi, la modalità di impostazione di `authenticatedState` e l&#39;identità contrassegnata come `primary` determinano direttamente il modo in cui Identity Service crea e unisce tali grafici.

Comportamenti chiave da considerare:

* **Le identità inviate nello stesso evento sono collegate tra loro.** Se includi un CRMID e uno spazio dei nomi e-mail nella stessa chiamata `sendEvent`, il servizio Identity crea un collegamento tra queste due identità. La diffusione degli identificatori tra eventi separati genera collegamenti più deboli e può causare la frammentazione dei grafici.
* **L&#39;identità `primary` ancorerà l&#39;evento in Real-Time Customer Profile.Il profilo** utilizza l&#39;identità primaria per determinare a quale profilo appartiene l&#39;evento. Contrassegnare l’identità errata come principale (ad esempio, impostando ECID come principale quando è disponibile un ID a livello di persona) può causare la memorizzazione di eventi sui profili a livello di dispositivo anziché sui profili a livello di persona.
* **`authenticatedState` influenza l&#39;affidabilità del grafico.** L&#39;invio di `authenticated` per un&#39;identità che non è stata effettivamente verificata può creare collegamenti tra dispositivi non corretti e difficili da annullare. Utilizza `authenticated` solo quando il visitatore ha dimostrato attivamente la propria identità durante la sessione corrente.

Se l&#39;implementazione utilizza [regole di collegamento del grafo delle identità](/help/identity-service/identity-graph-linking-rules/overview.md) (ad esempio, la priorità dello spazio dei nomi o l&#39;algoritmo di ottimizzazione delle identità), consultare la [guida all&#39;implementazione](/help/identity-service/identity-graph-linking-rules/implementation-guide.md) per capire come queste regole interagiscono con le identità inviate tramite `identityMap`.

>[!NOTE]
>
>`identityMap` viene inviato solo quando il Web SDK effettua una richiesta ad Edge Network, che viene gestita dallo stato di consenso del visitatore. Se l&#39;implementazione utilizza `defaultConsent: "pending"`, le identità non vengono inviate fino alla concessione del consenso. Per informazioni dettagliate, consulta [Consenso e identità](./consent.md).
