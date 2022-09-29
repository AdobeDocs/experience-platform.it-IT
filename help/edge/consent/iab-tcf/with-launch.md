---
title: Integrare il supporto IAB TCF 2.0 utilizzando i tag e l’estensione Platform Web SDK
description: Scopri come impostare il consenso IAB TCF 2.0 con i tag e l’estensione Adobe Experience Platform Web SDK.
exl-id: dc0e6b68-8257-4862-9fc4-50b370ef204f
source-git-commit: f5270d1d1b9697173bc60d16c94c54d001ae175a
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 0%

---

# Integrare il supporto IAB TCF 2.0 utilizzando i tag e l’estensione Platform Web SDK

Adobe Experience Platform Web SDK supporta il Transparency &amp; Consent Framework di Interactive Advertising Bureau, versione 2.0 (IAB TCF 2.0). Questa guida illustra come impostare una proprietà tag per l’invio ad Adobe di informazioni sul consenso IAB TCF 2.0 tramite l’estensione tag Adobe Experience Platform Web SDK.

Se non desideri utilizzare i tag, consulta la guida in [utilizzo di IAB TCF 2.0 senza tag](./without-launch.md).

## Introduzione

Per utilizzare IAB TCF 2.0 con tag e l’estensione Platform Web SDK, è necessario disporre di uno schema XDM e di un set di dati.

Inoltre, questa guida richiede una buona conoscenza di Adobe Experience Platform Web SDK. Per un rinfresco rapido, leggere il [Panoramica di Adobe Experience Platform Web SDK](../../home.md) e [Domande frequenti](../../web-sdk-faq.md) documentazione.

## Impostazione del consenso predefinito

Nella configurazione dell’estensione è presente un’impostazione per il consenso predefinito. Questo controlla il comportamento dei clienti che non dispongono di un cookie di consenso. Se desideri mettere in coda gli eventi di esperienza per i clienti che non dispongono di un cookie di consenso, imposta questo su `pending`. Se desideri eliminare gli eventi esperienza per i clienti che non dispongono di un cookie di consenso, imposta questo su `out`. Puoi anche utilizzare un elemento dati per impostare dinamicamente il valore di consenso predefinito.

Per ulteriori informazioni su come configurare il consenso predefinito, consulta la [sezione consenso predefinito](../../fundamentals/configuring-the-sdk.md#default-consent) nella guida alla configurazione dell’SDK.

## Aggiornamento del profilo con le informazioni sul consenso {#consent-code-1}

Per chiamare il `setConsent` quando le preferenze di consenso dei clienti sono cambiate, devi creare una nuova regola di tag. Inizia aggiungendo un nuovo evento e scegli il tipo di evento &quot;Custom Code&quot; dell’estensione Core.

Utilizza il seguente codice di esempio per il nuovo evento:

```javascript
// Wait for window.__tcfapi to be defined, then trigger when the customer has completed their consent and preferences.
function addEventListener() {
  if (window.__tcfapi) {
    window.__tcfapi("addEventListener", 2, function (tcData, success) {
      if (success && tcData.eventStatus === "useractioncomplete") {
        // save the tcData.tcString in a data element
        _satellite.setVar("IAB TCF Consent String", tcData.tcString);
        _satellite.setVar("IAB TCF Consent GDPR", tcData.gdprApplies);
        trigger();
      }
    });
  } else {
    // window.__tcfapi wasn't defined. Check again in 100 milliseconds
    setTimeout(addEventListener, 100);
  }
}
addEventListener();
```

Questo codice personalizzato effettua due operazioni:

* Imposta due elementi di dati, uno con la stringa di consenso e uno con il `gdprApplies` bandiera. Questa opzione è utile in un secondo momento quando si compila l’azione &quot;Imposta consenso&quot;.

* Attiva la regola quando le preferenze di consenso sono cambiate. L’azione &quot;Imposta consenso&quot; deve essere utilizzata ogni volta che le preferenze di consenso sono cambiate. Aggiungi un’azione &quot;Imposta consenso&quot; nell’estensione e compila il modulo come segue:

* Standard: &quot;IAB TCF&quot;
* Versione: &quot;2,0&quot;
* Valore: &quot;%IAB TCF Stringa di consenso%&quot;
* Il RGPD si applica: &quot;%IAB TCF Consenso RGPD%&quot;

![Azione di consenso set IAB](../../assets/consent/iab-tcf/with-launch/iab-action.png)

>[!IMPORTANT]
>
>Non puoi scegliere questi elementi dati utilizzando il selettore degli elementi dati perché sono stati creati tramite codice personalizzato. È necessario digitare il nome dell’elemento dati con i segni di percentuale. Questo codice aggiorna il profilo del cliente con le sue nuove preferenze di consenso ogni volta che cambia. Inoltre, il server restituisce un valore cookie che potrebbe impedire all’SDK Web di Adobe Experience Platform di registrare eventi Experience.

## Creazione di un elemento dati XDM per Experience Events

La stringa di consenso deve essere inclusa nell’evento esperienza XDM. A questo scopo, utilizza l’elemento dati dell’oggetto XDM. Per iniziare, crea un nuovo elemento dati oggetto XDM oppure, in alternativa, utilizza uno già creato per l’invio di eventi. Se hai aggiunto il gruppo di campi dello schema Privacy dell’evento esperienza allo schema, devi disporre di un `consentStrings` nell&#39;oggetto XDM.

1. Seleziona **[!UICONTROL permissionStrings]**.

1. Scegli **[!UICONTROL Fornire singoli elementi]** e seleziona **[!UICONTROL Aggiungi elemento]**.

1. Espandi la **[!UICONTROL permissionString]** e espandere il primo elemento, quindi inserire i seguenti valori:

* `consentStandard`: IAB TCF
* `consentStandardVersion`: 2,0
* `consentStringValue`: %IAB TCF Stringa di consenso%
* `gdprApplies`: %IAB TCF Consenso RGPD%

>[!IMPORTANT]
>
>Non puoi scegliere questi elementi dati utilizzando il selettore degli elementi dati perché sono stati creati tramite codice personalizzato. È necessario digitare il nome dell’elemento dati con i segni di percentuale.

## Invio di un evento esperienza iniziale con le informazioni di consenso IAB TCF 2.0

Se l&#39;evento esperienza iniziale sulla pagina viene attivato con un evento di caricamento della pagina, la stringa di consenso potrebbe non essere ancora stata caricata. Questa regola ha lo scopo di sostituire l&#39;evento di caricamento della pagina corrente. Per assicurarti che le informazioni sul consenso siano caricate per prime, crea una nuova regola e aggiungi il seguente codice come evento di codice personalizzato:

```javascript
// Wait for window.__tcfapi to be defined, then trigger when there is a consent string
function addEventListener() {
  if (window.__tcfapi) {
    window.__tcfapi("addEventListener", 2, function (tcData, success) {
      if (success && (tcData.eventStatus === "useractioncomplete" || tcData.eventStatus === "tcloaded")) {
        // save the tcData.tcString in a data element
        _satellite.setVar("IAB TCF Consent String", tcData.tcString);
        _satellite.setVar("IAB TCF GDPR Applies", tcData.gdprApplies);
        trigger();
      }
    });
  } else {
    // window.__tcfapi wasn"t defined. Check again in 100 milliseconds
    setTimeout(addEventListener, 100);
  }
}
addEventListener();
```

Questo codice è identico al codice personalizzato precedente, con la differenza che entrambi `useractioncomplete` e `tcloaded` gli eventi vengono gestiti. La [codice personalizzato precedente](#consent-code-1) viene attivato solo quando il cliente sceglie le proprie preferenze per la prima volta. Questo codice si attiva anche quando il cliente ha già scelto le proprie preferenze. Ad esempio, al secondo caricamento della pagina.

Aggiungi un’azione &quot;Invia evento&quot; dall’estensione Platform Web SDK. All’interno del campo XDM, scegli l’elemento dati XDM creato nella sezione precedente.

## Invio di altri eventi con le informazioni di consenso IAB TCF 2.0

Quando gli eventi vengono attivati dopo l’evento esperienza iniziale, i due elementi di dati sono ancora definiti e possono essere utilizzati per inviare le informazioni sul consenso IAB. Utilizza lo stesso elemento dati XDM per inviare eventi futuri. Sono incluse informazioni IAB TCF 2.0.

## Passaggi successivi

Ora che hai imparato a utilizzare IAB TCF 2.0 con l’estensione Platform Web SDK, puoi anche scegliere di integrarsi con altre soluzioni di Adobe come Adobe Analytics o Real-time Customer Data Platform. Consulta la sezione [Panoramica di IAB Transparency and Consent Framework 2.0](./overview.md) per ulteriori informazioni.
