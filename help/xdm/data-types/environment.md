---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;ambiente;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati ambiente
description: Scopri il tipo di dati XDM per l’ambiente.
exl-id: ec806ee5-ed65-4148-9dbe-e297d9e8cd73
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 5%

---

# [!UICONTROL Ambiente] tipo di dati

[!UICONTROL Ambiente] è un tipo di dati XDM standard che descrive l’ambiente circostante di un evento osservato, in particolare informazioni transitorie come le versioni di rete e software.

>[!IMPORTANT]
>
>Tutti i valori devono essere allineati con [DeviceAtlas](https://deviceatlas.com) database, concesso in licenza da Adobe.

<img src="../images/data-types/environment.png" width="400" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `_dc` | Oggetto | Oggetto contenente un singolo campo, `language`, che indica la lingua dell’ambiente per rappresentare le preferenze linguistiche, geografiche o culturali dell’utente per la presentazione dei dati. Le lingue sono specificate nel codice della lingua definito in [IETF RFC 3066](https://www.ietf.org/rfc/rfc3066.txt). |
| `browserDetails` | [Dettagli browser](./browser-details.md) | Descrive i dettagli specifici del browser per l’ambiente, ad esempio il nome, la versione, la versione JavaScript, la stringa dell’agente utente e il linguaggio di accettazione. |
| `ISP` | Stringa | Nome del provider di servizi Internet dell&#39;utente. |
| `carrier` | Stringa | Il nome dell&#39;operatore di rete mobile o MNO (noto anche come provider di servizi wireless, operatore wireless, società di telefonia mobile o operatore di rete mobile) che vende e fornisce servizi di comunicazione all&#39;utente. |
| `colorDepth` | Intero | Il numero di bit utilizzati per ogni componente di colore di un singolo pixel. |
| `connectionType` | Stringa | Tipo di connessione Internet. I valori accettati includono: <ul><li>`dialup`</li><li>`isdn`</li><li>`bisdn`</li><li>`dsl`</li><li>`cable`</li><li>`wireless_wifi`</li><li>`mobile`</li><li>`mobile_edge`</li><li>`mobile_2g`</li><li>`mobile_3g`</li><li>`mobile_lte`</li><li>`t1`</li><li>`t3`</li><li>`oc3`</li><li>`lan`</li><li>`modem`</li></ul> |
| `domain` | Stringa | Dominio dell’ISP dell’utente. |
| `ipV4` | Stringa | Etichetta numerica assegnata a un dispositivo che fa parte di una rete di computer che utilizza il protocollo Internet per la comunicazione (32 bit). |
| `ipV6` | Stringa | Etichetta numerica assegnata a un dispositivo che fa parte di una rete di computer che utilizza il protocollo Internet per la comunicazione (128 bit). |
| `operatingSystem` | Stringa | Il nome del sistema operativo utilizzato al momento dell’osservazione. L’attributo non deve contenere informazioni sulla versione, come `10.5.3`, ma contengono invece designazioni di &quot;edizione&quot; come `Ultimate` o `Professional`. |
| `operatingSystemVendor` | Stringa | Il nome del fornitore del sistema operativo utilizzato al momento dell’osservazione. |
| `operatingSystemVersion` | Stringa | L’identificatore della versione completa del sistema operativo utilizzato al momento dell’osservazione. Le versioni sono generalmente composte da numeri, ma possono essere in un formato definito dal fornitore. |
| `type` | Stringa | Il tipo di ambiente dell’applicazione. Consulta la [appendice](#type) per i valori accettati. |
| `viewportHeight` | Intero | La dimensione verticale in pixel della finestra in cui è stata visualizzata l’esperienza. Per un evento di visualizzazione web, corrisponde all’altezza del riquadro di visualizzazione del browser. |
| `viewPortWidth` | Intero | La dimensione orizzontale in pixel della finestra in cui è stata visualizzata l’esperienza. Per un evento di visualizzazione web, corrisponde alla larghezza del riquadro di visualizzazione del browser. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.schema.json)

## Appendice

La sezione seguente contiene informazioni aggiuntive sulle [!UICONTROL Dispositivo] tipo di dati.

## Valori accettati per il tipo {#type}

La tabella seguente illustra i valori accettati per `type` e il significato associato:

| Valore | Descrizione |
| --- | --- |
| `browser` | Browser |
| `application` | Applicazione |
| `iot` | Internet degli oggetti |
| `external` | Sistema esterno |
| `widget` | Estensione dell&#39;applicazione |
