---
keywords: ' Experience Platform;home;argomenti popolari;schema;schema;XDM;ExperienceEvent;fields;schemas;Schema design;mixin;mixin;enduserids;end user;end user;ids;'
solution: Experience Platform
title: Mixin dettagli ID utente finale
topic: overview
description: Questo documento fornisce una panoramica del mixin Dettagli ID utente finale.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 1%

---


# [!UICONTROL End User ID Details] mixin

>[!NOTE]
>
>I nomi di diversi mixin sono cambiati. Per ulteriori informazioni, consulta il documento relativo agli [aggiornamenti del nome del mixin](../name-updates.md).

[!UICONTROL End User ID Details] è un mixin standard per la  [[!DNL XDM ExperienceEvent] classe](../../classes/individual-profile.md), utilizzato per descrivere le informazioni di identità di un individuo in diverse applicazioni  Adobe. Il mixin fornisce un oggetto a livello principale `endUserIDs`, che a sua volta contiene un campo di sola lettura `_experience` i cui valori vengono automaticamente aggiornati durante l&#39;assimilazione dei dati.

<img src="../../images/mixins/enduserids.png" width="700" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `aacustomid` | [Identità](../../data-types/identity.md) | ID utente finale personalizzati per Adobe Analytics Cloud. |
| `aaid` | [Identità](../../data-types/identity.md) | ID utente finale per Adobe Analytics Cloud. |
| `acid` | [Identità](../../data-types/identity.md) | ID utente finale per  Adobe Campaign. |
| `adcloud` | [Identità](../../data-types/identity.md) | ID utente finale per Adobe Advertising Cloud. |
| `emailid` | [Identità](../../data-types/identity.md) | ID indirizzo e-mail. |
| `mcid` | [Identità](../../data-types/identity.md) | Adobe Marketing Cloud ID. |
| `phonenumberid` | [Identità](../../data-types/identity.md) | ID dei numeri di telefono. |
| `tntid` | [Identità](../../data-types/identity.md) | ID utente finale per  Adobe Target. |

Per ulteriori dettagli sul mixin, fare riferimento al repository XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.schema.json)
