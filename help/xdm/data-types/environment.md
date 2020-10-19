---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;environment;datatype;data-type;data type;
solution: Experience Platform
title: Tipo dati ambiente
topic: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM di ambiente.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 4%

---


# [!UICONTROL Environment] tipo di dati

[!UICONTROL Environment] è un tipo di dati XDM standard che descrive l&#39;ambiente circostante di un evento osservato, con informazioni dettagliate specifiche sul passaggio, come le versioni di rete e software.

>[!IMPORTANT]
>
>Tutti i valori devono essere allineati con il database [DeviceAtlas](https://deviceatlas.com) , concesso in licenza per  Adobe.

<img src="../images/data-types/environment.png" width="400" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `_dc` | Oggetto | Un oggetto che contiene un singolo campo, `language`, che indica la lingua dell&#39;ambiente in cui rappresentare le preferenze linguistiche, geografiche o culturali dell&#39;utente per la presentazione dei dati. Le lingue sono specificate nel codice della lingua come definito in [IETF RFC 3066](https://www.ietf.org/rfc/rfc3066.txt). |
| `browserDetails` | [Dettagli del browser](./browser-details.md) | Descrive i dettagli specifici dell&#39;ambiente del browser, come nome del browser, versione, versione JavaScript, stringa agente utente e linguaggio di accettazione. |
| `ISP` | Stringa | Nome del provider di servizi Internet dell&#39;utente. |
| `carrier` | Stringa | Nome del gestore della rete mobile o MNO (noto anche come fornitore di servizi wireless, vettore wireless, società cellulare o vettore di rete mobile) che vende e fornisce servizi di comunicazione all&#39;utente. |
| `colorDepth` | Intero | Il numero di bit utilizzati per ciascun componente colore di un singolo pixel. |
| `connectionType` | Stringa | Tipo di connessione Internet. I valori accettati includono: <ul><li>`dialup`</li><li>`isdn`</li><li>`bisdn`</li><li>`dsl`</li><li>`cable`</li><li>`wireless_wifi`</li><li>`mobile`</li><li>`mobile_edge`</li><li>`mobile_2g`</li><li>`mobile_3g`</li><li>`mobile_lte`</li><li>`t1`</li><li>`t3`</li><li>`oc3`</li><li>`lan`</li><li>`modem`</li></ul> |
| `domain` | Stringa | Il dominio dell&#39;ISP dell&#39;utente. |
| `ipV4` | Stringa | Etichetta numerica assegnata a un dispositivo che partecipa a una rete di computer che utilizza il protocollo Internet per la comunicazione (32 bit). |
| `ipV6` | Stringa | Etichetta numerica assegnata a un dispositivo che partecipa a una rete di computer che utilizza il protocollo Internet per la comunicazione (128 bit). |
| `operatingSystem` | Stringa | Nome del sistema operativo utilizzato al momento dell&#39;osservazione. L&#39;attributo non deve contenere informazioni sulla versione, ad esempio `10.5.3`, ma deve contenere denominazioni &quot;edition&quot; quali `Ultimate` o `Professional`. |
| `operatingSystemVendor` | Stringa | Nome del fornitore del sistema operativo utilizzato al momento dell&#39;osservazione. |
| `operatingSystemVersion` | Stringa | Identificatore completo della versione per il sistema operativo utilizzato al momento dell&#39;osservazione. Le versioni sono generalmente composte numericamente, ma possono essere in un formato definito dal fornitore. |
| `type` | Stringa | Il tipo di ambiente dell&#39;applicazione. Cfr. l&#39; [appendice](#type) per i valori accettati. |
| `viewportHeight` | Intero | La dimensione verticale in pixel della finestra in cui è stata visualizzata l&#39;esperienza. Per un evento di visualizzazione Web, si tratta dell&#39;altezza della finestra del browser. |
| `viewPortWidth` | Intero | La dimensione orizzontale in pixel della finestra in cui è stata visualizzata l&#39;esperienza. Per un evento di visualizzazione Web, si tratta della larghezza di visualizzazione del browser. |

Per ulteriori dettagli sul mixin, fare riferimento al repository XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.schema.json)

## Appendice

La sezione seguente contiene informazioni aggiuntive sul tipo di [!UICONTROL Device] dati.

## Valori accettati per il tipo {#type}

Nella tabella seguente sono riportati i valori accettati per `type` e i significati associati:

| Valore | Descrizione |
| --- | --- |
| `browser` | Browser |
| `application` | Applicazione |
| `iot` | Internet delle cose |
| `external` | Sistema esterno |
| `widget` | Estensione dell&#39;applicazione |