---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;Schema design;mixin;mixins;work details;profile work;
solution: Experience Platform
title: Mixaggio dei dettagli di lavoro profilo
topic: overview
description: Questo documento fornisce una panoramica della classe Profilo singolo XDM.
translation-type: tm+mt
source-git-commit: e58c669b5542453b7fbf6d90deedcd2cf349c0b6
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 3%

---


# [!UICONTROL Profile work details] mixin

[!UICONTROL Profile work details] è un mixin standard per la [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). Il mixin fornisce diversi campi che acquisiscono informazioni professionali relative a una singola persona, come l&#39;indirizzo di lavoro, l&#39;e-mail di lavoro, il numero di telefono di lavoro e le organizzazioni a cui la persona appartiene.

<img src="../../images/mixins/profile-work-details.png" width="550" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `workAddress` | [Indirizzo postale](../../data-types/postal-address.md) | Descrive l&#39;indirizzo di lavoro della persona. |
| `workEmail` | [Indirizzo e-mail](../../data-types/email-address.md) | Descrive l&#39;indirizzo e-mail dell&#39;utente. |
| `workPhone` | [Numero di telefono](../../data-types/phone-number.md) | Descrive il numero di telefono del lavoro della persona. |
| `organizations` | String (Array) | Un array di stringhe a forma libera che rappresentano le organizzazioni di cui la persona è membro. |

Per ulteriori dettagli sul mixin, fare riferimento al repository XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.schema.json)