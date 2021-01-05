---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;experience data model;data model;ui;workspace;array;field;
solution: Experience Platform
title: Definire un campo array nell’interfaccia utente
description: Scoprite come definire un campo array nell'interfaccia utente del Experience Platform .
topic: user guide
translation-type: tm+mt
source-git-commit: 2e20403122e65d28f04114af9b7e8d41874f76e2
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 0%

---


# Definire un campo array nell’interfaccia utente

Quando si definisce un campo Experience Data Model (XDM) nell&#39;interfaccia utente di Adobe Experience Platform, è possibile designare tale campo come un array.

Il contenuto dell&#39;array dipende dalla [!UICONTROL Type] selezionata per tale campo. Se ad esempio [!UICONTROL Type] di un campo è impostato su &quot;[!UICONTROL String]&quot;, l&#39;impostazione di tale campo come array indicherà il campo come una matrice di stringhe. Se il campo [!UICONTROL Type] è impostato su un tipo di dati multi-campo come &quot;[!UICONTROL Postal address]&quot;, diventa un array di oggetti postal-address conformi al tipo di dati.

Dopo aver [definito un nuovo campo nell&#39;interfaccia utente](./overview.md#define), è possibile impostarlo come campo matrice selezionando la casella di controllo **[!UICONTROL Array]** nella barra a destra.

![](../../images/ui/fields/special/array.png)

Una volta selezionata la casella di controllo, nella barra a destra vengono visualizzati controlli aggiuntivi che consentono di limitare ulteriormente l&#39;array. Se non si desidera applicare un vincolo particolare, lasciare vuoto il campo.

I controlli di configurazione aggiuntivi per gli array sono i seguenti:

| Proprietà field | Descrizione |
| --- | --- |
| [!UICONTROL Minimum length] | Il numero minimo di elementi che la matrice deve contenere affinché l&#39;assimilazione abbia esito positivo. |
| [!UICONTROL Maximum length] | Il numero massimo di elementi che la matrice deve contenere per garantire il successo dell&#39;assimilazione. |
| [!UICONTROL Unique items only] | Se è impostata su &quot;[!UICONTROL True]&quot;, ogni elemento dell&#39;array deve essere univoco per garantire il successo dell&#39;assimilazione. |

Una volta completata la configurazione del campo, selezionare **[!UICONTROL Apply]** per applicare la modifica allo schema.

![](../../images/ui/fields/special/array-config.png)

Il quadro si aggiorna per riflettere le modifiche apportate al campo. Il tipo di dati visualizzato accanto al nome del campo nell&#39;area di lavoro viene aggiunto con una coppia di parentesi quadre (`[]`), a indicare che il campo rappresenta una matrice di tale tipo di dati.

![](../../images/ui/fields/special/array-applied.png)

## Passaggi successivi

Questa guida descrive come definire un campo array nell’interfaccia utente. Per informazioni su come definire altri tipi di campi XDM nell&#39; [!DNL Schema Editor], vedere la panoramica relativa alla [definizione dei campi nell&#39;interfaccia utente](./overview.md#special).