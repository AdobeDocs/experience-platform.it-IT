---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;profilo individuale;campi;schemi;schemi;dettagli personali;progettazione schema;gruppo di campi;gruppo di campi;
solution: Experience Platform
title: Gruppo campi schema dettagli contatti personali
topic-legacy: overview
description: Questo documento fornisce una panoramica del gruppo di campi dello schema Dettagli contatto personali.
exl-id: a78d9aee-ecf6-45a9-b270-cdad5b800a86
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 2%

---


# [!UICONTROL Gruppo di campi ] Dettagli contatto personale

>[!NOTE]
>
>Sono stati modificati i nomi di diversi gruppi di campi dello schema. Per ulteriori informazioni, consulta il documento sugli [aggiornamenti dei nomi dei gruppi di campi](../name-updates.md) .

[!UICONTROL Contatti personali ] Consente di specificare un gruppo di campi schema standard per la  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) classe, che descrive le informazioni di contatto per una singola persona.

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

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.schema.json)
