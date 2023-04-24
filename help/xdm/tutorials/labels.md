---
title: Gestire le etichette di utilizzo dei dati per uno schema
description: Scopri come aggiungere etichette per l’utilizzo dei dati ai campi dello schema Experience Data Model (XDM) nell’interfaccia utente di Adobe Experience Platform.
exl-id: 92284bf7-f034-46cc-b905-bdfb9fcd608a
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 3%

---

# Gestione delle etichette di utilizzo dei dati per uno schema

>[!IMPORTANT]
>
>L&#39;etichettatura basata su schema fa parte di [controllo dell&#39;accesso basato sugli attributi](../../access-control/abac/overview.md), attualmente disponibile in una versione limitata per i clienti sanitari negli Stati Uniti. Questa funzionalità sarà disponibile per tutti i clienti Adobe Real-time Customer Data Platform una volta rilasciata.

Tutti i dati inseriti in Adobe Experience Platform sono vincolati dagli schemi Experience Data Model (XDM). Questi dati possono essere soggetti a restrizioni di utilizzo definite dalla tua organizzazione o da normative legali. Per tenere conto di ciò, Platform ti consente di limitare l’utilizzo di determinati set di dati e campi tramite l’utilizzo di [etichette di utilizzo dei dati](../../data-governance/labels/overview.md).

Un’etichetta applicata a un campo dello schema indica i criteri di utilizzo applicati ai dati contenuti in tale campo specifico.

Mentre le etichette possono essere applicate ai singoli set di dati (e ai campi all’interno di tali set di dati), puoi anche applicare etichette a livello di schema. Quando le etichette vengono applicate direttamente a uno schema, vengono propagate a tutti i set di dati esistenti e futuri basati su tale schema.

Inoltre, qualsiasi etichetta di campo aggiunta in uno schema si propaga a tutti gli altri schemi che utilizzano lo stesso campo da una classe o gruppo di campi condivisi. Questo consente di garantire che le regole di utilizzo per campi simili siano coerenti per l’intero modello dati.

Questa esercitazione descrive i passaggi per aggiungere etichette a uno schema utilizzando l’Editor di schema nell’interfaccia utente di Platform.

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../home.md): Il quadro standardizzato [!DNL Experience Platform] organizza i dati sulla customer experience.
   * [Editor di schema](../ui/overview.md): Scopri come creare e gestire schemi e altre risorse nell’interfaccia utente di Platform.
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md): Fornisce l’infrastruttura per applicare restrizioni di utilizzo dei dati sulle operazioni di Platform, utilizzando criteri che definiscono quali azioni di marketing possono (o non possono) essere eseguite sui dati etichettati.

## Selezionare uno schema o un campo a cui aggiungere le etichette {#select-schema-field}

>[!CONTEXTUALHELP]
>id="platform_schemas_editgovernancelabels"
>title="Modificare le etichette di governance"
>abstract="Applica un’etichetta a un campo dello schema per indicare i criteri di utilizzo applicati ai dati contenuti in quel campo specifico."

Per iniziare ad aggiungere etichette, devi prima [selezionare uno schema esistente da modificare](../ui/resources/schemas.md#edit) o [creare un nuovo schema](../ui/resources/schemas.md#create) per visualizzarne la struttura nell’Editor di schema.

Per modificare le etichette di un singolo campo, è possibile selezionare il campo nell’area di lavoro, quindi selezionare **[!UICONTROL Gestisci accesso]** nella barra a destra.

![Selezionare un campo dall’area di lavoro dell’Editor di schema](../images/tutorials/labels/manage-access.png)

Puoi anche selezionare la **[!UICONTROL Etichette]** , scegli il campo desiderato dall’elenco e seleziona **[!UICONTROL Modifica delle etichette di governance]** nella barra a destra.

![Seleziona un campo dal [!UICONTROL Etichette] scheda](../images/tutorials/labels/select-field-on-labels-tab.png)

Per modificare le etichette per l&#39;intero schema, seleziona l&#39;icona a forma di matita (![](../images/tutorials/labels/pencil-icon.png)) accanto al nome dello schema sotto il **[!UICONTROL Etichette]** scheda .

![Seleziona il nome dello schema dal [!UICONTROL Etichette] scheda](../images/tutorials/labels/select-schema-on-labels-tab.png)

>[!NOTE]
>
>Quando si tenta di modificare le etichette di uno schema o di un campo, viene visualizzato un messaggio di esclusione della responsabilità, in cui viene spiegato in che modo l&#39;utilizzo delle etichette influisce sulle operazioni downstream in base ai criteri dell&#39;organizzazione. Seleziona **[!UICONTROL Procedi]** per continuare la modifica.
>
>![Esclusione della responsabilità dall&#39;uso delle etichette](../images/tutorials/labels/disclaimer.png)

## Modificare le etichette per lo schema o il campo

Viene visualizzata una finestra di dialogo che consente di modificare le etichette per il campo selezionato. Se è stato selezionato un singolo campo di tipo oggetto, nella barra a destra sono elencati i campi secondari a cui si propagano le etichette applicate.

![Campi selezionati visualizzati](../images/tutorials/labels/edit-labels.png)

>[!NOTE]
>
>Se si modificano i campi per l’intero schema, la barra a destra non elenca i campi applicabili e visualizza invece il nome dello schema.

Utilizzare l&#39;elenco visualizzato per selezionare le etichette da aggiungere allo schema o al campo. Quando si selezionano le etichette, le **[!UICONTROL Etichette applicate]** la sezione viene aggiornata per mostrare le etichette selezionate finora.

![Etichette applicate visualizzate](../images/tutorials/labels/applied-labels.png)

Per filtrare le etichette visualizzate per tipo, seleziona la categoria desiderata nella barra a sinistra. Per creare una nuova etichetta personalizzata, seleziona **[!UICONTROL Crea etichetta]**.

![Filtrare le etichette visualizzate o creare una nuova etichetta](../images/tutorials/labels/filter-and-create-custom.png)

Una volta soddisfatte le etichette selezionate, seleziona **[!UICONTROL Salva]** per applicarli al campo o allo schema.

![Salva le etichette selezionate](../images/tutorials/labels/save-labels.png)

La **[!UICONTROL Etichette]** viene visualizzata nuovamente la scheda che mostra le etichette applicate per lo schema.

![Etichette campo applicate](../images/tutorials/labels/field-labels-added.png)

## Passaggi successivi

Questa guida illustra come gestire le etichette di utilizzo dei dati per schemi e campi. Per informazioni sulla gestione delle etichette di utilizzo dei dati, tra cui come aggiungerle a set di dati specifici anziché a livello di schema, consulta la sezione [guida all’interfaccia utente delle etichette per l’utilizzo dei dati](../../data-governance/labels/user-guide.md).
