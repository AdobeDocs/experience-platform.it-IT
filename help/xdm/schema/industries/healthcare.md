---
title: Medicale Settore Dati Modello ERD
description: Visualizzare un diagramma di relazione tra entità (ERD) che descrive un modello di dati standardizzato per il settore sanitario. Questo modello dati è compatibile con Experience Data Model (XDM) per l’utilizzo in Adobe Experience Platform.
source-git-commit: 721059a87347e371228d00edeac141afa894af47
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 1%

---

# [!UICONTROL Medicale] ERD

Il seguente schema di relazione tra entità (ERD) rappresenta un modello di dati standardizzato per il settore sanitario. L&#39;ERD viene presentato intenzionalmente in modo denormalizzato e tenendo conto del modo in cui i dati vengono memorizzati in Adobe Experience Platform.

>[!NOTE]
>
>L’ERD come descritto è una raccomandazione su come modellare i dati per questo caso d’uso del settore. Per utilizzare questo modello dati in Platform, è necessario creare autonomamente gli schemi consigliati e le relative relazioni. Consulta le guide sulla gestione [schemi](../../ui/resources/schemas.md) e [relazioni](../../tutorials/relationship-ui.md) nell’interfaccia utente di per ulteriori informazioni.

Utilizzare la seguente legenda per interpretare questo ERD:

* Ogni entità indicata in si basa su un sottostante [Classe Experience Data Model (XDM)](../composition.md#class).
* Per una determinata entità, ogni riga contrassegnata in **audace** rappresenta un gruppo di campi o un tipo di dati, con i campi pertinenti che fornisce elencati di seguito in un testo senza bolle.
* I campi più importanti per una determinata entità sono evidenziati in rosso.
* Tutte le proprietà che possono essere utilizzate per identificare i singoli clienti sono contrassegnate come &quot;identità&quot;, con una di queste proprietà contrassegnata come &quot;identità principale&quot;.
* Le relazioni di entità sono contrassegnate come non dipendenti, poiché gli eventi basati su cookie spesso non possono determinare la persona o la persona che ha eseguito la transazione.

![Immagine che mostra il diagramma del rapporto di entità per il modello dati del settore sanitario](../../images/industries/healthcare.png)

>[!NOTE]
>
>Ogni entità include un campo &quot;_ID&quot; che rappresenta l’identificatore stringa univoco (`_id`) per il record o l&#39;evento in questione. Questo campo viene utilizzato per tenere traccia dell&#39;univocità del singolo record o evento, impedire la duplicazione dei dati e cercare tali dati nei servizi a valle. In alcuni casi, `_id` può essere [Identificatore univoco universale (UUID)](https://tools.ietf.org/html/rfc4122) o [Identificatore univoco globale (GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>È importante distinguere che **questo campo non rappresenta un&#39;identità correlata a una singola persona** ma piuttosto la registrazione dei dati stessi. I dati di identità relativi a una persona, un evento o un’entità aziendale devono essere relegati a [campi di identità](../composition.md#identity) forniti invece da gruppi di campi compatibili.

## [!UICONTROL Medicale] casi d&#39;uso

La tabella seguente illustra le classi e i gruppi di campi dello schema consigliati per diversi casi d&#39;uso comuni per l&#39;assistenza sanitaria.

| Caso d’uso | Classi e gruppi di campi consigliati |
| --- | --- |
| Migliorare l&#39;acquisizione digitale e l&#39;esperienza dei consumatori che acquistano un&#39;assicurazione. Gli esempi includono: <ul><li>Quando le persone accedono a una pagina contenente informazioni generali (come piani, nomi/livelli di piano, medicaid, programmi di benessere e così via), devono comprendere il loro comportamento e ciò che cercano per inviare e-mail promozionali o indirizzarle su piattaforme di terze parti con annunci.</li><li>Quando le persone cercano informazioni sulla salute del cuore e sui vaccini, inviano loro informazioni relative ai vaccini sulla salute del cuore per creare consapevolezza del marchio o chiedono loro di programmare vaccini.</li></ul> | <ul><li>**[[!UICONTROL Profilo individuale XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Dettagli dei membri del settore sanitario]](../../field-groups/profile/healthcare-member-details.md)</li><li>Campo o campi di relazione stabiliti tra `planID` attributi e schemi che utilizzano [!UICONTROL Pianificare] classe.</li></ul></li><li>**[[!UICONTROL Pagatore]](../../classes/payer.md)**</li><li>**[[!UICONTROL Pianificare]](../../classes/plan.md)**:<ul><li>[[!UICONTROL Dettagli sul piano sanitario]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL ExperienceEvent XDM]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Dettagli applicazione]](../../field-groups/event/application-details.md)</li><li>[[!UICONTROL Dettagli Sitetool]](../../field-groups/event/sitetool-details.md)</li><li>[[!UICONTROL  Dettagli di marketing per le campagne]](../../field-groups/event/campaign-marketing-details.md)</li></ul></li></ul> |
| Aumentare l&#39;acquisizione digitale dei pazienti attraverso annunci mirati basati su comportamenti e dati sanitari online passati. | <ul><li>**[[!UICONTROL Profilo individuale XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Dettagli dei membri del settore sanitario]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Provider]](../../classes/provider.md)**:<ul><li>[[!UICONTROL Fornitore sanitario]](../../field-groups/provider/healthcare-provider.md)</li></ul></li><li>**[[!UICONTROL ExperienceEvent XDM]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Dettagli Web]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Dettagli sulla pubblicità]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| Migliorare l&#39;iscrizione e la creazione di account nei piani sanitari monitorando il marketing dell&#39;assicurazione attraverso diversi canali, al fine di capire come un cliente ha scoperto di una compagnia assicurativa. | <ul><li>**[[!UICONTROL Profilo individuale XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Dettagli dei membri del settore sanitario]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Pagatore]](../../classes/payer.md)**</li><li>**[[!UICONTROL Pianificare]](../../classes/plan.md)**:<ul><li>[[!UICONTROL Dettagli sul piano sanitario]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL ExperienceEvent XDM]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Dettagli Web]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Dettagli sulla pubblicità]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| Evitare la perdita della copertura assicurativa medica. | <ul><li>**[[!UICONTROL Profilo individuale XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Dettagli dei membri del settore sanitario]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Pianificare]](../../classes/plan.md)**:<ul><li>[[!UICONTROL Dettagli sul piano sanitario]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li></ul> |
| Promuovere le informazioni sui farmaci ai provider utilizzando annunci diretti ai clienti (DTC). | <ul><li>**[[!UICONTROL Profilo individuale XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Dettagli dei membri del settore sanitario]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Medicina]](../../classes/medication.md)**:<ul><li>[[!UICONTROL Medicina sanitaria]](../../field-groups/medication/healthcare-medication.md)</li></ul></li><li>**[[!UICONTROL ExperienceEvent XDM]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Dettagli Web]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Dettagli sulla pubblicità]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
