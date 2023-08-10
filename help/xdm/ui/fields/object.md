---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;XDM system;experience data model;data model;ui;workspace;object;field;
solution: Experience Platform
title: Definire i campi oggetto nell’interfaccia utente
description: Scopri come definire un campo di tipo oggetto nell’interfaccia utente di Experienci Platform.
exl-id: 5b7b3cf0-7f11-4e15-af87-09127f4423a5
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# Definire i campi oggetto nell’interfaccia utente

Adobe Experience Platform consente di personalizzare completamente la struttura delle classi XDM (Experience Data Model) personalizzate, dei gruppi di campi dello schema e dei tipi di dati. Per organizzare e nidificare i campi correlati nelle risorse XDM personalizzate, puoi definire campi di tipo oggetto che possono contenere ulteriori sottocampi.

Quando [definizione di un nuovo campo](./overview.md#define) nell’interfaccia utente di Adobe Experience Platform, utilizza **[!UICONTROL Tipo]** e seleziona &quot;[!UICONTROL Oggetto]&quot; dall’elenco.

![](../../images/ui/fields/special/object.png)

Seleziona **[!UICONTROL Applica]** per aggiungere l&#39;oggetto allo schema. L’area di lavoro viene aggiornata per mostrare il nuovo campo con il [!UICONTROL Oggetto] tipo di dati applicato, inclusi i controlli per modificare e aggiungere sottocampi all&#39;oggetto.

![](../../images/ui/fields/special/object-applied.png)

Per aggiungere un sottocampo, seleziona la **più (+)** accanto al campo oggetto nell’area di lavoro. Sotto l’oggetto viene visualizzato un nuovo campo, con i controlli per configurare il sottocampo nella barra a destra.

![](../../images/ui/fields/special/object-add-field.png)

Dopo aver configurato il sottocampo e selezionato **[!UICONTROL Applica]**, è possibile continuare ad aggiungere campi all’oggetto utilizzando lo stesso processo. È inoltre possibile aggiungere sottocampi che sono oggetti stessi, consentendo di nidificare i campi nel modo più profondo possibile.

Dopo aver completato la costruzione dell&#39;oggetto, è possibile che si desideri riutilizzarne la struttura in classi e gruppi di campi diversi. In questo caso, è possibile scegliere di convertire l&#39;oggetto in un tipo di dati. Consulta la sezione su [conversione di oggetti in tipi di dati](../resources/data-types.md#convert) per ulteriori informazioni, consulta la guida all’interfaccia utente per i tipi di dati.

## Passaggi successivi

Questa guida illustra come definire un campo oggetto nell’interfaccia utente. Consulta la panoramica su [definizione dei campi nell’interfaccia utente](./overview.md#special) per scoprire come definire altri tipi di campi XDM in [!DNL Schema Editor].
