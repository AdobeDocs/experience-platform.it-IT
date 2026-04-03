---
title: Condividere l’identità dalle app mobili al web/webViews per dispositivi mobili
description: Passa l’identità da un’app mobile a contenuti web per dispositivi mobili o a un WebView, in modo che la generazione rapporti e la personalizzazione possano continuare nel contesto web.
source-git-commit: bf0bb72777cacd822fd6e887ac3ef71764784214
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# Condividere l’identità dalle app mobili al web/webViews per dispositivi mobili

Quando un visitatore si sposta da un’app mobile a una pagina Web Web WebView o mobile, l’app e i contesti web mantengono ognuno la propria identità. Senza un handoff esplicito, l’esperienza web tratta il visitatore come una persona nuova e sconosciuta, che frammenta il reporting e riavvia la personalizzazione.

La condivisione di identità da dispositivo mobile a Web risolve questo problema passando il [ID Experience Cloud (ECID)](./overview.md) del visitatore dall&#39;app mobile alla destinazione Web tramite un parametro della stringa di query `adobe_mc`. Il parametro contiene l’ECID, l’ID organizzazione Experience Cloud e una marca temporale. Quando la destinazione Web viene caricata con un parametro `adobe_mc` valido, il Web SDK lo legge automaticamente e applica l&#39;identità consegnata alla sua prima richiesta Edge Network, in modo che entrambi i contesti condividano lo stesso visitatore.

Utilizza questo modello quando l’app mobile apre una pagina Web Web WebView o mobile controllata dalla tua organizzazione e desideri che l’attività dell’app e l’attività web rimangano associate allo stesso visitatore. Se l&#39;obiettivo è la continuità delle identità tra siti Web di domini diversi, utilizza invece [condivisione tra domini diversi](cross-domain-sharing.md).

## Prerequisiti

Prima di iniziare, assicurati che l’implementazione soddisfi i seguenti requisiti:

* **App mobile**: SDK Adobe Experience Platform Mobile con [Identità per Edge Network](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/) versione estensione **1.1.0 o successiva** (iOS e Android).
* **Destinazione Web**: [Web SDK](/help/collection/js/js-overview.md) versione **2.11.0 o successiva** o estensione tag Web SDK.
* **Controllo URL**: il codice controlla l&#39;URL passato dall&#39;app al WebView o al browser in modo che sia possibile accodare parametri di stringa di query.
* **Configurazione corrispondente**: lo stesso ID organizzazione Experience Cloud è configurato sia nelle implementazioni per dispositivi mobili che in quelle web.

## Recuperare l’identità dall’app mobile {#retrieve-identity}

Utilizzare l&#39;API [`getUrlVariables`](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#geturlvariables) dall&#39;estensione Identity for Edge Network per recuperare l&#39;identità del visitatore come stringa di query. È quindi possibile aggiungere la stringa all&#39;URL prima di aprire WebView o il browser.

La stringa restituita contiene i seguenti parametri con codifica URL:

| Parametro | Descrizione |
| --- | --- |
| `MCID` | L’Experience Cloud ID (ECID). |
| `MCORGID` | L&#39;ID organizzazione Experience Cloud. Questo parametro deve corrispondere all’organizzazione configurata nel Web SDK nella pagina di destinazione. |
| `TS` | Una marca temporale. La destinazione deve ricevere questo valore entro **cinque minuti** oppure il passaggio di consegne è stato rifiutato. |

Gli esempi di codice seguenti mostrano l’aspetto di un handoff nell’app mobile:

>[!BEGINTABS]

>[!TAB Swift (iOS)]

```swift
Identity.getUrlVariables { (urlVariables, error) in
    if let error = error {
        // Handle the error
        return
    }

    guard let urlVariables = urlVariables else { return }

    // Construct the full URL by appending the identity query string
    if let url = URL(string: "https://example.com/webapp?\(urlVariables)") {
        // Open the URL in a WebView or browser
        let request = URLRequest(url: url)
        webView.load(request)
    }
}
```

>[!TAB Cotlino (Android)]

```kotlin
Identity.getUrlVariables { urlVariables ->
    if (urlVariables != null) {
        // Construct the full URL by appending the identity query string
        val url = "https://example.com/webapp?$urlVariables"

        // Open the URL in a WebView or browser
        webView.loadUrl(url)
    }
}
```

>[!ENDTABS]

## Ricevi identità sul lato web {#receive-identity}

Non è richiesto alcun codice aggiuntivo nella destinazione web. Quando il Web SDK è presente nella pagina e l&#39;URL contiene un parametro `adobe_mc` valido, SDK estrae automaticamente l&#39;ECID e lo applica alla mappa di identità del visitatore alla prima richiesta di Edge Network.

Se la destinazione Web utilizza l&#39;estensione tag Web SDK e devi reindirizzare il visitatore a un&#39;altra pagina mantenendo l&#39;identità, utilizza l&#39;azione [Reindirizza con identità](/help/tags/extensions/client/web-sdk/actions/redirect-with-identity.md) per inoltrare il parametro `adobe_mc` alla pagina successiva.

>[!NOTE]
>
>Il parametro `adobe_mc` scade dopo **cinque minuti**. Assicurati che la destinazione web carichi e invii la sua prima richiesta Edge Network subito dopo l’apertura dell’URL.
