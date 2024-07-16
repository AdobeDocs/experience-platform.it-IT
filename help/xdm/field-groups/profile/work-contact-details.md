---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;profilo individuale;campi;schemi;schemi;progettazione schema;mixin;mixin;dettagli lavoro;lavoro profilo;
solution: Experience Platform
title: Gruppo di campi schema Dettagli contatto di lavoro
description: Scopri il gruppo di campi dello schema Dettagli contatto di lavoro.
exl-id: 0133622c-e95f-4833-b2f8-3694d41751b4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 2%

---


# [!UICONTROL Dettagli contatto di lavoro] gruppo di campi dello schema

>[!NOTE]
>
>I nomi di diversi gruppi di campi dello schema sono stati modificati. Per ulteriori informazioni, consulta il documento sugli aggiornamenti del nome del gruppo di campi [](../name-updates.md).

[!UICONTROL Dettagli contatto di lavoro] è un gruppo di campi dello schema standard per la [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). Il gruppo di campi fornisce diversi campi che acquisiscono informazioni professionali relative a una singola persona, ad esempio l’indirizzo del luogo di lavoro, l’e-mail aziendale, il numero di telefono aziendale e le organizzazioni a cui la persona appartiene.

![](../../images/field-groups/work-contact-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `workAddress` | [Indirizzo postale](../../data-types/postal-address.md) | Descrive l’indirizzo di lavoro della persona. |
| `workEmail` | [Indirizzo e-mail](../../data-types/email-address.md) | Descrive l’indirizzo e-mail aziendale della persona. |
| `workPhone` | [Numero di telefono](../../data-types/phone-number.md) | Descrive il numero di telefono aziendale della persona. |
| `organizations` | Stringa (array) | Array di stringhe in formato libero che rappresentano le organizzazioni di cui l’utente è membro. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-work-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-work-details.schema.json)
