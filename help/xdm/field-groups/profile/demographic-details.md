---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;profilo individuale;campi;schemi;schemi;struttura dello schema;gruppo di campi;gruppo di campi;persona;dettagli persona;dettagli persona profilo;persona;
solution: Experience Platform
title: Gruppo di campi schema dettagli demografici
description: Scopri il gruppo di campi dello schema Dettagli demografici.
exl-id: 588c044c-b80d-4cb9-9f97-92f040d54bb4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 26%

---


# [!UICONTROL Dettagli demografici] gruppo di campi schema

>[!NOTE]
>
>I nomi di diversi gruppi di campi dello schema sono stati modificati. Per ulteriori informazioni, consulta il documento sugli aggiornamenti del nome del gruppo di campi [](../name-updates.md).

[!UICONTROL Dettagli demografici] è un gruppo di campi di schema standard per la [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). Il gruppo di campi fornisce un oggetto `person` di livello principale, i cui sottocampi descrivono informazioni su una singola persona.

![](../../images/field-groups/demographic-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `person.name` | [Nome persona](../../data-types/person-name.md) | Oggetto i cui sottocampi descrivono vari elementi del nome di una persona. |
| `person.birthDate` | Data | La data di nascita completa di una persona, sotto forma di marca temporale ISO 8601. |
| `person.birthDayAndMonth` | Stringa | Il giorno e il mese di nascita di una persona, nel formato MM-GG. Questo campo dovrebbe essere usato quando il giorno e il mese di nascita di una persona sono noti, ma non l’anno. |
| `person.birthYear` | Intero | L’anno di nascita di una persona, incluso il secolo (ad esempio 1989). Questo campo deve essere utilizzato quando si conosce solo l’età della persona, non la data di nascita completa. |
| `person.gender` | Stringa | L’identità di genere della persona. |
| `person.martialStatus` | Stringa | Descrive la relazione di una persona con un partner. |
| `person.nationality` | Stringa | Il rapporto giuridico tra una persona e il suo stato rappresentato utilizzando il codice ISO 3166-1 Alpha-2. |
| `person.taxId` | Stringa | L’ID fiscale della persona, ad esempio il TIN negli Stati Uniti o l’CIF/NIF in Spagna. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.schema.json)