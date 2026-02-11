---
title: Aggiorna variabile
description: Modifica il contenuto di un elemento dati variabile.
exl-id: 6c558d1e-85b4-45f9-ba4d-5fed1ec6e308
source-git-commit: 50881ef9498196f2de5519f050800334019a2586
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# Aggiorna variabile

L&#39;azione **[!UICONTROL Update variable]** consente di apportare modifiche parziali o incrementali a un elemento dati [variabile](../data-element-types.md#variable). È possibile utilizzare questa azione per creare un oggetto a cui è possibile fare successivamente riferimento in un&#39;azione [[!UICONTROL Send event]](send-event.md). Compilare gli elementi dati e assegnarli alle proprietà all’interno di un oggetto XDM è adatto alla maggior parte dei casi d’uso; questa azione offre maggiore flessibilità per consentire di impostare le proprietà in modo condizionale per diversi elementi dati in base alle condizioni della regola.

Prima di utilizzare questa azione, è necessario aver già creato un elemento dati variabile. Dopo aver selezionato un elemento dati variabile da modificare, viene visualizzato un editor che consente di impostare tutti i campi desiderati per questa azione.

![Schermata dell&#39;azione aggiorna variabile nell&#39;interfaccia di configurazione dell&#39;azione](../assets/update-variable.png)

Lo schema XDM utilizzato nell’editor corrisponde allo schema selezionato all’interno dell’elemento dati variabile. È possibile impostare una o più proprietà dell&#39;oggetto espandendo gli oggetti e selezionando le proprietà desiderate. Ad esempio, nella schermata seguente, la proprietà `producedBy` è impostata sull&#39;elemento dati `%Produced by data element%`.

![Schermata dell&#39;interfaccia di configurazione dell&#39;azione che mostra una proprietà aggiornata](../assets/update-variable-set-property.png)

Se selezioni un elemento dati variabile che utilizza un oggetto dati invece di un oggetto XDM, i campi disponibili dipendono dai prodotti selezionati durante la configurazione dell’elemento dati. Ad esempio, se crei un oggetto dati che include Adobe Analytics, fields, se selezioni l’elemento dati variabile in questa interfaccia utente verranno visualizzati dei campi che puoi compilare in modo specifico per Adobe Analytics.

![Schermata dell&#39;interfaccia di configurazione dell&#39;azione che mostra un elemento dati variabile basato su un oggetto dati](../assets/variable-data-element-data.png)
