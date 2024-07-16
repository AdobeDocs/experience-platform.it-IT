---
title: Modello dati del settore sanitario ERD
description: Visualizzare un diagramma di relazione entità (ERD) che descrive un modello di dati standardizzato per il settore sanitario. Questo modello dati è compatibile con Experience Data Model (XDM) per l’utilizzo in Adobe Experience Platform.
exl-id: ebcf97ec-f5a4-46e5-b1ad-c80d55aa2c6e
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 0%

---

# [!UICONTROL Healthcare] modello di dati di settore ERD

Il seguente diagramma di relazione tra entità (ERD) rappresenta un modello di dati standardizzato per il settore sanitario. L&#39;ERD viene presentato intenzionalmente in modo denormalizzato e tenendo in considerazione il modo in cui i dati vengono memorizzati in Adobe Experience Platform.

>[!NOTE]
>
>Il documento ERD descritto è un consiglio su come modellare i dati per questo caso d’uso del settore. Per utilizzare questo modello dati in Platform, è necessario creare autonomamente gli schemi consigliati e le relative relazioni. Per ulteriori informazioni, consulta le guide sulla gestione di [schemi](../../ui/resources/schemas.md) e [relazioni](../../tutorials/relationship-ui.md) nell&#39;interfaccia utente.

Utilizzare la seguente legenda per interpretare questa ERD:

* Ogni entità mostrata in è basata su una classe sottostante di [Experience Data Model (XDM)](../composition.md#class).
* Per una determinata entità, ogni riga contrassegnata in **bold** rappresenta un gruppo di campi o un tipo di dati, con i campi pertinenti forniti elencati di seguito in formato testo non in grassetto.
* I campi più importanti per una determinata entità sono evidenziati in rosso.
* Tutte le proprietà che possono essere utilizzate per identificare i singoli clienti sono contrassegnate come &quot;identità&quot; e una di queste proprietà è contrassegnata come &quot;identità primaria&quot;.
* Le relazioni tra entità sono contrassegnate come non dipendenti, poiché gli eventi basati su cookie spesso non possono determinare la persona o l’individuo che ha eseguito la transazione.

![Immagine che mostra il diagramma delle relazioni tra le entità per il modello dati del settore sanitario](../../images/industries/healthcare.png)

>[!NOTE]
>
>Ogni entità include un campo &quot;_ID&quot; che rappresenta l&#39;attributo univoco dell&#39;identificatore di stringa (`_id`) per il record o l&#39;evento in questione. Questo campo viene utilizzato per tenere traccia dell’univocità del singolo record o evento, evitare la duplicazione dei dati e cercare tali dati nei servizi a valle. In alcuni casi, `_id` può essere un [Identificatore univoco universale (UUID)](https://tools.ietf.org/html/rfc4122) o [Identificatore univoco globale (GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>È importante distinguere che **questo campo non rappresenta un&#39;identità correlata a una singola persona**, ma il record dei dati stessi. I dati di identità relativi a una persona, un evento o un&#39;entità business devono essere relegati a [campi di identità](../composition.md#identity) forniti da gruppi di campi compatibili.

## [!UICONTROL Casi d&#39;uso per l&#39;assistenza sanitaria]

La tabella seguente illustra le classi e i gruppi di campi di schema consigliati per diversi casi d’uso comuni di assistenza sanitaria.

| Caso d’uso | Classi e gruppi di campi consigliati |
| --- | --- |
| Migliorare l’acquisizione digitale e l’esperienza tra i consumatori che acquistano prodotti assicurativi. Gli esempi includono: <ul><li>Quando le persone accedono a una pagina contenente informazioni generali (come piani, nomi/livelli del piano, medicaid, programmi per il benessere e così via), comprendono il loro comportamento e cosa stanno cercando per inviare e-mail promozionali o targetizzarli su piattaforme di terze parti con annunci.</li><li>Quando le persone cercano informazioni sulla salute cardiaca e sui vaccini, inviano loro informazioni relative alla salute cardiaca per creare consapevolezza del marchio o chiedono di pianificare i vaccini.</li></ul> | <ul><li>**[[!UICONTROL Profilo individuale XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Dettagli Membro Del Settore Sanitario]](../../field-groups/profile/healthcare-member-details.md)</li><li>Campo/i di relazione stabilito/i tra gli attributi `planID` e gli schemi che utilizzano la classe [!UICONTROL Plan].</li></ul></li><li>**[[!UICONTROL Pagatore]](../../classes/payer.md)**</li><li>**[[!UICONTROL Piano]](../../classes/plan.md)**:<ul><li>[[!UICONTROL Dettagli piano sanitario]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Dettagli applicazione]](../../field-groups/event/application-details.md)</li><li>[[!UICONTROL Dettagli Sitetool]](../../field-groups/event/sitetool-details.md)</li><li>[[!UICONTROL  dettagli marketing campagna]](../../field-groups/event/campaign-marketing-details.md)</li></ul></li></ul> |
| Aumentare l’acquisizione digitale dei pazienti tramite annunci mirati basati sui comportamenti online e sui dati sanitari passati. | <ul><li>**[[!UICONTROL Profilo individuale XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Dettagli Membro Del Settore Sanitario]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Provider]](../../classes/provider.md)**:<ul><li>[[!UICONTROL Provider assistenza sanitaria]](../../field-groups/provider/healthcare-provider.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Dettagli Web]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Dettagli Advertising]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| Migliorare l’iscrizione e la creazione di account nei piani sanitari monitorando il marketing dell’assicurazione attraverso diversi canali, al fine di comprendere in che modo un cliente ha scoperto di una società di assicurazione. | <ul><li>**[[!UICONTROL Profilo individuale XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Dettagli Membro Del Settore Sanitario]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Pagatore]](../../classes/payer.md)**</li><li>**[[!UICONTROL Piano]](../../classes/plan.md)**:<ul><li>[[!UICONTROL Dettagli piano sanitario]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Dettagli Web]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Dettagli Advertising]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| Evitare interruzioni nella copertura assicurativa medica. | <ul><li>**[[!UICONTROL Profilo individuale XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Dettagli Membro Del Settore Sanitario]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Piano]](../../classes/plan.md)**:<ul><li>[[!UICONTROL Dettagli piano sanitario]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li></ul> |
| Promuovi le informazioni sui farmaci ai provider che utilizzano annunci diretti ai clienti (DTC). | <ul><li>**[[!UICONTROL Profilo individuale XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Dettagli Membro Del Settore Sanitario]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Medicinale]](../../classes/medication.md)**:<ul><li>[[!UICONTROL Medicinale sanitario]](../../field-groups/medication/healthcare-medication.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Dettagli Web]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Dettagli Advertising]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
