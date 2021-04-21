---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati;ui;area di lavoro;identità;campo;
solution: Experience Platform
title: Definire i campi di identità nell’interfaccia utente
description: Scopri come definire un campo di identità nell’interfaccia utente di Experience Platform.
topic-legacy: user guide
exl-id: 11a53345-4c3f-4537-b3eb-ee7a5952df2a
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# Definire i campi di identità nell’interfaccia utente

In Experience Data Model (XDM), un campo identità rappresenta un campo che può essere utilizzato per identificare una persona singola correlata a un record o a un evento della serie temporale. Questo documento illustra come definire un campo di identità nell’interfaccia utente di Adobe Experience Platform.

## Prerequisiti

I campi di identità sono un componente fondamentale per la creazione dei grafici di identità del cliente in Platform, che in ultima analisi influisce sul modo in cui Profilo cliente in tempo reale unisce diversi frammenti di dati per ottenere una visione completa del cliente. Prima di definire i campi di identità negli schemi, consulta la seguente documentazione per informazioni sui servizi chiave e sui concetti relativi ai campi di identità:

* [Servizio](../../../identity-service/home.md) Adobe Experience Platform Identity: Collega le identità tra dispositivi e sistemi, collegando i set di dati in base ai campi di identità definiti dagli schemi XDM a cui sono conformi.
   * [Namespace](../../../identity-service/namespaces.md) di identità: Gli spazi dei nomi delle identità definiscono i diversi tipi di informazioni di identità che possono riferirsi a una singola persona e sono un componente obbligatorio per ciascun campo di identità.
* [Profilo](../../../profile/home.md) cliente in tempo reale: Sfrutta i grafici di identità dei clienti per fornire un profilo di consumatore unificato basato su dati aggregati provenienti da più sorgenti, aggiornati in tempo quasi reale.

## Definire un campo di identità

Quando [definisci un nuovo campo](./overview.md#define) nell&#39;interfaccia utente, puoi impostarlo come campo di identità selezionando la casella di controllo **[!UICONTROL Identity]** nella barra a destra.

![](../../images/ui/fields/special/identity.png)

Dopo aver selezionato la casella di controllo vengono visualizzati altri controlli. Se desideri che questo campo sia l’identità principale dello schema, seleziona la casella di controllo **[!UICONTROL Primary identity]** .

>[!NOTE]
>
>Un singolo schema può avere molti campi di identità definiti, ma può avere una sola identità primaria. Tutti i campi di identità (primari o di altro tipo) contribuiscono al grafico dell’identità per un singolo cliente, ma il profilo cliente in tempo reale utilizza solo l’identità principale come origine della verità durante l’unione dei frammenti di dati. Se desideri abilitare uno schema da utilizzare in Profilo, è necessario che lo schema disponga di un&#39;identità primaria definita.

In **[!UICONTROL Identity namespace]**, utilizza il menu a discesa per selezionare lo spazio dei nomi appropriato per il campo identity. Sono elencati gli spazi dei nomi standard forniti da Adobe, insieme a eventuali spazi dei nomi personalizzati definiti dall’organizzazione.

Al termine, seleziona **[!UICONTROL Apply]** per applicare la modifica allo schema.

![](../../images/ui/fields/special/identity-config.png)

L’area di lavoro viene aggiornata per riflettere le modifiche, con il campo selezionato che acquisisce un simbolo di impronta digitale (![](../../images/ui/fields/special/identity-symbol.png)) per designarlo come identità. Nella barra a sinistra, il campo identity è ora elencato sotto il nome della classe o del mixin che fornisce il campo allo schema.

Poiché tutti i campi di identità sono obbligatori per impostazione predefinita, il campo è ora elencato in **[!UICONTROL Required fields]** nella barra a sinistra. Se il campo Identity è nidificato all’interno della struttura dello schema, verranno elencati anche tutti i campi principali come richiesto.

![](../../images/ui/fields/special/identity-applied.png)

Se hai definito un&#39;identità primaria per lo schema, ora puoi procedere all&#39;abilitazione di [lo schema da utilizzare nel Profilo del cliente in tempo reale](../resources/schemas.md#profile).

## Passaggi successivi

Questa guida illustra come definire un campo di identità nell’interfaccia utente di . Poiché i dati vengono acquisiti utilizzando questo schema, i grafici delle identità del cliente vengono aggiornati per riflettere i campi di identità dello schema. Per informazioni su come esplorare il grafico privato dell’organizzazione nell’interfaccia utente, consulta la guida sul [visualizzatore grafico delle identità](../../../identity-service/ui/identity-graph-viewer.md) .

Per informazioni su come definire altri tipi di campi XDM nell’ [!DNL Schema Editor], consulta la panoramica relativa alla [definizione dei campi nell’interfaccia utente](./overview.md#special) .
