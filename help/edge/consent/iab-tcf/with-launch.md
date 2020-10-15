---
title: Utilizzo di IAB TCF 2.0 con Experience Platform Launch
seo-title: Impostazione del consenso IAB TCF 2.0 con  Adobe Experience Platform Launch e Adobe Experience Platform Web SDK
description: Scopri come impostare il consenso IAB TCF 2.0 con  Adobe Experience Platform Launch e Adobe Experience Platform Web SDK
seo-description: Scopri come impostare il consenso IAB TCF 2.0 con  Adobe Experience Platform Launch e Adobe Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: db742119d8f169817080f1fd4e0dc08a0f0faa47
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 0%

---


# Utilizzo di IAB TCF 2.0 con Experience Platform Launch e estensione AEP Web SDK

Adobe Experience Platform Web Software Development Kit (Adobe Experience Platform Web SDK) supporta Interactive Advertising Bureau Transparency &amp; Consent Framework, versione 2.0 (IAB TCF 2.0). Questa guida mostra come impostare una proprietà Adobe Experience Platform Launch  per l&#39;invio di informazioni di consenso IAB TCF 2.0 a  Adobe tramite l&#39;estensione AEP Web SDK per Experience Platform Launch.

Se non si desidera utilizzare il Experience Platform Launch, fare riferimento alla guida sull&#39; [utilizzo di IAB TCF 2.0 senza Experience Platform Launch](./without-launch.md).

## Introduzione

Per utilizzare IAB TCF 2.0 con Experience Platform Launch e estensione AEP Web SDK, è necessario disporre di uno schema XDM e di un set di dati. Se non avete impostato nessuno di questi, prima di continuare, visualizzate la guida di avvio rapido di Adobe Experience Platform Web SDK.

Inoltre, questa guida richiede una buona conoscenza dell’SDK Web per Adobe Experience Platform. Per un aggiornamento rapido, consulta la panoramica [](../../home.md) Adobe Experience Platform Web SDK e la documentazione sulle domande [](../../web-sdk-faq.md) frequenti.

## Impostazione del consenso predefinito

Nella configurazione dell&#39;estensione è presente un&#39;impostazione per il consenso predefinito. Questo controlla il comportamento dei clienti che non dispongono di un cookie di consenso. Se desiderate mettere in coda gli Eventi esperienza per i clienti che non dispongono di un cookie di consenso, impostate questa opzione su `pending`.

>[!NOTE]
>
>Al momento, non è possibile impostare questo valore in modo dinamico tramite l&#39;estensione del Experience Platform Launch.

Per ulteriori informazioni sul consenso predefinito, consulta la sezione relativa al consenso [predefinito](../../fundamentals/configuring-the-sdk.md#default-consent) nella documentazione di configurazione dell’SDK.

## Aggiornamento del profilo con informazioni di consenso {#consent-code-1}

Per richiamare l’azione quando i clienti hanno modificato le preferenze di consenso, è necessario creare una nuova regola di Experience Platform Launch. `setConsent` Per iniziare, aggiungete un nuovo evento e scegliete il tipo di evento &quot;Codice personalizzato&quot; dell&#39;estensione Core.

Utilizzate il seguente esempio di codice per il nuovo evento:

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

* Imposta due elementi di dati, uno con la stringa di consenso e uno con il `gdprApplies` flag. Questa funzione è utile in un secondo momento quando si compila l’azione &quot;Imposta consenso&quot;.

* Attiva la regola quando le preferenze di consenso sono cambiate. L&#39;azione &quot;Imposta consenso&quot; deve essere utilizzata ogni volta che le preferenze di consenso sono cambiate. Aggiungere un&#39;azione &quot;Imposta consenso&quot; nell&#39;estensione e compilare il modulo come segue:

* Standard: &quot;IAB TCF&quot;
* Versione: &quot;2.0&quot;
* Valore: &quot;%IAB Stringa di consenso TCF%&quot;
* GDPR si applica: &quot;%IAB TCF Consenso GDPR%&quot;

![Azione di consenso per i set IAB](../../../assets/iab_set_consent_action.png)

>[!IMPORTANT]
>
>Non è possibile scegliere questi elementi di dati utilizzando il selettore degli elementi di dati perché sono stati creati tramite codice personalizzato. È necessario digitare nel nome dell&#39;elemento dati i segni di percentuale. Questo codice aggiorna il profilo del cliente con le nuove preferenze di consenso ogni volta che viene modificato. Inoltre, il server restituisce un valore di cookie che potrebbe impedire all’SDK Web per Adobe Experience Platform di registrare eventi esperienza.

## Creazione di un elemento dati XDM per gli eventi di esperienza

La stringa di consenso deve essere inclusa nell&#39;evento esperienza XDM. A tal fine, utilizzare l&#39;elemento dati dell&#39;oggetto XDM. Per iniziare, creare un nuovo elemento dati oggetto XDM oppure utilizzare uno già creato per inviare gli eventi. Se hai aggiunto il mixin Experience Event Privacy allo schema, devi avere una `consentStrings` chiave nell&#39;oggetto XDM.

1. Seleziona **[!UICONTROL consentStrings]**.

1. Scegliete **[!UICONTROL Provide individual items]** e selezionate **[!UICONTROL Add Item]**.

1. Espandete l’ **[!UICONTROL consentString]** intestazione, espandete il primo elemento, quindi inserite i seguenti valori:

* `consentStandard`: IAB TCF
* `consentStandardVersion`: 2.0
* `consentStringValue`: %IAB Stringa di consenso TCF%
* `gdprApplies`: %IAB TCF Consenso GDPR%

>[!IMPORTANT]
>
>Non è possibile scegliere questi elementi di dati utilizzando il selettore degli elementi di dati perché sono stati creati tramite codice personalizzato. È necessario digitare nel nome dell&#39;elemento dati i segni di percentuale.

## Invio di un evento esperienza iniziale con le informazioni di consenso di IAB TCF 2.0

Se l&#39;evento esperienza iniziale nella pagina viene attivato con un evento di caricamento della pagina, la stringa di consenso potrebbe non essere ancora stata caricata. Questa regola è destinata a sostituire l&#39;evento di caricamento della pagina corrente. Per essere certi che le informazioni sul consenso vengano caricate per prime, create una nuova regola e aggiungete il codice seguente come evento di codice personalizzato:

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

Questo codice è identico al codice personalizzato precedente, con la differenza che vengono gestiti sia `useractioncomplete` gli `tcloaded` eventi che Il codice [personalizzato](#consent-code-1) precedente viene attivato solo quando il cliente sceglie per la prima volta le proprie preferenze. Questo codice viene attivato anche quando il cliente ha già scelto le proprie preferenze. Ad esempio, al secondo caricamento della pagina.

Aggiungete un&#39;azione &quot;Invia evento&quot; dall&#39;estensione Adobe Experience Platform Web SDK. All&#39;interno del campo XDM, scegliete l&#39;elemento dati XDM creato nella sezione precedente.

## Invio di altri eventi con informazioni di consenso IAB TCF 2.0

Quando gli eventi vengono attivati dopo l’evento esperienza iniziale, i due elementi di dati sono ancora definiti e possono essere utilizzati per inviare le informazioni di consenso IAB. Utilizzate lo stesso elemento dati XDM per inviare eventi futuri. Sono incluse le informazioni IAB TCF 2.0.

## Passaggi successivi

Ora che hai imparato a utilizzare IAB TCF 2.0 con l&#39;estensione Adobe Experience Platform Web SDK, puoi anche scegliere di integrarsi con altre soluzioni  Adobe come  Adobe Analytics o la piattaforma dati cliente in tempo reale. Per ulteriori informazioni, consulta [la panoramica](./overview.md) IAB Transparency &amp; Consent Framework 2.0.
