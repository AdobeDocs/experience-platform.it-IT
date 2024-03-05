---
title: Configurazione di un CSP
seo-title: Configuring a CSP for Adobe Experience Platform Web SDK
description: Scopri come configurare una CSP per l’SDK per web di Experience Platform
seo-description: Learn how to configure a CSP for the Experience Platform Web SDK
keywords: configurazione;configurazione;SDK;edge;Web SDK;configurare;contesto;web;dispositivo;ambiente;impostazioni web sdk;informativa sulla sicurezza dei contenuti;
exl-id: 661d0001-9e10-479e-84c1-80e58f0e9c0b
source-git-commit: 16e49628df73d5ce97ef890dbc0a6f2c8e7de346
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Configurazione di un CSP

A [Informativa sulla sicurezza dei contenuti](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP) viene utilizzato per limitare le risorse che un browser può utilizzare. I CSP possono anche limitare la funzionalità delle risorse di script e di stile. Adobe Experience Platform Web SDK non richiede un CSP, ma l’aggiunta di un CSP può ridurre la superficie di attacco per prevenire attacchi dannosi.

I CSP devono riflettere come [!DNL Platform Web SDK] è implementato e configurato. I CSP seguenti mostrano le modifiche necessarie per il corretto funzionamento dell’SDK. A seconda dell’ambiente specifico, potrebbero essere necessarie ulteriori impostazioni CSP.

## Esempio di criteri per la sicurezza dei contenuti

Gli esempi seguenti mostrano come configurare un CSP.

### Consenti accesso al dominio Edge

```
default-src 'self';
connect-src 'self' EDGE-DOMAIN
```

Nell’esempio precedente, `EDGE-DOMAIN` deve essere sostituito con il dominio di prime parti. Il dominio di prime parti è configurato per [edgeDomain](../commands/configure/edgedomain.md) impostazione. Se non è stato configurato alcun dominio di prima parte, `EDGE-DOMAIN` deve essere sostituito con `*.adobedc.net`. Se la migrazione dei visitatori è attivata con [idMigrationEnabled](../commands/configure/idmigrationenabled.md), il `connect-src` La direttiva deve inoltre includere `*.demdex.net`.

### Utilizzare NONCE per consentire gli elementi di script e di stile in linea

[!DNL Platform Web SDK] può modificare il contenuto della pagina e deve essere approvato per creare tag di script e di stile in linea. A questo scopo, l’Adobe consiglia di utilizzare un nonce per [default-src](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/default-src) Direttiva CSP. Un nonce è un token casuale crittograficamente sicuro generato dal server e generato una volta per ogni visualizzazione di pagina univoca.

```
default-src 'nonce-SERVER-GENERATED-NONCE'
```

Inoltre, il nonce CSP deve essere aggiunto come attributo al [!DNL Platform Web SDK] [codice di base](../install/library.md) tag script. [!DNL Platform Web SDK] utilizzerà quindi tale nonce quando si aggiungono tag di script o di stile in linea alla pagina:

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

## Configurare un CSP per la messaggistica in-app {#in-app-messaging}

Quando si configura [Messaggistica Web in-app](../personalization/web-in-app-messaging.md), devi includere la seguente direttiva nel CSP:

```
default-src  blob:;
```
