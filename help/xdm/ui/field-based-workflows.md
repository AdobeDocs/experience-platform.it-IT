---
title: Flussi di lavoro basati su campi nell’Editor di schema (Beta)
description: Scopri come aggiungere individualmente i campi dai gruppi di campi esistenti agli schemi Experience Data Model (XDM).
hide: true
hidefromtoc: true
exl-id: 0499ff30-a602-419b-b9d3-2defdd4354a7
source-git-commit: 1d4eba9f566dc1926afd7886c6ad2808ed91ea13
workflow-type: tm+mt
source-wordcount: '1208'
ht-degree: 0%

---

# Flussi di lavoro basati su campi nell’Editor di schema (Beta)

>[!IMPORTANT]
>
>I flussi di lavoro descritti in questo documento beta sono ora generalmente disponibili in Adobe Experience Platform. Per informazioni aggiornate sui flussi di lavoro basati su campi nell’Editor di schema, consulta [Guida all’interfaccia utente per gli schemi](./resources/schemas.md) invece. Questa guida verrà presto rimossa.

Adobe Experience Platform fornisce un solido set di prodotti standardizzati [gruppi di campi](../schema/composition.md#field-group) da utilizzare negli schemi Experience Data Model (XDM). La struttura e la semantica dietro questi gruppi di campi sono accuratamente studiate per soddisfare una vasta gamma di casi d&#39;uso di segmentazione e altre applicazioni a valle in Platform. Puoi anche definire gruppi di campi personalizzati per soddisfare esigenze aziendali specifiche.

Quando si aggiunge un gruppo di campi a uno schema, lo schema eredita tutti i campi contenuti in tale gruppo. Tuttavia, è ora possibile aggiungere singoli campi allo schema senza dover includere altri campi del gruppo di campi associato che non è necessariamente necessario utilizzare.

Questa guida descrive i diversi metodi per aggiungere singoli campi a uno schema nell’interfaccia utente di Platform.

## Prerequisiti

Questa esercitazione presuppone che tu abbia familiarità con [composizione degli schemi XDM](../schema/composition.md) e come utilizzare l’Editor di schema nell’interfaccia utente di Platform. Per seguire, dovresti iniziare il processo di [creazione di un nuovo schema](./resources/schemas.md) e assegnarla a una classe standard prima di continuare con questa guida.

## Rimuovi i campi aggiunti dai gruppi di campi standard

Dopo aver aggiunto un gruppo di campi standard a uno schema, puoi rimuovere tutti i campi standard di cui non hai bisogno.

>[!NOTE]
>
>La rimozione dei campi da un gruppo di campi standard influisce solo sullo schema su cui si lavora e non influisce sul gruppo di campi stesso. Se si rimuovono campi standard in uno schema, tali campi sono ancora disponibili in tutti gli altri schemi che utilizzano lo stesso gruppo di campi.

Nell’esempio seguente, il gruppo di campi standard **[!UICONTROL Dettagli demografici]** è stato aggiunto a uno schema. Per rimuovere un singolo campo, ad esempio `taxId`, seleziona il campo nell’area di lavoro, quindi seleziona **[!UICONTROL Rimuovi]** nella barra a destra.

![Rimuovi campo singolo](../images/ui/field-based-workflows/remove-single-field.png)

Se si desidera rimuovere più campi, è possibile gestire il gruppo di campi nel suo complesso. Seleziona un campo appartenente al gruppo nell’area di lavoro, quindi seleziona **[!UICONTROL Gestire i campi correlati]** nella barra a destra.

![Gestire i campi correlati](../images/ui/field-based-workflows/manage-related-fields.png)

Viene visualizzata una finestra di dialogo che mostra la struttura del gruppo di campi in questione. Da qui è possibile utilizzare le caselle di controllo fornite per selezionare o deselezionare i campi necessari. Quando sei soddisfatto, seleziona **[!UICONTROL Conferma]**.

![Seleziona campi dal gruppo di campi](../images/ui/field-based-workflows/select-fields.png)

L&#39;area di lavoro viene visualizzata nuovamente con solo i campi selezionati presenti nella struttura dello schema.

![Campi aggiunti](../images/ui/field-based-workflows/fields-added.png)

## Aggiungere campi standard direttamente a uno schema

È possibile aggiungere campi dai gruppi di campi standard direttamente a uno schema senza dover prima conoscere il gruppo di campi corrispondente. Per aggiungere un campo standard a uno schema, seleziona il segno più (**+**) accanto al nome dello schema nell’area di lavoro. Un **[!UICONTROL Campo senza titolo]** il segnaposto viene visualizzato nella struttura dello schema e nella barra a destra viene aggiornato per visualizzare i controlli per configurare il campo.

![Segnaposto campo](../images/ui/field-based-workflows/root-custom-field.png)

Sotto **[!UICONTROL Nome campo]**, inizia a digitare il nome del campo da aggiungere. Il sistema cerca automaticamente i campi standard corrispondenti alla query e li elenca in **[!UICONTROL Campi standard consigliati]**, compresi i gruppi di campi a cui appartengono.

![Campi standard consigliati](../images/ui/field-based-workflows/standard-field-search.png)

Anche se alcuni campi standard condividono lo stesso nome, la loro struttura può variare a seconda del gruppo di campi da cui provengono. Se un campo standard è nidificato all’interno di un oggetto principale nella struttura del gruppo di campi, anche il campo principale verrà incluso nello schema se viene aggiunto il campo figlio.

Seleziona l’icona di anteprima (![Icona Anteprima](../images/ui/field-based-workflows/preview-icon.png)) accanto a un campo standard per visualizzare la struttura del relativo gruppo di campi e comprendere meglio come potrebbe essere nidificato. Per aggiungere il campo standard allo schema, seleziona l’icona più (![Icona Plus](../images/ui/field-based-workflows/add-icon.png)).

![Aggiungi campo standard](../images/ui/field-based-workflows/add-standard-field.png)

L’area di lavoro viene aggiornata per mostrare il campo standard aggiunto allo schema, compresi tutti i campi principali nidificati all’interno della struttura del gruppo di campi. Il nome del gruppo di campi è inoltre elencato in **[!UICONTROL Gruppi di campi]** nella barra a sinistra. Se si desidera aggiungere altri campi dallo stesso gruppo di campi, selezionare **[!UICONTROL Gestire i campi correlati]** nella barra a destra.

![Campo standard aggiunto](../images/ui/field-based-workflows/standard-field-added.png)

## Aggiungere campi personalizzati direttamente a uno schema

Analogamente al flusso di lavoro per i campi standard, puoi anche aggiungere campi personalizzati direttamente a uno schema.

Per aggiungere campi al livello principale di uno schema, seleziona il segno più (**+**) accanto al nome dello schema nell’area di lavoro. Un **[!UICONTROL Campo senza titolo]** il segnaposto viene visualizzato nella struttura dello schema e nella barra a destra viene aggiornato per visualizzare i controlli per configurare il campo.

![Campo personalizzato radice](../images/ui/field-based-workflows/root-custom-field.png)

Inizia a digitare il nome del campo che desideri aggiungere e il sistema inizia automaticamente a cercare i campi standard corrispondenti. Per creare un nuovo campo personalizzato, seleziona l’opzione superiore con aggiunta di **([!UICONTROL Nuovo campo])**.

![Nuovo campo](../images/ui/field-based-workflows/custom-field-search.png)

Da qui, fornisci un nome visualizzato e un tipo di dati per il campo. Sotto **[!UICONTROL Assegna gruppo di campi]**, è necessario selezionare un gruppo di campi a cui associare il nuovo campo. Inizia a digitare il nome del gruppo di campi e se in precedenza [gruppi di campi personalizzati creati](./resources/field-groups.md#create) verranno visualizzati nell’elenco a discesa. In alternativa, è possibile digitare un nome univoco nel campo per creare un nuovo gruppo di campi.

![Seleziona gruppo di campi](../images/ui/field-based-workflows/select-field-group.png)

>[!WARNING]
>
>Se selezioni un gruppo di campi personalizzato esistente, anche gli altri schemi che utilizzano quel gruppo di campi erediteranno il campo appena aggiunto dopo il salvataggio delle modifiche. Per questo motivo, selezionare un gruppo di campi esistente solo se si desidera questo tipo di propagazione. In caso contrario, dovresti scegliere di creare un nuovo gruppo di campi personalizzato.

Al termine, seleziona **[!UICONTROL Applica]**.

![Campo Applica](../images/ui/field-based-workflows/apply-field.png)

Il nuovo campo viene aggiunto all’area di lavoro e viene aggiunto con un namespace sotto la [ID tenant](../api/getting-started.md#know-your-tenant_id) per evitare conflitti con i campi XDM standard. In viene visualizzato anche il gruppo di campi a cui è stato associato il nuovo campo. **[!UICONTROL Gruppi di campi]** nella barra a sinistra.

![ID tenant](../images/ui/field-based-workflows/tenantId.png)

>[!NOTE]
>
>Gli altri campi forniti dal gruppo di campi personalizzati selezionato vengono rimossi dallo schema per impostazione predefinita. Se si desidera aggiungere alcuni di questi campi allo schema, selezionare un campo appartenente al gruppo, quindi selezionare **[!UICONTROL Gestire i campi correlati]** nella barra a destra.

### Aggiungere campi personalizzati alla struttura dei gruppi di campi standard

Se lo schema su cui si sta lavorando dispone di un campo di tipo oggetto fornito da un gruppo di campi standard, è possibile aggiungere campi personalizzati a tale oggetto standard. Seleziona il segno più (**+**) accanto alla radice dell’oggetto e fornire i dettagli del campo personalizzato nella barra a destra.

![Aggiungi campo all’oggetto standard](../images/ui/field-based-workflows/add-field-to-standard-object.png)

Dopo aver applicato le modifiche, il nuovo campo viene visualizzato nello spazio dei nomi dell’ID tenant all’interno dell’oggetto standard. Questo spazio dei nomi nidificato evita conflitti tra nomi di campo all’interno del gruppo di campi stesso per evitare l’interruzione delle modifiche in altri schemi che utilizzano lo stesso gruppo di campi.

![Campo aggiunto all’oggetto standard](../images/ui/field-based-workflows/added-to-standard-object.png)

## Passaggi successivi

Questa guida ha trattato i nuovi flussi di lavoro basati su campi per l’Editor di schema nell’interfaccia utente di Platform. Per ulteriori informazioni sulla gestione degli schemi nell’interfaccia utente, consulta [Panoramica dell’interfaccia utente](./overview.md).
