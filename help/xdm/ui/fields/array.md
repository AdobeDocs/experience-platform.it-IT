---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati;ui;workspace;array;campo;
solution: Experience Platform
title: Definire i campi Array nell’interfaccia utente
description: Scopri come definire un campo array nell’interfaccia utente di Experience Platform.
exl-id: 9ac55554-c29b-40b2-9987-c8c17cc2c00c
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 2%

---

# Definire i campi array nell’interfaccia utente

Quando definisci un campo Experience Data Model (XDM) nell’interfaccia utente di Adobe Experience Platform, puoi designare tale campo come array.

Il contenuto dell’array dipende dal [!UICONTROL Tipo] selezionata per quel campo. Ad esempio, se un campo è [!UICONTROL Tipo] è impostato su &quot;[!UICONTROL Stringa]&quot;, impostando tale campo come array il campo verrà designato come array di stringhe. Se il campo è [!UICONTROL Tipo] è impostato su un tipo di dati con più campi, ad esempio &quot;[!UICONTROL Indirizzo postale]&quot;, diventerebbe un array di oggetti di indirizzo postale conformi al tipo di dati.

Dopo aver [ha definito un nuovo campo nell’interfaccia utente di](./overview.md#define), puoi impostarlo come campo array selezionando la **[!UICONTROL Array]** nella barra a destra.

![](../../images/ui/fields/special/array.png)

Una volta selezionata la casella di controllo, nella barra a destra vengono visualizzati controlli aggiuntivi che consentono di vincolare ulteriormente la matrice. Se non si desidera applicare un vincolo particolare, lasciare vuoto il campo.

I controlli di configurazione aggiuntivi per gli array sono i seguenti:

| Proprietà campo | Descrizione |
| --- | --- |
| [!UICONTROL Lunghezza minima] | Il numero minimo di elementi che la matrice deve contenere affinché l&#39;acquisizione abbia esito positivo. |
| [!UICONTROL Lunghezza massima] | Il numero massimo di elementi che la matrice deve contenere affinché l&#39;acquisizione abbia esito positivo. |
| [!UICONTROL Solo elementi univoci] | Se impostato su &quot;[!UICONTROL True]&quot;, ogni elemento dell’array deve essere univoco per garantire il successo dell’acquisizione. |

{style=&quot;table-layout:auto&quot;}

Al termine della configurazione del campo, seleziona **[!UICONTROL Applica]** per applicare la modifica allo schema.

![](../../images/ui/fields/special/array-config.png)

L’area di lavoro viene aggiornata per riflettere le modifiche apportate al campo. Al tipo di dati visualizzato accanto al nome del campo nell’area di lavoro viene aggiunta una coppia di parentesi quadre (`[]`), che indica che il campo rappresenta una matrice di quel tipo di dati.

![](../../images/ui/fields/special/array-applied.png)

## Passaggi successivi

Questa guida illustra come definire un campo array nell’interfaccia utente di . Vedi la panoramica su [definizione dei campi nell’interfaccia utente](./overview.md#special) per scoprire come definire altri tipi di campi XDM nel [!DNL Schema Editor].
