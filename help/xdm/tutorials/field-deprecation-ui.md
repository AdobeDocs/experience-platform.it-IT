---
title: Deprecare un campo XDM nell’interfaccia utente
description: Scopri come rendere obsoleti i campi Experience Data Model (XDM) utilizzando l’Editor di schema in Experienci Platform.
exl-id: f4c5f58a-5190-47d7-8bfc-b33ed238bf25
source-git-commit: 4fa98df9dcc296ba7cb141cb22df116524a0eb0c
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 0%

---

# Deprecare un campo XDM nell’interfaccia utente

Experience Data Model (XDM) offre la flessibilità di gestire il modello dati in base alle esigenze aziendali, rendendo obsoleti i campi dello schema dopo l’acquisizione dei dati. I campi indesiderati possono essere dichiarati obsoleti per rimuoverli dalla vista dell’interfaccia utente e nasconderli anche dalle interfacce a valle. Una casella di controllo nell’Editor schema consente di visualizzare i campi obsoleti e, se necessario, di annullarli.

Poiché i campi obsoleti sono nascosti dall’interfaccia utente per impostazione predefinita, questa funzione semplifica lo schema nell’Editor di schema e impedisce l’aggiunta di campi indesiderati alle dipendenze a valle, ad esempio il Generatore di segmenti, il progettista di percorsi e così via. Il campo obsoleto è compatibile anche con le versioni precedenti. Altri sistemi che utilizzano campi obsoleti, come tipi di pubblico e query, continueranno a valutarli come previsto. Se un campo obsoleto viene utilizzato in un pubblico esistente, viene trattato normalmente, il che significa che il campo viene visualizzato come previsto nell’area di lavoro del Generatore di segmenti o viene valutato in base a qualsiasi dato disponibile nei campi obsoleti. Si tratta di una modifica non definitiva che non influisce negativamente sui flussi di dati esistenti.

>[!NOTE]
>
>Prima che i dati vengano acquisiti in uno schema, puoi rimuovere i gruppi di campi non necessari. Consulta la documentazione su [come rimuovere un gruppo di campi da uno schema](../ui/resources/schemas.md#remove-fields) per ulteriori informazioni.

Una volta acquisiti i dati nello schema, non puoi più rimuovere i campi dallo schema senza apportare modifiche che causano interruzioni. In questo caso, puoi rendere obsoleto un campo indesiderato all’interno di uno schema o di una risorsa personalizzata utilizzando [Editor schema](./create-schema-ui.md) o [API del registro dello schema](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

Questo documento illustra come rendere obsoleti i campi per diverse risorse XDM utilizzando l’Editor di schema nell’interfaccia utente di Experienci Platform. Per i passaggi relativi alla rimozione di un campo XDM da un’API, consulta l’esercitazione su [deprecazione di un campo XDM tramite l’API Schema Registry](./field-deprecation-api.md).

## Deprecare un campo {#deprecate}

Per rendere obsoleto un campo personalizzato, passa all’Editor di schema per lo schema che desideri modificare. Selezionare il campo che si desidera rendere obsoleto dalla [!UICONTROL Struttura] sezione dell’area di lavoro, seguita da **[!UICONTROL Obsoleto]** dal [!UICONTROL Proprietà campo].

![Editor di schema con un campo selezionato ed evidenziato come obsoleto.](../images/tutorials/field-deprecation/deprecate-single-field.png)

Viene visualizzata una finestra di dialogo per confermare le scelte e avvisarti che il campo verrà rimosso dalla vista dell’interfaccia utente dello schema di unione e nascosto dalle interfacce a valle. Per completare l’azione, seleziona **[!UICONTROL Conferma]**.

![La finestra di dialogo Campo obsoleto con l’opzione Conferma evidenziata.](../images/tutorials/field-deprecation/deprecate-field-dialog.png)

Il campo viene ora rimosso dalla vista dell’interfaccia utente.

>[!NOTE]
>
>Una volta dichiarati obsoleti, le interfacce utente a valle come le dashboard di segmentazione, Customer Journey Analytics e Adobe Journey Optimizer non visualizzano più i campi obsoleti come parte del flusso di lavoro. Tuttavia, le interfacce utente a valle hanno la possibilità di mostrare i campi obsoleti se necessario e continuare a trattare il campo obsoleto come normale. Per ulteriori informazioni, consulta la relativa documentazione. Le query e i tipi di pubblico che utilizzano il campo obsoleto continueranno a essere eseguiti come previsto.

## Mostra campi obsoleti {#show-deprecated}

Per visualizzare i campi precedentemente dichiarati obsoleti, accedi allo schema corrispondente nell’Editor di schema. Seleziona la **[!UICONTROL Mostra campi obsoleti]** casella di controllo in [!UICONTROL Composizione] sezione dell’area di lavoro.

Il campo obsoleto viene ora visualizzato nella vista dell’interfaccia utente. Seleziona **[!UICONTROL Salva]** per confermare le impostazioni.

![Nell’Editor schema è selezionato un campo, sono evidenziati Mostra campi obsoleti e Salva.](../images/tutorials/field-deprecation/show-deprecated-fields.png)

## Campi non obsoleti {#undeprecate-fields}

Per annullare un campo obsoleto, prima [visualizza il campo obsoleto](#show-deprecated) come descritto in precedenza, quindi seleziona il campo obsoleto dall’ [!UICONTROL Struttura] sezione. Quindi, seleziona **[!UICONTROL Obsoleto]** dal [!UICONTROL Proprietà campo] barra laterale seguita da **[!UICONTROL Salva]**.

![Editor di schema con il campo obsoleto, Undeprecate e Save evidenziato.](../images/tutorials/field-deprecation/undeprecate-single-field.png)

Il [!UICONTROL Campo non obsoleto] viene visualizzata. Per confermare le modifiche, seleziona **[!UICONTROL Conferma]**.

![Il [!UICONTROL Campo non obsoleto] finestra di dialogo con Conferma evidenziata.](../images/tutorials/field-deprecation/undeprecate-field-dialog.png)

Il campo ora viene visualizzato come standard nella vista dell’interfaccia utente e anche nelle interfacce a valle. Anche in questo caso, ora è possibile rendere obsoleto il campo.

## Passaggi successivi

Questo documento illustra come rendere obsoleti i campi XDM utilizzando l’interfaccia utente dell’Editor di schema. Per ulteriori informazioni sulla configurazione dei campi per le risorse personalizzate, consulta la guida su [definizione dei campi XDM nell’API](./custom-fields-api.md). Per ulteriori informazioni sulla gestione dei descrittori, consulta [guida dell’endpoint &quot;descriptors&quot;](../api/descriptors.md).
