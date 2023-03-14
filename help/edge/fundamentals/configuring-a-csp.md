---
title: Configurazione di un CSP
seo-title: Configuring a CSP for Adobe Experience Platform Web SDK
description: Scopri come configurare una CSP per l’SDK per web di Experience Platform
seo-description: Learn how to configure a CSP for the Experience Platform Web SDK
keywords: configurazione;configurazione;SDK;edge;Web SDK;configurare;contesto;web;dispositivo;ambiente;impostazioni web sdk;informativa sulla sicurezza dei contenuti;
exl-id: 661d0001-9e10-479e-84c1-80e58f0e9c0b
source-git-commit: 0085306a2f5172eb19590cc12bc9645278bd2b42
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 2%

---

# Configurazione di un CSP

A [Informativa sulla sicurezza dei contenuti](https://developer.mozilla.org/it-IT/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP) viene utilizzato per limitare le risorse che un browser può utilizzare. I CSP possono anche limitare la funzionalità delle risorse di script e di stile. Adobe Experience Platform Web SDK non richiede un CSP, ma l’aggiunta di un CSP può ridurre la superficie di attacco per prevenire attacchi dannosi.

I CSP devono riflettere come [!DNL Platform Web SDK] è implementato e configurato. I CSP seguenti mostrano le modifiche necessarie per il corretto funzionamento dell’SDK. A seconda dell’ambiente specifico, potrebbero essere necessarie ulteriori impostazioni CSP.

## Esempio di criteri per la sicurezza dei contenuti

Gli esempi seguenti mostrano come configurare un CSP.

### Consenti accesso al dominio Edge

```
default-src 'self';
connect-src 'self' EDGE-DOMAIN
```

Nell’esempio precedente, `EDGE-DOMAIN` deve essere sostituito con il dominio di prime parti. Il dominio di prime parti è configurato per [edgeDomain](configuring-the-sdk.md#edge-domain) impostazione. Se non è stato configurato alcun dominio di prima parte, `EDGE-DOMAIN` deve essere sostituito con `*.adobedc.net`. Se la migrazione dei visitatori è attivata con [idMigrationEnabled](configuring-the-sdk.md#id-migration-enabled), il `connect-src` La direttiva deve inoltre includere `*.demdex.net`.

### Utilizzare NONCE per consentire gli elementi di script e di stile in linea

[!DNL Platform Web SDK] può modificare il contenuto della pagina e deve essere approvato per creare tag di script e di stile in linea. A questo scopo, l’Adobe consiglia di utilizzare un nonce per [default-src](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/default-src) Direttiva CSP. Un nonce è un token casuale crittograficamente sicuro generato dal server e generato una volta per ogni visualizzazione di pagina univoca.

```
default-src 'nonce-SERVER-GENERATED-NONCE'
```

Inoltre, il nonce CSP deve essere aggiunto come attributo al [!DNL Platform Web SDK] [codice di base](installing-the-sdk.md#adding-the-code) tag script. [!DNL Platform Web SDK] utilizzerà quindi tale nonce quando si aggiungono tag di script o di stile in linea alla pagina:

```
<script nonce="SERVER-GENERATED-NONCE">
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

Se non si utilizza un nonce, l’altra opzione consiste nell’aggiungere `unsafe-inline` al `script-src` e `style-src` Direttive CSP:

```
script-src 'unsafe-inline'
style-src 'unsafe-inline'
```

>[!NOTE]
>
>L’Adobe fa **non** consiglia di specificare `unsafe-inline` perché consente l’esecuzione di qualsiasi script sulla pagina, il che limita i vantaggi dei CSP.
