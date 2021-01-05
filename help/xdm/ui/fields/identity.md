---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;experience data model;data model;ui;workspace;identity;field;
solution: Experience Platform
title: Definire un campo di identità nell'interfaccia utente
description: Scoprite come definire un campo di identità nell'interfaccia utente del Experience Platform .
topic: user guide
translation-type: tm+mt
source-git-commit: f5f507c2e962e2ff9f81376bfe363a6f438056cd
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---


# Definire un campo di identità nell&#39;interfaccia utente

In Experience Data Model (XDM), un campo di identità rappresenta un campo che può essere utilizzato per identificare una singola persona correlata a un record o a un evento della serie temporale. Questo documento descrive come definire un campo di identità nell’interfaccia utente di Adobe Experience Platform.

## Prerequisiti

I campi di identità sono un componente fondamentale del modo in cui i grafici di identità del cliente vengono creati in Piattaforma, il che influisce sul modo in cui il profilo cliente in tempo reale unisce diversi frammenti di dati per ottenere una visione completa del cliente. Prima di definire i campi di identità negli schemi, consultate la seguente documentazione per informazioni sui servizi chiave e sui concetti correlati ai campi di identità:

* [Servizio](../../../identity-service/home.md) identità Adobe Experience Platform: Collega le identità tra dispositivi e sistemi, collegando i dataset in base ai campi di identità definiti dagli schemi XDM a cui sono conformi.
   * [Spazi dei nomi](../../../identity-service/namespaces.md) di identità: Gli spazi dei nomi delle identità definiscono i diversi tipi di informazioni di identità che possono riferirsi a una singola persona e sono un componente richiesto per ciascun campo di identità.
* [Profilo](../../../profile/home.md) cliente in tempo reale: Utilizza i grafici dell&#39;identità del cliente per fornire un profilo del consumatore unificato basato su dati aggregati provenienti da più origini, aggiornati in tempo quasi reale.

## Definire un campo di identità

Quando [definisci un nuovo campo](./overview.md#define) nell&#39;interfaccia utente, puoi impostarlo come campo di identità selezionando la casella di controllo **[!UICONTROL Identity]** nella barra a destra.

![](../../images/ui/fields/special/identity.png)

Dopo aver selezionato la casella di controllo vengono visualizzati altri controlli. Se si desidera che questo campo sia l&#39;identità principale dello schema, selezionare la casella di controllo **[!UICONTROL Primary identity]**.

>[!NOTE]
>
>Uno schema può avere molti campi di identità definiti, ma può avere una sola identità primaria. Tutti i campi di identità (primari o di altro tipo) contribuiscono al grafico dell&#39;identità per un singolo cliente, ma il profilo cliente in tempo reale utilizza solo l&#39;identità principale come origine di verità quando si uniscono i frammenti di dati. Se si desidera abilitare uno schema per l&#39;utilizzo in Profile, lo schema deve avere un&#39;identità primaria definita.

In **[!UICONTROL Identity namespace]**, utilizzare il menu a discesa per selezionare lo spazio dei nomi appropriato per il campo identità. Vengono elencati gli spazi dei nomi standard forniti  Adobe, insieme a eventuali spazi dei nomi personalizzati definiti dall&#39;organizzazione.

Al termine, selezionare **[!UICONTROL Apply]** per applicare la modifica allo schema.

![](../../images/ui/fields/special/identity-config.png)

Il quadro si aggiorna per riflettere le modifiche, con il campo selezionato che acquisisce un simbolo di impronta digitale (![](../../images/ui/fields/special/identity-symbol.png)) per specificarlo come identità. Nella barra a sinistra, il campo identità ora è elencato sotto il nome della classe o del mixin che fornisce il campo allo schema.

Poiché tutti i campi di identità sono obbligatori per impostazione predefinita, il campo è ora elencato in **[!UICONTROL Required fields]** nella barra a sinistra. Se il campo identità è nidificato all&#39;interno della struttura dello schema, anche tutti i campi principali saranno elencati come obbligatori.

![](../../images/ui/fields/special/identity-applied.png)

Se è stata definita un&#39;identità primaria per lo schema, ora è possibile attivare [lo schema da utilizzare nel profilo cliente in tempo reale](../resources/schemas.md#profile).

## Passaggi successivi

Questa guida descrive come definire un campo di identità nell’interfaccia utente. Durante l&#39;assimilazione dei dati con questo schema, i grafici dell&#39;identità del cliente si aggiorneranno per riflettere i campi dell&#39;identità dello schema. Per informazioni su come esplorare il grafico privato dell&#39;organizzazione nell&#39;interfaccia utente, consulta la guida sul [visualizzatore grafico dell&#39;identità](../../../identity-service/ui/identity-graph-viewer.md).

Per informazioni su come definire altri tipi di campi XDM nell&#39; [!DNL Schema Editor], vedere la panoramica relativa alla [definizione dei campi nell&#39;interfaccia utente](./overview.md#special).