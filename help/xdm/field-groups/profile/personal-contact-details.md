---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;personal details;Schema design;field group;Field group;
solution: Experience Platform
title: Gruppo campi schema dettagli contatti personali
topic-legacy: overview
description: Questo documento fornisce una panoramica del gruppo di campi dello schema Dettagli contatto personali.
exl-id: a78d9aee-ecf6-45a9-b270-cdad5b800a86
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 4%

---


# [!UICONTROL Personal Contact Details] schema field group

>[!NOTE]
>
>Sono stati modificati i nomi di diversi gruppi di campi dello schema. See the document on [field group name updates](../name-updates.md) for more information.

[!UICONTROL Contatti personali ] Consente di specificare un gruppo di campi schema standard per la  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) classe, che descrive le informazioni di contatto per una singola persona.

![](../../images/field-groups/personal-contact-details.png)

| Proprietà | Data type | Descrizione |
| --- | --- | --- |
| `faxPhone` | [Numero di telefono](../../data-types/phone-number.md) | Descrive il numero di fax della persona. |
| `homeAddress` | [Indirizzo postale](../../data-types/postal-address.md) | Describes the person&#39;s residential address. |
| `homePhone` | [Numero di telefono](../../data-types/phone-number.md) | Descrive il numero di telefono di casa della persona. |
| `mobilePhone` | [Phone number](../../data-types/phone-number.md) | Descrive il numero di cellulare della persona. |
| `personalEmail` | [Indirizzo e-mail](../../data-types/email-address.md) | Describes the person&#39;s email address. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)
