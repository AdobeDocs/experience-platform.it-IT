---
solution: Experience Platform
title: Modello dati del settore retail
description: Visualizza un modello dati standardizzato per il settore retail, compatibile con Experience Data Model (XDM) per l’utilizzo in Adobe Experience Platform.
exl-id: 40cbb243-668b-4280-815f-1f94a06b6b87
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 1%

---

# [!UICONTROL Retail] modello dati di settore

Il seguente diagramma di relazione tra entità (ERD) rappresenta un modello di dati standardizzato per il settore del commercio al dettaglio. L&#39;ERD viene presentato intenzionalmente in modo denormalizzato e tenendo in considerazione il modo in cui i dati vengono memorizzati in Adobe Experience Platform.

>[!NOTE]
>
>Il documento ERD descritto è un consiglio su come modellare i dati per questo caso d’uso del settore. Per utilizzare questo modello dati in Platform, è necessario creare autonomamente gli schemi consigliati e le relative relazioni. Consulta le guide sulla gestione di [schemi](../../ui/resources/schemas.md) e [relazioni](../../tutorials/relationship-ui.md) nell’interfaccia utente di per ulteriori informazioni.

Utilizzare la seguente legenda per interpretare questa ERD:

* Ogni entità mostrata in si basa su un sottostante [Classe Experience Data Model (XDM)](../composition.md#class).
* Per una determinata entità, ogni riga contrassegnata in **grassetto** rappresenta un gruppo di campi o un tipo di dati, con i campi pertinenti forniti elencati di seguito in testo non in grassetto.
* I campi più importanti per una determinata entità sono evidenziati in rosso.
* Tutte le proprietà che possono essere utilizzate per identificare i singoli clienti sono contrassegnate come &quot;identità&quot; e una di queste proprietà è contrassegnata come &quot;identità primaria&quot;.
* Le relazioni tra entità sono contrassegnate come non dipendenti, poiché gli eventi basati su cookie spesso non possono determinare la persona o l’individuo che ha eseguito la transazione.

![](../../images/industries/retail.png)

>[!NOTE]
>
>L’entità Experience Event include un campo &quot;_ID&quot; che rappresenta l’identificatore univoco (`_id`) fornito dalla classe ExperienceEvent XDM. Vedi il documento di riferimento su [XDM ExperienceEvent](../../classes/experienceevent.md) per ulteriori dettagli su ciò che è previsto per questo valore.

## [!UICONTROL Retail] casi d’uso

La tabella seguente illustra le classi e i gruppi di campi di schema consigliati per diversi casi d’uso comuni di vendita al dettaglio.

| Caso d’uso | Classi e gruppi di campi consigliati |
| --- | --- |
| Combina origini di dati online e offline e risolvi l’identità tra dispositivi e online/offline per fornire rapporti olistici di attribuzione tra canali e dispositivi. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Dettagli Commerce](../../field-groups/event/commerce-details.md)</li><li>[Dettagli web](../../field-groups/event/web-details.md)</li></ul></li><li>**[Prodotto](../../classes/product.md)**:<ul><li>[Catalogo prodotti](../../field-groups/product/product-catalog.md)</li><li>[Categoria di prodotto](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Fornisci esperienze mirate e personalizzate per vari segmenti per aumentare i ricavi e contribuire a migliorare la piattaforma nell’orchestrazione omnicanale. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Dettagli di marketing della campagna](../../field-groups/event/campaign-marketing-details.md)</li><li>[Dettagli canale](../../field-groups/event/channel-details.md)</li><li>[Dettagli Commerce](../../field-groups/event/commerce-details.md)</li><li>[Dettagli dell’ambiente](../../field-groups/event/environment-details.md)</li><li>[Dettagli web](../../field-groups/event/web-details.md)</li></ul></li><li>**[Profilo individuale XDM](../../classes/individual-profile.md)**:<ul><li>[Dettagli demografici](../../field-groups/profile/demographic-details.md)</li><li>[Dettagli di contatto personali](../../field-groups/profile/personal-contact-details.md)</li><li>[Dettagli contatto di lavoro](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| Analizza l’attribuzione multi-touch per migliorare l’efficienza del marketing. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Dettagli di marketing della campagna](../../field-groups/event/campaign-marketing-details.md)</li><li>[Dettagli canale](../../field-groups/event/channel-details.md)</li><li>[Dettagli Commerce](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[Profilo individuale XDM](../../classes/individual-profile.md)**:<ul><li>[Dettagli demografici](../../field-groups/profile/demographic-details.md)</li></ul></li></ul> |
| Migliorare la rilevanza delle e-mail migliorando la segmentazione tra uomini e donne. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Dettagli Commerce](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[Profilo individuale XDM](../../classes/individual-profile.md)**:<ul><li>[Dettagli demografici](../../field-groups/profile/demographic-details.md)</li></ul></li><li>**[Prodotto](../../classes/product.md)**:<ul><li>[Catalogo prodotti](../../field-groups/product/product-catalog.md)</li><li>[Categoria di prodotto](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Acquisisci dati sulla fedeltà (partner) per aumentare le informazioni rilevanti sui prodotti tra canali web, e-mail e di marketing digitale. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Dettagli web](../../field-groups/event/web-details.md)</li></ul></li><li>**[Profilo individuale XDM](../../classes/individual-profile.md)**:<ul><li>[Dettagli demografici](../../field-groups/profile/demographic-details.md)</li><li>[Dettagli fedeltà](../../field-groups/profile/loyalty-details.md)</li></ul></li><li>**[Prodotto](../../classes/product.md)**:<ul><li>[Catalogo prodotti](../../field-groups/product/product-catalog.md)</li><li>[Categoria di prodotto](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Indirizza gli utenti che abbandonano il carrello tramite e-mail automatizzate e personalizzate. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Dettagli Commerce](../../field-groups/event/commerce-details.md)</li><li>[Dettagli web](../../field-groups/event/web-details.md)</li></ul></li><li>**[Prodotto](../../classes/product.md)**:<ul><li>[Catalogo prodotti](../../field-groups/product/product-catalog.md)</li><li>[Categoria di prodotto](../../field-groups/product/product-category.md)</li></ul></li></ul> |

{style="table-layout:auto"}

*\*Mentre una classe di prodotto standard è pianificata per una versione futura, gli schemi di prodotto devono essere generati utilizzando una classe personalizzata. È quindi necessario creare manualmente la struttura della classe dello schema, nonché quella di eventuali gruppi di campi aggiunti. Consulta la sezione su [creazione di una classe personalizzata](../../ui/resources/classes.md#create) per ulteriori informazioni, consulta la guida dell’interfaccia utente XDM.*
