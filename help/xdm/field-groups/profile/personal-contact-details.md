---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;profilo individuale;campi;schemi;schemi;dettagli personali;schema design;gruppo di campi;gruppo di campi;
solution: Experience Platform
title: Gruppo di campi dello schema dei dettagli di contatto personali
description: In questo documento viene fornita una panoramica del gruppo di campi dello schema Dettagli contatto personale.
exl-id: a78d9aee-ecf6-45a9-b270-cdad5b800a86
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 3%

---


# [!UICONTROL Dettagli di contatto personali] gruppo di campi schema

>[!NOTE]
>
>I nomi di diversi gruppi di campi dello schema sono stati modificati. Vedi il documento su [aggiornamenti nome gruppo di campi](../name-updates.md) per ulteriori informazioni.

[!UICONTROL Dettagli di contatto personali] è un gruppo di campi di schema standard per [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md) che descrive le informazioni di contatto di una singola persona.

![](../../images/field-groups/personal-contact-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `faxPhone` | [Numero di telefono](../../data-types/phone-number.md) | Descrive il numero di fax della persona. |
| `homeAddress` | [Indirizzo postale](../../data-types/postal-address.md) | Descrive l’indirizzo dell’abitazione della persona. |
| `homePhone` | [Numero di telefono](../../data-types/phone-number.md) | Descrive il numero di telefono dell&#39;abitazione della persona. |
| `mobilePhone` | [Numero di telefono](../../data-types/phone-number.md) | Descrive il numero di telefono cellulare della persona. |
| `personalEmail` | [Indirizzo e-mail](../../data-types/email-address.md) | Descrive l’indirizzo e-mail della persona. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)
