---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati;ui;workspace;enum;campo;
solution: Experience Platform
title: Definire i campi Enum nell’interfaccia utente
description: Scopri come definire un campo enum nell’interfaccia utente di Experience Platform.
topic-legacy: user guide
exl-id: 67ec5382-31de-4f8d-9618-e8919bb5a472
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---

# Definire i campi enum nell’interfaccia utente

In Experience Data Model (XDM), un campo enum rappresenta un campo vincolato a un elenco predefinito di valori accettabili.

Quando [definisci un nuovo campo](./overview.md#define) nell&#39;interfaccia utente di Adobe Experience Platform, puoi impostarlo come campo enum selezionando la casella di controllo **[!UICONTROL Enum]** nella barra a destra.

![](../../images/ui/fields/special/enum.png)

Dopo aver selezionato la casella di controllo vengono visualizzati altri controlli che consentono di specificare i vincoli di valore per l’enum. Nella colonna **[!UICONTROL Value]** è necessario specificare il valore esatto in cui si desidera vincolare il campo. Questo valore deve essere conforme al valore [!UICONTROL Type] selezionato per il campo enum. Facoltativamente, puoi anche fornire un **[!UICONTROL Label]** descrittivo per il vincolo.

Per aggiungere vincoli aggiuntivi all’enum, seleziona **[!UICONTROL Add row]**.

![](../../images/ui/fields/special/enum-add-row.png)

Continua ad aggiungere all’enum i vincoli desiderati e le etichette facoltative. Al termine, seleziona **[!UICONTROL Apply]** per applicare le modifiche allo schema.

![](../../images/ui/fields/special/enum-configured.png)

L’area di lavoro viene aggiornata per riflettere le modifiche. Quando esplori questo schema in futuro, puoi visualizzare e modificare i vincoli per il campo enum nella barra a destra.

![](../../images/ui/fields/special/enum-applied.png)

## Passaggi successivi

Questa guida illustra come definire un campo enum nell’interfaccia utente di . Per informazioni su come definire altri tipi di campi XDM nell’ [!DNL Schema Editor], consulta la panoramica relativa alla [definizione dei campi nell’interfaccia utente](./overview.md#special) .
