---
solution: Experience Platform
title: Modello dati del settore viaggi e ospitalità ERD
description: Visualizzare un diagramma di relazione entità (ERD) che descrive un modello dati standardizzato per il settore dei viaggi e dell'ospitalità, compatibile con Experience Data Model (XDM) per l'utilizzo in Adobe Experience Platform.
exl-id: 4d454160-9066-4702-815b-9509942f709e
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# [!UICONTROL Viaggi e ospitalità] modello dati di settore ERD

Il seguente diagramma di relazione tra entità (ERD) rappresenta un modello di dati standardizzato per il settore dei viaggi e dell’ospitalità. L&#39;ERD viene presentato intenzionalmente in modo denormalizzato e tenendo in considerazione il modo in cui i dati vengono memorizzati in Adobe Experience Platform.

>[!NOTE]
>
>Il documento ERD descritto è un consiglio su come modellare i dati per questo caso d’uso del settore. Per utilizzare questo modello dati in Platform, è necessario creare autonomamente gli schemi consigliati e le relative relazioni. Consulta le guide sulla gestione di [schemi](../../ui/resources/schemas.md) e [relazioni](../../tutorials/relationship-ui.md) nell’interfaccia utente di per ulteriori informazioni.

Utilizzare la seguente legenda per interpretare questa ERD:

* Ogni entità mostrata in si basa su un sottostante [Classe Experience Data Model (XDM)](../composition.md#class).
* Per una determinata entità, ogni riga contrassegnata in **grassetto** rappresenta un gruppo di campi o un tipo di dati, con i campi pertinenti forniti elencati di seguito in testo non in grassetto.
* I campi più importanti per una determinata entità sono evidenziati in rosso.
* Tutte le proprietà che possono essere utilizzate per identificare i singoli clienti sono contrassegnate come &quot;identità&quot; e una di queste proprietà è contrassegnata come &quot;identità primaria&quot;.
* Le relazioni tra entità sono contrassegnate come non dipendenti, poiché gli eventi basati su cookie spesso non possono determinare la persona o l’individuo che ha eseguito la transazione.

![](../../images/industries/travel-hospitality.png)

>[!NOTE]
>
>L’entità Experience Event include un campo &quot;_ID&quot; che rappresenta l’identificatore univoco (`_id`) fornito dalla classe ExperienceEvent XDM. Vedi il documento di riferimento su [XDM ExperienceEvent](../../classes/experienceevent.md) per ulteriori dettagli su ciò che è previsto per questo valore.

## [!UICONTROL Viaggi e ospitalità] casi d’uso

La tabella seguente illustra le classi e i gruppi di campi di schema consigliati per diversi casi d’uso comuni per il settore dei viaggi e dell’ospitalità.

| Caso d’uso | Classi e gruppi di campi consigliati |
| --- | --- |
| Pranzo di cross-selling e altre attrazioni residenti per gli ospiti in-market e gli ospiti con imminenti prenotazioni di hotel. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Dettagli prenotazione](../../field-groups/event/reservation-details.md)</li><li>[Prenotazione alloggio](../../field-groups/event/lodging-reservation.md)</li><li>[Prenotazione ristorante](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[Profilo individuale XDM](../../classes/individual-profile.md)**:<ul><li>[Dettagli demografici](../../field-groups/profile/demographic-details.md)</li><li>[Dettagli di contatto personali](../../field-groups/profile/personal-contact-details.md)</li><li>[Dettagli contatto di lavoro](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| Ristoranti up-sell e altre attrazioni residenti per ospiti in-market e ospiti con imminenti prenotazioni alberghiere. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Dettagli prenotazione](../../field-groups/event/reservation-details.md)</li><li>[Prenotazione ristorante](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[Profilo individuale XDM](../../classes/individual-profile.md)**:<ul><li>[Dettagli demografici](../../field-groups/profile/demographic-details.md)</li><li>[Dettagli di contatto personali](../../field-groups/profile/personal-contact-details.md)</li><li>[Dettagli contatto di lavoro](../../field-groups/profile/work-contact-details.md)</li><li>[Dettagli fedeltà](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Hotel up-sell e altre attrazioni residenti per ospiti in-market e ospiti con imminenti prenotazioni alberghiere. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Dettagli prenotazione](../../field-groups/event/reservation-details.md)</li><li>[Prenotazione alloggio](../../field-groups/event/lodging-reservation.md)</li></ul></li><li>**[Profilo individuale XDM](../../classes/individual-profile.md)**:<ul><li>[Dettagli demografici](../../field-groups/profile/demographic-details.md)</li><li>[Dettagli di contatto personali](../../field-groups/profile/personal-contact-details.md)</li><li>[Dettagli contatto di lavoro](../../field-groups/profile/work-contact-details.md)</li><li>[Dettagli fedeltà](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Voli up-sell e altre attrazioni residenti per ospiti in-market e ospiti con imminenti prenotazioni alberghiere. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Dettagli prenotazione](../../field-groups/event/reservation-details.md)</li><li>[Prenotazione del volo](../../field-groups/event/flight-reservation.md)</li></ul></li><li>**[Profilo individuale XDM](../../classes/individual-profile.md)**:<ul><li>[Dettagli demografici](../../field-groups/profile/demographic-details.md)</li><li>[Dettagli di contatto personali](../../field-groups/profile/personal-contact-details.md)</li><li>[Dettagli contatto di lavoro](../../field-groups/profile/work-contact-details.md)</li><li>[Dettagli fedeltà](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |

{style="table-layout:auto"}
