---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;profilo individuale;campi;schemi;schemi;progettazione schema;mixin;mixin;dettagli lavoro;lavoro profilo;
solution: Experience Platform
title: Dettagli contatto lavoro Mixin
topic-legacy: overview
description: Questo documento fornisce una panoramica del mixin Dettagli contatto di lavoro.
exl-id: 0133622c-e95f-4833-b2f8-3694d41751b4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 2%

---

# [!UICONTROL Work Contact Details] mescolina

>[!NOTE]
>
>I nomi di diversi mixin sono cambiati. Per ulteriori informazioni, consulta il documento sugli [aggiornamenti dei nomi mixin](../name-updates.md) .

[!UICONTROL Work Contact Details] è un mixin standard per la  [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). Il mixin fornisce diversi campi che acquisiscono informazioni professionali relative a una singola persona, come indirizzo di lavoro, e-mail di lavoro, numero di telefono di lavoro e organizzazioni a cui la persona appartiene.

<img src="../../images/mixins/profile-work-details.png" width="550" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `workAddress` | [Indirizzo postale](../../data-types/postal-address.md) | Descrive l&#39;indirizzo di lavoro della persona. |
| `workEmail` | [Indirizzo e-mail](../../data-types/email-address.md) | Descrive l&#39;indirizzo e-mail di lavoro della persona. |
| `workPhone` | [Numero di telefono](../../data-types/phone-number.md) | Descrive il numero di telefono di lavoro della persona. |
| `organizations` | Stringa (Array) | Array di stringhe in formato libero che rappresentano le organizzazioni di cui la persona è membro. |

Per ulteriori dettagli sul mixin, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.schema.json)
