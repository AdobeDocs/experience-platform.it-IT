---
solution: Experience Platform
title: Modello dati retail
description: Visualizza un modello dati standardizzato per il settore retail, compatibile con Experience Data Model (XDM) per l’utilizzo in Adobe Experience Platform.
exl-id: 40cbb243-668b-4280-815f-1f94a06b6b87
source-git-commit: 5ceb261dbf1cac58d0cfe620875b8fa7c761abf2
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 4%

---

# [!UICONTROL Retail] modello dati del settore

Il seguente schema di relazione tra entità (ERD) rappresenta un modello di dati standardizzato per il settore retail. L&#39;ERD viene presentato intenzionalmente in modo denormalizzato e tenendo conto del modo in cui i dati vengono memorizzati in Adobe Experience Platform.

>[!NOTE]
>
>L’ERD come descritto è una raccomandazione su come modellare i dati per questo caso d’uso del settore. Per utilizzare questo modello dati in Platform, è necessario creare autonomamente gli schemi consigliati e le relative relazioni. Consulta le guide sulla gestione [schemi](../../ui/resources/schemas.md) e [relazioni](../../tutorials/relationship-ui.md) nell’interfaccia utente di per ulteriori informazioni.

Utilizzare la seguente legenda per interpretare questo ERD:

* Ogni entità indicata in si basa su un sottostante [Classe Experience Data Model (XDM)](../composition.md#class).
* Per una determinata entità, ogni riga contrassegnata in **audace** rappresenta un gruppo di campi o un tipo di dati, con i campi pertinenti che fornisce elencati di seguito in un testo senza bolle.
* I campi più importanti per una determinata entità sono evidenziati in rosso.
* Tutte le proprietà che possono essere utilizzate per identificare i singoli clienti sono contrassegnate come &quot;identità&quot;, con una di queste proprietà contrassegnata come &quot;identità principale&quot;.
* Le relazioni di entità sono contrassegnate come non dipendenti, poiché gli eventi basati su cookie spesso non possono determinare la persona o la persona che ha eseguito la transazione.

![](../../images/industries/retail.png)

>[!NOTE]
>
>L’entità Experience Event include un campo &quot;_ID&quot; che rappresenta l’identificatore univoco (`_id`) fornita dalla classe ExperienceEvent XDM. Vedere il documento di riferimento su [ExperienceEvent XDM](../../classes/experienceevent.md) per ulteriori dettagli su cosa ci si aspetta da questo valore.

## [!UICONTROL Retail] casi d&#39;uso

La tabella seguente illustra le classi e i gruppi di campi di schema consigliati per diversi casi d’uso comuni per la vendita al dettaglio.

| Caso d’uso | Classi e gruppi di campi consigliati |
| --- | --- |
| Combina le origini dati online e offline e risolvi l’identità tra dispositivi e online/offline per fornire rapporti di attribuzione olistici tra canali e dispositivi diversi. | <ul><li>**[ExperienceEvent XDM](../../classes/experienceevent.md)**:<ul><li>[Dettagli Commerce](../../field-groups/event/commerce-details.md)</li><li>[Dettagli Web](../../field-groups/event/web-details.md)</li></ul></li><li>**[Prodotto](../../classes/product.md)**:<ul><li>[Catalogo dei prodotti](../../field-groups/product/product-catalog.md)</li><li>[Categoria di prodotti](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Offri esperienze mirate e personalizzate per vari segmenti per aumentare i ricavi e migliorare la piattaforma nell’orchestrazione omnicanale. | <ul><li>**[ExperienceEvent XDM](../../classes/experienceevent.md)**:<ul><li>[Dettagli di marketing per le campagne](../../field-groups/event/campaign-marketing-details.md)</li><li>[Dettagli canale](../../field-groups/event/channel-details.md)</li><li>[Dettagli Commerce](../../field-groups/event/commerce-details.md)</li><li>[Dettagli dell’ambiente](../../field-groups/event/environment-details.md)</li><li>[Dettagli Web](../../field-groups/event/web-details.md)</li></ul></li><li>**[Profilo individuale XDM](../../classes/individual-profile.md)**:<ul><li>[Dettagli demografici](../../field-groups/profile/demographic-details.md)</li><li>[Dati di contatto personali](../../field-groups/profile/personal-contact-details.md)</li><li>[Dettagli contatto lavoro](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| Analizza l’attribuzione multi-touch per migliorare l’efficienza del marketing. | <ul><li>**[ExperienceEvent XDM](../../classes/experienceevent.md)**:<ul><li>[Dettagli di marketing per le campagne](../../field-groups/event/campaign-marketing-details.md)</li><li>[Dettagli canale](../../field-groups/event/channel-details.md)</li><li>[Dettagli Commerce](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[Profilo individuale XDM](../../classes/individual-profile.md)**:<ul><li>[Dettagli demografici](../../field-groups/profile/demographic-details.md)</li></ul></li></ul> |
| Migliorare la pertinenza delle e-mail grazie a una segmentazione migliorata tra uomini e donne. | <ul><li>**[ExperienceEvent XDM](../../classes/experienceevent.md)**:<ul><li>[Dettagli Commerce](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[Profilo individuale XDM](../../classes/individual-profile.md)**:<ul><li>[Dettagli demografici](../../field-groups/profile/demographic-details.md)</li></ul></li><li>**[Prodotto](../../classes/product.md)**:<ul><li>[Catalogo dei prodotti](../../field-groups/product/product-catalog.md)</li><li>[Categoria di prodotti](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Acquisisci dati fedeltà (partner) per aumentare le informazioni rilevanti sui prodotti su canali web, e-mail e di marketing digitale. | <ul><li>**[ExperienceEvent XDM](../../classes/experienceevent.md)**:<ul><li>[Dettagli Web](../../field-groups/event/web-details.md)</li></ul></li><li>**[Profilo individuale XDM](../../classes/individual-profile.md)**:<ul><li>[Dettagli demografici](../../field-groups/profile/demographic-details.md)</li><li>[Dettagli fedeltà](../../field-groups/profile/loyalty-details.md)</li></ul></li><li>**[Prodotto](../../classes/product.md)**:<ul><li>[Catalogo dei prodotti](../../field-groups/product/product-catalog.md)</li><li>[Categoria di prodotti](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Effettua il retargeting dell’abbandono del carrello tramite e-mail automatizzate e personalizzate. | <ul><li>**[ExperienceEvent XDM](../../classes/experienceevent.md)**:<ul><li>[Dettagli Commerce](../../field-groups/event/commerce-details.md)</li><li>[Dettagli Web](../../field-groups/event/web-details.md)</li></ul></li><li>**[Prodotto](../../classes/product.md)**:<ul><li>[Catalogo dei prodotti](../../field-groups/product/product-catalog.md)</li><li>[Categoria di prodotti](../../field-groups/product/product-category.md)</li></ul></li></ul> |

{style="table-layout:auto"}
