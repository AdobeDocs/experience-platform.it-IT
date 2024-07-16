---
solution: Experience Platform
title: Modello dati del settore dei servizi finanziari ERD
description: Visualizzare un diagramma di relazione tra entità (ERD) che descrive un modello di dati standardizzato per il settore bancario, dei servizi finanziari e assicurativo (BFSI). Questo modello dati è compatibile con Experience Data Model (XDM) per l’utilizzo in Adobe Experience Platform.
exl-id: 2e8f6b2a-10e7-4394-b45f-c03db0f25400
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---

# [!UICONTROL Servizi finanziari] modello dati di settore ERD

Il seguente schema di relazione tra entità (ERD) rappresenta un modello di dati standardizzato per il settore bancario, dei servizi finanziari e assicurativo (BFSI). L&#39;ERD viene presentato intenzionalmente in modo denormalizzato e tenendo in considerazione il modo in cui i dati vengono memorizzati in Adobe Experience Platform.

>[!NOTE]
>
>Il documento ERD descritto è un consiglio su come modellare i dati per questo caso d’uso del settore. Per utilizzare questo modello dati in Platform, è necessario creare autonomamente gli schemi consigliati e le relative relazioni. Per ulteriori informazioni, consulta le guide sulla gestione di [schemi](../../ui/resources/schemas.md) e [relazioni](../../tutorials/relationship-ui.md) nell&#39;interfaccia utente.

Utilizzare la seguente legenda per interpretare questa ERD:

* Ogni entità mostrata in è basata su una classe sottostante di [Experience Data Model (XDM)](../composition.md#class).
* Per una determinata entità, ogni riga contrassegnata in **bold** rappresenta un gruppo di campi o un tipo di dati, con i campi pertinenti forniti elencati di seguito in formato testo non in grassetto.
* I campi più importanti per una determinata entità sono evidenziati in rosso.
* Tutte le proprietà che possono essere utilizzate per identificare i singoli clienti sono contrassegnate come &quot;identità&quot; e una di queste proprietà è contrassegnata come &quot;identità primaria&quot;.
* Le relazioni tra entità sono contrassegnate come non dipendenti, poiché gli eventi basati su cookie spesso non possono determinare la persona o l’individuo che ha eseguito la transazione.

![](../../images/industries/financial.png)

>[!NOTE]
>
>L&#39;entità Experience Event include un campo &quot;_ID&quot; che rappresenta l&#39;attributo dell&#39;identificatore univoco (`_id`) fornito dalla classe XDM ExperienceEvent. Per ulteriori dettagli su ciò che è previsto per questo valore, consulta il documento di riferimento su [XDM ExperienceEvent](../../classes/experienceevent.md).

## [!UICONTROL Casi di utilizzo dei servizi finanziari]

La tabella seguente illustra le classi e i gruppi di campi di schema consigliati per diversi casi d’uso finanziari comuni.

| Caso d’uso | Classi e gruppi di campi consigliati |
| --- | --- |
| Promuovi la personalizzazione su larga scala per i segmenti preferiti tramite informazioni di reporting omnicanale e percorsi automatizzati per aumentare l’iscrizione a un programma di premi preferito. | <ul><li>**[[!UICONTROL Prodotto]](../../classes/product.md)**:<ul><li>[[!UICONTROL Categoria prodotto]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Azioni scheda]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL Dettagli richiesta preventivo]](../../field-groups/event/quote-request-details.md)</li><li>[[!UICONTROL Dettagli versamento]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL Dettagli canale]](../../field-groups/event/channel-details.md)</li><li>[[!UICONTROL Trasferimenti saldo]](../../field-groups/event/balance-transfers.md)</li></ul></li><li>**[[!UICONTROL Profilo individuale XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Dettagli demografici]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Dati personali]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL Dettagli fedeltà]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Ottimizza la personalizzazione cross-channel tra canali online e offline. | <ul><li>**[[!UICONTROL Prodotto]](../../classes/product.md)**:<ul><li>[[!UICONTROL Categoria prodotto]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Dettagli canale]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL Profilo individuale XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Dettagli demografici]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Dati personali]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL Dettagli fedeltà]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Crea nuove opportunità di profitto utilizzando le informazioni acquisite dall’analisi del comportamento cross-channel, identificando i modelli di utilizzo dei prodotti che potrebbero portare a nuove offerte di prodotti. | <ul><li>**[[!UICONTROL Criterio]](../../classes/policy.md)**</li><li>**[[!UICONTROL Prodotto]](../../classes/product.md)**:<ul><li>[[!UICONTROL Categoria prodotto]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Azioni scheda]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL Ricerca nel sito di supporto]](../../field-groups/event/support-site-search.md)</li><li>[[!UICONTROL Dettagli versamento]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL Dettagli canale]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL Profilo individuale XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Dettagli demografici]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Dati personali]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL Dettagli fedeltà]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
