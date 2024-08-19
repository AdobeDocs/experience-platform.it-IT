---
title: Hint client agente utente
description: Scopri come funzionano gli hint client dell’agente utente in Web SDK. Gli hint client consentono ai proprietari del sito web di accedere a gran parte delle stesse informazioni disponibili nella stringa dell’agente utente, ma in modo più rispettoso della privacy.
keywords: user-agent;client hints; string; user-agent string; bassa entropia; alta entropia
exl-id: a909b1d1-be9d-43ba-bb4b-d28b0c609f65
source-git-commit: 89dfe037e28bae51e335dc67185afa42b2c418e3
workflow-type: tm+mt
source-wordcount: '1245'
ht-degree: 3%

---

# Hint client agente utente

## Panoramica {#overview}

Ogni volta che un browser web invia una richiesta a un server web, l’intestazione della richiesta include informazioni sul browser e sull’ambiente in cui viene eseguito il browser. Tutti questi dati vengono aggregati in una stringa, denominata stringa dell’agente utente.

Di seguito è riportato un esempio dell&#39;aspetto di una stringa agente utente in una richiesta proveniente da un browser Chrome in esecuzione su un dispositivo [!DNL Mac OS].

>[!NOTE]
>
>Nel corso degli anni, la quantità di informazioni sul browser e sul dispositivo incluse nella stringa dell’agente utente è aumentata e modificata più volte. L’esempio seguente mostra una selezione delle informazioni più comuni sull’agente utente.

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36`
```

| Campo | Valore |
|---|---|
| Nome software | Chrome |
| Versione software | 105 |
| Versione software completa | 105.0.0.0 |
| Nome del motore di layout | AppleWebKit |
| Versione motore di layout | 537,36 |
| Sistema operativo | MAC OS X |
| Versione del sistema operativo | 10.15.7 |
| Dispositivo | Mac OS X 10_15_7 |

## Casi d’uso {#use-cases}

Le stringhe dell’agente utente sono state a lungo utilizzate per fornire ai team di marketing e sviluppo informazioni importanti sul modo in cui i browser, i sistemi operativi e i dispositivi visualizzano il contenuto del sito e sul modo in cui gli utenti interagiscono con i siti web.

Le stringhe dell’agente utente vengono utilizzate anche per bloccare la posta indesiderata e filtrare i bot che esaminano i siti per diversi scopi aggiuntivi.

## Stringhe dell’agente utente in Adobe Experience Cloud {#user-agent-in-adobe}

Le soluzioni Adobe Experience Cloud utilizzano le stringhe dell’agente utente in vari modi.

* Adobe Analytics utilizza la stringa user agent per incrementare e derivare informazioni aggiuntive relative ai sistemi operativi, ai browser e ai dispositivi utilizzati per visitare un sito web.
* Adobe Audience Manager e Adobe Target qualificano gli utenti finali per le campagne di segmentazione e personalizzazione, in base alle informazioni fornite dalla stringa dell’agente utente.

## Introduzione agli hint client dell’agente utente {#ua-ch}

Negli ultimi anni, i proprietari del sito e i fornitori di marketing hanno utilizzato le stringhe degli agenti utente insieme ad altre informazioni incluse nelle intestazioni delle richieste per creare impronte digitali. Queste impronte digitali possono essere utilizzate come mezzo per identificare gli utenti all&#39;insaputa di questi ultimi.

Nonostante lo scopo importante che le stringhe dell’agente utente svolgono per i proprietari del sito, gli sviluppatori del browser hanno deciso di modificare il funzionamento delle stringhe dell’agente utente per limitare potenziali problemi di privacy per gli utenti finali.

La soluzione sviluppata è denominata [user agent client hints](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). Gli hint client consentono ancora ai siti web di raccogliere le informazioni necessarie su browser, sistema operativo e dispositivo, fornendo al tempo stesso una maggiore protezione contro i metodi di tracciamento nascosti, come la impronta digitale.

Gli hint client consentono ai proprietari del sito web di accedere a gran parte delle stesse informazioni disponibili nella stringa dell’agente utente, ma in modo più rispettoso della privacy.

Quando i browser moderni inviano un utente a un server web, l’intera stringa dell’agente utente viene inviata a ogni richiesta, indipendentemente dal fatto che sia necessaria. Gli hint client, invece, impongono un modello in cui il server deve chiedere al browser le informazioni aggiuntive che desidera conoscere sul client. Dopo aver ricevuto questa richiesta, il browser può applicare i propri criteri o la propria configurazione utente per determinare quali dati vengono restituiti. Invece di esporre l’intera stringa dell’agente utente per impostazione predefinita su tutte le richieste, l’accesso viene ora gestito in modo esplicito e verificabile.

## Supporto browser {#browser-support}

[User agent client hints](https://developer.chrome.com/docs/privacy-sandbox/user-agent/) introdotti con [!DNL Google Chrome]versione 89.

Altri browser basati su Chromium supportano l’API dei Client Hints, ad esempio:

* [!DNL Microsoft Edge]
* [!DNL Opera]
* [!DNL Brave]
* [!DNL Chrome for Android]
* [!DNL Opera for Android]
* [!DNL Samsung Internet]

## Categorie {#categories}

Esistono due categorie di suggerimenti client dell’agente utente:

* [Hint client a bassa entropia](#low-entropy)
* [Hint client ad alta entropia](#high-entropy)

### Hint client a bassa entropia {#low-entropy}

Gli hint client a bassa entropia includono informazioni di base che non possono essere utilizzate per gli utenti di impronte digitali. Informazioni quali il marchio del browser, la piattaforma e se la richiesta proviene da un dispositivo mobile.

Gli hint client a bassa entropia sono abilitati per impostazione predefinita in Web SDK e vengono trasmessi a ogni richiesta.

| Intestazione HTTP | JavaScript | Incluso in User-Agent per impostazione predefinita | Incluso negli hint client per impostazione predefinita |
|---|---|---|---|
| `Sec-CH-UA` | `brands` | Sì | Sì |
| `Sec-CH-UA-Platform` | `platform` | Sì | Sì |
| `Sec-CH-UA-Mobile` | `mobile` | Sì | Sì |

### Hint client ad alta entropia {#high-entropy}

Gli hint client ad alta entropia sono informazioni più dettagliate sul dispositivo client, come la versione della piattaforma, l&#39;architettura, il modello, il bit (piattaforme a 64 bit o a 32 bit) o la versione completa del sistema operativo. Queste informazioni potrebbero essere potenzialmente utilizzate per il rilevamento delle impronte digitali.

| Proprietà | Descrizione | Intestazione HTTP | Percorso XDM | Esempio | Incluso nell’agente utente per impostazione predefinita | Incluso negli hint client per impostazione predefinita |
| --- | --- | --- | --- | --- |---|---|
| Versione del sistema operativo | Versione del sistema operativo. | `Sec-CH-UA-Platform-Version` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.platformVersion` | `10.15.7` | Sì | No |
| Architettura | Architettura CPU sottostante. | `Sec-CH-UA-Arch` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.architecture` | `x86` | Sì | No |
| Modello dispositivo | Nome del dispositivo utilizzato. | `Sec-CH-UA-Model` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.model` | `Intel Mac OS X 10_15_7` | Sì | No |
| Amarezza | Il numero di bit supportati dall&#39;architettura CPU sottostante. | `Sec-CH-UA-Bitness` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.bitness` | `64` | Sì | No |
| Fornitore browser | Azienda che ha creato il browser. Anche l&#39;hint a bassa entropia `Sec-CH-UA` raccoglie questo elemento. | `Sec-CH-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.vendor` | `Google` | Sì | No |
| Nome browser | Browser utilizzato. Anche l&#39;hint a bassa entropia `Sec-CH-UA` raccoglie questo elemento. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.brand` | `Chrome` | Sì | No |
| Versione browser | Versione significativa del browser. Anche l&#39;hint a bassa entropia `Sec-CH-UA` raccoglie questo elemento. La versione esatta del browser non viene raccolta automaticamente. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.version` | `105` | Sì | No |


Gli hint client ad alta entropia sono disabilitati per impostazione predefinita in Web SDK. Per abilitarli, devi configurare manualmente Web SDK per richiedere hint client ad alta entropia.

## Gli hint client ad alta entropia influiscono sulle soluzioni Experience Cloud {#impact-in-experience-cloud-solutions}

Alcune soluzioni Adobe Experience Cloud si basano sulle informazioni incluse negli hint client ad alta entropia durante la generazione dei rapporti.

Se non abiliti gli hint client ad alta entropia nell’ambiente, i rapporti e le caratteristiche di Adobe Analytics e Audience Manager descritti di seguito non funzioneranno.

### Adobe Analytics segnala che si basa su hint client ad alta entropia {#analytics}

La dimensione [Sistema operativo](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-systems.html) include la versione del sistema operativo memorizzata come hint client ad alta entropia. Se gli hint client ad alta entropia non sono abilitati, la versione del sistema operativo potrebbe non essere accurata per gli hit raccolti dai browser Chromium.

### caratteristiche Audienci Manager basate su hint client ad alta entropia {#aam}

[!DNL Google] ha aggiornato la funzionalità del browser [!DNL Chrome] per ridurre le informazioni raccolte tramite l&#39;intestazione `User-Agent`. Di conseguenza, i clienti Audience Manager che utilizzano [DIL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=it) non riceveranno più informazioni affidabili sulle caratteristiche basate su [chiavi a livello di piattaforma](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-device-targeting.html).

I clienti Audience Manager che utilizzano chiavi a livello di piattaforma per il targeting devono passare a [Experience Platform Web SDK](/help/web-sdk/home.md) invece di [DIL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=it) e abilitare [High Entropy Client Hints](#enabling-high-entropy-client-hints) per continuare a ricevere dati affidabili sulle caratteristiche.

## Abilitazione degli hint client ad alta entropia {#enabling-high-entropy-client-hints}

Per abilitare gli hint client ad alta entropia nella distribuzione Web SDK, è necessario includere l&#39;opzione di contesto `highEntropyUserAgentHints` aggiuntiva nel campo [`context`](/help/web-sdk/commands/configure/context.md).

Ad esempio, per recuperare gli hint client ad alta entropia dalle proprietà web, la configurazione sarà simile alla seguente:

`context: ["highEntropyUserAgentHints", "web"]`

## Esempio {#example}

Gli hint client contenuti nelle intestazioni della prima richiesta effettuata dal browser a un server web conterranno il marchio del browser, la versione principale del browser e un indicatore che indica se il client è un dispositivo mobile. Ogni elemento di dati avrà un proprio valore di intestazione anziché essere raggruppato in una singola stringa dell’agente utente, come illustrato di seguito:

```shell
Sec-CH-UA: "Chromium";v="101", "Google Chrome";v="101", " Not;A Brand";v="99"

Sec-CH-UA-Mobile: ?0

Sec-CH-UA-Platform: "macOS
```

L&#39;intestazione [!DNL User-Agent] equivalente per lo stesso browser sarà simile alla seguente:

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
```

Sebbene le informazioni siano simili, la prima richiesta al server contiene suggerimenti client. Questi includono solo un sottoinsieme di ciò che è disponibile nella stringa dell’agente utente. Mancano nella richiesta l’architettura del sistema operativo, la versione completa del sistema operativo, il nome del motore di layout, la versione del motore di layout e la versione completa del browser.

Tuttavia, nelle richieste successive, [!DNL Client Hints API] consente ai server Web di richiedere ulteriori dettagli sul dispositivo. Quando questi valori vengono richiesti, a seconda della policy del browser o delle impostazioni utente, la risposta del browser può includere tali informazioni.

Di seguito è riportato un esempio dell&#39;oggetto JSON restituito da [!DNL Client Hints API] quando sono richiesti valori di entropia elevati:


```json
{
   "architecture":"x86",
   "bitness":"64",
   "brands":[
      {
         "brand":" Not A;Brand",
         "version":"99"
      },
      {
         "brand":"Chromium",
         "version":"100"
      },
      {
         "brand":"Google Chrome",
         "version":"100"
      }
   ],
   "fullVersionList":[
      {
         "brand":" Not A;Brand",
         "version":"99.0.0.0"
      },
      {
         "brand":"Chromium",
         "version":"100.0.4896.127"
      },
      {
         "brand":"Google Chrome",
         "version":"100.0.4896.127"
      }
   ],
   "mobile":false,
   "model":"",
   "platformVersion":"12.2.1"
}
```
