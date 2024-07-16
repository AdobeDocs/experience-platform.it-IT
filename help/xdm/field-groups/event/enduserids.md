---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;ExperienceEvent;campi;schemi;schemi;struttura dello schema;gruppo di campi;gruppo di campi;enduserids;utente finale;id;
solution: Experience Platform
title: Gruppo di campi dello schema Dettagli ID utente finale
description: Scopri il gruppo di campi dello schema Dettagli ID utente finale.
exl-id: ff5b74f4-7700-4d10-821e-b50f80ea8c05
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 6%

---


# [!UICONTROL Dettagli ID utente finale] gruppo di campi schema

>[!NOTE]
>
>I nomi di diversi gruppi di campi dello schema sono stati modificati. Per ulteriori informazioni, consulta il documento sugli aggiornamenti del nome del gruppo di campi [](../name-updates.md).

[!UICONTROL Dettagli ID utente finale] è un gruppo di campi dello schema standard per la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md), utilizzato per descrivere le informazioni sull&#39;identità di un individuo in diverse applicazioni di Adobe. Il gruppo di campi fornisce un oggetto `endUserIDs` di livello principale, che contiene un campo `_experience` di sola lettura i cui valori vengono aggiornati automaticamente durante l&#39;acquisizione dei dati.

<img src="../../images/field-groups/enduserids.png" width="700" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `aacustomid` | [Identità](../../data-types/identity.md) | ID personalizzati degli utenti finali per Adobe Analytics Cloud. |
| `aaid` | [Identità](../../data-types/identity.md) | ID degli utenti finali per Adobe Analytics Cloud. |
| `acid` | [Identità](../../data-types/identity.md) | ID degli utenti finali per Adobe Campaign. |
| `adcloud` | [Identità](../../data-types/identity.md) | ID degli utenti finali per Adobe Advertising Cloud. |
| `emailid` | [Identità](../../data-types/identity.md) | ID degli indirizzi e-mail. |
| `mcid` | [Identità](../../data-types/identity.md) | Adobe Marketing Cloud ID (MCID). Il MCID è ora noto come ID Experience Cloud (ECID). |
| `phonenumberid` | [Identità](../../data-types/identity.md) | ID dei numeri di telefono. |
| `tntid` | [Identità](../../data-types/identity.md) | ID degli utenti finali per Adobe Target. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.schema.json)
