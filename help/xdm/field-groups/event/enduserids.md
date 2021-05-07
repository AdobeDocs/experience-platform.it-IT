---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;ExperienceEvent;campi;schemi;progettazione schema;gruppo di campi;gruppo di campi;enduserids;utente finale;utente finale;id;
solution: Experience Platform
title: Gruppo campi schema dettagli ID utente finale
topic-legacy: overview
description: Questo documento fornisce una panoramica del gruppo di campi dello schema Dettagli ID utente finale.
exl-id: ff5b74f4-7700-4d10-821e-b50f80ea8c05
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---


# [!UICONTROL End User ID Details] gruppo di campi schema

>[!NOTE]
>
>Sono stati modificati i nomi di diversi gruppi di campi dello schema. Per ulteriori informazioni, consulta il documento sugli [aggiornamenti dei nomi dei gruppi di campi](../name-updates.md) .

[!UICONTROL End User ID Details] è un gruppo di campi di schema standard per la  [[!DNL XDM ExperienceEvent] classe](../../classes/individual-profile.md), utilizzato per descrivere le informazioni di identità di un individuo in diverse applicazioni di Adobe. Il gruppo di campi fornisce un oggetto a livello principale `endUserIDs`, che a sua volta contiene un campo di sola lettura `_experience` i cui valori vengono aggiornati automaticamente al momento dell’acquisizione dei dati.

<img src="../../images/field-groups/enduserids.png" width="700" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `aacustomid` | [Identità](../../data-types/identity.md) | ID utente finale personalizzati per Adobe Analytics Cloud. |
| `aaid` | [Identità](../../data-types/identity.md) | ID utente finale per Adobe Analytics Cloud. |
| `acid` | [Identità](../../data-types/identity.md) | ID utente finale per Adobe Campaign. |
| `adcloud` | [Identità](../../data-types/identity.md) | ID utente finale per Adobe Advertising Cloud. |
| `emailid` | [Identità](../../data-types/identity.md) | ID degli indirizzi e-mail. |
| `mcid` | [Identità](../../data-types/identity.md) | Adobe Marketing Cloud ID. |
| `phonenumberid` | [Identità](../../data-types/identity.md) | ID dei numeri di telefono. |
| `tntid` | [Identità](../../data-types/identity.md) | ID utente finale per Adobe Target. |

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.schema.json)
