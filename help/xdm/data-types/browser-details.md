---
keywords: ' Experience Platform;home;argomenti più comuni;schema;schema;XDM;campi;schemi;browser;dettagli del browser;tipo di dati;tipo di dati;tipo di dati;'
solution: Experience Platform
title: Tipo di dati Dettagli browser
topic: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM Dettagli browser.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 6%

---


# [!UICONTROL Browser details] tipo di dati

[!UICONTROL Browser details] è un tipo di dati XDM standard che descrive i dettagli relativi a un browser o a un&#39;applicazione.

<img src="../images/data-types/browser-details.png" width="450" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `acceptLanguage` | Stringa | Un tag del linguaggio IETF ([RFC 5646](https://tools.ietf.org/html/rfc5646)). |
| `cookiesEnabled` | Booleano | Indica se le impostazioni dell&#39;utente consentono la scrittura dei cookie. |
| `javaEnabled` | Booleano | Indica se Java è stato abilitato nel dispositivo da cui è stata effettuata l&#39;osservazione. |
| `javaScriptEnabled` | Booleano | Indica se JavaScript è stato abilitato nel dispositivo da cui è stata effettuata l&#39;osservazione. |
| `javaScriptVersion` | Stringa | La versione di JavaScript supportata durante l&#39;osservazione. |
| `javaVersion` | Stringa | La versione di Java supportata durante l&#39;osservazione. |
| `name` | Stringa | Il nome dell’applicazione o del browser. |
| `quicktimeVersion` | Stringa | La versione di Apple Quicktime supportata durante l&#39;osservazione. |
| `thirdPartyCookiesEnabled` | Booleano | Indica se i cookie di terze parti sono stati attivati nel dispositivo da cui è stata effettuata l&#39;osservazione. |
| `userAgent` | Stringa | Stringa agente utente HTTP dalla richiesta client. |
| `vendor` | Stringa | Il fornitore dell’applicazione o del browser. |
| `version` | Stringa | La versione dell’applicazione o del browser. |
| `viewportHeight` | Intero | Le dimensioni verticali in pixel della finestra in cui l&#39;evento è stato visualizzato al suo interno. Per un evento di visualizzazione Web, si tratta dell&#39;altezza della finestra del browser. |
| `viewportWidth` | Intero | La dimensione orizzontale in pixel della finestra in cui l&#39;evento è stato visualizzato al suo interno. Per un evento di visualizzazione Web, si tratta della larghezza di visualizzazione del browser. |

Per ulteriori dettagli sul mixin, fare riferimento al repository XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.schema.json)