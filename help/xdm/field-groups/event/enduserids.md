---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;ExperienceEvent;campi;schemi;progettazione schema;gruppo di campi;gruppo di campi;enduserids;utente finale;utente finale;id;
solution: Experience Platform
title: Gruppo campi schema dettagli ID utente finale
topic-legacy: overview
description: Questo documento fornisce una panoramica del gruppo di campi dello schema Dettagli ID utente finale.
exl-id: ff5b74f4-7700-4d10-821e-b50f80ea8c05
source-git-commit: e33d59c4ac28f55ba6ae2fc073d02f8738159263
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 5%

---


# [!UICONTROL Dettagli ID utente finale] gruppo di campi schema

>[!NOTE]
>
>Sono stati modificati i nomi di diversi gruppi di campi dello schema. Visualizza il documento in [aggiornamenti dei nomi dei gruppi di campi](../name-updates.md) per ulteriori informazioni.

[!UICONTROL Dettagli ID utente finale] è un gruppo di campi di schema standard per [[!DNL XDM ExperienceEvent] Classe](../../classes/experienceevent.md), utilizzato per descrivere le informazioni di identità di una persona in diverse applicazioni di Adobe. Il gruppo di campi fornisce un livello principale `endUserIDs` oggetto, che contiene un oggetto di sola lettura `_experience` i cui valori vengono aggiornati automaticamente durante l’acquisizione dei dati.

<img src="../../images/field-groups/enduserids.png" width="700" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `aacustomid` | [Identità](../../data-types/identity.md) | ID utente finale personalizzati per Adobe Analytics Cloud. |
| `aaid` | [Identità](../../data-types/identity.md) | ID utente finale per Adobe Analytics Cloud. |
| `acid` | [Identità](../../data-types/identity.md) | ID utente finale per Adobe Campaign. |
| `adcloud` | [Identità](../../data-types/identity.md) | ID utente finale per Adobe Advertising Cloud. |
| `emailid` | [Identità](../../data-types/identity.md) | ID degli indirizzi e-mail. |
| `mcid` | [Identità](../../data-types/identity.md) | Adobe Marketing Cloud ID (MCID). Il MCID è ora noto come ID Experience Cloud (ECID). |
| `phonenumberid` | [Identità](../../data-types/identity.md) | ID dei numeri di telefono. |
| `tntid` | [Identità](../../data-types/identity.md) | ID utente finale per Adobe Target. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.schema.json)
