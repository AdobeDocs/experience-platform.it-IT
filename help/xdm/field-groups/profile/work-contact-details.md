---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;Schema design;mixin;mixins;work details;profile work;
solution: Experience Platform
title: Work Contact Details Schema Field Group
topic-legacy: overview
description: Questo documento fornisce una panoramica del gruppo di campi dello schema Dettagli contatto di lavoro.
exl-id: 0133622c-e95f-4833-b2f8-3694d41751b4
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 3%

---


# [!UICONTROL Gruppo di campi ] Dettagli contatto ufficio

>[!NOTE]
>
>The names of several schema field groups have changed. Per ulteriori informazioni, consulta il documento sugli [aggiornamenti dei nomi dei gruppi di campi](../name-updates.md) .

[!UICONTROL Work Contact Details] is a standard schema field group for the [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md). Il gruppo di campi fornisce diversi campi che acquisiscono informazioni professionali relative a una singola persona, ad esempio indirizzo di lavoro, e-mail di lavoro, numero di telefono di lavoro e organizzazioni a cui la persona appartiene.

![](../../images/field-groups/work-contact-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `workAddress` | [Postal address](../../data-types/postal-address.md) | Descrive l&#39;indirizzo di lavoro della persona. |
| `workEmail` | [Indirizzo e-mail](../../data-types/email-address.md) | Descrive l&#39;indirizzo e-mail di lavoro della persona. |
| `workPhone` | [Numero di telefono](../../data-types/phone-number.md) | Descrive il numero di telefono di lavoro della persona. |
| `organizations` | String (Array) | An array of free-form strings that represent the organizations the person is a member of. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-work-details.example.1.json)
* [Full schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-work-details.schema.json)
