---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;experience data model;data model;ui;workspace;object;field;
solution: Experience Platform
title: Definire un campo oggetto nell'interfaccia utente
description: Scoprite come definire un campo del tipo di oggetto nell'interfaccia utente del Experience Platform .
topic: user guide
translation-type: tm+mt
source-git-commit: 2e20403122e65d28f04114af9b7e8d41874f76e2
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---


# Definire un campo oggetto nell&#39;interfaccia utente

Adobe Experience Platform consente di personalizzare completamente la struttura delle classi, dei mixin e dei tipi di dati personalizzati Experience Data Model (XDM). Per organizzare e nidificare i campi correlati in risorse XDM personalizzate, è possibile definire campi di tipo oggetto che possono contenere campi secondari aggiuntivi.

Quando [definire un nuovo campo](./overview.md#define) nell&#39;interfaccia utente di Adobe Experience Platform, utilizzare il menu a discesa **[!UICONTROL Type]** e selezionare &quot;[!UICONTROL Object]&quot; dall&#39;elenco.

![](../../images/ui/fields/special/object.png)

Selezionare **[!UICONTROL Apply]** per aggiungere l&#39;oggetto allo schema. Il quadro viene aggiornato per mostrare il nuovo campo con il tipo di dati [!UICONTROL Object] applicato, compresi i controlli per la modifica e l&#39;aggiunta di campi secondari all&#39;oggetto.

![](../../images/ui/fields/special/object-applied.png)

Per aggiungere un sottocampo, selezionare l&#39;icona **più (+)** accanto al campo oggetto nel quadro. Sotto l&#39;oggetto viene visualizzato un nuovo campo, con controlli che consentono di configurare il sottocampo nella barra a destra.

![](../../images/ui/fields/special/object-add-field.png)

Dopo aver configurato il sottocampo e selezionato **[!UICONTROL Apply]**, è possibile continuare ad aggiungere campi all&#39;oggetto utilizzando lo stesso processo. È inoltre possibile aggiungere sottocampi che sono oggetti stessi, per nidificare i campi nel modo desiderato.

![](../../images/ui/fields/special/object-nested.png)

Una volta completata la creazione dell&#39;oggetto, potrebbe essere necessario riutilizzarne la struttura in classi e mixin diversi. In questo caso, è possibile scegliere di convertire l&#39;oggetto in un tipo di dati. Per ulteriori informazioni, vedere la sezione relativa alla [conversione di oggetti in tipi di dati](../resources/data-types.md#convert) nella guida dell&#39;interfaccia utente relativa ai tipi di dati.

## Passaggi successivi

Questa guida descrive come definire un campo oggetto nell’interfaccia utente. Per informazioni su come definire altri tipi di campi XDM nell&#39; [!DNL Schema Editor], vedere la panoramica relativa alla [definizione dei campi nell&#39;interfaccia utente](./overview.md#special).
