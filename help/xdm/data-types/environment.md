---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;ambiente;tipo di dati;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati ambiente
topic-legacy: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM per l’ambiente.
exl-id: ec806ee5-ed65-4148-9dbe-e297d9e8cd73
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 4%

---

#  Tipo di dati ambientali

 L&#39;ambiente è un tipo di dati XDM standard che descrive l&#39;ambiente circostante di un evento osservato, specificandone le informazioni transitorie, come le versioni di rete e software.

>[!IMPORTANT]
>
>Tutti i valori devono essere allineati con il database [DeviceAtlas](https://deviceatlas.com), concesso in licenza dall&#39;Adobe.

<img src="../images/data-types/environment.png" width="400" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `_dc` | Oggetto | Oggetto che contiene un singolo campo, `language`, che indica la lingua dell’ambiente in cui rappresentare le preferenze linguistiche, geografiche o culturali dell’utente per la presentazione dei dati. Le lingue sono specificate nel codice della lingua come definito in [IETF RFC 3066](https://www.ietf.org/rfc/rfc3066.txt). |
| `browserDetails` | [Dettagli del browser](./browser-details.md) | Descrive i dettagli dell&#39;ambiente specifici del browser, ad esempio nome del browser, versione, versione JavaScript, stringa dell&#39;agente utente e linguaggio di accettazione. |
| `ISP` | Stringa | Nome del provider di servizi Internet dell&#39;utente. |
| `carrier` | Stringa | Nome del gestore della rete mobile o dell&#39;operatore MNO (noto anche come fornitore di servizi wireless, vettore wireless, società cellulare o gestore della rete mobile) che vende e fornisce servizi di comunicazione all&#39;utente. |
| `colorDepth` | Intero | Il numero di bit utilizzati per ogni componente colore di un singolo pixel. |
| `connectionType` | Stringa | Tipo di connessione Internet. I valori accettati includono: <ul><li>`dialup`</li><li>`isdn`</li><li>`bisdn`</li><li>`dsl`</li><li>`cable`</li><li>`wireless_wifi`</li><li>`mobile`</li><li>`mobile_edge`</li><li>`mobile_2g`</li><li>`mobile_3g`</li><li>`mobile_lte`</li><li>`t1`</li><li>`t3`</li><li>`oc3`</li><li>`lan`</li><li>`modem`</li></ul> |
| `domain` | Stringa | Dominio dell&#39;ISP dell&#39;utente. |
| `ipV4` | Stringa | Etichetta numerica assegnata a un dispositivo che partecipa a una rete di computer che utilizza il protocollo Internet per la comunicazione (32 bit). |
| `ipV6` | Stringa | Etichetta numerica assegnata a un dispositivo che partecipa a una rete di computer che utilizza il protocollo Internet per la comunicazione (128 bit). |
| `operatingSystem` | Stringa | Nome del sistema operativo utilizzato al momento dell&#39;osservazione. L&#39;attributo non deve contenere informazioni sulla versione come `10.5.3`, ma deve contenere designazioni &quot;edition&quot; come ad esempio `Ultimate` o `Professional`. |
| `operatingSystemVendor` | Stringa | Nome del fornitore del sistema operativo utilizzato al momento dell&#39;osservazione. |
| `operatingSystemVersion` | Stringa | Identificatore della versione completa del sistema operativo utilizzato al momento dell&#39;osservazione. Le versioni sono generalmente composte numericamente ma possono essere in un formato definito dal fornitore. |
| `type` | Stringa | Il tipo di ambiente dell&#39;applicazione. Vedere l&#39; [appendice](#type) per i valori accettati. |
| `viewportHeight` | Intero | Dimensione verticale in pixel della finestra in cui veniva visualizzata l’esperienza. Per un evento di visualizzazione web, si tratta dell&#39;altezza del riquadro di visualizzazione del browser. |
| `viewPortWidth` | Intero | Dimensione orizzontale in pixel della finestra in cui veniva visualizzata l’esperienza. Per un evento di visualizzazione web, si tratta della larghezza del riquadro di visualizzazione del browser. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.schema.json)

## Appendice

La sezione seguente contiene informazioni aggiuntive sul tipo di dati [!UICONTROL Dispositivo].

## Valori accettati per tipo {#type}

La tabella seguente illustra i valori accettati per `type` e i relativi significati associati:

| Valore | Descrizione |
| --- | --- |
| `browser` | Browser |
| `application` | Applicazione |
| `iot` | Internet delle cose |
| `external` | Sistema esterno |
| `widget` | Estensione dell&#39;applicazione |
