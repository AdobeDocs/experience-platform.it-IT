---
solution: Experience Platform
title: Modello dati del settore delle telecomunicazioni ERD
description: Visualizzare un ERD (Entity Relationship Diagramma) che descrive un modello dati standardizzato per il settore delle telecomunicazioni, compatibile con Experience Data Model (XDM) per l'utilizzo in Adobe Experience Platform.
exl-id: 96f267ce-a177-4384-a512-841c89d942ba
source-git-commit: 23bf89977b13a1f51e1ea7a0bb0561522a09745d
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# [!UICONTROL Telecomunicazioni] modello dati di settore ERD

Il seguente schema di relazione tra entità (ERD) rappresenta un modello di dati standardizzato per il settore delle telecomunicazioni. L&#39;ERD viene presentato intenzionalmente in modo denormalizzato e tenendo in considerazione il modo in cui i dati vengono memorizzati in Adobe Experience Platform.

>[!NOTE]
>
>Il documento ERD descritto è un consiglio su come modellare i dati per questo caso d’uso del settore. Per utilizzare questo modello dati in Platform, è necessario creare autonomamente gli schemi consigliati e le relative relazioni. Per ulteriori informazioni, consulta le guide sulla gestione di [schemi](../../ui/resources/schemas.md) e [relazioni](../../tutorials/relationship-ui.md) nell&#39;interfaccia utente.

Utilizzare la seguente legenda per interpretare questa ERD:

* Ogni entità mostrata in è basata su una classe sottostante di [Experience Data Model (XDM)](../composition.md#class).
* I campi rientrati sotto un campo padre rappresentano un campo figlio, o campo secondario, che appartiene al gruppo di campi padre.
* I campi più importanti per una determinata entità sono evidenziati in rosso.
* Tutte le proprietà che possono essere utilizzate per identificare i singoli clienti sono contrassegnate come &quot;identità&quot; e una di queste proprietà è contrassegnata come &quot;identità primaria&quot;.
* Le relazioni tra entità sono contrassegnate come non dipendenti, poiché gli eventi basati su cookie spesso non possono determinare la persona o l’individuo che ha eseguito la transazione.


![Un esempio di ERD per un modello dati del settore delle telecomunicazioni](../../images/industries/telecom.png)

>[!NOTE]
>
>L&#39;entità Experience Event include un campo &quot;_ID&quot; che rappresenta l&#39;attributo dell&#39;identificatore univoco (`_id`) fornito dalla classe XDM ExperienceEvent. Per ulteriori dettagli su ciò che è previsto per questo valore, consulta il documento di riferimento su [XDM ExperienceEvent](../../classes/experienceevent.md).

## [!UICONTROL Casi d&#39;uso per le telecomunicazioni]

La tabella seguente illustra le classi e i gruppi di campi di schema consigliati per diversi casi d’uso comuni per il settore delle telecomunicazioni.

| Caso d’uso | Classi e gruppi di campi consigliati |
| --- | --- |
| Comprendi i clienti che sono buoni candidati per opportunità di upselling o cross-selling in base alle loro attuali partecipazioni e al loro comportamento di navigazione. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Dettagli di upselling]](../../field-groups/event/upsell-details.md)</li><li>[[!UICONTROL Dettagli aggiornamento]](../../field-groups/event/upgrade-details.md)</li></ul></li><li>**[[!UICONTROL Profilo individuale XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Abbonamento Telecom]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL Dettagli demografici]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Dati personali]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| Effettua il retargeting degli utenti che abbandonano il carrello attraverso annunci pertinenti e e-mail personalizzate automatizzate. Elimina gli annunci durante la conversione. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Dettagli Commerce]](../../field-groups/event/upsell-details.md) (per acquisire gli abbandoni del carrello)</li></ul></li><li>**[[!UICONTROL Profilo individuale XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Abbonamento Telecom]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL Dettagli demografici]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Dati personali]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| Quando un cliente è contrassegnato come probabile abbandono (in base a un’interazione con i dipendenti o a un algoritmo di apprendimento automatico automatizzato), invia i dettagli del cliente ai canali digitali e non digitali. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Dettagli marketing campagna]](../../field-groups/event/campaign-marketing-details.md)</li><li>[[!UICONTROL Dettagli canale]](../../field-groups/event/channel-details.md)</li><li>Un gruppo di campi personalizzato contenente contenuti personalizzati</li></ul></li><li>**[[!UICONTROL Profilo individuale XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Dettagli demografici]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Dati personali]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |

{style="table-layout:auto"}
