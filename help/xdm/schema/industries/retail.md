---
solution: Experience Platform
title: Modello dati retail
topic-legacy: overview
description: Visualizza un modello dati standardizzato per il settore retail, compatibile con Experience Data Model (XDM) per l’utilizzo in Adobe Experience Platform.
exl-id: 40cbb243-668b-4280-815f-1f94a06b6b87
source-git-commit: 9c5a4e064af0b46ff30b41afef71ca2fd3503a82
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---

#  Modello dati retail

Il seguente schema di relazione tra entità (ERD) rappresenta un modello di dati standardizzato per il settore retail. L&#39;ERD viene presentato intenzionalmente in modo denormalizzato e tenendo conto del modo in cui i dati vengono memorizzati in Adobe Experience Platform.

Utilizzare la seguente legenda per interpretare questo ERD:

* Ogni entità visualizzata in è basata su una classe [Experience Data Model (XDM) sottostante](../composition.md#class).
* Per una determinata entità, ogni riga contrassegnata in **grassetto** rappresenta un gruppo di campi o un tipo di dati, con i campi pertinenti che fornisce elencati di seguito nel testo senza bolli.
* I campi più importanti per una determinata entità sono evidenziati in rosso.
* Tutte le proprietà che possono essere utilizzate per identificare i singoli clienti sono contrassegnate come &quot;identità&quot;, con una di queste proprietà contrassegnata come &quot;identità principale&quot;.
* Le relazioni di entità sono contrassegnate come non dipendenti, poiché gli eventi basati su cookie spesso non possono determinare la persona o la persona che ha eseguito la transazione.

![](../../images/industries/retail.png)

>[!NOTE]
>
>L&#39;entità Experience Event include un campo &quot;_ID&quot; che rappresenta l&#39;attributo di identificatore univoco (`_id`) fornito dalla classe ExperienceEvent XDM. Per ulteriori informazioni su ciò che ci si aspetta da questo valore, consulta il documento di riferimento su [XDM ExperienceEvent](../../classes/experienceevent.md) .

##  Casi di utilizzo al dettaglio

La tabella seguente illustra le classi e i gruppi di campi di schema consigliati per diversi casi d’uso comuni per la vendita al dettaglio.

| Caso d’uso | Classi e gruppi di campi consigliati |
| --- | --- |
| Combina le origini dati online e offline e risolvi l’identità tra dispositivi e online/offline per fornire rapporti di attribuzione olistici tra canali e dispositivi diversi. | <ul><li>**[ExperienceEvent XDM](../../classes/experienceevent.md)**:<ul><li>[Dettagli Commerce](../../field-groups/event/commerce-details.md)</li><li>[Dettagli Web](../../field-groups/event/web-details.md)</li></ul></li><li>**Prodotto**  (classe personalizzata)\*:<ul><li>Prodotto (gruppo di campi personalizzato)\*</li></ul></li></ul> |
| Offri esperienze mirate e personalizzate per vari segmenti per aumentare i ricavi e migliorare la piattaforma nell’orchestrazione omnicanale. | <ul><li>**[ExperienceEvent XDM](../../classes/experienceevent.md)**:<ul><li>[Dettagli di marketing per le campagne](../../field-groups/event/campaign-marketing-details.md)</li><li>[Dettagli canale](../../field-groups/event/channel-details.md)</li><li>[Dettagli Commerce](../../field-groups/event/commerce-details.md)</li><li>[Dettagli dell&#39;ambiente](../../field-groups/event/environment-details.md)</li><li>[Dettagli Web](../../field-groups/event/web-details.md)</li></ul></li><li>**[Profilo](../../classes/individual-profile.md)** individuale XDM:<ul><li>[Dettagli demografici](../../field-groups/profile/demographic-details.md)</li><li>[Dati di contatto personali](../../field-groups/profile/personal-contact-details.md)</li><li>[Dettagli contatto lavoro](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| Analizza l’attribuzione multi-touch per migliorare l’efficienza del marketing. | <ul><li>**[ExperienceEvent XDM](../../classes/experienceevent.md)**:<ul><li>[Dettagli di marketing per le campagne](../../field-groups/event/campaign-marketing-details.md)</li><li>[Dettagli canale](../../field-groups/event/channel-details.md)</li><li>[Dettagli Commerce](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[Profilo](../../classes/individual-profile.md)** individuale XDM:<ul><li>[Dettagli demografici](../../field-groups/profile/demographic-details.md)</li></ul></li></ul> |
| Migliorare la pertinenza delle e-mail grazie a una segmentazione migliorata tra uomini e donne. | <ul><li>**[ExperienceEvent XDM](../../classes/experienceevent.md)**:<ul><li>[Dettagli Commerce](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[Profilo](../../classes/individual-profile.md)** individuale XDM:<ul><li>[Dettagli demografici](../../field-groups/profile/demographic-details.md)</li></ul></li><li>**Prodotto**  (classe personalizzata)\*:<ul><li>Prodotto (gruppo di campi personalizzato)\*</li></ul></li></ul> |
| Acquisisci dati fedeltà (partner) per aumentare le informazioni rilevanti sui prodotti su canali web, e-mail e di marketing digitale. | <ul><li>**[ExperienceEvent XDM](../../classes/experienceevent.md)**:<ul><li>[Dettagli Web](../../field-groups/event/web-details.md)</li></ul></li><li>**[Profilo](../../classes/individual-profile.md)** individuale XDM:<ul><li>[Dettagli demografici](../../field-groups/profile/demographic-details.md)</li><li>[Dettagli fedeltà](../../field-groups/profile/loyalty-details.md)</li></ul></li><li>**Prodotto**  (classe personalizzata)\*:<ul><li>Prodotto (gruppo di campi personalizzato)\*</li></ul></li></ul> |
| Effettua il retargeting dell’abbandono del carrello tramite e-mail automatizzate e personalizzate. | <ul><li>**[ExperienceEvent XDM](../../classes/experienceevent.md)**:<ul><li>[Dettagli Commerce](../../field-groups/event/commerce-details.md)</li><li>[Dettagli Web](../../field-groups/event/web-details.md)</li></ul></li><li>**Prodotto**  (classe personalizzata)\*:<ul><li>Prodotto (gruppo di campi personalizzato)\*</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}

*\*Mentre una classe di prodotto standard è pianificata per una versione futura, gli schemi di prodotto devono essere attualmente generati utilizzando una classe personalizzata. Pertanto, è necessario creare manualmente la struttura della classe dello schema e quella di tutti i gruppi di campi aggiunti a tale classe. Per ulteriori informazioni, consulta la sezione su [creazione di una classe personalizzata](../../ui/resources/classes.md#create) nella guida all&#39;interfaccia utente XDM.*
