---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;profilo individuale;campi;schemi;schemi;dettagli personali;progettazione schema;gruppo di campi;gruppo di campi;
solution: Experience Platform
title: Gruppo campi schema dettagli contatti personali
description: Questo documento fornisce una panoramica del gruppo di campi dello schema Dettagli contatto personali.
exl-id: a78d9aee-ecf6-45a9-b270-cdad5b800a86
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 5%

---


# [!UICONTROL Dati di contatto personali] gruppo di campi schema

>[!NOTE]
>
>Sono stati modificati i nomi di diversi gruppi di campi dello schema. Visualizza il documento in [aggiornamenti dei nomi dei gruppi di campi](../name-updates.md) per ulteriori informazioni.

[!UICONTROL Dati di contatto personali] è un gruppo di campi di schema standard per [[!DNL XDM Individual Profile] Classe](../../classes/individual-profile.md) che descrive le informazioni di contatto per una singola persona.

![](../../images/field-groups/personal-contact-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `faxPhone` | [Numero di telefono](../../data-types/phone-number.md) | Descrive il numero di fax della persona. |
| `homeAddress` | [Indirizzo postale](../../data-types/postal-address.md) | Descrive l&#39;indirizzo residenziale della persona. |
| `homePhone` | [Numero di telefono](../../data-types/phone-number.md) | Descrive il numero di telefono di casa della persona. |
| `mobilePhone` | [Numero di telefono](../../data-types/phone-number.md) | Descrive il numero di cellulare della persona. |
| `personalEmail` | [Indirizzo e-mail](../../data-types/email-address.md) | Descrive l&#39;indirizzo e-mail della persona. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)
