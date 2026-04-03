---
title: idMigrationEnabled
description: Consente al Web SDK di leggere i cookie AMCV.
exl-id: 33b9d645-0fbe-4fe4-8847-e6f9e78557b6
source-git-commit: bf0bb72777cacd822fd6e887ac3ef71764784214
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---

# `idMigrationEnabled`

La proprietà `idMigrationEnabled` consente al Web SDK di leggere i cookie AMCV impostati da implementazioni Adobe Experience Cloud precedenti. Se l’organizzazione aggiorna l’implementazione al Web SDK, questa impostazione consente una transizione più fluida al servizio Adobe Experience Cloud ID corrente. Questa impostazione è utile per evitare un netto aumento dei visitatori univoci durante l&#39;aggiornamento al Web SDK.

Se l’organizzazione esegue una nuova implementazione di Web SDK, l’abilitazione di questa impostazione non ha alcun impatto sulla raccolta dei dati o sull’identificazione dei visitatori. Non ci sono svantaggi a lasciarla abilitata per tutte le implementazioni.

## Come funziona la migrazione delle identità {#how-it-works}

L&#39;API visitatore memorizza l&#39;Experience Cloud ID (ECID) in un cookie denominato `AMCV_<ORG_ID>`. Quando `idMigrationEnabled` è `true` (impostazione predefinita), il Web SDK legge automaticamente l&#39;ECID dal cookie AMCV e lo utilizza come identità del visitatore alla prima richiesta di Edge Network.

1. Un visitatore arriva su una pagina che ora utilizza il Web SDK invece dell’API visitatore.
1. Il Web SDK verifica la presenza di un cookie di identità `kndctr_` esistente (nel formato del cookie). Se non ne viene trovato alcuno, cerca un cookie `AMCV_`.
1. Se viene trovato un cookie `AMCV_`, Web SDK estrae l&#39;ECID e lo utilizza per inizializzare l&#39;identità del visitatore.
1. Il Web SDK imposta un nuovo cookie di identità `kndctr_` con lo stesso ECID.
1. Nelle visite successive, il Web SDK utilizza direttamente il cookie `kndctr_`. Il cookie `AMCV_` non è più necessario.

Affinché la migrazione funzioni, il Web SDK deve essere configurato con lo stesso [`orgId`](/help/collection/js/commands/configure/orgid.md) utilizzato dall&#39;API visitatore e deve essere distribuito sullo stesso dominio (o su un sottodominio dello stesso dominio padre) in cui è stato impostato il cookie AMCV.

## Scenari di migrazione supportati

La migrazione degli ID supporta i seguenti modelli di transizione:

* **Alcune pagine utilizzano ancora l&#39;API Visitor, mentre altre utilizzano il Web SDK**: SDK legge i cookie AMCV esistenti e scrive un nuovo cookie con l&#39;ECID esistente. Scrive anche i cookie AMCV in modo che le pagine che utilizzano ancora l’API visitatore continuino a riconoscere lo stesso visitatore.
* **Web SDK e API visitatore sono entrambi presenti nella stessa pagina**: se il cookie AMCV non è impostato, SDK cerca l&#39;API visitatore nella pagina e la utilizza per ottenere l&#39;ECID.
* **Il sito è stato spostato completamente in Web SDK**: è possibile lasciare la migrazione abilitata per un periodo di tempo in modo che i visitatori basati su AMCV esistenti mantengano la continuità durante la transizione dei cookie.

>[!IMPORTANT]
>
>Non caricare contemporaneamente l’API visitatore e il Web SDK sulla stessa pagina, a meno che non sia stato confermato che il cookie AMCV è già impostato. L’esecuzione di entrambe le librerie in una singola pagina può causare race condition in cui ogni libreria tenta di gestire l’identità in modo indipendente, generando potenzialmente ECID duplicati o in conflitto.

## Disattivazione della migrazione {#turn-off-migration}

Se l&#39;intero sito viene eseguito sul Web SDK e nessun visitatore dispone di un solo cookie `AMCV_` senza il cookie `kndctr_` corrispondente, è possibile disabilitare la migrazione delle identità impostando `idMigrationEnabled` su `false`. Si tratta di una piccola ottimizzazione delle prestazioni e riduce l’area di superficie della logica di identità.

Come linea guida, attendi che sia trascorso il periodo di vita massima del cookie AMCV dopo la migrazione dell&#39;ultima pagina. Se i tuoi cookie AMCV hanno una scadenza di due anni, attendi due anni dopo che la pagina finale è stata tagliata sul Web SDK. In pratica, la maggior parte delle organizzazioni disabilita la migrazione prima (dopo alcuni mesi) e accetta una quantità trascurabile di inflazione dal numero ridotto di visitatori che ritornano per la prima volta dopo una lunga assenza.

## Aggiornamenti delle caratteristiche di Audience Manager

Quando i dati formattati XDM vengono inviati ad Audience Manager durante la migrazione, devono essere convertiti in segnali. Le caratteristiche devono essere aggiornate per riflettere le nuove chiavi fornite da XDM. Questo processo è semplificato utilizzando lo strumento [BAAAM](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html?lang=it#getting-started-with-bulk-management).

## Migrazione degli ID di terze parti {#third-party-id}

Se l&#39;implementazione dell&#39;API Visitor ha utilizzato ID di terze parti (cookie `demdex.net`), anche Web SDK può migrarli. Configurare [`thirdPartyCookiesEnabled`](/help/collection/js/commands/configure/thirdpartycookiesenabled.md) in `true` nella configurazione Web SDK. Il SDK web legge il cookie demdex esistente e include l’identità di terze parti nelle sue richieste Edge Network, seguendo lo stesso modello di migrazione del cookie AMCV.

## Convalida {#validation}

Per verificare che la migrazione delle identità funzioni correttamente:

1. Apri una pagina che in precedenza utilizzava l&#39;API visitatore (ora tramite Web SDK) in un browser che ha un cookie `AMCV_` esistente.
2. Negli strumenti per sviluppatori, verificare che sia stato impostato un cookie di identità `kndctr_` e che l&#39;ECID corrisponda a quello nel cookie `AMCV_`.
3. Dopo la distribuzione, confronta i conteggi di visitatori univoci prima e dopo la migrazione per lo stesso periodo di tempo. Un picco significativo di visitatori univoci può indicare che la migrazione non porta avanti le identità.

>[!TIP]
>
>Utilizza `getIdentity` per recuperare in modo programmatico l&#39;ECID per il confronto:
>
>```js
>alloy("getIdentity", { namespaces: ["ECID"] }).then(function(result) {
>   console.log("ECID:", result.identity.ECID);
>});
>```

## Configurare `idMigrationEnabled` {#configure}

Impostare il valore booleano `idMigrationEnabled` durante l&#39;esecuzione del comando `configure`. Se si omette questa proprietà durante la configurazione del Web SDK, per impostazione predefinita viene utilizzato `true`. Imposta questa proprietà se vuoi disabilitare la capacità di leggere i cookie AMCV impostati dall&#39;API visitatore. La maggior parte delle organizzazioni non deve impostare questa proprietà.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  idMigrationEnabled: false
});
```

## Abilitare la migrazione degli ID visitatore tramite l’estensione tag Web SDK

Queste impostazioni possono essere configurate nell&#39;estensione tag Web SDK utilizzando [Impostazioni di configurazione identità](/help/tags/extensions/client/web-sdk/configure/identity.md).
