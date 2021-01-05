---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;experience data model;data model;ui;workspace;enum;field;
solution: Experience Platform
title: Definire un campo enum nell’interfaccia utente
description: Scoprite come definire un campo enum nell’interfaccia utente del Experience Platform .
topic: user guide
translation-type: tm+mt
source-git-commit: 2e20403122e65d28f04114af9b7e8d41874f76e2
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---


# Definire un campo enum nell’interfaccia utente

In Experience Data Model (XDM), un campo enum rappresenta un campo vincolato a un elenco predefinito di valori accettabili.

Quando [definisci un nuovo campo](./overview.md#define) nell&#39;interfaccia utente di Adobe Experience Platform, puoi impostarlo come campo enum selezionando la casella di controllo **[!UICONTROL Enum]** nella barra a destra.

![](../../images/ui/fields/special/enum.png)

Dopo aver selezionato la casella di controllo vengono visualizzati controlli aggiuntivi, che consentono di specificare i vincoli di valore per l’enum. Nella colonna **[!UICONTROL Value]** è necessario specificare il valore esatto in cui si desidera vincolare il campo. Questo valore deve essere conforme alla [!UICONTROL Type] selezionata per il campo enum. Facoltativamente è possibile fornire un **[!UICONTROL Label]** descrittivo anche per il vincolo.

Per aggiungere vincoli aggiuntivi all&#39;enum, selezionare **[!UICONTROL Add row]**.

![](../../images/ui/fields/special/enum-add-row.png)

Continuate ad aggiungere i vincoli desiderati e le etichette facoltative all’enum. Al termine, selezionare **[!UICONTROL Apply]** per applicare le modifiche allo schema.

![](../../images/ui/fields/special/enum-configured.png)

Il quadro si aggiorna per riflettere le modifiche. Quando si esplora questo schema in futuro, è possibile visualizzare e modificare i vincoli per il campo enum all&#39;interno della barra a destra.

![](../../images/ui/fields/special/enum-applied.png)

## Passaggi successivi

Questa guida descrive come definire un campo enum nell’interfaccia utente. Per informazioni su come definire altri tipi di campi XDM nell&#39; [!DNL Schema Editor], vedere la panoramica relativa alla [definizione dei campi nell&#39;interfaccia utente](./overview.md#special).