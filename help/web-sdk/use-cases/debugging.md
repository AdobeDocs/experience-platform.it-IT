---
title: Metodi di debug
description: Scopri come attivare/disattivare le funzionalità di debug in Web SDK.
keywords: debug web sdk;debugging;configurare;configurare comando;debug comando;edgeConfigId;setDebug;debugEnabled;debug;
exl-id: 4e893af8-a48e-48dc-9737-4c61b3355f03
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# Metodi di debug

Quando il debug è abilitato, Web SDK invia messaggi alla console del browser che possono essere utili per il debug dell’implementazione. Il debug è utile quando desideri comprendere il comportamento dell’SDK in base alle regole e agli elementi dati stabiliti.

Il debug è disattivato per impostazione predefinita, ma può essere attivato in quattro modi diversi. È possibile utilizzare qualsiasi combinazione di questi metodi per abilitare o disabilitare il debug più adatto al flusso di lavoro di sviluppo.

## Usa `debugEnabled` nel comando `configure`

Imposta il valore booleano `debugEnabled` su true durante la configurazione dell&#39;estensione. Questa opzione viene in genere utilizzata per gli ambienti di sviluppo, in quanto consente il debug per tutti coloro che visitano qualsiasi pagina del sito:

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```

Per ulteriori informazioni, vedere [`debugEnabled`](../commands/configure/debugenabled.md).

## Usa il comando `setDebug`

Analogamente al valore booleano riportato sopra, questo comando abilita il debug per tutti i visitatori della pagina.

```js
alloy("setDebug", {"enabled": true});
```

Per ulteriori informazioni, vedere il comando [`setDebug`](../commands/setdebug.md).

## Imposta un parametro di stringa query

È possibile abilitare il debug aggiungendo la stringa di query `?alloy_debug=true` alla fine di qualsiasi URL. Ad esempio:

`http://example.com/?alloy_debug=true`

Questo metodo si applica solo al computer locale, consentendo di eseguire il debug dei siti Web di produzione senza abilitare il debug per tutti. Questa modalità di attivazione del debug rimane attiva per il resto della sessione di esplorazione o fino a quando non viene disattivata.

## Utilizza l’Adobe Experience Platform Debugger

L’Adobe Experience Platform Debugger è un potente strumento che esamina le pagine web e ti aiuta a eseguire il debug dell’implementazione dei prodotti Experience Cloud. Puoi abilitare il debug dalla scheda di configurazione della sezione AEP Web SDK.

![Abilita debugger](../assets/enable-debugging.png)

Per ulteriori informazioni, vedere [Panoramica Adobe Experience Platform Debugger](/help/debugger/home.md).
