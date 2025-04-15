---
title: Gestire le etichette di utilizzo dati per uno schema
description: Scopri come aggiungere etichette di utilizzo dei dati ai campi dello schema XDM (Experience Data Model) nel interfaccia Adobe Experience Platform.
exl-id: 92284bf7-f034-46cc-b905-bdfb9fcd608a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 8%

---

# Gestire le etichette di utilizzo dei dati per uno schema

Tutti i dati importati in Adobe Experience Platform sono vincolati dagli schemi XDM (Experience Data Model). Questi dati possono essere soggetti a restrizioni di utilizzo definite dalla tua organizzazione o da normative legali. A account tale scopo, il Experience Platform consente di limitare l&#39;utilizzo di determinati set di dati e campi mediante l&#39;uso di etichette](../../data-governance/labels/overview.md) di utilizzo dei [dati.

Un’etichetta applicata a un campo schema indica i criteri di utilizzo che si applicano ai dati contenuti in quel campo specifico.

Le etichette possono essere applicate a singoli schemi e ai campi all’interno di tali schemi. Quando le etichette vengono applicate direttamente a uno schema, vengono propagate a tutti i set di dati esistenti e futuri basati su tale schema.

Inoltre, qualsiasi etichetta di campo aggiunta in uno schema si propaga a tutti gli altri schemi che utilizzano lo stesso campo da una classe o un gruppo di campi condiviso. Questo consente di garantire che le regole di utilizzo per campi simili siano coerenti nell’intero modello di dati.

Questo tutorial illustra i passaggi necessari per aggiungere etichette a uno schema utilizzando l’Editor di schema nell’interfaccia utente di Experience Platform.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../home.md): il framework standardizzato in base al quale [!DNL Experience Platform] organizza esperienza del cliente dati.
   * [Editor schema](../ui/overview.md): Scopri come creare e gestire schemi e altre risorse nel Experience Platform interfaccia.
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md): fornisce l&#39;infrastruttura per applicare restrizioni sull&#39;utilizzo dei dati sulle operazioni Experience Platform, utilizzando criteri che definiscono quali azioni marketing possono (o non possono) essere eseguite sui dati etichettati.

## Selezionare uno schema o un campo a cui aggiungere etichette {#select-schema-field}

>[!CONTEXTUALHELP]
>id="platform_schemas_editgovernancelabels"
>title="Modificare le etichette di governance"
>abstract="Applica un’etichetta a un campo dello schema per indicare i criteri di utilizzo applicati ai dati contenuti in quel campo specifico."

Per iniziare ad aggiungere le etichette, devi prima [selezionare uno schema esistente da modificare](../ui/resources/schemas.md#edit) o [creare un nuovo schema](../ui/resources/schemas.md#create) per visualizzarne la struttura nell&#39;Editor di schema.

Per modificare le etichette di un singolo campo, seleziona il campo nell&#39;area di lavoro, quindi seleziona **[!UICONTROL Gestisci accesso]** nella barra a destra.

>[!IMPORTANT]
>
>È possibile applicare un massimo di 300 etichette a qualsiasi schema.

![Selezionare un campo dall&#39;area di lavoro dell&#39;Editor schema](../images/tutorials/labels/manage-access.png)

Puoi anche selezionare la scheda **[!UICONTROL Etichette]**, scegliere il campo desiderato dall&#39;elenco e selezionare **[!UICONTROL Applica etichette di accesso e governance dei dati]** nella barra a destra.

![Selezionare un campo dalla [!UICONTROL scheda Etichette]](../images/tutorials/labels/select-field-on-labels-tab.png)

Per modificare le etichette per l&#39;intero schema, nella **[!UICONTROL scheda Etichette]** selezionare la casella di controllo sotto l&#39;icona del filtro. In questo modo vengono selezionati tutti i campi disponibili nello schema. Successivo, seleziona **[!UICONTROL Applica Etichette]** di accesso e governance dei dati nel barra giusto.

![Selezionare il nome dello schema dalla [!UICONTROL scheda Etichette]](../images/tutorials/labels/select-schema-on-labels-tab.png)

>[!NOTE]
>
>Quando si tenta per la prima volta di modificare le etichette di uno schema o di un campo, viene visualizzato un messaggio di liberatoria che spiega in che modo l’utilizzo delle etichette influisce sulle operazioni a valle a seconda dei criteri dell’organizzazione. Seleziona **[!UICONTROL Procedi]** per continuare a modificare.
>
>![Dichiarazione di non responsabilità per l&#39;utilizzo dell&#39;etichetta](../images/tutorials/labels/disclaimer.png)

## Modifica le etichette per lo schema o il campo {#edit-labels}

Viene visualizzata una finestra di dialogo che consente di modificare le etichette per il campo selezionato. Se hai selezionato un singolo campo di tipo oggetto, la barra a destra elenca i sottocampi a cui verranno propagate le etichette applicate.

![Finestra di dialogo Applica etichette di accesso e governance dei dati con i campi selezionati evidenziati.](../images/tutorials/labels/edit-labels.png)

>[!NOTE]
>
>Se stai modificando i campi per l’intero schema, la barra a destra non elenca i campi applicabili e visualizza invece il nome dello schema.

Utilizzare l&#39;elenco visualizzato per selezionare le etichette che si desidera aggiungere allo schema o al campo. Man mano che vengono scelte le etichette, la **[!UICONTROL sezione Etichette]** applicate viene aggiornata per mostrare le etichette selezionate finora.

![La finestra di dialogo Applica Etichette per l&#39;accesso e la governance dei dati con le etichette applicate evidenziate.](../images/tutorials/labels/applied-labels.png)

Per filtrare le etichette visualizzate per tipo, selezionare la categoria desiderata nella barra sinistra. Per creare una nuova etichetta personalizzata, selezionare **[!UICONTROL Crea]** etichetta.

![Finestra di dialogo Applica etichette di accesso e governance dei dati con filtro di tipo etichetta applicato ed etichetta Crea evidenziata.](../images/tutorials/labels/filter-and-create-custom.png)

Una volta ottenute le etichette desiderate, selezionare **[!UICONTROL Salva]** per applicarle al campo o allo schema.

![Finestra di dialogo Applica etichette di accesso e governance dei dati con Salva evidenziato.](../images/tutorials/labels/save-labels.png)

Viene visualizzata di nuovo la scheda **[!UICONTROL Etichette]** con le etichette applicate per lo schema.

![Scheda Etichette dell&#39;area di lavoro degli schemi con le etichette dei campi applicate evidenziate.](../images/tutorials/labels/field-labels-added.png)

## Passaggi successivi

Questa guida spiega come gestire le etichette di utilizzo dei dati per schemi e campi. Per informazioni sulla gestione delle etichette di utilizzo dei dati, incluso come aggiungerle a set di dati specifici anziché a livello di schema, vedere la [guida](../../data-governance/labels/user-guide.md) interfaccia alle etichette di utilizzo dei dati.
