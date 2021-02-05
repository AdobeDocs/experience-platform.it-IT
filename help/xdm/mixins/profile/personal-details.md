---
keywords: ' Experience Platform;home;argomenti popolari;schema;schema;XDM;profilo singolo;campi;schemi;schemi;dettagli personali;schema di progettazione;mixin;Mixin;'
solution: Experience Platform
title: Dati personali di contatto Mixin
topic: overview
description: Questo documento fornisce una panoramica del mixin Dettagli contatto personali.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 2%

---


# [!UICONTROL Personal Contact Details] mixin

>[!NOTE]
>
>I nomi di diversi mixin sono cambiati. Per ulteriori informazioni, consulta il documento relativo agli [aggiornamenti del nome del mixin](../name-updates.md).

[!UICONTROL Personal Contact Details] è un mixin standard per l&#39; [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) aula che descrive le informazioni di contatto per una singola persona.

<img src="../../images/mixins/profile-personal-details.png" width="700" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `faxPhone` | [Numero di telefono](../../data-types/phone-number.md) | Descrive il numero di fax della persona. |
| `homeAddress` | [Indirizzo postale](../../data-types/postal-address.md) | Descrive l&#39;indirizzo residenziale della persona. |
| `homePhone` | [Numero di telefono](../../data-types/phone-number.md) | Descrive il numero di telefono di casa della persona. |
| `mobilePhone` | [Numero di telefono](../../data-types/phone-number.md) | Descrive il numero di telefono cellulare della persona. |
| `personalEmail` | [Indirizzo e-mail](../../data-types/email-address.md) | Descrive l&#39;indirizzo e-mail della persona. |

Per ulteriori dettagli sul mixin, fare riferimento al repository XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.schema.json)
