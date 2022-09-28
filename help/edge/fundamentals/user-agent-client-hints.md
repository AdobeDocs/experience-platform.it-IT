---
title: Suggerimenti client utente-agente
description: Scopri come funzionano i suggerimenti client User-Agent nell’SDK per web
keywords: user-agent;suggerimenti client; stringa; stringa agente utente; entropia bassa; entropia elevata
source-git-commit: 6c974d1a646ff1f3a8f7ad9d67a6840391fc739e
workflow-type: tm+mt
source-wordcount: '1081'
ht-degree: 6%

---


# Suggerimenti client utente-agente

## Panoramica {#overview}

Ogni volta che un browser Web effettua una richiesta a un server web, l’intestazione della richiesta include informazioni sul browser e sull’ambiente in cui il browser è in esecuzione. Tutti questi dati vengono aggregati in una stringa, denominata [!DNL User-Agent] stringa.

Ecco un esempio di un [!DNL User-Agent] la stringa è simile a una richiesta proveniente da un browser Chrome in esecuzione su un [!DNL Mac OS] dispositivo.

>[!NOTE]
>
>Nel corso degli anni, la quantità di informazioni sul browser e sul dispositivo incluse nella [!DNL User-Agent] la stringa è cresciuta e modificata più volte. L’esempio seguente mostra una selezione dei più comuni [!DNL User-Agent] informazioni.

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
| Dispositivo | Intel Mac OS X 10_15_7 |

## Casi d’uso {#use-cases}

[!DNL User-Agent] Le stringhe sono state a lungo utilizzate per fornire ai team di marketing e sviluppo informazioni importanti sul modo in cui i browser, i sistemi operativi e i dispositivi visualizzano il contenuto del sito, nonché sul modo in cui gli utenti interagiscono con i siti web.

[!DNL User-Agent] Le stringhe vengono inoltre utilizzate per bloccare lo spam e filtrare i bot che eseguono ricerche per indicizzazione dei siti per diversi scopi aggiuntivi.

## [!DNL User-Agent] stringhe in Adobe Experience Cloud {#user-agent-in-adobe}

Le soluzioni Adobe Experience Cloud utilizzano [!DNL User-Agent] stringhe in vari modi.

* Adobe Analytics utilizza [!DNL User-Agent] stringa per potenziare e derivare informazioni aggiuntive relative a sistemi operativi, browser e dispositivi utilizzati per visitare un sito web.
* Adobe Audience Manager e Adobe Target qualificano gli utenti finali per le campagne di segmentazione e personalizzazione, in base alle informazioni fornite dalla [!DNL User-Agent] stringa.

## Introduzione agli hint client User-Agent {#ua-ch}

Negli ultimi anni, i proprietari dei siti e i venditori di marketing hanno utilizzato [!DNL User-Agent] stringhe insieme ad altre informazioni incluse nelle intestazioni di richiesta per creare impronte digitali. Queste impronte digitali possono essere utilizzate come mezzo per identificare gli utenti senza che ne siano a conoscenza.

Nonostante l&#39;importante scopo che [!DNL User-Agent] le stringhe servono ai proprietari del sito, gli sviluppatori del browser hanno deciso di modificare il modo in cui [!DNL User-Agent] Le stringhe funzionano per limitare potenziali problemi di privacy per gli utenti finali.

La soluzione che hanno sviluppato si chiama [Suggerimenti client utente-agente](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). I suggerimenti dei clienti consentono ancora ai siti web di raccogliere le informazioni necessarie sul browser, il sistema operativo e il dispositivo, fornendo al contempo una maggiore protezione contro i metodi di tracciamento nascosti, come la impronte digitali.

I suggerimenti client consentono ai proprietari del sito web di accedere a molte delle stesse informazioni disponibili nel [!DNL User-Agent] Stringa, ma in un modo più rispettoso della privacy.

Quando i browser moderni inviano un utente a un server web, l&#39;intero [!DNL User-Agent] viene inviata a ogni richiesta, indipendentemente dal fatto che sia obbligatoria. I suggerimenti client, invece, impongono un modello in cui il server deve chiedere al browser le informazioni aggiuntive che desidera sapere sul client. Dopo aver ricevuto questa richiesta, il browser può applicare i propri criteri o la propria configurazione utente per determinare quali dati vengono restituiti. Invece di esporre l&#39;intero [!DNL User-Agent] Per impostazione predefinita, in tutte le richieste, l&#39;accesso viene ora gestito in modo esplicito e verificabile.

## Supporto browser {#browser-support}

[Suggerimenti client utente-agente](https://developer.chrome.com/docs/privacy-sandbox/user-agent/) sono stati introdotti con [!DNL Google Chrome ]versione 89.

I browser aggiuntivi basati su Chromium supportano l’API dei suggerimenti client, ad esempio:

* [!DNL Microsoft Edge]
* [!DNL Opera]
* [!DNL Brave]
* [!DNL Chrome for Android]
* [!DNL Opera for Android]
* [!DNL Samsung Internet]

## Categorie {#categories}

Esistono due categorie di suggerimenti client utente-agente:

* [Suggerimenti client entropici ridotti](#low-entropy)
* [Suggerimenti del client entropico elevati](#high-entropy)

### Suggerimenti client entropici ridotti {#low-entropy}

I suggerimenti per i client entropici bassi includono informazioni di base che non possono essere utilizzate per gli utenti di impronte digitali. Informazioni quali il marchio del browser, la piattaforma e se la richiesta proviene da un dispositivo mobile.

I suggerimenti per client entropici bassi sono abilitati per impostazione predefinita in SDK per web e vengono trasmessi a ogni richiesta.

| Intestazione HTTP | JavaScript | Incluso in User-Agent per impostazione predefinita | Incluso nei suggerimenti client per impostazione predefinita |
|---|---|---|---|
| `Sec-CH-UA` | `brands` | Sì | Sì |
| `Sec-CH-UA-Platform` | `platform` | Sì | Sì |
| `Sec-CH-UA-Mobile` | `mobile` | Sì | Sì |

### Suggerimenti del client entropico elevati {#high-entropy}

Gli hint client ad alta entropia sono informazioni più dettagliate sul dispositivo client, come la versione della piattaforma, l&#39;architettura, il modello, il bit (piattaforme a 64 bit o a 32 bit) o la versione completa del sistema operativo. Tali informazioni potrebbero essere potenzialmente utilizzate per la creazione di impronte digitali.

| Intestazione HTTP | JavaScript | Incluso in User-Agent per impostazione predefinita | Incluso negli hint client per impostazione predefinita |
|---|---|---|---|
| `Sec-CH-UA-Platform-Version` | `platformVersion` | Sì | No |
| `Sec-CH-UA-Arc` | `architecture` | Sì | No |
| `Sec-CH-UA-Model` | `model` | Sì | No |
| `Sec-CH-UA-Bitness` | `Bitness` | Sì | No |
| `Sec-CH-UA-Full-Version-List` | `fullVersionList` | Sì | No |

Gli hint client entropy elevati sono disabilitati per impostazione predefinita in SDK per web. Per abilitarli devi configurare manualmente l’SDK per web per richiedere hint client ad alta entropia.

## L&#39;impatto dei suggerimenti sul client entropici elevati sulle soluzioni Experience Cloud {#impact-in-experience-cloud-solutions}

Alcune soluzioni Adobe Experience Cloud si basano sulle informazioni incluse in suggerimenti client entropici elevati durante la generazione dei rapporti.

Se nell’ambiente non si abilitano hint client entropici elevati, i rapporti e le caratteristiche di Adobe Analytics e Audience Manager descritti di seguito non funzioneranno.

### Rapporti di Adobe Analytics basati su suggerimenti client entropici elevati {#analytics}

I seguenti rapporti di Adobe Analytics non funzioneranno quando gli hint client entropy elevati sono disabilitati.

* [Browser](https://experienceleague.adobe.com/docs/analytics/components/dimensions/browser.html)
* [Tipo di browser](https://experienceleague.adobe.com/docs/analytics/components/dimensions/browser-type.html)
* [Sistema operativo](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-systems.html)
* [Tipi di sistemi operativi](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-system-types.html)
* [Dimensioni per dispositivi mobili](https://experienceleague.adobe.com/docs/analytics/components/dimensions/mobile-dimensions.html)

### Caratteristiche di Audience Manager basate su suggerimenti client entropici elevati {#aam}

Se le caratteristiche di Audience Manager utilizzano una delle seguenti proprietà, è necessario abilitare hint client entropy elevati. In caso contrario, le caratteristiche smetteranno di funzionare.

* Versione del sistema operativo
* Modello del dispositivo
* produttore del dispositivo
* Fornitore di dispositivi

## Abilitazione di hint client entropy elevati {#enabling-high-entropy-client-hints}

Per abilitare hint client entropy elevati nella distribuzione SDK per web, devi includere `highEntropyUserAgentHints` opzione di contesto, come descritto in [documentazione di configurazione](configuring-the-sdk.md#context), insieme alla configurazione esistente.

Ad esempio, per recuperare suggerimenti client entropici elevati dalle proprietà web, la configurazione sarà simile alla seguente:

`context: ["highEntropyUserAgentHints", "web"]`

## Esempio {#example}

I suggerimenti client contenuti nelle intestazioni della prima richiesta effettuata dal browser a un server web conterranno il marchio del browser, la versione principale del browser e un indicatore che indichi se il client è un dispositivo mobile. Ogni elemento dati avrà un proprio valore di intestazione anziché essere raggruppato in un singolo [!DNL User-Agent] come illustrato di seguito:

```shell
Sec-CH-UA: "Chromium";v="101", "Google Chrome";v="101", " Not;A Brand";v="99"

Sec-CH-UA-Mobile: ?0

Sec-CH-UA-Platform: "macOS
```

Equivalente [!DNL User-Agent] intestazione per lo stesso browser, simile a questa:

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
```

Sebbene le informazioni siano simili, la prima richiesta al server contiene suggerimenti client. Includono solo un sottoinsieme di ciò che è disponibile nel [!DNL User-Agent] stringa. Mancano nella richiesta l&#39;architettura del sistema operativo, la versione completa del sistema operativo, il nome del motore di layout, la versione del motore di layout e la versione completa del browser.

Tuttavia, nelle richieste successive, il [!DNL Client Hints API] consente ai server web di richiedere ulteriori dettagli sul dispositivo. Quando questi valori vengono richiesti, a seconda dei criteri del browser o delle impostazioni utente, la risposta del browser potrebbe includere tali informazioni.

Di seguito è riportato un esempio dell’oggetto JSON restituito dal [!DNL Client Hints API] quando sono richiesti valori entropici elevati:


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
