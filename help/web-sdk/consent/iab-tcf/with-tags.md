---
title: Integrare il supporto IAB TCF 2.0 utilizzando i tag e l’estensione Platform Web SDK
description: Scopri come impostare il consenso IAB TCF 2.0 con i tag e l’estensione Adobe Experience Platform Web SDK.
exl-id: dc0e6b68-8257-4862-9fc4-50b370ef204f
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---

# Integrare il supporto IAB TCF 2.0 utilizzando i tag e l’estensione Platform Web SDK

Adobe Experience Platform Web SDK supporta Interactive Advertising Bureau Transparency &amp; Consent Framework, versione 2.0 (IAB TCF 2.0). Questa guida illustra come impostare una proprietà tag per inviare informazioni sul consenso IAB TCF 2.0 ad Adobe utilizzando l’estensione tag Adobe Experience Platform Web SDK.

Se non desideri utilizzare i tag, consulta la guida in [Utilizzo di IAB TCF 2.0 senza tag](./without-tags.md).

## Introduzione

Per utilizzare IAB TCF 2.0 con i tag e l’estensione Platform Web SDK, è necessario disporre di uno schema XDM e di un set di dati.

Inoltre, questa guida richiede una buona conoscenza di Adobe Experience Platform Web SDK. Per un rapido aggiornamento, leggere la [panoramica di Adobe Experience Platform Web SDK](../../home.md) e la [documentazione sulle domande frequenti](../../faq.md).

## Impostazione del consenso predefinito

Nella configurazione dell’estensione è presente un’impostazione per il consenso predefinito. Questo controlla il comportamento dei clienti che non hanno un cookie di consenso. Se desideri mettere in coda eventi esperienza per i clienti che non hanno un cookie di consenso, imposta questo su `pending`. Se desideri eliminare gli eventi esperienza per i clienti che non hanno un cookie di consenso, imposta questo su `out`. Puoi anche utilizzare un elemento dati per impostare dinamicamente il valore del consenso predefinito. Per ulteriori informazioni, vedere [`defaultConsent`](/help/web-sdk/commands/configure/defaultconsent.md).

## Aggiornamento del profilo con le informazioni sul consenso {#consent-code-1}

Per chiamare l&#39;azione [`setConsent`](/help/web-sdk/commands/setconsent.md) quando le preferenze di consenso dei clienti sono cambiate, crea una regola di tag. Per iniziare, aggiungi un nuovo evento e scegli il tipo di evento &quot;Custom Code&quot; dell’estensione Core.

Utilizza il seguente esempio di codice per il nuovo evento:

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

Questo codice personalizzato esegue due operazioni:

* Imposta due elementi dati, uno con la stringa di consenso e uno con il flag `gdprApplies`. Ciò è utile in un secondo momento durante la compilazione dell’azione &quot;Imposta consenso&quot;.

* Attiva la regola quando le preferenze di consenso sono cambiate. Utilizza l’azione &quot;Imposta consenso&quot; ogni volta che le preferenze di consenso vengono modificate. Aggiungi un’azione &quot;Imposta consenso&quot; nell’estensione e compila il modulo come segue:

* Standard: &quot;IAB TCF&quot;
* Versione: &quot;2.0&quot;
* Valore: &quot;%IAB TCF Consent String%&quot;
* Si applica il RGPD: &quot;%IAB TCF Consent RGPD%&quot;

![Azione impostazione consenso IAB](../../assets/consent/iab-tcf/with-launch/iab-action.png)

>[!IMPORTANT]
>
>Non puoi scegliere questi elementi dati utilizzando il selettore degli elementi dati perché sono stati creati tramite codice personalizzato. Digita il nome dell’elemento dati con i segni di percentuale. Questo codice aggiorna il profilo del cliente con le nuove preferenze di consenso ogni volta che cambia. Inoltre, il server restituisce un valore cookie che potrebbe impedire a Adobe Experience Platform Web SDK di registrare eventi esperienza.

## Creazione di un elemento dati XDM per eventi esperienza

La stringa di consenso deve essere inclusa nell’evento esperienza XDM. A questo scopo, utilizza l’elemento dati Oggetto XDM. Inizia creando un nuovo elemento dati Oggetto XDM o, in alternativa, utilizzane uno già creato per l’invio di eventi. Se hai aggiunto il gruppo di campi dello schema Privacy dell’evento esperienza allo schema, dovresti disporre di una chiave `consentStrings` nell’oggetto XDM.

1. Seleziona **[!UICONTROL consentStrings]**.

1. Scegliere **[!UICONTROL Fornisci singoli elementi]** e selezionare **[!UICONTROL Aggiungi elemento]**.

1. Espandi l&#39;intestazione **[!UICONTROL consentString]**, espandi il primo elemento e compila i seguenti valori:

* `consentStandard`: IAB TCF
* `consentStandardVersion`: 2,0
* `consentStringValue`: %IAB TCF stringa di consenso%
* `gdprApplies`: %IAB TCF consenso RGPD%

>[!IMPORTANT]
>
>Non puoi scegliere questi elementi dati utilizzando il selettore degli elementi dati perché sono stati creati tramite codice personalizzato. Digita il nome dell’elemento dati con i segni di percentuale.

## Invio di un evento esperienza iniziale con informazioni sul consenso IAB TCF 2.0

Se l’evento esperienza iniziale sulla pagina viene attivato con un evento di caricamento pagina, la stringa di consenso potrebbe non essere ancora stata caricata. Questa regola ha lo scopo di sostituire l&#39;evento di caricamento pagina corrente. Per assicurarti che le informazioni sul consenso siano caricate per prime, crea una nuova regola e aggiungi il seguente codice come evento di codice personalizzato:

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

Questo codice è identico al codice personalizzato precedente, con la differenza che vengono gestiti sia gli eventi `useractioncomplete` che `tcloaded`. Il [codice personalizzato precedente](#consent-code-1) viene attivato solo quando il cliente sceglie le proprie preferenze per la prima volta. Questo codice si attiva anche quando il cliente ha già scelto le proprie preferenze. Ad esempio, al secondo caricamento della pagina.

Aggiungi un’azione &quot;Invia evento&quot; dall’estensione Platform Web SDK. All’interno del campo XDM, scegli l’elemento dati XDM creato nella sezione precedente.

## Invio di altri eventi con informazioni sul consenso IAB TCF 2.0

Quando gli eventi vengono attivati dopo l’evento esperienza iniziale, i due elementi di dati sono ancora definiti e possono essere utilizzati per inviare le informazioni sul consenso IAB. Utilizza lo stesso elemento dati XDM per inviare eventi futuri. Sono incluse le informazioni IAB TCF 2.0.

## Passaggi successivi

Ora che hai imparato a utilizzare IAB TCF 2.0 con l’estensione Platform Web SDK, puoi anche scegliere di integrarla con altre soluzioni di Adobe come Adobe Analytics o Adobe Real-time Customer Data Platform. Per ulteriori informazioni, consulta la [panoramica su IAB Transparency &amp; Consent Framework 2.0](./overview.md).
