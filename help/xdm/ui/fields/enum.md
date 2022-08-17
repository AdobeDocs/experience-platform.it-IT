---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati;ui;workspace;enum;campo;
solution: Experience Platform
title: Definire i campi Enum nell’interfaccia utente
description: Scopri come definire un campo enum nell’interfaccia utente di Experience Platform.
topic-legacy: user guide
exl-id: 67ec5382-31de-4f8d-9618-e8919bb5a472
source-git-commit: f6fefda974d2ae6fd4b035ef3b5fe633311c9772
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 2%

---

# Definire i campi enum nell’interfaccia utente {#enum}

>[!CONTEXTUALHELP]
>id="platform_xdm_enumsuggestedvalue"
>title="Enum e valori suggeriti"
>abstract="Un enum vincola un campo stringa a consentire l’acquisizione solo dei dati che corrispondono a un set predefinito di valori. In alternativa, puoi definire un set di valori consigliati per il campo che non limita l’acquisizione, ma piuttosto gli attributi tra cui puoi scegliere nella segmentazione. Per ulteriori informazioni, consulta la documentazione dello strumento."

In Experience Data Model (XDM), un campo enum rappresenta un campo vincolato a un elenco predefinito di valori accettabili.

Quando [definizione di un nuovo campo](./overview.md#define) nell’interfaccia utente di Adobe Experience Platform, puoi impostarla come campo enum selezionando la **[!UICONTROL Enum]** nella barra a destra.

![](../../images/ui/fields/special/enum.png)

Dopo aver selezionato la casella di controllo vengono visualizzati altri controlli che consentono di specificare i vincoli di valore per l’enum. Sotto la **[!UICONTROL Valore]** È necessario specificare il valore esatto a cui si desidera vincolare il campo. Questo valore deve essere conforme al [!UICONTROL Tipo] è stato selezionato per il campo enum. Facoltativamente, puoi fornire un **[!UICONTROL Etichetta]** anche per il vincolo.

Per aggiungere vincoli aggiuntivi all’enum, seleziona **[!UICONTROL Aggiungi riga]**.

![](../../images/ui/fields/special/enum-add-row.png)

Continua ad aggiungere all’enum i vincoli desiderati e le etichette facoltative. Al termine, seleziona **[!UICONTROL Applica]** per applicare le modifiche allo schema.

![](../../images/ui/fields/special/enum-configured.png)

L’area di lavoro viene aggiornata per riflettere le modifiche. Quando esplori questo schema in futuro, puoi visualizzare e modificare i vincoli per il campo enum nella barra a destra.

![](../../images/ui/fields/special/enum-applied.png)

## Passaggi successivi

Questa guida illustra come definire un campo enum nell’interfaccia utente di . Vedi la panoramica su [definizione dei campi nell’interfaccia utente](./overview.md#special) per scoprire come definire altri tipi di campi XDM nel [!DNL Schema Editor].
