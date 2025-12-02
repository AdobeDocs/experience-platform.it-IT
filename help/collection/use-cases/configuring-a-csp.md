---
title: Configurazione di un CSP
seo-title: Configuring a CSP for Adobe Experience Platform Web SDK
description: Scopri come configurare una CSP per Experience Platform Web SDK
seo-description: Learn how to configure a CSP for the Experience Platform Web SDK
keywords: configurazione;configurazione;SDK;edge;Web SDK;configurare;contesto;web;dispositivo;ambiente;impostazioni web sdk;informativa sulla sicurezza dei contenuti;
exl-id: 661d0001-9e10-479e-84c1-80e58f0e9c0b
source-git-commit: 217282135bcd750740f4d3f8c6e17a0b8f9578bd
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Configurazione di un CSP

[Criteri sulla sicurezza dei contenuti](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP) viene utilizzato per limitare le risorse che un browser può utilizzare. I CSP possono anche limitare la funzionalità delle risorse di script e di stile. Adobe Experience Platform Web SDK non richiede un CSP, ma l&#39;aggiunta di un CSP può ridurre la superficie di attacco per prevenire attacchi dannosi.

Il CSP deve riflettere la modalità di distribuzione e configurazione di [!DNL Experience Platform Web SDK]. I CSP seguenti mostrano le modifiche necessarie per il corretto funzionamento di SDK. A seconda dell’ambiente specifico, potrebbero essere necessarie ulteriori impostazioni CSP.

## Esempio di criteri per la sicurezza dei contenuti

Gli esempi seguenti mostrano come configurare un CSP.

### Consenti accesso al dominio Edge

```
default-src 'self';
connect-src 'self' EDGE-DOMAIN
```

Nell&#39;esempio precedente, `EDGE-DOMAIN` deve essere sostituito con il dominio di prime parti. Il dominio di prime parti è configurato per l&#39;impostazione [edgeDomain](../js/commands/configure/edgedomain.md). Se non è stato configurato alcun dominio di prima parte, `EDGE-DOMAIN` deve essere sostituito con `*.adobedc.net`. Se la migrazione dei visitatori è attivata con [idMigrationEnabled](../js/commands/configure/idmigrationenabled.md), la direttiva `connect-src` deve includere anche `*.demdex.net`.

### Utilizzare NONCE per consentire gli elementi di script e di stile in linea

[!DNL Experience Platform Web SDK] può modificare il contenuto della pagina e deve essere approvato per creare tag di script e di stile in linea. A questo scopo, Adobe consiglia di utilizzare un nonce per la direttiva CSP [default-src](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/default-src). Un nonce è un token casuale crittograficamente sicuro generato dal server e generato una volta per ogni visualizzazione di pagina univoca.

```
default-src 'nonce-SERVER-GENERATED-NONCE'
```

Inoltre, il nonce CSP deve essere aggiunto come attributo al tag di script [!DNL Experience Platform Web SDK] [codice base](../js/install/library.md). [!DNL Experience Platform Web SDK] utilizzerà quindi il nonce quando aggiungerà tag di script o di stile in linea alla pagina:

```html
<script nonce="SERVER-GENERATED-NONCE">
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

Se non si utilizza un nonce, l&#39;altra opzione consiste nell&#39;aggiungere `unsafe-inline` alle direttive CSP `script-src` e `style-src`:

```
script-src 'unsafe-inline'
style-src 'unsafe-inline'
```

>[!NOTE]
>
>Adobe **non** consiglia di specificare `unsafe-inline` perché consente l&#39;esecuzione di qualsiasi script sulla pagina, limitando i vantaggi dei CSP.

## Configurare un CSP per la messaggistica in-app {#in-app-messaging}

Quando configuri la messaggistica Web in-app, devi includere la seguente direttiva nei CSP:

```
default-src  blob:;
```
