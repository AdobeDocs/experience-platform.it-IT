---
title: Gruppo di campi schema azioni scheda
description: Scopri il gruppo di campi schema Azioni con carta.
exl-id: 49851544-9118-4b73-b1d1-4cf49b3f1dee
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 8%

---

# [!UICONTROL Azioni carta] gruppo di campi schema

[!UICONTROL Azioni carta] è un gruppo di campi di schema standard per [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Il gruppo di campi fornisce un singolo `personalFinances.cardActions` a uno schema, che acquisisce i dettagli relativi a un’azione della carta come il tipo di carta, lo stato di attivazione e lo stato di blocco.

![](../../images/field-groups/card-actions.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `cardActivated` | Intero | Tiene traccia di quando la carta è stata attivata con successo. |
| `cardActivationStart` | Intero | Tiene traccia di quando il processo di attivazione della carta è stato avviato. |
| `cardCancelled` | Intero | Tiene traccia di quando una carta è stata annullata. |
| `cardControlsLocked` | Intero | Monitora quando i controlli di una carta sono stati bloccati. |
| `cardControlsUnlocked` | Intero | Monitora quando i controlli di una carta sono stati sbloccati. |
| `cardID` | Stringa | L’identificatore della scheda che si sta attivando. Questo valore potrebbe essere diverso dal numero della carta. |
| `cardLocked` | Intero | Monitora quando una carta è stata bloccata. |
| `cardOrderNew` | Intero | Tiene traccia di quando una carta è stata richiesta. |
| `cardOrderType` | Stringa | Il tipo di ordine della carta associato a un evento di ordine della carta. |
| `cardType` | Stringa | Il tipo di carta. |
| `cardUnlocked` | Intero | Monitora quando una carta è stata sbloccata. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta [archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-card-actions.schema.json).
