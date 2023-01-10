---
solution: Experience Platform
title: Settore dei servizi finanziari Modello dei dati ERD
description: Visualizzare un diagramma delle relazioni tra entità (ERD) che descrive un modello di dati standardizzato per il settore bancario, dei servizi finanziari e assicurativo (BFSI). Questo modello dati è compatibile con Experience Data Model (XDM) per l’utilizzo in Adobe Experience Platform.
exl-id: 2e8f6b2a-10e7-4394-b45f-c03db0f25400
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 1%

---

# [!UICONTROL Servizi finanziari] ERD

Il seguente schema delle relazioni tra entità (ERD) rappresenta un modello standardizzato di dati per il settore bancario, dei servizi finanziari e assicurativo (BFSI). L&#39;ERD viene presentato intenzionalmente in modo denormalizzato e tenendo conto del modo in cui i dati vengono memorizzati in Adobe Experience Platform.

>[!NOTE]
>
>L’ERD come descritto è una raccomandazione su come modellare i dati per questo caso d’uso del settore. Per utilizzare questo modello dati in Platform, è necessario creare autonomamente gli schemi consigliati e le relative relazioni. Consulta le guide sulla gestione [schemi](../../ui/resources/schemas.md) e [relazioni](../../tutorials/relationship-ui.md) nell’interfaccia utente di per ulteriori informazioni.

Utilizzare la seguente legenda per interpretare questo ERD:

* Ogni entità indicata in si basa su un sottostante [Classe Experience Data Model (XDM)](../composition.md#class).
* Per una determinata entità, ogni riga contrassegnata in **audace** rappresenta un gruppo di campi o un tipo di dati, con i campi pertinenti che fornisce elencati di seguito in un testo senza bolle.
* I campi più importanti per una determinata entità sono evidenziati in rosso.
* Tutte le proprietà che possono essere utilizzate per identificare i singoli clienti sono contrassegnate come &quot;identità&quot;, con una di queste proprietà contrassegnata come &quot;identità principale&quot;.
* Le relazioni di entità sono contrassegnate come non dipendenti, poiché gli eventi basati su cookie spesso non possono determinare la persona o la persona che ha eseguito la transazione.

![](../../images/industries/financial.png)

>[!NOTE]
>
>L’entità Experience Event include un campo &quot;_ID&quot; che rappresenta l’identificatore univoco (`_id`) fornita dalla classe ExperienceEvent XDM. Vedere il documento di riferimento su [ExperienceEvent XDM](../../classes/experienceevent.md) per ulteriori dettagli su cosa ci si aspetta da questo valore.

## [!UICONTROL Servizi finanziari] casi d&#39;uso

La tabella seguente illustra le classi e i gruppi di campi di schema consigliati per diversi casi d’uso finanziario comuni.

| Caso d’uso | Classi e gruppi di campi consigliati |
| --- | --- |
| Ottimizza la personalizzazione su larga scala per i segmenti preferiti tramite insights di reporting omnicanale e automatizza i percorsi per aumentare l’iscrizione a un programma di premi preferito. | <ul><li>**[[!UICONTROL Prodotto]](../../classes/product.md)**:<ul><li>[[!UICONTROL Categoria di prodotti]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL ExperienceEvent XDM]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Azioni a schede]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL Dettagli richiesta preventivo]](../../field-groups/event/quote-request-details.md)</li><li>[[!UICONTROL Dettagli sui depositi]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL Dettagli canale]](../../field-groups/event/channel-details.md)</li><li>[[!UICONTROL Trasferimenti di saldo]](../../field-groups/event/balance-transfers.md)</li></ul></li><li>**[[!UICONTROL Profilo individuale XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Dettagli demografici]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Dati di contatto personali]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL Dettagli fedeltà]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Ottimizza la personalizzazione cross-channel tra canali online e offline. | <ul><li>**[[!UICONTROL Prodotto]](../../classes/product.md)**:<ul><li>[[!UICONTROL Categoria di prodotti]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL ExperienceEvent XDM]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Dettagli canale]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL Profilo individuale XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Dettagli demografici]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Dati di contatto personali]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL Dettagli fedeltà]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Favorire nuove opportunità di profitto utilizzando le informazioni ottenute dall’analisi dei comportamenti cross-channel, identificando i modelli di utilizzo del prodotto che potrebbero portare a nuove offerte di prodotto. | <ul><li>**[[!UICONTROL Criterio]](../../classes/policy.md)**</li><li>**[[!UICONTROL Prodotto]](../../classes/product.md)**:<ul><li>[[!UICONTROL Categoria di prodotti]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL ExperienceEvent XDM]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Azioni a schede]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL Ricerca nel sito di supporto]](../../field-groups/event/support-site-search.md)</li><li>[[!UICONTROL Dettagli sui depositi]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL Dettagli canale]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL Profilo individuale XDM]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Dettagli demografici]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Dati di contatto personali]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL Dettagli fedeltà]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
