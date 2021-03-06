---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati;ui;workspace;oggetto;campo;
solution: Experience Platform
title: Definire i campi oggetto nell’interfaccia utente
description: Scopri come definire un campo di tipo oggetto nell’interfaccia utente di Experience Platform.
topic-legacy: user guide
exl-id: 5b7b3cf0-7f11-4e15-af87-09127f4423a5
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# Definire i campi oggetto nell’interfaccia utente

Adobe Experience Platform ti consente di personalizzare completamente la struttura delle classi Experience Data Model (XDM) personalizzate, dei gruppi di campi dello schema e dei tipi di dati. Per organizzare e nidificare i campi correlati nelle risorse XDM personalizzate, è possibile definire campi di tipo oggetto che possono contenere campi secondari aggiuntivi.

Quando [definisci un nuovo campo](./overview.md#define) nell&#39;interfaccia utente di Adobe Experience Platform, utilizza il menu a discesa **[!UICONTROL Type]** e seleziona &quot;[!UICONTROL Object]&quot; dall&#39;elenco.

![](../../images/ui/fields/special/object.png)

Selezionare **[!UICONTROL Apply]** per aggiungere l&#39;oggetto allo schema. L’area di lavoro viene aggiornata per mostrare il nuovo campo con il tipo di dati [!UICONTROL Object] applicato, compresi i controlli per modificare e aggiungere campi secondari all’oggetto.

![](../../images/ui/fields/special/object-applied.png)

Per aggiungere un sottocampo, seleziona l’icona **più (+)** accanto al campo oggetto nell’area di lavoro. Sotto l’oggetto viene visualizzato un nuovo campo con i controlli per configurare il sottocampo nella barra a destra.

![](../../images/ui/fields/special/object-add-field.png)

Dopo aver configurato il sottocampo e aver selezionato **[!UICONTROL Apply]**, è possibile continuare ad aggiungere campi all’oggetto utilizzando lo stesso processo. È inoltre possibile aggiungere campi secondari costituiti da oggetti, per nidificare i campi nel modo desiderato.

![](../../images/ui/fields/special/object-nested.png)

Una volta completata la costruzione dell’oggetto, potrebbe essere necessario riutilizzarne la struttura in classi e gruppi di campi diversi. In questo caso, è possibile scegliere di convertire l’oggetto in un tipo di dati. Per ulteriori informazioni, consulta la sezione sulla [conversione di oggetti in tipi di dati](../resources/data-types.md#convert) nella guida dell’interfaccia utente per i tipi di dati .

## Passaggi successivi

Questa guida illustra come definire un campo oggetto nell’interfaccia utente di . Per informazioni su come definire altri tipi di campi XDM nell’ [!DNL Schema Editor], consulta la panoramica relativa alla [definizione dei campi nell’interfaccia utente](./overview.md#special) .
