---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;persona;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati della persona
description: Scopri il tipo di dati Person Experience Data Model (XDM).
exl-id: f28a52be-90c7-4ed0-a460-97165bb58046
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 3%

---

# [!UICONTROL Persona] tipo di dati

[!UICONTROL Persona] è un tipo di dati Experience Data Model (XDM) standard che descrive una singola persona. Questo tipo di dati può rappresentare una persona che svolge vari ruoli, ad esempio un cliente, un contatto o un proprietario.

<img src="../images/data-types/person.PNG" width="500" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `name` | [[!UICONTROL Nome della persona]](./person-name.md) | Descrive i dettagli relativi al nome completo della persona. |
| `birthDate` | Data | La data completa di nascita di una persona. Il formato della data (senza ora) deve seguire il [RFC 3339, paragrafo 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) standard. |
| `birthDayAndMonth` | Stringa | Il giorno e il mese di nascita di una persona, nel formato MM-GG. Questo campo deve essere utilizzato quando il giorno e il mese di nascita di una persona sono noti, ma non l’anno. Il formato di questa proprietà deve essere conforme a questa espressione regolare `[0-1][0-9]-[0-9][0-9]`. |
| `birthYear` | Intero | L’anno di nascita di una persona incluso il secolo (ad esempio, `1983`). Questo campo deve essere utilizzato quando si conosce solo l’età della persona e non la data di nascita completa. Questo valore deve essere compreso tra 1 e 32767. |
| `gender` | Stringa | L’identità di genere della persona. Il valore di questa proprietà deve essere uguale a uno dei seguenti valori enum noti. <li> `female` </li> <li> `male` </li> <li> `not_specified` </li> <li> `non_specific` </li> Il valore predefinito è `not_specified`. |
| `maritalStatus` | Stringa | Descrive la relazione di una persona con un altro soggetto significativo. Il valore di questa proprietà deve essere uguale a uno dei seguenti valori enum. <li> `married` </li> <li> `single` </li> <li> `divorced` </li> <li> `widowed` </li> <li> `not_specified` </li> Il valore predefinito è `not_specified`. |
| `nationality` | Stringa | Il rapporto giuridico tra una persona e il suo stato rappresentato utilizzando il codice ISO 3166-1 Alpha-2. Il formato di questa proprietà deve essere conforme a questa espressione regolare `^[A-Z]{2}$`. |
| `taxId` | Stringa | Il codice fiscale della persona, ad esempio il codice fiscale (Taxpayer Identification Number, TIN) negli Stati Uniti o il Certificado de Identificación Fiscal (CIF/NIF) in Spagna. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.schema.json)
