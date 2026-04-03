---
title: defaultConsent
description: Imposta il metodo predefinito di raccolta dei consensi per la proprietà web.
exl-id: 2a22fa8b-a234-4d3e-9b55-c7482a928fe6
source-git-commit: bf0bb72777cacd822fd6e887ac3ef71764784214
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---


# `defaultConsent`

La proprietà `defaultConsent` determina la modalità di gestione del consenso alla raccolta dati prima di chiamare il comando [`setConsent`](../setconsent.md). Questa proprietà è utile quando non desideri raccogliere accidentalmente dati da individui residenti in aree in cui è richiesto il consenso prima di raccogliere i dati.

Se un visitatore non rientra nella giurisdizione del Regolamento generale sulla protezione dei dati (RGPD), il consenso predefinito può essere impostato su `in`. Per i visitatori all&#39;interno della giurisdizione del RGPD il consenso predefinito potrebbe essere impostato su `pending`. La piattaforma di gestione del consenso (CMP) è in grado di rilevare l&#39;area geografica del cliente e fornire il flag `gdprApplies` a IAB TCF 2.0. Questo flag può essere utilizzato per impostare il consenso predefinito.

Impostare la proprietà stringa `defaultConsent` sul livello di consenso desiderato durante l&#39;esecuzione del comando `configure`. Questa proprietà fa distinzione tra maiuscole e minuscole e supporta solo i tre valori seguenti: `"in"`, `"out"` e `"pending"`. Se tenti di utilizzare un altro valore, la libreria genera un errore. Se non è impostato nel comando `configure`, il valore predefinito è **`in`**.

>[!IMPORTANT]
>
>Il valore `defaultConsent` non persiste tra un caricamento di pagina e l&#39;altro. Assicurarsi di impostare il consenso predefinito desiderato ogni volta che si chiama il comando `configure`. Al contrario, il consenso risolto di un visitatore (impostato tramite [`setConsent`](../setconsent.md)) viene mantenuto in un cookie e applicato automaticamente ai caricamenti delle pagine successive.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  defaultConsent: "pending"
});
```

* **`in`**: la raccolta dati funziona normalmente finché l&#39;utente non rinuncia.
* **`out`**: i dati vengono eliminati definitivamente fino al consenso dell&#39;utente.
* **`pending`**: i dati vengono archiviati localmente finché l&#39;utente non acconsente utilizzando il comando [`setConsent`](../setconsent.md).

>[!NOTE]
>
>Anche se Adobe prevede di creare un set più solido di finalità o categorie corrispondenti alle funzionalità e alle offerte di prodotti di Adobe, l’implementazione corrente è un approccio &quot;tutto o niente&quot; all’opt-in. Questa limitazione si applica solo al Web SDK e non ad altre librerie Adobe JavaScript.

## Utilizzo di `defaultConsent` insieme a `setConsent` {#using-consent}

Se utilizzati insieme, `defaultConsent` e `setConsent` producono una raccolta di dati, un&#39;impostazione dei cookie e risultati di identità diversi a seconda dei valori configurati. Per una tabella di interazione completa, consulta [Consenso e identità nella raccolta dati](/help/collection/identity/consent.md#how-consent-affects-identity).

## Impostazione del consenso predefinito in base a `gdprApplies`

Alcune CMP consentono di determinare se al cliente si applica il Regolamento generale sulla protezione dei dati (RGPD). Se desideri presumere il consenso per i clienti a cui non si applica il RGPD, puoi utilizzare il flag `gdprApplies` in una chiamata API TCF. Ad esempio:

```js
var alloyConfiguration = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    alloyConfiguration.defaultConsent = tcData.gdprApplies ? "pending" : "in";
    window.alloy("configure", alloyConfiguration);
  }
});
```

Nel blocco di codice precedente, il comando `configure` viene chiamato dopo che `tcData` è stato ottenuto dall&#39;API TCF. Se `gdprApplies` è true, il consenso predefinito è impostato su `pending`. Se `gdprApplies` è false, il consenso predefinito è impostato su `in`. Assicurarsi di compilare la variabile `alloyConfiguration` con la configurazione.

## Consenso predefinito tramite l’estensione tag Web SDK

Per informazioni su come eseguire queste azioni utilizzando i tag, consulta le [impostazioni di consenso](/help/tags/extensions/client/web-sdk/configure/consent.md) nella documentazione dell&#39;estensione tag di Web SDK.
