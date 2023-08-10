---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;XDM system;experience data model;data model;ui;workspace;array;field;
solution: Experience Platform
title: Definire i campi array nell’interfaccia utente
description: Scopri come definire un campo array nell’interfaccia utente di Experienci Platform.
exl-id: 9ac55554-c29b-40b2-9987-c8c17cc2c00c
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 1%

---

# Definire i campi array nell’interfaccia utente

Quando definisci un campo Experience Data Model (XDM) nell’interfaccia utente di Adobe Experience Platform, puoi designare tale campo come array.

Il contenuto dell’array dipende dal [!UICONTROL Tipo] selezionato per quel campo. Ad esempio, se un campo [!UICONTROL Tipo] è impostato su &quot;[!UICONTROL Stringa]&quot;, impostando tale campo come array, il campo verrà designato come array di stringhe. Se il campo è [!UICONTROL Tipo] è impostato su un tipo di dati a più campi come &quot;[!UICONTROL Indirizzo postale]&quot;, diventerebbe un array di oggetti dell’indirizzo postale conformi al tipo di dati.

Dopo aver [definito un nuovo campo nell’interfaccia utente di](./overview.md#define), è possibile impostarlo come campo array selezionando il **[!UICONTROL Array]** nella barra a destra.

![](../../images/ui/fields/special/array.png)

Una volta selezionata la casella di controllo, nella barra a destra vengono visualizzati ulteriori controlli che consentono di vincolare ulteriormente l’array. Se non si desidera applicare un vincolo specifico, lasciare vuoto il campo.

I controlli di configurazione aggiuntivi per gli array sono i seguenti:

| Field, proprietà | Descrizione |
| --- | --- |
| [!UICONTROL Lunghezza minima] | Il numero minimo di elementi che l’array deve contenere per consentire l’acquisizione corretta. |
| [!UICONTROL Lunghezza massima] | Il numero massimo di elementi che l’array deve contenere per consentire l’acquisizione corretta. |
| [!UICONTROL Solo elementi univoci] | Se impostato su &quot;[!UICONTROL Vero]&quot;, affinché l’acquisizione abbia esito positivo, ogni elemento nell’array deve essere univoco. |

{style="table-layout:auto"}

Al termine della configurazione del campo, seleziona **[!UICONTROL Applica]** per applicare la modifica allo schema.

![](../../images/ui/fields/special/array-config.png)

L’area di lavoro viene aggiornata per riflettere le modifiche apportate al campo. Si noti che il tipo di dati visualizzato accanto al nome del campo nell&#39;area di lavoro viene aggiunto con una coppia di parentesi quadre (`[]`), che indica che il campo rappresenta un array di tale tipo di dati.

![](../../images/ui/fields/special/array-applied.png)

## Passaggi successivi

Questa guida illustra come definire un campo array nell’interfaccia utente. Consulta la panoramica su [definizione dei campi nell’interfaccia utente](./overview.md#special) per scoprire come definire altri tipi di campi XDM in [!DNL Schema Editor].
