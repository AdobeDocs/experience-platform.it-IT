---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;XDM system;experience data model;data model;ui;workspace;array;field;
solution: Experience Platform
title: Definire i campi array nell’interfaccia utente
description: Scopri come definire un campo array nell’interfaccia utente di Experience Platform.
exl-id: 9ac55554-c29b-40b2-9987-c8c17cc2c00c
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# Definire i campi array nell’interfaccia utente

Quando definisci un campo Experience Data Model (XDM) nell’interfaccia utente di Adobe Experience Platform, puoi designare tale campo come array.

Il contenuto dell&#39;array dipende dal [!UICONTROL Tipo] selezionato per quel campo. Ad esempio, se il tipo [!UICONTROL Type] di un campo è impostato su &quot;[!UICONTROL String]&quot;, impostando tale campo come matrice il campo verrà designato come matrice di stringhe. Se il tipo di dati [!UICONTROL Type] del campo è impostato su un tipo di dati multicampo, ad esempio &quot;[!UICONTROL Postal address]&quot;, diventerà un array di oggetti di indirizzo postale conformi al tipo di dati.

Dopo aver definito [un nuovo campo nell&#39;interfaccia utente](./overview.md#define), puoi impostarlo come campo array selezionando la casella di controllo **[!UICONTROL Array]** nella barra a destra.

![](../../images/ui/fields/special/array.png)

Una volta selezionata la casella di controllo, nella barra a destra vengono visualizzati ulteriori controlli che consentono di vincolare ulteriormente l’array. Se non si desidera applicare un vincolo specifico, lasciare vuoto il campo.

I controlli di configurazione aggiuntivi per gli array sono i seguenti:

| Field, proprietà | Descrizione |
| --- | --- |
| [!UICONTROL Lunghezza minima] | Il numero minimo di elementi che l’array deve contenere per consentire l’acquisizione corretta. |
| [!UICONTROL Lunghezza massima] | Il numero massimo di elementi che l’array deve contenere per consentire l’acquisizione corretta. |
| [!UICONTROL Solo elementi univoci] | Se è impostato su &quot;[!UICONTROL True]&quot;, ogni elemento nell&#39;array deve essere univoco affinché l&#39;acquisizione abbia esito positivo. |

{style="table-layout:auto"}

Al termine della configurazione del campo, selezionare **[!UICONTROL Applica]** per applicare la modifica allo schema.

![](../../images/ui/fields/special/array-config.png)

L’area di lavoro viene aggiornata per riflettere le modifiche apportate al campo. Si noti che il tipo di dati visualizzato accanto al nome del campo nell&#39;area di lavoro è seguito da una coppia di parentesi quadre (`[]`), che indica che il campo rappresenta una matrice di tale tipo di dati.

![](../../images/ui/fields/special/array-applied.png)

## Passaggi successivi

Questa guida illustra come definire un campo array nell’interfaccia utente. Per informazioni su come definire altri tipi di campi XDM in [!DNL Schema Editor], consulta la panoramica su [definizione dei campi nell&#39;interfaccia utente](./overview.md#special).
