---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati;ui;workspace;array;campo;
solution: Experience Platform
title: Definire i campi Array nell’interfaccia utente
description: Scopri come definire un campo array nell’interfaccia utente di Experience Platform.
topic-legacy: user guide
exl-id: 9ac55554-c29b-40b2-9987-c8c17cc2c00c
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 1%

---

# Definire i campi array nell’interfaccia utente

Quando definisci un campo Experience Data Model (XDM) nell’interfaccia utente di Adobe Experience Platform, puoi designare tale campo come array.

Il contenuto della matrice dipende dal [!UICONTROL Tipo] selezionato per quel campo. Ad esempio, se l&#39;impostazione di un campo [!UICONTROL Tipo] è impostata su &quot;[!UICONTROL Stringa]&quot;, l&#39;impostazione di tale campo come array indicherà il campo come una matrice di stringhe. Se il campo [!UICONTROL Tipo] è impostato su un tipo di dati a più campi come &quot;[!UICONTROL Indirizzo postale]&quot;, diventerà una matrice di oggetti indirizzo postale conforme al tipo di dati.

Dopo aver [definito un nuovo campo nell&#39;interfaccia utente](./overview.md#define), puoi impostarlo come campo matrice selezionando la casella di controllo **[!UICONTROL Array]** nella barra a destra.

![](../../images/ui/fields/special/array.png)

Una volta selezionata la casella di controllo, nella barra a destra vengono visualizzati controlli aggiuntivi che consentono di vincolare ulteriormente la matrice. Se non si desidera applicare un vincolo particolare, lasciare vuoto il campo.

I controlli di configurazione aggiuntivi per gli array sono i seguenti:

| Proprietà campo | Descrizione |
| --- | --- |
| [!UICONTROL Lunghezza minima] | Il numero minimo di elementi che la matrice deve contenere affinché l&#39;acquisizione abbia esito positivo. |
| [!UICONTROL Lunghezza massima] | Il numero massimo di elementi che la matrice deve contenere affinché l&#39;acquisizione abbia esito positivo. |
| [!UICONTROL Solo elementi univoci] | Se è impostato su &quot;[!UICONTROL True]&quot;, ogni elemento della matrice deve essere univoco per garantire il successo dell&#39;acquisizione. |

{style=&quot;table-layout:auto&quot;}

Al termine della configurazione del campo, selezionare **[!UICONTROL Applica]** per applicare la modifica allo schema.

![](../../images/ui/fields/special/array-config.png)

L’area di lavoro viene aggiornata per riflettere le modifiche apportate al campo. Al tipo di dati visualizzato accanto al nome del campo nell’area di lavoro viene aggiunta una coppia di parentesi quadre (`[]`) che indica che il campo rappresenta una matrice di tale tipo di dati.

![](../../images/ui/fields/special/array-applied.png)

## Passaggi successivi

Questa guida illustra come definire un campo array nell’interfaccia utente di . Per informazioni su come definire altri tipi di campi XDM nell’ [!DNL Schema Editor], consulta la panoramica relativa alla [definizione dei campi nell’interfaccia utente](./overview.md#special) .
