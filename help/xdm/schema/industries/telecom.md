---
solution: Experience Platform
title: Settore delle telecomunicazioni Modello dati ERD
description: Visualizza un diagramma di relazione tra entità (ERD) che descrive un modello di dati standardizzato per il settore delle telecomunicazioni, compatibile con Experience Data Model (XDM) per l’utilizzo in Adobe Experience Platform.
exl-id: 96f267ce-a177-4384-a512-841c89d942ba
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 1%

---

# [!UICONTROL Telecomunicazioni] ERD

Il seguente schema di relazioni tra entità (ERD) rappresenta un modello di dati standardizzato per l&#39;industria delle telecomunicazioni. L&#39;ERD viene presentato intenzionalmente in modo denormalizzato e tenendo conto del modo in cui i dati vengono memorizzati in Adobe Experience Platform.

>[!NOTE]
>
>L’ERD come descritto è una raccomandazione su come modellare i dati per questo caso d’uso del settore. Per utilizzare questo modello dati in Platform, è necessario creare autonomamente gli schemi consigliati e le relative relazioni. Consulta le guide sulla gestione [schemi](../../ui/resources/schemas.md) e [relazioni](../../tutorials/relationship-ui.md) nell’interfaccia utente di per ulteriori informazioni.

Utilizzare la seguente legenda per interpretare questo ERD:

* Ogni entità indicata in si basa su un sottostante [Classe Experience Data Model (XDM)](../composition.md#class).
* Per una determinata entità, ogni riga contrassegnata in **audace** rappresenta un gruppo di campi o un tipo di dati, con i campi pertinenti che fornisce elencati di seguito in un testo senza bolle.
* I campi più importanti per una determinata entità sono evidenziati in rosso.
* Tutte le proprietà che possono essere utilizzate per identificare i singoli clienti sono contrassegnate come &quot;identità&quot;, con una di queste proprietà contrassegnata come &quot;identità principale&quot;.
* Le relazioni di entità sono contrassegnate come non dipendenti, poiché gli eventi basati su cookie spesso non possono determinare la persona o la persona che ha eseguito la transazione.


![](../../images/industries/telecom.png)

>[!NOTE]
>
>L’entità Experience Event include un campo &quot;_ID&quot; che rappresenta l’identificatore univoco (`_id`) fornita dalla classe ExperienceEvent XDM. Vedere il documento di riferimento su [ExperienceEvent XDM](../../classes/experienceevent.md) per ulteriori dettagli su cosa ci si aspetta da questo valore.

## [!UICONTROL Telecomunicazioni] casi d&#39;uso

La tabella seguente illustra le classi e i gruppi di campi dello schema consigliati per diversi casi d’uso comuni per l’industria delle telecomunicazioni.

| Caso d’uso | Classi e gruppi di campi consigliati |
| --- | --- |
| Comprendere i clienti che sono buoni candidati alle opportunità di upselling o cross-selling in base alle loro attuali partecipazioni e al loro comportamento di navigazione. | <ul><li>**[ExperienceEvent XDM](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Dettagli di upselling]](../../field-groups/event/upsell-details.md)</li><li>[[!UICONTROL Dettagli aggiornamento]](../../field-groups/event/upgrade-details.md)</li></ul></li><li>**[[!UICONTROL Profilo individuale XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Abbonamento a domicilio]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL Dettagli demografici]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Dati di contatto personali]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| Effettua il retargeting dell’abbandono del carrello tramite annunci pertinenti ed e-mail personalizzate automatizzate. Elimina gli annunci quando vengono convertiti. | <ul><li>**[ExperienceEvent XDM](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Dettagli Commerce]](../../field-groups/event/upsell-details.md) (Per catturare carrelli abbandonati)</li></ul></li><li>**[[!UICONTROL Profilo individuale XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Abbonamento a domicilio]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL Dettagli demografici]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Dati di contatto personali]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| Quando un cliente è identificato come probabile abbandono (in base a un&#39;interazione del dipendente o a un algoritmo automatizzato di apprendimento automatico), invia i dettagli del cliente ai canali digitali e non digitali. | <ul><li>**[ExperienceEvent XDM](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Dettagli di marketing per le campagne]](../../field-groups/event/campaign-marketing-details.md)</li><li>[[!UICONTROL Dettagli canale]](../../field-groups/event/channel-details.md)</li><li>Un gruppo di campi personalizzato contenente contenuto personalizzato</li></ul></li><li>**[[!UICONTROL Profilo individuale XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Dettagli demografici]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Dati di contatto personali]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}
