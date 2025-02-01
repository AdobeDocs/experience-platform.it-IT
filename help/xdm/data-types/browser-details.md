---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;browser;dettagli browser;tipo di dati;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati Dettagli browser
description: Scopri il tipo di dati XDM per i dettagli del browser.
exl-id: c67ff8bc-0614-4422-9bb7-689b98d7086d
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 27%

---

# [!UICONTROL Dettagli browser] tipo di dati

[!UICONTROL Dettagli browser] è un tipo di dati XDM standard che descrive i dettagli relativi a un browser o a un&#39;applicazione.

![](../images/data-types/browser-details.png){width=450}

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `acceptLanguage` | Stringa | Un tag di lingua IETF ([RFC 5646](https://tools.ietf.org/html/rfc5646)). |
| `cookiesEnabled` | Booleano | Indica se le impostazioni dell’utente consentono la scrittura di cookie. |
| `javaEnabled` | Booleano | Indica se Java era abilitato nel dispositivo da cui è stata fatta l’osservazione. |
| `javaScriptEnabled` | Booleano | Indica se JavaScript è stato abilitato nel dispositivo da cui è stata effettuata l’osservazione. |
| `javaScriptVersion` | Stringa | La versione di JavaScript supportata durante l’osservazione. |
| `javaVersion` | Stringa | La versione di Java supportata durante l’osservazione. |
| `name` | Stringa | Il nome dell’applicazione o del browser. |
| `quicktimeVersion` | Stringa | La versione di Apple Quicktime supportata durante l’osservazione. |
| `thirdPartyCookiesEnabled` | Booleano | Indica se i cookie di terze parti sono stati abilitati nel dispositivo da cui è stata effettuata l’osservazione. |
| `userAgent` | Stringa | La stringa HTTP dell’agente-utente proveniente dalla richiesta del client. |
| `vendor` | Stringa | Il fornitore dell’applicazione o del browser. |
| `version` | Stringa | Versione dell’applicazione o del browser. |
| `viewportHeight` | Intero | La dimensione verticale in pixel della finestra in cui è stato visualizzato l’evento. Per un evento di visualizzazione web, corrisponde all’altezza del riquadro di visualizzazione del browser. |
| `viewportWidth` | Intero | La dimensione orizzontale in pixel della finestra in cui è stato visualizzato l’evento. Per un evento di visualizzazione web, corrisponde alla larghezza del riquadro di visualizzazione del browser. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.schema.json)
