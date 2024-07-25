---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;XDM system;experience data model;data model;ui;workspace;identity;field;
solution: Experience Platform
title: Definire i campi di identità nell’interfaccia utente
description: Scopri come definire un campo di identità nell’interfaccia utente di Experience Platform.
exl-id: 11a53345-4c3f-4537-b3eb-ee7a5952df2a
source-git-commit: d1b571fe72208cf2f2ae339273f05cc38dda9845
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 6%

---

# Definire i campi di identità nell’interfaccia utente

In Experience Data Model (XDM), un campo di identità rappresenta un campo che può essere utilizzato per identificare una singola persona correlata a un record o a un evento di serie temporale. Questo documento illustra come definire un campo di identità nell’interfaccia utente di Adobe Experience Platform.

## Prerequisiti

I campi di identità sono un componente fondamentale della costruzione dei grafici di identità del cliente in Platform, che influisce in ultima analisi sul modo in cui Real-Time Customer Profile unisce frammenti di dati diversi per ottenere una visualizzazione completa del cliente. Prima di definire i campi di identità negli schemi, consulta la seguente documentazione per scoprire i servizi e i concetti chiave relativi ai campi di identità:

* [Servizio Adobe Experience Platform Identity](../../../identity-service/home.md): collega le identità tra dispositivi e sistemi, collegando i set di dati in base ai campi di identità definiti dagli schemi XDM a cui sono conformi.
   * [Spazi dei nomi di identità](../../../identity-service/features/namespaces.md): gli spazi dei nomi di identità definiscono i diversi tipi di informazioni di identità che possono riferirsi a una singola persona e sono un componente obbligatorio per ogni campo di identità.
* [Profilo cliente in tempo reale](../../../profile/home.md): sfrutta i grafici di identità del cliente per fornire un profilo consumatore unificato basato su dati aggregati provenienti da più origini, aggiornati in tempo quasi reale.

## Definire un campo di identità {#define-a-identity-field}

>[!CONTEXTUALHELP]
>id="platform_schemas_identityField_primaryIdentityRestriction"
>title="Restrizioni all’identità primaria"
>abstract="Questo schema utilizza un gruppo di campi destinato a essere utilizzato in una connessione di origine specifica. La connessione richiede che identityMap sia utilizzata come identità primaria e la imposta automaticamente."

Quando [definisci un nuovo campo](./overview.md#define) nell&#39;interfaccia utente, puoi impostarlo come campo di identità selezionando la casella di controllo **[!UICONTROL Identità]** nella barra a destra.

![](../../images/ui/fields/special/identity.png)

Dopo aver selezionato la casella di controllo vengono visualizzati controlli aggiuntivi. Se si desidera che questo campo sia l&#39;identità primaria dello schema, selezionare la casella di controllo **[!UICONTROL Identità primaria]**.

>[!NOTE]
>
>Un singolo schema può avere molti campi di identità definiti, ma può avere una sola identità primaria. Tutti i campi di identità (principale o di altro tipo) contribuiscono al grafico delle identità di un singolo cliente, ma il profilo cliente in tempo reale utilizza solo l’identità primaria come origine di verità quando si uniscono i frammenti di dati. Se desideri abilitare uno schema da utilizzare nel profilo, lo schema deve avere un’identità primaria definita.

In **[!UICONTROL Spazio dei nomi identità]**, utilizza il menu a discesa per selezionare lo spazio dei nomi appropriato per il campo di identità. Sono elencati gli spazi dei nomi standard forniti da Adobe, insieme a tutti gli spazi dei nomi personalizzati definiti dalla tua organizzazione.

Al termine, selezionare **[!UICONTROL Applica]** per applicare la modifica allo schema.

![](../../images/ui/fields/special/identity-config.png)

L&#39;area di lavoro si aggiorna per riflettere le modifiche, con il campo selezionato che ottiene un simbolo di impronta digitale (![](/help/images/icons/identity-service.png)) per designarla come identità. Nella barra a sinistra, il campo di identità è ora elencato sotto il nome della classe o del gruppo di campi dello schema che fornisce il campo allo schema.

Se il campo è stato impostato anche come identità primaria, verrà elencato anche in **[!UICONTROL Campi obbligatori]** nella barra a sinistra. Se il campo di identità è nidificato all’interno della struttura dello schema, verranno elencati come obbligatori anche tutti i campi principali.

![](../../images/ui/fields/special/identity-applied.png)

Se hai definito un&#39;identità primaria per lo schema, ora puoi procedere con [abilitare lo schema per l&#39;utilizzo nel Profilo cliente in tempo reale](../resources/schemas.md#profile).

## Passaggi successivi

Questa guida illustra come definire un campo di identità nell’interfaccia utente. Man mano che i dati vengono acquisiti utilizzando questo schema, i grafici di identità del cliente si aggiorneranno per riflettere i campi di identità dello schema. Per informazioni su come esplorare il grafico privato della tua organizzazione nell&#39;interfaccia utente, consulta la guida del [visualizzatore del grafico delle identità](../../../identity-service/features/identity-graph-viewer.md).

Per informazioni su come definire altri tipi di campi XDM in [!DNL Schema Editor], consulta la panoramica su [definizione dei campi nell&#39;interfaccia utente](./overview.md#special).
