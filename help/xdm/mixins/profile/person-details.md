---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;Schema design;mixin;mixin;person;person details;profile person details;person;
solution: Experience Platform
title: Mixin dettagli demografici
topic: overview
description: Questo documento fornisce una panoramica del mixin Dettagli demografici.
translation-type: tm+mt
source-git-commit: f9d8021643e72e3fbb5315b54a19815dcdaaa702
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 3%

---


# [!UICONTROL Demographic Details] mixin

>[!NOTE]
>
>I nomi di diversi mixin sono cambiati. Per ulteriori informazioni, consulta il documento sugli aggiornamenti [dei nomi dei](../name-updates.md) mixin.

[!UICONTROL Demographic Details] è un mixin standard per la [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). Il mixin fornisce un oggetto a livello principale, i cui sottocampi descrivono le informazioni relative a una singola persona. `person`

<img src="../../images/mixins/profile-person-details.png" width="600" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `person.name` | [Nome della persona](../../data-types/person-name.md) | Un oggetto i cui sottocampi descrivono vari elementi del nome di una persona. |
| `person.birthDate` | Data | Data completa in cui è nata una persona, sotto forma di timestamp ISO 8601. |
| `person.birthDayAndMonth` | Stringa | Il giorno e il mese in cui è nata una persona, nel formato MM-GG. Questo campo deve essere utilizzato quando il giorno e il mese di nascita di una persona è noto, ma non l&#39;anno. |
| `person.birthYear` | Intero | L&#39;anno in cui è nata una persona, compreso il secolo (come il 1989). Questo campo deve essere utilizzato quando è nota solo l&#39;età della persona, non la data di nascita completa. |
| `person.gender` | Stringa | L&#39;identità di genere della persona. |
| `person.martialStatus` | Stringa | Descrive la relazione di una persona con un&#39;altra importante. |
| `person.nationality` | Stringa | La relazione giuridica tra una persona e il suo stato rappresentato utilizzando il codice alfa-2 ISO 3166-1. |
| `person.taxId` | Stringa | ID fiscale/fiscale della persona, come il TIN negli Stati Uniti o il CIF/NIF in Spagna. |

Per ulteriori dettagli sul mixin, fare riferimento al repository XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.example.1.json)
* [Schema](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.schema.json)å completo