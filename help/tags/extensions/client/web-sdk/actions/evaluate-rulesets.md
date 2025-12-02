---
title: Valuta set di regole
description: Attiva manualmente una valutazione del set di regole.
source-git-commit: 46e5d007b27eaa67c9ee49e35a711424de383d68
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---

# Valuta set di regole

Il tipo di azione **[!UICONTROL Evaluate rulesets]** consente di attivare manualmente le valutazioni del set di regole. I set di regole vengono restituiti da Adobe Journey Optimizer per supportare funzioni come i messaggi nel browser.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Rules]**, quindi seleziona la regola desiderata.
1. In [!UICONTROL Actions], selezionare un&#39;azione esistente o crearne una.
1. Imposta il campo a discesa [!UICONTROL Extension] su **[!UICONTROL Adobe Experience Platform Web SDK]**, quindi imposta [!UICONTROL Action type] su **[!UICONTROL Evaluate rulesets]**.

![Immagine dell&#39;interfaccia utente di Experience Platform che mostra il tipo di azione di risposta Valuta set di regole.](../assets/evaluate-rulesets.png)

## Campi disponibili

Questo tipo di azione supporta le seguenti opzioni:

* **[!UICONTROL Render visual personalization decisions]**: casella di controllo che, se abilitata, esegue il rendering delle decisioni di personalizzazione visiva per gli elementi del set di regole corrispondenti.
* **[!UICONTROL Decision context]**: mappa chiave-valore utilizzata durante la valutazione dei set di regole di Adobe Journey Optimizer per le decisioni sul dispositivo. Puoi fornire il contesto decisionale manualmente o tramite un elemento dati.
