---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;ExperienceEvent;campi;schemi;progettazione schema;gruppo di campi;gruppo di campi;enduserids;utente finale;utente finale;id;
solution: Experience Platform
title: Gruppo campi schema dettagli ID utente finale
topic-legacy: overview
description: Questo documento fornisce una panoramica del gruppo di campi dello schema Dettagli ID utente finale.
exl-id: ff5b74f4-7700-4d10-821e-b50f80ea8c05
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 2%

---


# [!UICONTROL Gruppo di campi ] Dettagli ID utente finale

>[!NOTE]
>
>The names of several schema field groups have changed. Per ulteriori informazioni, consulta il documento sugli [aggiornamenti dei nomi dei gruppi di campi](../name-updates.md) .

[!UICONTROL ID utente finale ] Consente di specificare un gruppo di campi di schema standard per la  [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md), utilizzato per descrivere le informazioni di identità di un individuo in diverse applicazioni di Adobe. Il gruppo di campi fornisce un oggetto a livello principale `endUserIDs`, che a sua volta contiene un campo di sola lettura `_experience` i cui valori vengono aggiornati automaticamente al momento dell’acquisizione dei dati.

<img src="../../images/field-groups/enduserids.png" width="700" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `aacustomid` | [Identità](../../data-types/identity.md) | ID utente finale personalizzati per Adobe Analytics Cloud. |
| `aaid` | [Identity](../../data-types/identity.md) | End user IDs for Adobe Analytics Cloud. |
| `acid` | [Identità](../../data-types/identity.md) | End user IDs for Adobe Campaign. |
| `adcloud` | [Identità](../../data-types/identity.md) | ID utente finale per Adobe Advertising Cloud. |
| `emailid` | [Identity](../../data-types/identity.md) | ID degli indirizzi e-mail. |
| `mcid` | [Identity](../../data-types/identity.md) | Adobe Marketing Cloud ID. |
| `phonenumberid` | [Identità](../../data-types/identity.md) | Phone number IDs. |
| `tntid` | [Identità](../../data-types/identity.md) | End user IDs for Adobe Target. |

{style=&quot;table-layout:auto&quot;}

For more details on the field group, refer to the public XDM repository:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.example.1.json)
* [Full schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.schema.json)
