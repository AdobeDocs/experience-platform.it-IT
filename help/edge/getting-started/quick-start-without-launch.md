---
title: Avvio rapido con javascript semplice
seo-title: ' Adobe Experience Platform Avvio rapido SDK Web '
description: Guida di avvio rapido per l'utilizzo  Experience Platform Web SDK per la raccolta dei dati
seo-description: Guida di avvio rapido per l'utilizzo  Experience Platform Web SDK per la raccolta dei dati
translation-type: tm+mt
source-git-commit: 9b8bddf39301cdc39bfa5370ef98d99434fc64f8
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 3%

---


# Benvenuti

Questa guida illustra i diversi modi in cui impostare l’SDK Web per Adobi Experience Platform . Per poter utilizzare questa funzione, è necessario essere sul elenco consentiti . Se vuoi entrare nella lista d&#39;attesa, contatta il tuo CSM.

- Accertati che sia attivato un dominio di [prime parti (CNAME)](https://docs.adobe.com/content/help/it-IT/core-services/interface/ec-cookies/cookies-first-party.html) . Se hai già un CNAME per  Analytics, devi usarlo. Il test in fase di sviluppo funziona senza un CNAME, ma ne hai bisogno prima di andare in produzione
- Avere diritto a  Platform dei dati di Adobe Experience Platform.  Se non hai acquistato Platform, ti verrà fornito  Experience Platform Data Services Foundation per l&#39;utilizzo limitato con l&#39;SDK senza alcun costo aggiuntivo.
- Usa la versione più recente del servizio ID visitatore

## Creare un ID di configurazione

Potete creare un ID di configurazione utilizzando lo strumento [di configurazione](../fundamentals/edge-configuration.md) edge in Adobe Launch, anche se non utilizzate le funzioni di gestione tag. Questo consente di abilitare Edge Network per l&#39;invio di dati alle varie soluzioni. Per informazioni su come trovare ciascuna opzione, consultate la pagina [Edge Configuration Tool](../fundamentals/edge-configuration.md) (Strumentodi configurazione Edge).

>[!NOTE]
>
>L&#39;organizzazione deve trovarsi nel elenco consentiti  per la funzione. Contattate il CSM per avere il elenco consentiti .

## Preparare uno schema

 Experience Platform Edge Network accetta i dati come XDM. XDM è un formato di dati che consente di definire gli schemi. Lo schema definisce il modo in cui Edge Network prevede la formattazione dei dati. Per inviare i dati, è necessario definire lo schema.

- [Creare uno schema](../../xdm/tutorials/create-schema-ui.md)
- Aggiungere il mixin SDK Web  Adobe Experience Platform allo schema creato

Il seguente video è stato creato per aiutarti a creare uno schema, un set di dati e un connettore di origine per lo streaming dei dati SDK per Web.

>[!VIDEO](https://video.tv.adobe.com/v/35395?quality=12&learn=on)

## Installare l’SDK

Per installare l’SDK, copiate e incollate il seguente &quot;codice di base&quot; il più possibile nel `<head>` tag del codice HTML:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js" async></script>
```

Per ulteriori informazioni sulle diverse opzioni disponibili, consulta [Installazione dell’SDK](../fundamentals/installing-the-sdk.md).

## Configurare l’SDK

Quindi, fornisci la configurazione all’SDK. Questa operazione viene eseguita utilizzando il `configure` comando. Deve essere il primo comando chiamato su ogni pagina.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93:dev",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

Qui puoi fornire l’ID di configurazione che hai creato sopra e l’ID organizzazione. Questi sono gli unici due campi obbligatori. Tuttavia, esistono molte altre opzioni [di](../fundamentals/configuring-the-sdk.md)configurazione.

## Invio di un evento

Dopo aver chiamato il comando di configurazione, potete avviare liberamente gli eventi di tracciamento.

```javascript
alloy("sendEvent", {});
```

In genere, gli eventi vengono inviati con alcuni dati. Potete inviare dati XDM come questo. I dati inviati devono trovarsi nello schema creato in XDM.

```javascript
alloy("sendEvent", {
  "xdm": {
    "web":{
      "webPageDetails":{
        "name":"Home Page"
      }
    }
  }
});
```

Per ulteriori dettagli su come tenere traccia degli eventi, vedere [Tracciamento degli eventi](../fundamentals/tracking-events.md).

## Passaggi successivi

Dopo avere eseguito lo scorrimento dei dati, è possibile effettuare le seguenti operazioni:

- [Creare lo schema](https://docs.adobe.com/content/help/en/experience-platform/xdm/schema/composition.html)
- [Informazioni sul debug](../fundamentals/debugging.md)
- Scoprite come [personalizzare l&#39;esperienza](../fundamentals/rendering-personalization-content.md)
- Scopri come inviare dati a più soluzioni
   - [Adobe Analytics](../solution-specific/analytics/analytics-overview.md)
   - [Adobe Audience Manager](../solution-specific/audience-manager/audience-manager-overview.md)
   - [Adobe Target](../solution-specific/target/target-overview.md)
