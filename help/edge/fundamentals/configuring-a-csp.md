---
title: Configurazione di una CSP
seo-title: Configurazione di una CSP per Adobe Experience Platform Web SDK
description: 'Scopri come configurare una CSP per l’SDK Web per Experience Platform '
seo-description: 'Scopri come configurare una CSP per l’SDK Web per Experience Platform '
keywords: configurazione;configurazione;SDK;edge;Web SDK;configure;context;web;device;environment;web sdk settings;content security policy;
translation-type: tm+mt
source-git-commit: 4f07d41197add406fbdd82caee5177a1ddaa7d7e
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 2%

---


# Configurazione di una CSP

Per limitare le risorse consentite da un browser, viene utilizzato un [Content Security Policy](https://developer.mozilla.org/it-IT/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP). La CSP può anche limitare le funzionalità delle risorse di script e stili. Adobe Experience Platform Web SDK non richiede una CSP, ma l&#39;aggiunta di una CSP può ridurre la superficie di attacco per prevenire attacchi dannosi.

La CSP deve riflettere il modo in cui [!DNL Platform Web SDK] viene distribuito e configurato. La seguente CSP mostra quali modifiche potrebbero essere necessarie per il corretto funzionamento dell’SDK. È probabile che saranno necessarie ulteriori impostazioni CSP, a seconda dell&#39;ambiente specifico.

## Esempio di criteri di protezione dei contenuti

Gli esempi seguenti mostrano come configurare una CSP.

### Consenti accesso al dominio periferico

```
default-src 'self';
connect-src 'self' EDGE-DOMAIN
```

Nell&#39;esempio precedente, `EDGE-DOMAIN` deve essere sostituito con il dominio di prime parti. Il dominio di prime parti è configurato per l&#39;impostazione [edgeDomain](configuring-the-sdk.md#edge-domain). Se non è stato configurato alcun dominio di prime parti, `EDGE-DOMAIN` deve essere sostituito con `*.adobedc.net`. Se la migrazione dei visitatori è attivata utilizzando [idMigrationEnabled](configuring-the-sdk.md#id-migration-enabled), la direttiva `connect-src` deve includere anche `*.demdex.net`.

### Usa NONCE per consentire l&#39;allineamento degli elementi di script e di stile

[!DNL Platform Web SDK] può modificare il contenuto della pagina e deve essere approvato per creare script in linea e tag di stile. A questo scopo,  Adobe consiglia di utilizzare un nonce per la direttiva CSP [default-src](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/default-src). Un nonce è un token casuale crittografato generato dal server che viene generato una volta per ogni visualizzazione di pagina univoca.

```
default-src 'nonce-SERVER-GENERATED-NONCE'
```

Inoltre, la voce CSP deve essere aggiunta come attributo al tag script [!DNL Platform Web SDK] [base code](installing-the-sdk.md#adding-the-code). [!DNL Platform Web SDK] utilizzerà quindi tale nonce quando si aggiungono tag di script o di stile in linea alla pagina:

```
<script nonce="SERVER-GENERATED-NONCE">
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

Se non viene utilizzata una nonce, l&#39;altra opzione consiste nell&#39;aggiungere `unsafe-inline` alle direttive `script-src` e `style-src` CSP:

```
script-src 'unsafe-inline'
style-src 'unsafe-inline'
```

>[!NOTE]
>
> Adobe **not** consiglia di specificare `unsafe-inline` perché consente l&#39;esecuzione di qualsiasi script sulla pagina, limitando i vantaggi della CSP.
