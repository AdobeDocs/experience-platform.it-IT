---
title: Gestire le etichette di utilizzo dati per uno schema
description: Scopri come aggiungere etichette di utilizzo dei dati ai campi dello schema Experience Data Model (XDM) nell’interfaccia utente di Adobe Experience Platform.
exl-id: 92284bf7-f034-46cc-b905-bdfb9fcd608a
source-git-commit: c35c270afca57cb96228cea29fd5a39ec6615332
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 9%

---

# Gestire le etichette di utilizzo dei dati per uno schema

>[!IMPORTANT]
>
>L’etichettatura basata su schema fa parte di [controllo degli accessi basato su attributi](../../access-control/abac/overview.md), attualmente disponibile in versione limitata per i clienti del settore sanitario negli Stati Uniti. Questa funzionalità sarà disponibile per tutti i clienti di Adobe Real-time Customer Data Platform una volta rilasciata completamente.

Tutti i dati inseriti in Adobe Experience Platform sono vincolati dagli schemi Experience Data Model (XDM). Questi dati possono essere soggetti a restrizioni di utilizzo definite dalla tua organizzazione o da normative legali. Per questo motivo, Platform ti consente di limitare l’utilizzo di determinati set di dati e campi tramite l’utilizzo di [etichette di utilizzo dei dati](../../data-governance/labels/overview.md).

Un’etichetta applicata a un campo schema indica i criteri di utilizzo che si applicano ai dati contenuti in quel campo specifico.

Le etichette possono essere applicate a singoli schemi e campi all’interno di tali schemi. Quando le etichette vengono applicate direttamente a uno schema, vengono propagate a tutti i set di dati esistenti e futuri basati su tale schema.

Inoltre, qualsiasi etichetta di campo aggiunta in uno schema si propaga a tutti gli altri schemi che utilizzano lo stesso campo da una classe o un gruppo di campi condiviso. Questo consente di garantire che le regole di utilizzo per campi simili siano coerenti nell’intero modello di dati.

Questo tutorial illustra i passaggi necessari per aggiungere etichette a uno schema utilizzando l’Editor di schema nell’interfaccia utente di Platform.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../home.md): framework standardizzato per l’organizzazione dei dati sull’esperienza del cliente in [!DNL Experience Platform].
   * [Editor schema](../ui/overview.md): scopri come creare e gestire schemi e altre risorse nell’interfaccia utente di Platform.
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md): fornisce l’infrastruttura per applicare le restrizioni di utilizzo dei dati sulle operazioni di Platform, utilizzando criteri che definiscono quali azioni di marketing possono o non possono essere eseguite sui dati con etichetta.

## Selezionare uno schema o un campo a cui aggiungere etichette {#select-schema-field}

>[!CONTEXTUALHELP]
>id="platform_schemas_editgovernancelabels"
>title="Modificare le etichette di governance"
>abstract="Applica un’etichetta a un campo dello schema per indicare i criteri di utilizzo applicati ai dati contenuti in quel campo specifico."

Per iniziare ad aggiungere le etichette, devi prima [seleziona uno schema esistente da modificare](../ui/resources/schemas.md#edit) o [crea un nuovo schema](../ui/resources/schemas.md#create) per visualizzarne la struttura nell&#39;Editor di schema.

Per modificare le etichette di un singolo campo, è possibile selezionare il campo nell&#39;area di lavoro e quindi selezionare **[!UICONTROL Gestisci accesso]** nella barra a destra.

![Seleziona un campo dall’area di lavoro dell’Editor di schema](../images/tutorials/labels/manage-access.png)

È inoltre possibile selezionare **[!UICONTROL Etichette]** , scegli il campo desiderato dall’elenco e seleziona **[!UICONTROL Applica etichette di accesso e governance dei dati]** nella barra a destra.

![Seleziona un campo dal [!UICONTROL Etichette] scheda](../images/tutorials/labels/select-field-on-labels-tab.png)

Per modificare le etichette per l&#39;intero schema, nel **[!UICONTROL Etichette]** , seleziona la casella di controllo sotto l’icona del filtro. In questo modo viene selezionato ogni campo disponibile nello schema. Quindi, seleziona **[!UICONTROL Applica etichette di accesso e governance dei dati]** nella barra a destra.

![Seleziona il nome dello schema da [!UICONTROL Etichette] scheda](../images/tutorials/labels/select-schema-on-labels-tab.png)

>[!NOTE]
>
>Quando si tenta per la prima volta di modificare le etichette di uno schema o di un campo, viene visualizzato un messaggio di liberatoria che spiega in che modo l’utilizzo delle etichette influisce sulle operazioni a valle a seconda dei criteri dell’organizzazione. Seleziona **[!UICONTROL Procedi]** per continuare la modifica.
>
>![Dichiarazione di utilizzo etichetta](../images/tutorials/labels/disclaimer.png)

## Modifica le etichette per lo schema o il campo {#edit-labels}

Viene visualizzata una finestra di dialogo che consente di modificare le etichette per il campo selezionato. Se hai selezionato un singolo campo di tipo oggetto, la barra a destra elenca i sottocampi a cui verranno propagate le etichette applicate.

![Viene evidenziata la finestra di dialogo Applica etichette di accesso e governance dei dati con i campi selezionati.](../images/tutorials/labels/edit-labels.png)

>[!NOTE]
>
>Se stai modificando i campi per l’intero schema, la barra a destra non elenca i campi applicabili e visualizza invece il nome dello schema.

Utilizza l’elenco visualizzato per selezionare le etichette da aggiungere allo schema o al campo. Quando si selezionano le etichette, **[!UICONTROL Etichette applicate]** La sezione viene aggiornata per mostrare le etichette selezionate finora.

![La finestra di dialogo Applica etichette di accesso e governance dei dati con le etichette applicate evidenziate.](../images/tutorials/labels/applied-labels.png)

Per filtrare le etichette visualizzate per tipo, seleziona la categoria desiderata nella barra a sinistra. Per creare una nuova etichetta personalizzata, seleziona **[!UICONTROL Crea etichetta]**.

![La finestra di dialogo Applica etichette di accesso e governance dei dati con un filtro per il tipo di etichetta applicato e l’opzione Crea etichetta evidenziata.](../images/tutorials/labels/filter-and-create-custom.png)

Una volta che sei soddisfatto delle etichette scelte, seleziona **[!UICONTROL Salva]** per applicarli al campo o allo schema.

![La finestra di dialogo Applica etichette di accesso e governance dei dati con Salva è evidenziata.](../images/tutorials/labels/save-labels.png)

Il **[!UICONTROL Etichette]** viene visualizzata di nuovo la scheda con le etichette applicate allo schema.

![La scheda Etichette dell’area di lavoro degli schemi con le etichette dei campi applicate evidenziate.](../images/tutorials/labels/field-labels-added.png)

## Passaggi successivi

Questa guida illustra come gestire le etichette di utilizzo dei dati per schemi e campi. Per informazioni sulla gestione delle etichette di utilizzo dei dati, tra cui come aggiungerle a set di dati specifici anziché a livello di schema, consulta [guida dell’interfaccia utente per le etichette di utilizzo dei dati](../../data-governance/labels/user-guide.md).
