---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati;ui;workspace;oggetto;campo;
solution: Experience Platform
title: Definire i campi oggetto nell’interfaccia utente
description: Scopri come definire un campo di tipo oggetto nell’interfaccia utente di Experience Platform.
topic-legacy: user guide
exl-id: 5b7b3cf0-7f11-4e15-af87-09127f4423a5
source-git-commit: fe3d9a3fc473e7ca13f0e0c2f222bcc1b1a991c4
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Definire i campi oggetto nell’interfaccia utente

Adobe Experience Platform ti consente di personalizzare completamente la struttura delle classi Experience Data Model (XDM) personalizzate, dei gruppi di campi dello schema e dei tipi di dati. Per organizzare e nidificare i campi correlati nelle risorse XDM personalizzate, è possibile definire campi di tipo oggetto che possono contenere campi secondari aggiuntivi.

Quando [definizione di un nuovo campo](./overview.md#define) nell’interfaccia utente di Adobe Experience Platform, utilizza il **[!UICONTROL Tipo]** a discesa e seleziona &quot;[!UICONTROL Oggetto]&quot; dall&#39;elenco.

![](../../images/ui/fields/special/object.png)

Seleziona **[!UICONTROL Applica]** per aggiungere l&#39;oggetto allo schema. L’area di lavoro viene aggiornata per mostrare il nuovo campo con la [!UICONTROL Oggetto] tipo di dati applicato, inclusi i controlli per modificare e aggiungere campi secondari all’oggetto.

![](../../images/ui/fields/special/object-applied.png)

Per aggiungere un sottocampo, seleziona la **più (+)** accanto al campo oggetto nell’area di lavoro. Sotto l’oggetto viene visualizzato un nuovo campo con i controlli per configurare il sottocampo nella barra a destra.

![](../../images/ui/fields/special/object-add-field.png)

Dopo aver configurato il sottocampo e aver selezionato **[!UICONTROL Applica]**, è possibile continuare ad aggiungere campi all’oggetto utilizzando lo stesso processo. È inoltre possibile aggiungere campi secondari costituiti da oggetti, per nidificare i campi nel modo desiderato.

Una volta completata la costruzione dell’oggetto, potrebbe essere necessario riutilizzarne la struttura in classi e gruppi di campi diversi. In questo caso, è possibile scegliere di convertire l’oggetto in un tipo di dati. Vedi la sezione su [conversione di oggetti in tipi di dati](../resources/data-types.md#convert) nella guida dell’interfaccia utente dei tipi di dati per ulteriori informazioni.

## Passaggi successivi

Questa guida illustra come definire un campo oggetto nell’interfaccia utente di . Vedi la panoramica su [definizione dei campi nell’interfaccia utente](./overview.md#special) per scoprire come definire altri tipi di campi XDM nel [!DNL Schema Editor].
