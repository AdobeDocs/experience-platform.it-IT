---
title: User-Agent Client Hints
description: Scopri come funzionano gli User-Agent Client Hints in Web SDK. Gli hint client consentono ai proprietari del sito web di accedere a gran parte delle stesse informazioni disponibili nella stringa dell’agente utente, ma in modo più rispettoso della privacy.
keywords: user-agent;client hints; string; user-agent string; bassa entropia; alta entropia
exl-id: a909b1d1-be9d-43ba-bb4b-d28b0c609f65
source-git-commit: 29679e85943f16bcb02064cc60a249a3de61e022
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 6%

---

# User-Agent Client Hints

## Panoramica {#overview}

Ogni volta che un browser web invia una richiesta a un server web, l’intestazione della richiesta include informazioni sul browser e sull’ambiente in cui viene eseguito il browser. Tutti questi dati sono aggregati in una stringa, denominata [!DNL User-Agent] stringa.

Di seguito è riportato un esempio di [!DNL User-Agent] stringa simile a una richiesta proveniente da un browser Chrome in esecuzione su un [!DNL Mac OS] dispositivo.

>[!NOTE]
>
>Nel corso degli anni, la quantità di informazioni sul browser e sul dispositivo incluse [!DNL User-Agent] la stringa è cresciuta e modificata più volte. L’esempio seguente mostra una selezione dei più comuni [!DNL User-Agent] informazioni.

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

[!DNL User-Agent] Le stringhe sono state a lungo utilizzate per fornire ai team di marketing e sviluppo informazioni importanti sul modo in cui i browser, i sistemi operativi e i dispositivi visualizzano i contenuti del sito e sul modo in cui gli utenti interagiscono con i siti web.

[!DNL User-Agent] Le stringhe vengono inoltre utilizzate per bloccare lo spam e filtrare i bot che esaminano i siti per diversi scopi aggiuntivi.

## [!DNL User-Agent] stringhe in Adobe Experience Cloud {#user-agent-in-adobe}

Le soluzioni Adobe Experience Cloud utilizzano [!DNL User-Agent] in vari modi.

* Adobe Analytics utilizza [!DNL User-Agent] stringa per aggiungere e derivare informazioni aggiuntive relative a sistemi operativi, browser e dispositivi utilizzati per visitare un sito Web.
* Adobe Audience Manager e Adobe Target qualificano gli utenti finali per le campagne di segmentazione e personalizzazione, in base alle informazioni fornite dal [!DNL User-Agent] stringa.

## Introduzione agli User-Agent Client Hints {#ua-ch}

Negli ultimi anni, proprietari di siti e fornitori di marketing hanno utilizzato [!DNL User-Agent] insieme ad altre informazioni incluse nelle intestazioni della richiesta per creare impronte digitali. Queste impronte digitali possono essere utilizzate come mezzo per identificare gli utenti all&#39;insaputa di questi ultimi.

Nonostante l&#39;importante scopo che [!DNL User-Agent] le stringhe vengono utilizzate dai proprietari dei siti; gli sviluppatori dei browser hanno deciso di modificare le modalità [!DNL User-Agent] Le stringhe funzionano per limitare potenziali problemi di privacy per gli utenti finali.

La soluzione che hanno sviluppato si chiama [User-Agent Client Hints](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). Gli hint client consentono ancora ai siti web di raccogliere le informazioni necessarie su browser, sistema operativo e dispositivo, fornendo al tempo stesso una maggiore protezione contro i metodi di tracciamento nascosti, come la impronta digitale.

Gli hint client consentono ai proprietari di siti web di accedere a gran parte delle stesse informazioni disponibili in [!DNL User-Agent] stringa, ma in modo più rispettoso della privacy.

Quando i browser moderni inviano un utente a un server web, l’intero [!DNL User-Agent] stringa viene inviata a ogni richiesta, indipendentemente dal fatto che sia necessaria. Gli hint client, invece, impongono un modello in cui il server deve chiedere al browser le informazioni aggiuntive che desidera conoscere sul client. Dopo aver ricevuto questa richiesta, il browser può applicare i propri criteri o la propria configurazione utente per determinare quali dati vengono restituiti. Invece di esporre l&#39;intero [!DNL User-Agent] per impostazione predefinita, in tutte le richieste l’accesso viene ora gestito in modo esplicito e verificabile.

## Supporto browser {#browser-support}

[User-Agent Client Hints](https://developer.chrome.com/docs/privacy-sandbox/user-agent/) sono stati introdotti con [!DNL Google Chrome ]versione 89.

Altri browser basati su Chromium supportano l’API dei Client Hints, ad esempio:

* [!DNL Microsoft Edge]
* [!DNL Opera]
* [!DNL Brave]
* [!DNL Chrome for Android]
* [!DNL Opera for Android]
* [!DNL Samsung Internet]

## Categorie {#categories}

Esistono due categorie di User-Agent Client Hints:

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

| Intestazione HTTP | JavaScript | Incluso in User-Agent per impostazione predefinita | Incluso negli Client Hints per impostazione predefinita |
|---|---|---|---|
| `Sec-CH-UA-Platform-Version` | `platformVersion` | Sì | No |
| `Sec-CH-UA-Arc` | `architecture` | Sì | No |
| `Sec-CH-UA-Model` | `model` | Sì | No |
| `Sec-CH-UA-Bitness` | `Bitness` | Sì | No |
| `Sec-CH-UA-Full-Version-List` | `fullVersionList` | Sì | No |

Gli hint client ad alta entropia sono disabilitati per impostazione predefinita in Web SDK. Per abilitarli, devi configurare manualmente Web SDK per richiedere hint client ad alta entropia.

## Gli hint client ad alta entropia influiscono sulle soluzioni Experience Cloud {#impact-in-experience-cloud-solutions}

Alcune soluzioni Adobe Experience Cloud si basano sulle informazioni incluse negli hint client ad alta entropia durante la generazione dei rapporti.

Se non abiliti gli hint client ad alta entropia nell’ambiente, i rapporti e le caratteristiche di Adobe Analytics e Audience Manager descritti di seguito non funzioneranno.

### Adobe Analytics segnala che si basa su hint client ad alta entropia {#analytics}

Il [Sistema operativo](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-systems.html) la dimensione include la versione del sistema operativo memorizzata come hint client ad alta entropia. Se gli hint client ad alta entropia non sono abilitati, la versione del sistema operativo potrebbe non essere accurata per gli hit raccolti dai browser Chromium.

### caratteristiche Audienci Manager basate su hint client ad alta entropia {#aam}

[!DNL Google] ha aggiornato il [!DNL Chrome] funzionalità del browser per ridurre al minimo le informazioni raccolte tramite `User-Agent` intestazione. Di conseguenza, Audience Manager i clienti che utilizzano [DIL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=en) non riceverà più informazioni affidabili sulle caratteristiche basate su [chiavi a livello di piattaforma](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-device-targeting.html?lang=it).

Audience Manager i clienti che utilizzano chiavi a livello di piattaforma per il targeting devono passare a [Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=it) invece di [DIL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=en), e abilita [Client Hints ad alta entropia](#enabling-high-entropy-client-hints) per continuare a ricevere dati affidabili sulle caratteristiche.

## Abilitazione degli hint client ad alta entropia {#enabling-high-entropy-client-hints}

Per abilitare gli hint client ad alta entropia nella distribuzione Web SDK, devi includere gli hint aggiuntivi `highEntropyUserAgentHints` come descritto nella sezione [documentazione di configurazione](configuring-the-sdk.md#context), insieme alla configurazione esistente.

Ad esempio, per recuperare gli hint client ad alta entropia dalle proprietà web, la configurazione sarà simile alla seguente:

`context: ["highEntropyUserAgentHints", "web"]`

## Esempio {#example}

Gli hint client contenuti nelle intestazioni della prima richiesta effettuata dal browser a un server web conterranno il marchio del browser, la versione principale del browser e un indicatore che indica se il client è un dispositivo mobile. Ogni elemento di dati avrà un proprio valore di intestazione anziché essere raggruppato in un singolo [!DNL User-Agent] come mostrato di seguito:

```shell
Sec-CH-UA: "Chromium";v="101", "Google Chrome";v="101", " Not;A Brand";v="99"

Sec-CH-UA-Mobile: ?0

Sec-CH-UA-Platform: "macOS
```

Equivalente [!DNL User-Agent] l’intestazione per lo stesso browser sarà simile alla seguente:

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
```

Sebbene le informazioni siano simili, la prima richiesta al server contiene suggerimenti client. Questi includono solo un sottoinsieme di ciò che è disponibile in [!DNL User-Agent] stringa. Mancano nella richiesta l’architettura del sistema operativo, la versione completa del sistema operativo, il nome del motore di layout, la versione del motore di layout e la versione completa del browser.

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
