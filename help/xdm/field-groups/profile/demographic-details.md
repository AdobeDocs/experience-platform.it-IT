---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;profilo individuale;campi;schemi;progettazione schema;schema;gruppo di campi;gruppo di campi;persona;dettagli persona;dettagli persona profilo;persona;
solution: Experience Platform
title: Gruppo campi schema dettagli demografici
description: Questo documento fornisce una panoramica del gruppo di campi schema Dettagli demografici.
exl-id: 588c044c-b80d-4cb9-9f97-92f040d54bb4
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 4%

---


# [!UICONTROL Dettagli demografici] gruppo di campi schema

>[!NOTE]
>
>Sono stati modificati i nomi di diversi gruppi di campi dello schema. Visualizza il documento in [aggiornamenti dei nomi dei gruppi di campi](../name-updates.md) per ulteriori informazioni.

[!UICONTROL Dettagli demografici] è un gruppo di campi di schema standard per [[!DNL XDM Individual Profile] Classe](../../classes/individual-profile.md). Il gruppo di campi fornisce un livello principale `person` oggetto , i cui sottocampi descrivono informazioni su una persona.

![](../../images/field-groups/demographic-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `person.name` | [Nome della persona](../../data-types/person-name.md) | Un oggetto i cui sottocampi descrivono vari elementi del nome di una persona. |
| `person.birthDate` | Data | La data completa in cui è nata una persona, sotto forma di marca temporale ISO 8601. |
| `person.birthDayAndMonth` | Stringa | Il giorno e il mese in cui è nata una persona, nel formato MM-DD. Questo campo deve essere utilizzato quando è noto il giorno e il mese della nascita di una persona, ma non l&#39;anno. |
| `person.birthYear` | Intero | L&#39;anno in cui è nata una persona, compreso il secolo (come il 1989). Questo campo deve essere utilizzato quando si conosce solo l&#39;età della persona, non la data di nascita completa. |
| `person.gender` | Stringa | L&#39;identità di genere della persona. |
| `person.martialStatus` | Stringa | Descrive il rapporto di una persona con un altro significativo. |
| `person.nationality` | Stringa | Il rapporto giuridico tra una persona e il suo stato rappresentato utilizzando il codice Alpha-2 ISO 3166-1. |
| `person.taxId` | Stringa | ID fiscale/fiscale della persona, ad esempio il TIN negli Stati Uniti o il CIF/NIF in Spagna. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.schema.json)