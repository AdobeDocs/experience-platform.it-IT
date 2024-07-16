---
keywords: Experience Platform;home;argomenti popolari;profilo prodotto;gestire le autorizzazioni
solution: Experience Platform
title: Gestire Le Autorizzazioni Per Un Profilo Di Prodotto
description: Il controllo degli accessi in Adobe Experience Platform consente di gestire ruoli e autorizzazioni per varie funzionalità di Platform utilizzando Adobe Admin Console. Questo documento funge da guida su come gestire le autorizzazioni per un profilo di prodotto per Platform.
exl-id: ca403bef-6d62-4ca9-bba6-d1280ac63171
source-git-commit: 1812af74e82f3071963177356b3cd4b23ea567f5
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---

# Gestire le autorizzazioni per un profilo di prodotto

Immediatamente dopo la [creazione di un nuovo profilo di prodotto](#create-a-new-product-profile), viene richiesto di configurare le autorizzazioni del profilo. Se stai modificando le autorizzazioni per un profilo esistente, seleziona il profilo dalla scheda **[!UICONTROL Profili di prodotto]** per aprire la pagina dei dettagli del profilo, quindi seleziona **[!UICONTROL Autorizzazioni]**.

![autorizzazioni](../images/permissions.png)

Le autorizzazioni sono suddivise in categorie ed elencate in questa pagina. Nell&#39;elenco vengono visualizzati il nome della categoria, il numero di autorizzazioni in esso contenute e il numero di autorizzazioni attive e la relativa descrizione. Per informazioni dettagliate sulle autorizzazioni disponibili per ogni ruolo, fare riferimento alla tabella in [Autorizzazioni risorsa](/help/access-control/home.md#permissions).

Selezionare una categoria nell&#39;elenco per aprire la pagina **[!UICONTROL Modifica autorizzazioni]**.

![modifica-autorizzazioni](../images/edit-permissions.png)

La pagina **[!UICONTROL Modifica autorizzazioni]** fornisce un&#39;area di lavoro per aggiungere e rimuovere le autorizzazioni dal profilo di prodotto selezionato. Nella parte sinistra della schermata viene visualizzato un elenco di categorie di autorizzazioni. La selezione di una categoria determina la modifica delle autorizzazioni visualizzate in **[!UICONTROL Elementi autorizzazioni disponibili]**.

Ad esempio, per aggiornare le autorizzazioni per Modellazione dati, selezionare **[!UICONTROL Modellazione dati]**.

![gestione profilo](../images/profile-management.png)

Per aggiungere un&#39;autorizzazione, selezionare l&#39;icona più **(+)** accanto al nome dell&#39;autorizzazione. In alternativa, è possibile selezionare **[!UICONTROL Aggiungi tutto]** per aggiungere al profilo tutte le autorizzazioni della categoria corrente. Le autorizzazioni aggiunte vengono visualizzate in **[!UICONTROL Elementi di autorizzazione inclusi]**.

![add-permission](../images/add-permission.png)

>[!NOTE]
>
>Nell&#39;elenco **[!UICONTROL Elementi di autorizzazione inclusi]** vengono visualizzate solo le autorizzazioni aggiunte dalla categoria attualmente selezionata.

Per rimuovere un&#39;autorizzazione, selezionare l&#39;icona **X** accanto al nome dell&#39;autorizzazione oppure selezionare **[!UICONTROL Rimuovi tutto]** per rimuovere tutte le autorizzazioni nella categoria corrente. Le autorizzazioni rimosse vengono nuovamente visualizzate in **[!UICONTROL Elementi di autorizzazione disponibili]**.

Continua a esaminare le categorie disponibili e ad aggiungere eventuali autorizzazioni desiderate. Al termine, selezionare **[!UICONTROL Salva]**.

![rimozione-autorizzazione](../images/remove-permission.png)

Viene visualizzata di nuovo la scheda **[!UICONTROL Autorizzazioni]** per il profilo di prodotto e viene mostrato che le autorizzazioni selezionate sono ora attive.

![autorizzazioni-aggiornate](../images/permissions-updated.png)

## Passaggi successivi

Una volta stabilite le autorizzazioni, puoi passare al passaggio successivo per [gestire i dettagli e i servizi per un profilo di prodotto](details-and-services.md)
