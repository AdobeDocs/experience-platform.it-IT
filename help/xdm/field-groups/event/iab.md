---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;ExperienceEvent;campi;schemi;progettazione schema;gruppo di campi;gruppo di campi;iab;tcf;consenso;
solution: Experience Platform
title: Gruppo di campi di consenso IAB TCF 2.0 per gli schemi di eventi
topic-legacy: overview
description: Questo documento fornisce una panoramica del gruppo di campi dello schema di consenso IAB TCF 2.0 per la classe ExperienceEvent XDM.
exl-id: c236d0d4-27bd-45d7-a912-d0e93a609254
source-git-commit: 046486d5e154b45fc2c2f5408eee235dddf46a4d
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 1%

---

# [!UICONTROL Consenso IAB TCF 2.0] gruppo di campi per gli schemi evento

>[!IMPORTANT]
>
>Il presente documento riguarda [!UICONTROL Consenso IAB TCF 2.0] gruppo di campi dello schema per la classe ExperienceEvent XDM. Utilizzare questo gruppo di campi solo se si intende tenere traccia degli eventi di modifica del consenso nel tempo.
>
>I valori di consenso registrati nei dati dell’evento non vengono rispettati nei flussi di lavoro di implementazione automatica. Affinché l’applicazione automatica avvenga, i valori di consenso devono essere acquisiti nella classe Profilo individuale XDM e attivati per il profilo cliente in tempo reale.
>
>Per il gruppo di campi destinato alla classe Profilo individuale XDM, consulta quanto segue [documento](../profile/iab.md) invece.

[!UICONTROL Consenso IAB TCF 2.0] è un gruppo di campi di schema standard per [[!DNL XDM ExperienceEvent] Classe](../../classes/experienceevent.md) utilizzato per acquisire le stringhe di consenso IAB di una serie con marca temporale, al fine di tenere traccia dei pattern di modifica del consenso nel tempo.

![](../../images/field-groups/iab-event.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `consentStrings` | Array di [Stringhe di consenso](../../data-types/consent-string.md) | Matrice di valori stringa di consenso associati all&#39;evento. |

{style=&quot;table-layout:auto&quot;}

Consulta la guida su [Supporto IAB TCF 2.0 in Platform](../../../landing/governance-privacy-security/consent/iab/overview.md) per ulteriori informazioni sul caso d’uso di questo gruppo di campi. Per ulteriori dettagli sul gruppo di campi stesso, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.schema.json)
