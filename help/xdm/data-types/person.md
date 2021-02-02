---
keywords: ' Experience Platform;home;argomenti comuni;schema;schema;XDM;campi;schemi;persona;tipo di dati;tipo di dati;tipo di dati;'
solution: Experience Platform
title: Tipo di dati Persona
topic: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM (Person Experience Data Model).
translation-type: tm+mt
source-git-commit: 194b604d4b23f2acfaa4243155b04a6793fb0727
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 4%

---


# [!UICONTROL Person] tipo di dati

[!UICONTROL Person] è un tipo di dati XDM (Experience Data Model) standard che descrive una singola persona. Questo tipo di dati può rappresentare una persona che agisce in vari ruoli, ad esempio un cliente, un contatto o un proprietario.

<img src="../images/data-types/person.PNG" width="500" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `name` | [[!UICONTROL Person name]](./person-name.md) | Descrive i dettagli relativi al nome completo della persona. |
| `birthDate` | Data | La data completa in cui è nata una persona. Il formato della data (senza tempo) deve seguire lo standard [RFC 3339, sezione 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `birthDayAndMonth` | Stringa | Il giorno e il mese in cui è nata una persona, nel formato MM-GG. Questo campo deve essere utilizzato quando il giorno e il mese di nascita di una persona è noto, ma non l&#39;anno. Il formato di questa proprietà deve essere conforme a questa espressione regolare `[0-1][0-9]-[0-9][0-9]`. |
| `birthYear` | Intero | L&#39;anno in cui è nata una persona compreso il secolo (ad esempio, `1983`). Questo campo deve essere utilizzato quando solo l&#39;età della persona è nota e non la data di nascita completa. Il valore deve essere compreso tra 1 e 32767. |
| `gender` | Stringa | L&#39;identità di genere della persona. Il valore di questa proprietà deve essere uguale a uno dei seguenti valori enum noti. <li> `female` </li> <li> `male` </li> <li> `not_specified` </li> <li> `non_specific` </li> Il valore predefinito per questo valore è `not_specified`. |
| `maritalStatus` | Stringa | Descrive la relazione di una persona con un&#39;altra importante. Il valore di questa proprietà deve essere uguale a uno dei seguenti valori enum. <li> `married` </li> <li> `single` </li> <li> `divorced` </li> <li> `widowed` </li> <li> `not_specified` </li> Il valore predefinito per questo valore è `not_specified`. |
| `nationality` | Stringa | La relazione giuridica tra una persona e il suo stato rappresentato utilizzando il codice alfa-2 ISO 3166-1. Il formato di questa proprietà deve essere conforme a questa espressione regolare `^[A-Z]{2}$`. |
| `taxId` | Stringa | L&#39;ID fiscale o fiscale della persona, ad esempio il Numero di identificazione del contribuente (TIN) negli Stati Uniti o il Certificato di identificazione fiscale (CIF/NIF) in Spagna. |

Per ulteriori dettagli sul tipo di dati, fare riferimento al repository XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.schema.json)