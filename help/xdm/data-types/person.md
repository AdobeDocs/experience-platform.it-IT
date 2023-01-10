---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;persona;tipo di dati;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati persona
description: Questo documento fornisce una panoramica del tipo di dati XDM (Person Experience Data Model).
exl-id: f28a52be-90c7-4ed0-a460-97165bb58046
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 5%

---

# [!UICONTROL Persona] tipo di dati

[!UICONTROL Persona] è un tipo di dati XDM (Experience Data Model) standard che descrive una singola persona. Questo tipo di dati può rappresentare una persona che agisce in vari ruoli, ad esempio un cliente, un contatto o un proprietario.

<img src="../images/data-types/person.PNG" width="500" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `name` | [[!UICONTROL Nome della persona]](./person-name.md) | Descrive i dettagli relativi al nome completo della persona. |
| `birthDate` | Data | La data completa in cui è nata una persona. Il formato della data (senza tempo) deve seguire il [RFC 3339, sezione 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) standard. |
| `birthDayAndMonth` | Stringa | Il giorno e il mese in cui è nata una persona, nel formato MM-DD. Questo campo deve essere utilizzato quando è noto il giorno e il mese della nascita di una persona, ma non l&#39;anno. Il formato di questa proprietà deve essere conforme a questa espressione regolare `[0-1][0-9]-[0-9][0-9]`. |
| `birthYear` | Intero | L&#39;anno in cui una persona è nata, compreso il secolo (per esempio, `1983`). Questo campo deve essere utilizzato quando si conosce solo l&#39;età della persona e non la data di nascita completa. Questo valore deve essere compreso tra 1 e 32767. |
| `gender` | Stringa | L&#39;identità di genere della persona. Il valore di questa proprietà deve essere uguale a uno dei seguenti valori enum noti. <li> `female` </li> <li> `male` </li> <li> `not_specified` </li> <li> `non_specific` </li> Il valore predefinito è `not_specified`. |
| `maritalStatus` | Stringa | Descrive il rapporto di una persona con un altro significativo. Il valore di questa proprietà deve essere uguale a uno dei seguenti valori enum. <li> `married` </li> <li> `single` </li> <li> `divorced` </li> <li> `widowed` </li> <li> `not_specified` </li> Il valore predefinito è `not_specified`. |
| `nationality` | Stringa | Il rapporto giuridico tra una persona e il suo stato rappresentato utilizzando il codice Alpha-2 ISO 3166-1. Il formato di questa proprietà deve essere conforme a questa espressione regolare `^[A-Z]{2}$`. |
| `taxId` | Stringa | ID fiscale o fiscale della persona, ad esempio il numero di identificazione del contribuente (TIN) negli Stati Uniti o il certificato di identificazione fiscale (CIF/NIF) in Spagna. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.schema.json)
