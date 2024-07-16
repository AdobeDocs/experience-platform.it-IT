---
title: Flussi di lavoro basati sui campi nell’Editor di schema
description: Scopri come aggiungere singolarmente i campi dai gruppi di campi esistenti agli schemi Experience Data Model (XDM).
exl-id: 0499ff30-a602-419b-b9d3-2defdd4354a7
source-git-commit: 19e0a26958ec57ccbc614be53b5aaacce7ce9450
workflow-type: tm+mt
source-wordcount: '1301'
ht-degree: 0%

---

# Flussi di lavoro basati sui campi nell’Editor di schema

Adobe Experience Platform fornisce un solido set di [gruppi di campi](../schema/composition.md#field-group) standardizzati da utilizzare negli schemi Experience Data Model (XDM). La struttura e la semantica di questi gruppi di campi sono attentamente personalizzate per soddisfare un’ampia varietà di casi di utilizzo di segmentazione e altre applicazioni a valle in Platform. Puoi anche definire gruppi di campi personalizzati per soddisfare esigenze aziendali specifiche.

Quando aggiungi un gruppo di campi a uno schema, quest’ultimo eredita tutti i campi contenuti in tale gruppo. Tuttavia, ora puoi aggiungere singoli campi allo schema senza dover includere altri campi del gruppo di campi associato che non necessariamente utilizzi.

Questa guida descrive i diversi metodi per aggiungere singoli campi a uno schema nell’interfaccia utente di Platform.

## Prerequisiti

Questa esercitazione presuppone che tu abbia familiarità con la [composizione degli schemi XDM](../schema/composition.md) e con le modalità di utilizzo dell&#39;Editor di schema nell&#39;interfaccia utente di Platform. Per continuare, è necessario avviare il processo di [creazione di un nuovo schema](./resources/schemas.md) e di assegnazione a una classe standard prima di continuare con questa guida.

## Rimuovi i campi aggiunti dai gruppi di campi standard {#remove-field-group}

Dopo aver aggiunto un gruppo di campi standard a uno schema, puoi rimuovere tutti i campi standard non necessari.

>[!NOTE]
>
>La rimozione di campi da un gruppo di campi standard influisce solo sullo schema su cui si lavora e non sul gruppo di campi stesso. Se rimuovi i campi standard in uno schema, tali campi sono ancora disponibili in tutti gli altri schemi che utilizzano lo stesso gruppo di campi.

Nell&#39;esempio seguente, il gruppo di campi standard **[!UICONTROL Dettagli demografici]** è stato aggiunto a uno schema. Per rimuovere un singolo campo, ad esempio `maritalStatus`, selezionare il campo nell&#39;area di lavoro, quindi selezionare **[!UICONTROL Rimuovi]** nella barra a destra.

![Editor schema con il gruppo di campi, il campo Stato civile e la rimozione evidenziati.](../images/ui/field-based-workflows/remove-single-field.png)

Se si desidera rimuovere più campi, è possibile gestire il gruppo di campi nel suo complesso. Seleziona un campo appartenente al gruppo nell&#39;area di lavoro, quindi seleziona **[!UICONTROL Gestisci campi correlati]** nella barra a destra.

![Editor schema con un campo e Gestisci campi correlati evidenziati.](../images/ui/field-based-workflows/manage-related-fields.png)

Viene visualizzata una finestra di dialogo che mostra la struttura del gruppo di campi in questione. Da qui puoi utilizzare le caselle di controllo fornite per selezionare o deselezionare i campi necessari. Al termine, selezionare **[!UICONTROL Conferma]**.

![Finestra di dialogo Gestisci campi correlati con diagramma gruppo campi e conferma evidenziati.](../images/ui/field-based-workflows/select-fields.png)

L’area di lavoro viene nuovamente visualizzata con solo i campi selezionati presenti nella struttura dello schema.

![Editor di schema con il gruppo di campi appena modificato evidenziato.](../images/ui/field-based-workflows/fields-added.png)

## Aggiungere campi standard direttamente a uno schema

Puoi aggiungere campi da gruppi di campi standard direttamente a uno schema, senza dover conoscere in anticipo il gruppo di campi corrispondente. Per aggiungere un campo standard a uno schema, selezionare l&#39;icona più (**+**) accanto al nome dello schema nell&#39;area di lavoro. Nella struttura dello schema viene visualizzato un segnaposto per **[!UICONTROL Campo senza titolo]** e la barra a destra viene aggiornata per visualizzare i controlli per la configurazione del campo.

![Editor schema con segnaposto campo radice evidenziato.](../images/ui/field-based-workflows/root-custom-field.png)

In **[!UICONTROL Nome campo]**, inizia a digitare il nome del campo che desideri aggiungere. Il sistema cerca automaticamente i campi standard corrispondenti alla query e li elenca in **[!UICONTROL Campi standard consigliati]**, inclusi i gruppi di campi a cui appartengono.

![Il nome del campo evidenziato e un elenco dei campi standard consigliati visualizzati nelle proprietà dei campi dell&#39;Editor schema.](../images/ui/field-based-workflows/standard-field-search.png)

Mentre alcuni campi standard condividono lo stesso nome, la loro struttura può variare a seconda del gruppo di campi da cui provengono. Se un campo standard è nidificato all’interno di un oggetto principale nella struttura del gruppo di campi, anche il campo principale verrà incluso nello schema se viene aggiunto il campo secondario.

Selezionare l&#39;icona di anteprima (![icona Anteprima](../images/ui/field-based-workflows/preview-icon.png)) accanto a un campo standard per visualizzare la struttura del relativo gruppo di campi e capire meglio come potrebbe essere nidificato. Per aggiungere il campo standard allo schema, seleziona l&#39;icona più (![Icona più](../images/ui/field-based-workflows/add-icon.png)).

![Icona Aggiungi evidenziata su un elemento dei campi standard suggeriti.](../images/ui/field-based-workflows/add-standard-field.png)

L’area di lavoro viene aggiornata per mostrare il campo standard aggiunto allo schema, inclusi eventuali campi principali nidificati all’interno della struttura del gruppo di campi. Il nome del gruppo di campi è anche elencato in **[!UICONTROL Gruppi di campi]** nella barra a sinistra. Se desideri aggiungere altri campi dallo stesso gruppo di campi, seleziona **[!UICONTROL Gestisci campi correlati]** nella barra a destra.

![Editor schema con il gruppo di campi, il campo standard e i campi correlati Gestisci evidenziati.](../images/ui/field-based-workflows/standard-field-added.png)

## Aggiungere campi personalizzati direttamente a uno schema

Analogamente al flusso di lavoro per i campi standard, puoi anche aggiungere campi personalizzati direttamente a uno schema.

Per aggiungere campi al livello principale di uno schema, seleziona l&#39;icona più (**+**) accanto al nome dello schema nell&#39;area di lavoro. Nella struttura dello schema viene visualizzato un segnaposto per **[!UICONTROL Campo senza titolo]** e la barra a destra viene aggiornata per visualizzare i controlli per la configurazione del campo.

![Editor schema con l&#39;icona di aggiunta e un campo di livello radice senza titolo evidenziato.](../images/ui/field-based-workflows/root-custom-field.png)

Iniziare a digitare il nome del campo che si desidera aggiungere e il sistema avvia automaticamente la ricerca dei campi standard corrispondenti. Per creare un nuovo campo personalizzato, seleziona l&#39;opzione superiore aggiunta con **([!UICONTROL Nuovo campo])**.

![Il nome del campo e il suggerimento Nuovo campo sono evidenziati nelle proprietà del campo dell&#39;Editor schema.](../images/ui/field-based-workflows/custom-field-search.png)

Da qui, fornisci un nome visualizzato e un tipo di dati per il campo. In **[!UICONTROL Assegna gruppo di campi]**, è necessario selezionare un gruppo di campi al quale associare il nuovo campo. Inizia a digitare il nome del gruppo di campi. Se in precedenza hai [creato gruppi di campi personalizzati](./resources/field-groups.md#create), questi verranno visualizzati nell&#39;elenco a discesa. In alternativa, è possibile digitare un nome univoco nel campo per creare un nuovo gruppo di campi.

![Le impostazioni di Nome visualizzato, Tipo e Assegna a proprietà campo sono evidenziate nell&#39;Editor schema.](../images/ui/field-based-workflows/select-field-group.png)

>[!WARNING]
>
>Se si seleziona un gruppo di campi personalizzato esistente, anche gli altri schemi che utilizzano tale gruppo di campi ereditano il campo appena aggiunto dopo il salvataggio delle modifiche. Per questo motivo, selezionare un gruppo di campi esistente solo se si desidera questo tipo di propagazione. In caso contrario, è consigliabile creare un nuovo gruppo di campi personalizzato.

Al termine, selezionare **[!UICONTROL Applica]**.

![L&#39;applicazione è evidenziata nelle proprietà dei campi dell&#39;Editor di schema.](../images/ui/field-based-workflows/apply-field.png)

Il nuovo campo viene aggiunto all&#39;area di lavoro e viene namespace sotto il tuo [ID tenant](../api/getting-started.md#know-your-tenant_id) per evitare conflitti con i campi XDM standard. Il gruppo di campi a cui hai associato il nuovo campo viene visualizzato anche in **[!UICONTROL Gruppi di campi]** nella barra a sinistra.

![L&#39;Editor di schema con il nuovo campo aggiunto all&#39;area di lavoro e namespace sotto l&#39;ID tenant. Il gruppo di campi e il campo sono evidenziati.](../images/ui/field-based-workflows/tenantId.png)

>[!NOTE]
>
>Gli altri campi forniti dal gruppo di campi personalizzato selezionato vengono rimossi dallo schema per impostazione predefinita. Se desideri aggiungere alcuni di questi campi allo schema, seleziona un campo appartenente al gruppo, quindi seleziona **[!UICONTROL Gestisci campi correlati]** nella barra a destra.

### Aggiungere campi personalizzati alla struttura dei gruppi di campi standard

Se lo schema su cui stai lavorando dispone di un campo di tipo oggetto fornito da un gruppo di campi standard, puoi aggiungere campi personalizzati a tale oggetto standard. Selezionare l&#39;icona più (**+**) accanto alla radice dell&#39;oggetto.

>[!IMPORTANT]
>
>Tutti i campi aggiunti a un gruppo di campi in uno schema verranno visualizzati anche in tutti gli altri schemi che utilizzano lo stesso gruppo di campi.

![Editor schema con l&#39;icona più accanto a un oggetto standard evidenziato.](../images/ui/field-based-workflows/add-field-to-standard-object.png)

Per ulteriori informazioni sull&#39;aggiunta di campi personalizzati, vedere [Creare e modificare gli schemi nella guida dell&#39;interfaccia utente](./resources/schemas.md#custom-fields-for-standard-groups).

## Passaggi successivi

Questa guida descrive i nuovi flussi di lavoro basati sui campi per l’Editor di schema nell’interfaccia utente di Platform. Per ulteriori informazioni sulla gestione degli schemi nell&#39;interfaccia utente, vedere [Panoramica dell&#39;interfaccia utente](./overview.md).
