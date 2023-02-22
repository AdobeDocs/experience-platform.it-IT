---
title: Un campo XDM nell’interfaccia utente di
description: Scopri come rendere obsoleti i campi Experience Data Model (XDM) utilizzando l’Editor di schema in Experience Platform.
source-git-commit: f791d32ae38dffe82723800aa9fb5b44bb4f0109
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 0%

---

# Un campo XDM nell’interfaccia utente di

Experience Data Model (XDM) offre la flessibilità necessaria per gestire il modello dati in base alle esigenze aziendali, in quanto i campi dello schema verranno deprecati dopo l’acquisizione dei dati. I campi indesiderati possono essere dichiarati obsoleti per rimuoverli dalla visualizzazione dell’interfaccia utente e anche per nasconderli dalle interfacce utente downstream. Una casella di controllo nell’Editor di schema consente di visualizzare campi obsoleti e, se necessario, di deprecarli.

Poiché i campi obsoleti sono nascosti dall’interfaccia utente per impostazione predefinita, questo semplifica lo schema nell’Editor di schema e impedisce l’aggiunta di campi indesiderati a dipendenze downstream come il generatore di segmenti, designer di percorsi e così via. Anche il campo obsoleto è compatibile con le versioni precedenti. Altri sistemi che utilizzano campi obsoleti, come segmenti e query, continueranno a valutarli come previsto. Se un campo obsoleto viene utilizzato in un segmento esistente, viene trattato normalmente, il che significa che il campo viene visualizzato come previsto nell’area di lavoro del generatore di segmenti o viene valutato in base ai dati disponibili nei campi obsoleti. Si tratta di una modifica non interrompere che non influisce negativamente sugli eventuali flussi di dati esistenti.

>[!NOTE]
>
>Prima di acquisire i dati in uno schema, è possibile rimuovere i gruppi di campi non necessari. Consulta la documentazione su [come rimuovere un gruppo di campi da uno schema](../ui/resources/schemas.md#remove-fields) per ulteriori informazioni.

Una volta acquisiti i dati nello schema, non è più possibile rimuovere i campi dallo schema senza apportare modifiche di interruzione. In questo caso, puoi deprecare un campo indesiderato all’interno di uno schema o di una risorsa personalizzata utilizzando la [Editor di schema](./create-schema-ui.md) o [API del Registro di sistema dello schema](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

Questo documento illustra come rendere obsoleti i campi per diverse risorse XDM utilizzando l’Editor di schema nell’interfaccia utente di Experience Platform. Per i passaggi sulla deprecazione di un campo XDM utilizzando l’API, consulta l’esercitazione su [deprecazione di un campo XDM tramite l’API del Registro di sistema dello schema](./field-deprecation-api.md).

## Campo obsoleto {#deprecate}

Per rendere obsoleto un campo personalizzato, passare all’Editor di schema per lo schema da modificare. Seleziona il campo da rendere obsoleto dal [!UICONTROL Struttura] sezione dell’area di lavoro, seguita da **[!UICONTROL Obsoleto]** dal [!UICONTROL Proprietà campo].

![Editor schema con un campo selezionato ed evidenziato come obsoleto.](../images/tutorials/field-deprecation/deprecate-single-field.png)

Viene visualizzata una finestra di dialogo per confermare le scelte e informarti che il campo verrà rimosso dalla visualizzazione dell’interfaccia utente dello schema dell’unione e nascosto dalle interfacce utente downstream. Per completare l’azione, seleziona **[!UICONTROL Conferma]**.

![Finestra di dialogo del campo Obsoleto con Conferma evidenziato.](../images/tutorials/field-deprecation/deprecate-field-dialog.png)

Il campo viene ora rimosso dalla visualizzazione dell’interfaccia utente.

>[!NOTE]
>
>Una volta disattivate, le interfacce utente downstream come dashboard di segmentazione, Customer Journey Analytics e Adobe Journey Optimizer non visualizzano più campi obsoleti come parte del loro flusso di lavoro. Tuttavia, le interfacce utente downstream possono mostrare campi obsoleti se necessario e continuare a trattare il campo obsoleto come normale. Per ulteriori informazioni, consulta la relativa documentazione. Le query e i segmenti che utilizzano il campo obsoleto continueranno a essere eseguiti come previsto.

## Mostra campi obsoleti {#show-deprecated}

Per visualizzare i campi precedentemente obsoleti, passare allo schema pertinente nell’Editor di schema. Seleziona la **[!UICONTROL Mostra campi obsoleti]** nella casella di controllo [!UICONTROL Composizione] sezione dell&#39;area di lavoro.

Il campo obsoleto viene ora visualizzato nella visualizzazione dell’interfaccia utente. Seleziona **[!UICONTROL Salva]** per confermare le impostazioni.

![Nell’Editor schema con un campo selezionato, Mostra campi obsoleti e Salva evidenziati.](../images/tutorials/field-deprecation/show-deprecated-fields.png)

## Campi non obsoleti {#undeprecate-fields}

Per annullare un campo obsoleto, prima [visualizzare il campo obsoleto](#show-deprecated) come descritto in precedenza, seleziona il campo obsoleto dall’editor di [!UICONTROL Struttura] sezione . Quindi, seleziona **[!UICONTROL Obsoleto]** dal [!UICONTROL Proprietà campo] barra laterale seguita da **[!UICONTROL Salva]**.

![Editor di schema con campi obsoleti, Non deprecati e Salva evidenziati.](../images/tutorials/field-deprecation/undeprecate-single-field.png)

La [!UICONTROL Campo non deprecato] viene visualizzata la finestra di dialogo . Per confermare le modifiche, seleziona **[!UICONTROL Conferma]**.

![La [!UICONTROL Campo non deprecato] con Conferma evidenziato.](../images/tutorials/field-deprecation/undeprecate-field-dialog.png)

Il campo viene ora visualizzato come standard nella visualizzazione dell’interfaccia utente e anche nelle interfacce a valle. Anche in questo caso, ora puoi rendere obsoleto il campo .

## Passaggi successivi

In questo documento viene illustrato come rendere obsoleti i campi XDM utilizzando l’interfaccia utente dell’Editor di schema. Per ulteriori informazioni sulla configurazione dei campi per le risorse personalizzate, consulta la guida su [definizione dei campi XDM nell’API](./custom-fields-api.md). Per ulteriori informazioni sulla gestione dei descrittori, consulta la sezione [guida all&#39;endpoint dei descrittori](../api/descriptors.md).
