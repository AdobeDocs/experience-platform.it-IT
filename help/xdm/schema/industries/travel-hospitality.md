---
solution: Experience Platform
title: Settore del viaggio e dell'ospitalità Modello dati ERD
description: Visualizza un diagramma di relazione tra entità (ERD) che descrive un modello di dati standardizzato per il settore dei viaggi e dell’ospitalità, compatibile con Experience Data Model (XDM) per l’utilizzo in Adobe Experience Platform.
exl-id: 4d454160-9066-4702-815b-9509942f709e
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 1%

---

# [!UICONTROL Viaggi e ospitalità] ERD

Il seguente diagramma di relazione tra entità (ERD) rappresenta un modello di dati standardizzato per il settore dei viaggi e dell’ospitalità. L&#39;ERD viene presentato intenzionalmente in modo denormalizzato e tenendo conto del modo in cui i dati vengono memorizzati in Adobe Experience Platform.

>[!NOTE]
>
>L’ERD come descritto è una raccomandazione su come modellare i dati per questo caso d’uso del settore. Per utilizzare questo modello dati in Platform, è necessario creare autonomamente gli schemi consigliati e le relative relazioni. Consulta le guide sulla gestione [schemi](../../ui/resources/schemas.md) e [relazioni](../../tutorials/relationship-ui.md) nell’interfaccia utente di per ulteriori informazioni.

Utilizzare la seguente legenda per interpretare questo ERD:

* Ogni entità indicata in si basa su un sottostante [Classe Experience Data Model (XDM)](../composition.md#class).
* Per una determinata entità, ogni riga contrassegnata in **audace** rappresenta un gruppo di campi o un tipo di dati, con i campi pertinenti che fornisce elencati di seguito in un testo senza bolle.
* I campi più importanti per una determinata entità sono evidenziati in rosso.
* Tutte le proprietà che possono essere utilizzate per identificare i singoli clienti sono contrassegnate come &quot;identità&quot;, con una di queste proprietà contrassegnata come &quot;identità principale&quot;.
* Le relazioni di entità sono contrassegnate come non dipendenti, poiché gli eventi basati su cookie spesso non possono determinare la persona o la persona che ha eseguito la transazione.

![](../../images/industries/travel-hospitality.png)

>[!NOTE]
>
>L’entità Experience Event include un campo &quot;_ID&quot; che rappresenta l’identificatore univoco (`_id`) fornita dalla classe ExperienceEvent XDM. Vedere il documento di riferimento su [ExperienceEvent XDM](../../classes/experienceevent.md) per ulteriori dettagli su cosa ci si aspetta da questo valore.

## [!UICONTROL Viaggi e ospitalità] casi d&#39;uso

La tabella seguente illustra le classi e i gruppi di campi dello schema consigliati per diversi casi d’uso comuni per il settore dei viaggi e dell’ospitalità.

| Caso d’uso | Classi e gruppi di campi consigliati |
| --- | --- |
| Cena e altre attrazioni residenti all&#39;interno del mercato e ospiti con le prossime prenotazioni alberghiere. | <ul><li>**[ExperienceEvent XDM](../../classes/experienceevent.md)**:<ul><li>[Dettagli prenotazione](../../field-groups/event/reservation-details.md)</li><li>[Riserva](../../field-groups/event/lodging-reservation.md)</li><li>[Prenotazione pranzo](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[Profilo individuale XDM](../../classes/individual-profile.md)**:<ul><li>[Dettagli demografici](../../field-groups/profile/demographic-details.md)</li><li>[Dati di contatto personali](../../field-groups/profile/personal-contact-details.md)</li><li>[Dettagli contatto lavoro](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| Cena e altre attrazioni residenti all&#39;interno del mercato e ospiti con le prossime prenotazioni alberghiere. | <ul><li>**[ExperienceEvent XDM](../../classes/experienceevent.md)**:<ul><li>[Dettagli prenotazione](../../field-groups/event/reservation-details.md)</li><li>[Prenotazione pranzo](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[Profilo individuale XDM](../../classes/individual-profile.md)**:<ul><li>[Dettagli demografici](../../field-groups/profile/demographic-details.md)</li><li>[Dati di contatto personali](../../field-groups/profile/personal-contact-details.md)</li><li>[Dettagli contatto lavoro](../../field-groups/profile/work-contact-details.md)</li><li>[Dettagli fedeltà](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Vendere hotel e altre attrazioni residenti per gli ospiti all&#39;interno del mercato e gli ospiti con le prossime prenotazioni alberghiere. | <ul><li>**[ExperienceEvent XDM](../../classes/experienceevent.md)**:<ul><li>[Dettagli prenotazione](../../field-groups/event/reservation-details.md)</li><li>[Riserva](../../field-groups/event/lodging-reservation.md)</li></ul></li><li>**[Profilo individuale XDM](../../classes/individual-profile.md)**:<ul><li>[Dettagli demografici](../../field-groups/profile/demographic-details.md)</li><li>[Dati di contatto personali](../../field-groups/profile/personal-contact-details.md)</li><li>[Dettagli contatto lavoro](../../field-groups/profile/work-contact-details.md)</li><li>[Dettagli fedeltà](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Voli e altre attrazioni residenti all&#39;interno del mercato e ospiti con le prossime prenotazioni alberghiere. | <ul><li>**[ExperienceEvent XDM](../../classes/experienceevent.md)**:<ul><li>[Dettagli prenotazione](../../field-groups/event/reservation-details.md)</li><li>[Riserva di volo](../../field-groups/event/flight-reservation.md)</li></ul></li><li>**[Profilo individuale XDM](../../classes/individual-profile.md)**:<ul><li>[Dettagli demografici](../../field-groups/profile/demographic-details.md)</li><li>[Dati di contatto personali](../../field-groups/profile/personal-contact-details.md)</li><li>[Dettagli contatto lavoro](../../field-groups/profile/work-contact-details.md)</li><li>[Dettagli fedeltà](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}
