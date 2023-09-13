---
title: Hint client agente utente
description: Scopri come funzionano gli hint client dell’agente utente in Web SDK. Gli hint client consentono ai proprietari del sito web di accedere a gran parte delle stesse informazioni disponibili nella stringa dell’agente utente, ma in modo più rispettoso della privacy.
keywords: user-agent;client hints; string; user-agent string; bassa entropia; alta entropia
exl-id: a909b1d1-be9d-43ba-bb4b-d28b0c609f65
source-git-commit: d856630d4c14387ad4d77a915585fe05803878fb
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 6%

---

# Hint client agente utente

## Panoramica {#overview}

Ogni volta che un browser web invia una richiesta a un server web, l’intestazione della richiesta include informazioni sul browser e sull’ambiente in cui viene eseguito il browser. Tutti questi dati vengono aggregati in una stringa, denominata stringa dell’agente utente.

Di seguito è riportato un esempio dell’aspetto di una stringa dell’agente utente in una richiesta proveniente da un browser Chrome in esecuzione su un [!DNL Mac OS] dispositivo.

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
| Versione del motore di layout | 537.36 |
| Sistema operativo | Mac OS X |
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

La soluzione che hanno sviluppato si chiama [user agent client hints](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). Gli hint client consentono ancora ai siti web di raccogliere le informazioni necessarie su browser, sistema operativo e dispositivo, fornendo al tempo stesso una maggiore protezione contro i metodi di tracciamento nascosti, come la impronta digitale.

Gli hint client consentono ai proprietari del sito web di accedere a gran parte delle stesse informazioni disponibili nella stringa dell’agente utente, ma in modo più rispettoso della privacy.

Quando i browser moderni inviano un utente a un server web, l’intera stringa dell’agente utente viene inviata a ogni richiesta, indipendentemente dal fatto che sia necessaria. Gli hint client, invece, impongono un modello in cui il server deve chiedere al browser le informazioni aggiuntive che desidera conoscere sul client. Dopo aver ricevuto questa richiesta, il browser può applicare i propri criteri o la propria configurazione utente per determinare quali dati vengono restituiti. Invece di esporre l’intera stringa dell’agente utente per impostazione predefinita su tutte le richieste, l’accesso viene ora gestito in modo esplicito e verificabile.

## Supporto browser {#browser-support}

[Hint client agente utente](https://developer.chrome.com/docs/privacy-sandbox/user-agent/) sono stati introdotti con [!DNL Google Chrome]versione 89.

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

| Intestazione HTTP | JavaScript | Incluso nell’agente utente per impostazione predefinita | Incluso negli hint client per impostazione predefinita |
|---|---|---|---|
| `Sec-CH-UA-Platform-Version` | `platformVersion` | Sì | No |
| `Sec-CH-UA-Arc` | `architecture` | Sì | No |
| `Sec-CH-UA-Model` | `model` | Sì | No |
| `Sec-CH-UA-Bitness` | `Bitness` | Sì | No |
| `Sec-CH-UA-Full-Version-List` | `fullVersionList` | Sì | No |

Gli hint client ad alta entropia sono disabilitati per impostazione predefinita in Web SDK. Per abilitarli, devi configurare manualmente Web SDK per richiedere hint client ad alta entropia.

## Gli hint client ad alta entropia influiscono sulle soluzioni Experience Cloud {#impact-in-experience-cloud-solutions}

Alcune soluzioni Adobe Experience Cloud si basano sulle informazioni incluse negli hint client ad alta entropia durante la generazione dei rapporti.

Se non abiliti gli hint client ad alta entropia nell’ambiente, i rapporti e le caratteristiche di Adobe Analytics e Audienci Manager descritti di seguito non funzioneranno.

### Adobe Analytics segnala che si basa su hint client ad alta entropia {#analytics}

Il [Sistema operativo](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-systems.html) la dimensione include la versione del sistema operativo memorizzata come hint client ad alta entropia. Se gli hint client ad alta entropia non sono abilitati, la versione del sistema operativo potrebbe non essere accurata per gli hit raccolti dai browser Chromium.

### caratteristiche Audienci Manager basate su hint client ad alta entropia {#aam}

[!DNL Google] ha aggiornato il [!DNL Chrome] funzionalità del browser per ridurre al minimo le informazioni raccolte tramite `User-Agent` intestazione. Di conseguenza, Audience Manager i clienti che utilizzano [DIL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=en) non riceverà più informazioni affidabili sulle caratteristiche basate su [chiavi a livello di piattaforma](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-device-targeting.html?lang=it).

Audience Manager i clienti che utilizzano chiavi a livello di piattaforma per il targeting devono passare a [Experienci Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=it) invece di [DIL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=en), e abilita [Client Hints ad alta entropia](#enabling-high-entropy-client-hints) per continuare a ricevere dati affidabili sulle caratteristiche.

## Abilitazione degli hint client ad alta entropia {#enabling-high-entropy-client-hints}

Per abilitare gli hint client ad alta entropia nella distribuzione Web SDK, devi includere gli hint aggiuntivi `highEntropyUserAgentHints` come descritto nella sezione [documentazione di configurazione](configuring-the-sdk.md#context), insieme alla configurazione esistente.

Ad esempio, per recuperare gli hint client ad alta entropia dalle proprietà web, la configurazione sarà simile alla seguente:

`context: ["highEntropyUserAgentHints", "web"]`

## Esempio {#example}

Gli hint client contenuti nelle intestazioni della prima richiesta effettuata dal browser a un server web conterranno il marchio del browser, la versione principale del browser e un indicatore che indica se il client è un dispositivo mobile. Ogni elemento di dati avrà un proprio valore di intestazione anziché essere raggruppato in una singola stringa dell’agente utente, come illustrato di seguito:

```shell
Sec-CH-UA: "Chromium";v="101", "Google Chrome";v="101", " Not;A Brand";v="99"

Sec-CH-UA-Mobile: ?0

Sec-CH-UA-Platform: "macOS
```

Equivalente [!DNL User-Agent] l’intestazione per lo stesso browser sarà simile alla seguente:

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
```

Sebbene le informazioni siano simili, la prima richiesta al server contiene suggerimenti client. Questi includono solo un sottoinsieme di ciò che è disponibile nella stringa dell’agente utente. Mancano nella richiesta l’architettura del sistema operativo, la versione completa del sistema operativo, il nome del motore di layout, la versione del motore di layout e la versione completa del browser.

Tuttavia, su richieste successive, [!DNL Client Hints API] consente ai server web di richiedere ulteriori dettagli sul dispositivo. Quando questi valori vengono richiesti, a seconda della policy del browser o delle impostazioni utente, la risposta del browser può includere tali informazioni.

Di seguito è riportato un esempio dell’oggetto JSON restituito da [!DNL Client Hints API] quando sono richiesti valori entropici elevati:


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
