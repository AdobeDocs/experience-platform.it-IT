---
title: Consenso e identità nella raccolta dati
description: Scopri in che modo le scelte di consenso influiscono sul comportamento di identità nelle implementazioni di Web SDK, inclusa la generazione di ECID, la persistenza dei cookie e la continuità dei visitatori.
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 2%

---

# Consenso e identità nella raccolta dati

Il consenso e l’identità sono strettamente connessi nelle implementazioni di Web SDK. Le modalità e i tempi di raccolta del consenso influiscono direttamente su quando e se Web SDK genera un ECID, imposta i cookie di identità e invia i dati ad Edge Network. Quando il consenso non viene gestito con attenzione, il risultato è spesso un’inflazione inaspettata dei visitatori, lacune nella continuità dell’identità o entrambi.

Questa pagina spiega come le scelte di consenso interagiscono con il comportamento di identità e fornisce indicazioni per configurare la tua implementazione per evitare insidie comuni. Per informazioni generali sulla gestione di ECID, FPID e altri segnali di identità da parte del Web SDK, vedere [Identità nella raccolta dati](./overview.md).

## Come il consenso influisce sull’identità {#how-consent-affects-identity}

Il Web SDK utilizza sia la variabile di configurazione [`defaultConsent`](/help/collection/js/commands/configure/defaultconsent.md) che il comando [`setConsent`](/help/collection/js/commands/setconsent.md) per controllare se invia dati ad Edge Network. Lo stato di consenso determina direttamente quando viene generato un ECID e quando vengono impostati i cookie di identità.

Nella tabella seguente viene illustrato l&#39;effetto combinato di `defaultConsent` e `setConsent` sulla raccolta dati, l&#39;impostazione dei cookie e il comportamento di identità.

| `defaultConsent` | `setConsent` | La raccolta dei dati avviene | Cookie del browser impostati | Comportamento identità |
| --- | --- | --- | --- | --- |
| `in` | Non impostato | Sì | Sì | Un ECID viene generato immediatamente alla prima richiesta. I cookie di identità sono impostati al caricamento della pagina. |
| `in` | `in` | Sì | Sì | L’ECID esistente del visitatore viene mantenuto. Il comportamento dell’identità è invariato. |
| `in` | `out` | No | Sì | La raccolta dei dati viene interrotta. I cookie di identità ECID e `kndctr_` esistenti rimangono nel browser fino alla loro scadenza. |
| `pending` | Non impostato | No | No | Non viene generato alcun ECID. Nessun cookie impostato. Gli eventi vengono messi in coda localmente finché non viene chiamato `setConsent`. |
| `pending` | `in` | Sì | Sì | Gli eventi in coda vengono inviati. Alla prima richiesta viene generato un ECID e vengono impostati i cookie di identità. |
| `pending` | `out` | No | Sì | Gli eventi in coda vengono eliminati. Non viene generato alcun ECID. Il cookie di consenso è impostato per registrare le preferenze del visitatore. |
| `out` | Non impostato | No | No | Non viene generato alcun ECID. Nessun cookie impostato. Nessun evento inviato. |
| `out` | `in` | Sì | Sì | Alla prima richiesta viene generato un ECID e vengono impostati i cookie di identità. |
| `out` | `out` | No | Sì | Non viene generato alcun ECID. Il cookie di consenso è impostato per registrare le preferenze del visitatore. |

>[!NOTE]
>
>I cookie di identità e di consenso vengono impostati anche quando un visitatore rinuncia. Questi cookie sono necessari per rispettare le preferenze di raccolta dei dati del visitatore. Per un elenco completo dei cookie impostati da Web SDK, vedere [Cookie di Web SDK](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/cookies/web-sdk).

Quando un visitatore concede nuovamente il consenso dopo averlo revocato in precedenza (chiamando `setConsent` con `"general": "in"` dopo `"general": "out"`), il Web SDK riprende a inviare eventi e utilizza l&#39;ECID esistente dal cookie se non è scaduto. L’identità del visitatore viene mantenuta.

Quando un visitatore concede o nega il consenso, il Web SDK mantiene la preferenza in un cookie di consenso `kndctr_`. Al caricamento delle pagine successive, il SDK legge il cookie e applica automaticamente la preferenza memorizzata. Non è necessario chiamare nuovamente `setConsent` a meno che la preferenza del visitatore non cambi. Il valore di configurazione `defaultConsent` non persiste tra i caricamenti di pagina, ma il consenso risolto del visitatore (impostato tramite `setConsent`) sì.

>[!NOTE]
>
>Gli eventi in coda mentre il consenso è `pending` vengono mantenuti in memoria e non sopravvivono ai ricaricamenti della pagina. Se un visitatore passa a una nuova pagina prima che il consenso sia risolto, gli eventi in coda della pagina precedente andranno persi.

## Modelli di implementazione {#implementation-patterns}

### Modello Opt-in (consenso necessario prima della raccolta) {#opt-in}

Utilizza questo modello quando le normative (come il RGPD) richiedono il consenso esplicito prima di raccogliere i dati.

```js
alloy("configure", {
  orgId: "YOUR_ORG_ID@AdobeOrg",
  edgeDomain: "data.example.com",
  defaultConsent: "pending"
});

// When the visitor grants consent:
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "1.0",
    value: { general: "in" }
  }]
});
```

Con questo pattern:
* Non viene generato alcun ECID finché non viene concesso il consenso.
* Gli eventi attivati prima del consenso (come la visualizzazione della pagina iniziale) vengono messi in coda e inviati dopo la concessione del consenso.
* I cookie di identità vengono impostati solo dopo la prima richiesta di Edge Network riuscita.

### Modello di rinuncia (raccolta per impostazione predefinita, interruzione in caso di rifiuto) {#opt-out}

Utilizza questo modello quando le normative consentono la raccolta dei dati per impostazione predefinita con un’opzione di rinuncia.

```js
alloy("configure", {
  orgId: "YOUR_ORG_ID@AdobeOrg",
  edgeDomain: "data.example.com",
  defaultConsent: "in"
});

// If the visitor opts out:
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "1.0",
    value: { general: "out" }
  }]
});
```

Con questo pattern:
* Un ECID viene generato immediatamente al primo caricamento della pagina.
* Tutti gli eventi vengono inviati finché il visitatore non rinuncia.
* Dopo la rinuncia, il Web SDK interrompe l’invio di eventi, ma i cookie esistenti rimangono.

## Consenso con gli ID dispositivo di prime parti {#consent-with-fpids}

Se la tua implementazione utilizza [ID dispositivo di prime parti (FPID)](./fpid.md), il cookie FPID viene impostato dal server indipendentemente dallo stato del consenso di Web SDK. Il cookie FPID è un identificatore che gestisci sulla tua infrastruttura. Tuttavia, l’FPID viene inviato all’Edge Network solo quando il Web SDK effettua una richiesta (che viene gestita dal consenso):

* Con `defaultConsent: "pending"`, l&#39;FPID esiste nel browser ma non viene utilizzato per il seeding di un ECID fino a quando non viene concesso il consenso.
* Con `defaultConsent: "in"`, l&#39;FPID viene utilizzato alla prima richiesta e avvia immediatamente l&#39;ECID.

Se l’implementazione del consenso richiede che nessun identificatore sia impostato prima del consenso, ritarda l’impostazione del cookie FPID fino alla comunicazione del consenso. Il solo controllo del consenso del Web SDK non impedisce l’impostazione del cookie FPID, in quanto è gestito dal server.

## Insidie comuni {#common-pitfalls}

+++**Il banner di consenso cancella i cookie di identità**

**Problema**: alcune piattaforme di gestione del consenso (CMP) cancellano tutti i cookie, inclusi `kndctr_` cookie di identità, durante la presentazione del banner di consenso, prima che il visitatore faccia una scelta. Quando il visitatore concede il consenso, il Web SDK genera un nuovo ECID perché il precedente è stato eliminato. Il visitatore viene visualizzato come una nuova persona nel reporting.

**Sintomi**:
* Un picco nel numero di visitatori univoci dopo la distribuzione di un banner di consenso.
* I visitatori di ritorno vengono conteggiati come nuovi visitatori ogni volta che scade il loro consenso e interagiscono nuovamente con il banner.

**Soluzione**: configurare CMP per mantenere i cookie `kndctr_`. Questi cookie sono cookie di identità, non di tracciamento dei cookie, identificano il dispositivo e non contengono dati comportamentali. Se la tua CMP richiede la cancellazione dei cookie, aggiungi `kndctr_` cookie con prefisso a un elenco di esclusione. In alternativa, ritarda la cancellazione dei cookie fino a quando il visitatore nega esplicitamente il consenso, anziché cancellarli preventivamente.

+++

+++**Il ritardo nel consenso causa la duplicazione dell&#39;identità**

**Problema**: quando `defaultConsent` è impostato su `pending`, Web SDK attende il consenso prima di inviare i dati. Se il consenso viene concesso in una fase tardiva del ciclo di vita della pagina (ad esempio, dopo un’interazione del banner che attiva un ricaricamento della pagina), la sequenza seguente può causare problemi:

1. Caricamento della pagina. `defaultConsent: "pending"`. Web SDK non invia richieste.
2. Il visitatore concede il consenso. CMP attiva il ricaricamento della pagina.
3. La pagina viene caricata di nuovo. Web SDK viene inizializzato con il consenso ora concesso e genera un ECID.

Questo flusso è normale e funziona correttamente. Il problema si verifica quando la CMP o la tua implementazione cancella inavvertitamente i cookie tra i passaggi 2 e 3 o quando il Web SDK viene configurato in modo diverso al ricaricamento.

**Soluzione**: verificare che la configurazione del Web SDK (in particolare `orgId` e `defaultConsent`) sia identica a ogni caricamento di pagina. Se la CMP attiva un ricaricamento dopo il consenso, verifica che i cookie di identità sopravvivano al ricaricamento.

+++

+++**Utilizzo di `defaultConsent: "in"` con un banner di consenso**

**Problema**: alcune implementazioni impostano `defaultConsent: "in"` e quindi chiamano `setConsent` con `"general": "out"` se il visitatore rifiuta. Questo approccio genera un ECID e invia almeno una richiesta prima che il consenso venga negato. A seconda dei requisiti normativi, questa raccolta dati iniziale potrebbe non essere in linea con l’informativa sulla privacy della tua organizzazione.

**Soluzione**: se l&#39;ambiente normativo richiede il consenso prima di qualsiasi raccolta dati o generazione ECID, utilizzare `defaultConsent: "pending"`. Questa impostazione assicura che il Web SDK non comunichi con Edge Network fino a quando non viene esplicitamente concesso il consenso.

+++
